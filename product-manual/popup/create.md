# 创建弹窗

进入**用户运营**模块，在顶部导航栏选择**运营**。

当前支持配置以下应用的弹窗：

{% tabs %}
{% tab title="网站" %}
一. 单击界面左上角的**新建**，选择**弹窗**，再选择**网站**。

二. 选择目标分群。

![](../../.gitbook/assets/image.png)

选择要发送弹窗的目标用户。可使用创建好的用户分群。

{% hint style="success" %}
**用户分群**

* 直接选择之前创建过的分群（创建好的用户分群每天凌晨会按照条件跑一遍分群数据），这种方式会有T+1的延时）用户次日访问App时会判断该用户是否在某个分群中，满足条件弹出。
* 但如果选择四种预定义分群：全部登录用户，全部访问用户，新登录用户，新访问用户，在弹窗SDK中是实时判断的。比如选择新登录用户，那么每个打开App的用户，弹窗 SDK 都会实时判断该用户是否为新登陆的用户。
{% endhint %}

三. 触发和素材。

![](../../.gitbook/assets/image%20%28179%29.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x53C2;&#x6570;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#x89E6;&#x53D1;&#x9875;&#x9762;</td>
      <td style="text-align:left">
        <p>&#x662F;&#x6307;&#xFF0C;&#x5F53;&#x7528;&#x6237;&#x5230;&#x8FBE;&#x54EA;&#x4E2A;/&#x4E9B;&#x9875;&#x9762;&#x7684;&#x65F6;&#x5019;&#xFF0C;&#x5F39;&#x51FA;&#x5F39;&#x7A97;&#x3002;&#x6DFB;&#x52A0;&#x591A;&#x4E2A;&#x6761;&#x4EF6;&#x65F6;&#xFF0C;&#x610F;&#x5473;&#x7740;&#x7528;&#x6237;&#x53EA;&#x8981;&#x5230;&#x8FBE;&#x5176;&#x4E2D;&#x4EFB;&#x610F;&#x4E00;&#x4E2A;&#x9875;&#x9762;&#xFF0C;&#x90FD;&#x4F1A;&#x5F39;&#x51FA;&#x5F39;&#x7A97;&#x3002;</p>
        <p>&#x6BD4;&#x5982;&#xFF0C;</p>
        <ul>
          <li>&#x652F;&#x6301;<b>&#x7279;&#x5B9A;&#x9875;&#x9762;</b>&#xFF1A;&#x4F60;&#x60F3;&#x5728;&#x7528;&#x6237;&#x5230;&#x8FBE;
            www.growingio.com &#x9875;&#x9762;&#x65F6;&#x53D1;&#x9001;&#x5F39;&#x7A97;&#xFF0C;&#x5C31;&#x53EF;&#x4EE5;&#x5C06;&#x8FD9;&#x4E2A;&#x9875;&#x9762;
            www.growingio.com &#x8F93;&#x5165;&#x8FDB;&#x53BB;&#x3002;</li>
          <li>&#x652F;&#x6301;<b>&#x9875;&#x9762;&#x7EC4;&#x901A;&#x914D;&#x7B26;</b>&#xFF1A;&#x5982;&#x679C;&#x4F60;&#x60F3;&#x5728;&#x7528;&#x6237;&#x5230;&#x8FBE;
            www.growingio.com &#x57DF;&#x540D;&#x4E0B;&#x6240;&#x6709;&#x9875;&#x9762;&#x65F6;&#x53D1;&#x9001;&#x5F39;&#x7A97;&#xFF0C;&#x53EF;&#x4EE5;&#x8F93;&#x5165;
            www.growingio.com*&#x3002;</li>
          <li>&#x652F;&#x6301;<b>&#x591A;&#x4E2A;&#x9875;&#x9762;&#x7EC4;&#x5408;</b>&#xFF1A;&#x4F60;&#x60F3;&#x5728;&#x7528;&#x6237;&#x5230;&#x8FBE;
            www.growingio.com/1 &#x548C; www.growingio.com/2 &#x65F6;&#x89E6;&#x53D1;&#xFF0C;&#x53EF;&#x4EE5;&#x901A;&#x8FC7;<b>&#x589E;&#x52A0;URL</b>&#x6309;&#x94AE;&#x8F93;&#x5165;&#x4E24;&#x4E2A;URL&#x3002;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x89E6;&#x53D1;&#x65F6;&#x673A;</td>
      <td style="text-align:left">
        <p></p>
        <p>&#x5C31;&#x662F;&#x7528;&#x6237;&#x4F1A;&#x5728;&#x4EC0;&#x4E48;&#x65F6;&#x95F4;&#x770B;&#x5230;&#x8FD9;&#x4E2A;&#x5F39;&#x7A97;&#xFF1F;</p>
        <p>&#x9ED8;&#x8BA4;&#x89E6;&#x53D1;&#x65F6;&#x673A;&#x4E3A;&#x300C;<b>&#x9875;&#x9762;&#x6253;&#x5F00;</b>&#x300D;&#x65F6;&#xFF0C;&#x4E5F;&#x53EF;&#x4EE5;&#x9009;&#x62E9;&#x5176;&#x4ED6;&#x4E8B;&#x4EF6;&#x4F5C;&#x4E3A;&#x89E6;&#x53D1;&#x65F6;&#x673A;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x5EF6;&#x8FDF;&#x8BBE;&#x7F6E;</td>
      <td style="text-align:left">&#x8BBE;&#x7F6E;&#x5F39;&#x7A97;&#x5728;&#x6EE1;&#x8DB3;&#x89E6;&#x53D1;&#x6761;&#x4EF6;&#x540E;&#x7684;&#x5EF6;&#x8FDF;&#x5F39;&#x51FA;&#x65F6;&#x95F4;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x89E6;&#x53D1;&#x6B21;&#x6570;</td>
      <td style="text-align:left">
        <p>&#x5F39;&#x7A97;&#x7684;&#x89E6;&#x53D1;&#x9891;&#x7387;&#x53EF;&#x4EE5;&#x8BBE;&#x7F6E;&#x4E3A;&#x53EA;&#x89E6;&#x53D1;
          1 &#x6B21;&#xFF0C;&#x6216;&#x662F;&#x591A;&#x6B21;&#x3002;</p>
        <p>&#x5982;&#x679C;&#x8BBE;&#x7F6E;&#x591A;&#x6B21;&#x89E6;&#x53D1;&#xFF0C;&#x9700;&#x8981;&#x5B9A;&#x4E49;&#x89E6;&#x53D1;&#x6B21;&#x6570;&#x4E0A;&#x9650;&#xFF0C;&#x4EE5;&#x53CA;&#x6BCF;&#x6B21;&#x7684;&#x95F4;&#x9694;&#x65F6;&#x95F4;&#x3002;</p>
        <p>&#x53EA;&#x8981;&#x7528;&#x6237;&#x6CA1;&#x6709;&#x70B9;&#x51FB;&#x67E5;&#x770B;&#x5F39;&#x7A97;&#x6216;&#x8005;&#x5173;&#x95ED;&#x5F39;&#x7A97;&#xFF0C;&#x4E14;&#x89E6;&#x53D1;&#x6B21;&#x6570;&#x6CA1;&#x6709;&#x8FBE;&#x5230;&#x4E0A;&#x9650;&#x5C31;&#x4F1A;&#x518D;&#x6B21;&#x89E6;&#x53D1;&#x3002;</p>
      </td>
    </tr>
  </tbody>
</table>{% hint style="info" %}
**触发时机注意事项**

如果运营人员选择了 「**打开App时**」 弹出。 需要注意：如果您的 App 包含闪屏页面，那么代码层面需要做特殊处理。因为 SDK 并不能判断闪屏什么时候结束。 为了避免在闪屏页面出现弹窗，有两种处理方法：

处理方法1：

* 在需要弹出的页面埋点，运营人员在下拉框中选择相应的埋点事件作为触发时机。这种方法可以精准的控制弹出时机。

处理方法2：

* 在 App onCreate 的时候设置关闭弹窗。使用 GrowingTouch.startWithConfig\(this, new GTouchConfig\(\) .setEventPopupEnable\(false\) 
* 然后再在首页MainActivity中调用 enableEventPopupAndGenerateAppOpenEvent 或者setEventPopupEnable\(true\)
{% endhint %}

埋点事件如何创建请参见：数据定义 &gt; [埋点事件及事件级变量](https://docs.growingio.com/docs/introduction/data-definition/ustom-event/event)。

四. 弹窗样式。

![](../../.gitbook/assets/image%20%28219%29.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x53C2;&#x6570;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#x56FE;&#x7247;&#x4E0A;&#x4F20;</td>
      <td style="text-align:left">&#x4E0A;&#x4F20;&#x60A8;&#x8981;&#x5728;Web&#x9875;&#x9762;&#x5F39;&#x7A97;&#x5C55;&#x793A;&#x7684;&#x56FE;&#x7247;&#xFF0C;&#x5927;&#x5C0F;&#x4E0D;&#x5F97;&#x8D85;&#x8FC7;500KB&#x3002;&#x4E0A;&#x4F20;&#x60A8;&#x53EF;&#x4EE5;&#x5728;&#x56FE;&#x7247;&#x4E0A;&#x4F20;&#x533A;&#x57DF;&#x9009;&#x586B;&#x6807;&#x9898;&#x548C;&#x90E8;&#x5206;&#x6587;&#x672C;&#x5185;&#x5BB9;&#x53CA;&#x4FEE;&#x6539;&#x6309;&#x94AE;&#x6587;&#x672C;&#x3002;&#x4E0A;&#x4F20;&#x7684;&#x56FE;&#x7247;&#x4F1A;&#x6839;&#x636E;&#x5F39;&#x7A97;&#x4F4D;&#x7F6E;&#x8FDB;&#x884C;&#x9AD8;&#x5EA6;&#x81EA;&#x9002;&#x5E94;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x5F39;&#x7A97;&#x4F4D;&#x7F6E;</td>
      <td style="text-align:left">
        <p>&#x5C4F;&#x5E55;&#x5C45;&#x4E2D;&#xFF1A;&#x5BBD;&#x5EA6;500px&#xFF0C;&#x4F4D;&#x7F6E;&#x4E3A;&#x5C4F;&#x5E55;&#x4E2D;&#x95F4;&#x7684;&#x5F39;&#x7A97;&#xFF0C;&#x5C06;&#x4F1A;&#x4E2D;&#x6B62;&#x7528;&#x6237;&#x5F53;&#x524D;&#x7684;&#x64CD;&#x4F5C;&#xFF0C;&#x9002;&#x7528;&#x4E8E;&#x6BD4;&#x8F83;&#x91CD;&#x7684;&#x63D0;&#x793A;&#x3002;</p>
        <p>&#x5C4F;&#x5E55;&#x5DE6;&#x5C0F;&#x89D2;/&#x5C4F;&#x5E55;&#x53F3;&#x4E0B;&#x89D2;&#xFF1A;&#x5BBD;&#x5EA6;344px&#xFF0C;&#x9002;&#x7528;&#x4E8E;&#x8F7B;&#x8F7B;&#x7684;&#x63D0;&#x9192;&#xFF0C;&#x7528;&#x6237;&#x4ECD;&#x7136;&#x53EF;&#x4EE5;&#x7EE7;&#x7EED;&#x64CD;&#x4F5C;&#xFF0C;&#x5F53;&#x7528;&#x6237;&#x7FFB;&#x9875;&#x5237;&#x65B0;&#x6216;&#x5BF9;&#x5F39;&#x7A97;&#x8FDB;&#x884C;&#x64CD;&#x4F5C;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x8F6C;&#x8DF3;&#x914D;&#x7F6E;</td>
      <td style="text-align:left">
        <p>&#x8F6C;&#x8DF3;&#x6309;&#x94AE;&#xFF1A;</p>
        <ul>
          <li>&#x8F6C;&#x8DF3;&#x6309;&#x94AE;&#xFF1A;&#x8BBE;&#x7F6E;&#x8F6C;&#x8DF3;&#x94FE;&#x63A5;&#xFF0C;&#x7528;&#x6237;&#x5355;&#x51FB;&#x6309;&#x94AE;&#x65F6;&#x4F1A;&#x8FDB;&#x884C;&#x8F6C;&#x8DF3;&#x3002;</li>
          <li>&#x590D;&#x5236;&#x6309;&#x94AE;&#xFF1A;&#x8BBE;&#x7F6E;&#x6587;&#x672C;&#x5185;&#x5BB9;&#xFF0C;&#x7528;&#x6237;&#x5355;&#x51FB;&#x6309;&#x94AE;&#x65F6;&#x4F1A;&#x590D;&#x5236;&#x6587;&#x6863;&#x3002;</li>
        </ul>
        <p>&#x56FE;&#x7247;&#x8F6C;&#x8DF3;&#xFF1A;&#x8BBE;&#x7F6E;&#x8F6C;&#x8DF3;&#x94FE;&#x63A5;&#xFF0C;&#x7528;&#x6237;&#x5355;&#x51FB;&#x56FE;&#x7247;&#x65F6;&#x8FDB;&#x884C;&#x8F6C;&#x8DF3;&#x3002;</p>
      </td>
    </tr>
  </tbody>
</table>四. 测试和上线。

![](../../.gitbook/assets/image%20%2839%29.png)

配置完二、三步骤后，单击保存即可进行测试和上线。

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x53C2;&#x6570;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#x6D4B;&#x8BD5;&#x6548;&#x679C;</td>
      <td style="text-align:left">&#x5355;&#x51FB;&#x6D4B;&#x8BD5;&#x6548;&#x679C;&#x53F3;&#x4FA7;&#x7684;&#x67E5;&#x770B;&#xFF0C;&#x4F1A;&#x8F6C;&#x8DF3;&#x5230;&#x5F39;&#x7A97;&#x9875;&#x9762;&#x5C55;&#x793A;&#x5F39;&#x7A97;&#x6548;&#x679C;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x4E0A;&#x7EBF;&#x65F6;&#x95F4;&#x914D;&#x7F6E;</td>
      <td style="text-align:left">
        <p></p>
        <p>&#x60A8;&#x53EF;&#x4EE5;&#x914D;&#x7F6E;&#x5F39;&#x7A97;&#x4E0A;&#x4E0B;&#x7EBF;&#x65F6;&#x95F4;&#x3002;</p>
      </td>
    </tr>
  </tbody>
</table>五. 配置完成后单击**上线**。
{% endtab %}

{% tab title="移动应用" %}
{% hint style="info" %}
本页内容不包含添加分群/控制组对比、添加素材对比、添加活动对比的配置，相关配置请参考[A/B测试](ab-experiment.md)。
{% endhint %}

一. 单击界面左上角的**新建**，选择**弹窗**，再选择**移动应用**。

二. 选择目标分群。



选择要发送弹窗的目标用户。可使用创建好的用户分群和或使用用户属性来筛选用户。

* **用户分群**

直接选择之前创建过的分群（创建好的用户分群每天凌晨会按照条件跑一遍分群数据），这种方式会有T+1的延时）用户次日访问App时会判断该用户是否在某个分群中，满足条件弹出。

但如果选择四种预定义分群：全部登录用户，全部访问用户，新登录用户，新访问用户，在弹窗SDK中是实时判断的。比如选择新登录用户，那么每个打开App的用户，弹窗 SDK 都会实时判断该用户是否为新登陆的用户。

* **用户属性**

> SDK版本要求：&gt;=0.3.0；在触发自定义事件之前，请确保已经上传过登录用变量。

通过用户属性的筛选，可以实时的判断用户在访问App时是否命中条件。

{% hint style="success" %}
弹窗 SDK 1.2.0 为移动应用新增登录用户属性：注册至今（天）。

如需使用您需上传用户注册时间，请参考：iOS SDK &gt; 弹窗SDK集成&gt; [设置用户登录时间](../../developers/integrations/ios-sdk/popup-component.md#5-she-zhi-yong-hu-zhu-ce-shi-jian) 或 Android SDK &gt; 弹窗SDK集成&gt; [设置用户登录时间](../../developers/integrations/android-sdk/popup-component.md#6-she-zhi-yong-hu-zhu-ce-shi-jian)。
{% endhint %}

* **产品选择**

您可以最多选择一个 Android 端和一个 iOS 端 App。

三. 选择触发条件和上传素材。

![](../../.gitbook/assets/image%20%28186%29.png)

* **触发时机**

就是用户会在什么时间看到这个弹窗？

默认触发时机为「**打开App时**」，也可以选择其他事件作为触发时机。

{% hint style="info" %}
如果运营人员选择了 「**打开App时**」 弹出。 需要注意：如果您的 App 包含闪屏页面，那么代码层面需要做特殊处理。因为 SDK 并不能判断闪屏什么时候结束。 为了避免在闪屏页面出现弹窗，有两种处理方法：

处理方法1：

* 在需要弹出的页面埋点，运营人员在下拉框中选择相应的埋点事件作为触发时机。这种方法可以精准的控制弹出时机。

处理方法2：

* 在 App onCreate 的时候设置关闭弹窗。使用 GrowingTouch.startWithConfig\(this, new GTouchConfig\(\) .setEventPopupEnable\(false\) 
* 然后再在首页MainActivity中调用 enableEventPopupAndGenerateAppOpenEvent 或者setEventPopupEnable\(true\)
{% endhint %}

埋点事件如何创建请参见：数据定义 &gt; [埋点事件及事件级变量](https://docs.growingio.com/docs/introduction/data-definition/ustom-event/event)。

* **触发次数**

弹窗的触发频率可以设置为只触发 1 次，或是多次。

如果设置多次触发，需要定义触发次数上限，以及每次的间隔时间。

{% hint style="info" %}
**触发说明**

只要用户没有点击查看弹窗或者关闭弹窗，且触发次数没有达到上限就会再次触发。
{% endhint %}

* **图片素材**

上传不超过500KB大小的背景图片素材，如果有需要可以使用 [tinypng](https://tinypng.com/) 等在线网站进行压缩，或者让设计师直接做出这个大小的图片。

{% hint style="success" %}
素材建议大小：

iPhone8 的屏幕宽度是375px。所以弹窗素材宽度在300px至330px左右，高度250px至600px左右，都是合适大小。GIO 弹窗不会拉伸用户上传的图片，会保证原始比例。为保证清晰度，请导出@2x或@3x的图片。
{% endhint %}

GIO 弹窗支持带有透明度的 PNG 格式图片，所以可以做任何形状，不一定要拘泥于矩形。

实践经验表明，弹窗做的越好看，愿意点击的用户越多哦！

![](../../.gitbook/assets/tips.png)

* **转跳页面**

用户点击弹窗后，跳转到哪个页面呢？

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">App&#x539F;&#x751F;&#x9875;</td>
      <td style="text-align:left">
        <p></p>
        <p>&#x539F;&#x751F;&#x9875;&#x9762;&#x8DF3;&#x8F6C;&#x94FE;&#x63A5;&#x662F;&#x7684;&#x683C;&#x5F0F;&#x4E3A; <code>classname?key1=value1&amp;key2=value2</code>&#xFF0C;&#x8BF7;&#x4E0E;&#x5F00;&#x53D1;&#x540C;&#x5B66;&#x786E;&#x8BA4;&#xFF08;&#x524D;&#x9762;&#x4E0D;&#x9700;&#x8981;&#x52A0;&#x534F;&#x8BAE;&#x540D;&#xFF0C;GIO&#x4F1A;&#x9ED8;&#x8BA4;&#x52A0;&#x4E0A;&#x81EA;&#x5DF1;&#x7684;&#x534F;&#x8BAE;&#x5934;&#xFF09;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">H5&#x9875;&#x9762;</td>
      <td style="text-align:left">&#x52A0;&#x4E0A; http:// &#x6216; https:// &#x5F00;&#x5934;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x81EA;&#x5B9A;&#x4E49;&#x534F;&#x8BAE;</td>
      <td style="text-align:left">&#x4EFB;&#x4F55;&#x60A8;&#x81EA;&#x5DF1;&#x7684;&#x534F;&#x8BAE;&#x5934;&#x90FD;&#x53EF;&#x4EE5;&#xFF08;&#x63A8;&#x8350;&#x8FD9;&#x79CD;&#x65B9;&#x5F0F;&#xFF0C;&#x66F4;&#x7075;&#x6D3B;&#xFF09;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x4E0D;&#x586B;&#x5199;</td>
      <td style="text-align:left">&#x5219;&#x9ED8;&#x8BA4;&#x4F5C;&#x4E3A;&#x5C55;&#x793A;&#x7528;&#xFF0C;&#x70B9;&#x51FB;&#x540E;&#x5173;&#x95ED;&#x5F39;&#x7A97;</td>
    </tr>
  </tbody>
</table>四. 测试和上线。

![](../../.gitbook/assets/image%20%289%29.png)

配置完二、三步骤后，单击保存即可进行测试和上线。

**扫码测试**：选择需要测试的 App ，使用包含有 **安装了弹窗 SDK 的 App** 的设备进行扫码唤醒 App ，进行测试。为了更方便的供测试者查看弹窗效果，不管扫码的设备是否在分群中，都会在相应的时机弹出弹窗。

**上线时间配置：**您可以配置弹窗上下线时间。

五. 配置完成后单击**上线**。
{% endtab %}

{% tab title="小程序" %}
一. 单击界面左上角的**新建**，选择**弹窗**，再选择**小程序**。

二. 选择目标分群。

![](../../.gitbook/assets/image%20%2898%29.png)

选择要发送弹窗的目标用户。可使用创建好的用户分群。

* **用户分群**

直接选择之前创建过的分群（创建好的用户分群每天凌晨会按照条件跑一遍分群数据），这种方式会有T+1的延 时）用户次日访问App时会判断该用户是否在某个分群中，满足条件弹出。

但如果选择四种预定义分群：全部登录用户，全部访问用户，新登录用户，新访问用户，在触达中是实时判断的。比如选择新登录用户，那么每个打开App的用户，触达 SDK 都会实时判断该用户是否为新登陆的用户。

* **产品选择**

您可以最多选择一个 微信小程序。

三. 选择触发条件和上传素材。

![](../../.gitbook/assets/image%20%2855%29.png)

* **触发时机**

就是用户会在什么时间看到这个弹窗？

默认触发时机为「**打开App时**」，也可以选择其他事件作为触发时机。

埋点事件如何创建请参见：数据定义 &gt; [埋点事件及事件级变量](https://docs.growingio.com/docs/introduction/data-definition/ustom-event/event)。

* **触发次数**

弹窗的触发频率可以设置为只触发 1 次，或是多次。

如果设置多次触发，需要定义触发次数上限，以及每次的间隔时间。

{% hint style="info" %}
**触发说明**

只要用户没有点击查看弹窗或者关闭弹窗，且触发次数没有达到上限就会再次触发。
{% endhint %}

* **图片素材**

上传不超过500KB大小的背景图片素材（允许包含透明度）

{% hint style="success" %}
图片处理建议

如果有需要可以使用 [tinypng](https://tinypng.com/) 等在线网站进行压缩，或者让设计师直接做出这个大小的图片。
{% endhint %}

* **点击转跳页面**

设置点击该弹窗会转跳的页面，可以为空。

四. 测试和上线。

![](../../.gitbook/assets/image%20%28216%29.png)

配置完二、三步骤后，单击保存即可进行测试和上线。

**扫码测试**：选择需要测试的 App ，使用包含有 **安装了弹窗 SDK 的 App** 的设备进行扫码唤醒 App ，进行测试。为了更方便的供测试者查看弹窗效果，不管扫码的设备是否在分群中，都会在相应的时机弹出弹窗。

**上线时间配置：**您可以配置弹窗上下线时间。

五. 配置完成后单击**上线**。
{% endtab %}

{% tab title="H5应用" %}
一. 单击界面左上角的**新建**，选择**弹窗**，再选择**H5应用**。

二. 选择目标分群。

![](../../.gitbook/assets/image%20%2837%29.png)

选择要发送弹窗的目标用户。可使用创建好的用户分群。

* **用户分群**

直接选择之前创建过的分群（创建好的用户分群每天凌晨会按照条件跑一遍分群数据），这种方式会有T+1的延 时）用户次日访问App时会判断该用户是否在某个分群中，满足条件弹出。

但如果选择四种预定义分群：全部登录用户，全部访问用户，新登录用户，新访问用户，在触达中是实时判断的。比如选择新登录用户，那么每个打开App的用户，触达 SDK 都会实时判断该用户是否为新登陆的用户。

三. 选择触发条件和上传素材。

![](../../.gitbook/assets/image%20%2874%29.png)



<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x53C2;&#x6570;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#x89E6;&#x53D1;&#x9875;&#x9762;</td>
      <td style="text-align:left">
        <p>&#x662F;&#x6307;&#xFF0C;&#x5F53;&#x7528;&#x6237;&#x5230;&#x8FBE;&#x54EA;&#x4E2A;/&#x4E9B;&#x9875;&#x9762;&#x7684;&#x65F6;&#x5019;&#xFF0C;&#x5F39;&#x51FA;&#x5F39;&#x7A97;&#x3002;&#x6DFB;&#x52A0;&#x591A;&#x4E2A;&#x6761;&#x4EF6;&#x65F6;&#xFF0C;&#x610F;&#x5473;&#x7740;&#x7528;&#x6237;&#x53EA;&#x8981;&#x5230;&#x8FBE;&#x5176;&#x4E2D;&#x4EFB;&#x610F;&#x4E00;&#x4E2A;&#x9875;&#x9762;&#xFF0C;&#x90FD;&#x4F1A;&#x5F39;&#x51FA;&#x5F39;&#x7A97;&#x3002;</p>
        <p>&#x6BD4;&#x5982;&#xFF0C;</p>
        <ul>
          <li>&#x652F;&#x6301;<b>&#x7279;&#x5B9A;&#x9875;&#x9762;</b>&#xFF1A;&#x4F60;&#x60F3;&#x5728;&#x7528;&#x6237;&#x5230;&#x8FBE;
            www.growingio.com &#x9875;&#x9762;&#x65F6;&#x53D1;&#x9001;&#x5F39;&#x7A97;&#xFF0C;&#x5C31;&#x53EF;&#x4EE5;&#x5C06;&#x8FD9;&#x4E2A;&#x9875;&#x9762;
            www.growingio.com &#x8F93;&#x5165;&#x8FDB;&#x53BB;&#x3002;</li>
          <li>&#x652F;&#x6301;<b>&#x9875;&#x9762;&#x7EC4;&#x901A;&#x914D;&#x7B26;</b>&#xFF1A;&#x5982;&#x679C;&#x4F60;&#x60F3;&#x5728;&#x7528;&#x6237;&#x5230;&#x8FBE;
            www.growingio.com &#x57DF;&#x540D;&#x4E0B;&#x6240;&#x6709;&#x9875;&#x9762;&#x65F6;&#x53D1;&#x9001;&#x5F39;&#x7A97;&#xFF0C;&#x53EF;&#x4EE5;&#x8F93;&#x5165;
            www.growingio.com*&#x3002;</li>
          <li>&#x652F;&#x6301;<b>&#x591A;&#x4E2A;&#x9875;&#x9762;&#x7EC4;&#x5408;</b>&#xFF1A;&#x4F60;&#x60F3;&#x5728;&#x7528;&#x6237;&#x5230;&#x8FBE;
            www.growingio.com/1 &#x548C; www.growingio.com/2 &#x65F6;&#x89E6;&#x53D1;&#xFF0C;&#x53EF;&#x4EE5;&#x901A;&#x8FC7;<b>&#x589E;&#x52A0;URL</b>&#x6309;&#x94AE;&#x8F93;&#x5165;&#x4E24;&#x4E2A;URL&#x3002;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x89E6;&#x53D1;&#x65F6;&#x673A;</td>
      <td style="text-align:left">
        <p></p>
        <p>&#x5C31;&#x662F;&#x7528;&#x6237;&#x4F1A;&#x5728;&#x4EC0;&#x4E48;&#x65F6;&#x95F4;&#x770B;&#x5230;&#x8FD9;&#x4E2A;&#x5F39;&#x7A97;&#xFF1F;</p>
        <p>&#x9ED8;&#x8BA4;&#x89E6;&#x53D1;&#x65F6;&#x673A;&#x4E3A;&#x300C;<b>&#x9875;&#x9762;&#x6253;&#x5F00;</b>&#x300D;&#x65F6;&#xFF0C;&#x4E5F;&#x53EF;&#x4EE5;&#x9009;&#x62E9;&#x5176;&#x4ED6;&#x4E8B;&#x4EF6;&#x4F5C;&#x4E3A;&#x89E6;&#x53D1;&#x65F6;&#x673A;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x5EF6;&#x8FDF;&#x8BBE;&#x7F6E;</td>
      <td style="text-align:left">&#x8BBE;&#x7F6E;&#x5F39;&#x7A97;&#x5728;&#x6EE1;&#x8DB3;&#x89E6;&#x53D1;&#x6761;&#x4EF6;&#x540E;&#x7684;&#x5EF6;&#x8FDF;&#x5F39;&#x51FA;&#x65F6;&#x95F4;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x89E6;&#x53D1;&#x6B21;&#x6570;</td>
      <td style="text-align:left">
        <p>&#x5F39;&#x7A97;&#x7684;&#x89E6;&#x53D1;&#x9891;&#x7387;&#x53EF;&#x4EE5;&#x8BBE;&#x7F6E;&#x4E3A;&#x53EA;&#x89E6;&#x53D1;
          1 &#x6B21;&#xFF0C;&#x6216;&#x662F;&#x591A;&#x6B21;&#x3002;</p>
        <p>&#x5982;&#x679C;&#x8BBE;&#x7F6E;&#x591A;&#x6B21;&#x89E6;&#x53D1;&#xFF0C;&#x9700;&#x8981;&#x5B9A;&#x4E49;&#x89E6;&#x53D1;&#x6B21;&#x6570;&#x4E0A;&#x9650;&#xFF0C;&#x4EE5;&#x53CA;&#x6BCF;&#x6B21;&#x7684;&#x95F4;&#x9694;&#x65F6;&#x95F4;&#x3002;</p>
        <p>&#x53EA;&#x8981;&#x7528;&#x6237;&#x6CA1;&#x6709;&#x70B9;&#x51FB;&#x67E5;&#x770B;&#x5F39;&#x7A97;&#x6216;&#x8005;&#x5173;&#x95ED;&#x5F39;&#x7A97;&#xFF0C;&#x4E14;&#x89E6;&#x53D1;&#x6B21;&#x6570;&#x6CA1;&#x6709;&#x8FBE;&#x5230;&#x4E0A;&#x9650;&#x5C31;&#x4F1A;&#x518D;&#x6B21;&#x89E6;&#x53D1;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x7D20;&#x6750;&#x9009;&#x62E9;</td>
      <td style="text-align:left">
        <p></p>
        <p>&#x4E0A;&#x4F20;&#x4E0D;&#x8D85;&#x8FC7;500KB&#x5927;&#x5C0F;&#x7684;&#x80CC;&#x666F;&#x56FE;&#x7247;&#x7D20;&#x6750;&#xFF08;&#x5141;&#x8BB8;&#x5305;&#x542B;&#x900F;&#x660E;&#x5EA6;&#xFF09;&#x3002;</p>
        <p>&#x5982;&#x679C;&#x6709;&#x9700;&#x8981;&#x53EF;&#x4EE5;&#x4F7F;&#x7528;
          <a
          href="https://tinypng.com/">tinypng</a>&#x7B49;&#x5728;&#x7EBF;&#x7F51;&#x7AD9;&#x8FDB;&#x884C;&#x538B;&#x7F29;&#xFF0C;&#x6216;&#x8005;&#x8BA9;&#x8BBE;&#x8BA1;&#x5E08;&#x76F4;&#x63A5;&#x505A;&#x51FA;&#x8FD9;&#x4E2A;&#x5927;&#x5C0F;&#x7684;&#x56FE;&#x7247;&#x3002;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x70B9;&#x51FB;&#x8F6C;&#x8DF3;&#x9875;&#x9762;</td>
      <td style="text-align:left">
        <p></p>
        <p>&#x8BBE;&#x7F6E;&#x70B9;&#x51FB;&#x8BE5;&#x5F39;&#x7A97;&#x4F1A;&#x8F6C;&#x8DF3;&#x7684;&#x9875;&#x9762;&#xFF0C;&#x53EF;&#x4EE5;&#x4E3A;&#x7A7A;&#x3002;</p>
      </td>
    </tr>
  </tbody>
</table>四. 测试和上线。

![](../../.gitbook/assets/image%20%2863%29.png)

配置完二、三步骤后，单击保存即可进行测试和上线。

**扫码测试**：选择需要测试的 App ，使用包含有 **安装了弹窗 SDK 的 App** 的设备进行扫码唤醒 App ，进行测试。为了更方便的供测试者查看弹窗效果，不管扫码的设备是否在分群中，都会在相应的时机弹出弹窗。

**上线时间配置：**您可以配置弹窗上下线时间。

五. 配置完成后单击**上线**。
{% endtab %}
{% endtabs %}

## 
