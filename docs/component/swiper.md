### swiper

滑块视图容器。
Slider view container.

一般用于左右滑动或上下滑动，比如banner轮播图。
Generally used to slide left and right or up and down, such as banner carousel.

注意滑动切换和滚动的区别，滑动切换是一屏一屏的切换。swiper下的每个swiper-item是一个滑动切换区域，不能停留在2个滑动区域之间。
Note the difference between sliding switching and scrolling. Sliding switching is switching one screen after the other. Each swiper-item under swiper is a sliding switching area, and cannot stay between two sliding areas.

**属性说明**
**Attribute description**

|属性名|类型|默认值|说明|平台差异说明|
| Attribute name| Type| Defaults| Instruction| Platform difference description|
|:-|:-|:-|:-|:-|
|indicator-dots|Boolean|false|是否显示面板指示点||
| indicator-dots| Boolean| false| Whether to display panel indicator points?| |
|indicator-color|Color|rgba(0, 0, 0, .3)|指示点颜色||
| indicator-color| Color| rgba(0, 0, 0, .3)| Indicator color| |
|indicator-active-color|Color|#000000|当前选中的指示点颜色||
| indicator-active-color| Color| #000000| Color of the currently selected indicator| |
|active-class|String||swiper-item 可见时的 class|支付宝小程序|
|active-class|String||class when swiper-item is visible|Alipay applet|
|changing-class|String||acceleration 设置为 {{true}} 时且处于滑动过程中，中间若干屏处于可见时的class|支付宝小程序|
|changing-class|String||acceleration is set to {{true}} and is in the sliding process, the class when several screens in the middle are visible|Alipay applet|
Class|Alipay applet|
|autoplay|Boolean|false|是否自动切换||
| autoplay| Boolean| false| Whether to switch automatically?| |
|current|Number|0|当前所在滑块的 index||
| current| Number| 0| index of the current slider| |
|current-item-id|String||当前所在滑块的 item-id ，不能与 current 被同时指定|支付宝小程序不支持|
|current-item-id|String||The item-id of the current slider, cannot be specified together with current |Alipay applet does not support|
|interval|Number|5000|自动切换时间间隔||
| interval| Number| 5000| Time interval for automatic switching| |
|duration|Number|500|滑动动画时长|app-nvue不支持|
| duration| Number| 500| Slide animation duration| Not supported by app-nvue|
|circular|Boolean|false|是否采用衔接滑动，即播放到末尾后重新回到开头||
| circular| Boolean| false| Whether to use circular sliding, i.e. return to the beginning after playing| |
|vertical|Boolean|false|滑动方向是否为纵向||
| vertical| Boolean| false| Whether the sliding direction is longitudinal?| |
|previous-margin|String|0px|前边距，可用于露出前一项的一小部分，接受 px 和 rpx 值|app-nvue、字节跳动小程序、飞书小程序不支持|
|previous-margin|String|0px|The front margin, which can be used to reveal a small part of the previous item, accepts px and rpx values|app-nvue, ByteDance applet, Feishu applet do not support|
|next-margin|String|0px|后边距，可用于露出后一项的一小部分，接受 px 和 rpx 值|app-nvue、字节跳动小程序、飞书小程序不支持|
|next-margin|String|0px|The back margin, which can be used to expose a small part of the next item, accepts px and rpx values|app-nvue, ByteDance applet, Feishu applet do not support|
|acceleration|Boolean|false|当开启时，会根据滑动速度，连续滑动多屏|支付宝小程序|
|acceleration|Boolean|false|When enabled, it will continuously slide multiple screens according to the sliding speed|Alipay applet|
|disable-programmatic-animation|Boolean|false|是否禁用代码变动触发 swiper 切换时使用动画。|支付宝小程序|
|disable-programmatic-animation|Boolean|false|Whether to disable the use of animation when code changes trigger swiper switching. |Alipay Mini Program|
|display-multiple-items|Number|1|同时显示的滑块数量|app-nvue、支付宝小程序不支持|
|display-multiple-items|Number|1|Number of sliders displayed at the same time|app-nvue, Alipay applet not supported|
|skip-hidden-item-layout|Boolean|false|是否跳过未显示的滑块布局，设为 true 可优化复杂情况下的滑动性能，但会丢失隐藏状态滑块的布局信息|App、微信小程序、京东小程序|
|skip-hidden-item-layout|Boolean|false|Whether to skip the slider layout that is not displayed, set to true to optimize the sliding performance in complex situations, but the layout information of the hidden state slider will be lost|App, WeChat small Program, JD Mini Program |
|disable-touch|Boolean|false|是否禁止用户 touch 操作|App 2.5.5+、H5 2.5.5+、支付宝小程序、字节跳动小程序与飞书小程序（只在初始化时有效，不能动态变更）|
|disable-touch|Boolean|false|Whether user touch operation is prohibited|App 2.5.5+, H5 2.5.5+, Alipay applet, ByteDance applet and Feishu applet (only valid during initialization, not dynamic change)|
|touchable|Boolean|true|是否监听用户的触摸事件，只在初始化时有效，不能动态变更|字节跳动小程序与飞书小程序（uni-app 2.5.5+ 推荐统一使用 disable-touch）|
|touchable|Boolean|true|Whether to monitor the user's touch events, it is only valid during initialization, and cannot be changed dynamically|ByteDance applet and Feishu applet (uni-app 2.5.5+ recommends the unified use of disable-touch)|
|easing-function|String|default|指定 swiper 切换缓动动画类型，有效值：default、linear、easeInCubic、easeOutCubic、easeInOutCubic|微信小程序、快手小程序、京东小程序|
|easing-function|String|default|Specify swiper to switch the easing animation type, valid values: default, linear, easeInCubic, easeOutCubic, easeInOutCubic|WeChat applet, Kuaishou applet, Jingdong applet|
|@change|EventHandle||current 改变时会触发 change 事件，event.detail = {current: current, source: source}||
| @change| EventHandle| | change event will be triggered when current changes, event.detail = {current: current, source: source}| |
|@transition|EventHandle||swiper-item 的位置发生改变时会触发 transition 事件，event.detail = {dx: dx, dy: dy}，支付宝小程序暂不支持dx, dy|App、H5、微信小程序、支付宝小程序、字节跳动小程序、飞书小程序、QQ小程序、快手小程序|
|@transition|EventHandle||The transition event will be triggered when the position of the swiper-item changes, event.detail = {dx: dx, dy: dy}, Alipay applet does not support dx, dy|App, H5, WeChat applet Program, Alipay applet, ByteDance applet, Feishu applet, QQ applet, Kuaishou applet|
|@animationfinish|EventHandle||动画结束时会触发 animationfinish 事件，event.detail = {current: current, source: source}|字节跳动小程序与飞书小程序不支持|
|@animationfinish|EventHandle||The animationfinish event will be triggered when the animation ends, event.detail = {current: current, source: source}|ByteDance applet and Feishu applet are not supported|

change 事件返回 detail 中包含一个 source 字段，表示导致变更的原因，可能值如下：
A source field is contained when change event returns detail, which indicates the cause of the change. Possible values are as follows:

- autoplay 自动播放导致swiper变化。
- Autoplay causes the swiper to change.
- touch 用户划动引起swiper变化。
- User touch causes the swiper to change.
- 其他原因将用空字符串表示。
- Other reasons will be indicated by an empty string.

**swiper做左右拖动的长列表的专项问题**
**A special issue about using swiper to make long lists of left and right drags**
- swiper是单页组件，适合做banner图轮播和简单列表左右滑动。
- Swiper is a single page component suitable for banner picture carousel and simple list sliding left and right.
- 因为性能问题，用swiper做复杂长列表，需要较高的优化技巧以及接受一些限制。
- For perlistance reasons, making complex long lists with swiper requires high optimization skills and will be subject to certain limitations.
- 这是一个范例，[插件市场新闻模板示例](https://ext.dcloud.net.cn/plugin?id=103)，它在App端使用了nvue的原生渲染，实现高性能的左右拖动长列表；并支持可自定义的任何形式的下拉刷新。它在非App端使用的模式是只缓存左右一共3列的数据，dom中的数据过多时，它会自动释放。就是说App上，只要看过这一页，再进去时内容是还在的。而在非App上，只能做到缓存3页数据，其他页即便看过，再进去也会重新加载。并且非App的这种情况下，不再提供下拉刷新。虽然插件市场也有其他前端模拟的下拉刷新，但性能不佳。一般小程序的大厂案例里，提供左右拖长列表的，都是这种做法。
- This is an example, [plugin market news template example](https://ext.dcloud.net.cn/plugin?id=103), which uses nvue's native rendering on the App side to achieve high-performance left-right dragging A long list; and supports any form of drop-down refresh that can be customized. The mode it uses on the non-App side is to cache only 3 columns of data on the left and right. When there is too much data in the dom, it will be automatically released. That is to say, on the App, as long as you read this page, the content is still there when you enter it again. On non-Apps, only 3 pages of data can be cached, and other pages will be reloaded even if they are read. And in this case of non-App, pull-down refresh is no longer provided. While the plugin marketplace has other front-end emulated pull-to-refreshes, they don't perform as well. In the case of large manufacturers of general small programs, this is the practice that provides long lists of left and right.

**Tips**

- 如果 nvue 页面 ``@animationfinish`` 事件不能返回正确的数据，可同时监听 ``@change`` 事件。
- If the `@animationfinish` event on the nvue page cannot return correct data, you can listen to the `@change` event at the same time.
- 使用竖向滚动时，需要给 ``<scroll-view>`` 一个固定高度，通过 css 设置 height。
- When using vertical scrolling, you need to give `<scroll-view>` a fixed height by css.
- 注意：其中只可放置 ``<swiper-item>`` 组件，否则会导致未定义的行为。 
- Note: Only the `<swiper-item>` component can be placed in it, or otherwise it will lead to undefined behavior.
- 如果遇到current、current-item-id属性设置不生效的问题参考：[组件属性设置不生效解决办法](/tutorial/vue-api.html#componentsolutions)
- If you encounter the problem that the current and current-item-id attribute settings do not take effect, please refer to: [Component attribute settings do not take effect solution](/tutorial/vue-api.html#componentsolutions)
- banner图的切换效果和指示器的样式，有多种风格可自定义，可在[uni-app插件市场](https://ext.dcloud.net.cn/search?q=%E8%BD%AE%E6%92%AD)搜索
- The switching effect of the banner picture and the style of the indicator can be customized in a variety of styles, which can be searched in the [uni-app plug-in market](https://ext.dcloud.net.cn/search?q=%E8%BD%AE%E6%92%AD)
- 如需banner管理后台，参考uniCloud admin banner插件：[https://ext.dcloud.net.cn/plugin?id=4117](https://ext.dcloud.net.cn/plugin?id=4117)
- For banner management background, refer to uniCloud admin banner plug-in: [https://ext.dcloud.net.cn/plugin?id=4117](https://ext.dcloud.net.cn/plugin?id=4117)
- swiper在App的vue中、百度支付宝头条QQ小程序中，不支持内嵌video、map等原生组件。在微信基础库2.4.4起和App nvue2.1.5起支持内嵌原生组件。竖向的swiper内嵌视频可实现抖音、映客等视频垂直拖动切换效果。
- swiper does not support native components such as embedded video and map in the app's vue and Baidu Alipay Toutiao QQ applet. Since WeChat base library 2.4.4 and App nvue 2.1.5, embedded native components are supported. The vertical swiper embedded video can realize the vertical drag switching effect of videos such as Douyin and Inke.
- 同时监听 change transition，开始滑动时触发transition, 放开手后，在ios平台触发顺序为 transition... change，Android/微信小程序/支付宝为 transition... change transition...
- Monitor the change transition at the same time, trigger the transition when you start to slide, and release the hand, the trigger sequence on the ios platform is transition... change, Android/WeChat applet/Alipay is transition... change transition...
 
 
#### easing-function 

|值	|	说明|
|value | description|
|--	|--	|
|default	|默认缓动函数	|
|default |Default easing function |
|linear	|线性动画	|
|linear |Linear animation |
|easeInCubic	|缓入动画	|
|easeInCubic |Ease-In Animation |
|easeOutCubic	|缓出动画	|
|easeOutCubic |Ease Out Animation |
|easeInOutCubic	|	缓入缓出动画	|
|easeInOutCubic | Ease In Ease Out Animation |

 
 
 
#### swiper-item
仅可放置在 ``<swiper>`` 组件中，宽高自动设置为100%。注意：宽高100%是相对于其父组件，不是相对于子组件，不能被子组件自动撑开。
It can only be placed in the `<swiper>` component, with the width and height automatically set to 100%. Note: 100% of the width and height is relative to its parent component rather than sub-component, and it cannot be opened automatically by sub-component.

|属性名|类型|默认值|说明|
| Attribute name| Type| Defaults| Instruction|
|:-|:-|:-|:-|
|item-id|String||该 swiper-item 的标识符|
| item-id| String| | The identifier of this swiper-item|

**示例** [查看演示](https://hellouniapp.dcloud.net.cn/pages/component/swiper/swiper)
**Example** [View demo](https://hellouniapp.dcloud.net.cn/pages/component/swiper/swiper)

以下示例代码，来自于[hello uni-app项目](https://github.com/dcloudio/hello-uniapp)，推荐使用HBuilderX，新建uni-app项目，选择hello uni-app模板，可直接体验完整示例。
The following sample code comes from the [hello uni-app project](https://github.com/dcloudio/hello-uniapp). It is recommended to use HBuilderX to create a new uni-app project and choose the hello uni-app template to directly experience the complete example.

::: preview https://hellouniapp.dcloud.net.cn/pages/component/swiper/swiper
> Template
```vue
<!-- 本示例未包含完整css，获取外链css请参考上文，在hello uni-app项目中查看 -->
<!-- This example does not include the complete css, please refer to the above to obtain the external css. View it in the hello uni-app project -->
<template>
	<view>
		<view class="uni-margin-wrap">
			<swiper class="swiper" circular :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval"
				:duration="duration">
				<swiper-item>
					<view class="swiper-item uni-bg-red">A</view>
				</swiper-item>
				<swiper-item>
					<view class="swiper-item uni-bg-green">B</view>
				</swiper-item>
				<swiper-item>
					<view class="swiper-item uni-bg-blue">C</view>
				</swiper-item>
			</swiper>
		</view>
		
		<view class="swiper-list">
			<view class="uni-list-cell uni-list-cell-pd">
				<view class="uni-list-cell-db">指示点</view>
				<switch :checked="indicatorDots" @change="changeIndicatorDots" />
			</view>
			<view class="uni-list-cell uni-list-cell-pd">
				<view class="uni-list-cell-db">自动播放</view>
				<switch :checked="autoplay" @change="changeAutoplay" />
			</view>
		</view>
		
		<view class="uni-padding-wrap">
			<view class="uni-common-mt">
				<text>幻灯片切换时长(ms)</text>
				<text class="info">{{duration}}</text>
			</view>
			<slider @change="durationChange" :value="duration" min="500" max="2000" />
			<view class="uni-common-mt">
				<text>自动播放间隔时长(ms)</text>
				<text class="info">{{interval}}</text>
			</view>
			<slider @change="intervalChange" :value="interval" min="2000" max="10000" />
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
            background: ['color1', 'color2', 'color3'],
            indicatorDots: true,
            autoplay: true,
            interval: 2000,
            duration: 500
        }
    },
    methods: {
        changeIndicatorDots(e) {
            this.indicatorDots = !this.indicatorDots
        },
        changeAutoplay(e) {
            this.autoplay = !this.autoplay
        },
        intervalChange(e) {
            this.interval = e.target.value
        },
        durationChange(e) {
            this.duration = e.target.value
        }
    }
}
</script>
```
> Style
```vue
<style>
	.uni-margin-wrap {
		width: 690rpx;
		width: 100%;
	}
	.swiper {
		height: 300rpx;
	}
	.swiper-item {
		display: block;
		height: 300rpx;
		line-height: 300rpx;
		text-align: center;
	}
	.swiper-list {
		margin-top: 40rpx;
		margin-bottom: 0;
	}
	.uni-common-mt {
		margin-top: 60rpx;
		position: relative;
	}
	.info {
		position: absolute;
		right: 20rpx;
	}
	.uni-padding-wrap {
		width: 550rpx;
		padding: 0 100rpx;
	}
</style>
```
:::

