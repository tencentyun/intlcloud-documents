You can bind multiple EIPs to a NAT gateway and assign them to different CVMs based on [SNAT rules](#cjgz) for the public network access.

Assume that a NAT gateway is bound with EIPs including EIP1, EIP2, EIP3, and EIP4. The load balancer distributes the access traffic to these EIPs for CVM access to the public network. If EIP1, EIP2 and EIP3 are added to the SNAT address pool, CLB will distribute the access traffic to the three EIPs, and CVM will use them to access the public network.
>?
>- When the load on a CVM instance surges, one EIP may not be enough to support huge access traffic, so you can choose to configure multiple EIPs.
>- The maximum number of connections from one EIP to the same destination service is 55,000. If the limit is exceeded, packet loss occurs.
>- In a NAT gateway, an EIP can be set in the SNAT rule and port forwarding rule at the same time. See [Managing Port Forwarding Rules](https://intl.cloud.tencent.com/document/product/1015/30237).
>


This document describes how to create and manage a SNAT rule.

## SNAT Rule Limits
- When an EIP is disassociated from a NAT gateway, the SANT rule is also deleted if the EIP is the only EIP.
- If the subnet configured for a SNAT rule does not exist, the SNAT rule is deleted as well.
- If the CVM configured for a SNAT rule does not exist, the SNAT rule is also deleted if this is the last CVM; otherwise, the CVM will be deleted from the SNAT rule.


## Prerequisites
Before creating a SNAT rule, make sure the route table where the subnet resides points to the corresponding NAT gateway. See [Routing to NAT Gateway](https://intl.cloud.tencent.com/document/product/1015/30236).


## Creating a SNAT rule [] (id:cjgz)
1. Log in to the [**NAT Gateway console**](https://console.cloud.tencent.com/vpc/nat?fromNav).
2. In the list, click the ID of the desired NAT gateway to go to its details page.
3. Select the **SNAT Rule** tab and enter the SNAT rule admin page.
4. Click **Create**.
5. In the **Create SNAT Rule** dialog box, configure a SNAT rule as follows:
   + **Source IP Range Granularity**: select **Subnet** or **CVM**.
     + Subnet: when **Subnet** is selected, the associated route table of the subnet must point to the NAT Gateway, allowing CVMs in the subnet to access the public network based on the SNAT rule.
     + CVM: when **CVM** is selected, the route table associated with the subnet where the CVM instance resides must point to the NAT Gateway. Only the selected CVM instances can access the public network based on the SNAT rule.
   + **Subnet**: select a subnet or the subnet where the CVM instance resides.
   + **CVM**: select CVM instances from the drop-down list if **CVM** is selected for **Source IP Range Granularity**.
   + **Public IP**: assign EIP for the public network access.
   + **Description**: enter the descriptive information with 60 or less characters.
![](https://main.qcloudimg.com/raw/551d8f30e40209db9aa4f249d5de4120.png)
6. After the configuration is completed, click **Submit**.    

## Modifying a SNAT Rule
>? Please note that changing the public IP of an existing SNAT rule may cause business interruption, which will be resumed after reconnection.
>
1. On the SNAT rule tab, click **Edit** on the right side of SNAT rule entry to enter the dialog box.
![]()
2. Modify the public IP address or description, and click **Submit**.
3. Click the pencil icon next to **Description** of the selected SNAT rule to directly modify its description.
    ![]()

## Querying SNAT Rules
1. In the search box at the top right of the SNAT rule tab, click to select the following filters, and enter the corresponding parameter values in the input box.
![]()
2. Click the search icon to filter results.
![]()
3. Click the **Subnet/CVM ID** to view the resource details.


## Deleting SNAT Rules
You can delete SNAT rules if CVM can access the public network without a specified EIP.
- **Delete a single SNAT rule**
 1. Click **Delete** to the right of the SNAT rule entry on the SNAT rule tab.
 2. Click **Confirm** to delete the selected SNAT rule.
![]()
- **Batch delete SNAT rules**
 1. On the SNAT rule tab, check several SNAT rules and click **Delete** at the top.
![]()
 2. In the pop-up window, click **Delete**.
![]()
