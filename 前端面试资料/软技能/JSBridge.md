## JSBridge 

### JSBridge是什么

H5和Native之间双向通信的桥梁。Hybird，既可以有H5快速迭代的功能，又可以有NA的体验。

### H5和Native的双向通信方法

#### H5调用Native的方式

|平台|方法|备注|
---|:--:|:---:
|Android|ShouldOverrideurlLoading|scheme拦截方法|
|Android|addJavascriptInterface|API|
|Android|OnJsAlert()、onJsConfirm()、onJsPrompt()||
|iOS|拦截URL||
|iOS(UIWebview)|JavascriptCore|API方法、iOS7+支持|
|iOS(WKWebview)|window.webkit.messageHandlers|API方法、iOS8+支持|

主要是两种类型：

1. `注入API`，注入Native对象或方法到JavaScript的window对象中
2. `拦截URL Scheme`，客户端拦截Webview的请求并做相应的操作

##### 注入API

通过WebView提供的接口，向JavaScript的window中注入对象或方法(Android使用addJavaScriptInterface()方法)，让JavaScript调用时相当于执行相应的Native逻辑，达到JavaScript调用Native的效果。

> tips：Android 4.2及以下的版本使用JavaScriptInterface有漏洞。因为没有正确限制使用WebView.addJavascriptInterface方法，远程攻击者可通过使用Java Reflection API利用该漏洞执行任意Java对象的方法，简单的说就是通过addJavascriptInterface给WebView加入一个JavaScript桥接接口，JavaScript通过调用这个接口可以直接操作本地的Java接口。在Android4.2以上提供@JavascriptInterface注解来规避该漏洞，但对于4.2以下版本则没有任何方法。所以使用该方法有一定的风险和兼容性问题。


##### 拦截URL Scheme

H5端通过iframe.src或location.href发送Url Scheme请求，之后Native (Android端通过ShouldOverrideurlLoading()方法) 拦截到请求的Url Scheme(包括参数等)进行相应的操作

类似于JSONP

1. 首先在H5中注入一个callback方法，放在window对象中。然后把callback的名字通过Url Scheme传到Native
2. Native通过ShouldOverrideurlLoading()，拦截到Webview的请求，并通过与前端约定好的Url Scheme判断是否是JSBridge调用
3. Native解析出前端带上的callback，并使用下面方式调用callback

#### Native调用H5的方式

|平台|方法|备注|
---|:--:|:---:
|Android|loadUrl()||
|Android|evaluateJavascript()|Android 4.4+|
|iOS(UIWebview)|stringByEvaluatingJavaScriptFromString||
|iOS(UIWebview)|JavascriptCore|iOS7+|
|iOS(WKWebview)|evaluateJavaScript:javaScriptString|iOS8+|

#### JSBridge注入时机

|平台|方法|时机|
---|:--:|:---:
|iOS(UI)|[self.webView.stringByEvaluatingJavaScriptFromString:injectjs]|webViewDidFinishLoad(会有时机问题)|
|iOS[wk]|elaluateJavaScript:www|didCreateJavaScriptContext|
|Android|webView.loadUrl("javascript:"+injectjs);|onPageFinished|

|名称|父对象|描述|兼容性|
---|:--:|:---:|:---:
|DOMContentLoaded|doc|页面内容OK|IE9+|
|onload|win|页面所有只要加载完成||
|readystatechange|doc|页面加载状态：uninitialized(未初始化)：对象存在但尚未初始化。loading(正在加载)：对象正在加载数据。loaded(加载完毕)：对象加载数据完成。interactive(交互)：可以操作对象了，但还没有完全加载。complete(完成)：对象依据加载完毕|IE9&IE10有实现bug|

iOS的UIWebview提供了代理WebViewDidFinishLoad，WebViewDidFinishLoad被调用时readyState可能出在interactive和complete两种状态，所以初始化页面直接调用会有问题。对于这个问题从NA角度可以实现一个NSObject的扩展，并实现webView:didCreateJavaScriptContext:forFrame。从H5角度可以检测页面状态，在complete之后再调用native。

iOS的didCreateJavaScriptContext和Android的OnPageFinished均是在页面onload之前完成，所以这两个时机没有调用顺序的问题。

##### 优点

注册早，即使在页面初始化就调用端能力，也可以满足

##### 缺点

监听成本高，需要NA注入，后期维护成本不可控制