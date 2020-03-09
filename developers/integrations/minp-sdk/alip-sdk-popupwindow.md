# 支付宝小程序弹窗SDK



> 参考代码：[https://github.com/growingio/minp-marketing-demo](https://github.com/growingio/minp-marketing-demo)

## 一. 集成小程序弹窗SDK

1. 首先先按照 [支付宝小程序SDK集成文档](https://docs.growingio.com/docs/developer-manual/sdkintegrated/other-sdk/ali-sdk)进行支付宝小程序SDK的集成。（如已集成SDK则跳过此步）
2. 登陆支付宝小程序后台，进入配置

   打开小程序详情/设置/开发设置

   配置httpRequest接口请求域名白名单：https://messages.growingio.com

3. 开发者工具要开启**component2**编译

## 二. 平台创建支付宝小程序SDK消息

进入**GrowingIO官网** -&gt; **用户运营**，点击左上角的**新建**按钮，选择**弹窗**，然后选择**小程序**，即可进入小程序的弹窗配置页面

![](../../../.gitbook/assets/image%20%2865%29.png)

![](../../../.gitbook/assets/image%20%28124%29.png)

根据您的需要，选择对应的**产品**、**触发时机**、**触发次数**、**图片素材**、**点击事件后**、**上线时间**、**停止时间**后，**保存上线**即可。

## 三. 使用支付宝小程序SDK组件

> 这里以**原生小程序应用**与**Taro应用**为例，其余支付宝小程序框架可参考对应框架对于小程序原生组件的使用方式。如果是第一次集成小程序SDK，建议下载最新GIOSDK全量替换。

### 3.1 原生小程序应用

1. 在**app.json**文件中的**usingComponents**属性中，添加**gio-marketing**组件

```java
"usingComponents": {
  "gio-marketing": "utils/es/components/gio-marketing/gio-marketing"
},
```

2. 在每一个page页面的axml文件里，引入gio-marketing组件（原则上只需要在需要弹窗的页面引入组件）

```java
// 例：pages/index/index.axml

<gio-marketing />
<View>Welcome to GrowingIO</View>
```

### 

## 四. 接入问题排查文档

> [遇到集成问题和弹窗未弹出等问题，点击查看文档](https://shimo.im/docs/xrP8cDKkYx9gJg8Y/read)

## 五. 登陆用户注册至今设置

使用特殊 登陆用户变量，**注册至今**  
需要在代码设置一下登陆用户变量 注册日期 CreateAt，需要保证key 是 CreateAt , 值是YYYYMMDD  
SDK 版本3.4.0以上

```java
//参考
gio('setUser', {'CreateAt':'20200107'})
```

  


