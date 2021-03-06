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
MIIGeDCCBWCgAwIBAgIQHjNQWZ7wMj3+VB9p4KLDpTANBgkqhkiG9w0BAQsFADCB
jzELMAkGA1UEBhMCR0IxGzAZBgNVBAgTEkdyZWF0ZXIgTWFuY2hlc3RlcjEQMA4G
A1UEBxMHU2FsZm9yZDEYMBYGA1UEChMPU2VjdGlnbyBMaW1pdGVkMTcwNQYDVQQD
Ey5TZWN0aWdvIFJTQSBEb21haW4gVmFsaWRhdGlvbiBTZWN1cmUgU2VydmVyIENB
MB4XDTE5MDkwMjAwMDAwMFoXDTIxMDkyMjIzNTk1OVowXTEhMB8GA1UECxMYRG9t
YWluIENvbnRyb2wgVmFsaWRhdGVkMR4wHAYDVQQLExVFc3NlbnRpYWxTU0wgV2ls
ZGNhcmQxGDAWBgNVBAMMDyouZ3Jvd2luZ2lvLmNvbTCCASIwDQYJKoZIhvcNAQEB
BQADggEPADCCAQoCggEBAKv9tDk+2fiPalexslgYbCLip4Ns/91Wt6X4Q6fGjuyr
8mIf/eG5yP9TeSgmTDdR8rMX2qFYfCw8Dt3KaWpfhL4zsafoz4AiaP9CMQCP8fwq
xjmUpcqnt2fguAyxbkZpyLnwKcHm7x/RJT1NdPBPylyIZ9WgmqKwhGoM8n3v1UaU
67jDjEj/eEm1WZVx45bauBSYVMW5xb5UL7fynmIhBkQJ3+l0lmGxki6Gte4ELAsp
nDJkckWBd/2/g2a8pA37VpwDrk2/aAwsucZaDIRDeuOtDIg0blJmbVpV0oMaIoLx
FdeUjgC3ACXOt87ajzdJz/ZFFobEBHCeUGf7JIhbyy8CAwEAAaOCAv8wggL7MB8G
A1UdIwQYMBaAFI2MXsRUrYrhd+mb+ZsF4bgBjWHhMB0GA1UdDgQWBBSlAD8AGhQj
8OlfefSZrxPv6ZVXlzAOBgNVHQ8BAf8EBAMCBaAwDAYDVR0TAQH/BAIwADAdBgNV
HSUEFjAUBggrBgEFBQcDAQYIKwYBBQUHAwIwSQYDVR0gBEIwQDA0BgsrBgEEAbIx
AQICBzAlMCMGCCsGAQUFBwIBFhdodHRwczovL3NlY3RpZ28uY29tL0NQUzAIBgZn
gQwBAgEwgYQGCCsGAQUFBwEBBHgwdjBPBggrBgEFBQcwAoZDaHR0cDovL2NydC5z
ZWN0aWdvLmNvbS9TZWN0aWdvUlNBRG9tYWluVmFsaWRhdGlvblNlY3VyZVNlcnZl
ckNBLmNydDAjBggrBgEFBQcwAYYXaHR0cDovL29jc3Auc2VjdGlnby5jb20wKQYD
VR0RBCIwIIIPKi5ncm93aW5naW8uY29tgg1ncm93aW5naW8uY29tMIIBfQYKKwYB
BAHWeQIEAgSCAW0EggFpAWcAdQD2XJQv0XcwIhRUGAgwlFaO400TGTO/3wwvIAvM
TvFk4wAAAWzw+80wAAAEAwBGMEQCIGa+uxrn7YC1pHF1e8ajPOSffMhJoEhupvQx
BQdeLEr6AiA6xE7pgIygEdLyI4zI/CF0H9M911aDZoPYERBHrmQL9QB3AESUZS6w
7s6vxEAH2Kj+KMDa5oK+2MsxtT/TM5a1toGoAAABbPD7zUsAAAQDAEgwRgIhAKWE
Z0RAxmqqM3bqPQmwNt02RTN7dEFB1xKZVmbP+CtAAiEAp+TfxTUlIxw3UinKhEjd
AZw7WDz/wiDZvR7y4vFGWXIAdQBVgdTCFpA2AUrqC5tXPFPwwOQ4eHAlCBcvo6od
BxPTDAAAAWzw+80nAAAEAwBGMEQCIE3arRcTs+XLCj5HDiDZhV1QkOMCqwnTp3NV
qkLXdecXAiA3xzd97tQnMIj6BIuYbfE+sONRUe4klZiFhwstlx4LTDANBgkqhkiG
9w0BAQsFAAOCAQEARChCUxNikK3PpBPy3vGbKeVra4TlbGKygI+8eaKrR5ShM3Ed
ehQuZKxtX0wrklRbWRdRXpBqXOz2NCWa8yFq1Z2Nu/14bUe/vXmxcF/1xTRvanPl
gD4bDlupkXK6asspDvy1lr+N4cYf63Q/UxkEbGFHbXdqsylZZNxrvy7Ax4cofMRN
CSF6KduF9Er34duYBCBUYlEXI0UvuuecQ1BWIebjaruDj4vDtYN1wOEUoAWine0a
BcFs6n04ii1vhi+4mtB5G9XnbakaNan/8iujJ8djRa9Pxs8lwIAhNayYnjUWqO+X
ImV7pBXFMpwSdsW0X1cqHsNFvpf/5MHiNpuBuw==
-----END CERTIFICATE-----
```

### 9. 厂商通道测试方法

1. 将集成好的App（测试版本）安装在一台华为测试机上，并且运行App
2. 保持App在前台运行，尝试扫码测试推送消息
3. 如果应用收到消息，将App退到后台，并且杀掉所有App进程
4. 再次进行测试推送消息，如果能够收到推送，则表明厂商通道集成成功
5. 最好能根据官方推荐方式，先[测通华为官方推送](https://developer.huawei.com/consumer/cn/doc/development/HMS-Guides/push-console)

