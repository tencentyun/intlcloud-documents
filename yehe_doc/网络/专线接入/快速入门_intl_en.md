After purchasing the Direct Connect service, use the Tencent Cloud Direct Connect console to create a Direct Connect instance and log in it. The steps are decribed as follows:

## Step 1: Log in to Direct Connect Console
Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and select **Tencent Cloud Services** > **Networking** > **Direct Connect** to go to the Direct Connect Console. If you do not already have an account, refer to [Signing Up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985).

## Step 2: create a connection.
1. In the left sidebar on the [Direct Connect Console](https://console.cloud.tencent.com/dc/dc), click **Connections** to go to the **Connections** page.
2. Click **+New**.
3. Enter the necessary information. After you submit the application, a Tencent Cloud Direct Connect representative will contact you and verify the details.

## Step 3: Create a Direct Connect Gateway
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and choose **Tencent Cloud Services** > **Networking** > **Virtual Private Cloud** to go to the VPC Console.
2. In the left sidebar, click **Direct Connect Gateways** to go to the management page.
3. On the top of the page, select the region and network, and click **+Create**.
4. In the page that appears, enter a name and select the type of network to associate.
 > For Cloud Connect Network (CCN), you do not need to associate the Direct Connect gateway with a CCN instance.
5. Click **OK** to complete the creation of the Direct Connect gateway.

## Step 4: Create a Dedicated Tunnel
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and select **Tencent Cloud Services** > **Networking** > **Direct Connect** to go to the Direct Connect Console.
2. In the left sidebar, click **Dedicated Tunnel** to go to the management page.
3. Click **+Create**.
4. Basic configuration:
 - Dedicated tunnel name: name of the dedicated tunnel.
 - Connection type: select a **Running** connection under your Tencent Cloud account.
 - Access network: VPC, BM network, CCN.
5. Advanced configuration:
 - VLAN ID: if the connection is provided by a partner, get the VLAN ID from the partner.
 - Bandwidth: set the upper limit of the bandwidth.
 - Edge IP: IP addresses of ingress points on both ends of the connection (the IDC and cloud access devices).
 - Routing mode: BGP routes and static routes are supported.
6. IDC device configuration: you can download a general configuration guide from the console.
7. Click **Submit** to complete the creation of the dedicated tunnel.

## Step 5: (Optional) Configure Direct Connect NAT
You can configure network address translation for the gateway on the Direct Connect Gateway page. Network address translation includes IP translation and IP port translation. For more information, refer to [Configuring the Network Address Translation (NAT)](https://intl.cloud.tencent.com/document/product/216/19257).

## Step 6: Configure the Route Table
Connecting to VPC or BM networks:
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and choose **Tencent Cloud Services** > **Networking** > **Virtual Private Cloud** to go to the VPC Console.
2. In the left sidebar, click **Route Tables** to go to the management page.
3. Locate the route table associated with the desired subnet in the list and click the ID to go to its details page.
4. Click **Add Routing Policy** and enter the destination IP range. For next hop type, select **Direct Connect Gateway**. For next hop, select the name of the gateway.
6. Click **OK**.

## Step 7: Set Alarms
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and choose **Tencent Cloud Services** > **Monitoring & OPS** > **Basic Cloud Monitor** to go to the Cloud Monitoring Console.
2. In the left sidebar, click **Alarm Configuration** > **Alarm Policy** to go to the management page.
3. Click **Add**.
4. Enter a name for the alarm policy. For policy type, select connection or dedicated tunnel, and add the alarm trigger.
5. Associate alarm objects: select the alarm receiver group, and when it is saved, you can view the alarm polices that are set in Alarm Policy List.
6. View alarm information: when the alarm condition is triggered, you will be notified via SMS, email, and Message Center. You can also view the alarm information by selecting **Direct Connect** -> **Connection** (or **Dedicated Tunnel**) from the left sidebar.
For more information on alarms, refer to [Creating Alarm Policies](https://intl.cloud.tencent.com/document/product/248/6215).
