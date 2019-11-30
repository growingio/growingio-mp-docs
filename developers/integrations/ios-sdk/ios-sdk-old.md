# iOS SDK 1.0.3及以下旧版本升级指导

本文旨在帮助您从 1.0.3 及以下版本无缝升级至 1.1.0 版本，由于两个版本间变动，因此建议您在升级前一定参照本文完成必要的实施工作。  
  
**头文件修改**  
升级后弹窗头文件修改  
import &lt;GrowingTouchKit/GrowingTouch.h&gt;修改为 **import &lt;GrowingTouchKit/GrowingTouch.h&gt;**  
  
升级后banner头文件修改  
****import &lt;GrowingTouchKit/GrowingTouchBannerView.h&gt;修改为**import &lt;GrowingTouchCoreKit/GrowingTouchBannerView.h&gt;  
  
  
  
包引入修改**  
使用CocoaPods快速集成升级的，

pod 'GrowingTouchKit', 修改为  **pod 'GrowingTouch/GrowingTouchKit'**

pod 'GrowingPushKit'  修改为  **pod 'GrowingTouch/GrowingPushKit'**

pod 'GrowingPushExtensionKit' 修改为 **pod 'GrowingTouch/GrowingPushExtensionKit'  
  
  
手动导入升级包，需要升级无埋点SDK 2.8.7 及以上版本**  
  


