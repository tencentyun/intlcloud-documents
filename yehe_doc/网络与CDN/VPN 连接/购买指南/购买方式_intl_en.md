This document introduces you how to purchase the IPSec VPN and SSL VPN in the Tencent Cloud console.
>? The SSL VPN is in beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>


## IPSec VPN Purchase Method
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connections** > **VPN Gateway** in the left sidebar to enter the admin page.
3. Select a region and VPC, and then click **+New**.
   ![]()
4. Configure the following parameters in the pop-up dialog box, and click **Create**.
 - Gateway name: Enter a VPN gateway name with up to 60 characters.
 - Protocol type: Select a protocol for the VPN connection to be created.
 - Associated network: Select the associated network of the VPN gateway as required. The IPSec VPN can be associated to CCN and VPC, while the SSL VPN can be associated to VPC only.
 - Network: Select the VPC to which the VPN gateway belongs.
 - Bandwidth cap: Select the maximum bandwidth for the VPN gateway as needed.
 - Tag: An optional configuration that helps you manage VPN gateways.
 - Billing mode: Select the billing mode for the VPN gateway as needed.
	+ Bill-by-traffic: This mode is suitable for scenarios where the bandwidth fluctuates greatly.
	![]()


## SSL VPN Purchase Method
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connections** > **VPN Gateway** in the left sidebar to enter the admin page.
3. Select a region and VPC, and then click **+New**.
   ![]()
4. Configure the following parameters in the pop-up dialog box, and click **Create**.
 - Gateway name: Enter a VPN gateway name with up to 60 characters.
 - Protocol type: Select a protocol for the VPN connection to be created.
 - SSL VPN connections: Specify the number of SSL VPN connections.
 - Associated network: The SSL VPN can be associated to VPC only currently.
 - Network: Select the VPC to which the VPN gateway belongs.
 - Bandwidth cap: Select the maximum bandwidth for the SSL VPN gateway as needed.
![]()
