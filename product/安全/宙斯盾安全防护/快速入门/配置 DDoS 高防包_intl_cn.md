宙斯盾 DDoS 高防包可为腾讯云公网 IP 地址提供高防能力。包括 [云服务器](https://cloud.tencent.com/doc/product/213/495)、[负载均衡](https://cloud.tencent.com/doc/product/214/524)、黑石服务器、黑石负载均衡、NAT IP、EIP、GAAP IP 等。DDoS 高防包使用简单，对于业务不可更改 IP 地址，或者有大量 IP 需要防护的场景下，可以快速简单地完成防护配置。目前 DDoS 高防包有单 IP 模式和多 IP 模式。

本文档将详细说明 DDoS 高防包配置接入的步骤。如何选择购买配置，详情请参见 [**产品配置说明**](https://cloud.tencent.com/document/product/685/18798)。

## 流程图
![0](https://main.qcloudimg.com/raw/56680ef9138fe084b097b0ca753b9636.png)

## 接入步骤
1. **购买 DDoS 高防包**
a. 用户进入 [宙斯盾高防控制台](https://console.cloud.tencent.com/gamesec)，在左侧目录中，单击【DDoS 高防包】，在 “高防包列表” 的下，单击【购买】。
![1](https://main.qcloudimg.com/raw/df630ccec3cab14691171922384836c5.png)
b. 选择好配置，单击【立即下单】。
![2](https://main.qcloudimg.com/raw/4f15ff65dce6198d107f20dcc0868615.png)
2. **绑定防护 IP**
a. 在 “DDoS 高防包” 页面的【高防包列表】下，单击高防包 ID，进入基本信息页。
![6](https://main.qcloudimg.com/raw/ca821b16273f669683d0ba85b59dcfab.png)
b. 在 “DDoS 高防包详情” 页面下，单击【防护 IP 列表】，单击【添加防护 IP】。
![7](https://main.qcloudimg.com/raw/b5c3b51d527183481d6dc854757e463a.png)
c. 在 “添加防护 IP” 弹窗中，勾选好云服务器的 “IP 地址”，单击【确定】。
![8](https://i.imgur.com/MmGjqdM.png)
d. 添加成功后，在【防护 IP 列表】下，可以看到该 IP 地址即可以获得 DDoS 高防包防护了。
![9](https://main.qcloudimg.com/raw/1e6247686a49f9053ee801ce865638a7.png)
