

## A

### AI 引擎

[AI 引擎（Artificial Intelligence Engine）](https://intl.cloud.tencent.com/document/product/627/35645)指在 Web 应用防火墙中，应用的基于机器学习的 Web 攻击检测技术，通过 AI 引擎的自学习、自进化和自适应能力，最大限度提高已知和未知 Web 威胁的检测率和捕获率，最大限度减少误报，并且灵活适应不断变化的 Web 应用。

## C

### CC 攻击防护

[CC 攻击防护（Challenge Collapsar Protection）](https://intl.cloud.tencent.com/document/product/627/11709)指攻击者通过工具，模拟多个用户不断向网站发送连接请求，导致用户业务不可用，添加 CC 防护规则，可以帮助用户防护针对页面请求的 CC 攻击。

## D

### 代理服务

代理服务（Proxy Server） 是一种重要的服务器安全功能，主要用于开放系统互联（OSI）模型的会话层，提高访问速度，隐藏真实网站 IP，增加网站安全性。

### 地域封禁

[地域封禁（Territorial Prohibition）](https://intl.cloud.tencent.com/document/product/627/14704)指判断攻击 IP 所属地域，封禁攻击 IP 所属地域的其它 IP 的访问，以达到快速封禁来自地域的其它 IP 攻击请求的目的。

## F

### 防篡改

[防篡改（Tamper Proofing）](https://intl.cloud.tencent.com/document/product/627/11710)指客户把核心网页内容缓存到云端，并对外发布缓存中的网页内容，实现网页替身效果，当核心页面收到请求时，返回缓存在云端的内容。

### 防泄露

[防泄露（Anti Leakage）](https://intl.cloud.tencent.com/document/product/627/14582) 指通过检测响应页面中是否带有身份证号、手机号等敏感信息，发现敏感信息后，根据所设置的匹配动作对敏感信息进行观察或替换操作。其中，敏感信息过滤动作以 * 替换敏感信息部分，以达到防止用户敏感信息泄露的目的。

## H

### 回源 IP 地址

回源 IP 地址（Return Source IP Address）指客户添加域名成功后，Web 应用防火墙根据客户添加的域名，自动分配多个回源 IP 地址，回源 IP 地址作为 Web 应用防火墙的出口 IP，把经过过滤的正常访问流量，导向客户源站。

## S

### SSL 证书

SSL 证书指一种安全协议，目的是为互联网通信提供安全及数据完整性保障。SSL 证书遵循 SSL 协议，可安装在服务器上，实现数据传输加密。

## V

### VIP 地址

VIP 地址（Virtual IP Address）指客户添加域名成功后，Web 应用防火墙根据客户添加的域名，自动分配一个对应的 VIP 地址。当客户源站被访问时，VIP 地址成为 Web 应用防火墙入口地址，访问流量经过域名解析到 VIP 地址后，会全部导向 Web 应用防火墙。

## W

### WAF

参见 [Web 应用防火墙](https://intl.cloud.tencent.com/document/product/627/35644#1297)

### Web 应用防火墙

腾讯云 Web 应用防火墙（Web Application Firewall，WAF）是一款基于 AI 的一站式 Web 业务运营风险防护方案。通过 AI+规则双引擎识别恶意流量，保护网站安全，提高 Web 站点的安全性和可靠性。通过 BOT 行为分析，防御恶意访问行为，保护网站核心业务安全和数据安全。

## Y

### 域名解析

域名解析（Domain Name Resolution）指互联网上的机器相互间通过 IP 地址来建立通信，但是人们大多数习惯记忆域名，将 IP 地址与域名之间建立一对多的关系，而它们之间转换工作的过程称为域名解析。
常用域名解析类型：

- A 记录解析：用来指定域名的 IPv4 地址。
  - 记录类型：选择 “A”。
  - 记录值：填写腾讯云提供的主机 IP 地址。
  - MX 优先级：不需要设置。
  - TTL ：设置默认600。
- CNAME 记录解析：将域名指向另一个域名，再由另一个域名来提供 IP 地址。
  - 记录类型：选择 “CNAME”。
  - 记录值：填写 Web 应用防火墙添加防护域名后的 CNAME 值。
  - MX 优先级：不需要设置。
  - TTL ：设置默认600。
