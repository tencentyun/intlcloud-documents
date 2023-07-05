<dx-alert infotype="explain" title="">
Security groups can be associated with CVMs, ENIs, TencentDB for MySQL, and CLBs. This topic describes how to associate a security group with a CVM.
</dx-alert>



## Overview
Security groups can be associated with one or more CVMs for network access control. They are an important part of CVM network security measures. You can associate your CVM with one or more security groups if necessary. The following are detailed instructions.

## Prerequisites
You should already have a CVM instance created before starting.

## Directions
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the left sidebar, choose **Security Group** to go to the **Security Group** page.
3. On the **Security Group** page, select a region and locate the security group for which you want to set rules.
4. In the row of the target security group, click **Manage Instances** in the **Operation** column of the target security group. The **Associated Instances** page then appears.
5. On the **Associates Instances** page, click **Add Instance**. 
6. In the pop-up **Add Instance** window, select the instances to bind and click **OK**
<dx-alert infotype="explain" title="">
After multiple security groups are bound to an instance, they are executed based on their priorities, which are consistent with their binding sequence. To adjust the priorities of the security groups, see [Adjusting Security Group Priority](https://intl.cloud.tencent.com/document/product/213/35375).
</dx-alert>



## Subsequent Operations
- You can check all security groups in a specific region. 
For operation details, see [Viewing Security Groups](https://intl.cloud.tencent.com/document/product/213/34828).
- If you want to disassociate a CVM instance from one or more security groups, you can remove it from the security group. 
For operation details, see [Remove from Security Groups](https://intl.cloud.tencent.com/document/product/213/34830).
- If you no longer need a security group, you can delete it. Once a security group is deleted, all rules within it are also deleted. 
For operation details, see [Deleting a Security Group](https://intl.cloud.tencent.com/document/product/213/34831).


