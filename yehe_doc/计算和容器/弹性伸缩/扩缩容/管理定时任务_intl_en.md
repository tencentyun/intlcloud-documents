## Scheduled Actions

Scheduled actions refer to scheduling scaling activities. This allows you to scale the number of CVM instances in response to predictable load changes.

For example, every week the traffic to your Web application starts to increase on Wednesday, remains high on Thursday, and starts to decrease on Friday. You can schedule scaling activities based on the predictable traffic pattern of your Web application.

To create a scheduled scaling action, specify the start time of the scaling action, the new minimum (min capacity), maximum (max capacity), and required size (desired capacity) for the scaling action. At the specified time, AS will update the number of instances in the scaling group based on these values.

You can create scheduled actions for one-time scaling or for a recurring schedule.


## Scheduled Action Management
1. Log in to the [Auto Scaling Console](https://console.cloud.tencent.com/autoscaling/group) and click **Scaling Groups** in the left sidebar.
2. Select the scaling group to be modified and click the **Scaling Group ID** to go to the basic information page, as shown in the figure below:
![](https://main.qcloudimg.com/raw/1f2704813583a24d01f11c8b849f4d9f.png)
3. On the details page of the scaling group, select the **Scheduled Action** tab and configure the scheduled action associated with the scaling group on the page, as shown in the figure below:
![](https://main.qcloudimg.com/raw/e10b7447c1a58eb9f8635472cdbc44ad.png)
	- Click **Create** to add a new scheduled action.
	- Select a scheduled action and click **Modify**. On the pop-up page, modify the action name, the execution time, and the activities to be executed and choose whether to execute the action periodically.
	- Click **Delete** to delete the scheduled action.
>? If you want to create a scheduled action on a recurring schedule, you can specify the start time. AS will perform the action at this time and then performs the action based on the recurring schedule. If you specify an end time, AS will not perform the action after the set time.

