The routing policies in the route table can be operated in a real-time manner. Some of the available routing policy actions are adding, deleting, quering, exporting, or publishing and withdrawing to/from CCN. This document describes all the aforementioned operations of the routing policies.

## Adding a Routing Policy
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/route?rid=1), and select **[Route Tables](https://console.cloud.tencent.com/vpc/route?rid=1)** in the left sidebar to go to the **Route Table** page.
2. In the list, click the route table ID to be modified to go to the details page.
3. Click **+New routing policies**.

 	<img src="https://main.qcloudimg.com/raw/5bde7782edfd3a7ade82aa669bd5a7a1.png" width="80%">
4. In the pop-up window, <span id="routeParam" />configure the routing policy.
 >? If you have deployed a <a href="https://int/product/457/6759">TKE service</a> in the VPC, when you configure the routing policy of the route table for the VPC subnet, the destination cannot be within the CIDR block range of the VPC, nor can it contain the container IP range. For example, if a VPC CIDR block is 172.168.0.0/16 and the container network CIDR block is 192.168.0.0/16, when you configure the routing policy for the VPC subnet, the destination IP range cannot be in the range of 172.168.0.0/16, and cannot contain 192.168.0.0/16.
 >
  <table><tbody>
   <tr><th>Configuration Item</th><th>Description</th></tr>
   <tr><td>Destination</td><td>The destination IP range to which you want to forward subnet outbound traffic. The requirements are as follows:
    <ul><li>The destination IP range can only be in the format of the IP range. If you want the destination to be a single IP, set the mask to 32 (for example, 172.16.1.1/32).</li>
	  <li>The destination cannot be an IP range in the VPC where the routing table is located, because the local routing has indicated that the private network is connected in this VPC by default.</li></ul>
    	</td></tr>
    <tr><td>Next hop type</td><td>The egress of the VPC data packets. The following types are supported:
        <ul>
           <li> NAT Gateway: the traffic designated for a destination IP range is forwarded to a NAT gateway.</li>
           <li>Peering Connections: the traffic designated for a destination IP range is forwarded to a VPC on the other end of a peering connection.</li>
           <li>Direct Connect Gateway: the traffic designated for a destination IP range is forwarded to a direct connect gateway.</li>
          <li>High Availability Virtual IP: the traffic designated for a destination IP range is forwarded to a high availability virtual IP.</li>
          <li>VPN Gateway: the traffic designated for a destination IP range is forwarded to a VPN gateway.</li>
          <li>Public IP of CVM: the traffic designated for a destination IP range is forwarded to the public IP of a CVM instance in a VPC (including public IPs and elastic IPs).</li>
          <li>CVM: the traffic designated for a destination IP range is forwarded to a CVM instance in a VPC.</li>
          </ul>
       </td></tr>
   <tr><td>Next hop</td><td>Specify the next hop instance to redirect to, such as the gateway or CVM IP.</td></tr>
    <tr><td>Notes</td><td>You can custom the description of the route for resource management.</td></tr>
    <tr><td>Add a line</td><td>You can click **+Add a line** to configure multiple routing policies, or click the deletion icon in the **Operation** column to delete the unnecessary routing policies.</td></tr>
     </tbody> </table>
		 <img src="https://main.qcloudimg.com/raw/c449580ff5918822373d9b0067ee877e.png">
5. Click **Create** to complete the creation.

## Publishing a Routing Policy to CCN/Withdrawing a Routing Policy from CCN
For the VPC or VPN instances associated with CCN, the routes are published to CCN by default. For the new custom routing policies that are not published to CCN by default, you need to manually publish them. The routing policies that are manually published or published by default can be withdrawn from CCN.
Currently, only the routing policies whose **Next hop type** is **High Availability Virtual IP**, **VPN Gateway**, or **CVM** in the route tables (including the default route tables and the custom route tables) can be manually published to CCN/withdrawn from CCN.

### Prerequisites
The VPCs where the high available virtual IP, VPN gateway, and CVM are located have been associated with CCN.

### Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/route?rid=1), and select **[Route Tables](https://console.cloud.tencent.com/vpc/route?rid=1)** in the left sidebar to go to the **Route Table** page.
2. In the list, click the route table ID to be modified to go to the details page.
   ![](https://main.qcloudimg.com/raw/db9290e78cfc13b9575e590a0f3fa680.png)
2. You can perform the following operations as needed:
   + For the custom routing policy, you can click **Publish to CCN** to manually publish this routing policy to CCN.
   + For the custom routing policy that have been published to CCN, you can click **Withdrawn from CCN** to reclaim the policy.
   + Click **Edit** to modify the routing policy.
 >?
 >+ When a routing policy is disabled, it cannot be published to CCN.
 >+ A routing policy cannot be disabled once being published to CCN.

## Editing a Routing Policy
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/route?rid=1), and select **[Route Tables](https://console.cloud.tencent.com/vpc/route?rid=1)** in the left sidebar to go to the **Route Table** page.
2. In the list, click the route table ID to go to the details page.
3. Click **Edit** on the right of the routing policy to modify it.
![](https://main.qcloudimg.com/raw/77dad0c5a0e0247b73e585cfa8075448.png)
4. Click **OK** to complete the modification, or click **Cancel** to cancel the modification.

## Querying and Exporting a Routing Policy
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/route?rid=1), and select **[Route Tables](https://console.cloud.tencent.com/vpc/route?rid=1)** in the left sidebar to go to the **Route Table** page.
2. In the list, click a route table ID to go to the details page. You can find the routing policies in this route table.
3. In the search box on the top right, you can query the routing policy by entering the destination address.
![](https://main.qcloudimg.com/raw/31318f03c644f0ac7b20dddced6ed026.png)
4. Click **Export** to export the routing policies in the list, and save it .csv format.

## Deleting a Routing Policy
You can delete the unnecessary routing policies. Only the custom routing policies can be deleted.
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/route?rid=1), and select **[Route Tables](https://console.cloud.tencent.com/vpc/route?rid=1)** in the left sidebar to go to the **Route Table** page.
2. In the list, click the route table ID to be modified to go to the details page.
3. Click **Delete** on the right of the routing policy that you want to delete.
![](https://main.qcloudimg.com/raw/dd381c2cddc335bf6e178013ad8b5424.png)
4. Please make sure that you are aware of any possible impact of deleting the routing policy, and then click **OK**.

 	<img src="https://main.qcloudimg.com/raw/bcb484e30a79717e40c8dc9b228757ff.png" width="70%" />
