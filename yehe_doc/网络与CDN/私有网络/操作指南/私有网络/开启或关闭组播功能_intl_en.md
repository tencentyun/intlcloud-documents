This document describes how to enable or disable multicast for VPCs.

## Background
Multicast and broadcast are modes of one-to-many communication, which can help enterprises reduce network bandwidth consumption and network load through point-to-multipoint efficient data transmission.
If unicast is used, the sending server needs to separately send to N servers for total N times. If multicast is used, the server sends the same data to N servers only once, which reduces server resource consumption and also bandwidth resources of the backbone network.
>?
>- The broadcast and multicast features are currently in beta phase. To become a beta user, please submit an application for broadcast or multicast.
>- Currently, the broadcast and multicast features are available in Beijing, Shanghai, Guangzhou, Nanjing, Chengdu, Chongqing, and Hong Kong, China.
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


### Disabling multicast
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. In the VPC list, locate the desired VPC, and toggle off **Multicast**.

## Relevant Operations
For detailed directions regarding the subnet broadcast, see [Enabling or Disabling Broadcast](https://intl.cloud.tencent.com/document/product/215/31809).

