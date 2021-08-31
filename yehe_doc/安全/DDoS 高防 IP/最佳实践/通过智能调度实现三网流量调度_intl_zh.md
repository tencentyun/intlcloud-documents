本文档将为您介绍如何通过智能调度实现三网流量调度。
## 操作场景
当 [购买三网的高防 IP](https://buy.cloud.tencent.com/antiddos#/advanced) 后，比较常见的业务流量调度方式是根据 DNS 请求的运营商来源进行转发，即来自电信的流量调度到电信高防 IP、来自联通的流量调度到联通高防 IP、来自移动的流量调度到移动高防 IP、来自其他运营商的流量调度到优先级最高的高防线路，您可以通过配置智能调度，实现上述场景。

## 前提条件
- 在开启智能调度前，请将需要防护的业务接入高防实例进行防护。
>?
>- 若您需要将防护的云上产品 IP 添加至已购买的高防包实例，请参见 DDoS 高防包 [快速入门](https://intl.cloud.tencent.com/document/product/1029/36116)。
>- 若您需要将四层或七层业务添加至已购买的 DDoS 高防 IP 实例，请参见 DDoS 高防 IP [端口接入](https://intl.cloud.tencent.com/document/product/297/37221) 或 [域名接入](https://intl.cloud.tencent.com/document/product/297/37222) 。


- 在修改 DNS 解析前，您需要成功购买域名解析产品。


## 操作步骤
1. 登录 [DDoS 高防 IP（新版）控制台](https://console.cloud.tencent.com/ddos/antiddos-advanced/overview)，在左侧导航栏，单击【智能调度】，进入列表页面，单击【新建调度】，系统自动生成一个 CNAME 记录。
2. 找到该 CNAME 记录所在行，单击【添加高防实例】，进入智能调度编辑页面。
3. 在智能调度编辑页面中，TTL 值默认60秒，取值范围为1（秒）- 3600（秒），调度方式为默认优先级。
4. 单击【添加高防资源IP】，勾选需要设置智能调度的高防实例及IP，单击【确定】。
5. 选择高防实例后，实例的高防线路默认开启域名解析，再为其设置优先级。
>?
>- 三条运营商线路的优先级配置要相同，保证按照 DNS 请求的运营商来源进行响应。
>- 关于智能调度的配置，请参见 [配置智能调度](https://intl.cloud.tencent.com/document/product/297/37229)。
>

