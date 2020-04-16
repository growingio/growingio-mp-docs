# iOS 运营SDK调试指南

集成SDK 需要验证一下功能  
  
**弹窗扫码测试**  
创建一个普通弹窗，触发时机选择打开APP，测试环节中通过扫描二维码，跳转app,触发弹窗，  
弹窗成功，点击弹窗，会跳转到你设置的H5或者内部页面。  
  
扫码测试环节是忽略用户分群的，只需要满足触发时机就会弹窗，方便快速验证埋点弹窗是否正确。

**推送扫码测试**

打开app，打开内部页，打开H5， 

**推送数据上报测试\(iOS 10以上\)**  
方法一：NotificationService中 加入调试代码

```text
        self.bestAttemptContent.title = [NSString stringWithFormat:@"%@ [PushExtentsion集成成功]", self.bestAttemptContent.title];
```

推送的标题有带上PushExtentsion集成成功  即可

方法二:

建测试分群，应用在后台或者杀死进程情况下，通过GIO平台进行分群推送，过一段时间约10分钟查看是否有消息送达数据的统计。

方法三 .通过手机代理抓包，观察应用在后台或者杀死进程情况下，通过GIO平台进行消息推送时，是否调用GIO的API接口\(api.growingio.com\)即可

