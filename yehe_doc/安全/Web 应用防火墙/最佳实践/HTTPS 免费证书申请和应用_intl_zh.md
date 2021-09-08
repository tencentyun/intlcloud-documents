## 前提条件
Web 应用防火墙提供域名 HTTPS 接入配置和防护能力，若您的网站未进行 HTTPS 改造，您可以在 [腾讯云 SSL 证书控制台](https://console.cloud.tencent.com/ssl) 申请免费的域名证书。证书申请后，在 Web 应用防火墙控制台关联证书，Web 应用防火墙将帮助您在不改造源站的情况下，一键实现全站 HTTPS 访问，客户端使用 HTTPS 连接网站。
## HTTPS 证书关联操作步骤
1. 登录 [Web 应用防火墙控制台](https://console.cloud.tencent.com/guanjia/waf/overview)，在左侧导航中，选择选择【实例管理】>【实例列表】，进入实例列表页面。
2. 在实例列表页面，选择需要添加域名的实例，在右侧单击所属实例的【域名接入】。
![](https://main.qcloudimg.com/raw/39245ce95463c096543cd5235d3f8c06.png)
3. 在域名接入页面，单击【添加域名】，进入添加域名页面。
3. 在域名配置的服务器配置中，勾选【HTTPS】，在证书配置中，单击【关联证书】。
>?证书格式为 PEM 格式，内容为文本类型。

![](https://main.qcloudimg.com/raw/99caab3e75e8ebe945ef196970ff35f3.png)
4. 选择证书来源为“腾讯云托管证书”，Web 应用防火墙会自动关联该域名的可用证书，配置完成后，单击【保存】。
![](https://main.qcloudimg.com/raw/a8ee70f99a6da5847fcc76b887d0cf5e.png)
5. 开启 HTTPS 强制跳转开关，并在上方勾选【HTTP】访问协议，同时选择 “HTTPS 回源方式”选择 HTTP，其他参数根据实际情况填写完成后，您的网站将支持 HTTPS 访问。
>!如需开启 HTTPS 强制跳转开关，需同时勾选 HTTP 和 HTTPS 访问协议。

![](https://main.qcloudimg.com/raw/afc93528ac57fc3b27d36fa6056e600e.png)

