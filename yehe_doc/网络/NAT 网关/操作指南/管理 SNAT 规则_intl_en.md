You can bind EIPs to the NAT Gateway and assign them to different CVMs based on [SNAT] rules](#cjgz) for the public network access.

Assume a NAT Gateway is bound with EIPs including EIP1, EIP2, EIP3, and EIP4, they will automatically share the public network access traffic. If you add EIP1, EIP2, and EIP3 to the SNAT address pool, these in the address pool will be used to access the public network and share the access traffic.

This document describes how to create and manage a SNAT rule.

<span id="cjgz"></span>
## Creating a SNAT Rule
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Choose *NAT Gateway** on the left sidebar to go to the **NAT Gateway** page.
3. Click the **ID/Name** of the target gateway to enter its details page.
4. Select the **SNAT Rule** tab.
5. Click **Create**.
6. In the **Create SNAT Rule** dialog box, configure a SNAT rule as follows:
   + **Source IP Range Granularity**: select **Subnet** or **CVM**.
     + Subnet: when **Subnet** is selected, the associated route table of the subnet must point to the NAT Gateway, allowing CVMs in the subnet to access the public network based on the SNAT rule.
     + CVM: when **CVM** is selected, the route table associated with the subnet where the CVM instance resides must point to the NAT Gateway. Only the selected CVM instances can access the public network based on the SNAT rule.
   + **Subnet**: select a subnet or the subnet where the CVM instance resides.
   + **CVM**: select CVM instances from the drop-down list if **CVM** is selected for **Source IP Range Granularity**.
   + **Public IP**: assign EIP for the public network access.
   + **Description**: enter the descriptive information, which cannot exceed 60 characters.
![](https://main.qcloudimg.com/raw/6d7cfff1507c9442b70ad008f72cb892.png)
7. After the configuration is completed, click **Submit**.    

## Editing a SNAT Rule
>? Please note that changing the public IP of an existing SNAT rule may cause business interruption, which will be resumed after reconnection.
>
1. Select the [SNAT Rule](https://console.cloud.tencent.com/vpc/nat/detail?rid=1&id=nat-oh8mtvzm&tab=snat) tab and click **Edit** on the right of a SNAT rule.
![](https://main.qcloudimg.com/raw/32cb6cd5d8a19f5e07ae80a76264faa0.png)
2. Modify the public IP address or description, and click **Submit**.
3. Click the pencil icon next to **Description** of the selected SNAT rule to directly modify its description.
    ![](https://main.qcloudimg.com/raw/64525964961cc447f448819213b0ff8e.png)

## Querying SNAT Rules
1. In the top-right corner search box of the [SNAT Rule](https://console.cloud.tencent.com/vpc/nat/detail?rid=1&id=nat-oh8mtvzm&tab=snat) tab, click to select a filter and enter the corresponding parameter value in the text box.
![](https://main.qcloudimg.com/raw/61057a1b9194a4937056aad3b6694c0e.png)
2. Click the search icon to filter results.
![](https://main.qcloudimg.com/raw/0f794a33ac4d48d33ff8838126e9b5b9.png)
3. Click the **Subnet/CVM ID** to view the resource details.


## Deleting SNAT Rules
You can delete SNAT rules if CVM can access the public network without a specified EIP.
- **Delete a single SNAT rule**
 1. Select the [SNAT Rule](https://console.cloud.tencent.com/vpc/nat/detail?rid=1&id=nat-oh8mtvzm&tab=snat) tab and click **Delete** on the right of the target SNAT rule.
 2. Click **Confirm** to delete the selected SNAT rule.
![](https://main.qcloudimg.com/raw/686a27e91f884856ea74b2279696567f.png)
- **Batch delete SNAT rules**
 1. On the [SNAT Rule](https://console.cloud.tencent.com/vpc/nat/detail?rid=1&id=nat-oh8mtvzm&tab=snat) tab, select SNAT rules and click **Delete** at the top of the list.
![](https://main.qcloudimg.com/raw/8c1fa2675cf1159e662661328bd388d8.png)
 2. In the pop-up window, click **Delete** to complete the deletion.
![](https://main.qcloudimg.com/raw/364b44365a78ac81f691a23baa3f0138.png)
