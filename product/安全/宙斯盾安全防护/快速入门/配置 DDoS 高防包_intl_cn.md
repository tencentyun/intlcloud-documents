宙斯盾 DDoS 高防包可为腾讯云公网 IP 地址提供高防能力。包括 [云服务器](https://cloud.tencent.com/doc/product/213/495)、[负载均衡](https://cloud.tencent.com/doc/product/214/524)、黑石服务器、黑石负载均衡、NAT IP、EIP、GAAP IP 等。DDoS 高防包使用简单，对于业务不可更改 IP 地址，或者有大量 IP 需要防护的场景下，可以快速简单地完成防护配置。目前 DDoS 高防包有单 IP 模式和多 IP 模式。

本文档将详细说明 DDoS 高防包配置接入的步骤。如何选择购买配置，详情请参见 [**产品配置说明**](https://cloud.tencent.com/document/product/685/18798)。

## 流程图
![0](https://main.qcloudimg.com/raw/56680ef9138fe084b097b0ca753b9636.png)

## 接入步骤
1. **购买 DDoS 高防包**
a. 用户进入 [宙斯盾高防控制台](https://console.cloud.tencent.com/gamesec)，在左侧目录中，单击【DDoS 高防包】，在 “高防包列表” 的下，单击【购买】。
![1](https://i.imgur.com/TBrDbFu.png)
b. 选择好配置，单击【立即下单】。
![2](https://i.imgur.com/R8NhTNf.png)
2. **绑定防护 IP**
a. 在 “DDoS 高防包” 页面的【高防包列表】下，单击高防包 ID，进入基本信息页。
![6](https://i.imgur.com/0hr040S.png)
b. 在 “DDoS 高防包详情” 页面下，单击【防护 IP 列表】，单击【添加防护 IP】。
![7](https://i.imgur.com/bHv4nvt.png)
c. 在 “添加防护 IP” 弹窗中，勾选好云服务器的 “IP 地址”，单击【确定】。
![8](https://i.imgur.com/MmGjqdM.png)
d. 添加成功后，在【防护 IP 列表】下，可以看到该 IP 地址即可以获得 DDoS 高防包防护了。
![9](https://i.imgur.com/FezkAQ5.png)
