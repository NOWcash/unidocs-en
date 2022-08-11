云端一体安全网络

## 简介

网络安全的问题很多：

1. 客户端受信。因为过去采用无状态网络通过接口交换数据，客户端的真实性很难保证。
2. 网络抓包，即便是https的请求也会被抓包。

当攻击者了解了你的服务器接收什么样的数据时，就可以冒名客户端，提交假数据来攻击你的服务器。

尤其当你的业务中涉及促销、返佣、激励视频等场景，非常容易被刷。褥羊毛已经是一个非常成熟的灰产。

当DCloud同时提供了`uni-app` 和 `uniCloud`时，事实上具备了提供云端一体的安全网络的能力。

在HBuilderX 3.5.5+ ，当开发者同时使用 `uni-app` 和 `uniCloud` 时，可以在网络请求时选择是否通过安全网络运行，它通过高安全的保护机制，防止客户端伪造和通信内容抓包。

注意：安全网络不支持web平台，只支持微信小程序和App。并且App的安全级别更高。

**平台差异说明**

|App|微信小程序|
|:-:|:-:|
|后续支持|3.5.5+|

## 开通流程

### App平台

后续支持

### 微信小程序

1. 下载uni-id插件

- `uni-id-co` [详情]()

2. 下载uni-open-bridge插件

在微信小程序上依赖 `access_token`、`session_key`, `encrypt_key`。这些凭据需要`uni-open-bridge`统一接管。

- `uni-open-bridge` [详情]()

3. 在应用的生命周期 `onLaunch` 中检查微信登陆状态，如果过期需要登陆

注意 `uni.checkSession` 有调用次数限制警告，一个 `pv` 可调用 `2` 次

```js
// App.vue
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


## 调用方式

开通配置后，在uni-app客户端调用uniCloud服务器时，可以通过加入secret参数来声明这次请求走安全网络，对传输数据加密。

- callFunction

客户端通过callFunction调用云函数时，加入secret参数。
```js
uniCloud.callFunction({
  name: 'collection',
  data: {
    name: 'user'
  },
  secret: 'both'
})
```


- 云对象

客户端通过importObject调用云对象时，加入secret和secretMethods参数。

```js
uniCloud.importObject('object-name', {
  customUI: false,
  secret: 'both',
  secretMethods: ['login']
})
```


**secret 属性说明**

|值				|描述																						|
|:-:			|:-:																						|
|none			|不加密，默认值																	|
|request	|只加密客户端请求时的上行数据，服务器下发数据不加密	|
|response	|客户端请求时不加密数据，只加密服务器下发的数据			|
|both			|客户端和服务器上行下行数据都加密数据							|

**secretMethods 属性说明**

`secretMethods` 是云对象中指定需要加密的方法名。因为云对象导入后，调用方法时没有额外指定的方式，所以集中在这里配置。如果不配置，则云对象的所有方法请求时都会加密。


## 小贴士

1. 安全是相对的，没有绝对的安全。
2. 安全是有代价的，加密的数据越庞大，加密和解密的耗时越长。