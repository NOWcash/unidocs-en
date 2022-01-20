#### picker

从底部弹起的滚动选择器。支持五种选择器，通过mode来区分，分别是普通选择器，多列选择器，时间选择器，日期选择器，省市区选择器，默认是普通选择器。
Scroll selector that pops up from the bottom. Five selectors are supported, which are distinguished by mode, namely, ordinary selector, multi-column selector, time selector, date selector, and province-city-district selector, with ordinary selector as default.

#### 普通选择器
#### Normal selector

``mode = selector``

**属性说明**
**Attribute description**

|属性名|类型|默认值|说明|平台差异说明|
| Attribute name| Type| Defaults| Instruction| Platform difference description|
|:-|:-|:-|:-|:-|
|range|Array / Array&lt;Object&gt;|[]|mode为 selector 或 multiSelector 时，range 有效||
| range| Array / Array\<Object>| \[]| range is valid for selector or multiSelector mode| |
|range-key|String||当 range 是一个 `Array＜Object＞` 时，通过 range-key 来指定 Object 中 key 的值作为选择器显示内容||
| range-key| String| | When range is a `Array＜Object＞`, range-key is used to specify the value of key in the Object as the selector display content.| |
|value|Number|0|value 的值表示选择了 range 中的第几个（下标从 0 开始）||
| value| Number| 0| The value indicates which term in range is selected (subscript starts from 0)| |
|selector-type|String|auto|大屏时UI类型，支持 picker、select、auto，默认在 iPad 以 picker 样式展示而在 PC 以 select 样式展示|H5 2.9.9+|
| selector-type| String| auto| UI type for large screen, which supports picker, select and auto. It is displayed in picker style on iPad and select style on PC by default| H5 2.9.9+|
|@change|EventHandle||value 改变时触发 change 事件，event.detail = {value: value}||
| @change| EventHandle| | change event will be triggered when value changes, event.detail = {value: value}| |
|disabled|Boolean|false|是否禁用||
| disabled| Boolean| false| Disable or not| |
|@cancel|EventHandle||取消选择或点遮罩层收起 picker 时触发||
| @cancel| EventHandle| | Triggered when cancelling the select or click the mask layer to collapse picker| |

- picker在各平台的实现是有UI差异的，有的平台没有取消按钮如App-iOS端。但均不影响功能使用。
- There are UI differences in the realization of picker on different platforms, and some platforms have no cancel button, such as App-iOS side. But it does not affect the use of the function.

#### 多列选择器
#### Multiple column selector

``mode = multiSelector``

**平台差异说明**
**Platform difference description**

|App|H5|
|:-:|:-:|
|vue支持，nvue自2.4起支持|√|
| Supported by vue, and nvue since version 2.4| √|


**属性说明**
**Attribute description**

|属性名|类型|默认值|说明|
| Attribute name| Type| Defaults| Instruction|
|:-|:-|:-|:-|
|range|二维 Array / 二维 Array＜Object＞|[]|mode为 selector 或 multiSelector 时，range 有效。二维数组，长度表示多少列，数组的每项表示每列的数据，如[["a","b"], ["c","d"]]|
| range| Two-dimensional Array/two-dimensional Array＜Object＞| \[]| range is valid for selector or multiSelector mode. Two-dimensional array, the length indicates the number of columns, and each item of the array indicates the data of each column, for example [["a","b"], \["c","d"]]|
|range-key|String||当 range 是一个二维 Array＜Object＞ 时，通过 range-key 来指定 Object 中 key 的值作为选择器显示内容|
| range-key| String| | For the range as a two-dimensional Array＜Object＞, use range-key to specify the value of key in Object as the display content of the selector|
|value|Array|[]|value 每一项的值表示选择了 range 对应项中的第几个（下标从 0 开始）|
| value| Array| \[]| Each of the value indicates which term in range is selected (subscript starts from 0)|
|@change|EventHandle||value 改变时触发 change 事件，event.detail = {value: value}|
| @change| EventHandle| | change event will be triggered when value changes, event.detail = {value: value}|
|@columnchange|EventHandle||某一列的值改变时触发 columnchange 事件，event.detail = {column: column, value: value}，column 的值表示改变了第几列（下标从0开始），value 的值表示变更值的下标|
| @columnchange| EventHandle| | columnchange event is triggered when the value from a column changes, event.detail = {column: column, value: value}, wherein the column indicates which column is changed (the subscript starts from 0), and the value indicates the subscript of the changed value|
|@cancel|EventHandle||取消选择时触发|
| @cancel| EventHandle| | Triggered when deselected|
|disabled|Boolean|false|是否禁用|
| disabled| Boolean| false| Disable or not|

**bug & tips**
- 由于 JavaScript 的限制 vue 不能观测如下方式设置 value：``this.value[0] = 0`` （[vue 注意事项](https://cn.vuejs.org/v2/guide/list.html#注意事项)），解决方式参考：[hello-uniapp 示例](https://github.com/dcloudio/hello-uniapp/commit/59264474172a591c865431d02a2a1e3583978827)
- Due to the limitation of JavaScript, vue cannot observe the setting value in the following way: `this.value[0] = 0` ([Precautions of vu](https://cn.vuejs.org/v2/guide/list.html#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9)), for the solution, please refer to: [hello-uniapp example](https://github.com/dcloudio/hello-uniapp/commit/59264474172a591c865431d02a2a1e3583978827)


#### 时间选择器
#### Time picker

``mode = time``

**平台差异说明**
**Platform difference description**

|App|H5|
|:-:|:-:|
|√|√|

- 时间选择在App端调用的是os的原生时间选择控件，在不同平台有不同的ui表现
- Time selection calls the native time selection control of os on the App side, which has different ui performance on different platforms

**属性说明**
**Attribute description**

|属性名|类型|默认值|说明|平台差异说明|
| Attribute name| Type| Defaults| Instruction| Platform difference description|
|:-|:-|:-|:-|:-|
|value|String||表示选中的时间，格式为"hh:mm"||
| value| String| | Indicate the selected time with the format of "hh:mm"| |
|start|String||表示有效时间范围的开始，字符串格式为"hh:mm"|App 不支持|
| start| String| | Indicate the beginning of the valid time range with the string format of "hh:mm"| Not supported on App|
|end|String||表示有效时间范围的结束，字符串格式为"hh:mm"|App 不支持|
| end| String| | Indicate the ending of the valid time range with the string format of "hh:mm"| Not supported on App|
|@change|EventHandle||value 改变时触发 change 事件，event.detail = {value: value}||
| @change| EventHandle| | change event will be triggered when value changes, event.detail = {value: value}| |
|@cancel|EventHandle||取消选择时触发||
| @cancel| EventHandle| | Triggered when deselected| |
|disabled|Boolean|false|是否禁用|&nbsp;|
| disabled| Boolean| false| Disable or not|  |

#### 日期选择器
#### Date picker

``mode = date``

**平台差异说明**
**Platform difference description**

|App|H5|
|:-:|:-:|
|√|√|

日期选择默认在App端和H5端（PC版Chrome以及PC版FireFox）调用的是os的原生日期选择控件，在不同平台有不同的ui表现，当配置fields参数后使用统一的展示方式。
Date selection calls the native date selection control of os on the App side and H5 side (Chrome for PC and FireFox for PC) by default, there are different ui performance on different platforms, and a unified display mode is used after configuring the fields parameter.

**属性说明**
**Attribute description**

|属性名|类型|默认值|说明|平台差异说明|
| Attribute name| Type| Defaults| Instruction| Platform difference description|
|:-|:-|:-|:-|:-|
|value|String|0|表示选中的日期，格式为"YYYY-MM-DD"||
| value| String| 0| Indicate the selected date with the format of "YYYY-MM-DD"| |
|start|String||表示有效日期范围的开始，字符串格式为"YYYY-MM-DD"||
| start| String| | Indicate the beginning of the valid date range with the string format of "YYYY-MM-DD"| |
|end|String||表示有效日期范围的结束，字符串格式为"YYYY-MM-DD"||
| end| String| | Indicate the ending of the valid date range with the string format of "YYYY-MM-DD"| |
|fields|String|day|有效值 year、month、day，表示选择器的粒度，默认为 day，App 端未配置此项时使用系统 UI|H5、App 2.6.3+|
| fields| String| day| Valid value for year, month and day, indicating the granularity of the selector, with day as default, if this item is not configured on the App side, the system UI will be used| H5, App 2.6.3+|
|@change|EventHandle||value 改变时触发 change 事件，event.detail = {value: value}||
| @change| EventHandle| | change event will be triggered when value changes, event.detail = {value: value}| |
|@cancel|EventHandle||取消选择时触发||
| @cancel| EventHandle| | Triggered when deselected| |
|disabled|Boolean|false|是否禁用|&nbsp;|
| disabled| Boolean| false| Disable or not|  |

**fields 有效值**
**valid values for fields**

|值|说明|
| Value| Instruction|
|:-|:-|
|year|选择器粒度为年|
| year| Selector granularity is year|
|month|选择器粒度为月份|
| month| Selector granularity is month|
|day|选择器粒度为天|
| day| Selector granularity is days|


**示例** [查看演示](https://hellouniapp.dcloud.net.cn/pages/component/picker/picker)
**Example** [View demo](https://hellouniapp.dcloud.net.cn/pages/component/picker/picker)
 
以下示例代码，来自于[hello uni-app项目](https://github.com/dcloudio/hello-uniapp)，推荐使用HBuilderX，新建uni-app项目，选择hello uni-app模板，可直接体验完整示例。
The following sample code comes from the [hello uni-app project](https://github.com/dcloudio/hello-uniapp). It is recommended to use HBuilderX to create a new uni-app project and choose the hello uni-app template to directly experience the complete example.
```html
<!-- 本示例未包含完整css，获取外链css请参考上文，在hello uni-app项目中查看 -->
<!-- This example does not include the complete css, please refer to the above to obtain the external css. View it in the hello uni-app project -->
<template>
	<view>
		<view class="uni-title uni-common-pl">Region selector</view>
		<view class="uni-list">
			<view class="uni-list-cell">
				<view class="uni-list-cell-left">
					Current selection
				</view>
				<view class="uni-list-cell-db">
					<picker @change="bindPickerChange" :value="index" :range="array">
						<view class="uni-input">{{array[index]}}</view>
					</picker>
				</view>
			</view>
		</view>

		<view class="uni-title uni-common-pl">Time selector</view>
		<view class="uni-list">
			<view class="uni-list-cell">
				<view class="uni-list-cell-left">
					Current selection
				</view>
				<view class="uni-list-cell-db">
					<picker mode="time" :value="time" start="09:01" end="21:01" @change="bindTimeChange">
						<view class="uni-input">{{time}}</view>
					</picker>
				</view>
			</view>
		</view>

		<view class="uni-title uni-common-pl">Date selector</view>
		<view class="uni-list">
			<view class="uni-list-cell">
				<view class="uni-list-cell-left">
					Current selection
				</view>
				<view class="uni-list-cell-db">
					<picker mode="date" :value="date" :start="startDate" :end="endDate" @change="bindDateChange">
						<view class="uni-input">{{date}}</view>
					</picker>
				</view>
			</view>
		</view>
	</view>
</template>
```
```javascript
export default {
    data() {
        const currentDate = this.getDate({
            format: true
        })
        return {
            title: 'picker',
            array: ['China',' America',' Brazil',' Japan'],
            index: 0,
            date: currentDate,
            time: '12:01'
        }
    },
    computed: {
        startDate() {
            return this.getDate('start');
        },
        endDate() {
            return this.getDate('end');
        }
    },
    methods: {
        bindPickerChange: function(e) {
            console.log ('picker sends the selection change, carrying with', e.target.value)
            this.index = e.target.value
        },
        bindDateChange: function(e) {
            this.date = e.target.value
        },
        bindTimeChange: function(e) {
            this.time = e.target.value
        },
        getDate(type) {
            const date = new Date();
            let year = date.getFullYear();
            let month = date.getMonth() + 1;
            let day = date.getDate();

            if (type === 'start') {
                year = year - 60;
            } else if (type === 'end') {
                year = year + 2;
            }
            month = month > 9 ? month : '0' + month;
            day = day > 9 ? day : '0' + day;
            return `${year}-${month}-${day}`;
        }
    }
}
```

![uniapp](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/42826b40-4f30-11eb-b680-7980c8a877b8.png)

示例代码说明：以上示例代码从hello uni-app示例中复制，涉及的css样式在hello uni-app的app.vue和uni.css中
Code description: The above code is copied from the example of hello uni-app, and the css styles involved can be found in app.vue and uni.css of hello uni-app

预览H5效果：使用浏览器的手机模式访问[https://hellouniapp.dcloud.net.cn/pages/component/picker/picker](https://hellouniapp.dcloud.net.cn/pages/component/picker/picker)
Preview the effect of H5: Visit [https://hellouniapp.dcloud.net.cn/pages/component/picker/picker](https://hellouniapp.dcloud.net.cn/pages/component/picker/picker) by using the mobile phone mode of the browser

**注意**
**Notice**
- 在picker内容还在滚动时或滚动回弹动画还未结束时，点确定关闭弹出的picker，数据无法及时更新。需等待一下，或手动触停滚动再点确定。所有平台均如此
- Click OK to close the pop-up picker if the picker content is still scrolling or the scrolling bounce animation is still on, and then the data will not be updated in time. For such case, you should wait for a minute, or manually touch and stop scrolling and then click OK. This is true for all platforms

**扩展**
**Extension**
- uni ui提供了增强版`<uni-data-picker>`组件，详见：[https://ext.dcloud.net.cn/plugin?id=3796](https://ext.dcloud.net.cn/plugin?id=3796)
- uni ui provides an enhanced version of the `<uni-data-picker>` component, see: [https://ext.dcloud.net.cn/plugin?id=3796](https://ext.dcloud.net.cn/plugin?id=3796)
- 该组件优势如下：
- The advantages of this component are as follows:
  * 符合[datacom](/component/datacom)规范，只需传入data，就可以自动生成界面
  * Comply with the [datacom](/component/datacom) specification, just input data, and the interface can be automatically generated
  * 符合[uni-forms](https://ext.dcloud.net.cn/plugin?id=2773)，表单校验规范
  * Comply with [uni-forms](https://ext.dcloud.net.cn/plugin?id=2773), form verification specifications
  * 突破多列picker的3列限制，可以承载更多列数据
  * Breaking through the three-column limit of multi-column picker will carry more columns of data
  * 选择区域面积更高更大
  * The selection area is higher and larger
  * 支持多列数据分级加载，比如省市区选择，先选择省，然后动态联网加载该省的市。
  * Support hierarchical loading of multi-column data. Taking province-city-district selector as an example, after the province is selected, the cities of this province will be dynamically loaded in-line.
  * uniCloud自带了[opendb](https://gitee.com/dcloud/opendb)表，[opendb-city-china](https://gitee.com/dcloud/opendb/tree/master/collection/opendb-city-china)，包括全国的省市区数据。在`<uni-data-picker>`组件上可直接绑定该数据，生成全端可用的、联网懒加载的省市区选择。
  * uniCloud comes with its own [opendb](https://gitee.com/dcloud/opendb) table,[opendb-city-china](https://gitee.com/dcloud/opendb/tree/master/collection/opendb-city-china), including provincial and urban data of the whole country. The data can be directly bound to the `<uni-data-picker>` component to generate a fully-available, lazy-loaded networked province and city selection.
  * unicloud数据库提供了[DB Schema](https://uniapp.dcloud.io/uniCloud/schema)，还提供了[schema2code](https://uniapp.dcloud.net.cn/uniCloud/schema?id=autocode)自动生成全套表单页面，包括界面、校验逻辑、提交入库。在schema中配置字段的格式，比如在用户地址表[uni-id-address](https://gitee.com/dcloud/opendb/tree/master/collection/uni-id-address)的字段`area_code`配置值域指向[opendb-city-china](https://gitee.com/dcloud/opendb/tree/master/collection/opendb-city-china)表，即可自动生成该用户地址的生成页面
  * unicloud database provides [DB Schema](https://uniapp.dcloud.io/uniCloud/schema) and [schema2code](https://uniapp.dcloud.net.cn/uniCloud/schema?id=autocode) to automatically generate a full set of form pages, including interface, verification logic, submission and warehousing. Configure the format of fields in schema. For example, by configuring the value field `area_code` in the user address table [uni-id-address](https://gitee.com/dcloud/opendb/tree/master/collection/uni-id-address) to point to the [ opendb-city-China](https://gitee.com/dcloud/opendb/tree/master/collection/opendb-city-china) table, a page for generating the user address can be automatically generated.
