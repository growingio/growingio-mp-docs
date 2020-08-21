# 推送API

## 1. 概述

为满足广大客户更灵活创建推送的诉求，GrowingIO 提供了一套创建推送的API。本文档旨在说明一些调用流程，逻辑及相关接口说明。

## 2. 认证

为保证数据安全，GrowingIO所有的API服务，请求Head中需要携带 Token。

Token 获取详见：[“GrowingIO接口认证”](https://docs.growingio.com/docs/developer-manual/api-reference/authenticate/)

## 3. 使用注意

1. 接口调用频率限制：单个 Token 调用限制 1200次/分钟。
2. 推送单条最大目标数限制：单次调用接口 audience 列表长度限制 2000 条。
3. 接口地址中的project\_uid就是项目ＵID，指的是访问项目的时候，页面 URL 以 /projects/:project\_uid 开头，例如 [https://www.growingio.c](https://www.growingio.com/admin/projects/nxog09md/dashboard)[o](https://www.growingio.com/admin/projects/nxog09md/dashboard)[m/admin/p](https://www.growingio.com/admin/projects/nxog09md/dashboard)[rojects/nxo](https://www.growingio.com/admin/projects/nxog09md/dashboard)[g0](https://www.growingio.com/admin/projects/nxog09md/dashboard)[9md/dashboard](https://www.growingio.com/admin/projects/nxog09md/dashboard) 中的 "nxog09mx"。
4. 接口参数中productId的获取方式：访问官网进入到推送的应用配置页面，点击目标推送应用的详细配置，浏览器地址栏的URL类似这样：[https://www.growingio.com/projects/nxog09md/mp/marketing-automation/manage/product/configuration/QPDM8loN](https://www.growingio.com/projects/nxog09md/mp/marketing-automation/manage/product/configuration/QPDM8loN)，最后面的"QPDM8loN"就是productId。

## 4. 接口说明

地址：POST    https://www.growingio.com/api/v1/projects/:project\_id/meta/marketing\_push

**请求头\(http header\)：**

| 字段名 | 是否必传 | 说明 | 示例 |
| :--- | :--- | :--- | :--- |
| Content-Type | 是 | 固定传json类型 | application/json |
| X-Client-Id | 是 | 项目公钥，参考上面认证部分的文档 | 06b3f5ec564f590eb7435a8940c4f431 |
| Authorization | 是 | Token+空格+真正的token，获取方式参考上面认证部分的文档 | Token J8GL8w3gXUyZGMlEhme3acaCJKAHryzASR1WuHu2DrbUOS89HzaDdHIjCbizdgS8 |

**请求对象：**

| 字段名 | 字段格式 | 是否必传 | 说明 | 限制 | 示例 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| cid | 字符串 | 是 | cid 用于标示同一批推送消息。cid 相同的推送消息会聚合到同一个消息记录里，便于后续查看数据。同一个cid，同样的请求参数推送服务器不会生成新的推送任务，用于防止 api 调用端重试造成服务端的重复推送。建议使用 UUID 。 | 长度不超过64个字符 | 61b757af-f877-4e15-84f2-0f0eef69277c |
| name | 字符串 | 是 | 推送名称。建议使用 业务含义名称 + 时间戳 ，不可重复，便于在管理后台查看使用。 | 长度不超过200个字符 | 用户召回推送20190716170520 |
| packageName | 字符串 | 是 | 推送应用包名。可以在应用管理后台获取，注意 sdk 上传的包名需要和后台配置的一致！ |  | com.growingio.PushTest |
| productId | 字符串 | 是 | 推送应用唯一标示，因为packageName苹果和安卓可能重复，使用productId能唯一标识出一个应用 |  | QPDM8loN |
| audience | 字符串数组 | 是 | 推送目标列表。 |  | 登录用户ID。一次推送最多 2000 个。 |
| notification | 对象 | 是 | 推送消息体。 |  | - |
| options | 对象 | 是 | 推送配置项。 |  | - |

**使用建议：**

* 推送目标放在audience字段里，填入接入方系统里的登录用户ID，登录用户ID的含义可以参考这个文档：[https://docs.growingio.com/docs/data-model/user-model/loginuser](https://docs.growingio.com/docs/data-model/user-model/loginuser)。再重申一下，就是接入SDK时上报的ID，理论上这个ID应该存储于接入方系统的数据库中。
* 推送目标用户如果小于等于2000个，可以将所有目标设备标识放到一个请求里批量推送，推送完成之后建议更换cid和消息内容再进行下次推送。
* 推送目标用户如果大于2000个，需要分批推送，每批目标设备标识个数小于等于2000，保证这些批次的cid相同和消息体内容相同，这样才能将这些批次的请求聚合，方便后续在web端查看消息状态**。**

应用管理入口：

![](../../.gitbook/assets/banner.png)

**notification：**

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x5B57;&#x6BB5;&#x540D;</th>
      <th style="text-align:left">&#x5B57;&#x6BB5;&#x683C;&#x5F0F;</th>
      <th style="text-align:left">&#x662F;&#x5426;&#x5FC5;&#x4F20;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
      <th style="text-align:left">&#x9650;&#x5236;</th>
      <th style="text-align:left">&#x793A;&#x4F8B;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">title</td>
      <td style="text-align:left">&#x5B57;&#x7B26;&#x4E32;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">&#x901A;&#x77E5;&#x6807;&#x9898;&#x3002;</td>
      <td style="text-align:left">&#x957F;&#x5EA6;&#x4E0D;&#x8D85;&#x8FC7;20&#x4E2A;&#x5B57;&#x7B26;</td>
      <td
      style="text-align:left">&#x65B0;&#x6D88;&#x606F;&#x901A;&#x77E5;&#xFF01;</td>
    </tr>
    <tr>
      <td style="text-align:left">alert</td>
      <td style="text-align:left">&#x5B57;&#x7B26;&#x4E32;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">&#x901A;&#x77E5;&#x5185;&#x5BB9;&#x3002;</td>
      <td style="text-align:left">&#x957F;&#x5EA6;&#x4E0D;&#x8D85;&#x8FC7;50&#x4E2A;&#x5B57;&#x7B26;</td>
      <td
      style="text-align:left">&#x6536;&#x5230;&#x4E00;&#x6761;&#x65B0;&#x7684;&#x7559;&#x8A00;&#xFF0C;&#x70B9;&#x51FB;&#x67E5;&#x770B;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">extras</td>
      <td style="text-align:left">&#x5BF9;&#x8C61;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">&#x6269;&#x5C55;&#x5B57;&#x6BB5;&#xFF0C;&#x53EF;&#x4EE5;&#x81EA;&#x5B9A;&#x4E49;
        JSON &#x683C;&#x5F0F;&#x7684; Key / Value &#x4FE1;&#x606F;&#x3002;&#x8FD9;&#x4E2A;&#x5B57;&#x6BB5;&#x6682;&#x65F6;&#x4FDD;&#x7559;&#xFF0C;&#x53EF;&#x4EE5;&#x5148;&#x4F20;&#x7A7A;&#x5BF9;&#x8C61;&#x3002;</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left">{}</td>
    </tr>
    <tr>
      <td style="text-align:left">actionType</td>
      <td style="text-align:left">&#x5B57;&#x7B26;&#x4E32;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">
        <p>&#x70B9;&#x51FB;&#x8DF3;&#x8F6C;&#x94FE;&#x63A5;&#x7C7B;&#x578B;&#x3002;</p>
        <p>&#x6253;&#x5F00;&#x7F51;&#x9875;&#xFF1A;&quot;openH5&quot;</p>
        <p>&#x6253;&#x5F00;APP&#x5185;&#x5177;&#x4F53;&#x67D0;&#x4E2A;&#x9875;&#x9762;&#xFF1A;&quot;openUrl&quot;</p>
        <p>&#x81EA;&#x5B9A;&#x4E49;&#x534F;&#x8BAE;&#xFF1A;&quot;custom&quot;&#xFF0C;&#x81EA;&#x5B9A;&#x4E49;&#x534F;&#x8BAE;&#x9700;&#x8981;&#x5BA2;&#x6237;&#x901A;&#x8FC7;actionParameters&#x4F20;&#x53C2;&#x6570;&#x5E76;&#x89E3;&#x6790;</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">openUrl</td>
    </tr>
    <tr>
      <td style="text-align:left">actionTarget</td>
      <td style="text-align:left">&#x5B57;&#x7B26;&#x4E32;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">&#x70B9;&#x51FB;&#x8DF3;&#x8F6C;&#x8DEF;&#x5F84;&#x3002;</td>
      <td style="text-align:left"></td>
      <td style="text-align:left">com.growingio.push</td>
    </tr>
    <tr>
      <td style="text-align:left">actionParameters</td>
      <td style="text-align:left">&#x5BF9;&#x8C61;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">&#x70B9;&#x51FB;&#x8DF3;&#x8F6C;&#x643A;&#x5E26;&#x53C2;&#x6570;&#xFF0C;&#x4EE5;&#x952E;&#x503C;&#x5BF9;&#x5F62;&#x5F0F;&#x4F20;&#x9012;&#x3002;</td>
      <td
      style="text-align:left"></td>
        <td style="text-align:left">{&quot;key1&quot;: &quot;value1&quot;, &quot;key2&quot;: &quot;value2&quot;}</td>
    </tr>
  </tbody>
</table>

**options**

| 字段名 | 类型 | 说明 | 示例 |
| :--- | :--- | :--- | :--- |
| apnsProduction | 字符串 | true 表示推送生产环境，false 表示要推送开发环境；如果不指定则为推送生产环境。 | ture |

示例：

{% tabs %}
{% tab title="请求示例" %}
```yaml
{
	"cid": "61b757af-f877-4e15-84f2-0f0eef69277c",
	"name": "用户召回推送20190716170520",
	"packageName": "com.growingio.PushTest",
    "productId": "QPDM8loN",
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
{% endtab %}

{% tab title="成功返回示例" %}
| 字段名 | 字段格式 | 说明 | 示例 |
| :--- | :--- | :--- | :--- |
| cid | 字符串 | 请求参数里的 cid | 61b757af-f877-4e15-84f2-0f0eef69277c |
| taskId | 字符串 | 任务ID，智能运营模块API单播功能查询使用 | 6gzPgHlS |

```c
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

 Response Data  

{
  "cid" : "61b757af-f877-4e15-84f2-0f0eef69277c"
}
```
{% endtab %}

{% tab title="失败返回示例" %}
| 字段名 | 字段格式 | 说明 | 示例 |
| :--- | :--- | :--- | :--- |
| code | int | 错误码 | 1011 |
| message | string | 错误描述 | 请求速度过快，请稍后再试 |

```c
HTTP/1.1 400 OK
Content-Type: application/json; charset=utf-8

 Response Data  
 
{
  "code" : 1011
  "message" : "请求速度过快，请稍后再试"
}
```
{% endtab %}
{% endtabs %}

**错误码及原因对照表**

| 错误码 | 错误描述 | 备注 |
| :--- | :--- | :--- |
| 1001 | 请求body json校验不通过 |  |
| 1002 |  | 自定义异常，描述可能不同 |
| 1010 | 系统内部异常，请稍后再试 | 联系技术支持解决 |
| 1011 | 请求速度过快，请稍后再试 | API不要请求过快 |
| 1012 | API token校验不通过 |  |
| 1013 | 未找到项目 | 联系技术支持解决 |
| 1014 | 项目已被禁用 | 联系技术支持解决 |
| 1015 | 未找到对应产品，请检查参数packageName |  |
| 1016 | 重复请求，请检查参数 | 两次请求的参数不能一模一样 |
| 1017 | 目标用户推送必备参数为空 | 请参考推送FAQ\(**API推送任务1017**\)排查 |
| 1018 | 未知异常，请更换cid后重试 |  |

## 5. 推送数据

API创建推送暂不支持用户运营平台推送任务列表页查看，推送数据请使用「产品分析」-&gt; 「事件分析」查看，页面填写参数可参考如下：

触达推送名称（新旧版本可能存在GIO\_区别） 对应发送body中的name

![&#x901A;&#x8FC7;&#x4E8B;&#x4EF6;&#x5206;&#x6790;&#x67E5;&#x770B;API&#x63A8;&#x9001;&#x6570;&#x636E;](../../.gitbook/assets/image%20%28249%29.png)





