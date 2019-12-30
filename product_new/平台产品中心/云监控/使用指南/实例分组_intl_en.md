## Overview

You can group cross-region and cross-project instances of a cloud product for unified management. When creating a large number of instances, you can create instance groups as needed. By managing instance groups, you can better manage instances, configure alarm policies, and improve OPS efficiency.

## Notes

- Each instance group can contain up to 2,000 instances, and a maximum of 200 instances can be added to an instance group at a time.
- By grouping instances, you can manage cross-region and cross-project cloud product instances in a unified manner and configure alarm policies to avoid repeated operations and improve OPS efficiency.


## Steps
### Creating instance groups

1. Log in to [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/).
2. In the left sidebar, click **Instance Group** to access the instance group page.
3. Click **Create** and set the following parameters:
 - **Group Name**: Enter an instance group name.
 - **Group Type**: Select an option based on your actual needs.
 - **Add to group**: Select an instance to be added to the group.
![](https://main.qcloudimg.com/raw/d44d0e35a54e689a6275a3b1e75bf37c.png)
4. Click **Save**.


### Editing instance groups


>!
>- If an instance group has been bound to an alarm policy, the instances added to the instance group are automatically bound to the alarm policy.
>- If an instance group has been bound to an alarm policy, the instances removed from this instance group are unbound from the alarm policy.

1. Log in to [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/).
2. In the left sidebar, click **Instance Group** to access the instance group page.
3. Select the name of the instance group to be edited to access the instance group details page. You can create or delete instances in the instance group on this page.

#### Adding Instances
1. Click **Add**.
![](https://main.qcloudimg.com/raw/a54bb9c85bb3a5d45aab48a5748007ef.png)
2. In the pop-up dialog box, select the instances to be added to the instance group.
3. Click **OK**.

#### Removing Instances
1. Select the instances to be removed from the instance group and click **Remove**.
![](https://main.qcloudimg.com/raw/291f79275f7dce9086af155ae87f1c14.png)
2. In the pop-up dialog box, click **Remove selected instance**.


### Deleting instance groups

1. Log in to [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/).
2. In the left sidebar, click **Instance Group** to access the instance group page.
3. Find the instance group to be deleted and click **Delete** in the column on the right.
![](https://main.qcloudimg.com/raw/be23ff6be2ad18f1157c8ffd3f868b62.png)
4. In the pop-up dialog box, click **Delete**.
>?When an instance group bound to an alarm policy is deleted, the alarm policy becomes invalid.


### Replicating instance groups

1. Log in to [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/).
2. In the left sidebar, click **Instance Group** to access the instance group page.
3. Find the instance group to be replicated and click **Replication** in the column on the right.
![](https://main.qcloudimg.com/raw/fa2ac5a4d01ca88f67129f60f42900b2.png)
4. In the pop-up dialog box, click **Copy**.
>?When an instance group is copied, only instances in the group are copied. If the copied instance group is bound to an alarm policy, the binding relationship is not copied.


### Binding instance groups to alarm policies

1. Log in to [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/).
2. In the left sidebar, choose **Alarm Configuration** > **Alarm Policy** to access the alarm policy management page.
3. Click **Add** to access the configuration page for creating policies.
4. Find the **Alarm Object** configuration item, enable **Select instance group**, and select the previously created instance group from the drop-down list, as shown below.
![](https://main.qcloudimg.com/raw/b1d55bbecb7c58137d0f385b3c763cb8.png)
5. Complete the configuration of other items on the page. For more information, see [Creating alarm policies](https://cloud.tencent.com/document/product/248/6215).

