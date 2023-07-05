This document describes the preset policies offered by Tencent Kubernetes Engine (TKE). It shows you how to associate sub-accounts with preset policies to grant specific permissions. You can use this document as a reference to configure preset policies that are in line with your particular business needs.

## TKE Preset Policies
You can grant relevant permissions to sub-accounts by using the following preset policies:

| Policy | Description |
|------- |--------|
|`QcloudTKEFullAccess` | This policy grants full read/write access permissions for TKE, including permissions for TKE and related CVMs, CLBs, VPCs, monitors, and user groups. |
|`QcloudTKEInnerFullAccess`| This policy grants full access permission for TKE. However, since TKE involves the use of many products, we recommend configuring `QcloudTKEFullAccess`. |
|`QcloudTKEReadOnlyAccess` | This policy grants read-only permission for TKE. |

The following preset policies are used to grant permissions for specific TKE services. We do not recommend associating the following preset policies with a sub-account:

| Policy | Description |
|------- |--------|
| `QcloudAccessForCODINGRoleInAccessTKE` | This policy grants the relevant TKE permissions for the Coding service. |
| `QcloudAccessForIPAMDofTKERole` | This policy grants the relevant ENI permissions for the TKE service. |
| `QcloudAccessForIPAMDRoleInQcloudAllocateEIP` | This policy grants the relevant EIP permissions for the TKE service. |
| `QcloudAccessForTKERole` | This policy grants the relevant CVM, Tag, CLB, and CLS permissions for the TKE service. |
| `QcloudAccessForTKERoleInCreatingCFSStorageclass` | This policy grants the relevant CFS permissions for the TKE service. |
| `QcloudAccessForTKERoleInOpsManagement` | This policy associates the TKE service role (TKE_QCSRole) so that TKE can access other Tencent Cloud services, including CLS. |


## Associating Sub-accounts with Preset Policies
When setting user permissions during the creation of a sub-account, you can associate preset policies with the sub-account by [direct association](#direct) or [association via group](#byGroup).


<span id="direct"></span>
### Direct association

By directly associating your sub-account with a policy, the sub-account obtains the permissions contained in the policy. The direct association process is outlined below:

1. Log in to the CAM console and select **Users** -> **[User List](https://console.cloud.tencent.com/cam)** on the left sidebar.
2. On the **User List** page, find the target sub-account and click **Grant Permission** in the **Operation** column.
3. On the **Associate Policies** page, select the policies that you want to associate.
4. Click **OK**.

<span id="byGroup"></span>
### Association via group

By adding your sub-account to a user group, the sub-account automatically obtains the permissions that are associated with the user group. To disassociate the sub-account from the policies of the group, you simply need to remove the sub-account from the user group. The group association process is outlined below: 

1. Log in to the CAM console and select **Users** -> **[User List](https://console.cloud.tencent.com/cam)** on the left sidebar.
2. On the **User List** page, find the target sub-account and choose **More** -> **Add to Group** in the **Operation** column.
3. On the **Add to Group** page, select the target user group.
4. Click **OK**.


### Logging in to the sub-account for verification

Log in to the [TKE console](https://console.cloud.tencent.com/tke2) to verify that the features corresponding to the associated policies can be used and/or accessed properly. If so, this indicates that the sub-account was successfully authorized.





