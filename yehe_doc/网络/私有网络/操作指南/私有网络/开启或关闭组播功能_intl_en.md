This document describes how to enable or disable multicast for VPCs.

## Background
Multicast and broadcast are modes of one-to-many communication, which can help enterprises reduce network bandwidth consumption and network load through point-to-multipoint efficient data transmission.
If unicast is used, the sending server needs to separately send to N servers for total N times. If multicast is used, the server sends the same data to N servers only once, which reduces server resource consumption and also bandwidth resources of the backbone network.
>?The broadcast and multicast features are currently in beta. To try it out, please submit an application.
>
- Multicast: Tencent Cloud provides multicast in a VPC.
- Broadcast: Tencent Cloud provides broadcast in a subnet.

## Use Cases
Multicast and broadcast are mostly used in the financial and game industries:
- Broadcast services or market data of the financial industry. For example, after obtaining stock prices and other real-time data, brokers can broadcast stock data to multiple clients in real time, effectively reducing network load.
- For the game industry, broadcast and multicast are mainly used for heartbeat holding between multiple servers.

## Instructions
### Enabling multicast
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. In the VPC list, locate the VPC for which you want to enable multicast, and click **Enable** under the **Multicast** column.


### Disabling multicast
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. In the VPC list, locate the VPC for which you want to disable multicast, and click **Disable** under the **Multicast** column.


## Relevant Operations
For detailed directions regarding the subnet broadcast, see [Enabling or Disabling the Broadcasting and Multicasting](https://intl.cloud.tencent.com/document/product/215/31809).

