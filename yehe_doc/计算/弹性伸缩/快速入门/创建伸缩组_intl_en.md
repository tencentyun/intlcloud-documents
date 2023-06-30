A scaling group contains a collection of CVM instances that follow the same policies and have a shared purpose.

## Creating a Scaling Group
1. Log in to **Auto Scaling Console** and click **[Scaling group](https://console.cloud.tencent.com/autoscaling/group)** in the left sidebar.
2. Select a region and click **Create** on the top of the scaling group list.
3. In Create scaling group pop-up, complete the basic configurations. Fields marked with <label style="color:#e1504a;">*</label>  are required, as shown below: 
![](https://main.qcloudimg.com/raw/09b130b952b426530acbe5ad6288b5d7.png)
 - A scaling group maintains the number of CVM instances to meet the desired capacity between the minimum and maximum capacity values.
 - The initial capacity defines the default number of CVM instances in the scaling group.
	- If a scaling group has a number of CVM instances fewer than the minimum scaling capacity value, it will automatically add instances to meet the minimum condition.
	- If a scaling group has a number of CVM instances greater than the maximum scaling capacity value, it will automatically terminate instances until the number of instances is equal to the maximum value allowed.
 - Select an existing launch configuration or create one.
 - Select the supported networks and subnet.
 - **(Optional) Associate with an existing CLB instance or create one.**
4. After the configuration is completed, you will see this entry on the scaling group list, as shown below:
![](https://main.qcloudimg.com/raw/3943d03b316974835be615acef893bd2.png)


## Adding an Instance (optional)
1. Click the ID of a scaling group in the **[Scaling group](https://console.cloud.tencent.com/autoscaling/group)** page.
2. Select the **Bind with Instance** tab, and click **Add Instances**, as shown below:
![](https://main.qcloudimg.com/raw/741d48877eaef9642dfff2193d540403.png)
3. In "Add Instances" pop-up, select instances to add to the scaling group.
4. Click **OK** to complete the configuration.
You will see the added instances on the launch configuration list.
> If you are unable to add or remove a CVM instance to or from the list, check the maximum and minimum capacity values you specified.


