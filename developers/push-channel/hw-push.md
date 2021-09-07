---
description: 华为推送通道是由华为官方提供的系统级推送通道。在华为手机上，推送消息能够通过华为的系统通道抵达终端，并且无需打开应用就能够收到推送。
---

# 华为推送通道集成指南

{% hint style="info" %}
* 华为推送只有在**签名发布包环境**下才可以收到推送消息
* 华为手机中的**移动推送服务**，必须升级到 2.5.3 以上版本
{% endhint %}

### 1. 获取华为推送秘钥

1. 访问 [华为开放平台](http://developer.huawei.com/)。
2. 注册/登录开发者账号。（如果您是新注册账号，需进行实名认证）.
3. 在华为推送平台中新建应用。注意：应用包名需跟您在GIO集成的包名保持一致

### 2. **在project 的 build.gradle 添加华为推送SDK的maven仓库地址**

```java
buildscript {
...
    repositories {
        google()
        jcenter()
        // sdk1.5.0版本开始迁移到了Maven Central
        mavenCentral()
        // 华为仓库
        maven { url 'http://developer.huawei.com/repo/' }
    }
    
    buildscript {
       dependencies {
           ...
           classpath 'com.huawei.agconnect:agcp:1.3.1.300'
       }
   }
...
}

allprojects {
...
    repositories {
        google()
        jcenter()
        // sdk1.5.0版本开始迁移到了Maven Central
        mavenCentral()
        // 华为仓库
        maven { url 'http://developer.huawei.com/repo/' }
    }
...
}
```

### 3. 在app build.gradle添加华为通道SDK依赖

```java
dependencies {
    ...
    //由于推送底层网络库依赖OkHttp3网络库，请添加OkHttp3依赖
    implementation 'com.squareup.okhttp3:okhttp:3.12.1'
    //推送SDK依赖
    implementation 'com.growingio.android:gtouch:$gtouch_version'
    //华为推送SDK依赖
    implementation 'com.growingio.android.gpush:gpush-huawei-adapter:$gtouch_version'
}
```

> $gtouch\_version 为最新SDK版本号，现最新的版本号为请参考[SDK更新日志](../integrations/changelog.md)。

### 4. 对接华为官方推送服务

根据[华为](https://developer.huawei.com/consumer/cn/hms/huawei-pushkit/)官方文档集成华为推送

1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，点击“我的项目”。
2. 在项目列表中找到您的项目，在项目中点击需要集成HMS Core SDK的应用。
3. 在“项目设置 &gt; 常规”页面的“应用”区域，点击“agconnect-services.json”下载配置文件。
4. 将“agconnect-services.json”文件拷贝到应用级根目录下。
5. 在app的 build.gradle文件添加

```text
apply plugin: 'com.huawei.agconnect'
```

![](../../.gitbook/assets/image%20%28278%29.png)

### ![](https://communityfile-drcn.op.hicloud.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20200918164206.94553315565562037073638607969959:50510918092852:2800:B5FA3DE2A53C2A9E17109F45EC3CEE32AF9838E495E6D786F9415DC9C6DF72AC.png?needInitFileName=true?needInitFileName=true)

### 5. 配置AppID

```java
android {
        ......
        defaultConfig {
            manifestPlaceholders = [
                PACKAGE_NAME        : "您的APP包名",

                GPUSH_HUAWEI_APP_ID : "华为推送的AppId(华为推送不需要AppKey)",
            ]
            ......
        }
        ......
}
```

### 6. 代码混淆

```java
-ignorewarning

-keepattributes *Annotation*

-keepattributes Exceptions

-keepattributes InnerClasses

-keepattributes Signature

-keepattributes SourceFile,LineNumberTable

-keep class com.hianalytics.android.**{*;}

-keep class com.huawei.updatesdk.**{*;}

-keep class com.huawei.hms.**{*;}

-keep class com.huawei.android.hms.agent.**{*;}
```

### 7. 配置服务端AppID和AppSecret

![](../../.gitbook/assets/image%20%2820%29.png)

### 8. 设置推送消息回执

在华为推送APP编辑界面配置回执，以便于我们GrowingIO更好的统计推送数据

![](../../.gitbook/assets/2%20%281%29.png)

{% hint style="info" %}
目前单击【测试回执】，会提示“https，error"，请忽略并直接单击【提交】。
{% endhint %}

其中回调地址

```java
https://messages.growingio.com/v1/callback/huawei
```

HTTPS证书

```text
-----BEGIN CERTIFICATE-----
MIIGOjCCBSKgAwIBAgIRALgnuZWCR+iOD4izy+ml7dgwDQYJKoZIhvcNAQELBQAw
gY8xCzAJBgNVBAYTAkdCMRswGQYDVQQIExJHcmVhdGVyIE1hbmNoZXN0ZXIxEDAO
BgNVBAcTB1NhbGZvcmQxGDAWBgNVBAoTD1NlY3RpZ28gTGltaXRlZDE3MDUGA1UE
AxMuU2VjdGlnbyBSU0EgRG9tYWluIFZhbGlkYXRpb24gU2VjdXJlIFNlcnZlciBD
QTAeFw0yMTA4MjYwMDAwMDBaFw0yMjA5MjMyMzU5NTlaMBoxGDAWBgNVBAMMDyou
Z3Jvd2luZ2lvLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAJQN
pLFM9rXcbQ0uvJBArJza9p7U9noR9O+DXguaHNMWp1kAQN45ZoVV5t3iqdPc6WaH
iUFRnAysDKs8Gdx6ArN2SDaekE119ywbZAkZNfwSESyXKND1cPBgu7AIcnwRwpTv
u946MIlQ2YDy/sVe2E9xNdCxtzfBsFCcBGdTUmiczjyowOvtdxWm9r7DDUAm5vFK
BZIqy5POXkAe4hTYb5m6VFHaZL+dXm02zZhbzFy8Rqlq9XK5N1WqQ9vDHkrS3v5H
6xsoE9QU52AvzBAdSiWjpM3LWijgWiEoRKL1HpfvYFiSZlqkVex/N3tewmLdOUSf
LG3DuyRCMqK9THRtqVkCAwEAAaOCAwMwggL/MB8GA1UdIwQYMBaAFI2MXsRUrYrh
d+mb+ZsF4bgBjWHhMB0GA1UdDgQWBBR8tPS9uoCpclkI17VYyWVHv1evKDAOBgNV
HQ8BAf8EBAMCBaAwDAYDVR0TAQH/BAIwADAdBgNVHSUEFjAUBggrBgEFBQcDAQYI
KwYBBQUHAwIwSQYDVR0gBEIwQDA0BgsrBgEEAbIxAQICBzAlMCMGCCsGAQUFBwIB
FhdodHRwczovL3NlY3RpZ28uY29tL0NQUzAIBgZngQwBAgEwgYQGCCsGAQUFBwEB
BHgwdjBPBggrBgEFBQcwAoZDaHR0cDovL2NydC5zZWN0aWdvLmNvbS9TZWN0aWdv
UlNBRG9tYWluVmFsaWRhdGlvblNlY3VyZVNlcnZlckNBLmNydDAjBggrBgEFBQcw
AYYXaHR0cDovL29jc3Auc2VjdGlnby5jb20wKQYDVR0RBCIwIIIPKi5ncm93aW5n
aW8uY29tgg1ncm93aW5naW8uY29tMIIBgQYKKwYBBAHWeQIEAgSCAXEEggFtAWsA
dwBGpVXrdfqRIDC1oolp9PN9ESxBdL79SbiFq/L8cP5tRwAAAXuA2OUoAAAEAwBI
MEYCIQDUPM7fUKfkZmuxIzjBUL3r1JJIMuxveatejFBqKLh85gIhAOHG0frydQMh
XraIwZ5wTd4K30nJAn28V6+2ohtW9LBzAHcAQcjKsd8iRkoQxqE6CUKHXk4xixsD
6+tLx2jwkGKWBvYAAAF7gNjk8gAABAMASDBGAiEA1lR2Nu6ERx8l3N4qIDUFJJ45
UEy6JJU52JdeZnmru5kCIQDV77MfJgDf+moLxQaQMHhGZlGcIHt7a2Bq1COoRwPK
aAB3ACl5vvCeOTkh8FZzn2Old+W+V32cYAr4+U1dJlwlXceEAAABe4DY5MUAAAQD
AEgwRgIhAJ8Lz2ic0KwfheQGEDsHdFG4H0otvgi3Fv8NPOu85wfsAiEA4yjHd2E0
GUtE+dBQMtAJzayxO5YE2gDcI2vzGmaOOtwwDQYJKoZIhvcNAQELBQADggEBAGGl
W+Eg48/p0YtRCOQ9rE87ZOgV0T7M2Xk9KLorzuB18ZWITk4lDSj7tPcgd0B0Rg3y
hXcmWfJjz8PLzYhCYZSlZuwGibcvFFe8Tpok18iO25dekxs9QsiRAEXbgTG13Fsf
j0NAGLxGUmnhoJn8x5fU9AGim/Rn313U99h5NqCPVPpwV6KQ3Z7Rt9q7ikvW5F2W
Wecsf2uvFgDU4NY9NINJYIOs3tnN/NHHkCQjseRRtmWTBS7m/fvZvSrvb7/o+Kse
7DlBTM/WCGDLo4ZW/BqwY2d4Gs2hnzqQqUPpz0tOZ3cWuA/D7jokOGFh2IxCwzQO
v7g0eJupNAawi4fBGrw=
-----END CERTIFICATE-----
```

### 9. 厂商通道测试方法

1. 将集成好的App（测试版本）安装在一台华为测试机上，并且运行App
2. 保持App在前台运行，尝试扫码测试推送消息
3. 如果应用收到消息，将App退到后台，并且杀掉所有App进程
4. 再次进行测试推送消息，如果能够收到推送，则表明厂商通道集成成功
5. 最好能根据官方推荐方式，先[测通华为官方推送](https://developer.huawei.com/consumer/cn/doc/development/HMS-Guides/push-console)

### 10. 兼容性

如果您的App已经集成了个推VIP或极光VIP版本的推送SDK，我们的Android SDK也能兼容。

为了和个推兼容，我们将厂商通道独立打包。以华为推送通道为例，我们打包两个SDK：gpush-huawei-sdk和gpush-huawei-adapter。

如果是个推、极光等VIP版本的用户可以将官方SDK包gpush-huawei-sdk 排除出去。

```java
implementation ('com.growingio.android.gpush:gpush-huawei-adapter:$gtouch_version') {
        exclude(group: 'com.huawei.hms' , module: 'push')
    }
```

