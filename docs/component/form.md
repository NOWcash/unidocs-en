#### form
表单，将组件内的用户输入的``<switch>`` ``<input>`` ``<checkbox>`` ``<slider>`` ``<radio>`` ``<picker>`` 提交。
Form, submit the `<switch>` `<input>` `<checkbox>` `<slider>` `<radio>` `<picker>` input by the user in the component.

当点击 ``<form>`` 表单中 formType 为 submit 的 ``<button>`` 组件时，会将表单组件中的 value 值进行提交，需要在表单组件中加上 name 来作为 key。
When you click on the `<button>` component with the formType of submit in the `<form>` form, the value in the form component will be submitted, and the name must be added to the form component as the key.

**属性说明**
**Attribute description**

|属性名|类型|说明|平台差异说明|
| Attribute name| Type| Instruction| Platform difference description|
|:-|:-|:-|:-|
|report-submit|Boolean|是否返回 formId 用于发送[模板消息](https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/template-message.html)|微信小程序、支付宝小程序|
|report-submit|Boolean|Whether formId is returned for sending [template message](https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/template-message.html)|WeChat Mini Program , Alipay applet |
|report-submit-timeout|number|等待一段时间（毫秒数）以确认 formId 是否生效。如果未指定这个参数，formId 有很小的概率是无效的（如遇到网络失败的情况）。指定这个参数将可以检测 formId 是否有效，以这个参数的时间作为这项检测的超时时间。如果失败，将返回 requestFormId:fail 开头的 formId|微信小程序2.6.2|
|report-submit-timeout|number|Wait a period of time (in milliseconds) for formId to take effect. If this parameter is not specified, there is a small chance that the formId will be invalid (such as in the case of a network failure). Specifying this parameter will check whether the formId is valid, and use the time of this parameter as the timeout for this check. If it fails, it will return the formId starting with requestFormId:fail|WeChat Mini Program 2.6.2|
|@submit|EventHandle|携带 form 中的数据触发 submit 事件，event.detail = {value : {'name': 'value'} , formId: ''}，report-submit 为 true 时才会返回 formId||
| @submit| EventHandle| Carrying the data in the form will trigger the submit event, event.detail = {value : {'name': 'value'} , formId: ''}, formId will only be returned when report-submit is true| |
|@reset|EventHandle|表单重置时会触发 reset 事件|&nbsp;|
| @reset| EventHandle| The reset event will be triggered when the form is reset|  |

**示例** [查看演示](https://hellouniapp.dcloud.net.cn/pages/component/form/form)
**Example** [View demo](https://hellouniapp.dcloud.net.cn/pages/component/form/form)
 
以下示例代码，来自于[hello uni-app项目](https://github.com/dcloudio/hello-uniapp)，推荐使用HBuilderX，新建uni-app项目，选择hello uni-app模板，可直接体验完整示例。
The following sample code comes from the [hello uni-app project](https://github.com/dcloudio/hello-uniapp). It is recommended to use HBuilderX to create a new uni-app project and choose the hello uni-app template to directly experience the complete example.

::: preview https://hellouniapp.dcloud.net.cn/pages/component/form/form
> Template
``` vue
<!-- 本示例未包含完整css，获取外链css请参考上文，在hello uni-app项目中查看 -->
<!-- This example does not include the complete css, please refer to the above to obtain the external css. View it in the hello uni-app project -->
<template>
	<view>
		<view>
			<form @submit="formSubmit" @reset="formReset">
				<view class="uni-form-item uni-column">
					<view class="title">switch</view>
					<view>
						<switch name="switch" />
					</view>
				</view>
				<view class="uni-form-item uni-column">
					<view class="title">radio</view>
					<radio-group name="radio">
						<label>
							<radio value="radio1" /><text>选项一</text>
						</label>
						<label>
							<radio value="radio2" /><text>选项二</text>
						</label>
					</radio-group>
				</view>
				<view class="uni-form-item uni-column">
					<view class="title">checkbox</view>
					<checkbox-group name="checkbox">
						<label>
							<checkbox value="checkbox1" /><text>选项一</text>
						</label>
						<label>
							<checkbox value="checkbox2" /><text>选项二</text>
						</label>
					</checkbox-group>
				</view>
				<view class="uni-form-item uni-column">
					<view class="title">slider</view>
					<slider value="50" name="slider" show-value></slider>
				</view>
				<view class="uni-form-item uni-column">
					<view class="title">input</view>
					<input class="uni-input" name="input" placeholder="这是一个输入框" />
				</view>
				<view class="uni-btn-v">
					<button form-type="submit">Submit</button>
					<button type="default" form-type="reset">Reset</button>
				</view>
			</form>
		</view>
	</view>
</template>
``` 
> Script
``` vue
<script>
	export default {
		data() {
			return {
			}
		},
		methods: {
			formSubmit: function(e) {
				console.log('form发生了submit事件，携带数据为：' + JSON.stringify(e.detail.value))
				var formdata = e.detail.value
				uni.showModal({
					content: '表单数据内容：' + JSON.stringify(formdata),
					showCancel: false
				});
			},
			formReset: function(e) {
				console.log('清空数据')
			}
		}
	}
</script>
``` 
> Style
``` vue
<style>
	.uni-form-item .title {
		padding: 20rpx 0;
	}
</style>
```
:::


**使用内置 behaviors**
**Use built-in behaviors**

小程序端在`form`内的自定义组件内有`input`表单控件时，或者用普通标签实现表单控件，例如``评分``等，无法在`form`的`submit`事件内获取组件内表单控件值，此时可以使用`behaviors`。
When the applet has an `input` form control in a custom component in `form`, or implements a form control with ordinary tags, such as `rating`, etc., the component cannot be obtained in the `submit` event of `form` Inner form control values, `behaviors` can be used in this case.

对于 form 组件，目前可以自动识别下列内置 behaviors:
For form components, the following built-in behaviors can be automatically recognized at present:

uni://form-field

> 目前仅支持 微信小程序、QQ小程序、百度小程序、h5。
> Currently only supports WeChat applet, QQ applet, Baidu applet, h5.

**uni://form-field**

使自定义组件有类似于表单控件的行为。 form 组件可以识别这些自定义组件，并在 submit 事件中返回组件的字段名及其对应字段值。这将为它添加以下两个属性。
Make custom components behave like form controls. form component can identify these custom components, and return the field names of the components and their corresponding field values in submit event. This will add the following two attributes to it.

|属性名|类型|描述|
| Attribute name| Type| Describe|
|:-|:-|:-|
|name|String|在表单中的字段名|
| name| String| Field name in the form|
|value|任意|在表单中的字段值|
| value| Arbitrary| Field value in the form|

示例如下：
The following is an example:

```html
<!-- /pages/index/index.vue -->
<template>  
    <view class="content">  
        <form @submit="onSubmit">  
            <comp-input name="test" v-model="testValue"></comp-input>  
            <button form-type="submit">Submit</button>  
        </form>  
    </view>  
</template>  

<script>  
    export default {  
        data() {  
            return {  
                testValue: 'Hello'  
            }  
        },  
        methods: {  
            onSubmit(e) {  
                console.log(e)  
            }  
        }  
    }  
</script>  

<style>  

</style>
```

```html
<!-- /components/compInput/compInput.vue -->
<template>  
    <view>  
        <input name="test" style="border: solid 1px #999999;height: 80px;" type="text" @input="onInput" :value="value" />  
    </view>  
</template>  

<script>  
    export default {  
        name: 'compInput',  
        behaviors: ['uni://form-field'],
        methods: {  
            onInput(e) {  
                this.$emit('input', e.detail.value)  
            }  
        }  
    }  
</script>  

<style>  

</style>  
```


**增强的uni-forms组件**
**Enhanced uni-forms component**
- 为方便做表单验证，uni ui提供了`<uni-forms>`组件，参考：[https://ext.dcloud.net.cn/plugin?id=2773](https://ext.dcloud.net.cn/plugin?id=2773)
- For the convenience of form validation, uni ui provides the `<uni-forms>` component, refer to [https://ext.dcloud.net.cn/plugin?id=2773](https://ext.dcloud.net.cn/plugin?id=2773)
- 如果使用uniCloud，其数据库提供了`DB Schema`，在schema中配置字段的格式，前端表单校验和服务器入参校验将可以复用该规则，无需在前端后端重复开发表单校验。[详见](https://uniapp.dcloud.io/uniCloud/schema)
- If you use uniCloud whose database provides `DB Schema`, configure the format of the field in the schema, the front-end form validation and the server input validation will be able to reuse this rule without repeating the development of the form validation in the front-end and back-end. [See details](https://uniapp.dcloud.io/uniCloud/schema)
- 有很多表单自助生成辅助工具
- There are many auxiliary tools to automatically generate forms
  * 如果使用uniCloud的`DB Schema`可以自动生成全套表单，包括界面、校验逻辑、提交入库，[详见](https://uniapp.dcloud.io/uniCloud/schema?id=autocode).
  * If uniCloud's `DB Schema` is used, a full set of forms can be automatically generated, including the interface, verification logic, and submission to the library. [See details](https://uniapp.dcloud.io/uniCloud/schema?id=autocode).
  * 不使用uniCloud的话，插件市场有可视化拖拽表单插件：[详见](https://ext.dcloud.net.cn/search?q=%E5%8F%AF%E8%A7%86%E5%8C%96)。这类插件只生成界面，没有逻辑。
  * If uniCloud is not used, there are visual drag-and-drop form plug-ins in the plug-in market: [See details](https://ext.dcloud.net.cn/search?q=%E5%8F%AF%E8%A7%86%E5%8C%96). Such plug-ins only generate interfaces without logic.
