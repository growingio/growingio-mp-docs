---
description: 是哪些因素影响了推送的到达率
---

# 推送数据

Push 发送完成后，可以实时看到数据效果。在推送管理列表中可以看到基础数据，如果想要看更详细的数据以及做更多深入的分析，可以在列表中点击推送名称进入数据报表页面查看。

## 推送数据报表页面

发送完成的推送在列表中点击标题就能进入数据详情页面，下面是数据页提供的数据口径解释：

* **目标推送设备数**：符合推送条件的所有用户数，跟所选分群相关。
* **服务器送达**：指的是发送推送请求到第三方服务器。该数据由 GIO 埋点获取。
* **有效设备**：指的是厂商通过回调接口返回给 GIO 的设备送达数据。**关机、无网络、卸载App**以及关闭卸载权限的设备是无法送达的。厂商每秒会发送一次回调数据。
* **消息点击**：指的是 GIO 的 SDK 采集到用户点击消息事件。该数据由 GIO 打点获取。

![](../../.gitbook/assets/image%20%2813%29.png)

运营者在发 Push 的时候非常关注的问题就是到达率的问题，下面详细解释在发 Push 的过程中每一步会发生什么，是哪些因素最终影响了实际到达用户设备的数量。

![](../../.gitbook/assets/liu-cheng-tu-xin.png)

首先运营选出一批推送的目标用户，GIO 会找到这些用户上报的信息，有上报过**推送令牌**的设备（token）就可以被成功送达到相应的厂商通道（凡是用户的 App 升级到含有Gpush SDK的版本且打开过应用都会上报token）。然后 GIO 会根据设备型号将这些信息发送到对应的厂商通道（比如华为设备会发给华为的服务器，小米会发给小米的服务器）这就是「**服务器送达」**，然后再由厂商将消息发送到用户设备，只有**打开了推送权限且网络状况良好**的设备才可以在这一步被送达，厂商通道会将成功到达设备的数量告诉 GIO，就是对应的「**设备送达数**」。送达到设备后，有些用户会忽略，有些会点击，GIO 会自动统计**消息的点击**数并展示。

通过这个流程图，可以发现「**能够成功推送的一个重要条件是该用户的设备已经拥有了合法的推送令牌**」，GIO 为了方便运营者自查数据，将 **触达推送令牌** 处理为一个预定义的访问用户变量，这样您自己就能在分群中看到，有多少用户是处于可被送达的状态，如下图，在**用户分群**中选择过去7天或任意时间段**有过访问的用户**，然后在过滤条件中选择 **「触达推送令牌」不等于  N/A**（意为不为空）

![](../../.gitbook/assets/p3.png)

这样设置后，可以在右边看到该分群的人数，通过下图看到，过去7天活跃用户大部分都有推送令牌，那么就可以放心推送了。

![](../../.gitbook/assets/p4.png)

## 使用分析工具看推送数据

推送功能为您预置了三个埋点指标及一个维度，您可以在分析工具中使用以获取更详细的数据趋势。比如下图直接在事件分析中就能选到

![](../../.gitbook/assets/p1.png)

预置指标：

* **消息发送：** （标识符：gio\_push\_message\_sent\)     
  * 由 GIO 服务器执行推送时上报
* **消息送达：**（标识符：gio\_push\_message\_arrived\)  
  * 安卓由厂商通道回调给我们，iOS由推送 SDK 上报
* **消息点击：**（标识符：gio\_push\_message\_clicked\)  
  * 安卓/iOS都由推送 SDK 上报

![](../../.gitbook/assets/p2.png)

预置维度：

* **触达推送名称：**（标识符：gio\_push\_message\_name）

注意：

* App集成GIO的推送SDK，并发布到商店后，用户只有下载并打开了新版的App才可以上报推送令牌，这台设备才能够被送达。
* 分群是每日凌晨计算，所以如果用户A今天是第一次打开新版的App，那么第二天才能进入分群被送达到。所以建议您第一次发送 Push 等待一天。
