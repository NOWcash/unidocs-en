## 互动广告

## 简介

互动广告是DCloud联合三方服务商为开发者提供新的广告场景增值服务。开发者在App中放置入口，用户点击入口参与权益化、趣味性的活动。


**平台差异说明**

|App				|H5					|微信小程序	|支付宝小程序	|百度小程序	|字节跳动小程序	|QQ小程序	|快应用	|360小程序|快手小程序	|京东小程序	|
|:-:				|:-:				|:-:				|:-:					|:-:				|:-:						|:-:			|:-:		|:-:			|:-:				|:-:				|
|√(3.5.5+)	|√(3.5.5+)	|√(3.5.5+)	|x						|x					|x							|x				|x			|x				|x					|x					|


**开通配置广告**

[开通广告步骤详情](https://uniapp.dcloud.net.cn/uni-ad.html#start)


## 语法

`<ad-interactive></ad-interactive>`


**属性说明**

|属性名																	|类型				|默认值		|说明																|
|:-																			|:-					|:-				|:-																	|
|adpid																	|String			|					|广告位id														|
|open-page-path													|String			|					|点击广告后需要打开的webview页面路径|
|v-slot:default="{data, loading, error}"|						|					|组件内部广告加载状态和加载错误信息	|
|@load																	|EventHandle|加载事件	|																		|
|@error																	|EventHandle|错误事件	|																		|


### 简单示例

```html
<template>
  <view>
    <!-- 互动广告组件, 3.5.5+，目前仅支持微信小程序 -->
    <!-- 用户点击组件后将打开广告页面，参见属性 open-page-path -->
    <ad-interactive adpid="1000000001" v-slot:default="{data, loading, error}" open-page-path="/pages/ad-interactive-webview/ad-interactive-webview">
      <view v-if="data">
        <!-- 可以自定义此图片，组件提供了默认素材，通过 uni-ad 后台配置 -->
        <image :src="data.imgUrl" style="width: 128px; height: 72px;"></image>
      </view>
    </ad-interactive>
  </view>
</template>
```

注意：需要添加依赖页面 [open-page-path](#openpagepath)

### 完整示例

```html
<template>
  <view class="content">
    <!-- 互动广告组件, 3.5.5+，目前仅支持微信小程序 -->
    <!-- 用户点击组件后将打开广告页面，参见属性 open-page-path -->
    <ad-interactive adpid="1000000001" v-slot:default="{data, loading, error}" @load="onadload" @error="onaderror" open-page-path="/pages/ad-interactive-webview/ad-interactive-webview">
      <view v-if="loading">Loading</view>
      <view v-if="data">
        <!-- 可以自定义此图片，组件提供了默认素材，通过 uni-ad 后台配置 -->
        <image :src="data.imgUrl" style="width: 128px; height: 72px;"></image>
      </view>
      <view v-if="error">{{error.errMsg}}</view>
    </ad-interactive>
  </view>
</template>

<script>
export default {
  data() {
    return {
    }
  },
  methods: {
    onadload(e) {
      console.log('广告数据加载成功');
    },
    onaderror(e) {
      // 广告加载失败
      console.log("onaderror", e.errCode, e.errMsg);
    }
  }
}
</script>
```


### open-page-path 页面代码@openpagepath

组件的 `open-page-path` 属性所需页面，点击广告后将打开此页面

在项目的pages目录上右键，新增 `ad-interactive-webview.vue` 页面，并复制替换为下面代码

```html
<template>
  <web-view :src="url"></web-view>
</template>

<script>
  export default {
    data() {
      return {
        url: ''
      }
    },
    onLoad(options) {
      if (options && options.url) {
        this.url = decodeURIComponent(options.url);
      }
    }
  }
</script>
```


## 接入步骤

1. 开通并[申请](https://uniapp.dcloud.net.cn/)广告位
3. 在需要展示广告的地方放入 `<ad-interactive></ad-interactive>` 组件代码，此广告可作为悬浮红包使用，设置组件样式 fixed 定位即可
4. 在项目中新增 [ad-interactive-webview](#openpagepath) 页面


运行到微信小程序时需要添加request合法域名和业务域名白名单

1. 登陆 [微信公众平台](https://mp.weixin.qq.com/)，左侧栏找到 `开发管理` 并点击 开发设置->服务器域名
2. 新增 `request合法域名`: `https://wxac1.dcloud.net.cn`
3. 新增 `业务域名`: `https://engine.dcad01.com`
