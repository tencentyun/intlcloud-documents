When the peering connection no longer meets your business requirements, you can smoothly migrate your network architecture to CCN, so as to get a quick and flexible access to the secure and reliable global network and achieve interconnection over the public and private network.

## Scenario

VPC1 and VPC2 are peer connected and you want to migrate them to CCN, to allow them connect with other VPCs over the public and private network.
- VPC1 (Guangzhou): 192.168.0.0/16, Subnet A: 192.168.0.0/24, Subnet B: 192.168.1.0/24.
- VPC2 (Shanghai): 10.0.0.0/16, Subnet C: 10.0.0.0/24, Subnet D: 10.0.1.0/24.

![](https://main.qcloudimg.com/raw/937834b52397e7c83072cda4764e5b73.jpg)
## Directions

1. Create a CCN instance by referring to [Creating a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062). Skip this step if you already have one.
2. Associate VPC1 (Guangzhou) and VPC2 (Shanghai) with the corresponding CCN instance. For more information, see [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064).
   And then, in the CCN instance route table, you should see routing policies with VPC1 (Guangzhou) and VPC2 (Shanghai) subnets as destination. There are four routing policies in this example, pointing to subnets A, B, C, and D.
   ![](https://qcloudimg.tencent-cloud.cn/raw/fd4bc095bf06c8253cc74fadb6a9a6d5.png)
3. Check the subnet route tables of VPC1 (Guangzhou) and VPC2 (Shanghai). By default, CCN route will be distributed to subnet routes. If the distribution fails, you need to enable or disable necessary route manually complete the migration. There’re three possible scenarios as follows.
>? Access the subnet route tables of VPC1 (Guangzhou) and VPC2 (Shanghai) as needed, and operate depending on the scenarios.
>
 - **Scenario 1: the CCN route does not conflict with existing peering connections, the CCN route will take effect.**
![](https://qcloudimg.tencent-cloud.cn/raw/83a1e5bde6e3250b39772f3fdb8a2f43.png)
      Complete the migration as follows:
		1. **Disable** the route that using this peering connection as the next hop.
		
		2. Check the monitoring data of network traffic over the peering connection. For more information, see [Viewing Monitoring Data of Network Traffic](https://intl.cloud.tencent.com/document/product/553/18842).
		>? You can delete the peering connection if there is no traffic go through it.
 - **Scenario 2: the CCN route is included in the route of peering connection, the CCN route will be ignored by default.**
 The route with the longest mask will be matched and used for forwarding. You can manually enable the CCN route to make it effective.
![](https://qcloudimg.tencent-cloud.cn/raw/99c098e813feb896b44bee223827d625.png)
   Complete the migration as follows:
   
     1. **Enable** the routing policies using CCN as the next hop.
     2. View the monitoring data of network traffic over the peering connection. For more information, see [Viewing Monitoring Data of Network Traffic](https://intl.cloud.tencent.com/document/product/553/18842).
     >? You can delete the peering connection if there is no traffic go through it.
 - **Scenario 3: if the CCN route includes or is the same as the peering connection route, the CCN route will be ignored by default.**
 The route with the longest mask will be matched and used for forwarding. You need to adjust the destination block of the peering connection route, and then manually enable the CCN route to make them effective. Complete the migration as follows:
      1. Modify the route of the peering connection. Change the destination that includes the original destination block and with a subnet mask shorter than that of the CCN route. For example, change “10.0.0.0/24” to “10.0.0.0/16”. 			
      2. **Enable** the route with CCN as the next hop.
    
        After the change, traffic will be first forwarded via the route with CCN as the next hop, and the original route with peering connection as the next hop becomes invalid.
      3. View the monitoring data of network traffic over the peering connection. For more information, see [Viewing Monitoring Data of Network Traffic](https://intl.cloud.tencent.com/document/product/553/18842).
      >? You can delete the peering connection if there is no traffic go through it.
