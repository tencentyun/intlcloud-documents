>? The following operations use Windows 2012 as an example.
>

## Directions
### Windows provided with DHCP
If the CVM is provided with DHCP, you can view its secondary ENI and IP by following steps below without any further configuration:
1. Log in to the CVM, and select **Control Panel** -> **Network and Internet** -> **Network and Sharing Center** to check the secondary ENI that has been automatically obtained.
2. Click the “Ethernet 2” secondary ENI to view its information.
3. In the **Ethernet 2 Status** pop-up window, click **Properties**.
4. In the **Ethernet 2 Properties** pop-up window, double-click **Internet Protocol Version 4 (TCP/IPv4)**.
5. In the **Internet Protocol Version 4 (TCP/IPv4)** pop-up window, you can see **Obtain an IP address automatically** is selected, so there is no need to enter one.
6. Return to the **Ethernet 2 Status** pop-up window and click **Details**. As shown in the figure below, DHCP is enabled and the IP automatically obtained is displayed.

### DHCP not set
If the CVM is not provided with DHCP, you need to configure the private IP by following the steps below:
1. Log in to the [Tencent Cloud console](https://console.cloud.tencent.com) and [bind the ENI to a CVM]#.E7.BB.91.E5.AE.9A.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8).
2. Log in to the CVM and select **Control Panel** -> **Network and Internet** -> **Network and Sharing Center**.
3. Click to edit the “Ethernet 2” secondary ENI.
4. In the **Ethernet 2 Status** pop-up window, click **Properties**.
5. In the **Ethernet 2 Properties** pop-up window, double-click **Internet Protocol Version 4 (TCP/IPv4)**.
6. In the **Internet Protocol Version 4 (TCP/IPv4)** pop-up window, enter the actual IP and click **OK**.
7. In the **Ethernet 2 Properties** pop-up window, click **OK** to complete the configuration.
8. In the **Ethernet 2 Status** pop-up window, click **Details**. As shown in the figure below, DHCP is disabled and the IP manually entered is displayed.
9. Ping the private address of a CVM that is in the same subnet. If the pinging succeeds, the configuration is correct. If no other CVM exists, you can bind the private IP address of the secondary ENI to a public IP address and then ping the public IP address.
