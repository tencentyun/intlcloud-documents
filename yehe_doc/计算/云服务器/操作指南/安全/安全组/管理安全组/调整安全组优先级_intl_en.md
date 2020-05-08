## Scenario
You can bind one or more security groups to a Cloud Virtual Machine (CVM) instance. If a CVM instance is bound with multiple security groups, these security groups are matched and executed sequentially by priority, for example, priorities 1 and 2. You can adjust the priority of a security group as follows.

## Prerequisites
The CVM instance is bound to two or more security groups.

## Directions
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the instance management page, click the ID of the CVM instance to go to the details page.
3. Click the **Security Groups** tab to go to the security group management page.
4. In the **Bound Security Groups** section on the right, click **Order**. Click the <img src="https://main.qcloudimg.com/raw/15a91d68b0396cb89bfd75a578b42130.png" style="margin:-3px 0px;width:20px"> icon for the security group, and drag up and down to adjust the priority of the security group. A higher position indicates a higher priority.
5. After finishing the adjustment, click **Save**.

