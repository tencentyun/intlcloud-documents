## Background
Multicast and broadcast are modes of one-to-many communication, which can help enterprises reduce network bandwidth consumption and network load through point-to-multipoint efficient data transmission.
If unicast is used, the sending server needs to separately send to N servers for total N times. If multicast is used, the server sends the same data to N servers only once, which reduces server resource consumption and also bandwidth resources of the backbone network.
- Multicast: Tencent Cloud supports multicast on the VPC dimension.
- Broadcast: Tencent Cloud supports broadcast on the subnet dimension.

>?
>- The broadcast and multicast features are currently in beta phase. To become a beta user, please submit an application for broadcast or multicast.
>- Currently, the broadcast and multicast features are available in Beijing, Shanghai, Guangzhou, Nanjing, Chengdu, Chongqing, and Hong Kong, China.
>

## Overview
Multicast and broadcast are mostly used in the financial and game industries:
- Broadcast services or market data of the financial industry. For example, after obtaining stock prices and other real-time data, brokers can broadcast stock data to multiple clients in real time, effectively reducing network load.
- For the game industry, broadcast and multicast are mainly used for heartbeat holding between multiple servers.

This document describes how to enable or disable broadcast for subnets.

## Directions
### Enabling broadcast
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click **Subnet** on the left sidebar to access the management page.
3. In the VPC list, locate the VPC for which you want to enable broadcast, and slide to **Enable** under the **Subnet broadcast** column.

### Disabling broadcast
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click **Subnet** on the left sidebar to access the management page.
3. In the VPC list, locate the VPC for which you want to disable broadcast, and slide to **Disable** under the **Subnet broadcast** column.

## Relevant Operations
For detailed directions regarding VPC multicast, see [Enabling or Disabling Multicast](https://intl.cloud.tencent.com/document/product/215/40072).

