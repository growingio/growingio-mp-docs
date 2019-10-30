# 小程序SDK

> 参考样板间代码：[https://github.com/growingio/minp-marketing-demo](https://github.com/growingio/minp-marketing-demo)

## 一. 集成小程序SDK

1. 首先先按照[微信小程序SDK集成文档](https://docs.growingio.com/docs/sdk-integration/xiao-cheng-xu-xiao-you-xi-yi-ji-nei-qian-ye-sdk/wei-xin-xiao-cheng-xu-sdk/wei-xin-xiao-cheng-xu-sdk-sdk-ban-ben1.9.1/)进行微信小程序SDK的集成。
2. 在小程序配置页面添加域名 [https://messages.growingio.com/](https://messages.growingio.com/)

## 二. 平台创建触达微信小程序SDK消息

进入**GrowingIO官网** -&gt; **用户运营**，点击左上角的**新建**按钮，选择**弹窗**，然后选择**小程序**，即可进入微信小程序的触达弹窗配置页面

![](../../.gitbook/assets/image%20%2827%29.png)

![](../../.gitbook/assets/image%20%2846%29.png)

根据您的需要，选择对应的**产品**、**触发时机**、**触发次数**、**图片素材**、**点击事件后**、**上线时间**、**停止时间**后，**保存上线**即可。

## 三. 使用微信小程序SDK组件

> 这里以**原生小程序应用**与**Taro应用**为例，其余微信小程序框架可参考对应框架对于小程序原生组件的使用方式。如果是第一次集成触达SDK，建议下载最新GIOSDK全量替换。

### 3.1 原生小程序应用

1. 在**app.json**文件中的**usingComponents**属性中，添加**gio-marketing**组件

```java
"usingComponents": {
  "gio-marketing": "utils/es/components/gio-marketing/gio-marketing"
},
```

2. 在每一个page页面的wxml文件里，引入gio-marketing组件（原则上只需要在需要埋点的页面引入组件）

```java
// 例：pages/index/index.wxml

<gio-marketing />
<View>Welcome to GrowingIO</View>
```

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

