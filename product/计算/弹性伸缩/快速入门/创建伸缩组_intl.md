A scaling group contains a collection of CVM instances that follow the same policies and have a shared purpose.

## Creating a Scaling Group

1. Log in to the [AS console](https://console.cloud.tencent.com/autoscaling/config).
2. In the left sidebar, click **Scaling Group** to go to the scaling group management page.
3. Click **Create**  and enter the necessary information of the scaling group on the pop-up page. Fields marked with ![](//mccdn.qcloud.com/static/img/f9df27a1d1e0d42a7ff08dd884bfa34c/image.png) are required. See the figure below:

![](https://main.qcloudimg.com/raw/09b130b952b426530acbe5ad6288b5d7.png)

 - A scaling group maintains the number of CVM instances to meet the desired capacity between the minimum and maximum capacity values.
    - The starting instance quantity defines the default number of CVM instances in the scaling group.
    - If a scaling group has a number of CVM instances less than the minimum scaling capacity value, it will automatically increase the number of instances to meet the minimum condition. 
    - If a scaling group has a number of CVM instances greater than the maximum scaling capacity value, it will automatically terminate instances until the number of instances is equal to the maximum value allowed.
 - Select an existing launch configuration or create a new one.
 - Select the network, availability zone, and removal policy.
 - **(Optional) Associate with an existing CLB instance or create a new one.**
4. After the configuration is completed, you will see this entry on the scaling group list, as shown below: 
![](https://main.qcloudimg.com/raw/3943d03b316974835be615acef893bd2.png)

## Adding a CVM (Optional)

1. On the **Scaling group** page, click "Scaling group" to go to the scaling group management page.
2. Select the **Associate with Instances** tab and click **Add Instances**. See the figure below:
![Add a CVM](https://main.qcloudimg.com/raw/741d48877eaef9642dfff2193d540403.png)
3. In "Add Instances" pop-up, add the instance that you want to bind to the scaling group.
4. Click **OK** to complete the configuration.
You will see the information of the added CVM on the launch configuration list.
> If you are unable to add/remove a CVM instance to/from the list, please check the maximum and minimum capacity values you specified.

