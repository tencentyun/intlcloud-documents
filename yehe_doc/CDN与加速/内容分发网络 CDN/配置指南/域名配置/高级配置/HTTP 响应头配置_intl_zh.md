## 配置场景

当您的业务用户请求业务资源时，您可以在返回的**响应消息**中配置头部，以实现跨域访问等目的。
响应头部配置是域名维度的，因此一旦配置生效，会对域名下任意一个资源的响应消息生效。配置响应头部仅影响客户端（如浏览器）的响应行为，不会影响到 CDN 节点的缓存行为。

## 配置指南

### 查看配置

登录 [CDN 控制台](https://console.cloud.tencent.com/cdn)，在菜单栏里选择【域名管理】，单击域名右侧【管理】，即可进入域名配置页面，在【高级配置】中可看到响应头部配置，默认情况下配置为关闭状态，单击【新增规则】可配置 HTTP 响应头规则：
![](https://main.qcloudimg.com/raw/979a6f3254776cdadd5ca4dc71d631a6.png)

### 操作类型

| 操作类型 | 说明                                                         |
| :------- | :----------------------------------------------------------- |
| 设置     | 变更指定响应头部参数的取值为设置后的值。<br/>若设置的头部不存在，则会增加该头部。<br>若存在多个重复的头部参数，则会全部变更，同时合并为一个头部。 即当配置规则为【设置 x-cdn: value1】，若请求中包含有多个 x-cdn 头部，则多个头部均会变更，合并为一个头部 x-cdn: value1。 |
| 删除     | 删除指定的响应头参数。                                       |

> !
> - 部分头部不支持自助设置/删除，具体清单请参见文档 [注意事项](#noice)。
> - HTTP 响应头配置规则最多可配置10条。
> - 多条规则支持调整优先级：底部优先级大于顶部。若同一头部参数配置了多条规则，则生效最底部，即优先级最高的那条。

### 头部参数

<table>
<thead>
<tr>
<th style="width:230px">头部参数</th>
<th>说明</th>
</tr>
</thead>
<tbody><tr>
<td>Access-Control-Allow-Origin</td>
<td>用于解决资源的跨域权限问题，域值定义了允许访问该资源的域。若来源请求 Host 在域名配置列表之内，则直接填充对应值在返回头部中。也可以设置通配符 “*”，允许被所有域请求。更多说明请见 <a href="#acao">Access-Control-Allow-Origin 匹配模式介绍</a>。</br>支持输入“*” ，或多个域名 / IP / 域名与 IP 混填（必须包含 <code>http://</code> 或 <code>https://</code>，填写示例：<code>http://test.com,http://1.1.1.1</code>， 逗号隔开）（注意：输入框最多可输入1000字符）。</td>
</tr>
<tr>
<td>Access-Control-Allow-Methods</td>
<td>用于设置跨域允许的 HTTP 请求方法，可同时设置多个方法，如下：<br>Access-Control-Allow-Methods: <code>POST, GET, OPTIONS</code>。</td>
</tr>
<tr>
<td>Access-Control-Max-Age</td>
<td>用于指定预请求的有效时间，单位为秒。<br>非简单的跨域请求，在正式通信之前，需要增加一次 HTTP 查询请求，称为“预请求”，用来查明这个跨域请求是不是安全可以接受的，如下请求会被视为非简单的跨域请求：<br>以 GET、HEAD 或者 POST 以外的方式发起，或者使用 POST，但是请求数据类型为 application / x-www-form-urlencoded、 multipart / form-data、text / plain 以外的数据类型，如 application / xml 或者 text / xml。<br>使用自定义请求头为：Access-Control-Max-Age:<code>1728000</code>，表明在1728000秒（20天）内，对该资源的跨域访问不再发送另外一条预请求。</td>
</tr>
<tr>
<td>Access-Control-Expose-Headers</td>
<td>用于指定哪些头部可以作为响应的一部分暴露给客户端。<br>默认情况下，只有6种头部可以暴露给客户端：Cache-Control、Content-Language、Content-Type、Expires、Last-Modified、Pragma。<br>如果想让客户端访问到其他的头部信息，可以进行如下设置，当输入多个头部时，需用 “,” 隔开，如：<code>Access-Control-Expose-Headers: Content-Length,X-My-Header</code>，表明客户端可以访问到 Content-Length 和 X-My-Header 这两个头部信息。</td>
</tr>
<tr>
<td>Content-Disposition</td>
<td>用来激活浏览器的下载，同时可以设置默认的下载的文件名。<br>服务端向客户端浏览器发送文件时，如果是浏览器支持的文件类型，如 TXT、JPG 等类型，会默认直接使用浏览器打开，如果需要提示用户保存，则可以通过配置 Content-Disposition 字段覆盖浏览器默认行为。常用的配置如下：<br><code>Content-Disposition：attachment;filename=FileName.txt</code></td>
</tr>
<tr>
<td>Content-Language</td>
<td>用于定义页面所使用的语言代码。常用配置如下：<br><code>Content-Language: zh-CN</code><br><code>Content-Language: en-US</code></td>
</tr>
<tr>
<td>自定义</td>
<td>支持添加自定义 Header，自定义 key-value 设置。<br>自定义头部参数：由大小写字母、数字及 - 组成，长度支持1 - 100个字符。<br>自定义头部取值：长度为1 - 1000个字符，不支持中文。</td>
</tr>
</tbody></table>


### Access-Control-Allow-Origin 匹配模式介绍[](id:acao)

| **匹配模式**   | **域值**                                                     | **说明**                                                     |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 全匹配         | *                                                            | 设置为 * 时，则响应添加头部： `Access-Control-Allow-Origin:*` |
| 固定匹配       | `http://cloud.tencent.com` `https://cloud.tencent.com` `http://www.b.com` | 来源`https://cloud.tencent.com`，命中列表，则响应添加头部： `Access-Control-Allow-Origin: https://cloud.tencent.com` <br/>来源为 `https://www.qq.com`，未命中列表，响应无变化。 |
| 二级泛域名匹配 | `https://*.tencent.com`                                       | 来源 `https://cloud.tencent.com`，命中列表，则响应添加头部： `Access-Control-Allow-Origin: https://cloud.tencent.com` <br/>来源为 `https://cloud.qq.com`，未命中列表，响应无变化。 |
| 端口匹配       | `https://cloud.tencent.com:8080`                             | 来源为 `https://cloud.tencent.com:8080`，命中列表，则响应添加头部： `Access-Control-Allow-Origin:https://cloud.tencent.com:8080`<br/>来源为 `https://cloud.tencent.com`，未命中列表，响应无变化。 |

> ! 若存在特殊端口，则需要在列表中填写相关信息，不支持任意端口匹配，必须指定。

### 注意事项[](id:noice)

此功能不支持以下头部，即以下头部不会生效：

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
