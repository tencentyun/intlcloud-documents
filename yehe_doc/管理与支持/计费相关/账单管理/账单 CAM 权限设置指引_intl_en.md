## Overview
This document shows you how to grant a sub-account (sub-user/collaborator) read-only or read/write access to bills via the CAM console.

## Directions

### Creating sub-user/collaborator
For detailed directions on how to create a sub-user/collaborator, see [Creating Sub-user](https://intl.cloud.tencent.com/document/product/598/13674)/[Creating Collaborator](https://intl.cloud.tencent.com/document/product/598/32639).

### Associating preset policy

1. On the [User List](https://console.cloud.tencent.com/cam) page, find the target sub-user/collaborator and click **Authorize**.
![](https://main.qcloudimg.com/raw/4ebbec079bc19c25e5e2f1008e5e77ca.jpg)
2. Select a [billing-related preset policy](#1) (e.g., QcloudFinanceBillReadOnlyAccess) you want to associate and click **Confirm**.
![](https://main.qcloudimg.com/raw/b7b4565679689521ca987000409b95c5.jpg)

For detailed directions, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).


## Billing-related Preset Policies[](id:1)

| Policy                          | Access             | Description                                                         |
| ------------------------------- | ---------------- | ------------------------------------------------------------ |
| QcloudFinanceBillReadOnlyAccess | Read-only access to bills | The sub-user/collaborator can read the bills of the root account and its sub-accounts, but are not allowed to configure bill storage, confirm bills, apply for stamps, or set cost allocation tags.<br>**Note: **If a sub-user/collaborator had been associated with the QCloudResourceFullAccess policy before July 29, 2021, you need to disassociate and associate the policy again; otherwise, all billing-related permissions will be denied.|
| QcloudFinanceBillFullAccess     | Read/Write access to bills | The sub-user/collaborator has read/write access to the bills of the root account and its sub-accounts.<br>**Notes:**<ul><li>If a sub-user/collaborator had been associated with the QCloudResourceFullAccess policy before July 29, 2021, you need to disassociate and associate the policy again; otherwise, all billing-related permissions will be denied.</li><li>To allow the sub-user/collaborator to configure bill storage, you also need to associate it with the following policies:<ul><li>QcloudCOSGetServiceAccess (access to COS buckets)</li><li>QcloudCamSubaccountsAuthorizeRoleFullAccess (permission to authorize CAM service roles)</li></ul></li></ul> |
| QCloudFinanceFullAccess         | All billing-related access     | The sub-user/collaborator can perform any billing-related operation, such as payment or invoicing, for the root account and its sub-accounts.   |
| AdministratorAccess             | Administrator access       | The sub-user/collaborator can manage all users and their permissions, billing information, and resources under the root account. |
