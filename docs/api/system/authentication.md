### 生物认证说明
### Biometric authentication instructions

生物认证，又称活体检测。它包含指纹识别、人脸识别这两部分。即通过人体身体特征来进行身份认证识别。
Biological authentication, also known as in vivo detection. It includes fingerprint recognition and face recognition. That is, carry on the identity authentication recognition  through human body characteristics.

### uni.startSoterAuthentication(OBJECT)

开始 SOTER 生物认证。
Start the SOTER biometric authentication.

**平台差异说明**
**Platform difference description**

|App				|H5|
|:-				|:-|
|√（2.3.8+）	|x	|

App端在2.3.8版以前，可在插件市场获取[指纹相关插件](https://ext.dcloud.net.cn/plugin?id=358)。
For APP side 2.3.8-, [Fingerprint related plug-ins](https://ext.dcloud.net.cn/plugin?id=358) can be obtained in the plug-in market.

**OBJECT参数说明**
**OBJECT parameter description**

|属性					|类型		|默认值	|必填	|说明					| 平台差异说明	|
| Attribute| Type| Defaults| Required| Instruction| Platform difference description|
|:-					|:-		|:-		|:-	|:-				|:-					|
|requestAuthModes	|Array	|			|是	|请求使用的可接受的生物认证方式		|APP		|
| requestAuthModes| Array| | Yes| Acceptable biometric authentication method requested| APP|
|authContent		|String	|''		|否	|验证描述，即识别过程中显示在界面上的对话框提示内容	|APP|
| authContent| String| ''| No| Verification description, that is the contents of the dialog box displayed on the interface during identification.| APP|
|success				|Function|			|否	|接口调用成功的回调函数	|						|
| success| Function| | No| Callback function for successful interface calling| |
|fail					|Function|			|否	|接口调用失败的回调函数	|						|
| fail| Function| | No| Callback function for failed interface calling| |
|complete			|Function|			|否	|接口调用结束的回调函数（调用成功、失败都会执行）	|						|
| complete| Function| | No| Callback function for closed interface calling (available both for successful and failed calling)| |


**OBJECT.requestAuthModes说明**
**OBJECT.requestAuthModes description**

|值					|说明			|
| Value| Instruction|
|:-					|:-				|
|fingerPrint|指纹识别	|
| fingerPrint| Fingerprint identification|
|facial			|人脸识别	|
| facial| Face identification|

注意：
Notice:
- App端指纹识别，Android平台从Android6.0起才提供了官方API，uni-app也是从Android6起支持。对于更低版本的安卓，某些rom私有的指纹识别API，uni-app并不支持。
- The official API of App side fingerprint recognition was not provided on the Android platform until Android6.0, and so was it on uni-app. For lower versions of Android, some rom has non official fingerprint APIs but they are not supported on uni-App.
- App端人脸识别，iOS平台使用自带的faceID，而Android平台需要依赖三方SDK方可实现，可在插件市场搜索[人脸识别](https://ext.dcloud.net.cn/search?q=%E4%BA%BA%E8%84%B8%E8%AF%86%E5%88%AB)插件
- Regarding the face recognition on the App side, the iOS platform uses its own faceID, while the Android platform needs to rely on a third-party SDK to realize face recognition. You can search for the [Face recognition](https://ext.dcloud.net.cn/search?q=%E4%BA%BA%E8%84%B8%E8%AF%86%E5%88%AB) plug-in in the plug-in market.


**OBJECT.success返回值说明**
**Description of return value of OBJECT.success**

|属性						|类型		|说明			|平台差异说明	|
| Attribute| Type| Instruction| Platform difference description|
|:-						|:-		|:-			|:-				|
|authMode				|string	|生物认证方式|APP				|
| authMode| string| Biometric authentication method| APP|
|errCode					|number	|错误码		|					|
| errCode| number| Error code| |
|errMsg					|string	|错误信息		|					|
| errMsg| string| Error message| |


**错误码说明**
**Error code description**

|错误码	|错误码说明																				|
| Error code| Error code description|
|:-			|:-																								|
|0			|识别成功																					|
| 0| Identification successful|
|90001	|本设备不支持生物认证														|
| 90001| This device does not support biometric authentication.|
|90002	|用户未授权使用该生物认证接口											|
| 90002| The user is not authorized to use the biometric authentication interface|
|90003	|请求使用的生物认证方式不支持											|
| 90003| The requested biometric authentication method is not supported|
|90004	|未传入challenge或challenge长度过长（最长512字符）|
| 90004| No challenge was passed in or the length of the challenge is too long (the maximum length is 512 characters)|
|90005	|auth_content长度超过限制（最长42个字符）					|
| 90005| auth_content length exceeds the limit (the maximum is 42 characters)|
|90007	|内部错误																					|
| 90007| Internal error|
|90008	|用户取消授权																			|
| 90008| User authorization cancellation|
|90009	|识别失败																					|
| 90009| Identification failed|
|90010	|重试次数过多被冻结																|
| 90010| Blocked due to too many retries|
|90011	|用户未录入所选识别方式														|
| 90011| User has not entered the selected identification method.|

### uni.checkIsSupportSoterAuthentication(OBJECT)

获取本机支持的 SOTER 生物认证方式
Obtain the supported SOTER biometric authentication mode

**OBJECT参数说明**
**OBJECT parameter description**

|属性			|类型			|默认值	|必填	|说明																							|
| Attribute| Type| Defaults| Required| Instruction|
|:-				|:-				|:-			|:-		|:-																								|
|success	|function	|				|否		|接口调用成功的回调函数														|
| success| function| | No| Callback function for successful interface calling|
|fail			|function	|				|否		|接口调用失败的回调函数														|
| fail| function| | No| Callback function for failed interface calling|
|complete	|function	|				|否		|接口调用结束的回调函数（调用成功、失败都会执行）	|
| complete| function| | No| Callback function for closed interface calling (available both for successful and failed calling)|

**OBJECT.success返回值说明**
**Description of return value of OBJECT.success**

|属性				|类型	|说明																		|
| Attribute| Type| Instruction|
|:-					|:-		|:-																			|
|supportMode|Array|该设备支持的可被SOTER识别的生物识别方式|
| supportMode| Array| Biometrics supported by this device that can be recognized by SOTER|

### uni.checkIsSoterEnrolledInDevice(OBJECT)

获取设备内是否录入如指纹等生物信息的接口
Interface for requesting whether biological information such as fingerprints are entered in the device

**OBJECT参数说明**
**OBJECT parameter description**

|属性					|类型			|默认值	|必填	|说明																							|
| Attribute| Type| Defaults| Required| Instruction|
|:-:					|:-:			|:-:		|:-:	|:-:																							|
|checkAuthMode|string		|				|是		|认证方式																					|
| checkAuthMode| string| | Yes| Verification method|
|success			|function	|				|否		|接口调用成功的回调函数														|
| success| function| | No| Callback function for successful interface calling|
|fail					|function	|				|否		|接口调用失败的回调函数														|
| fail| function| | No| Callback function for failed interface calling|
|complete			|function	|				|否		|接口调用结束的回调函数（调用成功、失败都会执行）	|
| complete| function| | No| Callback function for closed interface calling (available both for successful and failed calling)|

**OBJECT.checkAuthMode合法值**
**OBJECT.checkAuthMode legal values**

|值					|说明			|
| Value| Instruction|
|:-					|:-				|
|fingerPrint|指纹识别	|
| fingerPrint| Fingerprint identification|
|facial			|人脸识别	|
| facial| Face identification|

**OBJECT.success返回值说明**
**Description of return value of OBJECT.success**

|属性				|类型		|说明						|
| Attribute| Type| Instruction|
|:-					|:-			|:-							|
|isEnrolled	|boolean|是否已录入信息	|
| isEnrolled| boolean| Whether the information has been entered|
|errMsg			|string	|错误信息				|
| errMsg| string| Error message|

#### 代码示例
#### Code example

```html

<template>
	<view class="content">
		<button type="primary" @click="checkIsSupportSoterAuthentication">Check the supported authentication method</button>
		<button type="primary" @click="checkIsSoterEnrolledInDeviceFingerPrint">Check the fingerprint entered or not</button>
		<button type="primary" @click="checkIsSoterEnrolledInDeviceFaceID">Check the FaceID entered or not</button>
		<button type="primary" @click="startSoterAuthenticationFingerPrint">Start fingerprint authentication</button>
		<button type="primary" @click="startSoterAuthenticationFaceID">Start FaceID authentication</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
			}
		},
		onLoad() {

		},
		methods: {
			checkIsSupportSoterAuthentication() {
				uni.checkIsSupportSoterAuthentication({
					success(res) {
						console.log(res);
					},
					fail(err) {
						console.log(err);
					},
					complete(res) {
						console.log(res);
					}
				})
			},
			checkIsSoterEnrolledInDeviceFingerPrint() {
				uni.checkIsSoterEnrolledInDevice({
					checkAuthMode: 'fingerPrint',
					success(res) {
						console.log(res);
					},
					fail(err) {
						console.log(err);
					},
					complete(res) {
						console.log(res);
					}
				})
			},
			checkIsSoterEnrolledInDeviceFaceID() {
				uni.checkIsSoterEnrolledInDevice({
					checkAuthMode: 'facial',
					success(res) {
						console.log(res);
					},
					fail(err) {
						console.log(err);
					},
					complete(res) {
						console.log(res);
					}
				})
			},
			startSoterAuthenticationFingerPrint() {
				uni.startSoterAuthentication({
					requestAuthModes: ['fingerPrint'],
					challenge: '123456',
					authContent: 'Please unlock with your fingerprint',
					success(res) {
						console.log(res);
					},
					fail(err) {
						console.log(err);
					},
					complete(res) {
						console.log(res);
					}
				})
			},
			startSoterAuthenticationFaceID() {
				uni.startSoterAuthentication({
					requestAuthModes: ['facial'],
					challenge: '123456',
					authContent: 'Please unlock with FaceID',
					success(res) {
						console.log(res);
					},
					fail(err) {
						console.log(err);
					},
					complete(res) {
						console.log(res);
					}
				})
			}
		}
	}
</script>

<style>
	button {
		width: 200px;
		margin: 20px auto;
	}
</style>


```

#### 注意事项
#### Precautions

- App端自2.3.8版本起开始支持生物认证，更低版本或想使用指纹功能，可在插件市场获取[插件](https://ext.dcloud.net.cn/plugin?id=358)
- From App side 2.3.8+, biometric authentication is supported. For lower versions or if you want to use the fingerprint function, you can obtain the [Plug-in](https://ext.dcloud.net.cn/plugin?id=358) in the plug-in market.
- App端的人脸识别，仅支持iOS端的faceID。Android端需要依赖三方SDK方可实现，可在插件市场搜索[人脸识别](https://ext.dcloud.net.cn/search?q=%E4%BA%BA%E8%84%B8%E8%AF%86%E5%88%AB)插件
- Face recognition on the App side only supports faceID on the iOS side. The Android side needs to rely on a third-party SDK to realize face recognition. You can search for the [Face recognition](https://ext.dcloud.net.cn/search?q=%E4%BA%BA%E8%84%B8%E8%AF%86%E5%88%AB) plug-in in the plug-in market.
- App端打包时，注意需要在manifest的模块中选择指纹和faceID，否则打包后无法运行相关功能。
- When packaging the App side, select fingerprint and faceID in the manifest module, or otherwise, related functions cannot run after packaging.
- hello uni-app已经集成相关示例，最新版HBuilderX新建新版hello uni-app示例项目真机运行可见，在API-设备-生物认证里。
- hello uni-app has integrated relevant examples, and the latest version of HBuilderX creates a new version of hello uni-app example project, which can be seen in the mobile App Playground operation, in API- device-biometric authentication.
