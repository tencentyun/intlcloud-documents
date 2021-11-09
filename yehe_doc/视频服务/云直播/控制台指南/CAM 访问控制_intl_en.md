CSS supports permission control via CAM, where you can manage the CSS domain names, configurations, and data of your account. You can create, manage, or terminate users or user groups and grant API access permissions to them for the purpose of identity management and policy control.

You can use CAM to bind a user or user group to a policy which allows or denies them access to specified resources to complete specified tasks.

## Concepts

- Root account: a registered Tencent Cloud account.
- Sub-user: created and fully owned by a root account.
- Collaborator: after an account is added as a collaborator of a root account, it becomes one of the sub-accounts of the root account and has the identity of the root account.
- User group: created for users with the same functions and can be bound with a policy for centralized authorization management.

For more information on the definitions and permissions, see CAM [User Types](https://intl.cloud.tencent.com/document/product/598/32633).

## Directions
### Step 1. Create a sub-user or user group

One or more sub-users with specific roles and policies can be created under one root account. A sub-user has a unique ID and identity credential that can be used to log in to the Tencent Cloud console for configuration. It also has API access permissions. You can log in to the [CAM console](https://console.cloud.tencent.com/cam/) to create a sub-user, as shown below:
![](https://main.qcloudimg.com/raw/c1c92bdd08c8cf19ac17ba80cd4a11be.png)
For more information, see [Creating Sub-user](https://intl.cloud.tencent.com/document/product/598/13674) and [Creating User Group](https://intl.cloud.tencent.com/document/product/598/33380).

### Step 2. Add a policy to the sub-user or user group

You can add policies and authorize users or user groups on the user or user group management and policy management pages. For more information, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

<dx-tabs>
::: Method 1. Add a policy to the sub-user or user group
Enter the user/user group page and select the user/user group to which to add a policy.
- Click **Users** > **User List** on the left sidebar, select the user/user group to which to add a policy, click **Authorize** on the right, select the corresponding CSS policy, and click **Confirm**. ![](https://main.qcloudimg.com/raw/9da12095cfa57813a373ab9ffeabc9a4.png)

  ![](https://main.qcloudimg.com/raw/ec1e09ab6cde2a703ac90d7ccdad6424.png)

  ![](https://main.qcloudimg.com/raw/f09b5d456ba1fd554ad321ddcc67cbdc.png)

- Click **Users** > **User List** or **User Groups** on the left sidebar, click the name of the user/user group to which to add a policy to enter the details page, click **Associate Policy**, select the corresponding CSS policy, and click **OK**.
![](https://main.qcloudimg.com/raw/f09b5d456ba1fd554ad321ddcc67cbdc.png)
:::
::: Method 2. Associate policy with user/user group
Click **Policies** on the left sidebar, select the policy to be added, click **Associate Users/Groups** in the **Operation** column, select the user/user group to be authorized, and click **Confirm**.
![](https://main.qcloudimg.com/raw/5b5e0dc032934846e39e7aee740ae34b.png)

:::
</dx-tabs>

#### Addable policies
- **Preset policy**: click **Policies** on the left sidebar to go to the **Policies** page, where you can view all existing policies.
   - CSS preset policies include [QcloudLIVEFullAccess](https://console.cloud.tencent.com/cam/policy/detail/9545933&QcloudLIVEFullAccess&2) (read and write policy) and [QcloudLIVEReadOnlyAccess](https://console.cloud.tencent.com/cam/policy/detail/13346800&QcloudLIVEReadOnlyAccess&2) (read-only policy).
   - To use tags, authorization of [QcloudTAGFullAccess](https://console.cloud.tencent.com/cam/policy/detail/1592575&QcloudTAGFullAccess&2) (full read and write access by tag) is required.
   - To use real-time logs, authorization of [QcloudCamFullAccess](https://console.cloud.tencent.com/cam/policy/detail/596169&QcloudCamFullAccess&2) (full read/write access to CAM) is required.
- **Custom policy**: go to the **Policies** page, click **Create Custom Policy**, and select **Create by Policy Generator**. For more information, see [Custom Policy](https://intl.cloud.tencent.com/document/product/598/10601).
>? Currently, some APIs of CSS support resource-level authorization.

	**Operation example:** if you need to authorize the **DescribeLiveDomains** API to a sub-user for a specified domain name, follow the steps below to configure:
	1. Create a domain-level policy that allows access to the API, go to the **Create by Policy Generator** page, and set the configuration items:
<table>
<tr><th>Configuration Item</th><th>Required</th><th>Description</th></tr>
<tr>
<td>Effect</td><td>Yes</td><td>Select <b>Allow</b></td>
</tr><tr>
<td>Service</td><td>Yes</td><td>Select <b>Cloud Streaming Services</b></td>
</tr><tr>
<td>Action</td><td>Yes</td><td>Select <b>DescribeLiveDomains</b></td>
</tr><tr>
<td>Resource</td><td>Yes</td>
<td>Select all resources or specific resources that you want to authorize.<ul style="margin:0"><li>Tencent Cloud services where the authorization granularity is operation level or service level <b>don't support six-segment resource descriptions; for them, simply select all resources</b>. </li><li>For Tencent Cloud services where the authorization granularity is resource level, you can select specific resources. For the resource description method, see the corresponding CAM guide in <a href="https://intl.cloud.tencent.com/document/product/598/10588">CAM-Enabled Products</a>. For the specific authorization granularity of Tencent Cloud services, see Authorization Granularity in <a href="https://intl.cloud.tencent.com/document/product/598/10588">CAM-Enabled Products</a>.</li></ul></td>
</tr><tr>
<td>Condition</td><td>No</td>
<td>Set the effective condition of the above authorization and enter the source IP to be authorized, so as to allow access to specified operations only when requests come from the specified IP range. You can also add other conditions to further restrict the policy. For more information, see <a href="https://intl.cloud.tencent.com/document/product/598/10608">Condition</a>.</td>
</tr></table>
<img src="https://qcloudimg.tencent-cloud.cn/raw/da4b1d1379c74e8d5eeb3f79908191e6.png">

> ! If you want to authorize multiple services, you can click **Add Permissions** to configure authorization policies for these services.

2. Click **Next** to generate the policy. Then, associate it with users/user groups using either of the two methods above.
![](https://qcloudimg.tencent-cloud.cn/raw/c88a7d7181c31262d9ed46ce938361db.png)


### Step 3. Use a sub-account
You can use a sub-account identity (sub-account ID and password created by the root account) to call the authorized APIs (such as `DescribeLiveDomains`) to get the CSS information (such as all domains under the account).

