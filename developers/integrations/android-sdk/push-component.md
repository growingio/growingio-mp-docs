# 推送SDK集成

{% hint style="info" %}
最低兼Android版本4.2 API 17
{% endhint %}

触达SDK会根据运营人员对用户的分组情况，下发弹窗和推送消息。

## 一. 集成SDK

### 1. 集成GrowingIO Android无埋点SDK

添加触达 SDK前请确保您已经集成了我们公司的无埋点 SDK，版本需要在 2.6.9 及以上，详细情况请移步[Android无埋点SDK帮助文档](https://docs.growingio.com/docs/sdk-integration/android-sdk/android-sdk)。最低兼容的 Android 版本为 4.2 。

### 2. 添加依赖

#### 2.1 在project级别的build.gradle的allprojects-&gt;repositories添加华为推送SDK的maven仓库

{% hint style="info" %}
如果没有开通华为推送通道可以不用添加该仓库，跳过该步骤。
{% endhint %}

```swift
allprojects {    repositories {        google()        jcenter()        mavenLocal()        // 华为仓库        maven { url 'http://developer.huawei.com/repo/' }    }}
```

#### 2.2 在module级别的build.gradle添加SDK依赖

```swift
dependencies {    ...    //由于触达底层网络库依赖OkHttp3网络库，请添加OkHttp3依赖    implementation "com.squareup.okhttp3:okhttp:3.12.1"    //触达SDK依赖    implementation "com.growingio.android:gtouch:$gtouch_version"    //华为推送SDK依赖，如果没有开通华为推送通道可以不用添加该依赖    implementation "com.growingio.android.gpush:gpush-huawei-adapter:$gtouch_version"    //魅族推送SDK依赖，如果没有开通魅族推送通道可以不用添加该依赖    implementation "com.growingio.android.gpush:gpush-meizu-adapter:$gtouch_version"    //小米推送SDK依赖，如果没有开通小米推送通道可以不用添加该依赖    implementation "com.growingio.android.gpush:gpush-xiaomi-adapter:$gtouch_version"}
```

> $gtouch\_version 为触达SDK版本号，现最新的版本号为请参考[SDK更新日志](../changelog.md)。

### 3. 配置AppID和App**K**ey

在module级别的build.gradle里配置AppID和AppKey。

根据您APP的实际情况配置不同厂家渠道

```swift
android {        ......        defaultConfig {            manifestPlaceholders = [                PACKAGE_NAME        : "您的APP包名",                GPUSH_XIAOMI_APP_ID : "小米推送的AppId",                GPUSH_XIAOMI_APP_KEY: "小米推送的AppKey",                GPUSH_HUAWEI_APP_ID : "华为推送的AppId(华为推送不需要AppKey)",                GPUSH_MEIZU_APP_ID  : "魅族推送的AppId",                GPUSH_MEIZU_APP_KEY : "魅族推送的AppKey",            ]            ......        }        ......}
```

### 4.添加权限

集成推送SDK需在AndroidManifest.xml 中添以下权限

```swift
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" /><uses-permission android:name="android.permission.READ_PHONE_STATE" /> <uses-permission android:name="android.permission.GET_TASKS" /> <uses-permission android:name="android.permission.VIBRATE"/> 
```

### 5. 初始化SDK

请将以下`GrowingTouch.startWithConfig`加在您的Application 的 `onCreate` 方法中，且保证在无埋点SDK初始化代码`GrowingIO.startWithConfiguration`后

```swift
public class MyApplication extends Application {​    @Override    public void onCreate() {        super.onCreate();        GrowingIO.startWithConfiguration(this, new Configuration()            .trackAllFragments()            .setChannel("XXX应用商店")            );        GrowingTouch.startWithConfig(this, new GTouchConfig()             .setPushEnable(true)             .setDebugEnable(BuildConfig.DEBUG)             );    }}
```

### 6. 代码混淆

如果您启用了代码混淆，请务必在您的proguard-rules.pro文件里加入下面的代码：

```swift
#GrowingIO-keep class com.growingio.** {    *;}-dontwarn com.growingio.**-keepnames class * extends android.view.View-keepnames class * extends android.app.Fragment-keepnames class * extends android.support.v4.app.Fragment-keepnames class * extends androidx.fragment.app.Fragment-keep class android.support.v4.view.ViewPager{    *;}-keep class android.support.v4.view.ViewPager$**{	*;}-keep class androidx.viewpager.widget.ViewPager{    *;}-keep class androidx.viewpager.widget.ViewPager$**{	*;}#okhttp-dontwarn okhttp3.**-keep class okhttp3.**{*;}#okio-dontwarn okio.**-keep class okio.**{*;}#Xiaomi Push-dontwarn com.xiaomi.**-keep class com.xiaomi.**{*;}-keep public class * extends com.xiaomi.mipush.sdk.PushMessageReceiver#Huawei Push-ignorewarning-keepattributes *Annotation*-keepattributes Exceptions-keepattributes InnerClasses-keepattributes Signature-keepattributes SourceFile,LineNumberTable-keep class com.hianalytics.android.**{*;}-keep class com.huawei.updatesdk.**{*;}-keep class com.huawei.hms.**{*;}-keep class com.huawei.android.hms.agent.**{*;}#Meizu Push-dontwarn com.meizu.cloud.pushsdk.**-keep class com.meizu.cloud.pushsdk.**{*;}
```

## 二. 重要配置

### **1. 设置触达推送开关** setPushEnable

设置触达推送消息的开关

```swift
setPushEnable(boolean pushEnable)
```

**参数说明**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>&#x53C2;&#x6570;&#x540D;</b>
      </th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x5FC5;&#x586B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">enable</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">
        <p>&#x5F00;&#x5173;&#x89E6;&#x8FBE;&#x63A8;&#x9001;&#x529F;&#x80FD;</p>
        <ul>
          <li>true&#x5F00;&#x542F;</li>
          <li>false&#x5173;&#x95ED;</li>
        </ul>
        <p>&#x9ED8;&#x8BA4;&#x4E3A;true</p>
      </td>
    </tr>
  </tbody>
</table>**代码示例**

```swift
GrowingTouch.startWithConfig(this, new GTouchConfig()                .setPushEnable(true)                ...                );
```

### **2. 设Debug模式**（只在调试时使用，上线请务必关闭） **setDebugEnable**

查看数据采集发送日志，能够在Android Studio中通过Logcat查看GrowingTouch打印的数据发送日志，在 APP 的 Application onCreate 初始化SDK地方添加配置。

```swift
setDebugEnable(boolean debugEnable)
```

**参数说明**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>&#x53C2;&#x6570;&#x540D;</b>
      </th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x5FC5;&#x586B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">debugEnable</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">
        <p>&#x5F00;&#x542F;&#x89E6;&#x8FBE;&#x65E5;&#x5FD7;</p>
        <ul>
          <li>true&#x5F00;&#x542F;</li>
          <li>false&#x5173;&#x95ED;</li>
        </ul>
        <p>&#x9ED8;&#x8BA4;false</p>
      </td>
    </tr>
  </tbody>
</table>**代码示例**

```swift
GrowingTouch.startWithConfig(this, new GTouchConfig()                //BuildConfig.DEBUG 这样配置就不会上线忘记关闭                .setDebugEnable(BuildConfig.DEBUG)                ...                );
```

### **3.** 推送消息的自定义处理

触达推送功能默认提供 **打开APP、打开网页、打开APP内部页面** 三种功能，如果这三种功能还是满足不了您的需求，可以自定义一个**BroadcastReceiver**类，用于自定义处理各种消息的响应。例如自定义的BroadcastReceiver

```swift
public class PushMessageReceiver extends GPushMessageReceiver {    private static final String TAG = "PushMessageReceiver";    /**     * 推送注册成功     *      * @param context BroadcastReceiver的onReceive回调中的Context对象     * @param channel 推送通道，如华为、小米等     * @param pushToken 注册的推送Token     */    @Override    public void onRegister(Context context, PushChannel channel, String pushToken) {        Log.e(TAG, "onRegister: channel = " + channel.getChannelName() + ", pushToken = " + pushToken);    }    /**     * 推送注销成功     *     * @param context BroadcastReceiver的onReceive回调中的Context对象     */    @Override    public void onUnregister(Context context) {        Log.e(TAG, "onUnregister: ");    }    /**     * 推送消息被点击     *      * @param context BroadcastReceiver的onReceive回调中的Context对象     * @param pushMessage 推送的消息体     */    @Override    public void onNotificationMessageClicked(Context context, GPushMessage pushMessage) {        Log.e(TAG, "onNotificationMessageClicked: " + pushMessage.toString());    }}
```

将自定义的BroadcastReceiver注册到AndroidManifest.xml文件中

```swift
<receiver    android:name="您的包名.PushMessageReceiver"    android:enabled="true">    <intent-filter>        <action android:name="com.growingio.push.intent.action.MESSAGE" />    </intent-filter></receiver>
```

### 4. 设置触达SDK异常上传开关 setUploadExceptionEnable

触达SDK会收集SDK内部异常上报服务端，方便开发更好的追踪触达SDK的问题，和完善触达SDK的功能。如果您不想帮助我们触达产品完善功能，或者和您的crash收集框架有冲突，您可以选择关闭此功能。

```swift
setUploadExceptionEnable(boolean uploadExceptionEnable)
```

**参数说明**

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>&#x53C2;&#x6570;&#x540D;</b>
      </th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x5FC5;&#x586B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">uploadExceptionEnable</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">
        <p>&#x5F00;&#x5173;SDK&#x5F02;&#x5E38;&#x4E0A;&#x4F20;&#x529F;&#x80FD;</p>
        <ul>
          <li>true&#x5F00;&#x542F;</li>
          <li>false&#x5173;&#x95ED;</li>
        </ul>
        <p>&#x9ED8;&#x8BA4;&#x503C;true</p>
      </td>
    </tr>
  </tbody>
</table>**代码示例**

```swift
 GrowingTouch.startWithConfig(this, new GTouchConfig()                .setUploadExceptionEnable(true)                ...                );
```

## 三. API介绍\( GrowingTouch.class \)

### 1. void registerPush\(\)

注册消息推送功能

### 2. void unRegisterPush\(\)

注销消息推送功能

## 四. 其他

### 1. 推送消息跳转原生Activity界面

若触达推送跳转链接为 GInApp://com.growingio.gtouch.InAppPageActivity?key1=value1&key2=value2 那么会打开原生界面 InAppPageActivity，并携带两个参数。

对应的推送页面配置如下图所示：

其中「自定义参数」意思是输入任何您自己的scheme（自定义协议），

比如： myapp://productdetails/itemabc ，然后在onclick事件回调中解析出来就行了

* **推送Web页面配置截图如下：**

![](../../../.gitbook/assets/image%20%2811%29.png)

在InAppPageActivity可以通过intent获取参数

```swift
@Overrideprotected void onCreate(Bundle savedInstanceState) {    super.onCreate(savedInstanceState);    setContentView(R.layout.activity_in_app_page);    Intent intent = getIntent();    Log.e(TAG, "onCreate: key1 = " + intent.getStringExtra("key1"));    Log.e(TAG, "onCreate: key2 = " + intent.getStringExtra("key2"));}
```

### 2. okhttp 版本要求

需要升级到3.12.1，触达使用了新版的方法，否则会报错。

### 3. 集成推送后,原有应用将变为多进程应用

请注意规避类似如下问题

* Android9.0 禁止多个进程共享同一个WebView数据目录,参见[https://developer.android.google.cn/about/versions/pie/android-9.0-changes-28\#framework-security-changes](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-28#framework-security-changes)











