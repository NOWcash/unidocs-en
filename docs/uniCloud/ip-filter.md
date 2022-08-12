> 仅本地调试时需HBuilderX 3.5.4+。云端无版本限制，在uniCloud web控制台打开ip防刷即可

IP防刷功能旨在阻止某些ip的访问和防范短时间内大量相同ip请求导致云函数或数据库无法及时响应。

虽然uniCloud是serverless，云函数很难被打垮。但
1. 如果攻击者持续攻击运行耗时久的云函数，因云厂商根据GBS计费，会给开发者造成经济损失。需要在尽可能短的时间阻断云函数运行
2. 如果攻击访问大量数据库操作的云函数，会造成数据库整体性能下降，拖累正常用户对数据库的读写

不管是开发者被ddos攻击，还是因为发放奖励、促销或激励视频广告导致被刷单、刷激励，都应该开通`ip防刷`功能。

IP防刷包含两个子功能：
- IP黑名单：手动拉黑某些ip。
- IP访问频率控制：根据相同ip访问云函数的频次自动拉黑某些ip一段时间。

**注意**

- IP防刷功能相关的逻辑也是在云函数内执行的，因此在拒绝IP请求时也会消耗最小计费单元（配置的内存*100ms）的GBs

## 启用IP防刷功能

1. 服务空间内开通了redis
2. 在uniCloud web控制台左侧导航开启ip防刷：[uniCloud web控制台](https://unicloud.dcloud.net.cn/)

### 生效范围
在完成上2步的服务空间中，在如下范围内支持ip防刷：

1. 启用了redis扩展或jql扩展（jql扩展依赖了redis扩展）的云函数/云对象才会有防刷功能。未加载相关扩展库的云函数不生效。
2. clientDB，即客户端直接发起的数据库请求也生效。
3. 仅在客户端调用云函数/云对象时才会启用IP防刷功能。URL化、定时触发、云函数调用云函数均不触发此功能

需要redis的原因是被拉黑的IP需要存在redis内，其key为：`unicloud:ip-black-list:set`。
如果这些信息存在MongoDB中其实没有防刷的意义，而redis作为内存数据库，访问速度极快且不按照访问次数计费，是最佳方案。

## IP黑名单@ip-black-list

IP黑名单是用来完全阻止设定的IP或IP网段（cidr规范）访问云函数或clientDB的功能。

![black list](https://vkceyugu.cdn.bspapp.com/VKCEYUGU-f184e7c3-1912-41b2-b81f-435d1b37c7b4/7bf5e358-e627-4b3a-bafb-2b18d43c4d4b.jpg)

被封禁IP访问云函数及clientDB时会收到错误响应，错误码为：`ACCESS_DENIED`，错误信息为：`Access denied`

```js
// 云函数
const res = await uniCloud.callFunction({
  name: 'test',
  data: {}
})
// res.result = {
//   errCode: 'ACCESS_DENIED',
//   errMsg: 'Access denied'
// }

// 对于云对象而言，上述返回结果符合响应体规范因为会转化为错误抛出
const obj = uniCloud.importObject('obj')
try {
  const res = await obj.test()
} catch (e) {
  // e.errCode = 'ACCESS_DENIED'
  // e.errMsg = 'Access denied'
}
```

### IP网段规则

通常书写IPv4地址时会将IPv4地址写成由点分割的四段数字，每段取值范围为0-255。IP网段则是由IP加掩码位数组成的字符串，用于表示一个IP区间。

以`192.168.12.1/20`为例，要计算其表示的IP区间可以先将四段IP转为二进制（每段不足8位的往前补0）`11000000.10101000.00001100.00000001`，掩码位数20则表示经过此规则转化后的IP只要前20位和`192.168.12.1`转换后相同则此IP在`192.168.12.1/20`这个IP网段内。即IP区间为`11000000.10101000.00000000.00000000`(192.168.0.0) - `11000000.10101000.00001111.11111111`(192.168.15.255)

### 黑名单用到的Redis key

开发者配置的黑名单会以Set类型存储在redis内，其key为：`unicloud:ip-black-list:set`

### 注意事项

- 切换开关状态会更新所有依赖或间接依赖redis扩展的云函数及clientDB
- 一个区域内的多个用户可能拥有同一IP

## IP访问频率控制@ip-freq

IP访问频率控制用于限制单个IP访问云函数的频率。如图所示，开发者可以配置`${duration}秒内请求超过${limit}次，则将会临时封禁${blockTime}秒`。

就客户端体验来说这个配置表示，**任意连续**duration秒内访问均不可超过limit次，否则将会临时封禁blockTime秒。对于有相关开发经验的开发者来说应该很容易看出这就是一个漏桶算法的实现。

- blockTime配置为0时超出限制也不会进行封禁，只是拒绝请求。
- duration或limit配置为0时将不再限制访问频率，但是已被临时封禁的用户依然需要等到解封后才可以访问

![frequency limit](https://vkceyugu.cdn.bspapp.com/VKCEYUGU-f184e7c3-1912-41b2-b81f-435d1b37c7b4/76130f29-7c64-4406-af69-a3759e264726.jpg)

访问频率过高的用户及由于访问频率过高被临时封禁的用户访问云函数及clientDB时会收到错误响应，错误码为：`OPERATION_TOO_FREQUENT`，错误信息为：`Operation is too frequent, please try again later`

```js
// 云函数
const res = await uniCloud.callFunction({
  name: 'test',
  data: {}
})
// res.result = {
//   errCode: 'OPERATION_TOO_FREQUENT',
//   errMsg: 'Operation is too frequent, please try again later'
// }

// 对于云对象而言，上述返回结果符合响应体规范因为会转化为错误抛出
const obj = uniCloud.importObject('obj')
try {
  const res = await obj.test()
} catch (e) {
  // e.errCode = 'OPERATION_TOO_FREQUENT'
  // e.errMsg = 'Operation is too frequent, please try again later'
}
```

### IP访问频率控制用到的Redis key

**访问频率控制配置**

开发者配置的duration、limit、blockTime三个参数以hash类型存储在redis内，key为：`unicloud:ip-freq-config:hash`。

结构如下：

```js
{
	"duration": 10, // 单位秒
	"limit": 10, // 10（duration）秒内允许访问10次
	"blockTime": 1800 // 超限后封禁1800秒
}
```

**IP频率控制信息**

IP频率控制信息的以hash类型存储在redis内，key为：`unicloud:ip-info:${ip}:hash`其中${ip}表示客户端的ip

结构示例如下：

```js
{
	"bucket": 20, // 剩余访问次数，最大为配置的limit，最小为 0，以上面的访问频率控制配置为例
	"lastTime": 1656399171851 // 上次剩余访问次数变动的时间
}
```

**临时封禁信息**

临时封禁信息以string类型存储在redis内，key为：`unicloud:ip-blocked:${ip}:string`其中${ip}表示客户端的ip

其值为临时封禁开始的时间戳

### 注意事项

- 切换开关状态会更新所有依赖或间接依赖redis扩展的云函数及clientDB
- 一个区域内的多个用户可能拥有同一IP
- 本地调试期间如果开启或关闭了IP防刷功能，应停止所有客户端等待5秒重新运行才可生效