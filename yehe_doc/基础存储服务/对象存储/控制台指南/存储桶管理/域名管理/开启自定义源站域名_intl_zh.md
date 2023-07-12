## 简介

本文介绍如何将自定义域名绑定至存储桶中，您可以通过这个自定义域名访问存储桶内的文件。

>? 通过对象存储控制台添加自定义域名上限为20个，如您想提高自定义域名的个数上限，请 [联系我们](https://intl.cloud.tencent.com/contact-sales)。

## 操作步骤

1. 登录 [对象存储控制台](https://console.cloud.tencent.com/cos5)。 
2. 在左侧导航栏中，单击**存储桶列表**，进入存储桶列表页面。
3. 单击需要配置域名的存储桶，进入存储桶配置页面。
4. 在左侧导航栏中，选择**域名与传输管理 > 自定义源站域名**，单击**添加域名**，配置如下选项。

  - **域名**：输入待绑定的自定义域名（例如 `www.example.com`）。请确保输入的域名已备案且在 [域名服务控制台](https://console.cloud.tencent.com/cns/domains) 添加解析，并已在 DNS 服务商处设置好对应的 CNAME，详情请参见 [CNAME 配置](https://intl.cloud.tencent.com/document/product/228/3121)。若您在接入的自定义 CDN 加速域名为以下情况，则需要进行域名归属权验证，详情请查看 [域名归属验证](https://intl.cloud.tencent.com/document/product/228/42693) 文档。
     - 首次接入该域名
     - 该域名已被其他用户接入
     - 接入域名为泛域名
  - **源站类型**：有默认源站和静态网站源站两种，如果您的存储桶开启了静态网站功能即为静态网站源站，否则为默认源站。如果您的自定义域名需要用作静态网站，请使用静态网站源站并开启存储桶的静态网站功能。
  - **HTTPS 证书**：当域名保存后，可选择绑定证书。关于证书的安装方法，可参见 [证书安装](https://www.tencentcloud.com/document/product/1007/36568)。
  >?
  >- COS 国内公有云地域、新加坡地域已支持托管自定义源站域名的 HTTPS 证书，如果您的域名还没有 HTTPS 证书，可点击 [申请腾讯云证书](https://console.cloud.tencent.com/ssl)。
  >- 对于其他境外地域暂不支持 HTTPS 证书托管，若需要使用 HTTPS 证书，可参考 [方式二](https://intl.cloud.tencent.com/document/product/436/11142)。
