 非网站业务（例如：端游、手游、App等）接入 DDoS 边界防护时，需要在 DDoS 边界防护的端口规则页面为业务添加转发规则，本文将介绍如何添加相关转发规则。

 ## 前提条件
已购买 [DDoS 边界防护](https://intl.cloud.tencent.com/document/product/297/42172)。

## 操作步骤
1. 登录 [DDoS 边界防护管理控制台](https://console.cloud.tencent.com/ddos/antiddos-edge/policy/ddos) ，在左侧导航中，单击【业务配置】,并单击端口业务接入下方的【立即接入】。
![](https://main.qcloudimg.com/raw/e05e5c3ac29774380fba446574ccc460.png)
2. 在选择实例页面，选择关联资源 ID，单击【下一步：协议选择】。
![](https://main.qcloudimg.com/raw/36b46616e32c1b44d2546c038d3ec8f4.png)
3. 在协议选择页面，选择转发协议类型，单击【下一步：端口参数】。
![](https://main.qcloudimg.com/raw/d78eb1001864a5ff67d4b5f96764297c.png)
4. 在端口参数页面，填写业务域名，单击【下一步：回源方式】。
>?转发端口和源站端口为1到65535之间的数值。

![](https://main.qcloudimg.com/raw/093d1057f4991ddff26f6064e1ea49c9.png)
5. 在回源方式页面，填写相关参数，单击【下一步：修改解析】。
![](https://main.qcloudimg.com/raw/435cd4aa61b3662f9164cdd2bdd32adb.png)
6. 业务接入已完成，修改 DNS 解析进一步保护业务安全。
