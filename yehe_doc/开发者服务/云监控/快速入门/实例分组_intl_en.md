
## Feature Overview

You can group cross-region and cross-project group instances of a Tencent Cloud product for unified management. When creating a large number of instances, you can create instance groups as needed. By managing instance groups, you can better manage instances, configure alarm policies, and improve Ops efficiency.

## Use Cases
- Alarm policies can be set for cross-instance and cross-region projects of the same product in a unified manner.
- You can manage various resources under your Tencent Cloud account by service category.

## Notes

- Each instance group can contain up to 2,000 instances, and a maximum of 200 instances can be added to an instance group at a time.
- By grouping instances, you can manage cross-region and cross-project group Tencent Cloud products in a unified manner and configure alarm policies to avoid repeated operations and improve Ops efficiency.

  

## Directions
### Creating an instance group

1. Log in to the [CM console](https://console.cloud.tencent.com/monitor/).
2. On the left sidebar, click **Instance Group** to enter the **Instance Group** page.
3. Click **Create** and configure the following fields:
	- Group Name: Enter the instance group name.
	- Group Type: Select an option as needed.
	- Add to Group: Select instances to be added to the group.
	![](https://main.qcloudimg.com/raw/7c89f33d6e5ea641dcd34c5068e98804.png)
4. Click **Save**.


### Editing an instance group

>?
>- If an instance group has been bound to an alarm policy, the instances added to it will be automatically bound to the alarm policy.
>- If an instance group has been bound to an alarm policy, the instances removed from it will be unbound from the alarm policy.

1. Log in to the [CM console](https://console.cloud.tencent.com/monitor/).
2. On the left sidebar, click **Instance Group** to enter the **Instance Group** page.
3. Select the name of the target instance group to enter the instance management page. You can create or delete instances in the instance group on this page.

#### Adding an instance
1. Click **Add**.
2. In the pop-up window, select the target instance.
3. Click **OK**.

#### Removing an instance
1. Select the target instance and click **Remove**.
2. In the pop-up window, click **Remove**.


### Deleting an instance group

1. Log in to the [CM console](https://console.cloud.tencent.com/monitor/).
2. On the left sidebar, click **Instance Group** to enter the **Instance Group** page.
3. Find the target instance group and click **Delete** in the **Operation** column on the right.
![](https://main.qcloudimg.com/raw/1475184a686e5f3ac067de8b679b1a30.png)
4. In the pop-up window, click **Confirm**.
>?When an instance group bound to an alarm policy is deleted, the alarm policy will become invalid.


### Copying an instance group

1. Log in to the [CM console](https://console.cloud.tencent.com/monitor/).
2. On the left sidebar, click **Instance Group** to enter the **Instance Group** page.
3. Find the target instance group and click **Copy** in the **Operation** column on the right.
![](https://main.qcloudimg.com/raw/cbdc0cdd9656921a9c5894ebfbb98e84.png)
4. In the pop-up window, click **Copy**.
>?When an instance group is copied, only instances in the group will be copied. If the copied instance group is bound to an alarm policy, the binding relationship will not be copied.


### Binding an instance group to an alarm policy

1. Log in to the [CM console](https://console.cloud.tencent.com/monitor/).
2. On the left sidebar, click **Alarm Configuration** > **Alarm Policy** to enter the alarm policy management page.
3. Click **Create** to enter the **Create Policy** page.
4. Find the **Alarm Object** configuration item and select **Instance Group** as shown below:
![](https://main.qcloudimg.com/raw/e70acdee37c55399ae06e87306251003.png)
5. Complete settings of other configuration items on the page.

