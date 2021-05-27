## Overview

If your company has management personnel with different identities, you can use CAM to divide permissions and grant different permissions to different people to facilitate management and control. This document uses a typical case to describe how to manage the permissions of different identities through sub-accounts.

Suppose that:
- The company account `CompanyExample` has two OPS engineers `DevA` and `DevB`. 
- The OPS engineer `DevA` is responsible for server OPS and has all operation permissions of CVM instances under the company account `CompanyExample`.
- The OPS engineer `DevB` is responsible for TencentDB for MySQL OPS and has all operation permissions of TencentDB for MySQL instances under the company account `CompanyExample`.


## Directions

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam) with the company account `CompanyExample`.
2. Create two sub-accounts with usernames of `DevA` and `DevB` through [custom sub-User creation](https://intl.cloud.tencent.com/document/product/598/13674).
3. On the **[User List](https://console.cloud.tencent.com/cam)** page, find the just created sub-user `DevA` and click **Authorize** in the **Operation** column on the right as shown below:
![](https://main.qcloudimg.com/raw/68e813264316ad2ef97249077068634c.png)
4. In the **Associate Policy** window that pops up, search for and select `QcloudCVMFullAccess` and click **OK** as shown below:
![](https://main.qcloudimg.com/raw/445d5cf9dccc8c4c822faf71610f435b.png)
5. Associate the `QcloudCDBFullAccess` policy with the sub-account `DevB` as instructed in steps 2 and 3.
6. After the authorization is successful, the sub-account `DevA` has all the operation permissions of CVM instances, while the sub-account `DevB` has all the operation permissions of TencentDB for MySQL instances.
>?If you need to configure a CAM user as another role, you can follow the above process and search for and select the corresponding permissions policy name in steps 2 and 3. For specific permissions, please see [System Permissions](#System Permissions)

[](id:System Permissions)

## System Permissions

<table>
<tr><th width="20%">Owner</th><th width="40%">Policy Name</th><th width="40%">Description</th></tr><tr>
<td>Admin</td>
<td>AdministratorAccess</td><td>This policy allows you to manage all users and their permissions, related financial info, and cloud service assets under this account.</td>
</tr><tr>
<td>Financial admin</td>
<td>QCloudFinanceFullAccess</td><td>This policy allows you to manage related financial information under the account, such as payment and invoicing.</td>
</tr><tr>
<td rowspan="5">Database admin</td>
<td>QCloudFinanceFullAccess</td><td>This policy allows you to manage related financial information under the account, such as payment and invoicing.</td>
</tr>
<tr>
		<td>QcloudCynosDBFullAccess</td>
		<td>Full access to TDSQL-C</td>
	</tr>
  <tr>
		<td>QcloudMariaDBFullAccess</td>
		<td>Full access to TencentDB for MariaDB
</td>
	</tr>
    <tr>
		<td>QcloudSQLServerFullAccess
</td>
		<td>Full access to TencentDB for SQL Server
</td>
	</tr>
      <tr>
		<td>QcloudCDWPGFullAccess
</td>
		<td>Full access to TencentDB for PostgreSQL
</td>
	</tr>
  <td rowspan="3">Network admin</td>
<td>QcloudCLBFullAccess</td><td>Full access to CLB
</td>
</tr>
<tr>
		<td>QcloudVPCFullAccess</td>
		<td>Full access to VPC</td>
	</tr>
  <tr>
		<td>QcloudDCFullAccess</td>
		<td>Full access to Direct Connect
</td>
	</tr>
<td rowspan="3">Monitoring admin</td>
<td>QcloudMonitorFullAccess</td><td>Full access to Cloud Monitor, including the permission to view user groups
</td>
</tr>
<tr>
		<td>QcloudCATFullAccess</td>
		<td>Full access to CAT</td>
	</tr>
  <tr>
		<td>QcloudTAPMFullAccess</td>
		<td>Full access to TAPM
</td>
	</tr>
</table>



