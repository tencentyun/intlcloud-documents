>The VPN gateway for CCN is now in beta. To apply for it, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
> 
A VPN gateway for CCN can be associated with the Cloud Connect Network (CCN), through which, IDC establishes an encrypted communication with CCN. This document introduces how to associate the VPN gateway with CCN.

## Background
A VPN gateway for CCN is used to associate with CCN. You can create multiple VPN encrypted tunnels for each VPN gateway, through which, a on-premises IDC can be connected to CCN.
![](https://main.qcloudimg.com/raw/9c3a75859af98ace2bfe0bcc341d1f8d.png)

To associate a VPN gateway for CCN with CCN, perform the following steps:
1. [Create a VPN gateway for CCN](#step1): a VPN gateway is an egress gateway for establishing VPN connections to CCN, which is used with customer gateways.
2. [Associate with CCN instances](#step2): associate the VPN gateway created for CCN with CCN instances.
3. [Create a customer gateway](#step3): a customer gateway is a logical object that records the fixed public IP address of the IPsec VPN gateway on the IDC side. It is used with a Tencent Cloud VPN gateway. Encrypted VPN tunnels can be established between a VPN gateway and multiple customer gateways.
4. [Create a VPN tunnel](#step4): a VPN tunnel supports IPsec encryption protocol, which protects the information security of data transmission.
5. [Enable the IDC IP range](#step5): add the peer IP range of SPD policy to CCN.

## Directions
### <span id="step1" />Step 1: create a VPN gateway for CCN
1. Log in to [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** -> **VPN Gateway** in the left sidebar to go to the *VPN Gateway** page.
3. Select a region on the top of the *VPN Gateway** page and click **+New**.
4. In the **Create a VPN gateway** pop-up window, enter the gateway name, such as TomVPNGw. Select the associate network, bandwidth cap, and billing mode, and then click **Create**. After the VPN gateway is created, the system randomly allocates a public IP address, for example, `203.195.147.82`.
>To create a VPN gateway for CCN in the specified availability zone, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>
 - **Gateway Name**: enter a name for the new VPN gateway, which is limited to 60 characters.
 - **Network**: check the CCN.
 - **Bandwidth Cap**: select the maximum bandwidth for the VPN gateway as needed.
 - **Billing Method**: select the billing mode for the VPN gateway as needed.
   - **Bill-by-traffic**: this billing mode is suitable for applications subject to large bandwidth fluctuations.
      ![](https://main.qcloudimg.com/raw/a3c1bcd51643560d524e3b4dd54be18a.png)

### <span id="step2" />Step 2: associate with CCN instances
- You can associate with an existing CCN instance by following the steps below:
 1. In the **VPN Gateway** page, click the ID of a VPN gateway for CCN in the list to view its details.
 2. In the **Basic Information** tab, click <img src="https://main.qcloudimg.com/raw/7b27e195bfc7f7ee82118f80c4c96b28.png" style="margin:-4px 0;"/> next to **Network**, select a target CCN instance from the drop-down list, and then click **Save**.
![](https://main.qcloudimg.com/raw/95c284b4ca949dd4facb816bd305e34b.png)
- You can associate with a new CCN instance by following the steps below:
 1. Click **Cloud Connect Network** in the left sidebar to go to the **CCN** page.
 2. Select a region on the top of the **CCN** page and click **+New**.
 3. In the **New CCN instance** pop-up window, complete the following configurations and click **OK**.
   1. Enter the name and description for the CCN instance. Select its billing mode, service quality, and speed limit mode.
   2. Select **VPN Gateway** under *Associate with Instance**, and search for region and ID of the VPN gateway for CCN.
![](https://main.qcloudimg.com/raw/54cba45a12f8d6396f1dcd02b6dff281.png)

### <span id="step3" />Step 3: create a customer gateway
1. Click **VPN Connection** -> **Customer Gateway** in the left sidebar to go to the **Customer Gateway** page.
2. Select a region on the top of the **Customer Gateway** page and click **+New**.
3. In the **Create Customer Gateway** pop-up window, enter the name and public IP of the customer gateway on the IDC side, and click **Create**.
![](https://main.qcloudimg.com/raw/1ee24b6ea02197ee926a2c68cc6b07ad.png)

### <span id="step4" />Step 4: create a VPN tunnel
1. Click **VPN Connection** -> **VPN Tunnel** in the left sidebar to go to the **VPN Tunnel** page.
2. Select a region on the top of the **VPN Tunnel** page and click **+New**.
3. In the **Create VPN tunnel** pop-up window, enter the tunnel name and pre-shared key (such as `123456`), select **CCN** for **VPN Gateway type**, choose the customer gateway, and then click **Next**.
![](https://main.qcloudimg.com/raw/aaa4108a5c7256e787f2c6f464f2c9ce.png)
4. Enter an SPD policy to limit the communication between local IP ranges and peer IP ranges. Click **Next**.
>
>- Peer IP ranges in each rule cannot overlap.
>- Rules for tunnels in the same gateway cannot overlap.
>- Peer IP ranges of the SPD policy can be added to CCN.
>
![](https://main.qcloudimg.com/raw/3e93deb482a775a805bf7610a4cb2e1b.png)
5. (Optional) Configure IKE parameters. Click **Next** if no advanced configuration is required.
![](https://main.qcloudimg.com/raw/ba29246e26e44f88966fb22d4392f6e0.png)
6. (Optional) Configure IPsec parameters. Click **Complete** if no configuration is required.
![](https://main.qcloudimg.com/raw/a4644041c93d9a4a5365276161ba8e23.png)
8. After the VPN tunnel is successfully created, go back to the **VPN Tunnel** page and click **More** -> **Download config file** under the **Operation** column in the list.
![](https://main.qcloudimg.com/raw/eb9d4dbd1b4b58c4faa20dcff36bb206.png)

### <span id="step5" />Step 5: enable IDC IP ranges
1. Click **VPN Connection** -> **VPN Gateway** in the left sidebar.
2. Click the ID of a VPN gateway for CCN in the list to view its details.
3. Select the **IDC IP Range** tab, and enable the target IP range.
![](https://main.qcloudimg.com/raw/02b7c6412ac7de7ab50b203768e8ec0d.png)

## Result Validation
1. Click **Cloud Connect Network** in the left sidebar to go to the **CCN** page.
2. In the list, click the ID of a CCN instance associated with the VPN gateway for CCN to view its details.
3. Select the **Route table** tab. If the table shows the enabled IP range in the status of **Valid** and the **Next hop** is a VPN gateway for CCN, the CCN instance is successfully associated.
![](https://main.qcloudimg.com/raw/1f7089ad46654f9a3c2a9242c34302a4.png)
