Broadcasting and multicast are modes of one-to-many communication, which can help enterprises reduce network bandwidth consumption and network load through point-to-multipoint efficient data transmission.
- Broadcasting: Tencent Cloud supports broadcasting on the subnet dimension.
- Multicast: Tencent Cloud supports multicast on the VPC dimension.

>The broadcasting and multicast features are in beta test stage. If you do need to use both features, please submit a Beta test application.

## Operation Scenarios
Broadcasting and multicast are mostly used in the financial and gaming industries:
- Broadcasting services or market data of the financial industry. For example, after obtaining stock prices and other real-time data, brokers can broadcast stock data to multiple clients in real time, effectively reducing network load.
- For the gaming industry, broadcasting and multicast are mainly used for heartbeat holding between servers.

If unicast is used, the sending server needs to separately send to N servers for total N times. If multicast is used, the server sends the same data to N servers only once, which reduces server resource consumption and also bandwidth resources of the network backbone.

## Steps
### Enabling or disabling broadcasting
#### Enabling broadcasting
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Subnets** in the left sidebar to go to the management page.
3. In the list, find the row of the VPC for which you want to enable the broadcasting feature, click **Enable** under **Subnet Broadcast**, and confirm the enablement.
![](https://main.qcloudimg.com/raw/32f2b4fc747b7e9b3f68d3a166085133.png)

#### Disabling broadcasting
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Subnets** in the left sidebar to go to the management page.
3. In the list, find the row of the VPC for which you want to disable the broadcasting feature, click **Disable** under **Subnet Broadcast**, and confirm the disablement.
![](https://main.qcloudimg.com/raw/32f2b4fc747b7e9b3f68d3a166085133.png)

### Enabling or disabling multicast
#### Enabling multicast
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. In the list, find the row of the VPC for which you want to enable the multicast feature, click **Enable** under **Multicast**, and confirm the enablement.
![](https://main.qcloudimg.com/raw/9aca4e4474cc3d88063d48c20afb4538.png)

#### Disabling multicast
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. In the list, find the row of the VPC for which you want to disable the multicast feature, click **Disable** under **Multicast**, and confirm the disablement.
![](https://main.qcloudimg.com/raw/9aca4e4474cc3d88063d48c20afb4538.png)
