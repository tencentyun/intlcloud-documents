The VPN gateway for CCN can be associated with the Cloud Connect Network (CCN) to establish an encrypted communication between the IDC and CCN. This document introduces how to associate the VPN gateway for CCN with CCN.

## Background
A VPN gateway for CCN can be associated with CCN and create multiple encrypted VPN tunnels. Each VPN tunnel can connect one local IDC.
![](https://main.qcloudimg.com/raw/9c3a75859af98ace2bfe0bcc341d1f8d.png)

The steps to associate the VPN gateway for CCN with CCN are as follows:
1. [Create a VPN gateway for CCN](#step1): a VPN gateway is an egress gateway used by CCN along with the customer gateway to establish VPN connections.
2. [Associate CCN instances](#step2): associate the VPN gateway for CCN with CCN instances.
3. [Create a customer gateway](#step3): a customer gateway is a logical object used with a Tencent Cloud VPN gateway to record the fixed public IP address of the IPsec VPN gateway on the IDC side. A VPN gateway can establish encrypted VPN tunnels with multiple customer gateways.
4. [Create a VPN tunnel](#step4): VPN tunnel supports IPsec encryption protocol, which ensures secure data transmission.
5. [Enable the IDC IP range](#step5): add the IDC IP range of SPD policy to CCN.

## Directions
<span id="step1"></span>
### Step 1: Create a VPN gateway for CCN
1. Log in to [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** -> **VPN Gateway** in the left sidebar.
3. Select a region on the top of the **VPN Gateway** page and click **+New**.
4. In the **Create a VPN gateway** pop-up window, enter the gateway name, such as TomVPNGw. Select the associate network, bandwidth cap, billing method, and click **Create**. After the VPN gateway is created, the system randomly assigns it a public IP address such as `203.195.147.82`.
>?To create a VPN gateway for CCN in the specified availability zone, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>
 - **Gateway Name**: enter a VPN gateway name, which cannot exceed 60 characters.
 - **Associate Network**: select CCN.
 - **Bandwidth Cap**: select the maximum bandwidth for the VPN gateway as needed.
 - **Billing Method**: select the billing mode for the VPN gateway as needed.
   - **Bill-by-traffic**: this mode is suitable for scenarios where the bandwidth fluctuates greatly.
      ![](https://main.qcloudimg.com/raw/a3c1bcd51643560d524e3b4dd54be18a.png)
 
<span id="step2"></span>
### Step 2: Associate CCN instances
- You can associate an existing CCN instance by the following steps:
 1. Return to the **VPN Gateway** page, click the ID of an existing VPN gateway for CCN in the list to view its details.
 2. Under the **Basic Information** tab, click <img src="https://main.qcloudimg.com/raw/7b27e195bfc7f7ee82118f80c4c96b28.png" style="margin:-4px 0;"/>next to **Network**, select a CCN instance you want to associate from the drop-down list, and then click **Save**.
![](https://main.qcloudimg.com/raw/95c284b4ca949dd4facb816bd305e34b.png)
- You can associate a new CCN instance by the following steps:
 1. Click **Cloud Connect Network** in the left sidebar to go to the **CCN** page.
 2. Select a region on the top of the **CCN** page and click **+New**.
 3. In the **New CCN instance** pop-up window, complete the following configurations and click **OK**.
   1. Enter the name and description for the CCN instance. Select its billing mode, service quality, and speed limit mode.
   2. Select **VPN Gateway** under **Associate with Instance**, and search for regions and IDs of existing VPN gateways for CCN.
![](https://main.qcloudimg.com/raw/54cba45a12f8d6396f1dcd02b6dff281.png)

<span id="step3"></span>
### Step 3: Create a customer gateway
1. Log in to [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** -> **Customer Gateway** in the left sidebar to go to the **Customer Gateway** page.
3. Select a region on the top of the **Customer Gateway** page and click **+New**.
4. In the **Create Customer Gateway** pop-up window, enter the name and public IP of the customer gateway on the IDC side, and click **Create**.
![](https://main.qcloudimg.com/raw/1ee24b6ea02197ee926a2c68cc6b07ad.png)

<span id="step4"></span>
### Step 4: Create a VPN tunnel
1. Log in to [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** -> **VPN Tunnel** in the left sidebar to go to the **VPN Tunnel** page.
3. Select a region on the top of the **VPN Tunnel** page and click **+New**.
4. On the **Create VPN tunnel** page, enter the tunnel name and pre-shared key (such as `123456`), select **CCN** for **VPN Gateway type**, choose the customer gateway, and click **Next**.
![](https://main.qcloudimg.com/raw/aaa4108a5c7256e787f2c6f464f2c9ce.png)
5. Enter an SPD policy to specify which local IP ranges and IDC IP ranges can communicate with each other.
>!
>- IDC IP ranges in each rule cannot overlap.
>- Rules for tunnels in the same gateway cannot overlap.
>- IDC IP ranges of the SPD policy can be added to CCN.

![](https://main.qcloudimg.com/raw/3e93deb482a775a805bf7610a4cb2e1b.png)
6. (Optional) Configure IKE parameters. Click **Next** if no advanced configuration is required.
![](https://main.qcloudimg.com/raw/ba29246e26e44f88966fb22d4392f6e0.png)
7. (Optional) Configure IPsec parameters. Click **Completed** if no configuration is required.
![](https://main.qcloudimg.com/raw/a4644041c93d9a4a5365276161ba8e23.png)
8. After the VPN tunnel is successfully created, return to the **VPN Tunnel** list page and click **More** -> **Download config file** under the **Operation** column.
![](https://main.qcloudimg.com/raw/eb9d4dbd1b4b58c4faa20dcff36bb206.png)

<span id="step5"></span>
### Step 5: Enable IDC IP ranges
1. Log in to [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** -> **VPN Gateway** in the left sidebar.
3. Click the ID of a VPN gateway for CCN in the list to view its details.
4. Select the **IDC IP Range** tab, and activate the IP range you need.
![](https://main.qcloudimg.com/raw/02b7c6412ac7de7ab50b203768e8ec0d.png)

## Result Validation
1. Log in to [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **Cloud Connect Network** in the left sidebar to go to the **CCN** page.
3. In the list, click the ID of a CCN instance associated with the VPN gateway for CCN to view its details.
4. Select the **Route table** tab. If the table shows the enabled IP range with a **Valid** status and the **Next hop** is a VPN gateway for CCN, the CCN instance is successfully associated.
![](https://main.qcloudimg.com/raw/1f7089ad46654f9a3c2a9242c34302a4.png)
