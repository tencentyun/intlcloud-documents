This document describes NAT billing modes.
## Billing Description
NAT Gateway fees consist of the gateway usage (billed by hour) and the Internet access traffic.
- See **Billing Modes** below for gateway fees.
- For information on traffic fees, see bill-by-traffic in [Public Network Billing](https://intl.cloud.tencent.com/document/product/213/10578).

## Billing Modes
NAT Gateway is priced as follows:

| Configuration | Chinese mainland | Singapore, Silicon Valley, Virginia, Frankfurt, Hong Kong (China), Korea, Russia, and Japan | Mumbai | Toronto and Bangkok |
|-------------    | ---------------------------------------| -------------------------------------------------------- |-------------------| ----------- |
| Small             | 0.089                              | 0.13                                              | 0.18          | 0.14         |
| Medium             | 0.28                            | 0.39                                              | 0.54                                                 |0.42        |
| Large            | 0.89                        | 1.3                                               | 1.8                                               | 1.4         |



 >!
 >- NAT Gateway only supports [Bandwidth Package](https://intl.cloud.tencent.com/document/product/684/15245#ip-.E5.B8.A6.E5.AE.BD.E5.8C.85). NAT Gateway EIPs needs to be added to the bandwidth package for billing. [Check your account type](https://intl.cloud.tencent.com/document/product/684/15246) and select the bandwidth package beforehand.
 >- We recommend you to limit the outbound bandwidth of NAT Gateway to avoid high costs.
 >- NAT Gateway’s overdue payment policy follows that of pay-as-you-go CVM instances. For more information, see [Overdue Payment](https://intl.cloud.tencent.com/document/product/213/2181#.E6.8C.89.E9.87.8F.E8.AE.A1.E8.B4.B9.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8).
 >- NAT Gateway features dual-server hot backup. The system sends a 5 KB detection packet to the primary and secondary NAT Gateway servers every 3 seconds, thereby generating 0.2747 GB of traffic each day. The prices of the traffic in the Chinese mainland, Hong Kong (China), and North America are 0.032964 USD, 0.032964 USD and 0.0211519 USD respectively.
