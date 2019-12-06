# 推送SDK集成

推送SDK最低兼容iOS 8.0 系统。

> 参考代码：[https://github.com/growingio/GIOiOSDemo](https://github.com/growingio/GIOiOSDemo)  
>   
> GrowingTouchCoreKit.framework触达基础库  
> GrowingTouchCoreUI.bundle UI页面图  
> GrowingPushKit.framework 触达推送库  
> GrowingPushExtensionKit.framework  iOS 10以上统计后台通知的到达率

## 一. 集成SDK

### 1. 集成GrowingIO iOS埋点SDK  \(版本要求最低2.8.7\)

详细集成步骤请参考[ iOS 埋点 SDK 帮助文档](https://docs.growingio.com/docs/developer-manual/sdkintegrated/ios-sdk/manunl-ios-sdk) 。

### 2. 选择集成方式

GrowingPushKit 和 GrowingPushExtensionKit 都需要集成 

**（1）使用CocoaPods快速集成**

* 添加 pod 'GrowingTouch/GrowingPushKit' 以及pod'GrowingTouch/GrowingPushExtensionKit' 到 Podfile 文件中，特别需要注意的是要添加到**不同的 TARGET** 中，如下所示，GIOEdemo 是主工程的 TARGET，而  GIOEdemoServiceExtension 是扩展的 TARGET。

```objectivec
target 'GIOEdemo' do
   pod 'GrowingTouch/GrowingPushKit'
end
```

* **添加扩展 Notification Service Extension** ，在 File -&gt; New -&gt; Target 中选择箭头所指，即可建立扩展GIOEdemoServiceExtension，
  * 请将 Notification Service Extension 中的 Deployment Target 设置为 10.0。

![](../../../.gitbook/assets/image%20%2881%29.png)

  
pod 'GrowingTouch/GrowingPushExtensionKit' 到该扩展 TARGET 的Podfile 文件中，如下所示，GIOEdemo是主工程的 TARGET， GIOEdemoServiceExtension 是扩展的 TARGET，

```objectivec
target 'GIOEdemoServiceExtension' do
  pod 'GrowingTouch/GrowingPushExtensionKit'
end
```

* 执行`pod update`，不要用 `--no-repo-update`选项  确保扩展GrowingPushExtensionKit引入成功，other link flags选项有添加`$(inherited)`

![](../../../.gitbook/assets/image%20%2872%29.png)

 ****另外也要为扩展ServiceExtension注册推送证书 [苹果开发者网站](https://developer.apple.com/)

参考Podfile示例

![](../../../.gitbook/assets/image%20%28101%29.png)

\*\*\*\*

**（2）手动集成SDK**

* 下载最新的iOS GrowingTouch SDK包，并将其中的GrowingTouchCoreKit.framework、GrowingTouchCoreUI.bundle以及GrowingPushKit.framework 添加到iOS工程中。下载链接：[https://github.com/growingio/GrowingSDK-iOS-GrowingTouchCoreKit/archive/master.zip](https://github.com/growingio/GrowingSDK-iOS-GrowingTouchCoreKit/archive/master.zip)

  选项如下图所示。

![](../../../.gitbook/assets/image%20%28124%29.png)



* **添加扩展 Notification Service Extension** ，在 File -&gt; New -&gt; Target 中选择箭头所指，即可建立扩展GIOEdemoServiceExtension，
  * 请将 Notification Service Extension 中的 Deployment Target 设置为 10.0。

![](../../../.gitbook/assets/image%20%2881%29.png)

* 将其中的**GrowingPushExtensionKit.framework**包将之添到扩展**Notification Service Extension**\(创建见注意事项3\)中， 选项如下图所示。下载链接：

  [https://github.com/growingio/GrowingSDK-iOS-GrowingTouchCoreKit/archive/master.zip](https://github.com/growingio/GrowingSDK-iOS-GrowingTouchCoreKit/archive/master.zip)

![](../../../.gitbook/assets/image%20%2852%29.png)



* 添加编译参数，并注意大小写：

![](../../../.gitbook/assets/image%20%2891%29.png)



请保证扩展的target  最低版本 iOS10.0  


![](../../../.gitbook/assets/image%20%2811%29.png)

## 二. 重要配置

### **1. 推送设备的deviceToken上传**

用户自行实现通知注册请求授权后，在 AppDelegate 的 deviceToken 代理方法中调用API，传入获取到的 deviceToken，请确保能获取 deviceToken，否则无法接收通知消息。

```swift
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
    [GrowingTouch registerDeviceToken:deviceToken];
}
```

通知注册请求授权码可参考如下：

```swift
- (void)registerRemoteNotification {
    if (@available(iOS 10,*)) {
        UNUserNotificationCenter *center = [UNUserNotificationCenter currentNotificationCenter];
        center.delegate = self;
        [center requestAuthorizationWithOptions:(UNAuthorizationOptionAlert | UNAuthorizationOptionSound )
                              completionHandler:^(BOOL granted, NSError * _Nullable error) {
                                  if (granted) {
                 dispatch_async(dispatch_get_main_queue(), ^{         
                                          [[UIApplication sharedApplication] registerForRemoteNotifications];
                                      });
                                  }
                              }];
    } else if ([[UIApplication sharedApplication] respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        UIUserNotificationType type =  UIUserNotificationTypeAlert | UIUserNotificationTypeBadge | UIUserNotificationTypeSound;
        UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:type
categories:nil];
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
    }
}
```

### 2. **Notification Service Extension**扩展的后台通知回执接口调用 sendNotificationRequest:request withCompletionHandler:

在 iOS10 提供的扩展 Notification Extension Service 中通知接收方法中调用通知消息回执接口，代码示例如下：\(**注意不是写在AppDelegate中,是写在你新建的扩展里面**\)



```swift
- (void)didReceiveNotificationRequest:(UNNotificationRequest *)request withContentHandler:(void (^)(UNNotificationContent * _Nonnull))contentHandler {
    self.contentHandler = contentHandler;
    self.bestAttemptContent = [request.content mutableCopy];
 
    [GrowingPushExtensionKit sendNotificationRequest:request withCompletionHandler:^(NSError* error) {
        //  修改通知消息
        self.contentHandler(self.bestAttemptContent);
    }];
}
```

### 示例如下

![](../../../.gitbook/assets/image%20%2854%29.png)

### 3. 推送消息的处理 clickMessageWithCompletionHandler:

推送功能默认提供打开APP、打开网页、打开APP内部页面三种功能，如果该三种功能还是满足不了您的需求，您可以在SDK提供的以下方法回调中自定义自己的跳转逻辑。

```swift
//  点击消息跳转用户自定义
+ (void)clickMessageWithCompletionHandler:(void (^)(NSDictionary *params))completionHandler;
```

## **三.注意事项**

由于iOS的远程推送通知在各个版本上有一定的改动，为了统计数据更加准确，需要针对不同的系统分别做相应的处理

### **1. iOS 10以下的系统**

针对 Remote Notifications 系统提供了以下2个通知接收方法，如果您的应用支持iOS 10 以下的系统，请至少实现如下2个方法中的任意一个，建议实现方法2

```swift
//  1、早期的方法，iOS 10 以后废弃，依然可以使用
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo NS_DEPRECATED_IOS(3_0, 10_0）；

//  2、上述方法的替代方法
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))completionHandler NS_AVAILABLE_IOS(7_0)；
```

### **2. iOS 10及以上系统**

对于iOS 10 及以上的系统，请通过 **UNUserNotificationCenter** 请求通知授权并设置代理，并同时实现如下2个通知代理接收方法

```swift
- (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler；

- (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)(void))completionHandler ;
```

### **3. 如何在当前项目中添加**Notification Service Extension

针对 iOS 10.0 以上的系统，为了能准确统计后台通知的到达率，可添加 **Notification Service Extension** 类型的 target ，调用指定的 API，具体参见“重要配置”中的第2条，在当前项目中添加 **Notification Service Extension** 步骤如下：

在 File -&gt; New -&gt; Target 中选择箭头所指，即可建立

![](../../../.gitbook/assets/image%20%2849%29.png)

## 四. 常见问题

### 1. 推送跳转App原生界面

特别需要注意以下两点：

（1）如果点击跳转的原生界面是通过Objective-C开发的控制器，例如控制器名称为 InAppViewController ，传递参数为key1、key2，则推送Web 页面配置如下：

* **推送Web页面配置如下：**

![](../../../.gitbook/assets/image%20%2892%29.png)

此时生成的跳转链接为`InAppViewController?key1=value1&key2=value2` ，点击自动跳转到原生界面InAppViewController，并携带两个参数。

在InAppViewController可以通过提前定义属性，获取参数

```swift
@interface InAppViewController : UIViewController
@property (nonatomic, copy) NSString *key1;
@property (nonatomic, copy) NSString *key2;
@end
```

（2）如果跳转的原生界面是通过swift开发的控制器，需要按照以下步骤进行接入。

例如跳转的原生界面是SFViewController.swift，示例项目工程为 TestDemo，在SFViewController.swift中可以通过提前定义属性，用于获取参数

```swift
class SFViewController: UIViewController {
    @objc var key1: String?
    @objc var key2: String?
    override func viewDidLoad() {
        super.viewDidLoad()  
        // Do any additional setup after loading the view.
    }
}
```

第1步：编译运行当前示例项目工程TestDemo（实际过程中应为对应的项目工程名称）

![](../../../.gitbook/assets/image%20%2897%29.png)

第2步：运行成功之后，在Products文件夹下，选中 TestDemo.app 后 Show in Finder

![](../../../.gitbook/assets/image%20%287%29.png)

第3步：可以看到在Products文件夹同级补录下，有一个名为Intermediates.noindex 的文件夹，依次进入 TestDemo.build -&gt; Debug-iphoneos\(或Debug-iphonesimulator\) -&gt; TestDemo.build -&gt; DerivedSources 文件夹下

![](../../../.gitbook/assets/image%20%2885%29.png)

![](../../../.gitbook/assets/image%20%2876%29.png)

第4步：当前文件下有一个名为 TestDemo-Swift.h 的文件，双击打开在该文件中查找 SFViewController，发现该类声明的上方有一句 SWIFT\_CLASS\("\_TtC8TestDemo16SFViewController"\)

![](../../../.gitbook/assets/image%20%2898%29.png)

\_TtC8TestDemo16SFViewController 即为原生界面SFViewController.swift转换后的类名， Web 页面配置如下：

**推送Web页面配置如下：**

![](../../../.gitbook/assets/image%20%28106%29.png)

## 五. 如何判断iOS push集成成功

1.扫码测试推送成功挑战对应页面跳转，代表GrowingPushKit集成成功  
2.app完全退出后，收到推送时，未打开app时就可以在charles抓包工具能看到埋点请求api.growingio.com ，代表GrowingPushExtensionKit集成成功  


