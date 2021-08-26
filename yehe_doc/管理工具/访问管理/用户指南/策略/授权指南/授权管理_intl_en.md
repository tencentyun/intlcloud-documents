## Overview
When a user or user group is created, they have no permissions by default. You can associate a policy with them to grant them the corresponding operation permissions.


## Prerequisites
- You have [created a sub-user](https://intl.cloud.tencent.com/document/product/598/13674) or [user group](https://intl.cloud.tencent.com/document/product/598/33380).
- If you need to associate a custom policy, please [create one](https://intl.cloud.tencent.com/document/product/598/35596) first.

## Directions
You can associate policies with users/user groups and vice versa. These two methods have different operation entries, but they implement the same feature.

### Associating policy with user/user group
<dx-tabs>
::: Associating\spolicy\swith\suser

1. On the **[Policies](https://console.cloud.tencent.com/cam/policy)** page in the CAM console, select a policy type.
>?This document takes a **preset policy** as an example. You can also select a **custom policy**.
2. Search for the preset policy you want to associate and click **Associated Users/Groups** in the **Operation** column.
![](https://main.qcloudimg.com/raw/c3c39a4e97345a3b31728f0e1b0ed379.png)
3. In the **Associate Users/User Groups** pop-up window, select the user you want to associate and click **OK** to complete the association.
![](https://main.qcloudimg.com/raw/59476a8d463f448046cca3362deaae7c.png)
:::
::: Associating\spolicy\swith\suser\sgroup
1. On the **[Policies](https://console.cloud.tencent.com/cam/policy)** page in the CAM console, select a policy type.
>?This document takes a **preset policy** as an example. You can also select a **custom policy**.
2. Search for the preset policy you want to associate and click **Associated Users/Groups** in the **Operation** column.
![](https://main.qcloudimg.com/raw/c3c39a4e97345a3b31728f0e1b0ed379.png)
3. In the **Associate Users/User Groups** pop-up window, click **Switch to User Group**.
4. Select the user group you want to associate and click **OK** to complete the association.
![](https://main.qcloudimg.com/raw/65c0a435424d34db5e6b529e07ca1e99.png)
:::
</dx-tabs>


### Associating user/user group with policy

<dx-tabs>
::: Associating\suser\swith\spolicy

1. On the **Users** > **[User List](https://console.cloud.tencent.com/cam)** page in the CAM console, find the user to be authorized and click **Authorization** in the **Operation** column to enter the **Associate Policy** page.
![](https://main.qcloudimg.com/raw/a29dc8dd4c1a7e587140b9dfeb101b58.png)
2. On the **Associate Policy** page, select a policy type.
>?All policies are displayed by default. You can filter custom or preset policies to find specific policy information.
3. Select the policy you want to associate and click **OK** to complete the association.
![](https://main.qcloudimg.com/raw/a743ce549be775bd50b42296c03af43b.png)
:::
::: Associating\suser\sgroup\swith\spolicy
1. On the **[User Groups](https://console.cloud.tencent.com/cam/groups)** page in the CAM console, click the name of the target user group to enter the user group details page.
2. On the user group details page, click **Associate Policy** to enter the **Associate Policy** page.
![](https://main.qcloudimg.com/raw/78e647a8af6f34e96c384e5f02fd15d0.png)
3. On the **Associate Policy** page, select a policy type.
>?All policies are displayed by default. You can filter custom or preset policies to find specific policy information.
4. Select the policy you want to associate and click **OK** to complete the association.
![](https://main.qcloudimg.com/raw/a743ce549be775bd50b42296c03af43b.png)
:::
</dx-tabs>

## Relevant Documents

 For more information on the concept of policy, please see [Policy](https://intl.cloud.tencent.com/document/product/598/10601). 

