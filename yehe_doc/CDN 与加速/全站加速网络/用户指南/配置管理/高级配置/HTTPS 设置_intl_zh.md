
## 配置说明
HTTPS 指超文本传输安全协议（Hypertext Transfer Protocol Secure），是一种在 HTTP 协议基础上进行传输加密的安全协议，能够有效保障数据传输安全。配置 HTTPS 时，需要您提供域名对应的证书，将其部署在全网 ECDN 节点，实现全网数据加密传输功能。

>!
>- 您配置 HTTPS 的域名需已接入 ECDN，且状态为**部署中**或**已上线**。
>- 若您的业务已迁移至 CDN 控制台，请参考 [CDN 产品文档](https://intl.cloud.tencent.com/document/product/228)，前往 CDN 控制台进行操作。

## 配置新增
### 选择域名
1. 登录 [ECDN 控制台](https://console.cloud.tencent.com/dsa)，在左侧目录中，单击【域名管理】，进入管理页面。
2. 在列表中，找到需要配置的域名，单击【管理】，进入详情页后，选择【高级配置】。  
3. 开启 HTTPS 功能需要先部署域名证书，单击【前往配置】进入域名证书配置页面。
![](https://main.qcloudimg.com/raw/f6802014b9cea8eda9fbb0eff85fc120.png)

### 配置证书
进入证书配置页面，您可以为域名配置自有证书或腾讯云托管证书。域名证书配置详细流程请参见 [证书管理](https://intl.cloud.tencent.com/document/product/570/10366)。
![](https://main.qcloudimg.com/raw/8a8977310c0f1d6f01a7470a4df234b6.png)



## 配置修改
- **开启 HTTP2.0 功能**
已配置证书的域名，可以在高级配置页面开启HTTP2.0功能。
- **开启 HTTPS 强制跳转功能**
已配置证书的域名，可以开启 HTTPS 强制跳转功能，功能开启后，所有 HTTP 请求将强制跳转成 HTTPS 请求。
开启HTTPS强制跳转，您还可以指定使用301或302状态码跳转，默认使用302状态码。
- **修改证书及回源方式**
已配置证书的域名，可以单击【前往配置】，进入证书管理页面，修改证书内容或修改回源方式。

![](https://main.qcloudimg.com/raw/e93ea220aa260f173438f1a70907d9ed.png)
