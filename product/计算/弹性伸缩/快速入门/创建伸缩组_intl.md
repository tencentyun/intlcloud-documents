A scaling group is a collection of CVM instances that follow the same rules and are used for the same scenario.

## Creating a Scaling Group

1. Log in to the [AS console](https://console.cloud.tencent.com/autoscaling/config).
2. In the left sidebar, click **Scaling Group** to go to the scaling group management page.
3. Click ![](//mccdn.qcloud.com/static/img/9d38f7bfbe02a922370765f3adfa58bf/image.png) and enter the basic information of the scaling group on the pop-up page. Fields marked with ![](//mccdn.qcloud.com/static/img/f9df27a1d1e0d42a7ff08dd884bfa34c/image.png) are required. See the figure below:
![](https://mc.qcloudimg.com/static/img/2fb365611291fb8917637dba46f398f4/image.png)
 - The current number of CVM instances in the scaling group will be maintained between the minimum and maximum capacity.
 - The starting instance quantity defines the number of CVM instances in the scaling group at the very beginning.
	- If the current number of CVM instances is less than the minimum scaling capacity, AS will automatically add instances to make the former equal to the latter.
	- If the current number of CVM instances is greater than the maximum scaling capacity, AS will automatically remove instances to make the former equal to the latter.
 - Select an existing launch configuration or create a new one.
 - Select the network, availability zone, and removal policy.
 - **(Optional) Associate with an existing CLB instance or create a new one.**
4. After the configuration is completed, this entry will be displayed in the list of scaling groups on the page. See the figure below:
![](https://main.qcloudimg.com/raw/0197c612535f16befb90c11c3fa51951.png)

## Adding a CVM (Optional)

1. On the **Scaling group** page, click "Scaling group" to go to the scaling group management page.
2. Select the **Associate a CVM** tab and click **Add a CVM**. See the figure below:
![Add a CVM](https://main.qcloudimg.com/raw/ff81144cd7c6b7a0eb27ec4be2533aaa.png)
3. In the "Add a CVM" window that pops up, add the instance that you need to bind.
4. Click **OK** to complete the configuration.
Information of the added CVM will be displayed in the launch configuration list.
>? If you are unable to add or remove an CVM here, please check the maximum and minimum capacity setting.

