网站业务接入 DDoS 边界防护时，需要在DDoS 边界防护的域名规则页面为业务添加转发规则，本文将介绍如何接入域名业务相关的步骤。
 ## 前提条件
已购买 [DDoS 边界防护](https://intl.cloud.tencent.com/document/product/297/42172)。

## 操作步骤
1. 登录 [DDoS 边界防护管理控制台](https://console.cloud.tencent.com/ddos/antiddos-edge/policy/ddos) ，在左侧导航中，单击【业务配置】,并单击域名业务接入下方的【立即接入】。
![](https://main.qcloudimg.com/raw/d83c5acd556973ba5535dd4986712f09.png)
2. 在选择实例页面，选择关联资源 ID，单击【下一步：协议选择】。
![](https://main.qcloudimg.com/raw/10358df9a34a3369a5f254b4e8f379fe.png)
3. 在协议选择页面，选择转发协议类型，如果选择 HTTPS 协议，需要选择相关证书，单击【下一步：端口参数】。
![](https://main.qcloudimg.com/raw/9b0f7d24f42a1106d6cf95536f53a9d3.png)
4. 在端口参数页面，填写业务域名，单击【下一步：回源方式】。
>?域名长度不能超过67。
5. 在回源方式页面，填写相关参数，单击【下一步：修改解析】。
![](https://main.qcloudimg.com/raw/8afb4199cf221635ce215cbc45e5d98c.png)
6. 业务接入已完成，修改 DNS 解析进一步保护业务安全。


