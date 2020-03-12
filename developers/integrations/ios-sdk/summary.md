# iOS SDK 概述

### iOS SDK 集成 <a id="ios-sdk_1"></a>

弹窗集成

推送集成

 iOS推送 SDK 方便开发者快捷地为 iOS 应用增加推送功能，减少开发者集成 APNs\(Apple Push Notification Service\) 需要的工作量，降低开发复杂度。同时最新SDK还支持独有的 APNs 展示和点击统计，有助于开发者掌握更精准的推送数据，优化运营效果。  
推送支持打开app，跳转内部页，跳转H5 ，支持原有自定义协议

资源位集成

### iOS SDK 说明 <a id="ios-sdk_2"></a>

* 支持的 iOS 版本为 8.0 及以上版本
* 推送支持 iOS 版本为 10.0 以上的版本时需知。
  * Notification Service Extension 证书配置时需要注意 BundleID 不能与 Main Target 一致，证书需要单独额外配置
  * 请将 Notification Service Extension 中的 Deployment Target 设置为 10.0

