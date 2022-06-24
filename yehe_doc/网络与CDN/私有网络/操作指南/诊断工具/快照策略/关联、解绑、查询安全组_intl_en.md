After creating a snapshot policy, you can associate it with security groups. Security groups added to the snapshot list will be backed up according to the policy and can be disassociated when snapshot backup is no longer needed. This document describes how to associate and disassociate security groups with/from a snapshot policy and how to view the associated security groups.

## Prerequisites
- You have created a snapshot policy.
- You have prepared security groups to be associated.

## Associating Security Group[](id:glaqz)
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/) and select **Diagnostic Tools** > **Snapshot Policy** on the left sidebar.
2. On the **Snapshot Policy** page, click the snapshot policy ID to enter the details page.
![]()
3. Click **Associate Security Group**.
![]()
4. On the **Associate Security Group** page, select the **Region** and click the arrow icon on the right of the security groups to be associated in the **Select** list. The selected security groups are displayed in the **Selected** list on the right. Click **OK**.
>?
> - A snapshot policy is not specific to a region and can be associated with security group instances in all regions. However, only security groups in the same region can be associated with at a time. To associate a snapshot policy with security groups in different regions, perform multiple association operations.
> - A security group can be associated with only one snapshot policy.
> 
![]()



## Disassociating Security Group  
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/) and select **Diagnostic Tools** > **Snapshot Policy** on the left sidebar.
2. On the **Snapshot Policy** page, click the snapshot policy ID to enter the details page.
3. Click **Disassociate** on the right of the security group to be disassociated.
![]()
4. In the **Disassociate Security Group** pop-up window, confirm the information and click **OK**. The security group rules will no longer be backed up, but the existing backup records will not be deleted.
![]()
5. (Optional) To disassociate multiple security groups at a time, select them, click **Batch Disassociate** at the top, and click **OK** in the pop-up window.
>?Only security groups in the same region can be disassociated at a time.
>
 ![]()   


## Querying Security Group
To query the security groups associated with a snapshot policy, follow the instructions below.
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/) and select **Diagnostic Tools** > **Snapshot Policy** on the left sidebar.
2. On the **Snapshot Policy** page, click the snapshot policy ID to enter the details page.
3. In the **Associated Security Groups** section, you can view all the security groups associated with the snapshot policy.
4. Click the filter icon next to the region to filter security groups by region. Click the settings icon in the top-right corner to customize the list fields.
![]()
5. Click the **Security Group ID** to enter the security group details page.
