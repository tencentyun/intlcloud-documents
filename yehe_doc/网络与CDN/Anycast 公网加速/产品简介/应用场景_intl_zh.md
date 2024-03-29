腾讯云 Anycast 公网加速能实现 IP 传输的质量优化和多入口就近接入，下面将为您介绍其应用场景。
## 游戏加速
Anycast 的 IP 能起到游戏加速的作用：游戏请求就近接入腾讯云，通过腾讯云的内网到达游戏服务器，极大缩短经过的公网路径，减少了延时、抖动、丢包等问题的发生。跟传统加速比，IP 入口无需额外部署流量接收设备，且 IP 无需区分地域，简化了 DNS 部署。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/i2ne440_PRELIM__Anycast%20%E5%85%AC%E7%BD%91%E5%8A%A0%E9%80%9F_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-1.png)


## 视频直播互动
视频直播在跨地域传输的情况下还要求视频和语音清晰，无延迟，这就要求直播平台搭建覆盖多地域的专线网络和接入点。直播平台使用 AIA 服务后，可以直接利用腾讯云内网和 POP 点为直播用户服务，无需另外搭建专线网络。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/E7I3409_PRELIM__Anycast%20%E5%85%AC%E7%BD%91%E5%8A%A0%E9%80%9F_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-2.png)

## 金融服务
证券等金融服务要求很高的实时性，不稳定的公网传输无法满足需求。这类应用的接入层绑定 Anycast 公网加速的 IP 后，利用腾讯云内网传输能够实现多地域覆盖，同时 Anycast 公网加速服务还可以实现多地域同用一个 IP，简化了 IP 相关的审批工作，如备案、金融监管部门登记等。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/983d465_PRELIM__Anycast%20%E5%85%AC%E7%BD%91%E5%8A%A0%E9%80%9F_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-3.svg)

## 安全服务
安全清洗服务提供商、游戏、大型网站应用经常面临 Syn Flood、ICMP Flood 等各种大流量攻击。普通公网 IP 在单个地域发布，所有攻击流量都集中在一个出入口。使用 AIA 后，IP 在多地同时发布，无需改动 DNS 配置，攻击流量被导流到各个入口就近消化。
>?AIA 默认启用 DDoS 基础防护，使用 AIA 的 IP 拥有与普通 BGP IP 一样的 DDoS 基础防护能力，如需提升 DDoS 防护能力，可另行购买 [DDoS 高防包](https://www.tencentcloud.com/document/product/1029)。
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/RsuE490_PRELIM__Anycast%20%E5%85%AC%E7%BD%91%E5%8A%A0%E9%80%9F_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-4.svg)

