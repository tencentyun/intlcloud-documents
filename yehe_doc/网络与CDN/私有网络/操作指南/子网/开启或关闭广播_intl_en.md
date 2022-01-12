## Background
Multicast and broadcast are modes of one-to-many communication, which can help enterprises reduce network bandwidth consumption and network load through point-to-multipoint efficient data transmission.
In the unicast mode, the initiating server sends data to N servers separately. If the multicast mode, the server sends the same data to N servers in once, which reduces the server resource consumption and also the bandwidth resource of the backbone network.
- Multicast: Tencent Cloud supports multicast on the VPC dimension.
- Broadcast: Tencent Cloud supports broadcast on the subnet dimension.

>?
>- The broadcast and multicast features are currently in beta test. If you do need to use them, please [submit an application](https://console.cloud.tencent.com/workorder/category).
>- At present, the regions supporting multicast and broadcast are: Beijing, Shanghai, Guangzhou, Chengdu, Chongqing, Nanjing, Hong Kong of China, Singapore, Seoul, Tokyo, Mumbai, Bangkok, Toronto, Silicon Valley, Virginia, Frankfurt and Moscow.
>

## Overview
Multicast and broadcast are mostly used in the financial and game industries:
- Broadcast services or market data of the financial industry. For example, after obtaining stock prices and other real-time data, brokers can broadcast stock data to multiple clients in real time, effectively reducing network load.
- For the game industry, broadcast and multicast are mainly used for heartbeat holding between multiple servers.

This document describes how to enable or disable broadcast for subnets.

## Directions
### Enabling broadcast
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click **Subnet** on the left sidebar to access the admin page.
3. In the VPC list, locate the target VPC, and toggle on **Enable** under the **Subnet broadcast** column.
![]()

### Disabling broadcast
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click **Subnet** on the left sidebar to access the admin page.
3. In the VPC list, locate the target VPC, and toggle on **Disable** under the **Subnet broadcast** column.
![]()

## References
For more information about the VPC-level multicast, see [Enabling or Disabling Multicast](https://intl.cloud.tencent.com/document/product/215/40072).

