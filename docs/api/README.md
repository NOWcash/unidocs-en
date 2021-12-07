`uni-app`的js API由标准ECMAScript的js API 和 uni 扩展 API 这两部分组成。

标准ecmascript的API非常多，本文档没有必要列全，仅以console、settimeout为例做简要说明。

## 标准js和浏览器js的区别

`uni-app`的js代码，h5端运行于浏览器中。非h5端，Android平台运行在v8引擎中，iOS平台运行在iOS自带的jscore引擎中。

非H5端，虽然不支持window、document、navigator等浏览器的js API，但也支持标准ECMAScript。

开发者不要把浏览器里的js等价于标准js。

ECMAScript由Ecma国际管理，是基础js语法。浏览器基于标准js扩充了window、document等js API；Node.js基于标准js扩充了fs等模块；

所以uni-app的非H5端，一样支持标准js，支持if、for等语法，支持字符串、数组、时间等变量及各种处理方法。仅仅是不支持浏览器专用对象。

## 各端特色API调用

除了uni-app框架内置的跨端API，各端自己的特色API也可通过[条件编译](https://uniapp.dcloud.io/platform)自由使用。

各端特色API规范参考各端的开发文档。uni-app也支持通过扩展原生插件来丰富App端的开发能力，具体参考[插件开发文档](http://ask.dcloud.net.cn/article/35408)

各平台的API新增，不需要uni-app升级，开发者就可以直接使用。

## 说明

- uni.on 开头的 API 是监听某个事件发生的 API 接口，接受一个 CALLBACK 函数作为参数。当该事件触发时，会调用 CALLBACK 函数。
- 如未特殊约定，其他 API 接口都接受一个 OBJECT 作为参数。
- OBJECT 中可以指定 success，fail，complete 来接收接口调用结果。
- **平台差异说明**若无特殊说明，则表示所有平台均支持。

## API `Promise 化`

1. 具体 API `Promise 化` 的策略：
   - 异步的方法，如果不传入 success、fail、complete 等 callback 参数，将以 Promise 返回数据。例如：`uni.getImageInfo()`
   - 异步的方法，且有返回对象，如果希望获取返回对象，必须至少传入一项 success、fail、complete 等 callback 参数。例如：

		```js
			// 正常使用
			const task = uni.connectSocket(
				success(res){
					console.log(res)
				}
			)

			// Promise 化
			uni.connectSocket().then(res => {
					// 此处即为 success 回调的 res
					// 如果想获取 task ，则不要使用 Promise 化
					console.log(res)
			})
		```

2. 不进行 `Promise 化` 的 API：
   - 同步的方法（即以 sync 结束）。例如：`uni.getSystemInfoSync()`
   - 以 create 开头的方法。例如：`uni.createMapContext()`
   - 以 manager 结束的方法。例如：`uni.getBackgroundAudioManager()`

### Vue 2 和 Vue 3 的 API `Promise 化`
> 返回结果不一致，以下为 `不同点` 和 `互相转换`

#### Vue 2

> 对部分 API 进行了 Promise 封装，返回数据的第一个参数是错误对象，第二个参数是返回数据。

**使用示例：**

```js
// 默认方式
uni.request({
	url: 'https://www.example.com/request',
	success: (res) => {
		console.log(res.data);
	},
	fail:(err) => {
		console.error(err)
	}
});

// Promise
uni.request({
		url: 'https://www.example.com/request'
	})
	.then(data => {
		// data为一个数组
		// 数组第一项为错误信息 即为 fail 回调
		// 第二项为返回数据
		var [err, res]  = data;
        console.log(res.data);
	})

// Await
async function request () {
	var [err, res] = await uni.request({
		url: 'https://www.example.com/request'
	});
	console.log(res.data);
}
```

#### Vue 3

> 对部分 API 进行了 Promise 封装，`then` 为 success 成功回调。`catch` 为 fail 失败回调

**使用示例：**

```js
// 默认方式
uni.request({
	url: 'https://www.example.com/request',
	success: (res) => {
		console.log(res.data);
	},
	fail:(err) => {
		console.error(err)
	}
});

// Promise
uni.request({
		url: 'https://www.example.com/request'
	})
	.then(res => {	// 此处即为 success 回调中的 res
		console.log(res.data);
	})
	.catch(err => {	// 此处即为 fail 回调中的 err
		console.error(err)
	})

// Await
async function request () {
	try{
		var res = await uni.request({
			url: 'https://www.example.com/request'
		});
		console.log(res); // 此处即为 success 回调中的 res
	} catch (err) {
		console.error(err) // 此处即为 fail 回调中的 err
	}
}
```

#### Vue 2 写法转 Vue 3 写法

```js
// 在 main.js 中写入以下代码即可
function isPromise (obj) {
  return !!obj && (typeof obj === 'object' || typeof obj === 'function') && typeof obj.then === 'function'
}

uni.addInterceptor({
  returnValue (res) {
    if (!isPromise(res)) {
      return res
    }
    return new Promise((resolve, reject) => {
      res.then(res => {
        if (res[0]) {
          reject(res[0])
        } else {
          resolve(res[1])
        }
      })
    })
  }
})
```

#### Vue 3 写法转 Vue 2 写法

```js
// 在 main.js 中写入以下代码即可
function isPromise (obj) {
  return !!obj && (typeof obj === 'object' || typeof obj === 'function') && typeof obj.then === 'function'
}

uni.addInterceptor({
	returnValue(res) {
		if (!isPromise(res)) {
			return res
		}
		const returnValue = [undefined, undefined]
		return res
			.then((res) => {
				returnValue[1] = res
			})
			.catch((err) => {
				returnValue[0] = err
			})
			.then(() => returnValue)
	}
})
```

### API 列表
#### 网络
##### 发起请求

|API|说明|
|:-|:-|
|[uni.request](api/request/request?id=request)|发起网络请求|

##### 上传、下载

|API|说明|
|:-|:-|
|[uni.uploadFile](api/request/network-file?id=uploadfile)|上传文件|
|[uni.downloadFile](api/request/network-file?id=downloadfile)|下载文件|

##### WebSocket

|API|说明|
|:-|:-|
|[uni.connectSocket](api/request/websocket?id=connectsocket)|创建 WebSocket 连接|
|[uni.onSocketOpen](api/request/websocket?id=onsocketopen)|监听 WebSocket 打开|
|[uni.onSocketError](api/request/websocket?id=onsocketerror)|监听 WebSocket 错误|
|[uni.sendSocketMessage](api/request/websocket?id=sendsocketmessage)|发送 WebSocket 消息|
|[uni.onSocketMessage](api/request/websocket?id=onsocketmessage)|接受 WebSocket 消息|
|[uni.closeSocket](api/request/websocket?id=closesocket)|关闭 WebSocket 连接|
|[uni.onSocketClose](api/request/websocket?id=onsocketclose)|监听 WebSocket 关闭|

##### SocketTask

|API|说明|
|---|---|
|[SocketTask.send](/api/request/socket-task?id=sockettasksend)		|通过 WebSocket 连接发送数据			|
|[SocketTask.close](/api/request/socket-task?id=sockettaskclose)		|关闭 WebSocket 连接					|
|[SocketTask.onOpen](/api/request/socket-task?id=sockettaskonopen)		|监听 WebSocket 连接打开事件			|
|[SocketTask.onClose](/api/request/socket-task?id=sockettaskonclose)		|监听 WebSocket 连接关闭事件			|
|[SocketTask.onError](/api/request/socket-task?id=sockettaskonerror)		|监听 WebSocket 错误事件				|
|[SocketTask.onMessage](/api/request/socket-task?id=sockettaskonmessage)	|监听 WebSocket 接受到服务器的消息事件	|

#### 媒体
##### 图片

|API|说明|
|:-|:-|
|[uni.chooseImage](api/media/image?id=chooseimage)|从相册选择图片，或者拍照|
|[uni.previewImage](api/media/image?id=previewimage)|预览图片|
|[uni.getImageInfo](api/media/image?id=getimageinfo)|获取图片信息|
|[uni.saveImageToPhotosAlbum](api/media/image?id=saveimagetophotosalbum)|保存图片到系统相册|

##### 文件

|API|说明|
|:-|:-|
|[uni.chooseFile](api/media/file?id=chooseFile)|从本地选择文件|

##### 录音管理

|API|说明|
|:-|:-|
|[uni.getRecorderManager](api/media/record-manager)|录音管理|

##### 背景音频播放管理

|API|说明|
|:-|:-|
|[uni.getBackgroundAudioManager](api/media/background-audio-manager)|背景音频播放管理|

##### 音频组件管理

|API|说明|
|:-|:-|
|[uni.createInnerAudioContext](api/media/audio-context)|音频组件管理|

##### 视频

|API|说明|
|:-|:-|
|[uni.chooseVideo](api/media/video?id=choosevideo)|从相册选择视频，或者拍摄|
|[uni.chooseMedia](api/media/video?id=choosemedia)|拍摄或从手机相册中选择图片或视频。|
|[uni.saveVideoToPhotosAlbum](api/media/video?id=savevideotophotosalbum)|保存视频到系统相册|
|[uni.createVideoContext](/api/media/video-context?id=createvideocontext)|视频组件管理|

##### 相机组件管理

|API|说明|
|:-|:-|
|[uni.createCameraContext](api/media/camera-context.md)|相机组件管理|

##### 直播组件管理

|API|说明|
|:-|:-|
|[uni.createLivePlayerContext](api/media/live-player-context.md)|直播组件管理|

#### 文件

|API|说明|
|:-|:-|
|[uni.saveFile](api/file/file?id=savefile)|保存文件|
|[uni.getSavedFileList](api/file/file?id=getsavedfilelist)|获取已保存的文件列表|
|[uni.getSavedFileInfo](api/file/file?id=getsavedfileinfo)|获取已保存的文件信息|
|[uni.removeSavedFile](api/file/file?id=removesavedfile)|删除已保存的文件信息|
|[uni.getFileInfo](/api/file/file?id=getfileinfo)|获取文件信息|
|[uni.openDocument](api/file/file?id=opendocument)|打开文件|


#### 数据缓存

|API|说明|
|:-|:-|
|[uni.getStorage](api/storage/storage?id=setstorage)|获取本地数据缓存|
|[uni.getStorageSync](api/storage/storage?id=setstoragesync)|获取本地数据缓存|
|[uni.setStorage](api/storage/storage?id=getstorage)|设置本地数据缓存|
|[uni.setStorageSync](api/storage/storage?id=getstoragesync)|设置本地数据缓存|
|[uni.getStorageInfo](api/storage/storage?id=getstorageinfo)|获取本地缓存的相关信息|
|[uni.getStorageInfoSync](api/storage/storage?id=getstorageinfosync)|获取本地缓存的相关信息|
|[uni.removeStorage](api/storage/storage?id=removestorage)|删除本地缓存内容|
|[uni.removeStorageSync](api/storage/storage?id=removestoragesync)|删除本地缓存内容|
|[uni.clearStorage](api/storage/storage?id=clearstorage)|清理本地数据缓存|
|[uni.clearStorageSync](api/storage/storage?id=clearstoragesync)|清理本地数据缓存|


#### 位置
##### 获取位置 

|API|说明|
|:-|:-|
|[uni.getLocation](api/location/location?id=getlocation)|获取当前位置|
|[uni.chooseLocation](api/location/location?id=chooselocation)|打开地图选择位置|

##### 查看位置

|API|说明|
|:-|:-|
|[uni.openLocation](api/location/open-location?id=openlocation)|打开内置地图|

##### 地图组件控制

|API|说明|
|:-|:-|
|[uni.createMapContext](api/location/map?id=createmapcontext)|地图组件控制|


#### 设备

##### 系统信息

|API|说明|
|:-|:-|
|[uni.getSystemInfo](api/system/info?id=getsysteminfo)|获取系统信息|
|[uni.getSystemInfoSync](api/system/info?id=getsysteminfosync)|获取系统信息|
|[uni.canIUse](/api/system/info?id=caniuse)|判断应用的 API，回调，参数，组件等是否在当前版本可用|

##### 网络状态

|API|说明|
|:-|:-|
|[uni.getNetworkType](api/system/network?id=getnetworktype)|获取网络类型|
|[uni.onNetworkStatusChange](api/system/network?id=onnetworkstatuschange)|监听网络状态变化|
|[uni.offNetworkStatusChange](api/system/network?id=offnetworkstatuschange)|取消监听网络状态变化|

##### 加速度计

|API|说明|
|:-|:-|
|[uni.onAccelerometerChange](api/system/accelerometer?id=onaccelerometerchange)|监听加速度数据|
|[uni.offAccelerometerChange](api/system/accelerometer?id=offaccelerometerchange)|取消监听加速度数据|
|[uni.startAccelerometer](api/system/accelerometer?id=startaccelerometer)|开始监听加速度数据|
|[uni.stopAccelerometer](api/system/accelerometer?id=stopaccelerometer)|停止监听加速度数据|

##### 罗盘

|API|说明|
|:-|:-|
|[uni.onCompassChange](api/system/compass?id=oncompasschange)|监听罗盘数据|
|[uni.offCompassChange](api/system/compass?id=offcompasschange)|取消监听罗盘数据|
|[uni.startCompass](api/system/compass?id=startcompass)|开始监听罗盘数据|
|[uni.stopCompass](api/system/compass?id=stopcompass)|停止监听罗盘数据|


##### 拨打电话

|API|说明|
|:-|:-|
|[uni.makePhoneCall](api/system/phone?id=makephonecall)|拨打电话|

##### 扫码

|API|说明|
|:-|:-|
|[uni.scanCode](api/system/barcode?id=scancode)|扫码|

##### 剪切板

|API|说明|
|:-|:-|
|[uni.setClipboardData](api/system/clipboard?id=setclipboarddata)|设置剪贴板内容|
|[uni.getClipboardData](api/system/clipboard?id=getclipboarddata)|获取剪贴板内容|

##### 屏幕亮度

|API|说明|
|:-|:-|
|[uni.setScreenBrightness](api/system/brightness?id=setscreenbrightness)|设置屏幕亮度|
|[uni.getScreenBrightness](api/system/brightness?id=getscreenbrightness)|获取屏幕亮度|
|[uni.setKeepScreenOn](api/system/brightness?id=setkeepscreenon)|设置是否保持常亮状态|


##### 振动

|API|说明|
|:-|:-|
|[uni.vibrate](api/system/vibrate?id=vibrate)|使手机发生振动|
|[uni.vibrateLong](api/system/vibrate?id=vibratelong)|使手机发生较长时间的振动|
|[uni.vibrateShort](api/system/vibrate?id=vibrateshort)|使手机发生较短时间的振动|

##### 手机联系人

|API|说明|
|:-|:-|
|[uni.addPhoneContact](api/system/contact?id=addphonecontact)|添加手机通讯录|

##### 蓝牙

|API|说明|
|:-|:-|
|[uni.openBluetoothAdapter](/api/system/bluetooth?id=openbluetoothadapter)|初始化蓝牙模块|
|[uni.startBluetoothDevicesDiscovery](/api/system/bluetooth?id=startbluetoothdevicesdiscovery)|搜寻附近的蓝牙外围设备|
|[uni.onBluetoothDeviceFound](/api/system/bluetooth?id=onbluetoothdevicefound)|监听寻找到新设备的事件    |
|[uni.stopBluetoothDevicesDiscovery](/api/system/bluetooth?id=stopbluetoothdevicesdiscovery)|停止搜寻|
|[uni.onBluetoothAdapterStateChange](/api/system/bluetooth?id=onbluetoothadapterstatechange)|监听蓝牙适配器状态变化事件|
|[uni.getConnectedBluetoothDevices](/api/system/bluetooth?id=getconnectedbluetoothdevices)|根据 uuid 获取处于已连接状态的设备|
|[uni.getBluetoothDevices](/api/system/bluetooth?id=getbluetoothdevices)|获取已发现的蓝牙设备|
|[uni.getBluetoothAdapterState](/api/system/bluetooth?id=getbluetoothadapterstate)|获取本机蓝牙适配器状态|
|[uni.closeBluetoothAdapter](/api/system/bluetooth?id=closebluetoothadapter)|关闭蓝牙模块|

##### 低耗蓝牙

|API|说明|
|:-|:-|
|[uni.writeBLECharacteristicValue](/api/system/ble?id=writeblecharacteristicvalue)|向低功耗蓝牙设备特征值中写入二进制数据|
|[uni.readBLECharacteristicValue](/api/system/ble?id=readblecharacteristicvalue)|读取低功耗蓝牙设备的特征值的二进制数据值|
|[uni.onBLEConnectionStateChange](/api/system/ble?id=onbleconnectionstatechange)|监听低功耗蓝牙连接状态的改变事件|
|[uni.onBLECharacteristicValueChange](/api/system/ble?id=onblecharacteristicvaluechange)|监听低功耗蓝牙设备的特征值变化事件|
|[uni.notifyBLECharacteristicValueChange](/api/system/ble?id=notifyblecharacteristicvaluechange)|监听低功耗蓝牙设备的特征值变化事件|
|[uni.getBLEDeviceServices](/api/system/ble?id=getbledeviceservices)|获取蓝牙设备所有服务(service)|
|[uni.getBLEDeviceCharacteristics](/api/system/ble?id=getbledevicecharacteristics)|获取蓝牙设备某个服务中所有特征值(characteristic)|
|[uni.createBLEConnection](/api/system/ble?id=createbleconnection)|连接低功耗蓝牙设备|
|[uni.closeBLEConnection](/api/system/ble?id=closebleconnection)|断开与低功耗蓝牙设备的连接|

##### iBeacon

|API|说明|
|:-|:-|
|[uni.onBeaconServiceChange](/api/system/ibeacon?id=onbeaconservicechange)|监听 iBeacon 服务状态变化事件|
|[uni.onBeaconUpdate](/api/system/ibeacon?id=onbeaconupdate)|监听 iBeacon 设备更新事件|
|[uni.getBeacons](/api/system/ibeacon?id=getbeacons)|获取所有已搜索到的 iBeacon 设备|
|[uni.startBeaconDiscovery](/api/system/ibeacon?id=startbeacondiscovery)|停止搜索附近的 iBeacon 设备|
|[uni.stopBeaconDiscovery](/api/system/ibeacon?id=stopbeacondiscovery)|开始搜索附近的 iBeacon 设备|

##### 生物认证

|API|说明|
|:-|:-|
|[uni.startSoterAuthentication](/api/system/authentication?id=startsoterauthentication)|开始生物认证|
|[uni.checkIsSupportSoterAuthentication](/api/system/authentication?id=checkissupportsoterauthentication)|获取本机支持的生物认证方式|
|[uni.checkIsSoterEnrolledInDevice](/api/system/authentication?id=checkissoterenrolledindevice)|获取设备内是否录入如指纹等生物信息的接口|

#### 界面

##### 交互反馈

|API|说明|
|:-|:-|
|[uni.showToast](api/ui/prompt?id=showtoast)|显示提示框|
|[uni.showLoading](api/ui/prompt?id=showloading)|显示加载提示框|
|[uni.hideToast](api/ui/prompt?id=hidetoast)|隐藏提示框|
|[uni.hideLoading](api/ui/prompt?id=hideloading)|隐藏加载提示框|
|[uni.showModal](api/ui/prompt?id=showmodal)|显示模态弹窗|
|[uni.showActionSheet](api/ui/prompt?id=showactionsheet)|显示菜单列表|

##### 设置导航条

|API|说明|
|:-|:-|
|[uni.setNavigationBarTitle](api/ui/navigationbar?id=setnavigationbartitle)|设置当前页面标题|
|[uni.setNavigationBarColor](/api/ui/navigationbar?id=setnavigationbarcolor)|设置页面导航条颜色|
|[uni.showNavigationBarLoading](api/ui/navigationbar?id=shownavigationbarloading)|显示导航条加载动画|
|[uni.hideNavigationBarLoading](api/ui/navigationbar?id=hidenavigationbarloading)|隐藏导航条加载动画|

##### 设置TabBar

|API|说明|
|:-|:-|
|[uni.setTabBarItem](/api/ui/tabbar?id=settabbaritem)|动态设置 tabBar 某一项的内容|
|[uni.setTabBarStyle](/api/ui/tabbar?id=settabbarstyle)|动态设置 tabBar 的整体样式|
|[uni.hideTabBar](/api/ui/tabbar?id=hidetabbar)|隐藏 tabBar|
|[uni.showTabBar](/api/ui/tabbar?id=showtabbar)|显示 tabBar|
|[uni.setTabBarBadge](/api/ui/tabbar?id=settabbarbadge)|为 tabBar 某一项的右上角添加文本|
|[uni.removeTabBarBadge](/api/ui/tabbar?id=removetabbarbadge)|移除 tabBar 某一项右上角的文本|
|[uni.showTabBarRedDot](/api/ui/tabbar?id=showtabbarreddot)|显示 tabBar 某一项的右上角的红点|
|[uni.hideTabBarRedDot](/api/ui/tabbar?id=hidetabbarreddot)|隐藏 tabBar 某一项的右上角的红点|


##### 动画

|API|说明|
|:-|:-|
|[uni.createAnimation](/api/ui/animation?id=createanimation)|创建一个动画实例 animation。调用实例的方法来描述动画。最后通过动画实例的export方法导出动画数据传递给组件的animation属性。|

##### 滚动

|API|说明|
|:-|:-|
|[uni.pageScrollTo](/api/ui/scroll?id=pagescrollto)|将页面滚动到目标位置。|

##### 绘画

|API|说明|
|:-|:-|
|[uni.createCanvasContext](/api/canvas/createCanvasContext)|创建绘图上下文|
|[uni.canvasToTempFilePath](/api/canvas/canvasToTempFilePath)|将画布内容保存成文件|
|[uni.canvasGetImageData](/api/canvas/canvasGetImageData)|获取画布图像数据|
|[uni.canvasPutImageData](/api/canvas/canvasPutImageData)|设置画布图像数据|

##### 下拉刷新

|API|说明|
|:-|:-|
|[onPullDownRefresh](/api/ui/pulldown?id=onpulldownrefresh)|监听该页面用户下拉刷新事件|
|[uni.startPullDownRefresh](/api/ui/pulldown?id=startpulldownrefresh)|开始下拉刷新|
|[uni.stopPullDownRefresh](/api/ui/pulldown?id=stoppulldownrefresh)|停止当前页面下拉刷新|

##### 节点信息

|API|说明|
|:-|:-|
|[uni.createSelectorQuery](api/ui/nodes-info?id=createselectorquery)|创建查询请求|
|[selectorQuery.select](/api/ui/nodes-info?id=selectorquery-对象的方法列表)|根据选择器选择单个节点|
|[selectorQuery.selectAll](/api/ui/nodes-info?id=selectorquery-对象的方法列表)|根据选择器选择全部节点|
|[selectorQuery.selectViewport](/api/ui/nodes-info?id=selectorquery-对象的方法列表)|选择显示区域|
|[selectorQuery.exec](/api/ui/nodes-info?id=selectorquery-对象的方法列表)|执行查询请求|
|[nodesRef.boundingClientRect](/api/ui/nodes-info?id=nodesref-对象的方法列表)|获取布局位置和尺寸|
|[nodesRef.scrollOffset](/api/ui/nodes-info?id=nodesref-对象的方法列表)|获取滚动位置|
|[nodesRef.fields](/api/ui/nodes-info?id=nodesref-对象的方法列表)|获取任意字段|

##### 节点布局相交状态

|API|说明|
|:-|:-|
|[uni.createIntersectionObserver](api/ui/intersection-observer?id=createintersectionobserver)|创建 IntersectionObserver 对象|
|[intersectionObserver.relativeTo](/api/ui/intersection-observer?id=intersectionobserver-对象的方法列表)|指定参照节点|
|[intersectionObserver.relativeToViewport](/api/ui/intersection-observer?id=intersectionobserver-对象的方法列表)|指定页面显示区域作为参照区域|
|[intersectionObserver.observe](/api/ui/intersection-observer?id=intersectionobserver-对象的方法列表)|指定目标节点并开始监听|
|[intersectionObserver.disconnect](/api/ui/intersection-observer?id=intersectionobserver-对象的方法列表)|停止监听|


#### 路由

|API|说明|
|:-|:-|
|[uni.navigateTo](/api/router?id=navigateto)|保留当前页面，跳转到应用内的某个页面，使用uni.navigateBack可以返回到原页面|
|[uni.redirectTo](/api/router?id=redirectto)|关闭当前页面，跳转到应用内的某个页面|
|[uni.reLaunch](/api/router?id=relaunch)|关闭所有页面，打开到应用内的某个页面|
|[uni.switchTab](/api/router?id=switchtab)|跳转到 tabBar 页面，并关闭其他所有非 tabBar 页面|
|[uni.navigateBack](/api/router?id=navigateback)|关闭当前页面，返回上一页面或多级页面|


#### 平台扩展

|API|说明|
|:-|:-|
|[uni.requireNativePlugin](/api/extend/native-plugin?id=requirenativeplugin)|引入 App 原生插件|





