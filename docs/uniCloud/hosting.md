## 简介
## Introduction

DCloud为开发者提供了`uni发布平台`，包括网站发布、App发布和统一门户页面。
DCloud provides developers with a `uni publishing platform`, including website publishing, App publishing and unified portal pages.

`前端网页托管`是其中的网页发布环节产品。
`Front-end web hosting` is one of the web publishing products.

`前端网页托管`基于uniCloud的能力，为开发者的html网页提供**更快速、更安全、更省心、更便宜**的网站发布。
`Front-end web hosting` is based on the ability of uniCloud, which provides **faster, safer, more worry-free and cheaper** website publishing for developers' html webpages.

- 更快速：不经过web server，页面和资源直接上cdn，就近访问，速度更快。
- Faster: pages and resources can be accessed directly on the CDN without going through the web server, and the speed is faster.
- 更安全：不存在传统服务器各种操作系统、web server的漏洞，不用天天想着打补丁。不怕DDoS攻击，永远打不垮的服务。
- More secure: There are no loopholes in various operating systems and web servers of traditional servers, so you don't need to think about patching every day. A service that is not afraid of DDoS attacks and will never be defeated.
- 更省心：无需再购买虚拟机、安装操作系统、配置web服务器、处理负载均衡、处理大并发、处理DDoS攻击......您什么都不用管，只需上传您写的页面文件
- More peace of mind: no need to buy a virtual machine, install an operating system, configure a web server, handle load balancing, handle large concurrency, handle DDoS attacks... You don't have to worry about anything, just upload the page file you write
- 更便宜：uniCloud由DCloud联合阿里云和腾讯云推出，享受云厂商政策优惠。
- Cheaper: uniCloud is launched by DCloud in conjunction with Alibaba Cloud and Tencent Cloud, and enjoys preferential policies from cloud manufacturers.

## 案例
## case

- `HBuilderX`文档网站，是一个基于`markdown`的文档系统，域名：[https://hx.dcloud.net.cn/](https://hx.dcloud.net.cn/)
- `HBuilderX` documentation website, is a `markdown`-based documentation system, domain name: [https://hx.dcloud.net.cn/](https://hx.dcloud.net.cn/)
- `uni统计`官网现已部署到uniCloud，一份报表，掌握业务全景，域名：[https://tongji.dcloud.net.cn](https://tongji.dcloud.net.cn)
- `uni statistics` official website has been deployed to uniCloud, a report, mastering the business panorama, domain name: [https://tongji.dcloud.net.cn](https://tongji.dcloud.net.cn)
- `hello uni-app`项目现已部署到uniCloud，线上地址：[https://hellouniapp.dcloud.net.cn](https://hellouniapp.dcloud.net.cn)
- The `hello uni-app` project has been deployed to uniCloud, online address: [https://hellouniapp.dcloud.net.cn](https://hellouniapp.dcloud.net.cn)

## 开通
## open

首先开发者需要开通`uniCloud`，登录[https://unicloud.dcloud.net.cn/](https://unicloud.dcloud.net.cn/)。
First, developers need to activate `uniCloud` and log in to [https://unicloud.dcloud.net.cn/](https://unicloud.dcloud.net.cn/).

然后选择或创建一个服务空间。
Then select or create a service space.

最后在上述网页左侧导航点击`前端网页托管`，即可开始使用。
Finally, navigate to the left side of the above webpage and click `Front-end Web Hosting` to get started.

`前端网页托管`和云函数没有绑定关系，可以和云函数部署在一个服务空间，也可以是不同的空间，甚至是不同云服务商的空间。
`Front-end web hosting` has no binding relationship with cloud functions. It can be deployed in the same service space with cloud functions, or in a different space, or even in the space of different cloud service providers.

- 阿里云`前端网页托管`免费。
- Alibaba Cloud `Front-end web hosting` is free.
- 腾讯云`前端网页托管`需付费开通，定价由腾讯云提供。由于腾讯云新计费已上线，新计费模式下前端网页托管仅支持按量计费模式，原包年包月套餐已下线。
- Tencent Cloud `Front-end web hosting` needs to be activated for a fee, and the pricing is provided by Tencent Cloud. Since Tencent Cloud's new billing has been launched, the front-end web hosting under the new billing model only supports the pay-as-you-go billing model, and the original annual and monthly package has been offline.

现存包年包月`前端网页托管`，如果服务空间升级到新套餐，则`前端网页托管`会自动切换为按量计费模式，请确保余额充足。
Existing annual and monthly `Front-end web hosting`, if the service space is upgraded to a new package, the `Front-end web hosting` will automatically switch to the pay-as-you-go model, please ensure that the balance is sufficient.


## 使用
## use

开通后，需要把开发者的前端网页，上传到uniCloud的`前端网页托管`中。
After activation, you need to upload the developer's front-end web page to the `front-end web page hosting` of uniCloud.

目前提供了2种方式操作：
There are currently 2 ways to operate:

方式1. 通过[uniCloud控制台](https://unicloud.dcloud.net.cn/)，在web界面上传。
Method 1. Through the [uniCloud console](https://unicloud.dcloud.net.cn/), upload on the web interface.

  上传时，可以按文件上传，也可以按文件夹上传。
  When uploading, you can upload by file or by folder.

  如果是按文件夹上传，可以选择上传后的目录是否包含上传文件夹的根目录。
  If uploading by folder, you can choose whether the uploaded directory contains the root directory of the uploaded folder.

![](https://img.cdn.aliyun.dcloud.net.cn/uni-app/uniCloud/unicloud-web-hosting.jpg)

方式2. 通过HBuilderX工具上传。
Method 2. Upload through HBuilderX tool.

  > HBuilderX 2.8+起，支持在HBuilderX中直接上传前端网页到uniCloud阿里云版；3.5.1起，支持uniCloud腾讯云版。
  > From HBuilderX 2.8+, it supports uploading front-end web pages to uniCloud Alibaba Cloud Edition directly in HBuilderX; from 3.5.1, supports uniCloud Tencent Cloud Edition.

  在菜单发行中，选择`上传网站到服务器`。
  In the menu distribution, select 'Upload Website to Server'.

  - 对于uni-app项目，可以先编译为h5，然后直接把编译后的h5上传上去。如下图
  - For the uni-app project, you can compile it to h5 first, and then upload the compiled h5 directly. As shown below

![](https://img.cdn.aliyun.dcloud.net.cn/uni-app/uniCloud/unicloud-hx-hosting.jpg)

  - 对于非uni-app项目，可以自己选择要上传的目录，包含html、js、css、图片等静态前端文件接口。如下图
  - For non-uni-app projects, you can choose the directory to upload, including static front-end file interfaces such as html, js, css, and pictures. As shown below

![](https://img.cdn.aliyun.dcloud.net.cn/uni-app/uniCloud/unicloud-hx-hosting-h5.jpg)

  > HBuilderX 2.8.9+，支持前端网页托管管理器管理uniCloud阿里云版，3.5.1起，支持uniCloud腾讯云版。
  > HBuilderX 2.8.9+, supports front-end web hosting manager to manage uniCloud Alibaba Cloud Edition, from 3.5.1, supports uniCloud Tencent Cloud Edition.

  在菜单视图中，或者在左下角状态栏中，点击`前端网页托管`，可在左侧打开前端网页托管管理器。如下图
  In the menu view, or in the status bar in the lower left corner, click `Frontend Web Hosting` to open the Frontend Web Hosting Manager on the left. As shown below
  
<img style="max-width:750px;" src="https://vkceyugu.cdn.bspapp.com/VKCEYUGU-f184e7c3-1912-41b2-b81f-435d1b37c7b4/aa6a801a-3fbc-441d-98ce-156ccb221f3e.jpg"/>


  在前端网页托管管理器中，可以看到当前用户的服务空间列表，置灰表示该服务空间还没有开通前端网页托管，点击后可根据提示开通。（如上图中置灰的ali1服务空间）。
  In the front-end web hosting manager, you can see the list of the current user's service space. If it is grayed out, it means that the front-end web hosting has not been activated for the service space. After clicking, you can activate it according to the prompts. (As shown in the grayed out ali1 service space in the above figure).

  点击可用的服务空间，在右侧可以看到远端的资源管理器，把本地文件拖进入，即可上传文件。
  Click the available service space, you can see the remote resource manager on the right, drag the local file into it, and then upload the file.

**注意事项**
**Precautions**

1. `前端网页托管`适于uni-app的h5页面发布。尤其是配搭uniCloud云开发，将彻底不用再租用任何传统的服务器。
1. `Front-end web hosting` is suitable for publishing h5 pages of uni-app. Especially with uniCloud cloud development, there will be no need to rent any traditional servers.
2. `前端网页托管`适于所有前后端分离的网站中的前端页面发布，包括pc网页。
2. `Front-end web hosting` is suitable for publishing front-end pages in all websites with front-end and back-end separation, including pc web pages.
3. 仅支持html、CSS、JavaScript、字体、图片、音视频、json等文件。不支持php、java、python、ruby、go、c++等其他需要额外语言解释器解释的语言文件。
3. Only supports html, CSS, JavaScript, fonts, pictures, audio and video, json and other files. It does not support php, java, python, ruby, go, c++ and other language files that require additional language interpreters to be interpreted.
4. 如果开发者需要做a/b test或灰度新功能，需要自己在js里写代码实现，不能通过路由到不同服务器实现。
4. If developers need to do a/b tests or new grayscale functions, they need to write code in js to implement them, and they cannot be implemented by routing to different servers.
5. uni-app项目编译为h5时，在项目的manifest中配置二级目录。上传时无需重复设置二级目录。
5. When the uni-app project is compiled to h5, configure the secondary directory in the manifest of the project. There is no need to repeatedly set the secondary directory when uploading.
6. 一个`前端网页托管`的空间里，可以上传多个网站，用不同目录区分开，访问时使用同一个域名后加不同目录的方式访问。不支持每个目录单独设置不同域名。
6. In a `front-end web hosting` space, you can upload multiple websites, separate them with different directories, and use the same domain name followed by different directories to access. Different domain names are not supported for each directory.
7. 部署到不同的服务空间的`前端网页托管`内的网站，也是可以访问同一个服务空间内的云函数的，只需要在部署云函数的服务空间的`跨域配置`内添加部署前端页面的域名即可
7. Websites in `Front-end web hosting` deployed to different service spaces can also access cloud functions in the same service space. You only need to add the deployment front-end in the `cross-domain configuration` of the service space where cloud functions are deployed. the domain name of the page

## 基础配置@base-config
## Basic configuration @base-config

本章节介绍`前端网页托管`提供的各种配置项目说明。其中配置域名、网站首页、404页面，是阿里云和腾讯云均支持的，其他配置仅腾讯云支持。
This chapter introduces the description of various configuration items provided by `Frontend Web Hosting`. The configuration of the domain name, website home page, and 404 page is supported by both Alibaba Cloud and Tencent Cloud. Other configurations are only supported by Tencent Cloud.

### 配置域名@domain
### Configure the domain name @domain

`前端网页托管`，自带一个测试域名，仅用于产品体验及测试可快速体验前端网页部署的完整流程，该域名有如下限制：
`Front-end web hosting` comes with a test domain name, which is only used for product experience and testing. You can quickly experience the complete process of front-end web page deployment. This domain name has the following limitations:
  + 阿里云每分钟最多60次请求，默认每日仅允许10个公网IP访问，超出部分，需通过手动方式将来源IP加入白名单,IP白名单也会有数量限制
  + Alibaba Cloud has a maximum of 60 requests per minute. By default, only 10 public IPs are allowed to access each day. For the excess, you need to manually add the source IP to the whitelist, and the number of IP whitelists will also be limited.
  + 腾讯云限速100K/s
  + Tencent Cloud speed limit is 100K/s

业务如要上线商用，请配置自己的正式域名，配置自己的正式域名后，将不受上述测试域名的限制。（尤其注意阿里云测试域名是公共的，任意一个服务空间如果有上传恶意文件被投诉，会导致测试域名被微信内置浏览器整体禁封）
If the business is to be launched for commercial use, please configure your own official domain name. After configuring your own official domain name, it will not be restricted by the above test domain name. (Especially note that the Alibaba Cloud test domain name is public. If any service space is complained about uploading malicious files, the test domain name will be banned by the WeChat built-in browser as a whole.)


前端网页托管配置自己域名的步骤如下：
The steps to configure your own domain name for front-end web hosting are as follows:

1、登录[uniCloud控制台](https://unicloud.dcloud.net.cn/)。
1、 Log in to the [uniCloud console](https://unicloud.dcloud.net.cn/).
2、进入前端网页托管页面，选择【基础设置】，单击【添加域名】，进行域名添加，（注意：域名是需要自行购买的）如下图所示：
2、 Enter the front-end web hosting page, select [Basic Settings], and click [Add Domain Name] to add a domain name. (Note: the domain name needs to be purchased by yourself) as shown in the following figure:

 ![](https://img-cdn-aliyun.dcloud.net.cn/uni-app/uniCloud/uniCloud-hosting-domain-add.jpg)

3、添加后，系统会自动分配一个 CNAME 域名，CNAME 域名不能直接访问，您需要在域名服务提供商处完成 CNAME 配置（将添加的域名CNAME到此域名），配置生效后，新域名即可使用。
3、 After adding, the system will automatically assign a CNAME domain name. The CNAME domain name cannot be accessed directly. You need to complete the CNAME configuration at the domain name service provider (CNAME the added domain name to this domain name). After the configuration takes effect, the new domain name can be used. .

阿里云现已支持http强制跳转https，在上述添加界面打开对应开关即可
Alibaba Cloud now supports http forcibly redirecting to https, and you can turn on the corresponding switch in the above add interface.

**域名备案**
**Domain name registration**

如果你已经有备案过的域名，直接解析过来即可；如果你要新注册域名，首先自行在网上购买，然后注意域名如果想在国内正常绑定阿里云或腾讯云，需要域名备案。这里的备案流程和传统云主机略有不同，涉及一个uniCloud没有固定ip的问题。此时可以去买花生壳的备案服务；也可以临时买一个短期传统云，走传统备案；还有授权码方案，这里有开发者分享的经验贴：[https://ask.dcloud.net.cn/article/38116](https://ask.dcloud.net.cn/article/38116)
If you already have a registered domain name, you can directly resolve it; if you want to register a new domain name, first buy it online, and then note that if you want to normally bind the domain name to Alibaba Cloud or Tencent Cloud in China, you need domain name registration. The filing process here is slightly different from traditional cloud hosting, involving a problem that uniCloud does not have a fixed IP. At this time, you can buy the filing service of peanut shells; you can also temporarily buy a short-term traditional cloud and go for traditional filing; there is also an authorization code scheme, here are the experience shared by developers: [https://ask.dcloud.net. cn/article/38116](https://ask.dcloud.net.cn/article/38116)

**关于证书内容与私钥**
**About certificate content and private key**

域名如果使用https，则需要证书。证书签发后，可下载到本地，然后将内容复制黏贴到uniCloud web控制台。
If the domain name uses https, a certificate is required. After the certificate is issued, you can download it locally, and then copy and paste the content to the uniCloud web console.

注意：各运营商下载证书的后缀可能不同，一般来说，`.key`文件对应私钥，`.pem`或`.crt`文件对应证书。这几种类型文件都是文本内容，可选择记事本打开查看内容。
Note: The suffix of the downloaded certificate may be different for each operator. Generally speaking, the `.key` file corresponds to the private key, and the `.pem` or `.crt` file corresponds to the certificate. These types of files are all text content, you can select Notepad to open and view the content.

如果您还没有SSL证书，点此[快速获取](https://cloud.tencent.com/act/cps/redirect?redirect=33848&cps_key=c858f748f10419214b870236b5bb94c6)。
If you don't have an SSL certificate, click here [Quick Get](https://cloud.tencent.com/act/cps/redirect?redirect=33848&cps_key=c858f748f10419214b870236b5bb94c6).

**注意事项**
**Precautions**

- 在阿里云开启了泛域名加速的情况下，对应的子域名可能无法配置到前端网页托管，**这种情况下可能会提示：该域名已被添加过，不能重复添加**
- When Alibaba Cloud has enabled pan-domain acceleration, the corresponding sub-domain name may not be configured for front-end web hosting. **In this case, it may prompt: The domain name has already been added and cannot be added again**
- 暂不支持绑定中文域名
- Currently does not support binding Chinese domain names
- 阿里云要求必须有一个备案在阿里才可以绑定，按照uniCloud web控制台提示操作即可，腾讯云没有此条限制。
- Alibaba Cloud requires that there must be a record in Alibaba before it can be bound. Just follow the prompts in the uniCloud web console. Tencent Cloud does not have this restriction.

**务必注意，如果你是在腾讯购买并备案的域名需要保留一个到腾讯ip的解析，否则备案会被撤销，阿里云同理。具体细节可以咨询购买域名的云厂商**
**It is important to note that if you purchased and filed a domain name in Tencent, you need to keep a resolution to Tencent IP, otherwise the record will be revoked, and Alibaba Cloud is the same. For details, please consult the cloud vendor that purchased the domain name**

### 路由规则@routing
### Routing rules @routing

**网站首页**
**Home page**

设置网站首页文档名
Set the website homepage document name

**404页面**
**404 page**

访问静态网站出错后返回的页面。
The page returned after an error occurs when accessing a static website.

**history模式路径**
**history mode path**

> 仅阿里云支持
> Only supported by Alibaba Cloud

为指定目录开启`uni-app history`模式支持，此路径下无法访问的文件会被重定向到此路径下的`index.html`, 并返回`200`状态码
Enable `uni-app history` mode support for the specified directory, inaccessible files in this path will be redirected to `index.html` in this path, and return `200` status code

**重定向规则**
**Redirection Rules**

> 仅腾讯云支持
> Only supported by Tencent Cloud

支持以下三种组合配置
The following three combination configurations are supported

- 类型：错误码、规则：替换路径。将特定错误码的请求重定向到目标文档，仅支持对4xx错误码。
- Type: Error code, Rule: Replacement path. Redirects requests for specific error codes to the target document, only supports 4xx error codes.

例：将404错误码重定向至index.html，需做如下配置（uni-app项目使用history模式发行到h5时可以使用此配置）：
Example: To redirect the 404 error code to index.html, the following configuration is required (this configuration can be used when the uni-app project uses the history mode to release to h5):

|类型		|描述	|规则			|替换内容		|
|Type |Description |Rules |Replace Content |
|:-:		|:-:	|:-:			|:-:				|
|错误码	|404	|替换路径	|index.html	|
|Error Code |404 |Replace Path |index.html |

- 类型：前缀匹配、规则：替换路径。将匹配到特定前缀的请求重定向到目标文档
- Type: Prefix Match, Rule: Replace Path. Redirect requests matching a specific prefix to the target document

例：当您删除了images/文件夹（即删除了具有前缀images/的所有对象）。您可以添加重定向规则，将具有前缀images/的任何对象的请求重定向至test.html页面。
Example: When you delete the images/ folder (ie delete all objects with the prefix images/). You can add redirect rules to redirect requests for any object with the prefix images/ to the test.html page.

|类型			|描述		|规则			|替换内容	|
|Type |Description |Rules |Replace Content |
|:-:			|:-:		|:-:			|:-:			|
|前缀匹配	|images/|替换路径	|test.html|
|Prefix match |images/|Replace path |test.html|

- 类型：前缀匹配、规则：替换前缀。将匹配到特定前缀的请求中的前缀替换为替换内容，例：
- Type: prefix match, rule: replace prefix. Replace the prefix in the request matching a specific prefix with the replacement content, for example:

例：当您将文件夹从docs/重命名为documents/后，用户在访问docs/文件夹会产生错误。所以，您可以将前缀docs/的请求重定向至documents/。
Example: When you rename the folder from docs/ to documents/, users will get an error when accessing the docs/ folder. So, you can redirect requests prefixed with docs/ to documents/.

|类型			|描述	|规则			|替换内容		|
|Type |Description |Rules |Replace Content |
|:-:			|:-:	|:-:			|:-:				|
|前缀匹配	|docs/|替换前缀	|documents/	|
|Prefix match |docs/|Replace prefix |documents/ |

**注意**
**Notice**

- 阿里云每天仅能修改3次路由规则
- Alibaba Cloud can only modify routing rules 3 times a day

### 缓存配置@cache
### Cache configuration @cache

> 仅腾讯云支持
> Only supported by Tencent Cloud

- 文件类型：根据填入的文件后缀进行缓存过期时间设置，格式为.jpg形式，不同后缀之间用;间隔。
- File type: Set the cache expiration time according to the file suffix filled in. The format is .jpg, and the interval is used between different suffixes.
- 文件夹：根据填入的目录路径进行缓存过期时间设置，格式为/test形式，无需以/结尾，不同目录之间用;间隔。
- Folder: Set the cache expiration time according to the directory path filled in. The format is /test, no need to end with /, and the interval between different directories is used.
- 全路径文件：指定完整的文件路径进行缓存过期时间设置，格式为/index.html，支持完整路径加文件类型匹配模式，如/test/*.jpg。
- Full path file: Specify the complete file path to set the cache expiration time, the format is /index.html, and the full path plus file type matching pattern is supported, such as /test/*.jpg.

**注意**
**Notice**

- 缓存过期规则最多可配置10条。
- Up to 10 cache expiration rules can be configured.
- 多条缓存过期规则之间的优先级为底部优先。
- The priority among multiple cache expiration rules is bottom priority.
- 缓存过期时间最多可设置365天。
- The cache expiration time can be set up to 365 days.

### 防盗链配置@referer
### Anti-leech configuration @referer

> 仅腾讯云支持
> Only supported by Tencent Cloud

**referer 黑名单：**
**referer blacklist:**

- 若请求的 referer 字段匹配黑名单内设置的内容，CDN 节点拒绝返回该请求信息，直接返回403状态码。
- If the referer field of the request matches the content set in the blacklist, the CDN node refuses to return the request information and directly returns the 403 status code.
- 若请求的 referer 不匹配黑名单内设置的内容，则 CDN 节点正常返回请求信息。
- If the requested referer does not match the content set in the blacklist, the CDN node returns the request information normally.
- 当勾选包含空 referer 选项时，此时若请求 referer 字段为空或无 referer 字段（如浏览器请求），则 CDN 节点拒绝返回该请求信息，返回403状态码。
- When the Include empty referer option is checked, if the request referer field is empty or has no referer field (such as a browser request), the CDN node refuses to return the request information and returns a 403 status code.

**referer白名单：**
**Referer whitelist:**

- 若请求的 referer 字段匹配白名单设置的内容，则 CDN 节点正常返回请求信息。
- If the referer field of the request matches the content set in the whitelist, the CDN node returns the request information normally.
- 若请求的 referer 字段不匹配白名单设置的内容，则 CDN 节点拒绝返回该请求信息，会直接返回状态码403。
- If the referer field of the request does not match the content set in the whitelist, the CDN node refuses to return the request information and directly returns the status code 403.
- 当设置白名单时，CDN 节点只能返回符合该白名单内字符串内容的请求。
- When a whitelist is set, the CDN node can only return requests that match the string content in the whitelist.
- 当勾选包含空 referer 选项时，此时若请求 referer 字段为空或无 referer 字段（如浏览器请求），则 CDN 正常返回请求信息。
- When the option Include an empty referer is checked, if the referer field of the request is empty or has no referer field (such as a browser request), the CDN will normally return the request information.

**配置规则：**
**Configuration rules:**

防盗链支持域名 / IP 规则，匹配方式为前缀匹配（仅支持路径情况下，域名的前缀匹配不支持），即假设配置名单为www.abc.com，则www.abc.com/123匹配，www.abc.com.cn不匹配；假设配置名单为127.0.0.1，则127.0.0.1/123也会匹配。
Anti-leech supports domain name/IP rules, and the matching method is prefix matching (if only paths are supported, domain name prefix matching is not supported), that is, if the configuration list is www.abc.com, then www.abc.com/123 matches, www.abc.com .abc.com.cn does not match; assuming the configuration list is 127.0.0.1, 127.0.0.1/123 will also match.
防盗链支持通配符匹配，即假设名单为*.qq.com，则www.qq.com、a.qq.com均会匹配。
Anti-leech supports wildcard matching, that is, if the list is *.qq.com, both www.qq.com and a.qq.com will match.

### IP黑白名单配置@ip-filter
### IP black and white list configuration @ip-filter

> 仅腾讯云支持
> Only supported by Tencent Cloud

**IP 黑名单**
**IP Blacklist**

用户端 IP 匹配黑名单中的 IP 或 IP 段时 ，访问 CDN 节点时将直接返回403状态码。
When the client IP matches the IP or IP segment in the blacklist, the 403 status code will be returned directly when accessing the CDN node.

**IP 白名单**
**IP whitelist**

用户端 IP 未匹配白名单中的 IP 或 IP 段时 ，访问 CDN 节点时将直接返回403状态码。
When the client IP does not match the IP or IP range in the whitelist, the 403 status code will be directly returned when accessing the CDN node.

**名单规则**
**List Rules**

- IP 黑名单与 IP 白名单二选一，不可同时配置。
- IP blacklist and IP whitelist can be selected. They cannot be configured at the same time.
- IP 段仅支持 /8、/16、/24 网段，不支持其他网段。
- The IP segment only supports /8, /16, /24 network segments, other network segments are not supported.
- 不支持IP：端口形式的黑白名单
- Does not support IP: port form black and white list
- 名单最多可输入50个。
- Up to 50 lists can be entered.

### 默认域名IP白名单@default-domain-ip-whitelist
### Default domain IP whitelist @default-domain-ip-whitelist

> 仅阿里云支持
> Only supported by Alibaba Cloud

为保障默认域名不被滥用，阿里云对默认域名做出了如下限制：每天前10个IP可以直接访问，超出10个IP后需要配置IP白名单才可以访问
In order to protect the default domain name from being abused, Alibaba Cloud imposes the following restrictions on the default domain name: the first 10 IPs can be accessed directly every day, and an IP whitelist needs to be configured to access after exceeding 10 IPs.

仅支持配置ipv4，可以配置IP或者IP网段，掩码位数取值范围24-31。最多可同时配置三个，多个之间用逗号隔开，如：123.120.5.235/24,123.123.123.123
Only supports the configuration of ipv4, you can configure the IP or IP network segment, and the value of the mask bits ranges from 24 to 31. Up to three can be configured at the same time, separated by commas, such as: 123.120.5.235/24,123.123.123.123

### IP访问限频配置@ip-freq
### IP access frequency limit configuration @ip-freq

> 仅腾讯云支持
> Only supported by Tencent Cloud

**配置说明**
**Configuration instructions**

- 配置开启后，超出 QPS 限制的请求会直接返回514，设置较低频次限制可能会影响您的正常高频用户的使用，请根据业务情况、使用场景合理设置阈值。
- After the configuration is enabled, requests that exceed the QPS limit will directly return 514. Setting a lower frequency limit may affect the use of your normal high-frequency users. Please set the threshold reasonably according to the business situation and usage scenario.
- 限频仅针对与单 IP 单节点访问次数进行约束，若恶意用户海量 IP 针对性的进行全网节点攻击，则通过此功能无法进行有效控制。
- The frequency limit is only limited to the number of visits to a single IP and a single node. If malicious users target a large number of IPs to attack the entire network node, this function cannot be effectively controlled.

## 跨域
## cross domain

web浏览器有跨域限制，A域名的网站如果通过js请求另一个域名B，且另一个B域名并没有放开跨域策略，那么浏览器就会报跨域错误。
Web browsers have cross-domain restrictions. If a website with domain A requests another domain name B through js, and the other domain name B does not release the cross-domain policy, the browser will report a cross-domain error.

在前端网页托管里，托管前端网页的网站就是A域名。要连接的服务器接口就是B域名。
In front-end web hosting, the website hosting the front-end web page is the A domain name. The server interface to be connected is the B domain name.

1. B域名是uniCloud的云函数/云对象
1. Domain B is a cloud function/cloud object of uniCloud

也就是业务后台也在uniCloud的云函数或云对象上。此时需要在uniCloud的[web控制台](https://unicloud.dcloud.net.cn/)的`跨域配置`中，把A域名填写在Web安全域名中。
That is, the business background is also on the cloud function or cloud object of uniCloud. At this time, you need to fill in the A domain name in the web security domain name in the `cross-domain configuration` of uniCloud's [web console](https://unicloud.dcloud.net.cn/).

2. B域名是开发者自己的传统服务器
2. Domain B is the developer's own traditional server

需要在开发者自己的传统服务器上配置跨域，允许A域名跨域访问自己。
You need to configure cross-domain on the developer's own traditional server to allow A domain name to access itself across domains.

## 最佳实践
## Best Practices

### 部署uni-app项目@host-uni-app
### Deploy uni-app project @host-uni-app

uni-app项目根据路由模式不同需要做不同的配置
The uni-app project needs to be configured differently depending on the routing mode

- 使用hash模式时，无需特别的配置即可正常使用
- When using hash mode, it can be used normally without special configuration

- 使用history模式时可以配置如下规则
- When using history mode, the following rules can be configured

  + 腾讯云配置重定向规则将404错误码重定向至`index.html`
  + Tencent Cloud configures redirection rules to redirect 404 error codes to `index.html`
  + 阿里云配置错误文档为`index.html`
  + Alibaba Cloud configuration error document is `index.html`

手动部署uni-app项目时需要注意将文件部署在配置的h5基础路径下。**HBuilderX一键部署时会自动按照manifest.json内配置的基础路径进行部署**
When manually deploying the uni-app project, you need to pay attention to deploying the files under the configured h5 base path. **HBuilderX will automatically deploy according to the basic path configured in manifest.json during one-click deployment**

### 部署多个项目@host-multi-project
### Deploying multiple projects @host-multi-project

如果部署多个项目到一个服务空间可以使用不同的基础路径来区分，需要注意的是这多个项目中只有一个项目可以使用history模式。
If you deploy multiple projects to a service space, you can use different base paths to distinguish them. It should be noted that only one of the multiple projects can use the history mode.

以一个admin项目和一个用户端项目为例，可以将用户端项目部署在前端网页托管的根目录下，admin项目部署在`/admin`目录下。通过`https://xxx.com/`访问用户端项目，通过`https://xxx.com/admin/`来访问admin项目
Taking an admin project and a client project as an example, the client project can be deployed in the root directory of the front-end web page hosting, and the admin project can be deployed in the `/admin` directory. Access the client project via `https://xxx.com/`, and access the admin project via `https://xxx.com/admin/`

**注意**
**Notice**

- 部署到子目录内的uni-app项目发行前需要将项目下manifest.json内`h5配置-->运行的基础路径`配置为子目录名，例`/admin/`
- Before the uni-app project deployed in the subdirectory is released, you need to configure the `h5 configuration --> running base path` in the manifest.json under the project as the subdirectory name, for example `/admin/`

## 阿里云使用限制
## Alibaba Cloud usage restrictions

- 前端网页部署限制为最大存储空间用量2GB
- Front-end web deployment is limited to a maximum storage space usage of 2GB
- 单文件最大限制为50MB
- The maximum limit for a single file is 50MB


<!--
### 腾讯云费用说明
### Tencent Cloud Fee Description

**新购**
**NEW PURCHASED**

- 新购时某套餐时有效期按自然月计。例：2020年5月28日购买2个月套餐，则套餐有效期至2020年7月28日23时59分59秒
- When a new package is purchased, the validity period is calculated in calendar months. Example: If you purchase a 2-month package on May 28, 2020, the package will be valid until July 28, 2020 at 23:59:59

**续费**
**Renewal**

- 续费逻辑和新购一样以自然月计。例：当前有效期至2020年7月28日23时59分59秒，续费一个月，则套餐有效期至2020年8月28日23时59分59秒
- The renewal logic is the same as the new purchase, which is calculated by natural month. Example: The current validity period is until 23:59:59 on July 28, 2020, and if the subscription is renewed for one month, the package is valid until 23:59:59 on August 28, 2020

**升配**
**Upgrade**

- 升配费用 = 按月升配差价 × 升配天数 / (365 / 12) × 适用折扣
- Upgrade fee = monthly upgrade price difference × upgrade days / (365 / 12) × applicable discount
  - 按月升配差价：新老配置原价按月的单价。
  - Monthly upgrade price difference: The original price of the new and old configuration is the monthly unit price.
  - 升配的费用按天计算：升配天数 = 资源到期时间 - 当前时间。
  - The cost of an upgrade is calculated on a daily basis: upgrade days = resource expiration time - current time.
  - 适用折扣：根据升配天数向下匹配适用折扣。
  - Applicable discounts: The applicable discounts are matched downwards according to the upgrade days.
  - 折扣为现网生效的折扣。
  - Discounts are valid on the current network.
- 升配不影响资源到期时间。
- Upgrading does not affect the resource expiration time.

**升配示例**
**Upgrade example**

>以下价格仅作示例用，非官网实际价格，实际单价请以购买时为准。
>The following prices are for example only, not the actual prices on the official website, please refer to the actual unit price at the time of purchase.

举例：
Example:

2019年11月1日，购买3个月专业版套餐，到期时间为2020年2月1日23时59分59秒，包年包月单价为100元/月。
On November 1, 2019, the 3-month Professional Edition package is purchased, and the expiration time is 23:59:59 on February 1, 2020. The unit price of the annual package is 100 yuan/month.

2019年12月15日，将该套餐升级为1000元/月的企业版套餐。
On December 15, 2019, the package was upgraded to a 1,000 yuan/month enterprise version package.

- 按月升配差价 = 1000 - 100 = 900元/月
- Monthly upgrade price difference = 1000 - 100 = 900 yuan/month
- 升配天数 = 31 × 1 + 15 + 1 = 47天（1指1月份为31天，15指12月份剩余15天， 1指2月份1天）
- Upgrade days = 31 × 1 + 15 + 1 = 47 days (1 means 31 days in January, 15 means the remaining 15 days in December, 1 means 1 day in February)
- 适用折扣：暂无折扣
- Applicable discounts: No discounts yet
- 升配费用 = （1000 - 100） × 47 /（365 / 12） = 1390.53元
- Upgrade fee = (1000 - 100) × 47 / (365 / 12) = 1390.53 yuan
-->
