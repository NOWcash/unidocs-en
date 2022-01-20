#### uni.createCanvasContext(canvasId, this)

#### 定义
#### Definition

创建 ```canvas``` 绘图上下文（指定 canvasId）。在自定义组件下，第二个参数传入组件实例this，以操作组件内 ```<canvas/>``` 组件
Create `canvas` Graphics Context (specify canvasId). Under custom components, the second parameter is passed into the custom component instance this to operate the `<canvas/>` component.

**Tip:** 需要指定 canvasId，该绘图上下文只作用于对应的 `<canvas/>`
**Tip:** canvasId needs to be specified, and this Graphics Context only works on the corresponding `<canvas/>`

#### 参数
#### Parameter

|参数|类型|说明|
| Parameter| Type| Instruction|
|----|----|-----|
|canvasId|String	|画布表示，传入定义在 `<canvas/>` 的 canvas-id或id|
| canvasId| String| Canvas identification, passing in the canvas-id or id defined in `<canvas/>`|
|componentInstance|Object	|自定义组件实例 this ，表示在这个自定义组件下查找拥有 canvas-id 的 `<canvas/>` ，如果省略，则不在任何自定义组件内查找	|
| componentInstance| Object| Custom component instance this means to find the `<canvas/>` with canvas-id under this custom component. If omitted, it will not find in any custom component|

#### 返回值
#### Return value

[CanvasContext](/api/canvas/CanvasContext.md)