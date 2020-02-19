> Security groups can be bound with CVMs, ENIs, TencentDB for MySQL, and CLBs. In this document, a CVM is bound as an example.

## Operation Scenarios
A security group is used to set network access control for one or more CVMs. It is an important network security isolation method. You can bind one CVM instance with one or more security groups based on your business needs. This document describes how to bind a CVM instance with a security group in the console.

## Prerequisites
A CVM instance has been created.

## Directions
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the left sidebar, select **[Security Groups](https://console.cloud.tencent.com/cvm/securitygroup)** to go to the **Security Group** page.
3. On the **Security Group** page, select a region, and find the security group for which you want to set rules.
4. In the row of the security group for which you want to set rules, click **Manage Instances** in the **Operation** column to go to the **Bind with Instance** page.
5. On the **Bind with Instance** page, click **Add Instances**.
6. In the **Add Instances** window, select the instance to be bound with the security group, and click **OK**.

## Subsequent Operations
- To view all the security groups that you have created in a region, you can query the security group list.
- You can also remove a CVM from one or more security groups.
- You can delete the security groups when they are not necessary. After you delete a security group, all security group rules in this group will also be deleted.

