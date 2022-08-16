Data Lake Compute has a complete data access control mechanism and divides permissions into operation permissions and data permissions. The former is managed by CAM, while the latter is managed by the permission module of Data Lake Compute.
- A root account has all the operation and data permissions of Data Lake Compute by default.
- If a sub-user is granted the operation permissions of Data Lake Compute, the sub-user can grant the data permissions to other sub-users and can be regarded as an "admin" of this type of sub-users.
- If a sub-user is granted the data read/write permissions, the sub-user can query data as permitted. The data permissions are granted by an "admin".
- The data permissions of all sub-users other than root accounts are granted by an "admin". They cannot query data which they don't have permissions on.

A root account has all the operation permissions of Data Lake Compute by default and can grant sub-users the access permissions of Data Lake Compute through CAM, so that the sub-users can have corresponding operation permissions of Data Lake Compute.
## Directions
1. Create and authorize a sub-user.
 In the CAM console, create a sub-user and grant permissions as instructed in [Sub-user authorization](#jump).
 - Preset policy `QcloudDLCFullAccess`: All the operation permissions in Data Lake Compute.
 - Custom policy: Specified operation permissions of Data Lake Compute.
2. Log in to the Data Lake Compute console with a sub-user account and verify the permissions.
If the operation succeeds, the authorization has taken effect.


## Operation permission category
Data Lake Compute operation permissions are categorized by API as follows. 

| Permission Type   | Description                                |
| ---------- | ----------------------------------- |
| Metadata management | Manipulate the metadata information of databases and data tables managed in Data Lake Compute. |
| Task management  | Submit and view tasks in Data Lake Compute.                   |
| Permission management   | Manage users' data access permissions.              |
| System configuration   | Perform basic configurations of the Data Lake Compute service.                     |

[](id:jump)
## Sub-user authorization
If you access Data Lake Compute as a root account, skip this step.
1. Create a sub-account as instructed in [Creating and Authorizing Sub-account](https://intl.cloud.tencent.com/document/product/598/40985).
2. Create a custom policy.
 - On the [Policies](https://console.cloud.tencent.com/cam/policy) page in the CAM console, click **Create Custom Policy**.
 - In the pop-up window, click **Create by Policy Syntax**.
 - On the **Create by Policy Syntax** page, select **Blank Template** and click **Next**.
 - In the template, enter the **Policy Name** (e.g., `DLCDataAccess`) and **Description**, copy the following policy, paste it into **Policy Content**, and click **Complete**. A sub-user bound to the custom policy can log in to the Data Lake Compute console to run SQL tasks but cannot manage data permissions. For more information, see [Sub-Account Permission Management]().
```json
{
	 "version": "2.0",
	 "statement": [
		 {
			 "effect": "allow",
			 "action": [
				 "dlc:DescribeStoreLocation",
				 "dlc:DescribeTable",
				 "dlc:DescribeViews",
				 "dlc:CancelTask",
				 "dlc:CreateDatabase",
				 "dlc:CreateScript",
				 "dlc:CreateTable",
				 "dlc:CreateTask",
				 "dlc:DeleteScript",
				 "dlc:DescribeDatabases",
				 "dlc:DescribeScripts",
				 "dlc:DescribeTables",
				 "dlc:DescribeTasks",
				 "dlc:DescribeQueue"
			 ],
			 "resource": [
				 "*"
			 ]
		 }
	 ]
}
```
![]()
5. Bind the preset or custom policy to a sub-account, and the sub-account can log in to and access Data Lake Compute. For more information, see [Setting Sub-user Permissions](https://intl.cloud.tencent.com/document/product/598/32650).
 - Preset policy: `QcloudDLCFullAccess`.
 - Custom policy: The policy customized in the above steps for accessing Data Lake Compute.
