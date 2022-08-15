# uni-open-bridge

`uni-open-bridge` 是统一接管微信等三方平台认证凭据（包括但不限于`access_token`、`session_key`、`encrypt_key`、`ticket`）的开源库。

## 背景

调用微信等三方开放平台时，涉及众多凭据。有的是固定凭据，没有有效期。有的是临时凭据，会在一定时间或一定操作后失效。

尤其是临时凭据，比如微信的`access_token`、`session_key`、`encrypt_key`、`ticket`， 开发者需要动态从微信服务器获取，统一保存。

但实际上这里面的坑很多：

1. 微信官方建议公众号开发者使用中控服务器统一获取和刷新 `access_token`，其他业务逻辑服务器所使用的 `access_token` 均来自于该中控服务器，不应该各自去刷新，否则容易造成冲突，导致 `access_token` 覆盖而影响业务；
2. 有的凭据有效期较短，比如`ticket` 的有效期为7200秒，需要定时请求，避免过期。并且由于获取 `ticket` 的 api 调用次数非常有限，频繁刷新 `ticket` 会导致 api 调用受限，影响自身业务，开发者必须在自己的服务全局缓存 `ticket `
3. 在客户端任意地方调用 `wx.login()` 后，会让上一个 `session_key` 立即过期

当多个业务都需要这些临时凭据时，无法让每个业务各自请求微信服务器，会非常混乱和容易冲突。

所以需要在一个中央系统，在定时任务里统一请求微信服务器，保存到数据库。

然后各个业务需要这些凭据时，从这个中央系统的接口中获取，而不是自己向微信服务器请求。

这个中央系统就是`uni-open-bridge`。

## 流程介绍

`uni-open-bridge` 包括：
1. 一个云对象 `uni-open-bridge` 
2. 一个公共模块 `uni-open-bridge-common` 
3. 配套的数据库，表名为 `opendb-open-data`。在redis中的key格式为 `uni-id:[dcloudAppid]:[platform]:[openid]:[access-token|user-access-token|session-key|encrypt-key-version|ticket]`

`uni-open-bridge`系统中，有一个同名云对象`uni-open-bridge`，它默认就是定时运行的，在package.json中配置了每小时定时运行一次（部署线上系统生效）。

该云对象根据在 `uni-config-center` 中[配置](#uni-id-config)固定凭据，从而有权定时向微信服务器发请求，将获取到的 `access_token`或`ticket` 保存到数据库 `opendb-open-data` 表中。

当所在服务空间开通redis时，还会缓存在redis的key。这会让系统性能更好。

上述获取到微信的各种临时凭据后，当各个业务代码需要这些凭据时，通过如下方式获取。

- 云函数/云对象获取这些临时凭据，可引用公共模块 `uni-open-bridge-common` ，通过该模块的API获取，比如getAccessToken。[见下](#uni-open-bridge-common)
- 非uniCloud系统，比如传统云，获取这些凭据，需要将云对象`uni-open-bridge`进行URL化，通过Http方式请求凭据。[见下](#http)

流程图如下：

![](https://vkceyugu.cdn.bspapp.com/VKCEYUGU-a90b5f95-90ba-4d30-a6a7-cd4d057327db/b80cec3b-e106-489d-9075-90b5ecb02963.png)

## 使用
1. **下载插件[uni-open-bridge](https://ext.dcloud.net.cn/plugin?id=9002)到项目中。

2. 在`uni-config-center`的 `uni-id` 下配置固定凭据，详情见下面的示例代码

首先向微信的[公众平台](https://mp.weixin.qq.com/)申请 `appid` 和 `secret` 固定凭据
然后在项目的 uniCloud/cloudfunctions/common/uni-config-center/uni-id/config.json 文件中配置

**示例代码**

### uni-id-config

```json
// uniCloud/cloudfunctions/common/uni-config-center/uni-id/config.json
{
  "dcloudAppid": "__UNI__xxxxxx", // 在项目的 manifest.json 中
  "mp-weixin": {
    "tokenExpiresIn": 259200,
    "oauth": {
      "weixin": {
        "appid": "", // 微信公众平台申请的小程序 appid
        "appsecret": "" // 微信公众平台申请的小程序 secret
      }
    }
  },
  "web": {
    "oauth": {
      "h5-weixin": {
        "appid": "", // 微信公众平台申请的网页授权 appid
        "appsecret": "" // 微信公众平台申请的网页授权 secret
      }
    }
  }
}
```

注意：拷贝此文件内容时需要移除 `注释`

3. 在`uni-config-center`目录下新建子目录`uni-open-bridge`, 新增 `config.json`，配置 dcloudAppid ，详情见下面的示例代码

### uni-open-bridge-config@uniopenbridgeconfig

**示例代码**

```json
// uniCloud/cloudfunctions/common/uni-config-center/uni-open-bridge/config.json
{
  "schedule": {
    "__UNI__xxxxxx": { // dcloudAppid, 需要和 `uni-config-center` uni-id中的配置一致
      "enable": true, // 任务全局开关，优先级最高
      "mp-weixin": { // 平台，目前仅支持 微信小程序、微信 H5，详情参见 https://uniapp.dcloud.net.cn/uniCloud/uni-open-bridge#platform
        "enable": true, // 当前平台任务开关
        "tasks": ["accessToken"] // 要执行的任务，微信小程序支持 accessToken
      },
      "h5-weixin": {
        "enable": false,
        "tasks": ["ticket"] // 支持微信 H5 ticket，因 ticker 依赖微信 H5 accessToken，内部自动先获取 accessToken。此处的 accessToken 和微信小程序的 accessToken 不是一个值
      }
    }
  },
  "ipWhiteList": ["0.0.0.0"] // 用于 http 调用的服务器IP白名单
}
```

注意：拷贝此文件内容时需要移除 `注释`

4. 将插件上传到服务空间。最好开通redis，会有更好的性能
然后在数据库和redis的`uni-id`分组中会看到数据。

如果异常，请在 [uniCloud Web控制台](https://unicloud.dcloud.net.cn/)，找到云函数/云对象 `uni-open-bridge` 检查运行日志。很可能是第一步或第二步的配置出错了。

## 业务系统获取相关凭据的方法

当业务不在uniCloud上时，在`uni-open-bridge`云对象获取到相关凭据后，当业务系统需要使用这些凭据时，通过下面的云对象URL化方式获取。


注意：为了安全鉴权需要在 `uni-open-bridge-config` 中的 ipWhiteList 节点下配置服务器IP

### 云函数公共模块方式@uni-open-bridge-common

当你的业务在uniCloud上时，在你的业务云函数/云对象中引用公共模块`uni-open-bridge-common`，然后调用下面的API。

> `云函数公共模块`是不同云函数共享代码的一种方式。如果你不了解什么是`云函数公共模块`，请另读文档[公共模块](https://uniapp.dcloud.io/uniCloud/cf-common)

`uni-open-bridge-common` 提供了 `access_token`、`session_key`、`encrypt_key`、`ticket` 的读取、写入、删除操作。

`uni-open-bridge-common` 支持多层 读取 / 写入 机制，`redis -> database -> fallback`，优先级如下:

如果用户没有开通 `redis` 或者操作失败，透传到 `database`，`database` 失败后，如果用户配置了 `fallback`，继续调用 `fallback` 方法，否则抛出 `Error`，`database` 对应的表为: `opendb-open-data`

#### getAccessToken(key: Object, fallback: Function)

读取 access_token

#### setAccessToken(key: Object, value: Object, expiresIn: Number)

写入 access_token

#### removeAccessToken(key: Object)

删除 access_token


**key 属性**

|参数				|类型			|必填	|描述																															|
|:-:				|:-:			|:-:	|:-:																															|
|dcloudAppid|String		|是		|DCloud应用appid。[详情](https://ask.dcloud.net.cn/article/35907)	|
|platform		|String		|是		|[详情](#platform)																								|

**value 属性**

|参数					|类型		|描述					|
|:-:					|:-:		|:-:					|
|access_token	|String	|							|

**expiresIn**

有效时间(秒)


**示例代码**

```js
'use strict';

const {
  getAccessToken,
  setAccessToken,
  removeAccessToken
} = require('uni-open-bridge-common')

exports.main = async (event, context) => {
  const key = {
    dcloudAppid: '__UNI__xxx',
    platform: 'mp-weixin'
  }
  const value = {
    access_token: ''
  }
  const expiresIn = 7200

  // 写入 (redis / 数据库)
  await setAccessToken(key, value, expiresIn)

  // 读取 (redis / 数据库)
  let result1 = await getAccessToken(key)

  // 删除
  await removeAccessToken(key)

  // 删除后读取, 返回 null
  let result2 = await getAccessToken(key)
  console.log(result2) // null

  return null
};
```

#### getUserAccessToken(key: Object, fallback: Function)

读取 user_access_token

#### setUserAccessToken(key: Object, value: Object, expiresIn: Number)

写入 user_access_token

#### removeUserAccessToken(key: Object)

删除 user_access_token


对应微信公众平台网页用户授权 `access_token`，详情见下文说明


**key 属性**

|参数				|类型			|必填	|描述																															|
|:-:				|:-:			|:-:	|:-:																															|
|dcloudAppid|String		|是		|DCloud应用appid。[详情](https://ask.dcloud.net.cn/article/35907)	|
|platform		|String		|是		|[详情](#platform)																								|
|openid			|String		|是		|																																	|

**value 属性**

|参数					|类型		|描述											|
|:-:					|:-:		|:-:											|
|access_token	|String	|微信公众平台用户会话密钥	|

**expiresIn**

有效时间(秒)

**示例代码**

```js
'use strict';

const {
  getUserAccessToken,
  setUserAccessToken,
  removeUserAccessToken
} = require('uni-open-bridge-common')

exports.main = async (event, context) => {
  const key = {
    dcloudAppid: '__UNI__xxx',
    platform: 'h5-weixin',
    openid: ''
  }
  const value = {
    'access_token': ''
  }
  const expiresIn = 7200

  // 写入 (redis / 数据库)
  await setUserAccessToken(key, value, expiresIn)

  // 读取 (redis / 数据库)
  let result1 = await getUserAccessToken(key)

  // 删除
  await removeUserAccessToken(key)


  // 删除后读取, 返回 null
  let result2 = await getUserAccessToken(key)
  console.log(result2) // null

  return null
};
```


#### getSessionKey(key: Object, fallback: Function)

读取 session_key

#### setSessionKey(key: Object, value: Object, expiresIn: Number)

写入 session_key

#### removeSessionKey(key: Object)

删除 session_key


**key 属性**

|参数				|类型			|必填	|描述																															|
|:-:				|:-:			|:-:	|:-:																															|
|dcloudAppid|String		|是		|DCloud应用appid。[详情](https://ask.dcloud.net.cn/article/35907)	|
|platform		|String		|是		|[详情](#platform)																								|
|openid			|String		|是		|																																	|

**value 属性**

|参数				|类型		|描述								|
|:-:				|:-:		|:-:								|
|session_key|String	|微信小程序会话密钥	|

**expiresIn**

有效时间(秒)


**示例代码**

```js
'use strict';

const {
  getSessionKey,
  setSessionKey,
  removeSessionKey
} = require('uni-open-bridge-common')

exports.main = async (event, context) => {
  const key = {
    dcloudAppid: '__UNI__xxx',
    platform: 'mp-weixin',
    openid: ''
  }
  const value = {
    'session_key': ''
  }
  const expiresIn = 7200

  // 写入 (redis / 数据库)
  await setSessionKey(key, value, expiresIn)

  // 读取 (redis / 数据库)
  let result1 = await getSessionKey(key)

  // 删除
  await removeSessionKey(key)


  // 删除后读取, 返回 null
  let result2 = await getSessionKey(key)
  console.log(result2) // null

  return null
};
```


#### getEncryptKey(key: Object, fallback: Function)

读取 encrypt_key

#### setEncryptKey(key: Object, value: Object, expiresIn: Number)

写入 encrypt_key

#### removeEncryptKey(key: Object)

删除 encrypt_key


**key 属性**

|参数				|类型			|必填	|描述																															|
|:-:				|:-:			|:-:	|:-:																															|
|dcloudAppid|String		|是		|DCloud应用appid。[详情](https://ask.dcloud.net.cn/article/35907)	|
|platform		|String		|是		|[详情](#platform)																								|
|openid			|String		|是		|																																	|
|version		|Number		|是		|版本																															|


**value 属性**

|参数				|类型		|描述			|
|:-:				|:-:		|:-:			|
|encrypt_key|String	|加密 key	|
|iv					|String	|加密 iv	  |

**expiresIn**

有效时间(秒)


**示例代码**

```js
'use strict';

const {
  getEncryptKey,
  setEncryptKey,
  removeEncryptKey
} = require('uni-open-bridge-common')

exports.main = async (event, context) => {
  const key = {
    dcloudAppid: '__UNI__xxx',
    platform: 'mp-weixin',
    openid: '',
    version: 1
  }
  const value = {
    encrypt_key: '',
    iv: ''
  }
  const expiresIn = 7200

  // 写入 (redis / 数据库)
  await setEncryptKey(key, value, expiresIn)

  // 读取 (redis / 数据库)
  let result1 = await getEncryptKey(key)

  // 删除
  await removeEncryptKey(key)

  // 删除后读取, 返回 null
  let result2 = await getEncryptKey(key)
  console.log(result2) // null

  return null
};
```


#### getTicket(key: Object, fallback: Function)

读取 ticket

#### setTicket(key: Object, value: Object, expiresIn: Number)

写入 ticket

#### removeTicket(key: Object)

删除 ticket


**key 属性**

|参数				|类型			|必填	|描述																															|
|:-:				|:-:			|:-:	|:-:																															|
|dcloudAppid|String		|是		|DCloud应用appid。[详情](https://ask.dcloud.net.cn/article/35907)	|
|platform		|String		|是		|[详情](#platform)																								|

**value 属性**

|参数				|类型		|描述			|
|:-:				|:-:		|:-:			|
|ticket			|String	|					|

**expiresIn**

有效时间(秒)


**示例代码**

```js
'use strict';

const {
  getTicket,
  setTicket,
  removeTicket
} = require('uni-open-bridge-common')

exports.main = async (event, context) => {
  const key = {
    dcloudAppid: '__UNI__xxx',
    platform: 'h5-weixin'
  }
  const value = {
    ticket: ''
  }
  const expiresIn = 7200

  // 写入 (redis / 数据库)
  await setTicket(key, value, expiresIn)

  // 读取 (redis / 数据库)
  let result1 = await getTicket(key)

  // 删除
  await removeTicket(key)


  // 删除后读取, 返回 null
  let result2 = await getTicket(key)
  console.log(result2) // null

  return null
};
```


#### Platform@platform

平台对应的值

|值					|描述				|
|:-:				|:-:				|
|mp-weixin	|微信小程序	|
|app-weixin	|微信 App	  |
|h5-weixin	|微信公众号	|
|web-weixin	|微信pc网页	|
|mp-qq			|QQ 小程序		|
|app-qq			|QQ App			|

提示：目前仅支持 `mp-weixin`、`h5-weixin` 后续补充其他平台

#### fallback

可选 `async function fallback()`，当 `reids -> database` 都找不到对应 `key` 时，调用此方法，需要返回数据格式如下

```json
{
  value: null,
  duration: 1
}
```

为了简化调用 `getAccessToken()`、`getTicket()` 已内置 `fallback` 到微信的服务器，需要在 `config-center` 中配置 `appid` `appsecret`

#### 注意事项

- 所有方法类型为 `async`，需要使用 `await`
- 所有方法校验 `key` 属性是否有效，无效则 `throw new Error()`，对 `value` 仅校验是否为 `Object`


### 云对象URL化方式

云对象 `uni-open-bridge` URL化后，让非uniCloud系统可通过 http 方式访问凭据。

[URL化](http.md)，是一种让云函数或云对象暴露为Http接口的方式，[详见](http.md)。可以在 [uniCloud Web控制台](https://unicloud.dcloud.net.cn/) 操作。

请求类型 `POST`, 可以配置IP白名单字段 `ipWhiteList`，参见 `config.json`


#### getAccessToken

Url

```
https://xxxxxxxx-xxxx-4xxx-xxxx-xxxxxxxxxxxx.bspapp.com/uni-open-bridge/getAccessToken
```

参数

```json
{
  "dcloudAppid": "__UNI__xxx",
  "platform": "mp-weixin"
}
```

#### setAccessToken

Url

```
https://xxxxxxxx-xxxx-4xxx-xxxx-xxxxxxxxxxxx.bspapp.com/uni-open-bridge/setAccessToken
```

```json
{
  "dcloudAppid": "__UNI__xxx",
  "platform": "mp-weixin",
  "value": {
    "access_token": ""
  },
  "expiresIn": 7200
}
```

#### removeAccessToken

Url

```
https://xxxxxxxx-xxxx-4xxx-xxxx-xxxxxxxxxxxx.bspapp.com/uni-open-bridge/removeAccessToken
```

参数

```json
{
  "dcloudAppid": "__UNI__xxx",
  "platform": "mp-weixin"
}
```

其中参数platform值域[详见](#platform)

#### getUserAccessToken

Url

```
https://xxxxxxxx-xxxx-4xxx-xxxx-xxxxxxxxxxxx.bspapp.com/uni-open-bridge/getUserAccessToken
```

参数

```json
{
  "dcloudAppid": "__UNI__xxx",
  "platform": "h5-weixin",
  "openid": ""
}
```

#### setUserAccessToken

Url

```
https://xxxxxxxx-xxxx-4xxx-xxxx-xxxxxxxxxxxx.bspapp.com/uni-open-bridge/setUserAccessToken
```

参数

```json
{
  "dcloudAppid": "__UNI__xxx",
  "platform": "h5-weixin",
  "openid": "",
  "value": {
    "access_token": ""
  },
  "expiresIn": 7200
}
```

#### removeUserAccessToken

Url

```
https://xxxxxxxx-xxxx-4xxx-xxxx-xxxxxxxxxxxx.bspapp.com/uni-open-bridge/removeUserAccessToken
```

参数

```json
{
  "dcloudAppid": "__UNI__xxx",
  "platform": "h5-weixin",
  "openid": ""
}
```

#### getSessionKey

Url

```
https://xxxxxxxx-xxxx-4xxx-xxxx-xxxxxxxxxxxx.bspapp.com/uni-open-bridge/getSessionKey
```

参数

```json
{
  "dcloudAppid": "__UNI__xxx",
  "platform": "mp-weixin",
  "openid": ""
}
```

#### setSessionKey

Url

```
https://xxxxxxxx-xxxx-4xxx-xxxx-xxxxxxxxxxxx.bspapp.com/uni-open-bridge/setSessionKey
```

参数

```json
{
  "dcloudAppid": "__UNI__xxx",
  "platform": "mp-weixin",
  "openid": "",
  "value": {
    "session_key": ""
  },
  "expiresIn": 7200
}
```

#### removeSessionKey

Url

```
https://xxxxxxxx-xxxx-4xxx-xxxx-xxxxxxxxxxxx.bspapp.com/uni-open-bridge/removeSessionKey
```

参数

```json
{
  "dcloudAppid": "__UNI__xxx",
  "platform": "mp-weixin",
  "openid": ""
}
```

#### getEncryptKey

Url

```
https://xxxxxxxx-xxxx-4xxx-xxxx-xxxxxxxxxxxx.bspapp.com/uni-open-bridge/getEncryptKey
```

参数

```json
{
  "dcloudAppid": "__UNI__xxx",
  "platform": "mp-weixin",
  "openid": "",
  "version": 1 // 此版本号应根据客户端传递的版本号
}
```

#### setEncryptKey

Url

```
https://xxxxxxxx-xxxx-4xxx-xxxx-xxxxxxxxxxxx.bspapp.com/uni-open-bridge/setEncryptKey
```

参数

```json
{
  "dcloudAppid": "__UNI__xxx",
  "platform": "mp-weixin",
  "openid": "",
  "version": 1,
  "value": {
    "encrypt_key": "",
    "iv": ""
  }
}
```

#### removeEncryptKey

Url

```
https://xxxxxxxx-xxxx-4xxx-xxxx-xxxxxxxxxxxx.bspapp.com/uni-open-bridge/removeEncryptKey
```

参数

```json
{
  "dcloudAppid": "__UNI__xxx",
  "platform": "mp-weixin",
  "openid": "",
  "version": 1
}
```


#### getTicket

Url

```
https://xxxxxxxx-xxxx-4xxx-xxxx-xxxxxxxxxxxx.bspapp.com/uni-open-bridge/getTicket
```

参数

```json
{
  "dcloudAppid": "__UNI__xxx",
  "platform": "h5-weixin"
}
```

#### setTicket

Url

```
https://xxxxxxxx-xxxx-4xxx-xxxx-xxxxxxxxxxxx.bspapp.com/uni-open-bridge/setTicket
```

参数

```json
{
  "dcloudAppid": "__UNI__xxx",
  "platform": "h5-weixin",
  "value": {
    "ticket": ""
  }
}
```

#### removeTicket

Url

```
https://xxxxxxxx-xxxx-4xxx-xxxx-xxxxxxxxxxxx.bspapp.com/uni-open-bridge/removeTicket
```

参数

```json
{
  "dcloudAppid": "__UNI__xxx",
  "platform": "h5-weixin"
}
```


## 微信凭据介绍

### access_token(应用级)@access_token

- 微信小程序 `access_token` 是微信小程序全局唯一后台接口调用凭据，调用绝大多数后台接口时都需使用。[详情](https://developers.weixin.qq.com/miniprogram/dev/framework/server-ability/backend-api.html#access_token)

- 微信H5 `access_token` 是公众号的全局唯一接口调用凭据，公众号调用各接口时都需使用 `access_token`。开发者需要进行妥善保存。`access_token` 的存储至少要保留512个字符空间。`access_token` 的有效期目前为2个小时，需定时刷新，重复获取将导致上次获取的 `access_token` 失效。

公众平台的 API 调用所需的 `access_token` 的使用及生成方式说明：

1、建议公众号开发者使用中控服务器统一获取和刷新 `access_token`，其他业务逻辑服务器所使用的 `access_token` 均来自于该中控服务器，不应该各自去刷新，否则容易造成冲突，导致 `access_token` 覆盖而影响业务；

2、目前`access_token` 的有效期通过返回的expires_in来传达，目前是7200秒之内的值。中控服务器需要根据这个有效时间提前去刷新新 `access_token`。在刷新过程中，中控服务器可对外继续输出的老 `access_token`，此时公众平台后台会保证在5分钟内，新老 `access_token` 都可用，这保证了第三方业务的平滑过渡；

3、`access_token` 的有效时间可能会在未来有调整，所以中控服务器不仅需要内部定时主动刷新，还需要提供被动刷新 `access_token` 的接口，这样便于业务服务器在 API 调用获知 `access_token` 已超时的情况下，可以触发 `access_token` 的刷新流程。

4、对于可能存在风险的调用，在开发者进行获取 `access_token` 调用时进入风险调用确认流程，需要用户管理员确认后才可以成功获取。具体流程为：

开发者通过某 IP 发起调用->平台返回错误码[89503]并同时下发模板消息给公众号管理员->公众号管理员确认该 IP 可以调用->开发者使用该 IP 再次发起调用->调用成功。

如公众号管理员第一次拒绝该 IP 调用，用户在1个小时内将无法使用该 IP 再次发起调用，如公众号管理员多次拒绝该 IP 调用，该 IP 将可能长期无法发起调用。平台建议开发者在发起调用前主动与管理员沟通确认调用需求，或请求管理员开启 IP 白名单功能并将该 IP 加入 IP 白名单列表。

### user_access_token(用户级)@user_access_token

平台对应的值

|平台							|值						|描述																																																													|
|:-:							|:-:					|:-:																																																													|
|微信内置浏览器H5	|access_token	|微信内置浏览器H5用户会话密钥。[详情](https://developers.weixin.qq.com/doc/offiaccount/OA_Web_Apps/Wechat_webpage_authorization.html)	|

对应微信公众平台网页用户授权 `access_token`

微信公众平台网页授权有两个相同名字 `access_token`，分别用于

1、公众号的全局唯一接口调用凭据，公众号调用各接口时都需使用 `access_token`。
2、网页授权接口调用凭证，用户授权的作用域 `access_token`。

在微信内置浏览器H5无法区分两个相同名称值不同的 `access_token`，所以以更直观的名称 `user_access_token` 对应用户授权 `access_token`

### session_key

平台对应的值

|平台				|值					|描述																																																								|
|:-:				|:-:				|:-:																																																								|
|微信小程序	|session_key|微信小程序会话密钥。[详情](https://developers.weixin.qq.com/miniprogram/dev/OpenApiDoc/user-login/code2Session.html)	|

会话密钥 `session_key` 有效性

开发者如果遇到因为 `session_key` 不正确而校验签名失败或解密失败，请关注下面几个与 `session_key` 有关的注意事项。

`uni.login` 调用时，用户的 `session_key` 可能会被更新而致使旧 `session_key` 失效（刷新机制存在最短周期，如果同一个用户短时间内多次调用 `uni.login`，并非每次调用都导致 `session_key` 刷新）。

开发者应该在明确需要重新登录时才调用 `uni.login`，及时通过 `code2Session` 接口更新服务器存储的 `session_key`。

微信不会把 `session_key` 的有效期告知开发者。我们会根据用户使用小程序的行为对 `session_key` 进行续期。用户越频繁使用小程序，`session_key` 有效期越长。

开发者在 `session_key` 失效时，可以通过重新执行登录流程获取有效的 `session_key`。使用接口 `uni.checkSession` 可以校验 `session_key` 是否有效，从而避免小程序反复执行登录流程。

当开发者在实现自定义登录态时，可以考虑以 `session_key` 有效期作为自身登录态有效期，也可以实现自定义的时效性策略。

### encrypt_key

为了避免小程序与开发者后台通信时数据被截取和篡改，微信侧维护了一个用户维度的可靠key，用于小程序和后台通信时进行加密和签名。[详情](https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/user-encryptkey.html)

开发者可以分别通过小程序前端和微信后台提供的接口，获取用户的加密 key。

### ticket

`ticket` 是公众号用于调用微信 JS 接口的临时票据。正常情况下，`ticket` 的有效期为7200秒，通过 `access_token` 来获取。

由于获取 `ticket` 的 api 调用次数非常有限，频繁刷新 `ticket` 会导致 api 调用受限，影响自身业务，开发者必须在自己的服务全局缓存 `ticket `。[详情](https://developers.weixin.qq.com/doc/offiaccount/OA_Web_Apps/JS-SDK.html#62)