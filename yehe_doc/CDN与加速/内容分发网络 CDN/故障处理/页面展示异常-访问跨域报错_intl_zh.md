
## 现象描述

前端报跨域错误，导致页面错误或展示异常等问题，如下图

![](https://main.qcloudimg.com/raw/af636dbb5bba454bb79234cd7b49dca2.png)

## 可能原因

跨域是由于浏览器的同源策略限制，同时也为了网页的安全性考虑，当通过脚本向不同的来源发送请求时，这个请求的响应会被浏览器拦截，从而导致前端报错或页面无法正常展示。而当一个请求URL的**协议、域名、端口**三者之间任意一个与当前页面URL不同即为跨域。

## 解决思路

1. 确认页面异常报错是否是由跨域造成的，如下所示。
![](https://main.qcloudimg.com/raw/78d05383b9040d313c05add33a1737df.png)
2. 在 CDN 控制台配置对应的 HTTP 响应头部，定义允许访问该资源的域。

## 处理步骤

1. 登录 <a href="https://console.cloud.tencent.com/cdn/domains">CDN 控制台</a>，在对应的域名管理-高级配置-HTTP 响应头配置下，设置好 Access-Control-Allow-Origin 头部参数即可。如下图，即允许所有域名发起的跨域请求。详情请见 [Access-Control-Allow-Origin 匹配模式介绍](#ac)。

2. 或针对性的设置为单个或多个已知的允许发起跨域请求的域名/IP，如下所示。
同时也可以根据业务需要，加上如 Access-Control-Request-Method、Access-Control-Request-Headers 、Access-Control-Max-Age 等头部参数，来限制浏览器所能接受的请求的方法、可携带的头、预请求的有效时间等等。详情请见 [参数支持列表](#ap)。


>! 若您已在 COS 侧存储桶配置了跨域访问，为保证正常访问，请在 CDN 控制台 <a href="https://intl.cloud.tencent.com/document/product/228/35320">HTTP 响应头</a> 同步配置跨域规则。

[](id:ap)
### 参数支持列表

| 头部参数                      | 说明                                                         |
| :---------------------------- | :----------------------------------------------------------- |
| Access-Control-Allow-Origin   | 用于解决资源的跨域权限问题，域值定义了允许访问该资源的域。若来源请求 Host 在域名配置列表之内，则直接填充对应值在返回头部中。也可以设置通配符 `“*”`，允许被所有域请求。更多说明请见 [Access-Control-Allow-Origin 匹配模式介绍](#ac)。 支持输入`“*”` ，或多个域名 / IP / 域名与 IP 混填（必须包含 `http://` 或 `https://`，填写示例：`http://test.com,http://1.1.1.1`， 逗号隔开）（注意：输入框最多可输入1000字符）。 |
| Access-Control-Allow-Methods  | 用于设置跨域允许的 HTTP 请求方法，可同时设置多个方法，如下： Access-Control-Allow-Methods: `POST, GET, OPTIONS`。 |
| Access-Control-Max-Age        | 用于指定预请求的有效时间，单位为秒。 非简单的跨域请求，在正式通信之前，需要增加一次 HTTP 查询请求，称为“预请求”，用来查明这个跨域请求是不是安全可以接受的，如下请求会被视为非简单的跨域请求： 以 GET、HEAD 或者 POST 以外的方式发起，或者使用 POST，但是请求数据类型为 application / x-www-form-urlencoded、 multipart / form-data、text / plain 以外的数据类型，如 application / xml 或者 text / xml。 使用自定义请求头为：Access-Control-Max-Age:`1728000`，表明在1728000秒（20天）内，对该资源的跨域访问不再发送另外一条预请求。 |
| Access-Control-Expose-Headers | 用于指定哪些头部可以作为响应的一部分暴露给客户端。 默认情况下，只有6种头部可以暴露给客户端：Cache-Control、Content-Language、Content-Type、Expires、Last-Modified、Pragma。 如果想让客户端访问到其他的头部信息，可以进行如下设置，当输入多个头部时，需用 “,” 隔开，如：`Access-Control-Expose-Headers: Content-Length,X-My-Header`，表明客户端可以访问到 Content-Length 和 X-My-Header 这两个头部信息。 |

[](id:ac)
### Access-Control-Allow-Origin 匹配模式介绍

| **匹配模式**   | **域值**                                                     | **说明**                                                     |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 全匹配         | `*`                                                            | 设置为 `*` 时，则响应添加头部： `Access-Control-Allow-Origin:*` |
| 固定匹配       | `http://cloud.tencent.com` `https://cloud.tencent.com` `http://www.b.com` | 来源`https://cloud.tencent.com`，命中列表，则响应添加头部： `Access-Control-Allow-Origin: https://cloud.tencent.com` 来源为 `https://www.qq.com`，未命中列表，响应无变化。 |
| 二级泛域名匹配 | `https://*.tencent.com`                                      | 来源 `https://cloud.tencent.com`，命中列表，则响应添加头部： `Access-Control-Allow-Origin: https://cloud.tencent.com` 来源为 `https://cloud.qq.com`，未命中列表，响应无变化。 |
| 端口匹配       | `https://cloud.tencent.com:8080`                             | 来源为 `https://cloud.tencent.com:8080`，命中列表，则响应添加头部： `Access-Control-Allow-Origin:https://cloud.tencent.com:8080` 来源为 `https://cloud.tencent.com`，未命中列表，响应无变化。 |

> !若存在特殊端口，则需要在列表中填写相关信息，不支持任意端口匹配，必须指定。
