* A function deployed in a VPC is isolated from the public network by default. If you want the function to have access to both private network and public network, you can add a NAT gateway to the VPC.
> **Note:**
> Even after a NAT gateway is configured, functions still cannot access resources on the basic network. If you need to access the basic network, you can contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1).

## Usage Scenario
* Access control: This can uniformly converge access requests from the public network to the same address and ensure the uniqueness of the egress address by means of the public network egress in the VPC.
* Public network permissions for VPC: Functions deployed in the VPC can access the public network.

## Creating a NAT Gateway
NAT Gateway is a network cloud service that supports IP address translation and enables high-performance internet access for resources in Tencent Cloud. It can translate the private IP address in a VPC to a public IP address if the private and public networks are isolated from each other, enabling the VPC to access the internet. 

Log in to the VPC console > [NAT gateway console](https://console.cloud.tencent.com/vpc/nat?rid=4) to create a new NAT gateway. Note:
* The NAT gateway should be deployed in the same region as the function and VPC.
* The network to which the NAT gateway belongs should be the VPC where the function is located.

See the figure below:
![](https://main.qcloudimg.com/raw/be489caa5334ce7fc251a1cc09d28297.png)

## Creating a Routing Policy 
Go to the [Routing Table](https://console.cloud.tencent.com/vpc/route?rid=4) on the left in the VPC console, select the region where the routing table is located and the VPC, and click **+ Create** to create a routing table.
![](https://main.qcloudimg.com/raw/4c3cc4c6b5336699dc1141cbbc980cf8.png)

### Enabling SCF to Access All Public IP Addresses
If you want SCF to have access to all public networks, you can configure IP:0.0.0.0/0 in the destination in the routing table, and associate the routing table with the created NAT gateway and SCF subnet, as shown in the figure below:
![](https://main.qcloudimg.com/raw/337f8d6e7f9396ed3d9de86822db3932.png)

### Enabling SCF to Access Certain Public IP Addresses
Add the public IP addresses to be accessed by SCF to the routing table, and associate the routing table with the created NAT gateway and SCF subnet, as shown in the figure below:
![](https://main.qcloudimg.com/raw/f28904a4c9e94719733c954cd935cf82.png)
