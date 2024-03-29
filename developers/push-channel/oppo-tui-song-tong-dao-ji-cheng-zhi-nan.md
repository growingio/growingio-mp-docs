---
description: OPPO推送通道是由OPPO官方提供的系统级推送通道。在OPPO手机上，推送消息能够通过OPPO的系统通道抵达终端，并且无需打开应用就能够收到推送。
---

# OPPO推送通道集成指南

### 1. 获取OPPO推送密钥

1.打开[OPPO推送平台](https://push.oppo.com/)。

2.注册/登录开发者账号。

3.在[OPPO推送平台](https://push.oppo.com/) 中新建应用。注意「应用包名」需跟您在GrowingIO推送填写的包名保持一致。

{% hint style="info" %}
注: 更多详情请参照[OPPO开发文档](https://push.oppo.com/documents)。
{% endhint %}

### 2. 创建通道

参考[OPPO推送平台开发文档](https://open.oppomobile.com/wiki/doc#id=10289),对于target API≥ 26\(Android 8.0\)的应用，必须适配通知通道，未指定通道的情况下发出的通知将无法显示。

请按照下图配置channel。

![](../../.gitbook/assets/111.png)

channel的内容如下：请不要随意改动

```text
// 需要填写的地方可以复制下方内容
分组ID: GPUSH_GROUP_ID
分组名称:推送消息
通道ID:GPUSH_CHANNEL_ID
通道名称:标准推送消息
消息用途:标准推送消息
```

![](../../.gitbook/assets/222.png)

### 3. 在app build.gradle添加OPPO通道SDK依赖

```java
dependencies {
    ...
    //由于推送底层网络库依赖OkHttp3网络库，请添加OkHttp3依赖
    implementation 'com.squareup.okhttp3:okhttp:3.12.1'
    //推送SDK依赖
    implementation 'com.growingio.android:gtouch:$gtouch_version'
    //OPPO推送SDK依赖 
    implementation 'com.growingio.android.gpush:gpush-oppo-adapter:$gtouch_version'
    
}
```

> $gtouch\_version 为最新SDK版本号，现最新的版本号为请参考[SDK更新日志](../integrations/changelog.md)。

### 4. 在app build.gradle配置AppID, AppKey和AppSecret

```java
android {
        ......
        defaultConfig {
            manifestPlaceholders = [
                PACKAGE_NAME          : "您的APP包名",

                GPUSH_OPPO_APP_ID     : "OPPO推送的AppId",
                GPUSH_OPPO_APP_KEY    : "OPPO推送的AppKey",
                GPUSH_OPPO_APP_SECRET : "OPPO推送的AppSecret",
            ]
            ......
        }
        ......
```

### 5. 代码混淆

```java
-keep public class * extends android.app.Service
```

### 6. 配置服务端AppID和**MasterSecrect**

![](../../.gitbook/assets/image%20%2826%29.png)

MasterSecret在这里找

![](../../.gitbook/assets/image%20%28189%29.png)

### 7. 厂商通道测试方法\(通用\)

1. 将集成好的App（测试版本）安装在一台OPPO测试机上，并且运行App。
2. 保持App在前台运行，尝试扫码测试推送消息。
3. 如果应用收到消息，将App退到后台，并且杀掉所有App进程。
4. 再次进行测试推送消息，如果能够收到推送，则表明厂商通道集成成功。

### 8 兼容性

如果您的App已经集成了个推VIP或极光VIP版本的推送SDK，我们的Android SDK也能兼容。

为了和个推兼容，我们将厂商通道独立打包。OPPO推送通道为例，我们打包两个SDK：gpush-oppo-adapter和gpush-oppo-sdk。如果是从未接过个推、极光等VIP版本的用户可以直接添加OPPO推送通道依赖。

```java
implementation 'com.growingio.android.gpush:gpush-oppo-adapter:$ersion'
```

如果是个推、极光等VIP版本的用户可以将OPPO官方SDK包gpush-oppo-sdk 排除出去。

```java
implementation ('com.growingio.android.gpush:gpush-oppo-adapter:$gtouch_version'){
      exclude(group: 'com.growingio.android.gpush' , module: 'gpush-oppo-sdk')
}
```



