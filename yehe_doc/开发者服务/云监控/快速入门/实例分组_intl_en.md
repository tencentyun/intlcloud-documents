## Feature Overview

You can group cross-region and cross-project instances of a Tencent Cloud product for unified management. When creating a large number of instances, you can create instance groups as needed to better manage instances, configure alarm policies, and improve OPS efficiency.

## Use Cases
- Alarm policies can be configured for cross-instance and cross-region projects of the same product in a unified manner.
- You can manage various resources under your Tencent Cloud account by service category.

## Notes

- Each instance group can contain up to 2,000 instances, and a maximum of 200 instances can be added to an instance group at a time.
- By grouping instances, you can manage cross-region and cross-project Tencent Cloud products in a unified manner and configure alarm policies, avoiding repeated operations and improving OPS efficiency.

  

## Directions
### Creating instance group

1. Log in to the [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/).
2. On the left sidebar, click **Instance Group** to enter the instance group page.
3. Click **Create** and configure the following fields:
	- Group Name: enter the instance group name.
	- Group Type: select an option based on your actual needs.
	- Add to Group: check instances to be added to the group.
![](https://main.qcloudimg.com/raw/13dfee6c477e03c6272af47beebc36c9.png)
4. Click **Save**.


### Editing instance group

>
>- If an instance group has been bound to an alarm policy, new instances added to it will be automatically bound to the alarm policy.
>- If an instance group has been bound to an alarm policy, instances removed from it will be unbound from the alarm policy.

1. Log in to the [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/).
2. On the left sidebar, click **Instance Group** to enter the instance group page.
3. Select the name of the instance group to be edited to enter the instance management page. You can create or delete instances in the instance group on this page.

#### Adding instance
1. Click **Add**.
2. In the pop-up box, select the instance to be added to the instance group.
3. Click **OK** to add the instance to the instance group.

#### Removing instance
1. Select the instance to be removed from the instance group and click **Remove**.
2. In the pop-up dialog box, click **Remove selected instance** to remove the instance from the instance group.


### Deleting instance group

1. Log in to the [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/).
2. On the left sidebar, click **Instance Group** to enter the instance group page.
3. Find the instance group to be deleted and click **Delete** in the "Operation" column on the right.
![](https://main.qcloudimg.com/raw/6d6e0317382b75f2e04888f9097e9175.png)
4. In the pop-up dialog box, click **Delete** to delete the instance group.
>When an instance group bound to an alarm policy is deleted, the alarm policy will become invalid.


### Copying instance group

1. Log in to the [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/).
2. On the left sidebar, click **Instance Group** to enter the instance group page.
3. Find the instance group to be copied and click **Replication** in the "Operation" column on the right.
![](https://main.qcloudimg.com/raw/536ec4ef933bd01b7d8cb230d902ed10.png)
4. In the pop-up dialog box, click **Copy** to copy the instance group.
>When an instance group is copied, only instances in the group will be copied. If the copied instance group is bound to an alarm policy, the binding relationship will not be copied.


### Binding instance group to alarm policy

1. Log in to the [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/).
2. On the left sidebar, click **Alarm Configuration** > **Alarm Policy** to enter the alarm policy management page.
3. Click **Add** to enter the configuration page for creating policies.
4. Find the **Alarm Object** configuration item, enable **Select instance group**, and select the previously created instance group from the drop-down list as shown below.
![](https://main.qcloudimg.com/raw/061e22856354bdedcc321fa28869a5f4.png)
5. Complete the configurations for other items on the page. For more information, please see [Creating Alarm Policies](https://intl.cloud.tencent.com/document/product/248/38908).

