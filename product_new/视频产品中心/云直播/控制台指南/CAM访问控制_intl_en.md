CSS supports permission control via CAM, where you can manage your CSS domain names, configurations, and information of your account. You can create, manage, or terminate users/user groups and grant different API access permissions to different users/user groups for the purpose of identity management and policy control.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks.

## Basic Concepts

- Root account: It is a registered Tencent Cloud account.
- Sub-user: It is created and fully owned by a root account.
- Collaborator: It has the identity of a root account. After it is added as a collaborator of the current root account, it becomes one of the sub-accounts of the current root account.
- User group: It is created for users with the same functions and can be associated with a policy for centralized authorization management.

For more information on the definitions and permission, see [CAM Users](https://intl.cloud.tencent.com/document/product/598/13665).

## Directions
### Step 1. Create a user/user group

One or more users with specific roles and policies can be created under one root account. A sub-user has a specific ID and identity credential that can be used to log in to the Tencent Cloud Console for configuration. It also has API access permission. You can log in to the Tencent Cloud Console and go to [CAM](https://console.cloud.tencent.com/cam/) to create a user, as shown below:

![](https://main.qcloudimg.com/raw/809314273b9a8a01dfd9e686775df4bd.png)
For more information, see [CAM Sub-users](https://intl.cloud.tencent.com/document/product/598/13674) and [User Groups](https://intl.cloud.tencent.com/document/product/598/10599).

### Step 2. Add a policy to a user/user group

You can add policies and authorize users/user groups on the User/User Group Management and Policy Management pages. For more information, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

- Method 1: Go to the User/User Group page, select a user/user group, click **Authorize** in the "Operation" column, select the corresponding CSS policy, and click **OK**.
![](https://main.qcloudimg.com/raw/e90b74bc2279512a5c075a57296ea2f1.png)

- Method 2: Go to the Policy page, select the policy to be added, click **Bind User/Group**, select the user/user group, and click **OK**.
![](https://main.qcloudimg.com/raw/c7948939b954b8f84a7a2ee9e5041ef4.png)

**Policies that can be added include:**
1. Preset policy: Click "Policy" on the left sidebar to enter the Policy page, where you can query all current policies. CSS preset policies include [QcloudLIVEFullAccess](https://console.cloud.tencent.com/cam/policy/detail/9545933&QcloudLIVEFullAccess&2) (read/write policy) and [QcloudLIVEReadOnlyAccess](https://console.cloud.tencent.com/cam/policy/detail/13346800&QcloudLIVEReadOnlyAccess&2) (read-only policy).
2. Custom policy: Go to the Policy page, click **Create Custom Policy**, and select **Create by policy generator**. For more information, see [Custom Policies](https://intl.cloud.tencent.com/document/product/598/10601#.E8.87.AA.E5.AE.9A.E4.B9.89.E7.AD.96.E7.95.A5).

**Example:**
If you need to grant a user the permission to use the **certificate adding** API only for the specified domain name, follow the steps below:
1. Create a domain name-level policy that allows access to the API and go to the **Create by policy generator** page.
2. Enter relevant items, select **Allow** for **Effect**, **CSS** for **Service**, and **DescribeLiveDomain** for **Action**, and enter the domain name to be authorized in the **Resource** text box. Below is the policy syntax:
 ```
qcs::${ApiModule}:${Region}:uin/:domain/${DomainName}
 ```
 Here:
 - `${ApiModule}` is "live".
 - `${Region}` is "ap-guangzhou".
 - `uin` is the account to be authorized. If this parameter is left empty, it indicates that the current account is authorized.
 - `${DomainName}` is the domain name to be authorized.
 Example: Click **Add Statement** > **Next** > **Create Policy** to generate the `qcs::live:ap-guangzhou::domain/cloud.tencent.com` policy. Once generated, the policy can be associated with users/user groups by using the aforementioned two methods.
![](https://main.qcloudimg.com/raw/ab4a2aa08be8f7ddedf2368ffde9e762.png)

>If you need to grant a sub-user the permission to use the API for all domain names, enter \* in the **Resource** text box.


### Step 3. Use a sub-account

You can use a sub-account identity (sub-account ID and password created by the root account) to call the authorized APIs (such as the "domain name list querying API") to get the corresponding CSS information (such as all domain names under the account).

