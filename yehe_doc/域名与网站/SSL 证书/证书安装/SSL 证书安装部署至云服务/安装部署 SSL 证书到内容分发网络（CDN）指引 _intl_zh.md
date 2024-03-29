## 概述

本文档指导您将 SSL 证书部署到 CDN 内容分发网络。

## 前提条件

已登录 [证书管理控制台](https://console.cloud.tencent.com/certoverview)，成功申请获取证书。

## 操作步骤

>!
> 
> - 域名需要已经接入 CDN，且状态为部署中或已启动，关闭状态的域名无法部署证书。具体操作请参考 [接入域名](https://www.tencentcloud.com/document/product/228/5734)。
> - COS 或 数据万象开启 CDN 加速后，默认的 .file.myqcloud.com 或 .image.myqcloud.com 域名无法配置证书。
> - SVN 托管源暂时无法配置

1. 单击**已签发**页签，选择您需要部署的证书，并单击**证书详情**。

2. 进入 “证书详情” 管理页面，单击**一键部署**。

3. 在弹出的**选择部署类型**窗口中，选择 **CDN**，并单击**确定**。

4. 跳转到 [CDN 控制台](https://console.cloud.tencent.com/cdn)，进入**配置证书**详情页，已显示对应的域名、证书来源以及证书 ID。

5. 选择回源协议方式，您可以选择 CDN 节点回源站获取资源时的回源方式。

  - 选择 **HTTP** 回源配置成功后，用户至 CDN 节点请求支持 HTTPS/HTTP，CDN 节点回源站请求均为 HTTP。

  - 选择 **协议跟随** 回源配置，您的源站需要部署有效证书，否则将导致回源失败。配置成功后，用户至 CDN 节点请求为 HTTP 时，CDN 节点回源请求也为 HTTP。用户至 CDN 节点请求为 HTTPS 时，CDN 节点回源请求也为 HTTPS。

  - 若域名源站修改 HTTPS 端口为非 443 端口，会导致配置失败。

  - COS 源或 FTP 源域名仅支持 HTTP 回源。

6. 配置成功后，您可以在**证书管理**页面看到已经配置成功的域名以及证书情况。
