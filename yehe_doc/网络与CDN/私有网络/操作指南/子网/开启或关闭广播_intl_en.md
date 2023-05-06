## Background
Broadcast and multicast are modes of one-to-many communication, which can save businesses on the network bandwidth and reduce network load through point-to-multipoint efficient data transmission.
In the unicast mode, the initiating server sends data to N servers separately. If the multicast mode, the server sends the same data to N servers in once, which reduces the server resource consumption and also the bandwidth resource of the backbone network.
- Multicast: Tencent Cloud supports multicast on the VPC dimension.
- Broadcast: Tencent Cloud supports broadcast on the subnet dimension.

>?
>- The trail period of VPC has 
>- Multicast and broadcast are available in Beijing, Shanghai, Guangzhou, Chengdu, Chongqing, Nanjing, Hong Kong, Singapore, Seoul, Tokyo, Bangkok, Toronto, Silicon Valley, Virginia and Frankfurt.
>- For single-VPC multicast and broadcast, up to 50,000 PPS and 190 Mbps are supported.
>

## Scenarios
Multicast and broadcast are mostly used in the financial and game industries:
- Broadcast services or market data of the financial industry. For example, after obtaining stock prices and other real-time data, brokers can broadcast stock data to multiple clients in real time, effectively reducing network load.
- For the game industry, broadcast and multicast are mainly used for heartbeat holding between multiple servers.

 

## Directions
### Enabling broadcast
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click **Subnet** on the left sidebar.
3. In the VPC list page, locate the target VPC, and toggle on **Subnet broadcast**.

### Disabling broadcast
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Click **Subnet** on the left sidebar.
3. In the VPC list page, locate the target VPC, and toggle off **Subnet broadcast**.


## Related Operations
For information about VPC-level multicast, see [Enabling/Disabling Multicast](https://www.tencentcloud.com/document/product/215/40072).

