端口转发表是 NAT 网关上的一张配置表，用于配置 NAT 网关上的 DNAT 功能，可将 VPC 内云服务器的 **[ 内网 IP，协议，端口 ]** 映射成 **[ 外网 IP，协议，端口 ]**，使得云服务器上的资源可被外网访问。
下面将为您详细介绍如何新建端口转发规则。

>?NAT 网关支持将同一个 EIP 同时用于配置端口转发规则和 SNAT 规则，SNAT 规则的详细信息请参考 [管理 SNAT 规则](https://intl.cloud.tencent.com/document/product/1015/39703)。
>
1. 登录 [NAT 网关控制台](https://console.cloud.tencent.com/vpc/nat?fromNav)。
2. 在列表中单击需要修改的 NAT 网关 ID 进入详情页，单击选项卡中的**端口转发**。
<img src="https://qcloudimg.tencent-cloud.cn/raw/899b2499c178d8ba1a8b6086bd399978.png" width="70%">
3. 单击**新建**，选择协议、外部端口 IP 及内部端口 IP 后，单击**确定**即可。
>!内部 IP 仅支持该 VPC 内的云服务器内网 IP。
>
![](https://qcloudimg.tencent-cloud.cn/raw/7e89db9a6122f50d4fc0ac55ad016684.png)

