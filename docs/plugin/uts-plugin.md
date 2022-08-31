> HBuilderX 3.6+ 支持uts插件

## 1 uts插件介绍

### 什么是uts

uts，是DCloud推出的、基于typescript的、跨平台的、高性能的编程语言。

- UTS语言编译到Web和小程序平台，会转为js
- 编译到Android平台，会转为kotlin
- 编译到iOS平台，会转为swift（暂未发版）

js的跨平台，需要在每个平台的js引擎上运行，性能受限。而uts不需要js引擎，它直接编译为真正的原生语言。

详见[uts语法介绍](../tutorial/syntax-uts.md)

### 什么是uts插件

现有的uni-app，仍以js引擎为主。但从HBuilderX 3.6开始，uni-app支持uts插件。

也就是uts的第一步不是完整开发一个独立的app，而是作为uni-app的插件。后续uts会持续迭代，达到完整开发app的水平。

uts插件编译到app平台时，在功能上相当于uni-app之前的app原生插件，也就是kotlin和swift开发的插件。

开发uts插件不需要熟悉kotlin和swift的语法，因为使用的是基于ts的语法。但需要熟悉Android和iOS的系统API，否则无法调用原生能力。

![uts插件结构](https://native-res.dcloud.net.cn/images/uts/UTS%E7%BB%93%E6%9E%84%E7%A4%BA%E6%84%8F%E5%9B%BE1.png)
![uts plugin structure](https://native-res.dcloud.net.cn/images/uts/UTS%E7%BB%93%E6%9E%84%E7%A4%BA%E6%84%8F %E5%9B%BE1.png)

### uts插件与uni原生语言插件的区别

在HBuilderX 3.6以前，uni-app在App侧只有一种原生插件，即用java或object-c开发的插件。
Before HBuilderX 3.6, uni-app had only one native plug-in on the App side, that is, a plug-in developed with java or object-c.

在uts推出后，原来的“App原生插件”，更名为“App原生语言插件”。

不同的名字，代表它们需要开发者编写语言不同。但殊途同归，最后都编译为原生的二进制代码。
Different names mean that they require developers to write in different languages. But the same results are obtained, and they are finally compiled into native binary code.

|-				|原生语言插件				|uts插件					|
|-				|-------					|--------						|
|开发语言		|java/oc					|uts							|
|开发环境		|Android studio/XCode		|HBuilderX						|
|打包方式		|外挂aar 等产出物			|编译时生成原生代码				|
|js层调用方式	|uni.requireNativePlugin()	|普通的js函数/对象，可以直接import|

相当于原生语言插件，uts插件的优势：

1. 统一了编程语言（uts），一种语言开发所有平台，真正大前端。
2. 统一了开发工具（HBuilderX），免除搭建复杂的原生开发环境。
2. The development tool (HBuilderX) is unified, eliminating the need to build a complex native development environment.
3. 插件封装中要理解的概念更少。 传统原生语言插件需要在js和原生层处理通信，使用各种特殊转换，使用特殊语法导入，注意事项很多。**uts统一为纯前端概念，简单清晰。**
4. uts下前端和原生可以统一在HBuilderX中联调。而传统原生语言插件需要在多个开发工具间切换，联调复杂。


## 2 创建uts插件

### uts插件目录结构

在uni-app的项目工程下，提供了独立的目录`utssdk`，来存放uts插件。

当然官方更推荐使用[uni_modules](uni_modules.md)方式，这是更好的包管理方案。

首先确保项目根目录存在uni_modules文件夹，如果不存在，需要手动创建一个。

![插件目录](https://native-res.dcloud.net.cn/images/uts/uni_modules.jpg)
![Plugin Directory](https://native-res.dcloud.net.cn/images/uts/uni_modules.jpg)

### 新建步骤拆解

选中`uni_modules`目录 -- 右键 -- 新建插件
Select the `uni_modules` directory -- right click -- create a new plugin

![新建插件1](https://native-res.dcloud.net.cn/images/uts/new_uts_plugin.jpg)
![New Plugin 1](https://native-res.dcloud.net.cn/images/uts/new_uts_plugin.jpg)

选择 **uts原生插件**

![新建插件2](https://native-res.dcloud.net.cn/images/uts/new_uts_plugin2.jpg)
![New Plugin 2](https://native-res.dcloud.net.cn/images/uts/new_uts_plugin2.jpg)

uts插件目录结构

![新建插件3](https://native-res.dcloud.net.cn/images/uts/new_uts_plugin3.jpg)
![New Plugin 3](https://native-res.dcloud.net.cn/images/uts/new_uts_plugin3.jpg)


### 清单文件package.json

package.json为uni_modules的配置清单文件。


```json
{
  "id": "uts-helloworld",
  "displayName": "uts插件示例",
  "version": "0.1",
  "description": "uts插件示例",
  "uni_modules": {
    
  }
}
```

package.json的完整文档[详见](uni_modules.md#package.json)

### 插件的目录结构

```
uni_modules插件标识  
  - utssdk
  	+ app-android //Android平台目录
  	  * index.uts
  	  * config.json //Android原生配置
  	+ app-ios //ios平台目录
  	  * index.uts
  	  * config.json //ios原生配置
  	+ web //web平台目录
	  * index.uts
  	+ mp-xxx  // 其他平台，待实现
  - common // 可跨端公用的uts代码。推荐，不强制
  - static // 静态资源
  - package.json
  - index.d.ts  // 插件能力声明，非必需
  - index.uts   // 插件能力实现
```


index.uts文件是程序主入口。如果插件根目录下没有index.uts，则会在编译到不同平台时，寻找分平台的目录下的index.uts文件。

比如编译到app-android平台时，如果uts插件根目录没有index.uts，会寻找app-android/index.uts。如果也没有找到，会报错。

当同时存在分平台目录的index.uts和根目录index.uts时，会优先获取具体的分平台目录。

开发者有多种组织自己代码的方式：
1. 在插件根目录的index.uts中写条件编译代码。简单的业务一个文件搞定
2. 在插件根目录index.uts中写条件编译，import分平台的文件
3. 不写根目录的index.uts，直接在分平台目录写index.uts。不跨端时，比如只做一个Android插件，这样写比较简单

index.d.ts文件是对当前插件能力的**声明**，用于语法提示。它不是必写项。
因为uts写好后，HBuilderX可以自动识别uts api并进行语法提示。它更多的用于后续uts插件加密时给予语法提示。
如果不熟悉d.ts，可以自行网上搜索，它属于ts标准技术。

app-android 文件夹下存在下面两个文件
The following two files exist in the app-android folder

|文件名		|用途										|
|---		|---										|
|index.uts	|index.d.ts声明的能力在Android平台下的实现	|
|config.json|Android平台下的配置文件					|
 
下面是config.json的示例，可以在其中配置aar包或gradle配置。

```json
{
         // 依赖某些aar
	"libs": [
	  "xxx.aar"
	],
        // 依赖某些gradle配置
        // Depends on some gradle configuration
	"dependencies": [{
	  "id": "com.xxx.richtext:richtext",
	  "source": "implementation 'com.xxx.richtext:richtext:3.0.7'"
	}],
        // Android系统版本要求，最低Android 5.0
        // Android system version requirements, minimum Android 5.0
	"minSdkVersion": 21
}
```


## 3 开发uts原生插件

以android平台获取电量为例，介绍uts原生插件开发步骤

![OSAPI示例](https://native-res.dcloud.net.cn/images/uts/uts_osapi_demo.jpg)
![OSAPI example](https://native-res.dcloud.net.cn/images/uts/uts_osapi_demo.jpg)

在android平台目录下，编辑index.uts，键入以下内容。


```ts
// index.uts

// 引用android api
// refer to android api
import Context from "android.content.Context";
import BatteryManager from "android.os.BatteryManager";
// 引用uts环境库
// Refer to the uts environment library
import { getAppContext } from "io.dcloud.uts.android";

export function getBatteryCapacity(): string {
	// 获取android系统 application上下文
	// Get the android system application context
    const context = getAppContext();
    if (context != null) {
        const manager = context.getSystemService(
            Context.BATTERY_SERVICE
        ) as BatteryManager;
        const currentLevel: number = manager.getIntProperty(
            BatteryManager.BATTERY_PROPERTY_CAPACITY
        );
        return '' + currentLevel + '%';
    }
    return "0%";
}

```

`io.dcloud.uts.android`库介绍文档[见下](#iodcloudutsandroid)

至此，我们已经完成一个android平台上获取电量的原生能力封装。
So far, we have completed the encapsulation of the native ability to obtain electricity on the android platform.

在下一节，将介绍插件的使用，可以像使用普通js函数一样，使用getBatteryCapacity函数来获取设备电量。
In the next section, we will introduce the use of plug-ins. You can use the getBatteryCapacity function to get the device battery like a normal js function.

注：HBuilderX的代码提示系统，支持在uts文件中对Android的原生API进行提示。
Note: HBuilderX's code prompt system supports prompting Android's native API in the uts file.

## 4 前端使用插件

虽然uts插件由uts语法开发，但前端引用插件并不要求一定需要ts，普通js即可引用uts插件。

下面介绍两种常见的引入方式
Two common introduction methods are described below.

 **泛型引用**
 **Generic reference**

作为一个对象全部import进来，然后通过点运算符调用这个对象的方法或属性。
All imported as an object, and then call the method or property of this object through the dot operator.

```js
// 先引用，全部导入，对象起名为UTSHello
import * as UTSHello from "../../../uni_modules/uts-osapi";

// 然后使用UTSHello的方法
// Then use the method of UTSHello
UTSHello.getBatteryCapacity()
```


**显性引用**
**Explicit references**

从可导出的选项里import 1个或多个（逗号分隔），然后直接使用导出的方法或属性。
Import 1 or more (comma-separated) from the exportable options, and then use the exported methods or properties directly.

```js
//先引用，导入指定方法或属性
//First reference, import the specified method or property
import {
  getBatteryCapacity
} from "../../../uni_modules/uts-osapi";

// 然后使用导入的方法
// then use the imported method
getBatteryCapacity()
```

更多示例，可以参考 [HelloUTS](https://gitcode.net/dcloud/hello-uts)。

## 5 真机运行
## 5 Real machine running

**uts虽然是原生代码，但同样具有真机运行功能。**
Although **uts is a native code, it also has the function of running on a real machine. **

若HBuilderX中没有`uts编译运行插件`，在第一次运行时会自动下载。
If there is no `uts compile and run plugin` in HBuilderX, it will be downloaded automatically when it is run for the first time.

在Android上，运行体验与uni-app基本无差异。一样可以热刷新，打印console.log。
On Android, the running experience is basically the same as uni-app. You can also hot refresh and print console.log.

**自定义基座**：同之前的uni-app。如果涉及微信支付等自定义manifest信息，需要选择自定义基座运行。自定义基座也支持uts插件。

截止到HBuilderX 3.6时遗留事项：
- 不能debug uts源码
- iOS版还未发布

遗留事项后续升级完善。

## 6 云端打包
## 6 Cloud Packaging

正常支持云端打包。
Cloud packaging is normally supported.

**注意，虽然uts在真机运行时支持热刷，但打包后uts编译为了纯原生二进制代码，不支持wgt热更新。**
**Note that although uts supports hot flashing when the real machine is running, after packaging, uts is compiled into pure native binary code and does not support wgt hot update. **


## 7 Android内置库@iodcloudutsandroid

在uts里，Android的所有api都可以访问。同时DCloud提供了`io.dcloud.uts.android`库，处理在uni-app下的特殊情况。

```ts
import { getAppContext } from "io.dcloud.uts.android";
```

### getAppContext

获取当前应用Application上下文，对应android平台上的application context
```ts
fun getAppContext():Context?
```

### getUniActivity

获取当前应用宿主activity示例，当前 uni-app 应用实例的宿主activity
```ts
fun getUniActivity():Context?
```

### getResourcePath(resourceName:String)

获取指定插件资源 的运行期绝对路径
```ts
fun getResourcePath(resourceName:String):String
```

比如，插件A使用到了一张图片，开发期间 存放位置为`uni_modules/test-uts-static/static/logo.png`

程序运行期间，需要获取到此资源，可以使用 
 
```ts
getResourcePath("uni_modules/test-uts-static/static/logo.png")
```

得到文件运行时路径: `/storage/emulated/0/Android/data/io.dcloud.HBuilder/apps/__UNI__3732623/www/uni_modules/test-uts-static/static/logo.png`

### onAppActivityPause

容器的宿主activity onPause时触发

### onAppActivityResume

容器的宿主activity onResume时触发

### onAppActivityDestroy

容器的宿主activity onDestroy时触发

### onAppActivityBack

容器的宿主activity 回退物理按键点击时触发


## 8 常见问题

### Float类型传参

android很多布局参数强制要求Float,但是ts中没有内置这种类型。可以使用下面的代码实现转换

```
let textSize =  30.0.toFloat();
```

### 泛型参数

android中UI相关的api,很多会要求泛型，目前uts支持用as关键字强转，满足类似的场景

```
let frameContent = decorView.findViewById(android.R.id.content) as FrameLayout
```


## 9 示例项目

完整的示例项目地址：[HelloUTS](https://gitcode.net/dcloud/hello-uts)。