### There is no network connection after I log in to the CVM. How do I solve this problem?
If there is no network access (for example, the webpage is inaccessible) after you log in to the CVM, you need to check the DNS configuration. Set the CVM to obtain the DNS address automatically by following the instructions below.
> The following operations take Windows Server 2012 as an example.
> 
1. Log in to the Windows CVM.
2. On the desktop, click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;width: 22px;"> and select **Control panel** -> **Network and Internet** -> **View network status and tasks** -> **Change adapter settings**.
3. Right-click **Ethernet** and select **Properties** to open the “Ethernet Properties” window.
4. In the “Ethernet Properties” window, double-click and open the **Internet Protocol Version 4 (TCP/IPv4) Properties** window.
5. In the **Internet Protocol Version 4 (TCP/IPv4) Properties** window, select **Obtain an IP address automatically** and **Obtain DNS server address automatically**, and click **OK**, as shown below:
![](https://main.qcloudimg.com/raw/8a597efe05adc2f96d4b40b6cd633ca4.png)

### Can a VPC instance interconnect with the classic network instance?

#### Yes, but it has the following restriction:
The VPC IP address range (CIDR) must be 10.0.0.0/16 - 10.0.47.0/16 (including subsets). Otherwise, there will be conflicts.

#### Directions
Log in to the [VPC Console](https://console.cloud.tencent.com/vpc/vpc?rid=1), click the VPC ID/name to access its details page, and then click the **Classiclink** tab to associate the classic network CVM to be interconnected. 

### How do I view classic network CVMs that are interconnected with VPC CVMs?
Log in to the [VPC Console](https://console.cloud.tencent.com/vpc/vpc?rid=1), click the VPC ID/name to access its details page, and view classic network CVMs interconnected with VPC CVMs in **Classiclink**.

### Can the CVM be switched to an overseas network?
After being purchased, the network cannot be changed for CVM. If you need an overseas network, we recommend that you return the CVM and purchase an overseas CVM.

### How do I configure a private network DNS?
Please see [Private Network Access](https://intl.cloud.tencent.com/document/product/213/5225).

### Within the same IP range, the VPN can obtain the IP address of an IP range but cannot access the internet. How do I solve this problem?

Please check that the following configurations are correct:
1. Are the manually added IP and the automatically obtained IP in the same IP subnet? Are the subnet masks the same? Is the default gateway configured? Is the default gateway address correct?
2. Is DNS configured and is the DNS address correct?
3. If all of the configurations above are correct, check if the statically configured IP address has an IP conflict.
  
If none of the above works, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us.

### How do I add CVMs under accounts A and B to the same subnet?

By default, accounts are not interconnected by network. To interconnect accounts, see [Creating Cross-account Peering Connection](https://intl.cloud.tencent.com/document/product/553/35190) or [Network Instance Interconnection Crossing Account](https://intl.cloud.tencent.com/document/product/1003/31987).
