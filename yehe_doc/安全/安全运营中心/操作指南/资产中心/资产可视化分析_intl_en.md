## Scenarios
Asset Center provides the visual analysis of assets feature, which performs interactive, graphical, and visual analysis of the cloud network.
- This feature gives you an intuitive view of the network topology relationship among VPCs, subnets, and instances on the cloud. In this way, you can manage and optimize cloud asset risks quickly in the topological graph.
- This feature allows you to quickly view the network traffic of assets in the network topology as needed, and intuitively monitor the network traffic of cloud assets, to get a full picture of the overall network security of cloud assets.

## Prerequisites
To use the visual analysis of assets feature, you must have enabled [Security Operation Center Premium](https://buy.cloud.tencent.com/soc). 

## Directions
1. Log on to the [Security Operation Center Console](https://console.cloud.tencent.com/ssav2/assets). In the left navigation pane, select **Asset Center** -> **Visual Analysis of Assets** to go to the Visual Analysis of Assets page.
2. On the Visual Analysis of Assets page, you can view the network security topological graph that shows the relationship among VPCs, subnets, and CVMs. You can click on the leaf node ![](https://qcloudimg.tencent-cloud.cn/raw/fde4d5ae51c28caa5435e76c12662f78.png) to view the asset details of the corresponding CVM.
>? The leaf nodes in the network security topological graph are CVMs. Red indicates that the CVM is at risk, and green indicates that the CVM is risk free.

![](https://qcloudimg.tencent-cloud.cn/raw/0123681ed77202fccd934297277a7465.png)
3. On the Visual Analysis of Assets page, you can perform the following operations.
 - **Search**
 In the upper-right corner of the network security topological graph, you can search by the Quick Filter item and Network to view the network security topological graphs that meet the search criteria.
 ![](https://qcloudimg.tencent-cloud.cn/raw/def48cd68ef1a2dd38a0c576c8c0d39c.png)
 The following is the description of Quick Filter items:
    - Public IP: CVM with a public IP.
    - Open port 22 on the public network: The CVM with port 22 open in the mapping data.
    - Security group configuration risk: The CVM with security group configuration risk.
 - **Zoom in/out the topological graph**
In the lower-right corner of the network security topological graph, click ![](https://qcloudimg.tencent-cloud.cn/raw/357956c33ac5b65b9f982376e73ac870.png) or ![](https://qcloudimg.tencent-cloud.cn/raw/5ae6519df2f2ca60bfea08dc99724236.png) to zoom in or out the topological graph.
 - **View VPC information**
In the network security topological graph, move the pointer over a VPC to view the VPC information.
![](https://qcloudimg.tencent-cloud.cn/raw/06bccf43e8a4918f2ea8634f6efa115b.png)
 - **View subnet information**
In the network security topological graph, move the pointer over a subnet to view the subnet information.
![](https://qcloudimg.tencent-cloud.cn/raw/92924178b664d1f4ab81f2ac00270182.png)
 - **View subnet topological graph**
In the network security topological graph, click the target subnet node ![](https://qcloudimg.tencent-cloud.cn/raw/5e5cf362e93f6a0003d9549b598e41d7.png) to go to the corresponding subnet topological graph.
![](https://qcloudimg.tencent-cloud.cn/raw/264ed8140fb3e32ffb4677bd1bc96043.png)
 - **View CVM asset information**
 In the network security topological graph, move the pointer over a CVM leaf node ![](https://qcloudimg.tencent-cloud.cn/raw/83a9b67d8d327142743316cb311bf2c5.png) to view the CVM asset information.
 ![](https://qcloudimg.tencent-cloud.cn/raw/c3f3e6311a7ae0cfc2680b447c2a0507.png)
 - **View CVM asset details**
    1. In the network security topological graph, click the target CVM leaf node ![](https://qcloudimg.tencent-cloud.cn/raw/02bc8ef83b241bd6227bb7fe02a25ccd.png) to go to the Asset Details page of the CVM.
    2. On the Asset Details page, you can view the basic information, security risks, and network information of the asset.
>?
>- The Security Risks tab displays fingerprint information, threat alerts, configuration risks, attack surface, vulnerabilities, and configuration history of the asset, and you can perform relevant operations.
>- The Network Information tab displays the security group information bound to the asset and LAN and WAN bandwidth monitoring data.

![](https://qcloudimg.tencent-cloud.cn/raw/42a87f46ec722881b130285a52dc0723.png)