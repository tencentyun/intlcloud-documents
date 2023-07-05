
<dx-alert infotype="explain" title="">
A security group can be associated with resources such as ECM instance, ELB instance, and ENI. This document uses an ECM instance as an example to describe how to associate a security group.
</dx-alert>


## Overview
As an important means for network security isolation, a security group can be used to set network access controls for one or more ECM instances. You can associate your ECM instance with one or more security groups as needed. This document describes how to associate an ECM instance with a security group in the ECM console.

## Prerequisites
You have created an ECM instance.

## Directions
1. Log in to the ECM console and select **Edge Network** > **[Security Group](https://console.cloud.tencent.com/ecm/safe)** on the left sidebar.
3. On the **Security Group** management page, select **More** > **Manage Instance** on the right of the instance to be associated.
4. On the **Associate Instance** page, click **Associate**.
5. In the **Associate Instance** pop-up window, perform the operations as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/46e13de2751e1ce4da86b58610515edb.png)
 1. Filter out the node region, and the page will display all ECM instances in this region. The instance data in all regions is displayed by default.
 2. Filter out the module, and the page will display all ECM instances under this module. The instance data under all modules is displayed by default.
 3. Select the instance ID/name of the ECM instance to be associated.
6. Click **OK**.

## Subsequent Operations
- If you want to view all created security groups, query the security group list and filter groups by resource attribute.
For detailed directions, see [Viewing Security Group](https://intl.cloud.tencent.com/document/product/1119/43435).
- To disassociate an ECM instance from one or more security groups, remove it from the security groups.
  For detailed directions, see [Removing Instance from Security Group](https://intl.cloud.tencent.com/document/product/1119/43436).
- If you no longer need a security group, you can delete it. Once a security group is deleted, all rules within it are also deleted.
  For detailed directions, see [Deleting Security Group](https://intl.cloud.tencent.com/document/product/1119/43437).

