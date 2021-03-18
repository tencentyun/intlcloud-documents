CSS supports permission control via CAM, where you can manage the CSS domains, configurations, and data of your account. You can create, manage, or terminate users or user groups and grant API access permissions to different users or user groups for the purpose of identity management and policy control.

When using CAM, you can associate a policy with a user or user group to allow or forbid them to use specified resources to complete specified tasks.

## Basic Concepts

- Root account: a registered Tencent Cloud account.
- Sub-user: created and fully owned by a root account.
- Collaborator: after an account is added as a collaborator of a root account, it becomes one of the sub-accounts of the root account and has the identity of the root account.
- User group: created for users with the same functions and can be associated with a policy for centralized authorization management.

For more information on the definitions and permissions, see CAM [User Types](https://intl.cloud.tencent.com/document/product/598/32633).

## Directions
### Step 1. Create a sub-user or user group

One or more sub-users with specific roles and policies can be created under one root account. A sub-user has a specific ID and identity credential that can be used to log in to the Tencent Cloud console for configuration. It also has API access permissions. You can log in to the [CAM console](https://console.cloud.tencent.com/cam/) to create a sub-user, as shown below:

![](https://main.qcloudimg.com/raw/c1c92bdd08c8cf19ac17ba80cd4a11be.png)
For more information, see [Creating a Custom Sub-user](https://intl.cloud.tencent.com/document/product/598/13674) and [Creating User Groups](https://intl.cloud.tencent.com/document/product/598/33380).

### Step 2. Add a policy to the sub-user or user group

You can add policies and authorize users or user groups on the user or user group management and policy management pages. For more information, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

- Method 1: go to the **User List** or **User Groups** page, click **Authorize**/**Associate Policy** on the right of the created sub-user or user group, select the corresponding CSS policy, and click **Confirm**.
![](https://main.qcloudimg.com/raw/9da12095cfa57813a373ab9ffeabc9a4.png)

![](https://main.qcloudimg.com/raw/ec1e09ab6cde2a703ac90d7ccdad6424.png)

![](https://main.qcloudimg.com/raw/f09b5d456ba1fd554ad321ddcc67cbdc.png)

- Method 2: go to the **Policies** page, click **Associate Users/Groups** on the right of the policy to be associated, select the created sub-user or user group, and click **Confirm**.
![](https://main.qcloudimg.com/raw/5b5e0dc032934846e39e7aee740ae34b.png)

**Policies that can be associated include:**
1. Preset policy: click **Policies** on the left sidebar to go to the **Policies** page, where you can view all existing policies.
	- CSS preset policies include [QcloudLIVEFullAccess](https://console.cloud.tencent.com/cam/policy/detail/9545933&QcloudLIVEFullAccess&2) (read/write policy) and [QcloudLIVEReadOnlyAccess](https://console.cloud.tencent.com/cam/policy/detail/13346800&QcloudLIVEReadOnlyAccess&2) (read-only policy).
	- To use tags, authorization of [QcloudTAGFullAccess](https://console.cloud.tencent.com/cam/policy/detail/1592575&QcloudTAGFullAccess&2) (full read/write access to Tag) is required.
	- To use real-time logs, authorization of [QcloudCamFullAccess](https://console.cloud.tencent.com/cam/policy/detail/596169&QcloudCamFullAccess&2) (full read/write access to CAM) is required.
2. Custom policy: go to the **Policies** page, click **Create Custom Policy**, and select **Create by Policy Generator**. For more information, see [Custom Policy](https://intl.cloud.tencent.com/document/product/598/10601).

**Example:**
If you need to grant a user the permission to use the `CreateLiveCert` API only for the specified domain, follow the steps below:
1. Create a domain-level policy that allows access to the API and go to the **Create by Policy Generator** page.
2. Enter relevant items, select **Allow** for **Effect**, **Live Streaming Services (live)** for **Service**, and **DescribeLiveDomains** for **Action**, and enter the domain to be authorized in the **Resource** text box. Below is the policy syntax:
```
qcs::${ApiModule}:${Region}:uin/:domain/${DomainName}
```
 Where:
 - `${ApiModule}` is `live`.
 - `${Region}` is `ap-guangzhou`.
 - `uin` is the account to be authorized. If this parameter is left empty, it indicates that the current account is authorized.
 - `${DomainName}` is the domain name to be authorized.
 Example: click **Add Statement** > **Next** > **Create Policy** to generate the `qcs::live:ap-guangzhou::domain/cloud.tencent.com` policy. Once generated, the policy can be associated with users or user groups by using the aforementioned two methods.
![](https://main.qcloudimg.com/raw/2e28228e7226ad3617880b0985ee5709.png)

>?If you need to grant a sub-user the permission to use the API for all domains, enter \* in the **Resource** text box.


### Step 3. Use a sub-account
You can use a sub-account identity (sub-account ID and password created by the root account) to call the authorized APIs (such as the `DescribeLiveDomains` API) to get the corresponding CSS information (such as all domains under the account).
