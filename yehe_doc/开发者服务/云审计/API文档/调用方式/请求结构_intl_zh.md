## 1. 服务地址

API 支持就近地域接入，本产品就近地域接入域名为 cvm.tencentcloudapi.com ，也支持指定地域域名访问，例如广州地域的域名为 cvm.ap-guangzhou.tencentcloudapi.com 。

推荐使用就近地域接入域名。根据调用接口时客户端所在位置，会自动解析到**最近的**某个具体地域的服务器。例如在广州发起请求，会自动解析到广州的服务器，效果和指定 cvm.ap-guangzhou.tencentcloudapi.com 是一致的。

**注意：对时延敏感的业务，建议指定带地域的域名。**

目前支持的域名列表为：

| 接入地域 | 域名 |
|----------|------|
| 就近地域接入（推荐，只支持非金融区）| cvm.tencentcloudapi.com|
| 华南地区(广州) | cvm.ap-guangzhou.tencentcloudapi.com|
| 华东地区(上海) | cvm.ap-shanghai.tencentcloudapi.com|
| 华北地区(北京) | cvm.ap-beijing.tencentcloudapi.com|
| 西南地区(成都) | cvm.ap-chengdu.tencentcloudapi.com|
| 西南地区(重庆) | cvm.ap-chongqing.tencentcloudapi.com|
| 港澳台地区(中国香港) | cvm.ap-hongkong.tencentcloudapi.com |
| 亚太东南(新加坡) | cvm.ap-singapore.tencentcloudapi.com|
| 亚太东南(曼谷) | cvm.ap-bangkok.tencentcloudapi.com |
| 亚太南部(孟买) | cvm.ap-mumbai.tencentcloudapi.com|
| 亚太东北(首尔) | cvm.ap-seoul.tencentcloudapi.com|
| 亚太东北(东京) | cvm.ap-tokyo.tencentcloudapi.com |
| 美国东部(弗吉尼亚) | cvm.na-ashburn.tencentcloudapi.com|
| 美国西部(硅谷) | cvm.na-siliconvalley.tencentcloudapi.com|
| 北美地区(多伦多) | cvm.na-toronto.tencentcloudapi.com |
| 欧洲地区(法兰克福) | cvm.eu-frankfurt.tencentcloudapi.com |
| 欧洲地区(莫斯科) | cvm.eu-moscow.tencentcloudapi.com |

**注意：由于金融区和非金融区是隔离不互通的，因此当访问金融区服务时（公共参数 Region 为金融区地域），需要同时指定带金融区地域的域名，最好和 Region 的地域保持一致。**

| 金融区接入地域 | 金融区域名 |
|----------|------|
|华东地区(上海金融)| cvm.ap-shanghai-fsi.tencentcloudapi.com|
|华南地区(深圳金融)| cvm.ap-shenzhen-fsi.tencentcloudapi.com|

## 2. 通信协议

腾讯云 API 的所有接口均通过 HTTPS 进行通信，提供高安全性的通信通道。

## 3. 请求方法

支持的 HTTP 请求方法:

* POST（推荐）
* GET

POST 请求支持的 Content-Type 类型：

* application/json（推荐），必须使用签名方法 v3（TC3-HMAC-SHA256）。
* application/x-www-form-urlencoded，必须使用签名方法 v1（HmacSHA1 或 HmacSHA256）。
* multipart/form-data（仅部分接口支持），必须使用签名方法 v3（TC3-HMAC-SHA256）。

GET 请求的请求包大小不得超过32KB。POST 请求使用签名方法 v1（HmacSHA1、HmacSHA256）时不得超过1MB。POST 请求使用签名方法 v3（TC3-HMAC-SHA256）时支持10MB。

## 4. 字符编码

均使用`UTF-8`编码。
