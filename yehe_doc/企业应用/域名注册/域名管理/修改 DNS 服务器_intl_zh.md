


## 操作场景
若您注册的域名需添加解析，则需将域名的托管至 DNS 解析商后才可正常解析。本文将指导您如何通过修改 DNS 服务器地址方式指定对应的 DNS 服务解析商。


## 操作步骤
如果域名在腾讯云注册，或者已转入腾讯云，可以通过以下步骤修改 DNS 服务器：
1. 登录 [腾讯云域名注册控制台](https://console.intl.cloud.tencent.com/domain/manage)，进入 “我的域名” 页面。
2. 选择待修改 DNS 的域名，单击**管理**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/8bd6a6c32828f4cfc0f647d9cb728d28.png)
3. 在 “基本信息” 栏中，单击 “DNS 服务器” 的**修改**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/e54332d4d0cbb5a45e79f3921eb1af55.png)
4. 在弹出的 “修改 DNS 服务器” 窗口中，选择您需要修改域名 DNS 服务器方式。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/85d545523f617ae84411c366d324db1e.png)
 - **使用 DNSPod**：自动为该域名匹配 DNSPod 服务器的 DNS 地址。
 - **自定义 DNS**： 填写您需要设置的 DNS 服务器地址。
>? 
>- 自定义的 DNS 服务器域名不能是私建的 DNS 服务器域名，必须是解析商的权威 DNS 服务器域名。
>- 需要在腾讯云进行解析的域名，修改 DNS 服务器地址请参考 [各个套餐对应的 DNS 服务器地址](https://docs.dnspod.com/dns/6036185c718dbb61ac2bee96/)。
