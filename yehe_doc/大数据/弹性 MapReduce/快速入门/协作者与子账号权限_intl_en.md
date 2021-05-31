Elastic MapReduce (EMR) will need to access or operate other cloud products. To ensure that sub-users or collaborators can use and operate EMR normally, this document describe how to grant sub-users or collaborators related permissions.

## Permission Policy Overview

| Policy | Description | Required | Notes  |
| ----------------------------------- | ------------------------------- | --------- | ------------------------------- |
| QcloudCamSubaccountsAuthorizeRoleFullAccess | Permission required for CAM sub-users to obtain permissions granted by service roles | No | For more information, see [Authorizing EMR to access other services](#jump). |
| QcloudCamRoleFullAccess | Full access to CAM roles  | No | Permission to custom service roles to control access to data across services. For more information, see [Custom Service Roles](https://intl.cloud.tencent.com/document/product/1026/39661). |
| QcloudEMRFullAccess | Full access to EMR | No | Full permission to use all EMR features. For more information, see [Purchasing and managing EMR clusters](#jump2). |
| QcloudEMRReadOnlyAccess   | Read-only access to EMR | No | Permission to view EMR features  |
| QcloudCVMFinanceAccess | Financial access to CVM | No | For more information, see [Purchasing and managing EMR clusters](#jump2). This permission is not required if you don't need to purchase or change the configuration. |
| Custom TencentDB instance purchase policy  | Permission to purchase TencentDB instances | No      | For more information, see [Purchasing and managing EMR clusters](#jump2). This permission is not required if you don't need to add components after the cluster is deployed. |

## Scenarios
[](id:jump)
### Authorizing EMR to access other cloud services
Tencent Cloud root accounts and sub-users and collaborators with the `QcloudCamSubaccountsAuthorizeRoleFullAccess` permission can access other cloud services after being authorized.
- To use EMR to access CVM, CBS, TencentDB, and other services, you need to assign the `EMR_QCSRole` service role and grant the `QcloudAccessForEMRRole` permission (for EMR to read CVM, CBS, TencentDB, COS, and other services) to the first EMR instance you purchase.
- To use EMR to access the data stored in COS, you need to assign the `EMR_QCSRole` service role and grant the `QcloudAccessForEMRRoleInApplicationDataAccess` permission (for EMR big data applications to access other data services, such as COS) to EMR.

The root account can grant the `QcloudCamSubaccountsAuthorizeRoleFullAccess` permission to sub-users or collaborators via the following steps:
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview), click **Users** > **User List**, find the target sub-user or collaborator, and click **Authorize**.
![](https://main.qcloudimg.com/raw/a23eaa5e8c3d5c1561705081b977585b.png)
2. Search for and select the `QcloudCamSubaccountsAuthorizeRoleFullAccess` policy, then click **Confirm**.
![](https://main.qcloudimg.com/raw/97f9ef517eeefdfef7fc84d98c3d0a91.png)
You can associate the `QcloudAccessForEMRRole` and `QcloudAccessForEMRRoleInApplicationDataAccess` policies with the root account, sub-user, or collaborator. The process is the same as step 2.

[](id:jump2)
### Purchasing and managing EMR clusters
To create a cluster, add a component, or scale out a cluster, a sub-user or collaborator must be associated with the `QcloudEMRFullAccess` and `QcloudCVMFinanceAccess` policies and the custom TencentDB purchase policy. In cases not involving resource purchase, such as service configuration management, only the `QcloudEMRFullAccess` policy is required.

>!Only accounts with the financial permission can purchase pay-as-you-go EMR clusters.

| **Policy Type** | **Policy Name**  | **Description** |
| ------------ | ----------------------- | ----------------------- |
| Preset EMR policy  | QcloudEMRFullAccess     | Full access to EMR |
| Preset EMR policy | QcloudEMRReadOnlyAccess | Read-only access to EMR |
| Preset CVM policy  | QcloudCVMFinanceAccess  | Financial access to CVM |
| Custom policy   | Users can custom the name as needed.   | Permission to purchase TencentDB instances |

The root account can grant the above permissions to a sub-user or collaborator via the following steps:
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview), click **Users** > **User List**, find the target sub-user or collaborator, and click **Authorize**.
![](https://main.qcloudimg.com/raw/f71fb2171be39b80e28306b68e718f7c.png) 
2. Search for and select each policy listed in the above table in the **Associate Policy** dialog box, then click **Confirm**. The `QcloudEMRFullAccess` policy is used as an example in the following figure:
![](https://main.qcloudimg.com/raw/45261553e06052a261412a358ae73309.png)
3. Custom a TencentDB purchase policy.
 - **(1). Create a custom policy.**
Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview), click **Policies** > **Create Custom Policy** > **Create by Policy Syntax**, select **Blank Template** on the **Create by Policy Syntax** page, and click **Next**.
![](https://main.qcloudimg.com/raw/517cc56fe1d70289b9c49941adcece01.png)
Enter a policy name (such as EMRvisitedCDB) and a description (such as permission to purchase TencentDB instances for new EMR components), enter the following JSON content under **Policy Content**, and click **Done**.
```
{
			 "version": "2.0",
			 "statement":[
				 {
					 "effect": "allow",
					 "resource": [
						 "*"
					 ],
					 "action": [
						 "cdb:CreateDBInstance",
						 "cdb:CreateDBInstanceHour"
					 ]
				 }
			 ]
 }
```
 - **(2). Associate the sub-user or collaborator with the custom TencentDB policy.**
Find the target sub-user or collaborator on the user list in the CAM console, click **Authorize** in the **Action** column, and search for and associate the custom policy (such as EMRvisitedCDB).



### Custom Service Roles
Tencent Cloud root accounts and collaborators and sub-users with the `QcloudCamRoleFullAccess` permission can precisely control COS bucket permissions and other cloud resource permissions. For more information see [Custom Service Roles](https://intl.cloud.tencent.com/document/ product/1026/39661).
 A root account can grant the `QcloudCamRoleFullAccess` permission to a sub-user or collaborator via the following steps:
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview), click **Users** > **User List**, find the target sub-user or collaborator, and click **Authorize**.
![](https://main.qcloudimg.com/raw/f8b985ec2cab79090e6a96675f2f7773.png) 
2. Search for and select the `QcloudCamRoleFullAccess` policy, then click **Confirm**.
![](https://main.qcloudimg.com/raw/4b07b852fa000ac7569c0136fe1a3a90.png)
