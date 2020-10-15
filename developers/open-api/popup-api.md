# 弹窗API

## 1. 概述

为满足广大客户更灵活创建弹窗的诉求，GrowingIO 提供了一套创建弹窗的API。本文档旨在说明一些调用流程，逻辑及相关接口说明。

## 2. 认证

为保证数据安全，GrowingIO所有的API服务，请求Head中需要携带 Token。

Token 获取详见：[GrowingIO接口认证](https://docs.growingio.com/v3/product-manual/projectmange/projectmange/api-token)

获取到 Token 后所有的 HTTP 请求头都需要带上 X-Client-Id 和 Authorization，具体如下：

| 名称 | 类型 | 描述 | 示例 |
| :--- | :--- | :--- | :--- |
| X-Client-Id | string | GrowingIO分配的公钥，请在GrowingIO后台“项目配置”页面获取 | X-Client-Id: 123abc |
| Authorization | string | 认证后获取到的Token | Authorization: {替换成获取到的Token} |

例子：

```swift
X-Client-Id: 7f8it37dxdt91x4n5cvuvccc1cgaqe21
Authorization:  EcWylTb23T5yoNMkna51VsyVfGovQHMVc1neljuK5TpqNTz9U5c9Z2BYZLUos244
```

## 3. 使用注意

1. 接口调用频率限制：单个 Token 调用限制 1200次/分钟。
2. 项目UID 指的是访问项目的时候，页面 URL 以 /projects/:project\_uid 开头，例如 https://www.growingio.com/admin/projects/nxog09md/dashboard 中的 "nxog09mx"。
3. 创建站内消息需要使用分群作为目标用户，分群获取接口参考文档：[获取分群列表](https://docs.growingio.com/docs/developer-manual/api-reference/statistics-api/definition/get-segm)
4. 创建消息需要指定对应应用的 ID，通过以下接口获得（请求Head中均需要携带Token ）

```aspnet
GET https://www.growingio.com/api/v1/projects/项目UID/meta/products
```

返回字段：

| 字段名 | 类型 | 说明 | 示例 |
| :--- | :--- | :--- | :--- |
| id | string | 产品编号 | GQPDxPNm |
| name | string | 名字 | GrowingIO测试产品 |
| displayName | string | 产品显示名称，展示在deeplink页面 | gio |
| activated | bool | 是否有效 | true |
| spn | string | spn | www.gioee.com |
| urlScheme | string | 产品的URL Scheme | 8137d31f4e7b819f |
| platform | string | 平台 | iOS |
| createdAt | long | 创建时间 | 1522019721098 |

5. 创建站内消息需要先上传素材到GrowingIO服务，参素材上传接口

6. 接口调用流程：

![](../../.gitbook/assets/liu-cheng.png)

## 4. 接口说明

### 接口：素材上传

URL：`https://www.growingio.com/api/v1/projects/:project_uid/meta/marketing_medias`

方法：POST

请求对象：

| 字段名 | 类型 | 说明 |
| :--- | :--- | :--- |
| file | 字符串 | 图片base64编码后的值。 |

请求示例：

```c
Headers: 
Content-Type: application/json
X-Client-Id: 7f8it37dxdt91x4n5cvuvccc1cgaqe22
Authorization: EcWylTb23T5yoNMkna51VsyVfGovQHMVc1

Request Body:
{
  "file":"data:image/jpeg;base64,......."
}
```

返回示例：

```c
{
 "url":"https://statics.growingio.com/media/20190813/3/1565873249372/test.jpeg"
 }
```

### 接口：创建消息

URL：`https://www.growingio.com/api/v1/projects/:project_uid/meta/marketing_in_app_messages`

方法**：**POST

请求对象：

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x5B57;&#x6BB5;&#x540D;</th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x662F;&#x5426;&#x5FC5;&#x586B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">name</td>
      <td style="text-align:left">&#x5B57;&#x7B26;&#x4E32;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">
        <p>&#x6D88;&#x606F;&#x540D;&#x79F0;&#x3002;&#x5EFA;&#x8BAE;&#x4F7F;&#x7528;&#x4E1A;&#x52A1;&#x542B;&#x4E49;&#x540D;&#x79F0;+&#x65F6;&#x95F4;&#x6233;&#xFF0C;&#x4E0D;&#x53EF;&#x91CD;&#x590D;&#xFF0C;&#x4FBF;&#x4E8E;&#x5728;&#x7BA1;&#x7406;&#x540E;&#x53F0;&#x67E5;&#x770B;&#x4F7F;&#x7528;&#x3002;</p>
        <p>&#x793A;&#x4F8B;&#xFF1A;&#x7528;&#x6237;&#x53EC;&#x56DE;&#x5F39;&#x7A97;20190716170520</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">audience</td>
      <td style="text-align:left">&#x5B57;&#x7B26;&#x4E32;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">
        <p>&#x76EE;&#x6807;&#x4EBA;&#x7FA4;&#x3002;</p>
        <p>&#x5206;&#x7FA4;&#xFF1A;&#x5206;&#x7FA4; id</p>
        <p>&#x8BBF;&#x95EE;&#x7528;&#x6237;&#xFF1A;visitors</p>
        <p>&#x65B0;&#x8BBF;&#x95EE;&#x7528;&#x6237;&#xFF1A;newVisitors</p>
        <p>&#x767B;&#x9646;&#x7528;&#x6237;&#xFF1A;loginUsers</p>
        <p>&#x65B0;&#x767B;&#x5F55;&#x7528;&#x6237;&#xFF1A;newLoginUsers</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">rule</td>
      <td style="text-align:left">&#x5BF9;&#x8C61;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">&#x6D88;&#x606F;&#x89E6;&#x53D1;&#x89C4;&#x5219;&#x914D;&#x7F6E;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">state</td>
      <td style="text-align:left">&#x5B57;&#x7B26;&#x4E32;</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">
        <p>activated&#xFF1A;&#x4E0A;&#x7EBF;&#xFF08;&#x9ED8;&#x8BA4;&#xFF09;</p>
        <p>draft&#xFF1A;&#x8349;&#x7A3F;</p>
        <p>stop&#xFF1A;&#x4E0B;&#x7EBF;</p>
        <p>archived&#xFF1A;&#x5F52;&#x6863;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">content</td>
      <td style="text-align:left">&#x5BF9;&#x8C61;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">&#x6D88;&#x606F;&#x7D20;&#x6750;&#xFF0C;&#x56FE;&#x7247;&#x7684;&#x5730;&#x5740;&#x3002;</td>
    </tr>
  </tbody>
</table>

rule

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x5B57;&#x6BB5;&#x540D;</th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x662F;&#x5426;&#x5FC5;&#x586B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">targets</td>
      <td style="text-align:left">&#x5BF9;&#x8C61;&#x6570;&#x7EC4;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">&#x6307;&#x5B9A;&#x4EA7;&#x54C1;&#x548C;&#x8DF3;&#x8F6C;&#x9875;&#x9762;&#x7684;&#x5173;&#x7CFB;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">action</td>
      <td style="text-align:left">&#x5B57;&#x7B26;&#x4E32;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">
        <p>&#x6253;&#x5F00;&#x5E94;&#x7528;&#xFF1A;appOpen</p>
        <p>&#x81EA;&#x5B9A;&#x4E49;&#x57CB;&#x70B9;&#x4E8B;&#x4EF6;&#xFF1A;&#x4E8B;&#x4EF6;key</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">limit</td>
      <td style="text-align:left">&#x6570;&#x5B57;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">&#x672C;&#x6761;&#x6D88;&#x606F;&#x6700;&#x5927;&#x5C55;&#x793A;&#x6B21;&#x6570;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">startAt</td>
      <td style="text-align:left">&#x6570;&#x5B57;</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">&#x9884;&#x7EA6;&#x4E0A;&#x7EBF;&#x8D77;&#x59CB;&#x65F6;&#x95F4;&#xFF0C;unix&#x65F6;&#x95F4;&#x6233;</td>
    </tr>
    <tr>
      <td style="text-align:left">endAt</td>
      <td style="text-align:left">&#x6570;&#x5B57;</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">&#x9884;&#x7EA6;&#x4E0B;&#x7EBF;&#x65F6;&#x95F4;unix&#x65F6;&#x95F4;&#x6233;</td>
    </tr>
    <tr>
      <td style="text-align:left">triggerCd</td>
      <td style="text-align:left">&#x6570;&#x5B57;</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">&#x672C;&#x6761;&#x6D88;&#x606F;&#x5C55;&#x793A;&#x95F4;&#x9694;&#xFF0C;&#x5355;&#x4F4D;&#x79D2;&#x3002;</td>
    </tr>
  </tbody>
</table>

targets里每个target的结构：

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x5B57;&#x6BB5;&#x540D;</th>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x662F;&#x5426;&#x5FC5;&#x4F20;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">productId</td>
      <td style="text-align:left">&#x5B57;&#x7B26;&#x4E32;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">&#x4EA7;&#x54C1;ID&#xFF0C;&#x4ECE;&#x4E0A;&#x9762;&#x7684;&#x4EA7;&#x54C1;&#x4FE1;&#x606F;&#x63A5;&#x53E3;&#x83B7;&#x53D6;</td>
    </tr>
    <tr>
      <td style="text-align:left">type</td>
      <td style="text-align:left">&#x5B57;&#x7B26;&#x4E32;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">
        <p>&#x70B9;&#x51FB;&#x8F6C;&#x8DF3;&#x94FE;&#x63A5;&#x7C7B;&#x578B;&#x3002;</p>
        <p>&#x6253;&#x5F00;&#x7F51;&#x9875;&#xFF1A;&#x201C;openH5&#x201D;</p>
        <p>&#x6253;&#x5F00;&#x5E94;&#x7528;&#x5185;&#x5177;&#x4F53;&#x9875;&#x9762;&#xFF1A;&#x201C;openUrl&#x201D;</p>
        <p>&#x81EA;&#x5B9A;&#x4E49;&#x53C2;&#x6570;&#xFF1A;&#x201C;custom&#x201D;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">url</td>
      <td style="text-align:left">&#x5B57;&#x7B26;&#x4E32;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">
        <p>&#x70B9;&#x51FB;&#x8DF3;&#x8F6C;&#x8DEF;&#x5F84;&#x3002;&#x7F51;&#x9875;&#x9700;&#x8981;&#x5236;&#x5B9A;&#x5177;&#x4F53;&#x534F;&#x8BAE;&#xFF0C;&#x652F;&#x6301;
          http/https&#x3002;</p>
        <p>&#x793A;&#x4F8B;&#xFF1A;com.growingio.push &#x6216;&#x8005;</p>
        <p>https://www.gio.com</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">parameters</td>
      <td style="text-align:left">&#x5BF9;&#x8C61;</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">
        <p>&#x70B9;&#x51FB;&#x8DF3;&#x8F6C;&#x643A;&#x5E26;&#x53C2;&#x6570;&#xFF0C;&#x4EE5;
          queryString &#x7684;&#x5F62;&#x5F0F;&#x6DFB;&#x52A0;&#x5230; url &#x540E;&#x9762;&#x3002;&#x6BD4;&#x5982;
          {&quot;key1&quot;: &quot;value1&quot;} &#x4F1A;&#x8F6C;&#x5316;&#x4E3A;
          &quot;?key1=value1&quot; &#x6DFB;&#x52A0;&#x5230; url &#x540E;&#x3002;</p>
        <p>&#x793A;&#x4F8B;&#xFF1A;{&quot;key1&quot;: &quot;value1&quot;, &quot;key2&quot;:
          &quot;value2&quot;}</p>
      </td>
    </tr>
  </tbody>
</table>

请求示例：

```c
Headers: 
Content-Type: application/json
X-Client-Id: 7f8it37dxdt91x4n5cvuvccc1cgaqe22
Authorization: EcWylTb23T5yoNMkna51VsyVfGovQHMVc1

Request Body:
{
	"name": "用户召回弹窗",
	"audience": "nPNYj7aR",
	"rule": {
		"targets": [{
				"productId": "L9GcmZo6",
				"type": "openUrl",
				"url": "MainActivity",
				"parameters": {
					"key1": "value1",
					"key2": "value2"
				}
			},
			{
				"productId": "a9xVmZo5",
				"type": "openUrl",
				"url": "ViewController",
				"parameters": {
					"key1": "value1",
					"key2": "value2"
				}
			}
		],
		"action": "appOpen",
		"limit": 2,
		"startAt": 1565870400000,
		"triggerCd": 86400
	},
	"content": "https://k8s-statics.growingio.com/media/20190523/3/1558601993407/test.png"
}
```

返回示例：

| 字段名 | 类型 | 说明 | 示例 |
| :--- | :--- | :--- | :--- |
| id | 字符串 | 消息ID | xL9GWJ96 |

```c
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

 Response Data  

{
  "id" : "wL9GWJ96"
}
```

### 接口：更新消息

URL：`https://www.growingio.com/api/v1/projects/:project_uid/meta/marketing_in_app_messages/:message_id`

方法：PUT

请求体：同创建消息

### 接口：删除消息

URL:`https://www.growingio.com/api/v1/projects/:project_uid/meta/marketing_in_app_messages/:message_id`

方法：DELETE

```swift
Headers: 
Content-Type: application/json
X-Client-Id: 7f8it37dxdt91x4n5cvuvccc1cgaqe22
Authorization: EcWylTb23T5yoNMkna51VsyVfGovQHMVc1
```

返回：

```swift
HTTP/1.1 204 No Content
```

### 接口：获取所有消息

URL： `https://www.growingio.com/api/v1/projects/:project_uid/meta/marketing_in_app_messages`

方法：GET

```swift
Headers: 
Content-Type: application/json
X-Client-Id: 7f8it37dxdt91x4n5cvuvccc1cgaqe22
Authorization: EcWylTb23T5yoNMkna51VsyVfGovQHMVc1
```

返回：消息列表



