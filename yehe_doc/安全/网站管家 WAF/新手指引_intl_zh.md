本文将为刚入门 Web 应用防火墙（Web Application Firewall，WAF）的用户提供一条学习路径。
## 1. 熟悉 WAF 的基础知识
- [WAF 具备哪些功能？](https://intl.cloud.tencent.com/document/product/627/17470)
- [为什么选择 WAF？](https://intl.cloud.tencent.com/document/product/627/17470#.E4.B8.BA.E4.BD.95.E9.9C.80.E8.A6.81-web-.E5.BA.94.E7.94.A8.E9.98.B2.E7.81.AB.E5.A2.99)
- [WAF 有哪些应用场景？](https://intl.cloud.tencent.com/document/product/627/13514)
- [如何选择 WAF 使用版本？](https://intl.cloud.tencent.com/document/product/627/34717)
- [WAF 支持在哪些地域使用？](https://intl.cloud.tencent.com/document/product/627/38085)
-----

## 2. WAF 的计费模式
腾讯云 WAF 提供两种产品形态，**SaaS 型 WAF** 和**负载均衡型 WAF**，两种 WAF 计费项目基本相同，且计费模式与价格相同，详情请参见 [购买指南](https://intl.cloud.tencent.com/zh/document/product/627/11730)。
您可以根据不同接入方式选择购买不同类型的 WAF。

-----
## 3. 新手入门
#### 3.1 了解 WAF 各版本功能
腾讯云 WAF 提供两种产品形态，**SaaS 型 WAF** 和**负载均衡型 WAF**，不同版本所提供的主要功能不同，详情请参见 [产品分类](https://intl.cloud.tencent.com/document/product/627/34717)。

#### 3.2 购买 WAF
您可以在 [Web 应用防火墙购买页](https://buy.cloud.tencent.com/buy/waf) 选购产品。

#### 3.3 接入 WAF
腾讯云 WAF 分为两种类型，**SaaS 型 WAF** 和**负载均衡型 WAF**，两种类型 WAF 域名接入方式不同，详情请参见 [入门概述](https://intl.cloud.tencent.com/document/product/627/18635)。


#### 3.4 相关实践
WAF 可在某些特定场景进行使用，同时可结合腾讯云其他产品为您提供安全防护：
- [WAF 与 DDoS 高防包结合应用](https://intl.cloud.tencent.com/zh/document/product/627/34723)
- [WAF 结合 API 网关提供安全防护](https://intl.cloud.tencent.com/document/product/627/38375)
- [HTTPS 免费证书申请和应用](https://intl.cloud.tencent.com/document/product/627/34724)

-----
## 4. 控制台功能概述

| 如果您想 | 您可以阅读 |
|---------|---------|
|查看 WAF 防护域名的访问日志信息。 | [访问日志](https://intl.cloud.tencent.com/document/product/627/35648) |
|按照过滤条件进行查询 Web 攻击日志信息，并下载查询结果。|[攻击日志](https://intl.cloud.tencent.com/document/product/627/35649) |
|开启紧急模式 CC 防护或自定义 CC 防护策略。|[CC 防护设置2.0](https://intl.cloud.tencent.com/document/product/627/11709)|
|防止发生指定页面被篡改而显示异常的问题|[网页防篡改](https://intl.cloud.tencent.com/document/product/627/11710)|
|通过自定义策略组合出有针对性的规则，来阻断各类攻击行为。|[自定义策略](https://intl.cloud.tencent.com/document/product/627/11711)|
|将网页中返回的敏感信息进行替换，防止信息泄露。|[防信息泄露](https://intl.cloud.tencent.com/document/product/627/14582)|
|对境外国家和地区以及中国各大省份和地区进行黑名单封禁，阻断该区域的所有访问来源。|[地域封禁](https://intl.cloud.tencent.com/document/product/627/14704)|
|对友好及恶意机器人程序进行甄别分类，并采取针对性的流量管理策略。| [BOT 行为管理](https://intl.cloud.tencent.com/document/product/627/15340)|
|对已知和未知 Web 威胁进行检测和捕获。|[AI 引擎](https://intl.cloud.tencent.com/document/product/627/35645)|
|对经过 WAF 防护域名的访问源 IP 进行状态查询和黑白名单设置。|[IP 管理](https://intl.cloud.tencent.com/document/product/627/35646)|

----------------
## 5. 新手常见问题
[非腾讯云内的服务器能否使用 WAF？](https://intl.cloud.tencent.com/document/product/627/11731)
[WAF 是否支持 HTTPS 防护？](https://intl.cloud.tencent.com/document/product/627/11731#waf-.E6.98.AF.E5.90.A6.E6.94.AF.E6.8C.81-https-.E9.98.B2.E6.8A.A4.EF.BC.9F)
[WAF 的源站 IP 可以填写腾讯云 CVM 内网 IP 吗？](https://intl.cloud.tencent.com/document/product/627/11731#waf-.E7.9A.84.E6.BA.90.E7.AB.99-ip-.E5.8F.AF.E4.BB.A5.E5.A1.AB.E5.86.99.E8.85.BE.E8.AE.AF.E4.BA.91-cvm-.E5.86.85.E7.BD.91-ip-.E5.90.97.EF.BC.9F)
[如何接入域名？](https://intl.cloud.tencent.com/document/product/627/35778)
[WAF 是否支持泛域名接入？](https://intl.cloud.tencent.com/document/product/627/35778#waf.E6.98.AF.E5.90.A6.E6.94.AF.E6.8C.81.E6.B3.9B.E5.9F.9F.E5.90.8D.E6.8E.A5.E5.85.A5.EF.BC.9F)

--------

## 6. 反馈与建议
使用腾讯云 WAF 产品和服务中有任何问题或建议，您可以通过以下渠道反馈，将有专人跟进解决您的问题：
- 如果发现产品文档的问题，如链接、内容、API 错误等，您可以单击文档页右侧 【文档反馈】或选中存在问题的内容进行反馈。
- 如果遇到产品相关问题，您可 [提交工单](https://console.cloud.tencent.com/workorder/category?level1_id=141&level2_id=642&source=0&data_title=T-Sec-Web%E5%BA%94%E7%94%A8%E9%98%B2%E7%81%AB%E5%A2%99&step=1) 寻求帮助。
