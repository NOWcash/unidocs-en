`uni-app`的js API由标准ECMAScript的js API 和 uni 扩展 API 这两部分组成。

标准ECMAScript的js仅是最基础的js。浏览器基于它扩展了window、document、navigator等对象。小程序也基于标准js扩展了各种wx.xx、my.xx、swan.xx的API。node也扩展了fs等模块。

uni-app基于ECMAScript扩展了uni对象，并且API命名与小程序保持兼容。

## 标准js和浏览器js的区别

`uni-app`的js代码，h5端运行于浏览器中。非h5端（包含小程序和App），Android平台运行在v8引擎中，iOS平台运行在iOS自带的jscore引擎中，都没有运行在浏览器或webview里。

非H5端，虽然不支持window、document、navigator等浏览器的js API，但也支持标准ECMAScript。

请注意不要把浏览器里的js扩展对象等价于标准js。

所以uni-app的非H5端，一样支持标准js，支持if、for等语法，支持字符串、数字、时间、布尔值、数组、自定义对象等变量类型及各种处理方法。仅仅是不支持window、document、navigator等浏览器专用对象。

## ES6 支持
## Supported on ES6
uni-app 在支持绝大部分 ES6 API 的同时，也支持了 ES7 的 await/async。
uni-app supports not only most ES6 API, but also await/async of ES7.

ES6 API 的支持，详见如下表格部分（`x` 表示不支持，无特殊说明则表示支持）：
For the support of ES6 API, see the following table for details (`x` means no support, and no special instructions means support):
- 因为iOS上不允许三方js引擎，所以iOS上不区分App、小程序、H5，各端均仅依赖iOS版本。
- 各端Android版本有差异：
- Differences can be seen among Android versions of various sides:

    * App端的数据见下表；
    * H5端数据见caniuse；
    * 微信小程序[详见](https://developers.weixin.qq.com/miniprogram/dev/framework/runtime/js-support.html#%E5%AE%A2%E6%88%B7%E7%AB%AF%20ES6%20API%20%E6%94%AF%E6%8C%81%E6%83%85%E5%86%B5)
    * 阿里小程序[详见](https://docs.alipay.com/mini/framework/implementation-detail)
    * 百度小程序[详见](https://smartprogram.baidu.com/docs/develop/framework/operating-environment/)
    * 字节跳动小程序[详见](https://developer.toutiao.com/dev/cn/mini-app/develop/framework/mini-app-runtime/javascript-support)
    * QQ小程序[详见](https://q.qq.com/wiki/develop/miniprogram/frame/useful/useful_env.html#es6%E6%94%AF%E6%8C%81%E6%83%85%E5%86%B5)

|String|iOS8|iOS9|iOS10|Android|
|:-|:-|:-|:-|:-|
|codePointAt|||||
|normalize|x|x||仅支持 NFD/NFC|
|includes|||||
|startsWith|||||
|endsWith|||||
|repeat|||||
|String.fromCodePoint||||&nbsp;|

|Array|iOS8|iOS9|iOS10|Android|
|:-|:-|:-|:-|:-|
|copyWithin|||||
|find|||||
|findIndex|||||
|fill|||||
|entries|||||
|keys|||||
|values|x|||x|
|includes|x||||
|Array.from|||||
|Array.of||||&nbsp;|

|Number|iOS8|iOS9|iOS10|Android|
|:-|:-|:-|:-|:-|
|isFinite|||||
|isNaN|||||
|parseInt|||||
|parseFloat|||||
|isInteger|||||
|EPSILON|||||
|isSafeInteger||||&nbsp;|

|Math|iOS8|iOS9|iOS10|Android|
|:-|:-|:-|:-|:-|
|trunc|||||
|sign|||||
|cbrt|||||
|clz32|||||
|imul|||||
|fround|||||
|hypot|||||
|expm1|||||
|log1p|||||
|log10|||||
|log2|||||
|sinh|||||
|cosh|||||
|tanh|||||
|asinh|||||
|acosh|||||
|atanh||||&nbsp;|

|Object|iOS8|iOS9|iOS10|Android|
|:-|:-|:-|:-|:-|
|is|||||
|assign|||||
|getOwnPropertyDescriptor|||||
|keys|||||
|getOwnPropertyNames|||||
|getOwnPropertySymbols||||&nbsp;|

|Other|iOS8|iOS9|iOS10|Android<5|
|:-|:-|:-|:-|:-|
|Symbol|||||
|Set|||||
|Map|||||
|Proxy|x|x||x|
|Reflect|||||
|Promise||||&nbsp;|

**注意**
**Notice**
- App端Android支持不依赖Android版本号，即便是Android4.4也是上表数据。因为uni-app的js代码运行在自带的独立jscore中，没有js的浏览器兼容性问题。uni-app的vue页面在Android低端机上只有css浏览器兼容性问题，因为vue页面仍然渲染在webview中，受Android版本影响，太新的css语法在低版本不支持。
- On the App side, Android supports less dependence on the Android version number. The data in the above table is applicable even on Android 4.4. Because js code of uni-app runs in its own independent jscore, there is no browser compatibility problem of js. The vue page of uni-app only has css browser compatibility problem on Android low-end device, because vue page is still rendered in webview. Affected by the Android version, too new css syntax is not supported in lower versions.
- 默认不需要在微信工具里继续开启es6转换。但如果用了微信的wxml自定义组件（wxcomponents目录下），uni-app编译器并不会处理这些文件中的es6代码，需要去微信工具里开启转换。从HBuilderX调起微信工具时，如果发现工程下有wxcomponents目录会自动配置微信工程打开es6转换。