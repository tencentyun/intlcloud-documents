This document describes how to enable or disable multicast for VPCs.

## Background
Broadcast and multicast are modes of one-to-many communication, which can save businesses on the network bandwidth and reduce network load through point-to-multipoint efficient data transmission.
In the unicast mode, the initiating server sends data to N servers separately. If the multicast mode, the server sends the same data to N servers in once, which reduces the server resource consumption and also the bandwidth resource of the backbone network.
>?
>- The broadcast and multicast features are currently in beta test. If you do need to use them, please [submit an application](https://console.cloud.tencent.com/workorder/category).
>- At present, the regions supporting multicast and broadcast are: Beijing, Shanghai, Guangzhou, Chengdu, Chongqing, Nanjing, Hong Kong of China, Singapore, Seoul, Tokyo,  Bangkok, Toronto, Silicon Valley, Virginia, Frankfurt and Moscow.
>

- Multicast: Tencent Cloud supports multicast on the VPC dimension.
- Broadcast: Tencent Cloud supports broadcast on the subnet dimension.

## Overview
Multicast and broadcast are mostly used in the financial and game industries:
- Broadcast services or market data of the financial industry. For example, after obtaining stock prices and other real-time data, brokers can broadcast stock data to multiple clients in real time, effectively reducing network load.
- For the game industry, broadcast and multicast are mainly used for heartbeat holding between multiple servers.

## Directions
### Enabling multicast
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. In the VPC list, locate the desired VPC, and toggle on **Multicast**.
![]()


### Disabling multicast
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. In the VPC list, locate the desired VPC, and toggle off **Multicast**.
![]()

## References
For more information about the subnet-level broadcasting, see [Enabling or Disabling Broadcast](https://intl.cloud.tencent.com/document/product/215/31809).

