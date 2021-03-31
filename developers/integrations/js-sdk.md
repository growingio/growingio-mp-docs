# Web弹窗SDK

## 集成SDK

### 1. 无埋点SDK

Web弹窗SDK会自动去识别Web无埋点的版本进行兼容，所以Web无埋点1.x和2.x均可集成Web弹窗SDK。

{% hint style="info" %}
注意：web 弹窗sdk只能识别web弹窗，不识别H5弹窗，想要使用H5弹窗请集成H5弹窗SDK.
{% endhint %}

### 2. 集成Web弹窗SDK

将以下深色区内的整个JS代码复制到您所需分析页面中的`<head>`和`<head>`标签之间, 放置在GrowingIO无埋点集成代码的下方即可。

```javascript
!function(n,e){function t(e,n){return function(){e.apply(n,1===arguments.length?[arguments[0]]:Array.apply(null,arguments))}}var s=n.gio?t(n.gio.q.unshift,n.gio.q):t(n._vds.push,n._vds),i="growingio-sdk";n[i]={pendingEvents:[]},s(["setListener",function(e){n[i]&&n[i].eventMessageQueue?n[i].eventMessageQueue.feed(e):n[i].pendingEvents.length<=200&&n[i].pendingEvents.push(e)}]);var o=e.createElement("script"),r=e.getElementsByTagName("script");o.async=1,o.src=("https:"==e.location.protocol?"https://":"http://")+"assets.giocdn.com/sdk/marketing/1.1/access.js";var g=r[r.length-1];g.parentNode.insertBefore(o,g)}(window,document);
```

> **未压缩的代码（供参考）**

```javascript
// 集成代码
(function(window, document, src) {
  // _vds 是 1.x版本无埋点，gio.q是2.x
  // 1.x 插入队尾，2.x插入队顶
  // Function.prototype.bind方法ie8 不支持
  function bind(fn, obj) {
    return function() {
      fn.apply(obj, (arguments.length === 1 ? [arguments[0]] : Array.apply(null, arguments)))
    }
  }
  var gio_q = !!window.gio ? bind(window.gio.q.unshift, window.gio.q) : bind(window._vds.push, window._vds);
  var key = "growingio-sdk";
  window[key] = {
    pendingEvents: []
  }
  gio_q(['setListener', function(event) {
    if (!!window[key] && !!window[key].eventMessageQueue) {
      window[key].eventMessageQueue.feed(event)
    } else if (window[key].pendingEvents.length <= 200) {
      window[key].pendingEvents.push(event)
    }
  }])


  var script = document.createElement("script");
  var scriptTags=document.getElementsByTagName("script");
  script.async=1;
  script.src = ('https:' == document.location.protocol ? 'https://' : 'http://' )+ src;
  var tag = scriptTags[scriptTags.length - 1];
  tag.parentNode.insertBefore(script, tag);
 })(window, document, "assets.giocdn.com/sdk/marketing/1.1/access.js");
```

## 浏览器兼容性

### Web浏览器

| IE | Firefox | Chorme | Safari | QQ Browser | 360 | 百度浏览器 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 8、9、10、11 | 全部 | 全部 | 12 | 10.5 | 10 | 8.7 |

{% hint style="info" %}
目前还未正式支持移动端浏览器和WebView
{% endhint %}





