# iOS SDK 概述

### iOS SDK 集成 <a id="ios-sdk_1"></a>

弹窗集成

推送集成

资源位集成

### iOS SDK 说明 <a id="ios-sdk_2"></a>

* 支持的 iOS 版本为 8.0 及以上版本
* 推送支持 iOS 版本为 10.0 以上的版本时需知。
  * Notification Service Extension 证书配置时需要注意 BundleID 不能与 Main Target 一致，证书需要单独额外配置
  * 请将 Notification Service Extension 中的 Deployment Target 设置为 10.0

