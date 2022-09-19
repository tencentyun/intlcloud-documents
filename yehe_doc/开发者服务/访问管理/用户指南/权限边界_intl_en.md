## Concept

Permissions boundary is an advanced feature used by Tencent Cloud to set a permissions boundary for a sub-account/role. After you set a permissions boundary for a sub-account/role, it can only perform operations allowed by both the associated policy and the permissions boundary. A permissions boundary only limits the maximum scope of permissions owned by a sub-account/role, but cannot be used to set permissions for the sub-account/role.
![](https://main.qcloudimg.com/raw/f615ce99d062318ced060777f4f3435b.png)

## Overview

You can use a preset or custom policy to set permissions for a sub-account/role. This policy is the maximum scope of permissions that the sub-account/role can have. This document describes how to use a permissions boundary to set the maximum scope of permissions for a sub-account.
Suppose a company's Tencent Cloud resource admin needs to set permissions for Ops employees to meet the following requirements:

- The company has two Ops employees, each with their own sub-account: 'test1' and 'test2'.
- The employee with the sub-account `test1` only needs to manage all TencentDB for MySQL permissions under the root account.
- The employee with the sub-account `test2` only needs to manage the operation permission for the server with the instance ID of `ins-1` under the root account.
- The company stipulates that all operations on CVM and TencentDB for MySQL under the root account by sub-accounts must be performed in the IP range of the company (10.217.182.3/24 or 111.21.33.72/24).

## Directions

### Setting permissions for sub-account `test1`

1. Log in to the admin account and enter the [user list page](https://console.cloud.tencent.com/cam).
2. On the user list page, find the sub-account `test1` and click the user's nickname to enter the user details page.
3. In the **Permissions Policy** section under the **Permission** tab, click **Associate Policy** and select the `QcloudCDBFullAccess` policy to set all TencentDB for MySQL permissions for the sub-account `test1`.
4. In the **Permissions Boundary** section under the **Permission** tab, click **Set Boundary** to enter the **Set Permissions Boundary** page.
5. On the permissions boundary setting page, click **Create Custom Policy** to enter the custom policy creation page.
6. On the custom policy creation page, set the policy name to `policygen-1`.
7. In **Visual Policy Generator**, add the following information:
   - Effect: Select **Allow**.
   - Service: Select **TencentDB for MySQL**.
   - Action: Select **All actions** and click **OK**.
   - Resource: The default value is **All resources (*)**.
   - Condition: Select **Source IP** and enter `10.217.182.3/24, 111.21.33.72/24` as the IP value.
8. Click **Create** to enter the permissions boundary setting page.
9. On the permissions boundary setting page, select the created custom policy in the policy list.
10. Click **Set Boundary**.

### Setting permissions for sub-account `test2`

1. Log in to the admin account and create a custom policy syntax named `policygen-2` by referring to the following policy syntax. For more information, see [Creating Custom Policy>>Creating by policy syntax](https://www.tencentcloud.com/document/product/598/35596).
```json
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "resource":[
                "qcs::cvm:gz::instance/ins-1"
            ],
            "action": [
                "name/cvm:*"
            ]
        }
    ]
}
```
2. On the [user list page](https://console.cloud.tencent.com/cam), find the sub-account `test2` and click the user's nickname to enter the user details page.
3. In the **Permissions Policy** section under the **Permission** tab, click **Associate Policy** and select the `policygen-2` policy to set the operation permission of the CVM instance named `ins-1` for the sub-account `test2`.
4. In the **Permissions Boundary** section under the **Permission** tab, click **Set Boundary** to enter the **Set Permissions Boundary** page.
5. On the permissions boundary setting page, click **Create Custom Policy** to enter the custom policy creation page.
6. On the custom policy creation page, set the policy name to **policygen-3**.
7. In **Visual Policy Generator**, add the following information:
   - Effect: Select **Allow**.
   - Service: Select **CVM**.
   - Action: Select **All actions** and click **OK**.
   - Resource: The default value is **All resources (*)**.
   - Condition: Select **Source IP** and enter `10.217.182.3/24, 111.21.33.72/24` as the IP value.
8. Click **Create** to enter the permissions boundary setting page.
9. On the permissions boundary setting page, select `policygen-3` in the policy list.
10. Click **Set Boundary** to complete the permission setting process.
