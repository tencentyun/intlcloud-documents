<span id="scenes"></span>

### 全站加速网络适用哪些场景？

全站加速网络（ECDN）主要适用于动静混合资源请求加速场景，可以优化请求的响应时间和稳定性，为网站提供优质、流畅的访问体验服务。  
典型应用场景包括：
- 政务数据传输加速
- 游戏数据传输加速
- 金融数据传输加速
- 电商数据传输加速
- 在线教育数据传输加速
- 互动娱乐数据传输加速

<span id="https"></span>

### 全站加速是否支持 HTTPS？

支持，ECDN 支持 HTTP/HTTPS/WebSocket 协议，HTTPS 仅支持兼容 SNI 扩展的客户端访问。

<span id="sni"></span>

### 什么是 SNI？

SNI（Server Name Indication）是为了解决一个服务器使用多个域名和证书的 SSL/TSL 扩展，它的工作原理就是在客户端连接到服务器建立 SSL 链接之前，先发送要访问站点的域名，这样服务器就可以根据该域名返回合适的证书。目前大部分操作系统和浏览器都很好地支持 SNI 扩展，极小部分操作系统（如 XP）和低版本浏览器（IE6 及以前版本）不支持。 

### 全站加速是否支持 Websocket?

支持，全站加速全面支持 WebSocket 协议。

<span id="websocket"></span>

### 什么是 Websocket？

WebSocket 协议是基于 TCP 的一种持久化协议，它实现了客户端与服务器全双工（full-duplex）通信，允许服务器主动发送信息给客户端。在 Websocket 协议之前，实现客户端和服务端双工通讯的 Web App 需要通过不断发送 HTTP 请求呼叫来进行询问，这导致了服务成本增加和效率低下的问题。
由于具有全双工通信的优势，WebSocket 广泛应用于社交订阅、协同办公、行情播报、互动直播、在线教育、物联网等场景，能更好地节省服务器资源和带宽，并且能够更实时地进行通讯。

<span id="global"></span>

### 全站加速支持中国境外加速吗？

支持，全站加速具备全球动态数据交付能力，平台默认全量开放中国境内加速服务，限量开放中国境外加速服务。单击前往 [ECDN 全球加速资格申请](https://console.cloud.tencent.com/apply) 页面申请开放权限。
权限申请通过后，您可以通过控制台域名管理页面，自助添加中国境外加速服务区域。  
![](https://main.qcloudimg.com/raw/d5c2c6d2c10e3129b728ab5b589ee9c7.png)

<span id="wsa"></span>

### ECDN 是否支持上传加速？
ECDN 支持对 POST 和 PUT 上传请求提供加速服务。

