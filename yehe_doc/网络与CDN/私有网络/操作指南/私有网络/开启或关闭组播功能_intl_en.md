This document describes how to enable or disable multicast for VPCs.

## Background
Broadcast and multicast are modes of one-to-many communication, which can save businesses on the network bandwidth and reduce network load through point-to-multipoint efficient data transmission.
In the unicast mode, the initiating server sends data to N servers separately. If the multicast mode, the server sends the same data to N servers in once, which reduces the server resource consumption and also the bandwidth resource of the backbone network.
>?
>- The trial period has ended. Please stay tuned for the official launch. 
>- Multicast and broadcast are available in Beijing, Shanghai, Guangzhou, Chengdu, Chongqing, Nanjing, Hong Kong, Singapore, Seoul, Tokyo, Bangkok, Toronto, Silicon Valley, Virginia and Frankfurt.
>- For single-VPC multicast and broadcast, up to 50,000 PPS and 190 Mbps are supported.
>

- Multicast: Tencent Cloud supports multicast on the VPC dimension.
- Broadcast: Tencent Cloud supports broadcast on the subnet dimension.

## Overview
Multicast and broadcast are mostly used in the financial and game industries:
- Broadcast services or market data of the financial industry. For example, after obtaining stock prices and other real-time data, brokers can broadcast stock data to multiple clients in real time, effectively reducing network load.
- For the game industry, broadcast and multicast are mainly used for heartbeat holding between multiple servers.

## How It Works
### Enabling multicast
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. In the VPC list, locate the target VPC, and toggle on **Multicast**.


### Disabling multicast
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. In the VPC list, locate the target VPC, and toggle off **Multicast**.

## More
For detailed directions regarding the subnet broadcast, see [Enabling/Disabling Broadcast](https://www.tencentcloud.com/document/product/215/31809).

