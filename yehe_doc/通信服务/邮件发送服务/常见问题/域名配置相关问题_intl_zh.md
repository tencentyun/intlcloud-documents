## 域名配置相关问题
#### 创建域名有什么限制？
-   每个腾讯云账户最多可以验证 5 个发信域名。建议您创建 2 个不同的域名，用来区分触发邮件和批量邮件。
    
-   建议您使用子域名，避免因为外发信誉等问题影响主域名。可以创建一个企业邮箱域名的子域名作为邮件推送发送域名。
    
-   已通过所有验证项的域名不可删除。
    
-   一个主域名及其所有子域名，只能被一个腾讯云账号作为发信域名使用。

#### 为什么需要验证域名？各项配置的作用是什么？
验证域名的作用是验证您对域名的所有权，避免他人伪造使用您的域名发送垃圾邮件，并同时向邮件服务商验证身份，提高邮件的送达率。

SPF、DKIM以及DMARC验证主要用于保障发送邮件时的安全，MX验证用于接收来自收件人的回信，它们的具体功能如下：
-   SPF 验证  
    发件人策略框架 (SPF) 是一种电子邮件验证标准，旨在防止电子邮件欺骗。域所有者使用 SPF 来告知电子邮件提供商，允许哪些服务器从其域发送电子邮件。
    
-   DKIM 验证
	域名秘钥识别邮件 (DKIM) 是一种允许发件人使用加密密钥为其电子邮件签名的标准。然后，电子邮件提供商使用这些签名来验证这些邮件在传输过程中是否未被第三方修改。
	
-   DMARC 验证
	基于域的消息身份验证、报告和合规性 (DMARC) 是一种电子邮件身份验证协议，它使用发件人策略框架 (SPF) 和域名密钥识别邮件 (DKIM) 来检测电子邮件欺骗。为了符合 DMARC 标准，邮件必须通过 SPF 和/或 DKIM 进行身份验证。

-   MX 验证  
    邮件交换记录 (MX)，它指向一个邮件服务器。用于电子邮件系统发邮件时根据收信人的地址后缀来定位邮件服务器。

#### 如何在 DNS 服务器上配置域名？
本文介绍在 DNS 服务器上如何进行域名解析绑定邮件发送服务。

首先，登录  [邮件发送控制台](https://console.cloud.tencent.com/dms)，创建需验证的域名，单击对应域名的【配置】操作查看域名配置信息。

然后，登录您的域名注册商网站，将您查询的域名配置记录值逐条添加域名解析。

更新 DNS 记录的步骤因您使用的 DNS 或 Web 托管提供商而异。下表列出了指向几个常用提供商的文档的链接。此列表并不详尽，并且其中包含的内容不是对任何公司的产品或服务的认可或推荐。
| DNS/托管提供商 |文档链接  |
|--|--|
| Tencent Cloud | [TXT 记录](https://cloud.tencent.com/document/product/302/12648)（仅支持中文）|
| AWS | [基本记录的值](https://docs.aws.amazon.com/zh_cn/Route53/latest/DeveloperGuide/resource-record-sets-values-basic.html)（外部链接） |
| GoDaddy | [添加 TXT 记录](https://www.godaddy.com/help/add-a-txt-record-19232)（外部链接） |
| Dreamhost | [如何添加自定义 DNS 记录？](https://help.dreamhost.com/hc/en-us/articles/215414867-How-do-I-add-custom-DNS-records-)（外部链接） |
| Cloudflare | [在 CloudFlare 中管理 DNS 记录](https://support.cloudflare.com/hc/en-us/articles/360019093151)（外部链接） |
| HostGator | [通过 HostGator/eNom 管理 DNS 记录](https://support.hostgator.com/articles/hosting-guide/lets-get-started/dns-name-servers/manage-dns-records-with-hostgatorenom)（外部链接） |
| Namecheap | [如何为我的域添加 TXT/SPF/DKIM/DMARC 记录？](https://www.namecheap.com/support/knowledgebase/article.aspx/317/2237/how-do-i-add-txtspfdkimdmarc-records-for-my-domain)（外部链接） |
| Names.co.uk | [更改您的域的 DNS 设置](https://www.names.co.uk/support/1156-changing_your_domains_dns_settings.html)（外部链接） |
| Wix | [在您的 Wix 账户中添加或更新 TXT 记录](https://support.wix.com/en/article/adding-or-updating-txt-records-in-your-wix-account)（外部链接） |


#### 域名配置的 DNS 记录能否修改？
发信域名验证成功后，DNS 记录不能修改或删除。否则可能会导致某些收件服务器拒收，影响邮件到达。