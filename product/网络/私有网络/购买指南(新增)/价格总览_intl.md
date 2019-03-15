## Overview

#### Free products:

- VPC, Subnet, Route Table, Network ACL, Security Group, Direct Connect Gateway, VPN Tunnel, Customer Gateway are available free of charge.
- Intra-region private connection is free of charge. 
- The pricing of Tencent Cloud services (Cloud Virtual Machine, TencentDB for MySQL, etc) for VPC is the same as that of regular network. 

#### Paid products:

- There is a cost to communicate on public networks. For more details, see communication via public networks charges.
- For charges of NAT gateway, VPN gateway, and cross-region peering connection, see the following sections.

## NAT Gateway

NAT gateway fees include the gateway rental fee (billed hourly) and iccured Internet access traffic:

| Billable Item | Specification | Mainland China | Hong Kong, Singapore, South Korea, Frankfurt, Silicon Valley & Bangkok | Toronto & Mumbai | Virginia |
| ---------------------------------- | ------------------------ | -------------------- | ------------------------------------------------------------ | --------------- | -------- |
| Gateway Rental Fee (USD/hour) | Small (1,000,000 connections maximum) | 0.089                | 0.13                                                         | 0.14            | 0.18     |
| Gateway Rental Fee (USD/hour) | Medium (3,000,000 connections maximum) | 0.28                 | 0.39                                                         | 0.42            | 0.54     |
| Gateway Rental Fee (USD/hour) | Large (5,000,000 connections maximum) | 0.89                 | 1.3                                                          | 1.4             | 1.8      |

Iccured Internet access traffic fees:

| Billable Item | Mainland China, Hong Kong, South Korea | Toronto, Frankfurt & Silicon Valley | Singapore | Virginia & Mumbai | Bangkok |
| ---------------------------------- | -------------------------------------- | ---------------------------------- | --------- | ---------------- | ------- |
| Internet Access Traffic (USD/GB) | 0.12                                   | 0.077                              | 0.081     | 0.1              | 0.075   |

> Note:
>
> - For those who have a bandwidth sharing package, NAT gateway-generated outbound traffic will be covered by the package (network traffic will not be charged again). It is recommended that you limit the NAT gateway outbound bandwidth to avoid excessive bandwidth package fee. For more information, see bandwidth package billing.
> - Past due rule is the same as CMV.
> - As the NAT gateway features master/slave hot backup, a 5 KB detection packet to the master/slave servers of the NAT gateway every three seconds, which incurs a traffic of 0.2747 GB/day.

## VPN Connection

VPN tunnels and customer gateway are free of charge. VPN gateway is not free. Charges include a gateway rental fee (see below) and Internet traffic fee. For more information, see [Public Network Billing Methods](https://cloud.tencent.com/document/product/213/10578#.E6.8C.89.E6.B5.81.E9.87.8F.E8.AE.A1.E8.B4.B912).

| Region | Mainland China | Hong Kong, Korea, Frankfurt, Silicon Valley, Virginia & Mumbai | Singapore, Toronto & Bangkok |
| ---- | -------------------- | ------------------------------------------------------------ | --------------------------- |
| Price (USD/hr) | 0.078                | 0.088                                                        | 0.12                        |

## Peering Connection

- Intra-region peering connection is available for free.

- Cross-region peering connection and cross-region interconnection over a basic network:

  - Postpaid on a daily basis. Payment is borne by the peering connection initiator.
  - Calculated as the peak bandwidth of the day multiplied by the applicable tiered price.
  - Peak bandwidth of the day is calculated as follows: Inbound/outbound bandwidth is captured every 5 minutes, and the maximum is taken as the peak bandwidth.

For more information, see the following table:

| Feature | Billing Method | Configuration | Price | | |
| -------------- | ------------------------------------------------------------ | ----------------- | ------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
|                |           | | Connection in Mainland China (all regions) | Connection between Mainland China (all regions) and regions outside Mainland China (Hong Kong, Korea, Frankfurt, Silicon Valley, Virginia, Mumbai, Singapore, Toronto & Bangkok) | Connection between regions outside Mainland China (Hong Kong, Korea, Frankfurt, Silicon Valley, Virginia, Mumbai, Singapore, Toronto & Bangkok) |
| Intra-region peering connection | Free | Free | Free | Free | Free |
| Cross-region peering connection | Peak bandwidth of the day billed on a daily basis (USD/Mbps/day). Peak bandwidth is calculated using the average bandwidth per 5 minutes | (0 , 20] Mbps     | 3.19                     | 15                                                           | 15                                                           |
|                |                                                              | (20 ,100] Mbps    | 1.98                     | 12                                                           | 12                                                           |
|                |                                                              | (100 , 500] Mbps  | 1.48                     | 9                                                            | 9                                                            |
|                |                                                              | (500 , 2000] Mbps | 1.19                     | 6                                                            | 6                                                            |
|                |                     | Over 2,000 Mbps  | 0.82                     | 5                                                            | 5                                                            |
