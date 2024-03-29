>? 若您的业务已迁移至 CDN 控制台，请参考 [CDN 产品文档](https://intl.cloud.tencent.com/document/product/228)，前往 CDN 控制台进行操作。
HTTP 的消息通常包括：
+ 客户端向服务端发送的请求消息。
+ 服务端向服务端发送的响应消息。

以上几种类型的消息均由一个起始行，一个或多个头部，一个标明头部结束的空行和可选的消息体组成。
![](https://main.qcloudimg.com/raw/75b4558def817c65217447f3b9ae0da2.png)
其中 HTTP 头部分为：通用头、请求头、响应头、实体头。每一个头部由域名、冒号（:）、域值组成，如： `Connection:keep-alive`。
使用腾讯云 ECDN 提供的 HTTP Header 配置功能，当您的用户请求业务资源时，会在返回的**响应消息**中添加您配置的头部，以实现跨域访问等目的。

>!
> + 由于 HTTP Header 配置是针对域名，因此一旦配置生效，用户对该域名下任意一个资源的响应消息中均会加入所配置头部。
> + 配置 HTTP Header 仅影响客户端（如浏览器）的响应行为，不会影响到 ECDN 节点的缓存行为。

## 配置说明
ECDN 提供以下几种头部的配置：
+ Content-Disposition：激活客户端下载资源及设置默认的文件名。
+ Content-Language：指定资源在客户端（如浏览器）响应的语言。
+ Access-Control-Allow-Origin：指定跨域请求时，允许访问资源的请求来源。
+ Access-Control-Allow-Methods： 指定跨域请求时，允许的跨域请求方法。
+ Access-Control-Max-Age：指定跨域请求时，对特定资源的预请求返回结果的缓存时间。
+ Access-Control-Expose-Headers：指定跨域请求时，客户端可见的头部集合。

### 通用配置
#### Content-Disposition
Content-Disposition 用来激活浏览器的下载，同时可以设置默认的下载的文件名。服务端向客户端浏览器发送文件时，如果是浏览器支持的文件类型，如 .txt、.jpg 等类型，会默认直接使用浏览器打开，如果需要提示用户保存，则可以通过配置 Content-Disposition 字段覆盖浏览器默认行为。常用配置：`Content-Disposition：attachment;filename=FileName.txt`

#### Content-Language
Content-Language 是用于定义页面所使用的语言代码，常用配置如下：
- `Content-Language: zh-CN`
- `Content-Language: en-US`

### 跨域配置
跨域是指某一个域名，如 `www.abc.com` 下的某资源，向另一个域名 `www.def.com` 下的某资源发起请求，此时由于资源所属域名不同，即出现 **跨域**，不同的协议、不同的端口均会造成跨域访问的出现。此时必须在 Response Header 中增加跨域相关配置，才能让前者成功获得数据。

#### Access-Control-Allow-Origin
Access-Control-Allow-Origin 用于解决资源的跨域权限问题，域值定义了允许访问该资源的域，也可以设置通配符“\*” ，允许被所有域请求。常用配置如下：
- `Access-Control-Allow-Origin: *`
- `Access-Control-Allow-Origin: http://www.test.com`

配置 Access-Control-Allow-Origin，有以下限制条件：
+ 不支持泛域名，如 `*.qq.com`。
+ 仅可配置为“\*”，或指定一个 URI。
+ 在配置指定域名时，需要加上 “http://” 或 “https://” 前缀。

#### Access-Control-Allow-Methods 
Access-Control-Allow-Methods 用于设置跨域允许的 HTTP 请求方法，可同时设置多个方法，如下：
`Access-Control-Allow-Methods: POST, GET, OPTIONS`

#### Access-Control-Max-Age
Access-Control-Max-Age 用于指定预请求的有效时间。
非简单的跨域请求，在正式通信之前，需要增加一次 HTTP 查询请求，称为“预请求”，用来查明这个跨域请求是不是安全可以接受的，如下请求会被视为非简单的跨域请求：
+ 以 GET、HEAD 或者 POST 以外的方式发起的请求，或者使用 POST，但是请求数据类型为 application/x-www-form-urlencoded、 multipart/form-data、text/plain 以外的数据类型，如 application/xml 或者 text/xml。
+ 使用自定义请求头。

Access-Control-Max-Age 的单位为秒，设置示例：`Access-Control-Max-Age: 1728000`，表明在1728000秒（20天）内，对该资源的跨域访问不再发送另外一条预请求。

#### Access-Control-Expose-Headers
Access-Control-Expose-Headers 指定跨域请求时，允许访问的头部信息。默认情况下，只有 6 种头部可以暴露给客户端：
- Cache-Control
- Content-Language
- Content-Type
- Expires
- Last-Modified
- Pragma

如果想让客户端访问到其他的头部信息，可以进行如下设置，当输入多个头部时，需用“,”隔开：
`Access-Control-Expose-Headers: Content-Length，QCloud-DSA-MyCustom-HeaderY`

那么服务器就会允许请求中包含 Content-Length，QCloud-DSA-MyCustom-HeaderY 这两个字段。

### 自定义头部
ECDN 支持用户添加自定义头部，您可以根据业务需要，添加自定义头部字段。
以下字段暂不支持添加：
```
	Date  
	Expires 
	Content-Type
	Content-Encoding
	Content-Length
	Transfer-Encoding
	Cache-Control
	If-Modified-Since
	Last-Modified
	Connection
	Content-Range
	ETag
	Accept-Ranges
	Age
	Authentication-Info
	Proxy-Authenticate
	Retry-After
	Set-Cookie
	Vary
	WWW-Authenticate
	Content-Location
	Content-MD5
	Content-Range
	Meter
	Allow
	Error
```

### 配置流程
1. 登录 [ECDN 控制台](https://console.cloud.tencent.com/dsa)，单击左侧菜单栏的【域名管理】，进入管理页面，在页面中，单击您要配置的域名右侧的【管理】，进入域名配置页面。
2. 单击【高级配置】，在 **HTTP Header 配置** 模块中单击【添加 HTTP Header】。
![](https://main.qcloudimg.com/raw/96abcdc42d7f33432c3c2abbace73251.png)
3. 在弹出的窗口中选择要添加的 HTTP Header，填写对应的值，单击【新增参数】可以继续添加头部字段，最后单击【确定】提交。
![](https://main.qcloudimg.com/raw/6124ce1d6a6bbeedd6146e16dbef6575.png)
4. 配置生效时间约为5分钟，在下方表格中可以查看添加的 HTTP Header。单击 Header 右侧的【修改】或【删除】可以对该 Header 进行操作。
![](https://main.qcloudimg.com/raw/15b6cf8531c72f39d8ac6d04a4ca769e.png)
5. 您可以通过再次单击【添加 HTTP Header】继续添加 HTTP Header，每个 HTTP Header 只能添加一次。
