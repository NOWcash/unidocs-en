#### web-view

`web-view` 是一个 web 浏览器组件，可以用来承载网页的容器，会自动铺满整个页面（nvue 使用需要手动指定宽高）。
`web-view` is a web browser component that can be used as a container for hosting web pages, and will automatically cover the whole page (you need to manually specify the width and height when using nvue).

> 各小程序平台，web-view 加载的 url 需要在后台配置域名白名单，包括内部再次 iframe 内嵌的其他 url 。
> For each applet platform, the url loaded by web-view needs to configure the domain name whitelist in the background, including other urls embedded in the iframe again.

**属性说明**
**Attribute description**

|属性名|类型|说明|平台差异说明|
| Attribute name| Type| Instruction| Platform difference description|
|:-|:-|:-|:-|
|src|String|webview 指向网页的链接|&nbsp;|
| src| String| webview links to web pages|  |
|allow|String|用于为 [iframe](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/iframe) 指定其[特征策略](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/策略特征)|H5|
| allow| String| Used to specify its [feature strategy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Feature_Policy) for [iframe](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/iframe)| H5|
|sandbox|String|该属性对呈现在 [iframe](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/iframe) 框架中的内容启用一些额外的限制条件。|H5|
| sandbox| String| This attribute enables some additional restrictions on the content presented in the [iframe](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/iframe) frame.| H5|
|fullscreen|Boolean|是否铺满整个页面，默认值：`true`。|H5 (HBuilder X 3.5.4+)|
|fullscreen|Boolean|Whether to fill the entire page, default: `true`. |H5 (HBuilder X 3.5.4+)|
|webview-styles|Object|webview 的样式|App-vue|
| webview-styles| Object| Style of webview| App-vue|
|update-title|Boolean|是否自动更新当前页面标题。默认值：`true`|App-vue (HBuilder X 3.3.8+)|
|update-title|Boolean| Whether to automatically update the current page title. Default: `true`|App-vue (HBuilder X 3.3.8+)|
|@message|EventHandler|网页向应用 `postMessage` 时，会在特定时机（后退、组件销毁、分享）触发并收到消息。|H5 暂不支持（可以直接使用 [window.postMessage](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/postMessage)）|
| @message| EventHandler| When a web page sends `postMessage` to an application, it triggers and receives a message at a specific time (back, component destruction, sharing).| not supported by H5 temporarily (you can use [window.postMessage](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/postMessage) directly)|
|@onPostMessage|EventHandler|网页向应用实时 `postMessage`|App-nvue|
| @onPostMessage| EventHandler| Web page sends real-time `postMessage` to application| App-nvue|

**注意**
**Notice**
- `update-title` 仅支持 `App-vue` 。`小程序` 恒为 `true`，`H5、nvue` 恒为 `false`
- `update-title` only supports `App-vue`. `Mini Program` is always `true`, `H5, nvue` is always `false`

**src**

|来源|App|H5|微信小程序|支付宝小程序|百度小程序|字节跳动小程序、飞书小程序|QQ小程序|快应用|360小程序|快手小程序|京东小程序|
|Source|App|H5|WeChat applet|Alipay applet|Baidu applet|ByteDance applet, Feishu applet|QQ applet|Quick application|360 applet|Kaishou applet|Jingdong applet|
|:-|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|网络|√|√|√|√|√|√|√|√|√|√|√|
|Network|√|√|√|√|√|√|√|√|√|√|√|
|本地|√|√|x|x|x|x|x|x|x|x|x|
|local|√|√|x|x|x|x|x|x|x|x|x|

**webview-styles**

|属性|类型|说明|
| Attribute| Type| Instruction|
|:-|:-|:-|
|progress|Object/Boolean|进度条样式。仅加载网络 HTML 时生效，设置为 `false` 时禁用进度条。|
| progress| Object/Boolean| Progress bar style. Only takes effect when web HTML is loaded. When set to `false`, the progress bar is disabled.|
|width|String|web-view 组件的宽度。|
|width|String|The width of the web-view component. |
|height|String|web-view 组件的高度。|
|height|String|The height of the web-view component. |

**progress**

|属性|类型|默认值|说明|
| Attribute| Type| Defaults| Instruction|
|:-|:-|:-|:-|
|color|String|#00FF00|进度条颜色|
| color| String| #00FF00| Progress bar color|


::: preview https://hellouniapp.dcloud.net.cn/pages/component/web-view/web-view

```html
<template>
	<view>
		<web-view :webview-styles="webviewStyles" src="https://uniapp.dcloud.io/static/web-view.html"></web-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				webviewStyles: {
					progress: {
						color: '#FF3333'
					}
				}
			}
		}
	}
</script>

<style>

</style>
```
:::

注意：
Notice:
- 小程序仅支持加载网络网页，不支持本地html
- The applet only supports loading web pages, not local html
- 补充说明：app-vue下web-view组件不支持自定义样式，而v-show的本质是改变组件的样式。即组件支持v-if而不是支持v-show。
- Supplement: web-view components under app-vue do not support custom styles, and the essence of v-show is to change the styles of components. That is to say, components support v-if instead of v-show.
- 小程序端 web-view 组件一定有原生导航栏，下面一定是全屏的 web-view 组件，navigationStyle: custom 对 web-view 组件无效。
- The web-view component of the applet must have a native navigation bar, and the following must be a full-screen web-view component. navigationStyle: custom is invalid for the web-view component.
- App 端使用 uni.web-view.js 的最低版为 [uni.webview.1.5.4.js](https://gitee.com/dcloud/uni-app/raw/dev/dist/uni.webview.1.5.4.js)
- The minimum version of uni.web-view.js used on the App side is [uni.webview.1.5.4.js](https://gitee.com/dcloud/uni-app/raw/dev/dist/uni.webview .1.5.4.js)
- App 平台同时支持网络网页和本地网页，但本地网页及相关资源（js、css等文件）必须放在 `uni-app 项目根目录->hybrid->html` 文件夹下或者 `static` 目录下，如下为一个加载本地网页的`uni-app`项目文件目录示例：
- Web pages and local pages are simultaneously supported on the App platform. However, local web pages and related resources (js, css and other files) must be placed under the `uni-app project root directory->hybrid->html` folder or under the `static` directory. The following is an example of a `uni-app` project file directory that loads a local web page:
- nvue `web-view` 必须指定样式宽高
- nvue `web-view` must specify the style width and height
- App 网页向应用 `postMessage` 为实时消息
- App web page sends `postMessage` as real-time message to the application
- app-nvue `web-view` 默认没有大小，可以通过样式设置大小，如果想充满整个窗口，设置 `flex: 1` 即可，标题栏不会自动显示 `web-view` 页面中的 title。如果想充满整个窗口且想要显示标题推荐使用 vue 页面的 `web-view`(默认充满屏幕不可控制大小), 想自定义 `web-view` 大小使用 nvue `web-view`
- app-nvue `web-view` has no size by default. You can set the size by style. If you want to fill the entire window, just set `flex: 1`. The title bar will not automatically display the title in the `web-view` page. If you want to fill the whole window and display the title, the `web-view` of the vue page is recommended (the default is to fill the screen with no controllable size); If you want to customize the size of the `web-view`, nvue `web-view` is recommended.

<pre v-pre="" data-lang="">
	<code class="lang-" style="padding:0">
┌─components
├─hybrid
│  └─html
│     ├─css
│     │  └─test.css
│     ├─img
│     │  └─icon.png
│     ├─js
│     │  └─test.js
│     └─local.html
├─pages
│  └─index
│     └─index.vue
├─static
├─main.js
├─App.vue
├─manifest.json
└─pages.json
	</code>
</pre>

**示例** [查看示例](https://hellouniapp.dcloud.net.cn/pages/component/web-view/web-view)
**Example** [View examples](https://hellouniapp.dcloud.net.cn/pages/component/web-view/web-view)
```html
<template>
	<view>
		<web-view src="/hybrid/html/local.html"></web-view>
	</view>
</template>
```

`<web-view>` 加载的网页中支持调用部分 uni 接口：
The webpage loaded by `<web-view>` supports calling some uni interfaces:

|方法名|说明|平台差异说明|
| Method name| Instruction| Platform difference description|
|:-|:-|:-|
|uni.navigateTo|[navigateTo](/api/router?id=navigateto)||
|uni.redirectTo|[redirectTo](/api/router?id=redirectto)||
|uni.reLaunch|[reLaunch](/api/router?id=relaunch)||
|uni.switchTab|[switchTab](/api/router?id=switchtab)||
|uni.navigateBack|[navigateBack](/api/router?id=navigateback)||
|uni.postMessage|向应用发送消息|字节跳动小程序不支持、H5 暂不支持（可以直接使用 [window.postMessage](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/postMessage)）|
|uni.postMessage|Send a message to the app|ByteDance applet does not support, H5 does not currently support (you can directly use [window.postMessage](https://developer.mozilla.org/zh-CN/docs/Web/ API/Window/postMessage))|
|uni.getEnv|获取当前环境|字节跳动小程序与飞书小程序不支持|
|uni.getEnv|Get the current environment|ByteDance applet and Feishu applet are not supported|

##### uni.postMessage(OBJECT)
网页向应用发送消息，在 `<web-view>` 的 `message` 事件回调 `event.detail.data` 中接收消息。
The web page sends a message to the application, and receives the message in the `message`Event callback`event.detail.data` of `<web-view>`.

**Tips**

- 传递的消息信息，必须写在 data 对象中。
- The message and information passed by must be written in the data object.
- `event.detail.data` 中的数据，以数组的形式接收每次 post 的消息。（注：支付宝小程序除外，支付宝小程序中以对象形式接受）
- The data in `event.detail.data` to receive the message of each post in the form of an array. (Note: except Alipay applet, which is accepted in the form of objects in Alipay applet)

##### uni.getEnv(CALLBACK)

**callback 返回的对象**
**The object returned by callback**

|属性|类型|说明|
| Attribute| Type| Instruction|
|:-|:-|:-|
|plus|Boolean|App|
|nvue|Boolean|App-nvue, uni.webview.1.5.4.js+ 支持|
|nvue|Boolean|App-nvue, uni.webview.1.5.4.js+ Supported|
|miniprogram|Boolean|微信小程序|
|miniprogram|Boolean|WeChat Mini Program|
|smartprogram|Boolean|百度小程序|
|smartprogram|Boolean|Baidu Mini Program|
|miniprogram|Boolean|支付宝小程序|
|miniprogram|Boolean|Alipay Mini Program|

**示例**
**Example**

在 `<web-view>` 加载的 HTML 中，添加以下代码：
In the HTML loaded by `<web-view>`, add the following code:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width,initial-scale=1,minimum-scale=1,maximum-scale=1,user-scalable=no" />
    <title>网络网页</title>
    <style type="text/css">
      .btn {
        display: block;
        margin: 20px auto;
        padding: 5px;
        background-color: #007aff;
        border: 0;
        color: #ffffff;
        height: 40px;
        width: 200px;
      }

      .btn-red {
        background-color: #dd524d;
      }

      .btn-yellow {
        background-color: #f0ad4e;
      }

      .desc {
        padding: 10px;
        color: #999999;
      }

      .post-message-section {
        visibility: hidden;
      }
    </style>
  </head>
  <body>
    <p class="desc">web-view 组件加载网络 html 示例。点击下列按钮，跳转至其它页面。</p>
    <div class="btn-list">
      <button class="btn" type="button" data-action="navigateTo">navigateTo</button>
      <button class="btn" type="button" data-action="redirectTo">redirectTo</button>
      <button class="btn" type="button" data-action="navigateBack">navigateBack</button>
      <button class="btn" type="button" data-action="reLaunch">reLaunch</button>
      <button class="btn" type="button" data-action="switchTab">switchTab</button>
    </div>
    <div class="post-message-section">
      <p class="desc">网页向应用发送消息，注意：小程序端应用会在此页面后退时接收到消息。</p>
      <div class="btn-list">
        <button class="btn btn-red" type="button" id="postMessage">postMessage</button>
      </div>
    </div>
    <script type="text/javascript">
      var userAgent = navigator.userAgent;
      if (userAgent.indexOf('AlipayClient') > -1) {
        // 支付宝小程序的 JS-SDK 防止 404 需要动态加载，如果不需要兼容支付宝小程序，则无需引用此 JS 文件。
        // The JS-SDK of Alipay applet prevents 404 from needing to be dynamically loaded. If you do not need to be compatible with the Alipay applet, you do not need to reference this JS file.
        document.writeln('<script src="https://appx/web-view.min.js"' + '>' + '<' + '/' + 'script>');
      } else if (/QQ/i.test(userAgent) && /miniProgram/i.test(userAgent)) {
        // QQ 小程序
        // QQ applet
        document.write(
          '<script type="text/javascript" src="https://qqq.gtimg.cn/miniprogram/webview_jssdk/qqjssdk-1.0.0.js"><\/script>'
        );
      } else if (/miniProgram/i.test(userAgent) && /micromessenger/i.test(userAgent)) {
        // 微信小程序 JS-SDK 如果不需要兼容微信小程序，则无需引用此 JS 文件。
        // WeChat applet JS-SDK If you do not need to be compatible with WeChat applet, you do not need to reference this JS file.
        document.write('<script type="text/javascript" src="https://res.wx.qq.com/open/js/jweixin-1.4.0.js"><\/script>');
      } else if (/toutiaomicroapp/i.test(userAgent)) {
        // 头条小程序 JS-SDK 如果不需要兼容头条小程序，则无需引用此 JS 文件。
        // Toutiao applet JS-SDK If you don't need to be compatible with Toutiao applet, you don't need to reference this JS file.
        document.write(
          '<script type="text/javascript" src="https://s3.pstatp.com/toutiao/tmajssdk/jssdk-1.0.1.js"><\/script>');
      } else if (/swan/i.test(userAgent)) {
        // 百度小程序 JS-SDK 如果不需要兼容百度小程序，则无需引用此 JS 文件。
        // Baidu applet JS-SDK If you don't need to be compatible with Baidu applet, you don't need to reference this JS file.
        document.write(
          '<script type="text/javascript" src="https://b.bdstatic.com/searchbox/icms/searchbox/js/swan-2.0.18.js"><\/script>'
        );
      } else if (/quickapp/i.test(userAgent)) {
        // quickapp
        document.write('<script type="text/javascript" src="https://quickapp/jssdk.webview.min.js"><\/script>');
      }
      if (!/toutiaomicroapp/i.test(userAgent)) {
        document.querySelector('.post-message-section').style.visibility = 'visible';
      }
    </script>
    <!-- uni 的 SDK -->
    <!-- SDK of uni -->
    <!-- 需要把 uni.webview.1.5.4.js 下载到自己的服务器 -->
    <!-- You need to download uni.webview.1.5.4.js to your own server -->
    <script type="text/javascript" src="https://unpkg.com/@dcloudio/uni-webview-js@0.0.3/index.js"></script>
    <script type="text/javascript">
      // 待触发 `UniAppJSBridgeReady` 事件后，即可调用 uni 的 API。
      //After the 'UniAppJSBridgeReady' event is triggered, the API of uni can be called.
      document.addEventListener('UniAppJSBridgeReady', function() {
        uni.postMessage({
            data: {
                action: 'message'
            }
        });
        uni.getEnv(function(res) {
            console.log('当前环境：' + JSON.stringify(res));
        });

        document.querySelector('.btn-list').addEventListener('click', function(evt) {
          var target = evt.target;
          if (target.tagName === 'BUTTON') {
            var action = target.getAttribute('data-action');
            switch (action) {
              case 'switchTab':
                uni.switchTab({
                  url: '/pages/tabBar/API/API'
                });
                break;
              case 'reLaunch':
                uni.reLaunch({
                  url: '/pages/tabBar/component/component'
                });
                break;
              case 'navigateBack':
                uni.navigateBack({
                  delta: 1
                });
                break;
              default:
                uni[action]({
                  url: '/pages/component/button/button'
                });
                break;
            }
          }
        });
        document.getElementById('postMessage').addEventListener('click', function() {
          uni.postMessage({
            data: {
              action: 'message'
            }
          });
        });
      });
    </script>
  </body>
</html>

```


##### **App端web-view的扩展**
##### **App-side web-view extension**
App端的webview是非常强大的，可以更灵活的控制和拥有更丰富的API。
The webview on the App side is very powerful and can be controlled more flexibly and has a richer API.

每个vue页面，其实都是一个webview，而vue页面里的web-view组件，其实是webview里的一个子webview。这个子webview被append到父webview上。
Each vue page is actually a webview, and the web-view component in the vue page is actually a sub-webview in the webview. This child webview is appended to the parent webview.

通过以下方法，可以获得这个web-view组件对应的js对象，然后参考[https://www.html5plus.org/doc/zh_cn/webview.html#plus.webview.WebviewObject](https://www.html5plus.org/doc/zh_cn/webview.html#plus.webview.WebviewObject)，可以进一步重设这个web-view组件的样式，比如调整大小
The js object corresponding to this web-view component can be obtained by the following method, and then refer to [https://www.html5plus.org/doc/zh_cn/webview.html#plus.webview.WebviewObject](https://www.html5plus.org/doc/zh_cn/webview.html#plus.webview.WebviewObject](https://www. html5plus.org/doc/zh_cn/webview.html#plus.webview.WebviewObject), you can further reset the style of this web-view component, such as resizing

```html
<template>
	<view>
		<web-view src="https://www.baidu.com"></web-view>
	</view>
</template>
<script>
var wv;//计划创建的webview
export default {
	onReady() {
		// #ifdef APP-PLUS
		var currentWebview = this.$scope.$getAppWebview() //此对象相当于html5plus里的plus.webview.currentWebview()。在uni-app里vue页面直接使用plus.webview.currentWebview()无效
		setTimeout(function() {
			wv = currentWebview.children()[0]
			wv.setStyle({top:150,height:300})
		}, 1000); //如果是页面初始化调用时，需要延时一下
		// #endif
	}
};
</script>
```

甚至可以不用`web-view`组件，直接js创建一个子webview来加载html。比如不希望远程网页使用plus的API，不管是因为安全原因还是因为back监听冲突，可以使用如下代码：
You can even create a child webview directly in js to load html without using the `web-view` component. For example, if you do not want the remote web page to use the plus API, whether it is for security reasons or because of back monitoring conflicts, you can use the following code:
```html
<template>
	<view>
	</view>
</template>
<script>
var wv;//计划创建的webview
export default {
	onLoad() {
		// #ifdef APP-PLUS
		wv = plus.webview.create("","custom-webview",{
			plusrequire:"none", //禁止远程网页使用plus的API，有些使用mui制作的网页可能会监听plus.key，造成关闭页面混乱，可以通过这种方式禁止
      'uni-app': 'none', //不加载uni-app渲染层框架，避免样式冲突
			top:uni.getSystemInfoSync().statusBarHeight+44 //放置在titleNView下方。如果还想在webview上方加个地址栏的什么的，可以继续降低TOP值
		})
		wv.loadURL("https://www.baidu.com")
		var currentWebview = this.$scope.$getAppWebview(); //此对象相当于html5plus里的plus.webview.currentWebview()。在uni-app里vue页面直接使用plus.webview.currentWebview()无效
		currentWebview.append(wv);//一定要append到当前的页面里！！！才能跟随当前页面一起做动画，一起关闭
		setTimeout(function() {
			console.log(wv.getStyle())
		}, 1000);//如果是首页的onload调用时需要延时一下，二级页面无需延时，可直接获取
		// #endif
	}
};
</script>
```

如果想设置web-view组件可双指缩放，可参考如下代码：
If you want to set the web-view component to be pinch-zoomable, you can refer to the following code:
```js
export default {
	onReady() {
		// #ifdef APP-PLUS
		var currentWebview = this.$scope.$getAppWebview() //获取当前页面的webview对象
		setTimeout(function() {
			wv = currentWebview.children()[0]
			wv.setStyle({scalable:true})
		}, 1000); //如果是页面初始化调用时，需要延时一下
		// #endif
	}
};
```

##### `web-view`组件的层级问题解决
##### Solution to the level problem of the `web-view` component
web-view组件在App和小程序中层级较高，如需要在vue页面中写代码为web-view组件覆盖内容，小程序端无解，只能由web-view的组件自己弹出div。App端有如下若干方案：
The web-view component has a higher level in the App and the applet. If you need to write code in the vue page to cover the content for the web-view component, the applet has no solution, and the div can only be popped up by the web-view component itself. There are several options on the App side as follows:
1. 比较简单的方式是actionsheet等原生弹出菜单（小程序也可以使用此方案）
1. A simpler way is to use native pop-up menus such as actionsheet (applets can also use this solution)
2. 使用plus.nativeObj.view。这里有一个底部图标菜单的示例，可参考[https://ext.dcloud.net.cn/plugin?id=69](https://ext.dcloud.net.cn/plugin?id=69)
2. Use plus.nativeObj.view. Here is an example of the bottom icon menu, you can refer to [https://ext.dcloud.net.cn/plugin?id=69](https://ext.dcloud.net.cn/plugin?id=69)
3. 使用[原生子窗体subNvue](/api/window/subNVues)
3. Use [native child form subNvue](/api/window/subNVues)
4. 可以在web-view组件内嵌的网页中弹出z-index更高的div。如果是外部网页，可以在vue中获得子webview对象后，通过[evalJS](https://www.html5plus.org/doc/zh_cn/webview.html#plus.webview.WebviewObject.evalJS)为这个子webview注入一段js，操作其弹出div层。
4. You can pop up a div with a higher z-index in the web page embedded in the web-view component. If it is an external web page, you can obtain the sub webview object in vue and use [evalJS](https://www.html5plus.org/doc/zh_cn/webview.html#plus.webview.WebviewObject.evalJS) for this sub webview Inject a piece of js and operate it to pop up the div layer.

##### web-view组件的浏览器内核说明
##### Browser kernel description of the web-view component
- H5端的web-view其实是被转为iframe运行，使用的是当前的浏览器
- The web-view on the H5 side is actually converted to an iframe to run with the current browser
- 小程序的web-view使用的是小程序自带的浏览器内核，不同厂商不一样，[详见](https://ask.dcloud.net.cn/article/1318)
- The web-view of the applet uses the browser kernel that comes with the applet, which varies from manufacturer to manufacturer. [See details](https://ask.dcloud.net.cn/article/1318)
- App端，Android，默认使用的是os自带的浏览器内核，在设置-所有应用里，显示系统服务，可查看Android System Webview的版本。在Android5+，系统webview支持安装升级。
- On the App side, Android, the browser kernel that comes with os is used by default. In Settings - All Apps, system services are displayed, and you can view the version of Android System Webview. In Android5+, the system webview supports installation and upgrade.
- App端，Android，支持在manifest中配置选用腾讯X5浏览器内核。使用x5内核需要一些注意事项！具体请参考[详见](https://ask.dcloud.net.cn/article/36806)
- On the App side, Android supports the configuration and selection of Tencent X5 browser kernel in the manifest. Precautions for using the X5 kernel! [See details](https://ask.dcloud.net.cn/article/36806)
- App端，iOS，是分为UIWebview和WKWebview的，2.2.5+起默认为WKWebview，之前版本[详见](https://ask.dcloud.net.cn/article/36348)
- On the App side, iOS is divided into UIWebview and WKWebview. From 2.2.5+, the default is WKWebview. For the previous version, [See details](https://ask.dcloud.net.cn/article/36348)


**注意事项**
**Precautions**
- `<web-view>` 组件默认铺满全屏并且层级高于前端组件。App端想调节大小或在其上覆盖内容需使用plus规范，H5端可以改为直接使用 iframe。
- The `<web-view>` component fills the full screen by default and is higher than the front-end component. If you want to adjust the size or overlay content on the App side, you need to use the plus specification, and the H5 side can directly use iframe instead.
- `<web-view>` 组件所在窗口的标题，跟随页面的 `<title>` 值的变化而变化（不含H5端）。
- The title of the window where the `<web-view>` component is located will change with the change of the `<title>` value of the page (excluding the H5 side).
- App-vue的`web-view`加载的html页面可以运行plus的api，但注意如果该页面调用了plus.key的API监听了back按键（或使用mui的封装），会造成back监听冲突。需要该html页面移除对back的监听。或按照上面的示例代码禁止网页使用plus对象。app-nvue页面的`web-view`组件不能运行plus API。
- The html page loaded by the `web-view` of App-vue can run the plus API, but note that if the page calls the plus.key API to monitor the back button (or uses the mui package), it will cause a back monitoring conflict. The html page needs to remove the monitor for back. Or disallow web pages from using plus objects as per the sample code above. The `web-view` component of the app-nvue page cannot run the plus API.
- `uni.webview.js` 最新版地址：[https://gitee.com/dcloud/uni-app/raw/dev/dist/uni.webview.1.5.4.js](https://gitee.com/dcloud/uni-app/raw/dev/dist/uni.webview.1.5.4.js)
- `uni.webview.js` latest version address: [https://gitee.com/dcloud/uni-app/raw/dev/dist/uni.webview.1.5.4.js](https://gitee. com/dcloud/uni-app/raw/dev/dist/uni.webview.1.5.4.js)
- 小程序平台，个人类型与海外类型的小程序使用 `web-view` 组件，提交审核时注意微信等平台是否允许使用
- Mini Program platform, personal type and overseas type Mini Program use the `web-view` component, please pay attention to whether WeChat and other platforms are allowed to use when submitting for review
- 小程序平台， `src` 指向的链接需登录小程序管理后台配置域名白名单。`App`和`H5` 无此限制。
- The applet platform, the link pointed to by `src` needs to log in to the applet management background to configure the domain name whitelist. `App` and `H5` do not have this restriction.

##### FAQ

Q：web-view 的页面怎么和应用内的页面交互？
Q: How do pages of web-view interact with pages in the application?
A：调用 uni 相关的 API，就可以实现页面切换及发送消息。参考：[在 web-view 加载的 HTML 中调用 uni 的 API](https://ask.dcloud.net.cn/article/35083)
A: Call the API related to uni to switch pages and send messages. Refer to: [Call the API of uni in the HTML loaded by web-view](https://ask.dcloud.net.cn/article/35083)

Q：web-view 加载的 HTML 中，能够调用 5+ 的能力么？
Q: Can 5+ capabilities be invoked in the HTML loaded by web-view?
A：加载的 HTML 中是有 5+ 环境的，在 plusready 后调用即可。参考：[一个简单实用的 plusready 方法](https://ask.dcloud.net.cn/article/34922)
A: There is a 5+ environment in the loaded HTML, and it can be called after plusready. Reference: [A simple and practical plusready method](https://ask.dcloud.net.cn/article/34922)

Q: web-view 加载 uni-app H5，内部跳转冲突如何解决
Q: How to solve internal jump conflicts when web-view loads uni-app H5
A：使用 uni.webView.navigateTo...
A: Use uni.webView.navigateTo...


uni.webView.navigateTo 示例，注意uni sdk放到body下面
uni.webView.navigateTo example, note that the uni sdk is placed under the body
```html
<!DOCTYPE html>
<html lang="zh-CN">
  <head>
    ...
  </head>
  <body>
    <noscript>
      <strong>Please enable JavaScript to continue.</strong>
    </noscript>
    <div id="app"></div>
    <!-- built files will be auto injected -->
  </body>
  <!-- uni 的 SDK -->
  <!-- SDK of uni -->
  <!-- 需要把 uni.webview.1.5.4.js 下载到自己的服务器 -->
  <!-- You need to download uni.webview.1.5.4.js to your own server -->
  <script type="text/javascript" src="https://unpkg.com/@dcloudio/uni-webview-js@0.0.3/index.js"></script>
  <script>
    document.addEventListener('UniAppJSBridgeReady', function() {
      uni.webView.getEnv(function(res) {
        console.log('当前环境：' + JSON.stringify(res));
      });
      // uni.webView.navigateTo(...)
    });
  </script>
</html>
```

nvue webview通信示例
Example of nvue webview communication
```html
<template>
	<view>
		<web-view ref="webview" class="webview" @onPostMessage="handlePostMessage"></web-view>
		<button class="button" @click="evalJs">evalJs(改变webview背景颜色)</button>
	</view>
</template>

<script>
	export default {
		data: {
		},
		methods: {
			// webview向外部发送消息
			//webview sends messages to the outside
			handlePostMessage: function(data) {
				console.log("接收到消息：" + JSON.stringify(data.detail));
			},
			// 调用 webview 内部逻辑
			//Call internal logic of webview
			evalJs: function() {
				this.$refs.webview.evalJs("document.body.style.background ='#00FF00'");
			}
		}
	}
</script>
```
