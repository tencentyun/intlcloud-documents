由于苹果和谷歌根存储政策的更改，自2020年9月1日起，全球 CA 认证机构不再签发超过2年期的 SSL 证书，因此您对 SSL 证书进行续费操作时，相当于在控制台重新申请了一个新证书，旧证书并不会增加有效期。申请的新证书颁发后，您需将新证书重新安装部署到服务器上，部署后立即生效。
证书安装请查看 [证书安装相关文档](https://write.woa.com/#certificate)，若旧证书在有效期中，不影响旧证书的正常使用。

> **注意**
> 
>  免费证书续费操作，无需进行付费。
> 


## 免费证书续费流程

### 步骤1：免费证书快速重新申请
1. 免费证书在**过期前1个月**会开启快速续费通道，您可在 [SSL 证书管理控制台](https://console.cloud.tencent.com/ssl) 我的证书中，对应证书的状态项中单击**快速续期**，即可打开免费证书快速重新申请页面。

2. 在 “提交资料” 页面，请确认您的申请信息，单击**下一步**，即可进入 “选择验证方式” 页面。

### 步骤2：域名验证
1. 在 “选择验证方式” 页面，选择验证方式。

  - **选择自动添加 DNS**：验证方法可查看 [详情](https://www.tencentcloud.com/document/product/1007/53635)。
    

      > **说明**
      > 
      > 若申请的域名已成功托管在 [DNS 解析 DNSPod 控制台](https://console.cloud.tencent.com/cns/domains)，可支持自动添加 DNS。
      > 

  - **选择 DNS 验证**：验证方法可查看 [详情](https://intl.cloud.tencent.com/document/product/1007/45895)。

  - **选择文件验证**：验证方法可查看 [详情](https://intl.cloud.tencent.com/document/product/1007/43542)。

2. 根据**验证操作**提示，完成域名身份验证。
   

   > **说明**
   > 单击**查看域名验证状态**，即可查看当前域名验证的状态。 
   >   - 验证中：系统正在进行验证检查。
   >   - 等待验证：等待添加域名验证操作。
   >   - 验证超时：系统进行验证检查超过30s未成功检查将显示验证超时。
   >   - 已通过：已通过域名验证所有权认证。
   >   - 验证失败：验证期内未完成验证域名显示验证失败。

3. 域名验证通过后，CA 机构将在24小时内完成签发证书操作，请您耐心等待。


## 下载和部署
- 完成域名审核后，登录 [SSL 证书管理控制台](https://console.cloud.tencent.com/ssl)，选择已颁发的证书并单击**下载**，即可下载至本地进行证书安装。证书安装请查看 [证书安装相关文档](https://write.woa.com/#certificate)。

- 如您需要直接部署到腾讯云相关云服务上。相关操作请参见 [如何选择 SSL 证书安装部署类型？](https://intl.cloud.tencent.com/document/product/1007/30173)


## 证书安装相关文档

证书颁发成功后，您需要重新安装证书，您可以根据您搭建的服务器类型进行证书安装。

> **说明**
> 使用一键 HTTPS 功能，您无需进行繁琐的 SSL 证书部署操作，即可帮助您实现从 HTTP 到 HTTPS 的能力升级。

- 国际标准证书：

  -  若您购买使用的服务器是 Linux 系统，建议您使用以下方式：

    - [Apache 服务器证书安装部署](https://intl.cloud.tencent.com/document/product/1007/30953)

    - [Nginx 服务器证书安装部署](https://intl.cloud.tencent.com/document/product/1007/30954)

    - [Tomcat 服务器 SSL 证书安装部署（JKS 格式）](https://www.tencentcloud.com/document/product/1007/50805)

    - [Tomcat 服务器 SSL 证书安装部署（PFX 格式）](https://intl.cloud.tencent.com/document/product/1007/30956)

    - [GlassFish 服务器证书安装部署](https://intl.cloud.tencent.com/document/product/1007/36565)

    - [JBoss 服务器证书安装部署](https://intl.cloud.tencent.com/document/product/1007/36566)

    - [Jetty 服务器证书安装部署](https://intl.cloud.tencent.com/document/product/1007/36567)

  - 若您购买使用的服务器是 Windows 系统，建议您使用以下方式：

    - [IIS 服务器证书安装](https://intl.cloud.tencent.com/document/product/1007/30955)

    - [Weblogic 服务器证书安装部署](https://intl.cloud.tencent.com/document/product/1007/38093)

    - [Apache 服务器 SSL 证书安装部署（Windows）](https://intl.cloud.tencent.com/document/product/1007/50198)

    - [Tomcat 服务器 SSL 证书安装部署（JKS 格式）（Windows）](https://intl.cloud.tencent.com/document/product/1007/43804)


## 相关问题
- [免费 SSL 证书名额相关问题](https://intl.cloud.tencent.com/document/product/1007/51464)

- [SSL 证书配置的 TXT 解析是否可以删除？](https://intl.cloud.tencent.com/document/product/1007/37851)

- [忘记私钥密码怎么办？](https://intl.cloud.tencent.com/document/product/1007/30191)

