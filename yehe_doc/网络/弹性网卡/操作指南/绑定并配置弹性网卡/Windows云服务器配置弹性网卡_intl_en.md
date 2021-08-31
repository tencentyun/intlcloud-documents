>? The following operations use Windows 2012 as an example.
>

## Directions
### Windows provided with DHCP
If the CVM is provided with DHCP, you can view its secondary ENI and IP by following steps below without any further configuration:
1. Log in to the CVM, and select **Control Panel** -> **Network and Internet** -> **Network and Sharing Center** to check the secondary ENI that has been automatically obtained.
2. Click the “Ethernet 2” secondary ENI to view its information.
![](https://main.qcloudimg.com/raw/b8498adcc2896f436a1bfdc96d11090d.png)
3. In the **Ethernet 2 Status** pop-up window, click **Properties**.
4. In the **Ethernet 2 Properties** pop-up window, double-click **Internet Protocol Version 4 (TCP/IPv4)**.
5. In the **Internet Protocol Version 4 (TCP/IPv4)** pop-up window, you can see **Obtain an IP address automatically** is selected, so there is no need to enter one.
![](https://main.qcloudimg.com/raw/93256b91fa4124b39c9e67a7ca06ead4.png)
6. Return to the **Ethernet 2 Status** pop-up window and click **Details**. As shown in the figure below, DHCP is enabled and the IP automatically obtained is displayed.
![](https://main.qcloudimg.com/raw/2b8c5273070b0880a2e0b8482a572ce6.png)


### DHCP not set
If the CVM is not provided with DHCP, you need to configure the private IP by following the steps below:
1. Log in to the [Tencent Cloud console](https://console.cloud.tencent.com) and [bind the ENI to a CVM]#.E7.BB.91.E5.AE.9A.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8).
2. Log in to the CVM and select **Control Panel** -> **Network and Internet** -> **Network and Sharing Center**.
3. Click to edit the “Ethernet 2” secondary ENI.
![](https://main.qcloudimg.com/raw/b8498adcc2896f436a1bfdc96d11090d.png)
4. In the **Ethernet 2 Status** pop-up window, click **Properties**.
5. In the **Ethernet 2 Properties** pop-up window, double-click **Internet Protocol Version 4 (TCP/IPv4)**.
6. In the **Internet Protocol Version 4 (TCP/IPv4)** pop-up window, enter the actual IP and click **OK**.
![](https://main.qcloudimg.com/raw/71eefd1aa5299036a4789792b3bb9602.png)
7. In the **Ethernet 2 Properties** pop-up window, click **OK** to complete the configuration.
8. In the **Ethernet 2 Status** pop-up window, click **Details**. As shown in the figure below, DHCP is disabled and the IP manually entered is displayed.
![](https://main.qcloudimg.com/raw/3fe09a17eca280416d8ad64fb52a1675.png)
9. Ping the private address of a CVM that is in the same subnet. If the pinging succeeds, the configuration is correct. If no other CVM exists, you can bind the private IP address of the secondary ENI to a public IP address and then ping the public IP address.
