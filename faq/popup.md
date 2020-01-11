# 弹窗 FAQ

### **1. 想修改已经在运行的弹窗怎么办？**

在弹窗详情页规则右上角可以点击修改，为了降低对线上弹窗影响，需要先将线上的弹窗下线，再进去编辑页，修改条件并测试没有问题后，可以再次上线弹窗，再次上线后之前收到过的用户不会再收到。

### 2. 消息中止后再上线，之前收到过弹窗的用户还会再收到吗？

不会。每一个弹窗有唯一ID，会在SDK做去重。不管下线几次再上线，都是记录之前收到人的信息的。

### **3. 如果一个用户在同一个触发条件下同时触发了两个弹窗，会怎样处理？**

在同一个触发条件，且用户同时属于这两个弹窗的目标分群，那么在同一个时间只会收到一个弹窗，即最近更新过的弹窗消息。下次打开会看到第二个，是按时间优先级来展示。web弹窗里各个位置的弹窗支持同时弹。我们会持续优化这个逻辑的自定义配置功能，欢迎提出你的需求。

### **4. 为什么活动还没上线，但是已经有了点击/展示数据？**

弹窗上线前，自己进行测试时的展示和点击数据也会计算进来，所以在弹窗数据页看到的是全部的数据。

### 5. 弹窗功能是否稳定，上线后是否影响性能，是否页面加载时间过长?

GIO弹窗功能是后台加载的，不会影响用户现有的页面加载速度。已经有不少客户在线上环境验证过，弹窗稳定性应该是可以保证的。

### **6. 上线后收不到弹窗是为什么？**

1. 先用设备扫码测试，看是否能正常弹出。（扫码测试用的设备，必须安装了相应App，且App内成功安装了弹窗SDK）
2. 如果测试设备也无法弹出，请联系GIO开发人员。
3. 弹窗上线后，会有最多3分钟的延时，如果是第一次设置后的时间可能会久一些，如果1个小时后仍然没有收到，请联系GIO开发人员。
4. 如果测试能正常弹出，上线后却收不到，可能为以下原因，请一一排查：

* 请检查**是否关闭了埋点功能**，因为**弹窗SDK依赖埋点**功能。
* 你使用的设备没有在所选分群中，可以再复制一个同样的弹窗，修改分群为**全部访问用户**，测试能否收到。
* 已经点击过弹窗，所以不会再出现。
* 触发条件没有匹配，可以先选择系统触发条件，打开app的时候弹出。然后退出APP后台，重新启动。
* 重新冷启动APP，查看日志是否有类似下面内容，如果**popupWindows/PopupWindowEvent** 字段不为**null**表示弹窗正确获取到了，如果为**null**表示该设备不在群组中。

iOS

```text
GTouch.GTouchManager: Load touch event config success, eventConfig is <GTouchEventConfig: self.splashs=(null), self.popupWindows=(
    "<GrowingPopupWindowEvent: self.id=452, self.state=activated, self.content=https://statics.growingio.com/pages/20190410/1114/1554862553584/1554862553584-popupWindow.html?url_scheme=growing.4458a0c50d7fd57c, self.priority=1, self.updateAt=1554862553666, self.rule=<GrowingRule: self.action=appOpen, self.type=system, self.startAt=1176171353583, self.endAt=1933553753583, self.limit=5>>"
), self.idMappings=<GrowingIdMappings: self.bu=2787622, self.bcs=248881>>
```

Android

```text
D/GTouch.GTouchManager: Loading touch event config success result is TouchEventConfig{idMappings=IdMappings{bu=976846, bcs=137554}, splashs=[], popupWindows=[PopupWindowEvent{id=297, state='null', content='https://statics.growingio.com/pages/20190328/3/1553767879538/1553767879538-popupWindow.html?url_scheme=growing.638b52710867187c', priority=1, updateAt=1553767879559, rule=Rule{action='appOpen', type='system', startAt=1175076679537, endAt=1932459079537, limit=1}}]}
```

或者重新冷启动APP，通过抓包软件获取类似[https://messages.growingio.com/v3/xxxxxx/notifications?url\_scheme=xxxxx](https://messages.growingio.com/v1/xxxxxx/notifications?url_scheme=xxxxx) 的url的响应包，其中响应 json 中 popupWindows 字段不为 null 表示弹窗正确获取到了，如果为null表示该设备不在群组中。

### **7. 扫码测试时唤醒了app，但是没有弹出弹窗?**

如果 SDK 没有问题，可以试试杀死 app 后台进程，再次扫码唤醒。

### 8. 为什么目标分群人数会和实际展示的人数略有差异？

* 用户网络环境差，导致加载弹窗资源超时或者失败。
* 在极少数机型上面WebView会初始化失败，所以弹窗无法弹出。
* 分群是每天早上更新，有可能用户上午活跃，弹窗是下午上线，但用户之后并没有打开App

### 9. 是否Scheme必须配置正确，才能弹出弹窗?

是的，Scheme是用于标示产品，没有产品无法过滤弹窗

### 10. Scheme要在哪里获取 ？

在导航栏上点击齿轮按钮，在下拉菜单中点击「应用管理」

![](../.gitbook/assets/image%20%2869%29.png)

在应用列表中可以看到应用的scheme

### 11. 选择了某个分群作为弹窗的目标人群，但该分群中只有部分人收到了弹窗，为什么？

1. 这些用户的APP需要升级到了有弹窗SDK的App版本。
2. 因为网络环境或者手机版本兼容性等问题，可能有极少数用户是弹不出来的。

### 12. 我的App有闪屏广告，如何能在闪屏结束后再弹出弹窗？

appOpen是App从后台到前台，第一个activity onStarted 的时候触发，如果把握不准appOpen的时机，建议自定义事件（埋点），可以更精准的控制弹窗弹出的时机。

如下图，选择触发时机为您的打点时间，可以更精准的控制。

![](../.gitbook/assets/image%20%2837%29.png)

### **13. Android SDK 支持的最低版本是 Android 4.2，那低于这个版本的话会是什么表现？**

由于 GTouch SDK 依赖无埋点 SDK ，在低于 Android 4.2 的系统中，无埋点 SDK 会自动关闭，这样我们的弹窗功能也会自动关闭，不会影响任何业务。

### 14. 弹窗设置了只弹出一次，为什么同一个设备或者同一个用户仍然会多次收到弹窗？

1. 用户删除APP后重新下载了APP。
2. 用户同一个设备上切换了不同账号。 
3. 用户在多台设备上登录了同一个账号。 
4. 有极少数用户由于手机硬盘或者系统低概率出现问题，导致弹窗数据无法正常写入到本地，导致下次弹窗仍然会弹出\(基本可以忽略\)。

### 15. 预览弹窗连续弹两次？

  您有可能在同一时间触发了两次对应的埋点事件，在预览模式下我们的sdk是触发一次对应的事件就弹一次对应的预览弹窗。







