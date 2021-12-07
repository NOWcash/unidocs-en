#### icon

图标。

**平台差异说明**

|App|H5|
|:-:|:-:|
|√|√(2.2.3+)|

**Tips**

* 由于 icon 组件各端表现存在差异，可以通过使用 [字体图标](/frame?id=字体图标) 的方式来弥补各端差异。

**属性说明**

|属性名|类型|默认值|说明|
|---|---|---|---|
|type|String||icon的类型|
|size|Number|23|icon的大小，单位px|
|color|Color||icon的颜色，同css的color|

各平台 type 有效值说明：

|平台|type 有效值|
|:-:|:-:|
|App、H5|success, success_no_circle, info, warn, waiting, cancel, download, search, clear|


**示例**
```html
<view class="item" v-for="(value,index) in iconType" :key="index">
    <icon :type="value" size="26"/>
    <text>{{value}}</text>
</view>
```
```javascript
export default {
    data() {
        return {
            iconType: ['success']
        }
    },
    onLoad() {
        // #ifdef APP
        this.iconType = ['success', 'success_no_circle', 'info', 'warn', 'waiting', 'cancel', 'download', 'search','clear']
        // #endif
    }
}

```

**效果展示**

<div style="display:flex;align-items: flex-start;justify-content: center;flex-wrap: wrap;">
		<img src="https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/d188f390-4f30-11eb-97b7-0dc4655d6e68.png" width="375" style="margin-right:20px;"/>
		<img src="https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/d2562ea0-4f30-11eb-97b7-0dc4655d6e68.png" width="375"/>
</div>
