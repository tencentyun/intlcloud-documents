After a VPN tunnel is created, you can modify the basic information of it, such as the tunnel name, pre-shared key, tag information, and SPD policy, as well as advanced configurations such as IKE configuration and IPsec configuration. You can also reset all the configurations of the VPN tunnel.

## Impact on the System
The reset operation will interrupt data transmission over the existing VPN tunnel and reestablish the connection. Please get ready for network change in advance.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** > **VPN Tunnel** on the left sidebar to go to the management page.
3. On the **VPN Tunnel** page, click the ID of the target VPN tunnel to go to the details page.
4. Click the **Edit** icon on the **Basic Info** page to modify the tunnel name, pre-shared key, tag information and SPD policy rules. Then click **Save**.
    ![](https://main.qcloudimg.com/raw/4aed45da6f7c0e06085ac7ad2ff784f1.png)
	You can also modify the tunnel name and pre-shared key by clicking the edit icon on the VPN tunnel list page, as shown in the figure below.
	![](https://main.qcloudimg.com/raw/8a1fbc4e20c1bd1c1a6e963b09391a5c.png)
5. Click the **Advanced Configuration** tab to modify the IKE and IPsec configurations, and click **Save**.
    ![](https://main.qcloudimg.com/raw/307177eb253a5ce756510aa4d2b2f8b8.png)
6. Please be aware that, by clicking **Reset**, all your custom tunnel configurations will be cleared.
    ![](https://main.qcloudimg.com/raw/ee06065944ab863959499ad50ece556b.png)
