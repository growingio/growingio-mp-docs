# 小程序资源位SDK

> **参考代码：**[https://github.com/growingio/minp-marketing-demo](https://github.com/growingio/minp-marketing-demo)

## 集成小程序sdk \(如已集成最新弹窗sdk，跳过此步\)

首先按照官方文档 [微信小程序SDK](https://docs.growingio.com/docs/developer-manual/sdkintegrated/other-sdk/minp-sdk) 集成文档，集成最新的小程序sdk。集成成功后，可以在微信小程序开发者工具的控制台中看到打印输出 `init growingio...`。

## 查看sdk版本

正确集成小程序sdk后，可以通过在控制台输入 `global.vdsConfig.sdkVer` 查看sdk版本，要使用Banner功能，请确保版本在 `3.2.0` 之上。

## 集成小程序Banner



**小程序Banner分两种集成方式:**

* 模版模板
* 自渲染

bannerKey来源于网页配置

![](../../../.gitbook/assets/image%20%28178%29.png)

### 一、模板渲染

适合本身没有Banner组件或者希望全部使用GrowingIO触达Banner的场景。 此种方式集成，sdk提供小程序组件供调用，支持几乎所有小程序`swiper`属性。

#### 集成方式

**原生组件**

1. 在**app.json**文件中的**usingComponents**属性中，添加**gio-banner**组件

   ```text
   "usingComponents": {
   "gio-banner": "utils/es/components/gio-banner/gio-banner"
   },
   ```

2. 在需要集成的page页面的**wxml**文件里，引入**gio-banner**组件。

```text
// 例：pages/index/index.wxml
<gio-banner bannerKey='xxx' ...props />
<View>Welcome to GrowingIO</View>
```



**Taro**

1. 在需要集成的page页面的**config配置项里**通过**usingComponents属性引入组件**
2. 在**render方法**中使用组件。

```text
// 例：pages/index/index.js
export default class Index extends Component {
  config = {
    navigationBarTitleText: 'GrowingIO',
    usingComponents: {
      'gio-banner': 'utils/es/components/gio-banner/gio-banner'
    }
  }
  
  ...
  
  render() {
    return (
      <View>
        <gio-banner bannerKey='xxx' ...props />
        <View>Welcome to GrowingIO</View>
      </View>
    )
  }
}
```



**mpvue**

1. 将sdk文件包解压后放到`/src/utils`下
2. 将其中的`components`目录移动到`/static`下
3. 在`/src/pages/`下具体页面的`main.json`中或`/src/app.json`中使用`usingComponents`引入组件

```text
{
  "usingComponents": {
    "gio-banner": "../static/components/gio-banner/gio-banner"
  }
}
```

      4.在具体渲染组件的`template`中使用，bannerKey来自网页生成，值唯一

```text
<template>
<div>
 <gio-banner bannerKey='xxx' />
</div>
</template>
```

### wepy应用\(2.0.0以上版本\)

 在每一个page页面的wpy文件里，引入gio-banner组件（原则上只需要在需要banner的页面引入组件）

```text
// 例：pages/index.wpy

// template
<template>
    <gio-banner bannerKey='xxx' />
    // ...more
</template>

<config>
// usingComponents
"usingComponents": {
  "gio-banner": "../utils/gio-minp/components/gio-banner/gio-banner"
}
</config>
```

#### 属性参考

| 属性 | 类型 | 含义 |
| :--- | :--- | :--- |
| bannerKey | String | bannerKey，必填，唯一值 |
| placeholderDrawable | String | 默认占位图，建议使用本地图片 |
| errorReplaceDrawable | String | 请求出错时的占位图，建议使用本地图片 |
| indicatorDots | Boolean | 是否显示面板指示点，默认true |
| indicatorColor | String | 指示点颜色，默认 'rgba\(0, 0, 0, .3\)' |
| indicatorActiveColor | String | 当前选中的指示点颜色，默认 '\#000' |
| autoplay | Boolean | 是否自动切换，默认true |
| interval | Number | 自动切换时间间隔，默认5000ms |
| duration | Number | 滑动动画时长，默认500ms |
| circular | Boolean | 是否采用衔接滑动，默认true |
| vertical | Boolean | 滑动方向是否为纵向，默认false |
| previousMargin | String | 前边距，可用于露出前一项的一小部分，默认 '0px' |
| nextMargin | String | 后边距，可用于露出后一项的一小部分，默认 '0px' |
| easingFunction | String | 动画类型，默认 'default'，剩余值参考小程序swiper组件 |

### 模板渲染容错处理：

假如没有配置资源位banner也没有设置默认占位图，则隐藏banner区域  
假如服务器出错， 会先取缓存里banner的数据，如果没有缓存，会加载用户配置的错误占位图errorReplaceDrawable，如果没有设置错误占位图，会显示空白，所以建议设置好错误占位图。  
如果请求图片加载慢的话，可以设置默认占位图placeholderDrawable，作为中间过程显示的图片。

### 二、自渲染

仅提供数据，适合本身有banner组件，希望在已有的banner组件上添加触达banenr的场景。

#### 集成方式

1. 在需要触达banner的页面或者全局`usingComponents`上，引入触达banner。

   ```text
   "usingComponents": {
   "gio-banner": "utils/es/components/gio-banner/gio-banner"
   },
   ```

2. 引入成功后，会在gioGlobal上注册一个函数，接着可以通过调用此函数来异步获取触达banner信息。

   ```javascript
   gioGlobal.getBannerMessages(bannerKey).then(data => {
   console.log('触达banner数据', data);
   })
   ```

#### request

后台配置的bannerKey，必填。

#### response详情

| 属性 | 含义 |
| :--- | :--- |
| key | bannerKey |
| name | banner的名称 |
| messages | banner详情 |

#### messages详情

| 属性 | 含义 |
| :--- | :--- |
| id | 单张banner的Id |
| index | 单张banner的在后台配置显示的序号 |
| name | 单张banner的名称 |
| imageUrl | 单张banner的url |
| summary | 单张banner的summary，暂无 |
| onShow | 单张banner的显示事件，需要手动调用，调一次会上报一次显示次数 |
| onClick | 单张banner的点击事件，需要手动调用，调一次会上报一次点击次数并执行后台配置的操作 |

