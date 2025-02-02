

::: tip 组件名：uni-easyinput
::: tip Component name: uni-easyinput
> 代码块： `uEasyinput`
> Code block: `uEasyinput`

[点击下载&安装](https://ext.dcloud.net.cn/plugin?name=uni-easyinput)
[Click to download & install](https://ext.dcloud.net.cn/plugin?name=uni-easyinput)
:::


easyinput 组件是对原生input组件的增强 ，是专门为配合表单组件[uni-forms](https://ext.dcloud.net.cn/plugin?id=2773)而设计的，easyinput 内置了边框，图标等，同时包含 input 所有功能
The easyinput component is an enhancement of the native input component. It is specially designed to cooperate with the form component [uni-forms](https://ext.dcloud.net.cn/plugin?id=2773). Easyinput has built-in borders and icons. etc., including all functions of input at the same time

## 介绍
## introduce

### 基本用法
### Basic usage

输入内容后，输入框尾部会显示清除按钮，点击可清除内容，如不需要展示图标，`clearable` 属性设置为 `false` 即可
After entering the content, a clear button will be displayed at the end of the input box. Click to clear the content. If you do not need to display the icon, set the `clearable` property to `false`

`clearable` 属性设置为 `true` ，输入框聚焦且内容不为空时，才会显示内容
The `clearable` property is set to `true` , the content will only be displayed when the input box is focused and the content is not empty

```html
<uni-easyinput v-model="value" placeholder="请输入内容"></uni-easyinput>
```


### 输入框带左右图标
### Input box with left and right icons

设置 `prefixIcon` 属性来显示输入框的头部图标
Set the `prefixIcon` property to display the header icon of the input field

设置 `suffixIcon` 属性来显示输入框的尾部图标 
Set the `suffixIcon` property to display the suffix icon of the input field

注意图标当前只支持 `uni-icons` 内置的图标，当配置 `suffixIcon` 属性后，会覆盖 `:clearable="true"` 和 `type="password"` 时的原有图标
Note that the icon currently only supports the built-in icon of `uni-icons`. When the `suffixIcon` property is configured, the original icon when `:clearable="true"` and `type="password"` is overwritten

绑定 `@iconClick` 事件可以触发图标的点击 ，返回 `prefix` 表示点击左侧图标，返回 `suffix` 表示点击右侧图标
Binding the `@iconClick` event can trigger the click of the icon, returning `prefix` means clicking the left icon, returning `suffix` means clicking the right icon

```html

<!-- 输入框头部图标 -->
<!-- Input box header icon -->
<uni-easyinput prefixIcon="search" v-model="value" placeholder="请输入内容" @iconClick="onClick"></uni-easyinput>
<!-- 展示输入框尾部图标 -->
<!-- Display the icon at the end of the input box -->
<uni-easyinput suffixIcon="search"  v-model="value" placeholder="请输入内容" @iconClick="onClick"></uni-easyinput>
```

### 输入框禁用
### input box disabled

设置 `disable` 属性可以禁用输入框，此时输入框不可编辑
Set the `disable` property to disable the input box, in this case the input box is not editable

```html
<uni-easyinput disabled  v-model="value" placeholder="请输入内容"></uni-easyinput>
```

### 密码框
### Password box

设置 `type="password"` 时，输入框内容将会不可见，由实心点代替，同时输入框尾部会显示眼睛图标，点击可切换内容显示状态
When `type="password"` is set, the content of the input box will be invisible, replaced by solid dots, and the eye icon will be displayed at the end of the input box, click to switch the content display state

```html
<uni-easyinput type="password" v-model="password" placeholder="请输入密码"></uni-easyinput>
```

### 输入框聚焦
### input field focus

设置 `focus` 属性可以使输入框聚焦
Set the `focus` property to focus the input field

如果页面存在多个设置 `focus` 属性的输入框，只有最后一个输入框的 `focus` 属性会生效
If there are multiple input boxes with the `focus` property set on the page, only the `focus` property of the last input box will take effect

```html
<uni-easyinput focus v-model="password" placeholder="请输入内容"></uni-easyinput>
```


### 多行文本
### Multi-line text

设置 `type="textarea"` 时可输入多行文本
Multiple lines of text can be entered when `type="textarea"` is set

```html
<uni-easyinput type="textarea" v-model="value" placeholder="请输入内容"></uni-easyinput>
```

### 多行文本自动高度
### Multi-line text auto height

设置 `type="textarea"` 时且设置 `autoHeight` 属性，可使用多行文本的自动高度，会跟随内容调整输入框的显示高度
When `type="textarea"` is set and the `autoHeight` property is set, the automatic height of multi-line text can be used, and the display height of the input box will be adjusted according to the content

```html
<uni-easyinput type="textarea" autoHeight v-model="value" placeholder="请输入内容"></uni-easyinput>
```

### 取消边框
### Cancel the border

设置 `:inputBorder="false"` 时可取消输入框的边框显示，同时搭配 `uni-forms` 的 `:border="true"` 有较好的效果
When `:inputBorder="false"` is set, the border display of the input box can be canceled, and the `:border="true"` of `uni-forms` has a better effect.

```html
<uni-forms border>
	<uni-forms-item label="姓名">
		<uni-easyinput :inputBorder="false" placeholder="请输入姓名"></uni-easyinput>
	</uni-forms-item>
	<uni-forms-item label="年龄">
		<uni-easyinput :inputBorder="false" placeholder="请输入年龄"></uni-easyinput>
	</uni-forms-item>
</uni-forms>
```


## API

### Easyinput Props

|属性名| 类型|	可选值|默认值|说明|
|property name|type|optional value|default value|description|
|:-:|:-:|:-:|:-:|:-:|
|value|String/ Number|-|-|输入内容|
|value|String/ Number|-|-|Input Content|
|type|String|见 type Options|text|输入框的类型（默认text）|
|type|String|See type Options|text|Type of input box (default text)|
|clearable|Boolean|-|true| 是否显示右侧清空内容的图标控件(输入框有内容且不禁用时显示)，点击可清空输入框内容|
|clearable|Boolean|-|true| Whether to display the icon control on the right to clear the content (displayed when the input box has content and is not disabled), click to clear the content of the input box|
|autoHeight|Boolean|-|false|	是否自动增高输入区域，type为textarea时有效|
|autoHeight|Boolean|-|false| Whether to automatically increase the input area, valid when type is textarea|
|placeholder|String |-| - |	输入框的提示文字|
|placeholder|String |-| - | The prompt text of the input box|
|placeholderStyle|String| -	| - |	placeholder的样式(内联样式，字符串)，如"color: #ddd"|
|placeholderStyle|String| - | - | The style of placeholder (inline style, string), such as "color: #ddd"|
|focus|Boolean|-|false|是否自动获得焦点|
|focus|Boolean|-|false|Automatically get focus|
|disabled|Boolean|-|false|是否不可输入|
|disabled|Boolean|-|false|Cannot be entered|
|maxlength|Number|-|140|最大输入长度，设置为 -1 的时候不限制最大长度|
|maxlength|Number|-|140|Maximum input length, when set to -1, the maximum length is not limited|
|confirmType|String|-|done|设置键盘右下角按钮的文字，仅在type="text"时生效|
|confirmType|String|-|done|Set the text of the button in the lower right corner of the keyboard, it only takes effect when type="text"|
|clearSize|Number|-|15|清除图标的大小，单位px|
|clearSize|Number|-|15|The size of the clear icon, in px|
|prefixIcon|String|-|-|输入框头部图标	|
|prefixIcon|String|-|-|Input box header icon |
|suffixIcon|String|-|-|输入框尾部图标|
|suffixIcon|String|-|-|input box tail icon|
|trim|Boolean/String|见 trim Options	| false |	是否自动去除空格，传入类型为 Boolean 时，自动去除前后空格|
|trim|Boolean/String|See trim Options | false | Whether to automatically remove spaces, when the incoming type is Boolean, automatically remove the spaces before and after |
|inputBorder|Boolean|-|true|是否显示input输入框的边框|
|inputBorder|Boolean|-|true|Whether to display the border of the input box|
|styles|Object|-|-|	样式自定义|
|styles|Object|-|-| Style customization|
|passwordIcon|Boolean|-| true |	type=password 时，是否显示小眼睛图标|
|passwordIcon|Boolean|-| true | When type=password, whether to display the small eye icon|


#### Type Options

|属性名| 说明|
|property name| description|
|:-:| :-:|
|text|文本输入键盘|
|text|Text Input Keyboard|
|textarea|多行文本输入键盘|
|textarea|Multiline Text Input Keyboard|
|password|密码输入键盘|
|password|Password Input Keyboard|
|number|数字输入键盘，注意iOS上app-vue弹出的数字键盘并非9宫格方式	|
|number|Number input keyboard, note that the number keyboard popped up by app-vue on iOS is not a 9-square grid |
|idcard|身份证输入键盘，仅支持微信、支付宝、百度、QQ小程序|
|idcard|ID card input keyboard, only supports WeChat, Alipay, Baidu, QQ applet|
|digit|带小数点的数字键盘，仅支持微信、支付宝、百度、头条、QQ小程序	|
|digit|Numeric keyboard with decimal point, only supports WeChat, Alipay, Baidu, Toutiao, QQ applet |

#### ConfirmType Options

平台差异与 [input](https://uniapp.dcloud.io/component/input) 相同
Platform differences are the same as [input](https://uniapp.dcloud.io/component/input)

|属性名| 说明|
|property name| description|
|:-:| :-:|
|send|右下角按钮为“发送”|
|send|The button in the lower right corner is "Send"|
|search	|右下角按钮为“搜索”|
|search |The bottom right button is "Search"|
|next|右下角按钮为“下一个”|
|next|The button in the lower right corner is "Next"|
|go|右下角按钮为“前往”	|											
|go| The button in the lower right corner is "Go" |
|done|右下角按钮为“完成”|
|done|The bottom right button is "Done"|
	

#### Styles Options 
	
|属性名| 默认值 	|说明|
|property name| default value |description|
|:-:| :-:| :-:|
|color| #333|输入文字颜色|
|color| #333|Enter text color|
|disableColor|#eee|	输入框禁用背景色|
|disableColor|#eee| Disable background color of input box|
|borderColor|#e5e5e5	|	边框颜色|
|borderColor|#e5e5e5 | Border Color|

#### Trim Options

传入类型为 `Boolean` 时，自动去除前后空格,传入类型为 `String` 时，可以单独控制，下面是可选值
When the incoming type is `Boolean`, the spaces before and after are automatically removed. When the incoming type is `String`, it can be controlled separately. The following are optional values

|属性名|说明|
|property name|description|
|:-:| :-:|
|both|去除两端空格|
|both|remove spaces at both ends|
|left|去除左侧空格|
|left|Remove left spaces|
|right|去除右侧空格|
|right|Remove right spaces|
|all|去除所有空格|
|all|Remove all spaces|
|none|不去除空格|
|none|Does not strip spaces|


### Easyinput Events

|事件称名| 说明|返回值|兼容说明|
|EventName|Description|Return Value|Compatibility Description|
|:-:| :-:|:-:|:-:|
|@input|输入框内容发生变化时触发| -||
|@input|Triggered when the content of the input box changes | -||
|@clear|点击右侧叉号图标时触发| -|1.1.0新增|
|@clear|Triggered when the right cross icon is clicked| -|New in 1.1.0|
|@focus|输入框获得焦点时触发| -||
|@focus|Triggered when the input box gets focus| -||
|@blur|输入框失去焦点时触发| -||
|@blur| Fired when the input box loses focus| -||
|@confirm|点击完成按钮时触发| -||
|@confirm|Triggered when done button is clicked| -||
|@iconClick	|点击图标时触发| prefix/suffix	||
|@iconClick | Fired when an icon is clicked | prefix/suffix ||
|@change|仅在输入框失去焦点或用户按下回车时触发||1.1.0新增|
|@change|Only triggered when the input box loses focus or the user presses enter||New in 1.1.0|


## 示例
## Example
::: warning 注意
::: warning attention
示例依赖了 `uni-card` `uni-section` `uni-scss` 等多个组件，直接拷贝示例代码将无法正常运行 。
The example relies on multiple components such as `uni-card` `uni-section` `uni-scss`, copying the example code directly will not work properly.

请到 [组件下载页面](https://ext.dcloud.net.cn/plugin?name=uni-easyinput) ，在页面右侧选择 `使用 HBuilderX导入示例项目` ，体验完整组件示例。
Please go to the [Component download page](https://ext.dcloud.net.cn/plugin?name=uni-easyinput) , select `Import sample project using HBuilderX` on the right side of the page to experience the complete component example.
:::

::: preview https://hellouniapp.dcloud.net.cn/pages/extUI/easyinput/easyinput
> Template
``` html
<template>
	<view>
		<uni-card :is-shadow="false" is-full>
			<text class="uni-h6">easyinput 组件是对原生input组件的增强 ，是专门为配合表单组件 uni-forms 而设计的，easyinput 内置了边框，图标等，同时包含 input所有功能</text>
		</uni-card>
		<uni-section title="默认" subTitle="使用 focus 属性自动获取输入框焦点" type="line" padding>
			<uni-easyinput errorMessage v-model="value" focus placeholder="请输入内容" @input="input"></uni-easyinput>
		</uni-section>

		<uni-section title="去除空格" subTitle="使用 trim 属性 ,可以控制返回内容的空格 " type="line" padding>
			<text class="uni-subtitle">输入内容：{{ '"'+value+'"' }}</text>
			<uni-easyinput class="uni-mt-5" trim="all" v-model="value" placeholder="请输入内容" @input="input"></uni-easyinput>
		</uni-section>

		<uni-section title="自定义样式" subTitle="使用 styles 属性 ,可以自定义输入框样式" type="line" padding>
			<uni-easyinput v-model="value" :styles="styles" :placeholderStyle="placeholderStyle" placeholder="请输入内容"@input="input"></uni-easyinput>
		</uni-section>
		<uni-section title="图标" subTitle="使用 prefixIcon / suffixIcon 属性 ,可以自定义输入框左右侧图标" type="line" padding>
			<uni-easyinput prefixIcon="search" v-model="value" placeholder="左侧图标" @iconClick="iconClick">
			</uni-easyinput>
			<uni-easyinput class="uni-mt-5" suffixIcon="search" v-model="value" placeholder="右侧图标" @iconClick="iconClick"></uni-easyinput>
		</uni-section>
		<uni-section title="禁用" subTitle="使用 disabled 属性禁用输入框" type="line" padding>
			<uni-easyinput disabled value="已禁用" placeholder="请输入内容"></uni-easyinput>
		</uni-section>

		<uni-section title="密码框" subTitle="指定属性 type=password 使用密码框,右侧会显示眼睛图标" type="line" padding>
			<uni-easyinput type="password" v-model="password" placeholder="请输入密码"></uni-easyinput>
		</uni-section>

		<uni-section title="多行文本" subTitle="指定属性 type=textarea 使用多行文本框" type="line" padding>
			<uni-easyinput type="textarea" v-model="value" placeholder="请输入内容"></uni-easyinput>
		</uni-section>

		<uni-section title="多行文本自动高度" subTitle="使用属性 autoHeight 使多行文本框自动增高" type="line" padding>
			<uni-easyinput type="textarea" autoHeight v-model="value" placeholder="请输入内容"></uni-easyinput>
		</uni-section>
	</view>
</template>
``` 
> Script
``` html
<script>
	export default {
		data() {
			return {
				value: '',
				password: '',
				placeholderStyle: "color:#2979FF;font-size:14px",
				styles: {
					color: '#2979FF',
					borderColor: '#2979FF'
				}
			}

		},
		onLoad() {},
		onReady() {},
		methods: {
			input(e) {
				console.log('输入内容：', e);
			},
			iconClick(type) {
				uni.showToast({
					title: `点击了${type==='prefix'?'左侧':'右侧'}的图标`,
					icon: 'none'
				})
			}
		}
	}
</script>
``` 
> Ｓtyle
``` html
<style lang="scss">
.uni-mt-5 {
	margin-top: 5px;
}
</style>

```
:::

[完整示例演示](https://hellouniapp.dcloud.net.cn/pages/extUI/easyinput/easyinput)
[Complete example demo](https://hellouniapp.dcloud.net.cn/pages/extUI/easyinput/easyinput)