

## 配置场景

HSTS 即 HTTP Strict Transport Security，是国际互联网工程组织 IETE 推行的 Web 安全协议，通过强制客户端（浏览器等）使用 HTTPS 与服务器创建链接，帮助网站进行全局加密。

## 配置约束

- expireTime 约束为0 - 365天，配置时单位为秒。
- 可通过勾选是否包含子域名，来控制 includeSubDomain 参数。
- 开启 HSTS 配置需要先完成 HTTPS 加速配置。
- 开启 HSTS 后，建议您同步开启 [强制跳转](https://intl.cloud.tencent.com/document/product/228/35214) HTTP->HTTPS 配置，否则当请求为 HTTP 时，浏览器将不会进行 HSTS 缓存。

## 配置指南

登录 [CDN 控制台](https://console.cloud.tencent.com/cdn)，在菜单栏里选择【域名管理】，单击域名右侧【管理】，即可进入域名配置页面，【Https 配置】中可看到 HSTS 配置模块，默认情况下为关闭状态：
![](https://main.qcloudimg.com/raw/4e44076b3485c9de15776134af7d5e96.png)
单击开启，可进行相关配置：
![](https://main.qcloudimg.com/raw/5a98a2ede54d4eceb8b5f4f0a8bbaa3b.png)
单击【确定】后，根据所配置的内容决定响应头值，可单击【编辑】进行修改：
![](https://main.qcloudimg.com/raw/e22e2cf4ad493379db7f1bcf49cfa03a.png)

## 配置示例

假设域名`cloud.tencent.com`的 HSTS 配置如下：
![](https://main.qcloudimg.com/raw/58e49b2b5a0b94f21fa3547dda08daed.png)
访问时其 Response Header 为：
![](https://main.qcloudimg.com/raw/910e57e5abdedba4a33b4e4748a81318.png)

