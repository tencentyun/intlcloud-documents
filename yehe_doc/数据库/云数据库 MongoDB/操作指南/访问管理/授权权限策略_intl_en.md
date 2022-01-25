Permissions of Tencent Cloud root accounts and sub-accounts are separated. You can grant sub-accounts different permissions as needed, which avoids security risks caused by exposure of your Tencent Cloud account key. 

## Granting Sub-account permission policy
### Background
Company A activates the TencentDB for MongoDB service and wants its team members to manipulate the involved resources. For security or trust considerations, it doesn't want to directly disclose its Tencent Cloud account key to the team members; instead, it wants to create corresponding sub-accounts for them, which can manipulate resources only with authorization by its root account and don't require separate usage calculation and billing, as all fees are charged to its Tencent Cloud account. It also wants to be able to revoke or delete the operation permissions of sub-accounts at any time.

### Directions
#### Step 1. Create a sub-account user
You can create a sub-account user through the console or an API.
- Log in to the CAM console and enter the [User List](https://console.cloud.tencent.com/cam) page to create a user. For detailed directions, see [Creating Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).
- Create a sub-user and configure permissions for them by calling the `AddUser` API with an access key. For more information, see [AddUser](https://intl.cloud.tencent.com/document/product/598/32265).

#### (Optional) Step 2. Create a custom permission policy
1. On the [Policies](https://console.cloud.tencent.com/cam/policy) page in the CAM console, search for a target policy by policy name in the search box in the top-right corner.
2. If the permission policy does not exist, you need to customize one. For detailed directions, see [Creating Custom Policy](https://intl.cloud.tencent.com/document/product/598/35596).

#### Step 3. Assign the permission policy to the sub-account
- On the [Policies](https://console.cloud.tencent.com/cam/policy) page in the CAM console, find the target permission policy and associate it with the target sub-account. For detailed directions, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).
- On the [User List](https://console.cloud.tencent.com/cam) page in the CAM console, find the target sub-account and associate them with the target policy. For detailed directions, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

### References
#### Logging in to console
You can let your team members use a sub-account to log in to the Tencent Cloud console and access TencentDB for MongoDB. For detailed directions, see [Logging in to Console with Sub-account](https://intl.cloud.tencent.com/document/product/598/38248).

#### Modifying sub-account
You can view and modify the information of a sub-account as instructed in [User Information](https://intl.cloud.tencent.com/document/product/598/34005).

#### Deleting sub-account
You can revoke or delete the operation permissions of a sub-account as instructed in [Deleting Sub-Users](https://intl.cloud.tencent.com/document/product/598/32653).

## Granting Permission Policy Across Tencent Cloud Accounts
### Background
Company A activates TencentDB for MongoDB and wants company B to have part of the permissions of its TencentDB for MongoDB operations, such as monitoring, instance read/write, and slow query operation. Company B wants to have a sub-account to take care of such businesses. In this case, company A can authorize the root account of company B to access TencentDB for MongoDB resources through a role. For the specific concept and use cases of role, see [Role Overview](https://intl.cloud.tencent.com/document/product/598/19420).

### Directions
#### Step 1. Company A creates a role for company B
1. Log in to the CAM console and go to the [Roles](https://console.cloud.tencent.com/cam/role) page.
2. Click **Create Role**. In the **Select role entity** window, select **Tencent Cloud Account**
3. On the **Create Custom Role** page, create a role.
   a. On the **Enter role entity info** page, select **Other root account** as **Tencent Cloud account**, enter the root account of company B as **Account ID**, set other parameters as prompted, and click **Next**.
   b. On the **Configure role policy** page, select the target policy and click **Next**.
   c. On the **Review** page, enter a role name such as `DevOpsRole` in the **Role Name** box, review the selected policy, and click **Done**.

#### Step 2. Company B grants a sub-account the permission to assume the role
1. On the [Policies](https://console.cloud.tencent.com/cam/policy) page in the CAM console, click **Create Custom Policy**.
2. In the **Select Policy Creation Method** window, select **Create by Policy Syntax**.
3. On the **Create by Policy Syntax** page, create a policy.
   a. In the **Select a template type** section, select **Blank Template** and click **Next**.
   b. On the **Edit Policy** page, enter a policy name such as `sts:AssumeRole` in the **Policy Name** input box.
   c. In **Policy Content**, set the policy content according to the policy syntax and click **Done** as follows:
```
{
    "version": "2.0",
    "statement": [
    {
        "effect": "allow",
        "action": ["name/sts:AssumeRole"],
        "resource": ["qcs::cam::uin/12345:RoleName/DevOpsRole"]
    }
    ]
}
```
4. Return to the **[Policies](https://console.cloud.tencent.com/cam/policy)** page, find the created custom policy, and click **Associate Users/Groups** in the **Operation** column.
5. Associate the custom policy with the sub-account of company B and click **OK**.

#### Step 3. Company B uses the sub-account to access Tencent Cloud resources through the role
1. Log in to the console with the sub-account of company B and select **Switch Role** in the profile photo drop-down list.
2. On the role switch page, enter the root account of company A and role name to switch to the role of company A. 

### References
- You can modify a role as instructed in [Modifying a Role](https://intl.cloud.tencent.com/document/product/598/19389).
- You can delete a role as instructed in [Deleting a Role](https://intl.cloud.tencent.com/document/product/598/19388).
- For more information on how to use CAM, see [Overview](https://intl.cloud.tencent.com/document/product/598/17848).

