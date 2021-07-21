You can view the resources of all subnets in the VPC on the VPC console, for instance, the cloud resources deployed in the subnet, the route table associated with the subnet, and the ACL rules bound to the subnet.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select **Subnet** in the left sidebar to go to the subnet management page.
3. At the top of the **Subnet** page, select the region and VPC to which the subnet belongs. If you keep the default value, namely ‘**All VPCs**’, then you can view all subnets of all VPCs in this region, as shown below:
![](https://main.qcloudimg.com/raw/56e17047ec183ee28d6ffcd5784ffcb3.png)
The meaning of the list fields displayed in the interface is as follows:
 + ID/Name: displays the subnet ID and name. Each subnet is assigned an ID when it is created, and the subnet name can be modified in real-time.
 + Network: the VPC to which the subnet belongs.
 + CIDR: the CIDR block IP range of the subnet. The subnet CIDR block cannot be modified.
 + Availability Zone: displays the availability zone where the subnet is located.
 + Associated Route Table: the route table associated with the subnet.
 + CVM: displays the number of CVMs deployed in the subnet.
 + Available IPs: the number of available IP addresses within the CIDR block range of the subnet.
 + Default Subnet: for the subnets created by the user in the **Subnet** page on the VPC console, which are not the default subnets, the value field will display **No**. If you select the default VPC and subnet automatically created by Tencent Cloud in CVM purchase page, here will display **Yes**. There can only be a single default VPC and subnet in a given region.
 + Operation: the executable operations for the subnet. You can delete the subnet without resources, or you can click **More** > **Change Route Table** to replace the route table associated with the subnet.
4. Click the subnet ID to view the resource details of the subnet. Switch the tab to view the routing rules and the ACL rules.
![](https://main.qcloudimg.com/raw/308eaf31ea4d3a1f92fbc868fa7ce699.png)
5. Click the VPC ID of the network to which the subnet belongs, or the route table ID of the associated route table to view the detailed information of the corresponding resource.
6. Click the number of CVMs to go to the CVM instance page. If the quantity is 0, click the CVM icon to go to the CVM purchase page.
7. At the top of the page, click **Filter** to view the list of subnets in the specified available zone.
8. Click the search box on the upper right of the page to quickly query by the **subnet ID**, **Subnet Name**, **Tag**, and **IPv4 CIDR Block**.
9. Click the Setting icon in the upper right to customize the displayed fields.

