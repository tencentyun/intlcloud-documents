Before creating a CVD instance, you need to select a [VPC](https://www.tencentcloud.com/document/product/215), which serves as a dedicated cloud network space to sustain CVD resources to improve the resource security in different scenarios.
After you configure the CVD network based on VPC, CVD instances can access other businesses or Tencent Cloud services, the public network, and other VPCs.
## VPC Creation

CVD needs to work with VPC, so you need to [create a VPC](https://intl.cloud.tencent.com/document/product/215/31805) first. After a CVD instance is created, its VPC and subnet cannot be changed.

## CVD Access to Other VPCs
### Peering Connection
You can leverage [Peer Connection](https://www.tencentcloud.com/document/product/553) to connect a CVD instance to another **VPC**. Peer Connection supports VPC interconnection under the same account and across accounts. You can create a peer connection for your CVD instance as instructed in:
- [Connecting Network Instances Under the Same Account](https://intl.cloud.tencent.com/document/product/1003/31986)
- [Creating Cross-account Peering Connection](https://intl.cloud.tencent.com/document/product/553/35190)

### CCN
You can leverage [CCN](https://www.tencentcloud.com/document/product/1003) to connect a CVD instance to **two or more VPCs**. CCN supports VPC interconnection under the same account and across accounts. You can create a CCN instance for your CVD instance as instructed in:
- [Connecting Network Instances Under the Same Account](https://intl.cloud.tencent.com/document/product/1003/31986)
- [Connecting Network Instances Across Accounts](https://intl.cloud.tencent.com/document/product/1003/31987)

## CVD Access to the Internet via NAT Gateway
[NAT Gateway](https://www.tencentcloud.com/document/product/1015) is an IP translation service. You can bind an [elastic IP (EIP)](https://www.tencentcloud.com/document/product/213/16586) to provide secure and high-performance internet access for your CVD instance in the VPC.
>?When creating a NAT gateway, select the correct VPC and configure the routing rules to route subnet traffic to the NAT gateway.

For detailed directions on how to configure NAT Gateway, see:
- [Getting Started](https://intl.cloud.tencent.com/document/product/1015/30251)
- [Modifying NAT Gateway Configuration](https://intl.cloud.tencent.com/document/product/1015/30239)
- [Managing EIPs of NAT Gateway](https://intl.cloud.tencent.com/document/product/1015/30240)
- [Managing SNAT Rules](https://intl.cloud.tencent.com/document/product/1015/39703)
- [Managing Port Forwarding Rules](https://www.tencentcloud.com/document/product/1015/39942)
- [Routing to NAT Gateway](https://intl.cloud.tencent.com/document/product/1015/30236)
