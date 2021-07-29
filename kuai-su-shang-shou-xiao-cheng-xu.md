---
description: 帮助您快速了解小程序如何使用智能运营平台
---

# 快速上手 - 小程序

### **SDK接入与准备**

1. 用户运营小程序 SDK 与无埋点 SDK 是集成在一起的，集成方法参见：[微信小程序SDK集成](https://docs.growingio.com/v3/developer-manual/sdkintegrated/mini-program-sdk/minp-sdk)
2. 需要登陆您的微信小程序后台，进入配置，打开开发设置，到服务器域名配置部分

   在`request合法域名`中添加：https://messages.growingio.com  
   `downloadFile请求合法域名列表`中添加：https://statics.growingio.com和https://growing-statics-public.cn-bj.ufileos.com

3. 在小程序页面中使用触达组建，详见： [小程序SDK](developers/integrations/minp-sdk/)

### **了解「用户」**

规划用户属性字段，是精细化运营的基础

* 微信小程序项目如何使用和上传「用户属性」，请参见[微信用户信息的配置](https://docs.growingio.com/v3/developer-manual/sdkintegrated/other-sdk/minp-sdk#2-wei-xin-yong-hu-xin-xi-de-pei-zhi)。
* 如何使用「[用户分群](https://docs.growingio.com/v3/product-manual/user-warehouse/segmentations/segmentations/)」

### **了解「事件」**

在合适的时机触达，需要先定义埋点事件

* 小程序如何设置埋点事件和埋点事件变量，请参见[自定义数据上传](https://docs.growingio.com/v3/developer-manual/sdkintegrated/other-sdk/customize-api#she-zhi-zi-ding-yi-shi-jian-ji-shi-jian-ji-bian-liang-track)。

### **实际操作**

* 如何[发弹窗](product-manual/popup/)

