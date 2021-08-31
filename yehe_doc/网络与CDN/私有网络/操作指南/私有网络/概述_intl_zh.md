私有网络（VPC） 是您在腾讯云上可以独享并可自主规划的一个完全逻辑隔离的网络空间，在使用云资源之前，您必须先创建一个私有网络和子网。子网是私有网络中的一个网络空间，私有网络具有地域属性，子网具有可用区属性，一个私有网络内至少包含一个子网，您可以在一个私有网络中创建多个子网来划分网络，同一私有网络中的子网默认内网互通。

云服务器、负载均衡等云资源必须部署在子网内，不能直接部署在私有网络中。


## 背景信息
根据不同的使用需求，VPC 的使用生命周期如下图所示：
![](https://main.qcloudimg.com/raw/68556cee99a7ececc3936b45cdaa3ca5.svg)
1. [创建私有网络](https://intl.cloud.tencent.com/document/product/215/31805)：创建 VPC 前，您需要提前做好 [网络规划](https://intl.cloud.tencent.com/document/product/215/31795)。VPC 和子网的 CIDR 创建后不可更改。
2. [查看私有网络](https://intl.cloud.tencent.com/document/product/215/40069)：可查看 VPC 的基本信息、云联网的关联情况以及包含资源。
3. （可选）根据实际使用场景选择不同操作：
 - 主 CIDR 不够分配时，参考[ 编辑IPv4 CIDR](https://intl.cloud.tencent.com/document/product/215/40070)：
    - [创建辅助 CIDR](https://intl.cloud.tencent.com/document/product/215/40070#21)：主 CIDR 不够分配时，可以创建辅助 CIDR 以满足实际网络需求。
    - [删除辅助 CIDR](https://intl.cloud.tencent.com/document/product/215/40070#32)：若不需要辅助 CIDR，可将其删除。
4. [删除私有网络](https://intl.cloud.tencent.com/document/product/215/40073)：删除 VPC 后，该 VPC 下的子网和路由表将一并被删除。

