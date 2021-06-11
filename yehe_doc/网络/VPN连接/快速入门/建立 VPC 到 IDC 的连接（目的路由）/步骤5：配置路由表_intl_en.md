You can successfully configure a VPN tunnel after the aforementioned 4 steps, but you still need to configure a route table to route the traffic of the subnet A to the VPN gateway. Meanwhile, you need to configure the route table of the VPN gateway to import the traffic of the VPN gateway to the VPN tunnel. In this way, the IP range in subnet A can communicate with the IP range in the IDC.

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **Subnet** on the left sidebar and choose the corresponding region and VPC, such as **Tokyo** and `VPC1` in the example. Click the ID of the route table associated with subnet A to go to the details page.
![](https://main.qcloudimg.com/raw/2edc1c8c0d8596423383ccb4e3b86396.png)
3. Click **Add routing policy** on the “Basic Information” tab.
   ![](https://main.qcloudimg.com/raw/60984e42e4e2b0ae9b7c5d64c422fc54.png)
4. In the pop-up dialog box, enter the subnet IP range of the IDC (`10.0.1.0/24`). Choose **VPN gateway** as the “Next hop type” and choose the VPN gateway which has just been created, namely `VPN1`, as “Next hop”. Click **Create** to configure the route table of subnet A.
   ![](https://main.qcloudimg.com/raw/0ccfdc5d0f1fb1b5a0d66d9657e7422e.png)
5. Click **VPN Connection** > **VPN Gateway** on the left sidebar.
6. Click the ID of the VPN gateway instance to go to the details page.
7. Click the **Route Table** tab on the “Instance Details” page to configure the routing policy of the VPN gateway.
8. Click **Add routing** and enter the following parameters in the pop-up dialog box:
   + Destination: enter the private network IP range of the customer IDC which needs to communicate with the local IDC. Enter 10.0.1.0/24 in this example.
   + Next hop type: VPN tunnel is the only option. No setting required.
   + Next hop: choose the VPN tunnel created in [Step 3](https://intl.cloud.tencent.com/document/product/1037/39679).
   + Weight: If there are 2 VPN tunnels between VPC and IDC, you can set the active/standby linkage according to the weight. In this example, the default weight value is 0.
     ![](https://main.qcloudimg.com/raw/b6f5b65eadf82b090d60f79d4091bd65.png)
9. Click **OK** to complete the configuration of the VPN gateway route table.
   ![](https://main.qcloudimg.com/raw/7704e64f645f5dda5d0d43b4eeb5da28.png)
