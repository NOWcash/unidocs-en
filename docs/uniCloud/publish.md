本地开发调试后，务必上传到uniCloud服务空间才能在现网生效。

发行分为云端资源发行和客户端发行。

## 云资源发行

各种云函数、DB Schema，都需要上传发行。

HBuilderX有多种发行方式
- 发行菜单
- 对uniCloud目录中各种文件点右键上传。快捷键是【Ctrl+u】
- 对uniCloud目录点右键，启动 uniCloud服务空间初始化向导

### 小程序中使用uniCloud的白名单配置@useinmp

各家小程序平台，均要求在小程序管理后台配置小程序应用的联网服务器域名，否则无法联网。

使用uniCloud后，开发者将不再需要自己购买、备案域名，直接将uniCloud的域名填写在小程序管理后台即可。（如需使用前端网页托管仍需进行域名备案）

根据下表，在小程序管理后台设置request合法域名、uploadFile合法域名（如没有上传文件业务，可不设置）。下表的域名均为阿里云或腾讯云自有域名，并非DCloud所属域名。

|服务提供商	|request合法域名			|uploadFile合法域名					|download合法域名|
|:-:		|:-:						|:-:								|:-:|
|阿里云		|api.bspapp.com				|bsppub.oss-cn-shanghai.aliyuncs.com|需要从云存储下载文件的时候才需要配置，不同服务空间域名不同，可以在web控制台查看文件详情里面看到|
|腾讯云		|tcb-api.tencentcloudapi.com|cos.ap-shanghai.myqcloud.com		|需要从云存储下载文件的时候才需要配置，不同服务空间域名不同，可以在web控制台查看文件详情里面看到|

**如果需要用uni.request请求云存储内的文件，需要将云存储域名（即上表中的download合法域名）配置到request合法域名内**

小程序开发工具的真机预览功能，必须添加上述域名白名单，否则无法调用云函数。模拟器的PC端预览、真机调试不受此影响。

如果遇到正确配置了合法域名但是依然报`url not in domain list`，请尝试删除手机上的小程序、清理小程序所在的客户端缓存、重启对应的小程序开发工具后重试

如果遇到`invalid ip xxx, not in whitelist`，请检查是否在小程序管理后台开启了域名白名单。如果没用到可以关闭，如果确认需要使用ip白名单，请开通腾讯云收费空间并使用[固定IP](uniCloud/cf-functions.md?id=eip)功能

**关于云函数本地调试服务在小程序中的使用**

HBuilderX内使用运行菜单运行到小程序时会连接本地调试服务，即使你运行之前就选择了连接云端云函数，小程序也会发送一条请求到本地调试服务检测调用云函数是本地还是云端。

**在开发模式下推荐直接忽略域名校验。**

即使在开发工具勾选了忽略域名校验，体验版与正式版不会忽略域名校验。**如果要发布`体验版`或`正式版`，请务必在HBuilderX内使用发行菜单。**

### H5中使用uniCloud的跨域处理@useinh5

H5前端js访问云函数，涉及跨域问题，导致前端js无法连接云函数服务器。处理方式如下：。

- 运行到H5端时，使用HBuilderX内置浏览器，可以忽略跨域问题（需 HBuilderX 2.5.10+）。
- 发行到H5端时，需要在uniCloud后台操作，绑定安全域名（在部署云函数的服务空间配置部署h5的域名作为安全域名），否则会因为跨域问题而无法访问。（在`cloudfunctions`目录右键可打开uniCloud后台）

> 注意跨域配置需要带上端口信息。例如：前端页面运行于：www.xxx.com:5001，跨域配置内配置：www.xxx.com不会对此页面生效，需要配置为：www.xxx.com:5001

**uniCloud后台跨域配置：**

<div align=center>
  <img src="https://img.cdn.aliyun.dcloud.net.cn/uni-app/uniCloud/uniCloud-add-domain.png"/>
</div>

- 如果运行时，想使用外部浏览器运行，方案如下：
  * 方式1：在uniCloud web控制台绑定测试期的地址为安全域名，如配置：localhost:8080、192.168.0.1:8080（建议直接使用内置浏览器测试）
  * 方式2：在外部浏览器安装跨域插件，详见：[https://ask.dcloud.net.cn/article/35267](https://ask.dcloud.net.cn/article/35267)。要跨域的地址，详见上述文档中小程序配置安全域名章节。

**注意**

`2021年9月16日`之前阿里云跨域配置不对云存储及前端网页托管生效，表现为云存储中图片绘制到canvas会[污染画布](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Tutorial/Using_images#Using_other_canvas_elements)，前端网页托管的网页不可在iframe中使用。

`2021年9月16日`之后阿里云跨域配置可以对前端网页托管生效，**仅对前端网页托管的自定义域名生效，不对默认域名生效，如何绑定自定义域名请参考：[前端网页托管绑定自定义域名](uniCloud/hosting.md?id=domain)**，设置之后可能需要几分钟才会生效。如果你在之前已经设置了跨域域名和前端网页托管的自定义域名，需要重新设置一次跨域域名才能生效。

## 客户端资源发行

### 前端网页托管

uniCloud支持前端静态网页托管，在HBuilderX中点发行菜单，生成H5，将生成的前端文件部署在uniCloud的前端网页托管内即可[详情参考](uniCloud/hosting.md)。

需要注意的是你仍在[uniCloud web控制台](https://unicloud.dcloud.net.cn) 配置H5安全域名。

### App升级中心

uniCloud通过云端一体的升级检测、管理端版本维护。[详见](upgrade-center.md)

### 应用统一发布页

app、小程序、web统一发布页面。[详见](uni-publish.md)

## cli发行

规模化的开发时，经常需要通过命令行发行，做持续集成。

HBuilderX提供了cli，[详见](https://hx.dcloud.net.cn/cli/README)