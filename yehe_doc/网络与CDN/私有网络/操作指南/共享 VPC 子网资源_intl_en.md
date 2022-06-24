Currently, Tencent Cloud Group Account Management supports sharing of subnet resources in a VPC. With this feature, a management account can create a shared unit, select the VPC subnet resources under the account, and share them with specified member accounts. After the resources are successfully shared, members can log in to the console to view and use the shared resources.

## Prerequisites
The group account has added member accounts to the organization. 

## Directions
### Step 1. Share subnets with specified members
1. Log in to the [Group Account Management console](https://console.cloud.tencent.com/organization/setting) and select **Resource Sharing** > [**Shared by Me**](https://console.cloud.tencent.com/organization/share-by) on the left sidebar.
2. Select the **Shared Unit** tab, select the region of the subnet to be shared at the top of the page, and click **Create Shared Unit**.
3. On the **Create Shared Unit** page, configure the following information.
 - **Basic Info**
    - **Name**: Shared unit name, which can be customized.
 - **Shared Resources**
     - **Resource Type**: **Subnet** is selected by default.
     - **Shared Resources**: Select up to ten subnets to be shared as shown below:
>?The list displays the information of the subnets in the region selected by the current account.
>
![]()
 - **Shared Account**
    - **Account ID**: Click **Add Shared Account**, select the member account in the **Add Shared Account** pop-up window, and click **Save**.
4. Click **Complete**.
You can select the **Shared Resources** and **Shared Account** tabs to view the shared resources and the member accounts.

### Step 2. View subnets with a member account
1. Log in to the [Group Account Management console](https://console.cloud.tencent.com/organization/setting) and select **Resource Sharing** > **[Shared with Me](https://console.cloud.tencent.com/organization/share-with)** on the left sidebar.
2. On the **Shared with Me** page, select the region of the shared subnet at the top:
 - Select the **Shared Unit** tab to view the shared unit.
 - Select the **Shared Resources** tab to view the available shared subnet resources.
 You can also log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc), select **[Subnet](https://console.cloud.tencent.com/vpc/subnet?rid=1)** on the left sidebar, and select the region at the top of the **Subnet** page to view the shared subnet resources as shown below:
![]()


## Billing
Tencent Cloud Group Account Management is free of charge, and you only need to pay for the Tencent Cloud resources used under your account. For example, you need to pay standard fees for Tencent Cloud CVM instances and public network bandwidth.

## Appendix
<dx-tabs>
::: Use limits
| Resource Item | Quota |
|---------|---------|
| Number of members that resources can be shared with| 20 |
| Number of resources that can be shared each time| 10 |
| Number of times that a resource can be shared| 10 |

>?
>+ Other VPC quotas are the same as the current settings. The quotas are shared by the resource owners and users.
>+ If there are resources created by other member accounts (resource users) under the VPC/subnet, the subnet cannot be deleted.
>

:::
::: Permissions of resource owners and users
After a group management account (resource owner) shares VPC subnet resources with member accounts (resource users), their permissions to manipulate the shared subnet and the Tencent Cloud resources in it are as listed below.

| Role |When Subnet Resources Are Shared | When Subnet Resources Are Not Shared|After Sharing Is Exited|
|---------|---------|---------|---------|
| Resource owner |<li>They can use and manage all resources under the VPC, such as Direct Connect gateways, VPN Gateway, NAT Gateway, CCN, ACLs, and route tables. </li><li>They cannot modify or delete resources created by resource users, such as CVM, TencentDB, and CLB.</li>|They can use and manage all resources under the VPC. |Resources are no longer shared and all associated subnets are disassociated.|
| Resource user |<li>They can use existing VPC resources but cannot create or modify them (for example, CVM instances can use the VPC's existing NAT gateways to access the public network, but cannot create one).</li><li>They can create resources under the shared subnet, such as CVM, TencentDB, and CLB.</li><li>They cannot view or use resources created by other resource users.</li>  |<li>They can still use the resources they've created but cannot create resources in the subnet.</li> <li>They cannot use the existing resources under the VPC.</li> | All subnet resources are no longer shared.|

The permissions of the resource owners and users to manipulate other network resources in the VPC are as listed below.


| Network Resource |Resource User | Resource Owner |
|---------|---------|---------|
| VPC | They can only view the VPC of the shared subnet. |They have all the operation permissions but cannot delete a VPC with shared resources. |
| Subnet |They can only view the shared subnet.|They have all the operation permissions but cannot delete a subnet that is shared with other users. |
| Route table | They can only view the route table bound to the shared subnet and the routing policy of that table. |They have all the operation permissions. |
| Network ACL |They can view the ACL bound to the shared subnet.  |They have all the operation permissions. |
| CCN |They have no operation permissions.|They have all the operation permissions. All VPC resources (including those created by the resource owners/users) can communicate with other VPCs/IDCs over CCN. |
| VPN Gateway |They have no operation permissions.|They have all the operation permissions. All VPC resources (including those created by the resource owners/users) can communicate with other IDCs through a VPN gateway. |
| NAT gateway |They have no operation permissions.|They have all the operation permissions. All VPC resources (including those created by the resource owners/users) can access the internet through a NAT gateway. |
| Direct Connect gateway |They have no operation permissions.|They have all the operation permissions. All VPC resources (including those created by the resource owners/users) can communicate with other IDCs through the Direct Connect gateway. |
:::
</dx-tabs>

