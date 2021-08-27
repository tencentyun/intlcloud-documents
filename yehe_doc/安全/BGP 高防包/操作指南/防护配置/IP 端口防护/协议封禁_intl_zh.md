
DDoS 高防支持对访问 DDoS 高防的源流量按照协议类型一键封禁。您可配置 ICMP 协议封禁、TCP 协议封禁、UDP 协议封禁和其他协议封禁，配置后相关访问请求会被直接截断。由于 UDP 协议的无连接性（如 TCP 具有三次握手过程）具有天然的不安全性缺陷，若您没有 UDP 业务，建议封禁 UDP 协议。

## 前提条件
您需要成功 [购买 DDoS 高防包](https://intl.cloud.tencent.com/document/product/1029/36115) ，并设置防护对象。

## 操作步骤
1. 登录 [DDoS 高防包（新版）管理控制台](https://console.cloud.tencent.com/ddos/antiddos-native/package)，在左侧导航中，单击【防护配置】。
2. 在左边的列表选中高防包的 ID，如“bgp-00xxxxxx”。
![](https://main.qcloudimg.com/raw/ceb4f1ebedc2efb78e428f5ffe071473.png)
3. 在右侧卡片中单击“协议封禁”卡片中的【设置】，进入协议封禁页面。
![](https://main.qcloudimg.com/raw/fa38ed5eb9bb5bcf4d1668f9b4c6d807.png)
4. 在“协议封禁”页面，单击【新建】，弹窗新建协议封禁弹窗。
![](https://main.qcloudimg.com/raw/10d37670faa7de3167d8cdeb4cf85e61.png)
5. 在新建协议封禁弹窗中，单击开启所需协议后，单击【确定】，创建协议封禁规则。
![](https://main.qcloudimg.com/raw/58a617dbd1909430bf41de75fe34ed39.png)
6.	新建完成后协议封禁列表，将新增一条协议封禁规则，可以在右侧操作列，单击【配置】，修改协议封禁规则。
![](https://main.qcloudimg.com/raw/da1c3776c49b90c1d6f8b7dca0f2c41a.png)
