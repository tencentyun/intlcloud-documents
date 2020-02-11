## Scheduled Actions

Scheduled actions refer to scheduling scaling activities. This allows you to scale the number of CVM instances in response to predictable load changes.

For example, every week the traffic to your Web application starts to increase on Wednesday, remains high on Thursday, and starts to decrease on Friday. You can schedule scaling activities based on the predictable traffic pattern of your Web application.

To create a scheduled scaling action, specify the start time of the scaling action, the new minimum (min capacity), maximum (max capacity), and required size (desired capacity) for the scaling action. At the specified time, AS will update the number of instances in the scaling group based on these values.

You can create scheduled actions for one-time scaling or for a recurring schedule.


## Scheduled Action Management
1. Open the [Console](https://console.cloud.tencent.com/autoscaling/config), and select **Scaling Group** in the navigation bar.

2. Select the scaling group to be modified, and click the **Scaling Group ID** to enter the basic information page.
![](https://mc.qcloudimg.com/static/img/cebad1b79ccba9fb9548c2bd2c30a210/31.jpg)
3. Select **Scheduled Action** in the top navigation bar, and manage the scheduled action associated with the scaling group on the page:
![](https://mc.qcloudimg.com/static/img/a649a9205c2b994db09c4b79583a3827/32.jpg)

	- Click **Create** to add a new scheduled action.

	- Select a scheduled action and click **Modify**. On the pop-up page, modify the action name, the execution time, and the activities to be executed, and choose whether to execute the action periodically.

	- Click **Delete** to delete the scheduled action.

If you want to create a scheduled action on a recurring schedule, you can specify the start time. AS will perform the action at this time, and then performs the action based on the recurring schedule. If you specify an end time, AS does not perform the action after this time.

