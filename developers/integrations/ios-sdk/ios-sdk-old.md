# iOS SDK 1.0.3及以下旧版本升级指导

本文旨在帮助您从 1.0.3 及以下版本快速升级至 1.1.2 版本，由于两个版本间变动，因此建议您在升级前一定参照本文完成必要的实施工作。  
  
**头文件修改**  
升级后弹窗头文件修改  
import &lt;GrowingTouchKit/GrowingTouch.h&gt;修改为 **import &lt;GrowingTouchCoreKit/GrowingTouchCoreKit.h&gt;**  
  
升级后banner头文件修改  
****import &lt;GrowingTouchKit/GrowingTouchBannerView.h&gt;修改为**import &lt;GrowingTouchCoreKit/GrowingTouchBannerView.h&gt;  
  
  
  
包引入修改**  
  
使用CocoaPods快速集成升级的如下修改，  
pod 'GrowingTouchKit', 修改为  **pod 'GrowingTouch/GrowingTouchKit'**  
pod 'GrowingPushKit'  修改为  **pod 'GrowingTouch/GrowingPushKit'**  
pod 'GrowingPushExtensionKit' 修改为 **pod 'GrowingTouch/GrowingPushExtensionKit'**  
  
手动导入升级包如下修改  
**1.** 需要升级埋点SDK 2.8.7 及以上版本[iOS 埋点 SDK 帮助文档](https://docs.growingio.com/docs/sdk-integration/ios-sdk/ios-mai-dian-sdk) 。  
**2.** 下载最新的iOS GrowingTouch SDK包，并将其中的GrowingTouchCoreKit.framework以及相应功能需要的framework 添加到iOS工程中。下载链接：[https://github.com/growingio/GrowingSDK-iOS-GrowingTouchCoreKit/archive/master.zip](https://github.com/growingio/GrowingSDK-iOS-GrowingTouchCoreKit/archive/master.zip)  
 弹窗集成 GrowingTouchCoreKit、GrowingTouchCoreUI.bundle+ GrowingTouchKit   
 ****推送集成GrowingTouchCoreKit、GrowingTouchCoreUI.bundle、GrowingPushKit+GrowingPushExtensionKit'

  
  
****

