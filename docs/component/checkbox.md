#### checkbox-group
多项选择器，内部由多个 checkbox 组成。
Multi-item selector, consisting of multiple checkbox inside.

**属性说明**
**Attribute description**

|属性名|类型|默认值|说明|
| Attribute name| Type| Defaults| Instruction|
|:-|:-|:-|:-|
|@change|EventHandle||``<checkbox-group>``中选中项发生改变是触发 change 事件，detail = {value:[选中的checkbox的value的数组]}|
| @change| EventHandle| | Change of selected options in `<checkbox-group>` will trigger the change event, detail = {value:[array of values of the selected checkboxes]}|

#### checkbox
多选项目。
Multiple selection items.

**属性说明**
**Attribute description**

|属性名|类型|默认值|说明|
| Attribute name| Type| Defaults| Instruction|
|:-|:-|:-|:-|
|value|String||``<checkbox>`` 标识，选中时触发 ``<checkbox-group>`` 的 change 事件，并携带 ``<checkbox>`` 的 value。|
| value| String| | The `<checkbox>` tag triggers the change event of `<checkbox-group>` when selected, and carries the value of `<checkbox>`.|
|disabled|Boolean|false|是否禁用|
| disabled| Boolean| false| Disable or not|
|checked|Boolean|false|当前是否选中，可用来设置默认选中|
| checked| Boolean| false| Checked or not with checked as default.|
|color|Color||checkbox的颜色，同css的color|
| color| Color| | The color of the checkbox is the same as that of css.|

**示例** [查看演示](https://hellouniapp.dcloud.net.cn/pages/component/checkbox/checkbox)
**Example** [View demo](https://hellouniapp.dcloud.net.cn/pages/component/checkbox/checkbox)
 
以下示例代码，来自于[hello uni-app项目](https://github.com/dcloudio/hello-uniapp)，推荐使用HBuilderX，新建uni-app项目，选择hello uni-app模板，可直接体验完整示例。
The following sample code comes from the [hello uni-app project](https://github.com/dcloudio/hello-uniapp). It is recommended to use HBuilderX to create a new uni-app project and choose the hello uni-app template to directly experience the complete example.

::: preview https://hellouniapp.dcloud.net.cn/pages/component/checkbox/checkbox

> Template
```vue
<!-- 本示例未包含完整css，获取外链css请参考上文，在hello uni-app项目中查看 -->
<!-- This example does not include the complete css, please refer to the above to obtain the external css. View it in the hello uni-app project -->
<template>
	<view>
		<view class="uni-padding-wrap uni-common-mt">
			<view class="uni-title uni-common-mt">默认样式</view>
			<view>
				<checkbox-group>
					<label>
						<checkbox value="cb" checked="true" />选中
					</label>
					<label>
						<checkbox value="cb" />未选中
					</label>
				</checkbox-group>
			</view>
			<view class="uni-title uni-common-mt">不同颜色和尺寸的checkbox</view>
			<view>
				<checkbox-group>
					<label>
						<checkbox value="cb" checked="true" color="#FFCC33" style="transform:scale(0.7)" />选中
					</label>
					<label>
						<checkbox value="cb" color="#FFCC33" style="transform:scale(0.7)" />未选中
					</label>
				</checkbox-group>
			</view>
		</view>
		
		<view class="uni-padding-wrap">
			<view class="uni-title uni-common-mt">
				推荐展示样式
				<text>\n使用 uni-list 布局</text>
			</view>
		</view>
		<view class="uni-list">
			<checkbox-group @change="checkboxChange">
				<label class="uni-list-cell uni-list-cell-pd" v-for="item in items" :key="item.value">
					<view>
						<checkbox :value="item.value" :checked="item.checked" />
					</view>
					<view>{{item.name}}</view>
				</label>
			</checkbox-group>
		</view>
	</view>
</template>
```
> Script
```vue
<script>
	export default {
		data() {
			return {
				title: 'checkbox 复选框',
				items: [{
						value: 'USA',
						name: '美国'
					},
					{
						value: 'CHN',
						name: '中国',
						checked: 'true'
					},
					{
						value: 'BRA',
						name: '巴西'
					},
					{
						value: 'JPN',
						name: '日本'
					},
					{
						value: 'ENG',
						name: '英国'
					},
					{
						value: 'FRA',
						name: '法国'
					}
				]
			}
		},
		methods: {
			checkboxChange: function (e) {
				var items = this.items,
					values = e.detail.value;
				for (var i = 0, lenI = items.length; i < lenI; ++i) {
					const item = items[i]
					if(values.includes(item.value)){
						this.$set(item,'checked',true)
					}else{
						this.$set(item,'checked',false)
					}
				}
			}
		}
	}
</script>
``` 
> Style
``` vue
<style>
.uni-list-cell {
	justify-content: flex-start
}
</style>
```
:::
 

**注意**
**Notice**
- checkbox的默认颜色，在不同平台不一样。微信小程序、360小程序是绿色的，字节跳动小程序为红色，其他平台是蓝色的。更改颜色使用color属性。
- The default color of checkbox is different on different platforms. WeChat applet and 360 applet are green, ByteDance applet is red, and other platforms are blue. Change the color using the color property.
- 如需调节checkbox大小，可通过css的scale方法调节，如缩小到70%`style="transform:scale(0.7)"`
- If you need to adjust the checkbox size, you can adjust it by the scale method of css, such as scaling down it to 70% `style="transform:scale(0.7)"`

**扩展**
**Extension**
- uni-ui提供了增强的uni-data-checkbox组件，基于[datacom规范](/component/datacom)，只需传入data数据，即可自动生成一组复选框，使用方式更简洁，并且支持[uni-forms](https://ext.dcloud.net.cn/plugin?id=2773)的表单验证。uni-data-checkbox组件详见[https://ext.dcloud.net.cn/plugin?id=3456](https://ext.dcloud.net.cn/plugin?id=3456)
- uni-ui provides an enhanced uni-data-checkbox component. Based on the [datacom specification](/component/datacom), a set of checkboxes can be automatically generated by just inputting data, which is more concise and supports[uni-forms](https://ext.dcloud.net.cn/plugin?id=2773) form validation. For details of uni-data-checkbox components, please refer to [https://ext.dcloud.net.cn/plugin?id=3456](https://ext.dcloud.net.cn/plugin?id=3456)
