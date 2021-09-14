# 弹窗SDK（微信小程序）

> 参考代码：[https://github.com/growingio/minp-marketing-demo](https://github.com/growingio/minp-marketing-demo)

## 一. 集成小程序弹窗SDK

1. 首先先按照[微信小程序SDK集成文档](https://docs.growingio.com/v3/developer-manual/sdkintegrated/mini-program-sdk/minp-sdk)进行微信小程序采集SDK的集成。（如已集成采集SDK则跳过此步）
2. 登陆微信小程序后台，进入配置

   打开开发设置，到服务器域名配置部分

   在`request合法域名`中添加：https://messages.growingio.com  
   `downloadFile请求合法域名列表`中添加：https://statics.growingio.com和https://growing-statics-public.cn-bj.ufileos.com

## 二. 平台创建微信小程序SDK消息

进入**GrowingIO官网** -&gt; **用户运营**，点击左上角的**新建**按钮，选择**弹窗**，然后选择**小程序**，即可进入微信小程序的弹窗配置页面

![](../../../.gitbook/assets/image%20%2870%29.png)

![](../../../.gitbook/assets/image%20%28135%29.png)

根据您的需要，选择对应的**产品**、**触发时机**、**触发次数**、**图片素材**、**点击事件后**、**上线时间**、**停止时间**后，**保存上线**即可。

## 三. 使用微信小程序SDK组件

> 这里以**原生小程序应用**与**Taro应用**为例，其余微信小程序框架可参考对应框架对于小程序原生组件的使用方式。如果是第一次集成小程序SDK，建议下载最新GIOSDK全量替换。

### 3.1 原生小程序应用

1. 在**app.json**文件中的**usingComponents**属性中，添加**gio-marketing**组件

```java
"usingComponents": {
  "gio-marketing": "utils/es/components/gio-marketing/gio-marketing"
},
```

2. 在每一个page页面的wxml文件里，引入gio-marketing组件

{% hint style="info" %}
（原则上只需要在需要弹窗的页面引入组件）

3.7.3 版本支持跳转H5 和 第三方小程序，需要添加标签属性`h5-page和 env-version`
{% endhint %}

```java
// 例：pages/index/index.wxml,   假如H5承接页面为/pages/webview/index

<gio-marketing h5-page="/pages/webview/index" env-version="release"/>
<View>Welcome to GrowingIO</View>
```

#### H5页面跳转

小程序是无法直接跳转到浏览器的，要实现h5页面的跳转就需要在小程序内提供一个带有webview的承接页来展示h5页面，该页面要用户提供并配置，弹窗和资源位提供新的标签属性`h5-page`。

| **属性** | **类型** | **默认值** | **说明** |
| :--- | :--- | :--- | :--- |
| `h5-page` | String | /pages/h5/h5 | 配置h5页面的承接页 |

如承接页为: `/pages/webview/index`，应该如下配置**&lt;gio-marketing h5-page="/pages/webview/index" /&gt;**

承接页示例如下：

```javascript
 // pages/webview/index.js
 Page({
   /**
    * 生命周期函数--监听页面显示
    */
   onShow: function () {
     this.setData({
       url: this.options.url
     })
   }
 })
 ​
 // pages/webview/index.wxml
 <view>
   <web-view src="{{url}}"></web-view>
 </view>
```

注：承接页必须不为`tabBar`页面。

#### 三方小程序跳转

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>&#x5C5E;&#x6027;</b>
      </th>
      <th style="text-align:left"><b>&#x7C7B;&#x578B;</b>
      </th>
      <th style="text-align:left"><b>&#x9ED8;&#x8BA4;&#x503C;</b>
      </th>
      <th style="text-align:left"><b>&#x8BF4;&#x660E;</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>env-version</code>
      </td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">release</td>
      <td style="text-align:left">
        <p>&#x4E09;&#x65B9;&#x5C0F;&#x7A0B;&#x5E8F;&#x7684;&#x7248;&#x672C;&#xFF0C;&#x4EC5;&#x5F00;&#x53D1;&#x6D4B;&#x8BD5;&#x4F7F;&#x7528;&#x652F;&#x6301;&#xFF1A;<code>develop, trial, release</code>
        </p>
        <p><a href="https://developers.weixin.qq.com/miniprogram/dev/api/navigate/wx.navigateToMiniProgram.html">&#x5176;&#x4ED6;&#x7591;&#x95EE;&#x89C1;&#x5FAE;&#x4FE1;&#x5C0F;&#x7A0B;&#x5E8F;&#x6587;&#x6863;</a>
        </p>
      </td>
    </tr>
  </tbody>
</table>

### 3.2 Taro应用

在每一个page页面的**config配置项里**通过**usingComponents属性引入组件**，接着在**render方法**中使用组件（原则上只需要在需要埋点的页面引入组件）。

```java
// 例：pages/index/index.js

export default class Index extends Component {
  config = {
    navigationBarTitleText: 'GrowingIO',
    usingComponents: {
      'gio-marketing': 'utils/es/components/gio-marketing/gio-marketing'
    }
  }
  
  ...
  
  render() {
    return (
      <View>
        <gio-marketing />
        <View>Welcome to GrowingIO</View>
      </View>
    )
  }
}
```

### 3.3 mpvue应用

1. 将SDK文件包解压后放到**/src/utils**下
2. 将其中的**components**目录移动到**/static**下
3. 在**/src/pages/**下具体页面的**main.json**中或**/src/app.json**中使用**usingComponents**引入组件

```java
{
  "usingComponents": {
    "gio-marketing": "../static/components/gio-marketing/gio-marketing"
  }
}
```

4. 在具体渲染组件的template中使用

```java
<template>
  <div>
    <gio-marketing />
  </div>
</template>
```



### 3.4 wepy应用\(2.0.0以上版本\)

 在每一个page页面的wpy文件里，引入gio-marketing组件（原则上只需要在需要弹窗的页面引入组件）

```java
// 例：pages/index.wpy

// template
<template>
    <gio-marketing />
    // ...more
</template>

<config>
// usingComponents
"usingComponents": {
  "gio-marketing": "../utils/gio-minp/components/gio-marketing/gio-marketing"
}
</config>
```

## 四. 接入问题排查文档

> [遇到集成问题和弹窗未弹出等问题，点击查看文档](https://shimo.im/docs/xrP8cDKkYx9gJg8Y/read)



## 五. 弹窗大小说明

  宽度是窗口的80%，高度随内容的高度自动伸缩



## 六. 登陆用户注册至今设置

使用特殊 登陆用户变量，**注册至今**  
需要在代码设置一下登陆用户变量 注册日期 CreateAt，需要保证key 是 CreateAt , 值是YYYYMMDD  
SDK 版本3.3.0以上

```java
//参考
gio('setUser', {'CreateAt':'20200107'})
```

## 七. 弹窗 埋点事件时机选择

  
建议放在onShow 后，官网onLoad 有时不触发  
[https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/route.html](https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/route.html)  


