[](id:que1) 

### 邮件推送支持哪些身份验证机制？
邮件推送支持所有行业标准的身份验证机制，包括域名密钥识别邮件 (DKIM)、发件人策略框架 (SPF)、基于域的邮件身份验证、报告和一致性 (DMARC)。

[](id:que2) 
### 如何配置发信域名？
<dx-tabs>
::: 步骤一：DNS 解析界面配置
1. 通过 [发信域名](https://console.cloud.tencent.com/ses/domain) 设置页面，单击**新建域名**，填写域名后，提交即可。
![](https://qcloudimg.tencent-cloud.cn/raw/00947cc2ff7a7dc6855baee29d1a77ee.png)
2. 在 [DNS 解析 DNSPod 控制台](https://console.cloud.tencent.com/cns) 配置验证信息。
3. [](id:step2)返回至 [发信域名](https://console.cloud.tencent.com/ses/domain) 设置页面，单击**验证**。
4. 单击所在的发信域名地址，可进入配置详情页，可以看到域名值。
![](https://qcloudimg.tencent-cloud.cn/raw/7f5e04d51b3a6976eec099353f62cc07.png)
5. 将 [步骤3. ](#step3) 中的发信域名地址粘贴至 [DNS 解析 DNSPod](https://console.cloud.tencent.com/cns) 解析页面，完成添加记录，请避免空格。
 - DKIM 验证：
![](https://qcloudimg.tencent-cloud.cn/raw/db505d7e62fc62013e6d39d534dde126.png)
 - SPF 验证：
![](https://qcloudimg.tencent-cloud.cn/raw/c29031426e6fc6d7d8d073bb9bffea98.png)
 - _dmarc 记录：
记录值中填入 `v=DMARC1; p=none;rua=mailto:xxx@163.com;ruf=mailto:xxx@163.com;`
 <dx-alert infotype="explain"> `xxx@163.com`为示例，此处应填入您自己的发信地址。</dx-alert>
![](https://qcloudimg.tencent-cloud.cn/raw/64dc22f5ec2da2840115bb869a1ba95e.png)
- MX 记录：
![](https://qcloudimg.tencent-cloud.cn/raw/8727105c5607f0993f1668f63b130be4.png)
6. 再次回到 [发信域名](https://console.cloud.tencent.com/ses/domain) 配置详情页，单击**验证**即可。
![](https://qcloudimg.tencent-cloud.cn/raw/b65213aa84bd379a250084e72c8c3a34.png)
:::
::: 步骤二：验证结果
![](https://qcloudimg.tencent-cloud.cn/raw/275fb56fe9faa0a0ab3bd3735f3bd8c5.png)
![](https://qcloudimg.tencent-cloud.cn/raw/695ff02f3096d64481103a13e757362c.png)
![](https://qcloudimg.tencent-cloud.cn/raw/c9bc369664b4290a4048f94791f47209.png)

:::
::: 补充：当发信域名使用三级域名时

1. 通过 [发信域名](https://console.cloud.tencent.com/ses/domain) 设置页面，单击**新建域名**，填写域名后，提交即可。
2. 在 [DNS 解析 DNSPod 控制台](https://console.cloud.tencent.com/cns) 配置验证信息。
:::
</dx-tabs>

>?
>- 上面设定并校验后，仍然建发信域名有问题，请联系 [腾讯云技术人员](https://console.cloud.tencent.com/workorder/category) 解决。
>- 若注册了 Dnspod 解析，但是 dig 不到：可能域名实名认证未通过（注册局设置停止解析）。

