# 推送API

## 1. 概述

为满足广大客户更灵活创建触达消息推送的诉求，GrowingIO 提供了一套创建触达消息的API。本文档旨在说明一些调用流程，逻辑及相关接口说明。

## 2. 认证

为保证数据安全，GrowingIO所有的API服务，请求Head中需要携带 Token。

Token 获取详见：[“GrowingIO接口认证”文档](https://docs.growingio.com/docs/api/authentication)​

## 3. 使用注意

1. 接口调用频率限制：单个 Token 调用限制 1200次/分钟。
2. 推送单条最大目标数限制：单次调用接口 audience 列表长度限制 2000 条。

## 4. 接口说明

地址：POST    https://www.growingio.com/api/v1/projects/:project\_id/meta/marketing\_push

请求对象：

| 字段名 | 类型 | 说明 | 限制 | 示例 |
| :--- | :--- | :--- | :--- | :--- |
| cid | 字符串 | cid 用于标示同一批推送消息。cid 相同的推送消息会聚合到同一个消息记录里，便于后续查看数据。同一个cid，同样的请求参数推送服务器不会生成新的推送任务，用于防止 api 调用端重试造成服务端的重复推送。建议使用 UUID 。 | 长度不超过64个字符 | 61b757af-f877-4e15-84f2-0f0eef69277c |
| name | 字符串 | 推送名称。建议使用 业务含义名称 + 时间戳 ，不可重复，便于在管理后台查看使用。 | 长度不超过200个字符 | 用户召回推送20190716170520 |
| packageName | 字符串 | 推送应用包名。可以在应用管理后台获取，注意 sdk 上传的包名需要和后台配置的一致！ |  | com.growingio.PushTest |
| audience | 字符串数组 | 推送目标列表 |  | 登录用户标识。一次推送最多 2000 个。客户端集成 SDK 后可获取到该值。 |
| notification | 对象 | 推送消息体 |  | - |
| options | 对象 | 推送配置项 |  | - |

使用建议：

* 推送目标用户如果小于等于2000个，可以将所有目标设备标识放到一个请求里批量推送，推送完成之后建议更换cid和消息内容再进行下次推送
* 推送目标用户如果大于2000个，需要分批推送，每批目标设备标识个数小于等于2000，保证这些批次的cid相同和消息体内容相同，这样才能将这些批次的请求聚合，方便后续在web端查看消息状态

应用管理入口：

![](../../.gitbook/assets/banner.png)

notification

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x5B57;&#x6BB5;&#x540D;</th>
      <th style="text-align:left">&#x5B57;&#x6BB5;&#x683C;&#x5F0F;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
      <th style="text-align:left">&#x9650;&#x5236;</th>
      <th style="text-align:left">&#x793A;&#x4F8B;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">title</td>
      <td style="text-align:left">&#x5B57;&#x7B26;&#x4E32;</td>
      <td style="text-align:left">&#x901A;&#x77E5;&#x6807;&#x9898;&#x3002;</td>
      <td style="text-align:left">&#x957F;&#x5EA6;&#x4E0D;&#x8D85;&#x8FC7;32&#x4E2A;&#x5B57;&#x7B26;&#x3002;</td>
      <td
      style="text-align:left">&#x65B0;&#x6D88;&#x606F;&#x901A;&#x77E5;&#xFF01;</td>
    </tr>
    <tr>
      <td style="text-align:left">alert</td>
      <td style="text-align:left">&#x5B57;&#x7B26;&#x4E32;</td>
      <td style="text-align:left">&#x901A;&#x77E5;&#x5185;&#x5BB9;&#x3002;</td>
      <td style="text-align:left">&#x957F;&#x5EA6;&#x4E0D;&#x8D85;&#x8FC7;200&#x4E2A;&#x5B57;&#x7B26;&#x3002;</td>
      <td
      style="text-align:left">&#x6536;&#x5230;&#x4E00;&#x6761;&#x65B0;&#x7684;&#x7559;&#x8A00;&#xFF0C;&#x70B9;&#x51FB;&#x67E5;&#x770B;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">extras</td>
      <td style="text-align:left">&#x5BF9;&#x8C61;</td>
      <td style="text-align:left">&#x6269;&#x5C55;&#x5B57;&#x6BB5;&#x3002;&#x8FD9;&#x91CC;&#x81EA;&#x5B9A;&#x4E49;
        JSON &#x683C;&#x5F0F;&#x7684; Key / Value &#x4FE1;&#x606F;&#xFF0C;&#x4EE5;&#x4F9B;&#x4E1A;&#x52A1;&#x4F7F;&#x7528;&#x3002;</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left">{&quot;key1&quot;: &quot;value1&quot;, &quot;key2&quot;: &quot;value2&quot;}</td>
    </tr>
    <tr>
      <td style="text-align:left">actionType</td>
      <td style="text-align:left">&#x5B57;&#x7B26;&#x4E32;</td>
      <td style="text-align:left">
        <p>&#x70B9;&#x51FB;&#x8DF3;&#x8F6C;&#x94FE;&#x63A5;&#x7C7B;&#x578B;&#x3002;</p>
        <p>&#x6253;&#x5F00;&#x7F51;&#x9875;&#xFF1A;&quot;openH5&quot;</p>
        <p>&#x6253;&#x5F00;&#x5E94;&#x7528;&#x5185;&#x5177;&#x4F53;&#x9875;&#x9762;&#xFF1A;&quot;openUrl&quot;</p>
        <p>&#x81EA;&#x5B9A;&#x4E49;&#x53C2;&#x6570;&#xFF1A;&quot;custom&quot;</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">openUrl</td>
    </tr>
    <tr>
      <td style="text-align:left">actionTarget</td>
      <td style="text-align:left">&#x5B57;&#x7B26;&#x4E32;</td>
      <td style="text-align:left">&#x70B9;&#x51FB;&#x8DF3;&#x8F6C;&#x8DEF;&#x52B2;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">com.growingio.push</td>
    </tr>
    <tr>
      <td style="text-align:left">actionParameters</td>
      <td style="text-align:left">&#x5BF9;&#x8C61;</td>
      <td style="text-align:left">&#x70B9;&#x51FB;&#x8DF3;&#x8F6C;&#x643A;&#x5E26;&#x53C2;&#x6570;&#xFF0C;&#x4EE5;&#x952E;&#x503C;&#x5BF9;&#x5211;&#x4E8B;&#x4F20;&#x9012;&#x3002;</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left">{&quot;key1&quot;: &quot;value1&quot;, &quot;key2&quot;: &quot;value2&quot;}</td>
    </tr>
  </tbody>
</table>options

| 字段名 | 类型 | 说明 | 示例 |
| :--- | :--- | :--- | :--- |
| apnsProduction | 字符串 | true 表示推送生产环境，false 表示要推送开发环境；如果不指定则为推送生产环境。 | ture |

请求示例：

```c
{
	"cid": "61b757af-f877-4e15-84f2-0f0eef69277c",
	"name": "用户召回推送20190716170520",
	"packageName": "com.growingio.PushTest",
	"audience": ["d54f5085-a057-4aa0-8463-87a1fe56e9fe", "241131c1-f3ca-4584-99b5-8a5a8c50f9c7"],
	"notification": {
		"title": "新消息通知！",
		"alert": "收到一条新的留言，点击查看。",
		"extras": {
			"key1": "value1",
			"key2": "value2"
		},
		"actionType": "openUrl",
		"actionTarget": "com.growingio.push",
		"actionParameters": {
			"key1": "value1",
			"key2": "value2"
		}
	},
	"options": {
		"apnsProduction": true
	}
}
```

返回示例：

| 字段名 | 类型 | 说明 | 示例 |
| :--- | :--- | :--- | :--- |
| cid | 字符串 | 请求参数里的cid | 61b757af-f877-4e15-84f2-0f0eef69277c |

```c
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

 Response Data  

{
  "cid" : "61b757af-f877-4e15-84f2-0f0eef69277c"
}
```



