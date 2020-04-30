# 常见问题

### 推送流程介绍 <a id="ios_1"></a>

![](../../../.gitbook/assets/image%20%28163%29.png)

###  <a id="ios_1"></a>

简要说明iOS客户端实现推送流程的步骤：

* 第一步：要求客户端设备与APNs建立TSL连接，APNs需要验证设备的有效性；
* 第二步：客户端App向APNs请求推送消息用的Token；\(SDK 内部实现\)
* 第三步：客户端App将从APNs获取的Token注册到GrowingIO服务器分群信息中；（SDK内部实现）
* 第四步：通过用户运营官网或者是REST API创建分群推送消息，然后GrowingIO服务器再去请求APNs下发消息；
* 第五步：APNs服务器接收到GrowingIO服务器的推送消息请求后，根据Token来将推送的消息下发到指定的设备；
* 第六步：收到推送，上报推送送达信息，点击推送，跳转对应落地页

### 1. 集成后运行报错 <a id="ios_1"></a>

确认一下 依赖的埋点SDK是否是2.8.9以上  
  
Xcode 的控制台打印可看 **集成SDK版本  
GrowingIO version: 2.8.14 !!!  
Thank you very much for using GrowingIO Touch. SDK version 1.3.0**

### 2.为什么 iOS 收不到推送消息？ <a id="ios_1"></a>

确认SDK 是否是1.x版本以上，1.x 以下版本不能推送

确认集成步骤是否缺失

确认app是否开启推送

确认证书与包名都正确

确认推送环境选择生产环境 和开发环境正确

确认证书没有过期

### **3.为什么测试推送能推送到，分群推送推不到？**

如果是访问用户分群，可以先用户细查查看对应分群的包名和推送令牌有没有写入  
因为分群是T+1，推送令牌要写入分群，请在第二天测试分群推送

注意：

* App集成GIO的推送SDK，并发布到商店后，用户只有下载并打开了新版的App才可以上报推送令牌，这台设备才能够被送达。
* 分群是每日凌晨计算，所以如果用户A今天是第一次打开新版的App，那么第二天才能进入分群被送达到。所以建议您第一次发送 Push 等待一天。

#### 查询某个用户是否有推送token

#### 可以通过事件分析，筛选一下，确认用户是否有上报token

![](https://gblobscdn.gitbook.com/assets%2F-Lpwgem-x8KzhBglybzw%2F-M3zSOS-wxbLYblt7uEq%2F-M3zT-UNwL077cveAAcV%2Fimage.png?alt=media&token=8a2b2175-4b7f-4364-aaca-57c0544aa65b)

### **4.SDK最低兼容iOS系统。**

最低兼容iOS 8.0 系统。

### **5.官网推送证书配置常见疑问**

官网推送证书过期，更新后是否需要打包 App 重新上架？  ****不需要   
官网推送证书的有效期是否可以设置？ 不能，该有效期是 Apple 决定的，自生成起有效期 1 年。  
Apple 的生产推送证书允许用于开发环境的推送， 开发者可以上传生产证书到开发环境配置中，即可在官网推送平台处选择开发环境做推送。

### 6. **iOS Token 失效的原因？**

* 系统注销或者是应用被卸载。
* 用户在新的设备上安装 App。
* 用户从 backup 中恢复设备。
* 用户重新安装 OS。

### 7.其他推送问题

[点击查看](https://docs.growingio.com/mp/faq/push)  


  
  




