## Basic CAM Concepts

A root account authorizes sub-accounts by binding policies. The policy settings can be specific to the level of **API, Resource, User/User Group, Allow/Deny, and Condition**.

#### User type

- **Root account**: A root accounts owns all the resources in Tencent Cloud and can access any of these resources.
- **Sub-account**: Sub-accounts include sub-users, WeCom sub-users, collaborators, and message recipients.

For detailed definitions of the root account and sub-accounts and descriptions of their features, see [User Types](https://intl.cloud.tencent.com/document/product/598/32633).

#### Resources and Permissions

- **Resource**: An object that Tencent Cloud services operate on, such as a CVM instance, a COS bucket, or a VPC instance.
- **Permission**: An authorization to allow or forbid users to perform certain operations. By default, **a root account has full access to all resources under the account**, while **a sub-account does not have access to any resources under its root account**.
- **Policy**: Syntax rule to define and describe one or more permissions. **A root account** performs authorization by **associating policies** with users/user groups.


## Using TEM with a Sub-account

To allow a sub-account such as collaborator to use TEM, you need to complete the following authorization operations:

1. To pass a role and its policies to TEM, the user must have the permission to **pass roles** to the service, i.e., the **PassRole** policy must be created. For detailed directions, see [Granting the `PassRole` policy](#PassRole).
2. The permission to use TEM is required. You can grant the target sub-account the `QcloudTEMFullAccess` or `QcloudTEMReadOnlyAccess` policy to grant it full or read-only access to TEM. For detailed directions, see [Granting the permission to use TEM](#Granting-the-permission-to-use-TEM).
3. TEM may call other Tencent Cloud products when used, so the root account needs to authorize the target sub-account accordingly. For more information, see [Granting permissions to access other Tencent Cloud products](#Granting-permissions-to-access-other-Tencent-Cloud-products).

[](id:PassRole)
### Granting the PassRole policy

#### Step 1. Create policies

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam).
2. On the left sidebar, click **Policies** to enter the policy management page.
3. Click **Create Custom Policy**.
4. In the **Select Policy Creation Method** pop-up window, click **Create by Policy Syntax**.
5. On the [Create by Policy Syntax](https://console.cloud.tencent.com/cam/policy/createV2) page, select **Blank Template** and click **Next**.
6. Enter the policy name and content and click **Create Policy**. Use the root account or a sub-account with admin permissions to create the following two custom policies:
	- Access to resources of Tencent Cloud products other than CLS:
	```json
	{
			"version": "2.0",
			"statement": {
					"effect": "allow",
					"action": "cam:PassRole",
					"resource": "qcs::cam::uin/${OwnerUin}:role/tencentcloudServiceRoleName/TEM_QCSLinkedRoleInAccessCluster"
			}
	}
	```
	- Access to CLS resources:
	```json
	{
			"version": "2.0",
			"statement": {
					"effect": "allow",
					"action": "cam:PassRole",
					"resource": "qcs::cam::uin/${OwnerUin}:role/tencentcloudServiceRoleName/TEM_QCSLinkedRoleInTEMLog"
			}
	}
```
Here, `${OwnerUin}` is the root account ID, which can be obtained on the [Account Info](https://console.cloud.tencent.com/developer) page in the console.


#### Step 2. Bind the policies to the user

1. On the left sidebar, click **User** > [**User List**](https://console.cloud.tencent.com/cam) to enter the user management page.
2. Select the target user and click **Authorize** in the **Operation** column.
3. Filter the policies created in **step 1** in the **Policy List**.
4. Click **OK** to bind the policies, which will be displayed in the **Policy List** of the user.

### Granting the permission to use TEM[](id:Granting-the-permission-to-use-TEM)

**Full access policy**

Grant a sub-user full access (including resource creation and management) to the TEM service.

```json
{
    "version": "2.0",
    "statement": [
        {
            "action": "tem:*",
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

You can also configure the system's [full read/write policy](https://console.cloud.tencent.com/cam/policy/createV2) to support this permission.

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. Click **[Policies](https://console.cloud.tencent.com/cam/policy)** on the left sidebar.
3. In the policy list, click **Create Custom Policy**.
4. In the **Select Policy Creation Method** pop-up window, select **Create by Syntax**.
5. In **Template Type**, search for "tem", select **QcloudTEMFullAccess** (full access to TEM), and click **Next**.
6. Click **Complete**.

Subsequent operation: Bind the created policy to the target user.

**Read-only policy**

Grant a sub-user read-only access to the TEM service.

```json
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "tem:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

You can also configure the system's [read-only policy](https://console.cloud.tencent.com/cam/policy/createV2) to support this permission.

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. Click **[Policies](https://console.cloud.tencent.com/cam/policy)** on the left sidebar.
3. In the policy list, click **Create Custom Policy**.
4. In the **Select Policy Creation Method** pop-up window, select **Create by Syntax**.
5. In **Template Type**, search for "tem", select **QcloudTEMReadOnlyAccess** (read-only access to TEM), and click **Next**.
6. Click **Create Policy**.

### Granting permissions to access other Tencent Cloud products[](id:Granting-permissions-to-access-other-Tencent-Cloud-products)

TEM may call the following Tencent Cloud products when used, so the root account needs to authorize the target sub-account separately to ensure that the sub-account can use TEM product features normally:

Below is the sample code for authorization:

```json
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cam:DescribeRoleList",
                "cvm:DescribeSecurityGroups",
                "vpc:DescribeVpcEx",
                "vpc:DescribeSubnetEx",
                "tse:DescribeSREInstances",
                "cls:DescribeLogsets",
                "cls:DescribeTopics",
                "cfs:DescribeCfsFileSystems",
                "ssl:DescribeCertificate",
                "tcr:DescribeRepositoryOwnerPersonal",
                "tcr:DescribeRepositories",
                "tcr:DescribeInstances",
                "tcr:DescribeInternalEndpoints",
                "tcr:CreateInstanceToken"
            ],
            "resource":[
                "*"
            ]
        }
    ]
}
```
