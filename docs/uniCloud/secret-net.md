**云端一体安全网络**

> HBuilderX 3.6.2+ 支持

## 简介
## Introduction

网络安全的问题很多：
There are many problems with network security:

1. 客户端受信。因为过去采用无状态网络通过接口交换数据，客户端的真实性很难保证。
1. The client is trusted. Because in the past, stateless networks were used to exchange data through interfaces, the authenticity of the client was difficult to guarantee.
2. 网络抓包，即便是https的请求也会被抓包。
2. Network packet capture, even https requests will be captured.

当攻击者了解了你的服务器接收什么样的数据时，就可以冒名客户端，提交假数据来攻击你的服务器。
When an attacker knows what kind of data your server receives, they can impersonate the client and submit fake data to attack your server.

尤其当你的业务中涉及促销、返佣、激励视频等场景，非常容易被刷。褥羊毛已经是一个非常成熟的灰产。
Especially when your business involves promotions, rebates, incentive videos and other scenarios, it is very easy to be brushed. Bedding wool is already a very mature grey product.

DCloud面向开发者同时提供了端引擎`uni-app` 和 云引擎`uniCloud`，其实可以提供云端一体的安全网络的能力。

`uni-app` 连接 `uniCloud` 时，可以选择是否启动安全网络。它通过高安全的保护机制，防止客户端伪造和通信内容抓包。

注意：安全网络不支持web平台，只支持微信小程序和App。并且App的安全级别更高。
Note: Safe Network does not support web platform, only WeChat applet and App. And the security level of the App is higher.

**平台差异说明**
**Platform Difference Description**

|App|微信小程序|
|App|WeChat Mini Program|
|:-:|:-:|
|后续支持|3.6.2+|
|Follow-up support|3.6.2+|

## 准备工作

### 微信小程序

安全网络在微信小程序上的实现，依赖了微信提供的一些用户级的凭据。所以需要下载`uni-id`和`uni-open-bridge`，并在app.vue里初始化。

1. 工程中导入uni-id

- `uni-id` [文档](uni-id-summary.md#save-user-token)
- `uni-id-co` [插件下载地址](https://ext.dcloud.net.cn/plugin?id=8577)

`uni-id-pages`这个插件是云端一体的登录插件，其实安全网络只需要其中的`uni-id-co`云对象。插件中前端登录页面是否使用由开发者自己根据业务决定。

2. 工程中导入uni-open-bridge插件

安全网络在微信小程序上依赖了微信的 `access_token`、`session_key`、`encrypt_key`等凭据。这些凭据需要`uni-open-bridge`统一接管。

- `uni-open-bridge` [文档](https://uniapp.dcloud.net.cn/uniCloud/uni-open-bridge.html)
- `uni-open-bridge` [插件下载地址](https://ext.dcloud.net.cn/plugin?id=9002)

3. 配置uni-id和uni-open-bridge

**缺内容，说清楚从微信小程序后台取哪些凭据，填到哪里？**

如果项目之前已经使用过uni-id和uni-open-bridge，则上述步骤可省略。

4. 在应用的生命周期 `onLaunch` 中检查微信登陆状态，如果过期需要登陆

注意: [uni.checkSession](https://uniapp.dcloud.net.cn/api/plugins/login.html#uni-checksession) 有调用次数限制警告，一个 `pv` 可调用 `2` 次
Note: [uni.checkSession](https://uniapp.dcloud.net.cn/api/plugins/login.html#uni-checksession) has a warning about the number of calls, a `pv` can be called `2` times

App.vue页面需要补充如下代码：
```js
<script>
  function checkUserSession() {
    uni.checkSession({
      fail: (err) => {
        uni.login({
          success: async ({ code }) => {
            const uniIdCo = uniCloud.importObject('uni-id-co') // uniCloud云对象 uni-id-co
            await uniIdCo.loginByWeixin({ code })
          }
        })
      }
    })
  }

  export default {
    onLaunch: function() {
      console.log('App Launch')
      // #ifdef MP-WEIXIN
      checkUserSession();
      // #endif
    }
  }
</script>
```

5. 在manifest中勾选加密模块
**缺内容？**

## 调用方式
## calling method

准备工作完成后，在uni-app客户端调用uniCloud服务器时，可以通过加入secret参数来声明这次请求走安全网络，对传输数据加密。

- callFunction

客户端通过callFunction调用云函数时，加入secretType参数。
```js
uniCloud.callFunction({
  name: 'collection',
  data: {
    name: 'user'
  },
  secretType: 'both' //both指上下行数据都加密，具体见下
})
```

- 云对象
- cloud objects

客户端通过importObject调用云对象时，通过secretMethods参数来配置每个方法调用时是否加密。

```js
uniCloud.importObject('object-name', {
  secretMethods: {'login':'both'}
})
```

**clientDB呢？**

**secretType 属性说明**

|值			|描述												|
|:-:		|:-:												|
|none		|不加密，默认值										|
|request	|只加密客户端请求时的上行数据，服务器下发数据不加密	|
|response	|客户端请求时不加密数据，只加密服务器下发的数据		|
|both		|客户端和服务器上行下行数据都加密数据				|

**secretMethods 属性说明**

`secretMethods` 是云对象中指定需要加密的方法名。可对每个方法配置，例如: `secretMethods: {'login':'both'}`，指定 `login` 方法的 `secretType` 为 both

## 服务器端
## Service-Terminal

虽然uni-app客户端和uniCloud云端通信是加密的，但对于开发者而言过程是透明的。

**不管是客户端接收云端数据、还是云端接受客户端数据，开发者的代码拿到的拿到的数据都是加密后的数据。**

但云端有一个注意事项：为了避免客户端伪造`secretType`获取服务器敏感数据，应以服务器端为准，如果客户端携带的 `secretType` 不符合要求应拒绝响应数据。示例代码如下

- 云函数中验证secretType

在云函数的context中有secretType。

```js
exports.main = async (event, context) => {
  const secretType = context.secretType
  // secretType 是客户端调用 uniCloud.callFunction 传递的参数 secretType
  // secretType is the parameter secretType passed by the client to call uniCloud.callFunction

  if (secretType !== 'both' || secretType !== 'response') {
    return null
  }
}
```

- 云对象中验证secretType

在云对象的this中有secretType。

```js
module.exports = {
  async _before() {
    const methodName = this.getMethodName()
    const clientInfo = this.getClientInfo()
    const secretType = clientInfo.secretType
    // methodName 是客户端调用的方法名
    // methodName is the method name called by the client
    // secretType 是客户端调用 uniCloud.importObject 传递的参数 secretMethods
    // secretType is the parameter secretMethods passed by the client when calling uniCloud.importObject

    if (methodName === 'login' && (secretType !== 'both' || secretType !== 'response')) {
      throw new Error('secretType invalid')
    }
  }
}
```

## 错误码

**缺内容，客户端错误，服务器解密错误，都应该把错误码列出来？**

## 小贴士
## Tips

1. 安全是相对的，没有绝对的安全。
2. 安全是有代价的，加密的数据越庞大，加密和解密的耗时越长。
