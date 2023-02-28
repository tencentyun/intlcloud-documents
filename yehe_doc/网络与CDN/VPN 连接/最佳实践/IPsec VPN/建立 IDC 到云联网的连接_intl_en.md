The VPN gateway for CCN can be associated with the Cloud Connect Network (CCN) to establish an encrypted communication between the IDC and CCN. This document introduces how to associate the VPN gateway for CCN with CCN.

## Background
A VPN gateway for CCN can be associated with CCN and create multiple encrypted VPN tunnels. Each VPN tunnel can connect one local IDC.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ZND9436_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230228164603.png)

The steps to associate the VPN gateway for CCN with CCN are as follows:
1. [Create a VPN gateway for CCN](#step1): a VPN gateway is an egress gateway used by CCN along with the customer gateway to establish VPN connections.
2. [Associate CCN instances](#step2): associate the VPN gateway for CCN with CCN instances.
3. [Create a customer gateway](#step3): a customer gateway is a logical object used with a Tencent Cloud VPN gateway to record the fixed public IP address of the IPsec VPN gateway on the IDC side. A VPN gateway can establish encrypted VPN tunnels with multiple customer gateways.
4. [Create a VPN tunnel](#step4): VPN tunnel supports IPsec encryption protocol, which ensures secure data transmission.
5. [Configure the VPN gateway route](#step5): configure the VPN gateway route to the customer gateway.
6. [Configure the IDC devices](#step6): configure the VPN tunnel for Tencent Cloud on the local gateway of the IDC.
7. [Enable the IDC IP range](#step7): add the IDC IP range of the SPD policy to CCN.



## Directions
### Step 1: create a VPN gateway for CCN[](id:step1)
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Choose **VPN Connection** > **VPN Gateway** in the left sidebar.
3. On the **VPN Gateway** page, specify **Region** in the topbar and click **+New**.
4. In the **Create VPN Gateway** pop-up window, specify the gateway name (for example, TomVPNGw), associated network, bandwidth cap, and billing method, and then click **Create**. After the VPN gateway is created, the system randomly assigns the gateway a public IP address such as `203.195.147.82`.
>?To create a VPN gateway for CCN in the specified availability zone, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>
<table>
<tr>
<th>Parameter</th>
<th>Configuration</th>
</tr>
<tr>
<td>Gateway name</td>
<td>Enter the VPN gateway name (up to 60 characters)</td>
</tr>
<tr>
<td>Region</td>
<td>Display the region of the VPN gateway</td>
</tr>
<tr>
<td>AZ</td>
<td>Select the availability zone of the current gateway</td>
</tr>
<tr>
<td>Protocol Type</td>
<td>IPSec and SSL protocols are supported.</td>
</tr>
<tr>
<td>Bandwidth cap</td>
<td>Set a reasonable bandwidth cap for the VPN gateway according to the actual application scenarios.
</td>
</tr>
<tr>
<td>Associated Network</td>
<td>Select **CCN**.</td>
</tr>
<tr>
<td>Tag</td>
<td>Tags mark VPN gateway resources so that these resources can be queried and managed efficiently. Tag is not a required configuration. You can decide whether to configure it according to your demand.</td>
</tr>
<tr>
<td>Billing Mode</td>
<td>Bill-by-traffic mode is supported. This billing mode is applicable to scenarios with significant bandwidth fluctuations.</td>
</tr>
</table>

### Step 2: associate CCN instances[](id:step2)
- You can associate an existing CCN instance by the following steps:
 1. Return to the **VPN Gateway** page, click the ID of an existing VPN gateway for CCN in the list to view its details.
  2. On the **Basic Information** tab, click <img src="https://main.qcloudimg.com/raw/7b27e195bfc7f7ee82118f80c4c96b28.png" style="margin:-4px 0;"/> next to **Network**, select a CCN instance you want to associate from the drop-down list, and then click **Save**.
- You can associate a new CCN instance by the following steps:
 1. Click **[CCN](https://console.cloud.tencent.com/vpc/ccn)** in the left sidebar.
 2. On the **CCN** page, specify **Region** in the topbar and click **+New**.
 3. In the pop-up window, complete the following configurations and then click **OK**.
   1. Enter the name and description for the CCN instance. Select its billing mode, service quality, and bandwidth limit mode.
        5. Select **VPN Gateway** under **Associate with Instance**, and specify the region and ID of an existing VPN gateway for CCN.

### Step 3: create a customer gateway[](id:step3)
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Choose **VPN Connection** > **Customer Gateway** in the left sidebar.
3. On the **Customer Gateway** page, specify **Region** in the topbar and click **+New**.
4. In the **Create Customer Gateway** pop-up window, enter the name and public IP of the customer gateway on the IDC side, and click **Create**.



### Step 4: create a VPN tunnel[](id:step4)
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Choose **VPN Connection** > **VPN Tunnel** in the left sidebar.
3. On the **VPN Tunnel** page, specify **Region** in the top bar and click **+New**.
4. Configure the basic information about the VPN tunnel as prompted.
>!
>- IDC IP ranges in each rule cannot overlap.
>- Rules for tunnels in the same gateway cannot overlap.
>- Peer IP ranges in the SPD policy can be added to CCN.
>
5. Configure DPD and health check options.
  - **DPD**: By default, DPD is enabled. Retain the default settings. To modify the settings, check the parameters on the page.
  - **Health check**: By default, health check is disabled. Retain the default settings.
6. (Optional) Configure IKE parameters. Click **Next** if no advanced configuration is required.
7. (Optional) Configure IPsec parameters. Click **Completed** if no configuration is required.
8. Click **Create**. After the VPN tunnel is created, go back to the VPN tunnel list page. In the **Actions** column of the VPN tunnel, choose **More** > **Download config file** to download the configuration file.


### Step 5: configure the VPN gateway route[](id:step5)
After the VPN tunnel configuration is complete, configure the VPN gateway route to the customer gateway.
1. Choose **VPN Connection** > **VPN Gateway** in the left sidebar to go to the **VPN Gateway** page. Locate the VPN gateway that you created, and click the value in the **ID/Name** column to enter the gateway details page. 
2. Click the **Route Table** tab and click **Add a route**.
3. Configure the policy of routing from the VPN gateway to the customer gateway.
<table>
<tr>
<th>Configuration Item</th>
<th>Description</th>
</tr>
<tr>
<td>Destination</td>
<td>Enter the IDC IP range configured in the customer gateway for the public access.</td>
</tr>
<tr>
<td>Next Hop Type</td>
<td>The default value is <b>VPN Tunnel</b>.</td>
</tr>
<tr>
<td>Next Hop</td>
<td>Select a VPN tunnel that has been created.</td>
</tr>
<tr>
<td>Weight</td>
<td>Enter an integer within 0-100. The smaller the value, the higher the priority.</td>
</tr>
</table>
4. Click **OK**.


### Step 6: configure the IDC devices[](id:step6)
After the VPN gateway and VPN tunnel are configured on Tencent Cloud, you must configure the VPN tunnel on the local gateway of the IDC. For more information, see [Local Gateway Configurations](https://intl.cloudwww.tencentcloud.com/document/product/1037/40707).

### Step 7: enable IDC IP ranges[](id:step7)
>?
>+ This step is applicable only to VPN gateways v1.0 and v2.0. 
>+ If you use a VPN gateway v3.0 for CCN and have associated the gateway with a CCN instance, the routing policy in which the next hop is <b>CCN</b> will be automatically obtained and displayed in the route table. The routing policy configured on the VPN gateway is also automatically synchronized to CCN.
>

**For VPN gateways v1.0 and v2.0, enable the IDC IP ranges as follows:**

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Choose **VPN Connection** > **VPN Gateway** in the left sidebar.
3. Click the **ID/Name** of the VPN gateway for CCN in the list to view its details.
4. Click the **IDC IP Range** tab, and enable the IP range as needed.


## Result Validation
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Select **Cloud Connect Network** in the left sidebar to go to the **CCN** page.
3. In the list, click the **ID/Name** of the CCN instance associated with the VPN gateway for CCN to view its details.
4. Click the **Route table** tab. If the table shows that the enabled IP range is in the **Valid** state and **Next hop** is a VPN gateway for CCN, the CCN instance is associated.

