>>! This document describes the Cloud Access Management (CAM) feature for IM. For more information on CAM for other Tencent Cloud services, see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).
>
>Essentially, IM CAM binds sub-accounts to policies or grants policies to sub-accounts. You can use preset policies in the console for simple authorization operations. For more information on complicated authorization operations, see [Custom Policies](https://intl.cloud.tencent.com/document/product/1047/38088).
>The table describes the preset policies provided by IM.
>
><table class="table"><thead><tr><th>Policy</th><th>Description</th></tr></thead>
><tbody><tr><td>QcloudAVCFullAccess</td><td>IM read and write permissions</td></tr>
><tr><td>QcloudIMReadOnlyAccess</td><td>IM read-only permission</td></tr></tbody></table>
>
>## Preset Policy Usage Example
>
>### Creating a sub-account with IM permissions
>
>
>1. Log in to the [**User List**](https://console.cloud.tencent.com/cam) page in the CAM console with the [root account](https://intl.cloud.tencent.com/document/product/598/32633). Then, click **Create User**.
>2. On the **Create User** page, click **Custom Create** to go to the **Create Sub-user** page.
>>? For information on the operations that you must perform before configuring user permissions, see [Creating Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).
>3. On the **User Permissions** page:
>    (1) Search for and select the `Instant Messaging` preset policy.
>    (2) Click **Next**.
>4. Click **Complete** in the **Review** column. After the sub-user is created, record the login link, download the security credentials, and store them properly. The table describes the relevant information.
>
><table class="table"><tbody><tr><td>Information</td><td>Source</td><td>Function</td><td>Required</td></tr>
>o<tr><td>Login link</td><td>Copied on the page</td><td>Facilitate console login and skip the root account entry step</td><td>No</td></tr>
><tr><td>Username</td><td>Security credential CSV file</td><td>Entered when you log in to the console</td><td>Yes</td></tr>
><tr><td>Password</td><td>Security credential CSV file</td><td>Entered when you log in to the console</td><td>Yes</td></tr>
><tr><td>SecretId</td><td>Security credential CSV file</td><td>Used when a server API is called. For more information, see <a href="https://intl.cloud.tencent.com/document/product/598/32675" target="_blank">Access Key</a></td><td>Yes</td></tr>
><tr><td>SecretKey</td><td>Security credential CSV file</td><td>Used when a server API is called. For more information, see <a href="https://intl.cloud.tencent.com/document/product/598/32675" target="_blank">Access Key</a></td><td>Yes</td></tr></tbody></table>
>5. Provide the authorized party with the preceding login link and security credentials. The authorized party can then use the sub-account to perform IM operations, including accessing the IM console and calling IM server APIs.
>
>### Granting IM permissions to an existing sub-account
>
>
>1. Log in to the [**User List**](https://console.cloud.tencent.com/cam) page in the CAM console with the [root account](https://intl.cloud.tencent.com/document/product/598/32633). Then, click the sub-account to authorize.
>2. On the **User Details** page, click **Add Policy**. If the sub-account already has permissions, click **Associate Policy**.
>3. Select **Select policies from the policy list**, search for and select the `Instant Messaging` preset policy and complete the authorization process as instructed.
>
>
>### Deleting IM permissions from a sub-account
>
>
>1. Log in to the [**User List**](https://console.cloud.tencent.com/cam) page in the CAM console with the [root account](https://intl.cloud.tencent.com/document/product/598/32633). Then, click the sub-account from which you want to delete permissions.
>2. On the **User Details** page, find the `Instant Messaging` preset policy, and click **Unassociate** for the policy. Then, complete the deauthorization process as instructed.
