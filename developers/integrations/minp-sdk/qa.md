# 小程序集成常见问题

### 1.[遇到集成问题和弹窗未弹出等问题，点击查看文档](https://shimo.im/docs/xrP8cDKkYx9gJg8Y/read)

### 2.查看 SDK 版本信息

正确集成小程序sdk后，可以通过在控制台输入 `gioGlobal.vdsConfig.sdkVer` 查看sdk版本

### **3. 应用设置中填写微信小程序 key 和 Secret用途 \(非必填\)**

生成二维码，通过扫码来预览配置的微信弹窗。（注：App Secret用于生成accessToken，其只会在一个弹窗第一次生成预览二维码时调用一次）  
SDK 3.4.0版本已支持设备ID预览弹窗

### 4. 弹窗 埋点事件时机选择

  
建议放在onShow 后，官网onLoad 有时不触发  
[https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/route.html](https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/route.html)

### **5. 小程序的打开App事件**

小程序 每个页面的访问，都算一次打开APP事件，建议不要对同一个用户同时上线多个打开app事件的弹窗， 可以在不同页面采用埋点事件触发事件弹窗

### **6. 如果忘记关闭预览弹窗**

如果忘记关闭预览弹窗，或者一直处于预览弹窗状态，可以将这个弹窗上线再下线，取消预览状态

