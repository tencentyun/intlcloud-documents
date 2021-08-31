## Operation Scenario
As an important network security isolation method, a security group is used to configure network access control for one or more CVMs. You can associate CVM instances with one or more security groups based on your business needs. This document describes how to associate a CVM instance with a security group in the console.

## Prerequisites
A CVM instance has been created.

## Steps
1. Log in to [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the left sidebar, click **[Security Group](https://console.cloud.tencent.com/cvm/securitygroup)** to enter the security group management page.
3. On the security group management page, choose **Region**, and locate the row of the security group for which you want to set rules.
4. In the operation column, click **Manage instance** to enter the **Associate with Instance** page.
5. On the **Associate with Instance** page, click **Add Association**.
6. In the "Add Instance Association" window that appears, select the instance to be bound with the security group and click **OK**.

## Subsequent Operations
- To view all the security groups that you have created in a region, query the security group list.
For details about the operation, see [Viewing a Security Group](https://intl.cloud.tencent.com/document/product/215/35507).
- If you do not want a CVM instance to belong to one or multiple security groups, remove it from them.
For details about the operation, see [Removing from a Security Group](https://intl.cloud.tencent.com/document/product/215/35508).
- If your business no longer needs one or multiple security groups, you can delete them. After you delete a security group, all security group rules in it will also be deleted.
For details about the operation, see [Deleting a Security Group](https://intl.cloud.tencent.com/document/product/215/35510).

