You can successfully configure a VPN tunnel after the aforementioned 4 steps, but you still need to configure a route table to route the traffic of the subnet A to the VPN gateway. Meanwhile, you need to configure the route table of the VPN gateway to import the traffic of the VPN gateway to the VPN tunnel. In this way, the IP range in subnet A can communicate with the IP range in the IDC.

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **Subnet** on the left sidebar and choose the corresponding region and VPC, such as **Tokyo** and `VPC1` in the example. Click the ID of the route table associated with subnet A to go to the details page.
3. Click **Add routing policy** on the “Basic Information” tab.
4. In the pop-up dialog box, enter the subnet IP range of the IDC (`10.0.1.0/24`). Choose **VPN gateway** as the “Next hop type” and choose the VPN gateway which has just been created, namely `VPN1`, as “Next hop”. Click **Create** to configure the route table of subnet A.
5. Click **VPN Connection** > **VPN Gateway** on the left sidebar.
6. Click the ID of the VPN gateway instance to go to the details page.
7. Click the **Route Table** tab on the “Instance Details” page to configure the routing policy of the VPN gateway.
8. Click **Add routing** and enter the following parameters in the pop-up dialog box:
   + Destination: enter the private network IP range of the customer IDC which needs to communicate with the local IDC. Enter 10.0.1.0/24 in this example.
   + Next hop type: VPN tunnel is the only option. No setting required.
   + Next hop: choose the VPN tunnel created in [Step 3](https://intl.cloud.tencent.com/document/product/1037/39679).
   + Weight: If there are 2 VPN tunnels between VPC and IDC, you can set the active/standby linkage according to the weight. In this example, the default weight value is 0.
9. Click **OK** to complete the configuration of the VPN gateway route table.
