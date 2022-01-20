#### rich-text

富文本。
Rich text.

支持默认事件，包括：click、touchstart、touchmove、touchcancel、touchend、longpress。
Default events are supported, including click, touchstart, touchmove, touchcancel, touchend and longpress.

**属性说明**
**Attribute description**

|属性名|类型|默认值|说明|平台兼容|
| Attribute name| Type| Defaults| Instruction| Platform compatibility|
|:-|:-|:-|:-|:-|
|nodes|Array / String|[]|节点列表 / HTML String||
| nodes| Array / String| \[]| Node list/HTML String| |
|space|string||显示连续空格||
| space| string| | Display continuous whitespace| |

##### nodes

nodes 值为 HTML String 时，在组件内部将自动解析为节点列表，推荐直接使用 Array 类型避免内部转换导致的性能下降。App-nvue 不支持 HTML String 方式，仅支持直接使用节点列表即 Array 类型，如要使用 HTML String，则需自己将 HTML String 转化为 nodes 数组，可使用 [html-parser](https://github.com/dcloudio/hello-uniapp/blob/master/common/html-parser.js) 转换。
For the node value of HTML String, it will be automatically resolved into a node list inside the component. It is recommended to use Array type directly to avoid perlistance degradation caused by internal conversion. App-nvue does not support the HTML String method, but only supports the direct use of the node list, i.e., Array type. If you want to use HTML String, you need to convert the HTML String into an array of nodes with the help of [html-parser](https://github.com/dcloudio/hello-uniapp/blob/master/common/html-parser.js).

节点列表内的节点现支持两种类型，通过 type 来区分，分别是元素节点和文本节点，默认是元素节点，在富文本区域里显示的 HTML 节点。
The nodes in the list now support two types, and distinguished by types: element nodes and text nodes. Element nodes are the default nodes, and HTML nodes are displayed in the rich text area.

**元素节点：type = node**
**Element nodes: type = node**

|属性|说明|类型|必填|备注|
| Attribute| Instruction| Type| Required| Remark|
|:-|:-|:-|:-|:-|
|name|标签名|String|是|支持部分受信任的 HTML 节点|
| name| Label name| String| Yes| Part of the trusted HTML nodes are supported|
|attrs|属性|Object|否|支持部分受信任的属性，遵循 Pascal 命名法|
| attrs| Attribute| Object| No| Part of the trusted attributes are supported, in consistent with the Pascal nomenclature|
|children|子节点列表|Array|否|结构和 nodes 一致|
| children| Child node list| Array| No| The structure is consistent with nodes|

**文本节点：type = text**
**Text nodes: type = text**

|属性|说明|类型|必填|备注|
| Attribute| Instruction| Type| Required| Remark|
|:-|:-|:-|:-|:-|
|text|文本|String|是|支持 entities|
| text| Text| String| Yes| Supported entities|
 
##### 受信任的HTML节点及属性
##### Trusted HTML nodes and attributes

全局支持 class 和 style 属性，**不支持 id 属性**。
The class and style attributes are supported globally, but **id attributes are not supported**.

|节点|属性|
| Node| Attribute|
|:-|:-|
|a||
|abbr||
|b||
|blockquote||
|br||
|code||
|col|span，width|
|colgroup|span，width|
|dd||
|del||
|div||
|dl||
|dt||
|em||
|fieldset||
|h1||
|h2||
|h3||
|h4||
|h5||
|h6||
|hr||
|i||
|img|alt，src，height，width|
|ins||
|label||
|legend||
|li||
|ol|start，type|
|p||
|q||
|span||
|strong||
|sub||
|sup||
|table|width|
|tbody||
|td|colspan，height，rowspan，width|
|tfoot||
|th|colspan，height，rowspan，width|
|thead||
|tr||
|ul|&nbsp;|

**示例** [查看演示](https://hellouniapp.dcloud.net.cn/pages/component/rich-text/rich-text)
**Example** [View demo](https://hellouniapp.dcloud.net.cn/pages/component/rich-text/rich-text)

以下示例代码，来自于[hello uni-app项目](https://github.com/dcloudio/hello-uniapp)，推荐使用HBuilderX，新建uni-app项目，选择hello uni-app模板，可直接体验完整示例。
The following sample code comes from the [hello uni-app project](https://github.com/dcloudio/hello-uniapp). It is recommended to use HBuilderX to create a new uni-app project and choose the hello uni-app template to directly experience the complete example.
```html
<!-- 本示例未包含完整css，获取外链css请参考上文，在hello uni-app项目中查看 -->
<!-- This example does not include the complete css, please refer to the above to obtain the external css. View it in the hello uni-app project -->
<template>
	<view class="content">
		<page-head :title="title"></page-head>
		<view class="uni-padding-wrap">
			<view class="uni-title uni-common-mt">
				Array type
				<text>\nnodes attribute is Array</text>
			</view>
			<view class="uni-common-mt" style="background:#FFF; padding:20rpx;">
				<rich-text :nodes="nodes"></rich-text>
			</view>
			<view class="uni-title uni-common-mt">
				String type
				<text>\nnodes attribute is String</text>
			</view>
			<view class="uni-common-mt" style="background:#FFF; padding:20rpx;">
				<rich-text :nodes="strings"></rich-text>
			</view>
		</view>
	</view>
</template>
```
```javascript
export default {
    data() {
        return {
            nodes: [{
                name: 'div',
                attrs: {
                    class: 'div-class',
                    style: 'line-height: 60px; color: red; text-align:center;'
                },
                children: [{
                    type: 'text',
                    text: 'Hello&nbsp;uni-app!'
                }]
            }],
            strings: '<div style="text-align:center;"><img src="https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/d8590190-4f28-11eb-b680-7980c8a877b8.png"/></div>'
        }
    }
}
```

![uniapp](https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/ef5ba530-4f2f-11eb-bdc1-8bd33eb6adaa.png)

**Tips**

- nodes 不推荐使用 String 类型，性能会有所下降。
- String type is not recommended for nodes, or the performance will be degraded.
- rich-text 组件内屏蔽所有节点的事件。所以如果内容中有链接、图片需要点击，则不能使用rich-text，此时可在[uni-app插件市场](https://ext.dcloud.net.cn/search?q=parse)搜索parse插件使用。app-nvue的rich-text组件支持链接图片点击。
- Events of all nodes are blocked in the rich-text component. Therefore, if there are links or images in the content that need to be clicked, rich-text cannot be used. At this time, you can search for the parse plug-in in the [uni-app plug-in market](https://ext.dcloud.net.cn/search?q=parse). The rich-text component of app-nvue supports to click on linked pictures.
- attrs 属性不支持 id ，支持 class 。
- attrs attribute supports class instead of id.
- name 属性大小写不敏感。
- name attribute is case insensitive.
- 如果使用了不受信任的HTML节点，该节点及其所有子节点将会被移除。
- If an untrusted HTML node is used, the node and all its child nodes will be removed.
- 非 App 平台 img 标签仅支持网络图片。
- On non-App platforms, the img tag only supports web pictures.
- 如果在自定义组件中使用 rich-text 组件，那么仅自定义组件的 css 样式对 rich-text 中的 class 生效。
- If rich-text components are used in custom components, only css style of the custom components will take effect on class in rich-text.
