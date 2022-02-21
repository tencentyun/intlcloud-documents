>!This document describes the access management feature of **SMS**. For more information on access management for other Tencent Cloud services, please see [CAM-Enabled Products](https://intl.cloud.tencent.com/document/product/598/10588).

SMS access management essentially binds sub-accounts to policies or grants policies to sub-accounts. You can use default policies directly in the console to implement some simple authorization operations. For more complicated authorization operations, please see [Custom Policies](https://intl.cloud.tencent.com/document/product/382/38456).

Currently, SMS provides the following default policies:

| Policy Name | Description |
|--------------------------|--------------|
| QcloudSMSFullAccess     | Full access permission |
| QcloudSMSReadonlyAccess | Read-Only access permission |

## Default Policy Use Cases
### Creating sub-accounts with full access permission
1. Access the [User List](https://console.cloud.tencent.com/cam) page in the CAM Console using the Tencent Cloud [root account](https://intl.cloud.tencent.com/document/product/598/32633) and click **Create User**.
2. On the "Create User" page, select **Custom Create** to enter the "Create Sub-user" page.
>?Please perform the steps before "User Permissions" as instructed in [Creating a Custom Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).
3. On the "User Permissions" page:
	1. Search for and select the default policy `QcloudSMSFullAccess`.
	2. Click **Next**.
4. Click **Complete** in the "Review" column. After the sub-user is created successfully, download the login link and security credentials as shown below and keep them private.
<table>
<thead>
<tr>
<th>Information</th>
<th>Source</th>
<th>Description</th>
<th>Storage Required</th>
</tr>
</thead>
<tbody><tr>
<td>Login link</td>
<td>Copy it on the page</td>
<td>Makes it easier to log in to the console without having to enter the root account</td>
<td>No</td>
</tr>
<tr>
<td>Username</td>
<td>Security credential file in CSV format</td>
<td>Needed for console login</td>
<td>Yes</td>
</tr>
<tr>
<td>Password</td>
<td>Security credential file in CSV format</td>
<td>Needed for console login</td>
<td>Yes</td>
</tr>
<tr>
<td>SecretId</td>
<td>Security credential file in CSV format</td>
<td>Needed for calling server APIs. For more information, please see "Access Key"</td>
<td>Yes</td>
</tr>
<tr>
<td>SecretKey</td>
<td>Security credential file in CSV format</td>
<td>Needed for calling server APIs. For more information, please see "Access Key"</td>
<td>Yes</td>
</tr>
</tbody></table>
5. With the above login link and security credentials, you can use this sub-user to perform all operations in SMS (such as accessing the SMS console and calling SMS server APIs).

## Granting Existing Sub-account Full Access to SMS
1. Access the **[User List](https://console.cloud.tencent.com/cam)** in the CAM console using a Tencent Cloud [root account](https://intl.cloud.tencent.com/document/product/598/32633) and click the target sub-account.
2. Click **Add Policy** under the "Permissions" tab on the "User Details" page. If the permission of a sub-account is not empty, click **Associate Policy**.
3. Click **Select policies from the policy list**, search for and check the preset policy `QcloudSMSFullAccess`, and complete the authorization as prompted.

## Removing a Sub-account’s Full Access to SMS
1. Access the **[User List](https://console.cloud.tencent.com/cam)** in the CAM console using a Tencent Cloud [root account](https://intl.cloud.tencent.com/document/product/598/32633) and click the target sub-account.
2. Find the preset policy `QcloudSMSFullAccess` under the "Permissions" tab on the "User Details" page, click **Unassociate** on the right, and complete deauthorization as prompted.

