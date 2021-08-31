## Operation Scenarios

If you want to send an alarm notification for the specific status of a product, you need to create an alarm policy first. The alarm policy consists of three mandatory components: name, type, and alarm trigger condition. You can create an alarm policy as instructed below.

## Directions

>The **Deprecated/Instances** field in the alarm policy list displays the number of [alarm objects](https://intl.cloud.tencent.com/document/product/248/6216) associated with the alarm policy. If the value is not 0, the policy cannot be deleted. Only when all alarm objects are disassociated can the policy be deleted.

1. Log in to the [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor).
2. Click **Alarm Configuration** > **Alarm Policy** to enter the alarm policy configuration page.
3. Click **Add** to configure an alarm policy.
4. Configure the basic items as shown below:
	- **Policy Name**: enter a policy name.
	- **Remarks**: add remarks to the policy.
	- **Policy Type**: select the monitoring metric.
	- **Project**: select a project as needed.
		![](https://main.qcloudimg.com/raw/0d04abed550857b11049e5b5e0060c48.png)
>
> - If you want to create a project, please see [Project Management](https://intl.cloud.tencent.com/document/product/378/34726).
> - After a project is created, you can assign it to cloud product resources in their respective consoles (some cloud products do not support project assignment). For example, in TencentDB for MySQL, you can assign instances to the corresponding project as instructed in [Specifying Project for Instance](https://intl.cloud.tencent.com/document/product/236/8460).
5. Configure alarm objects.
	- **If you select "All objects"**, the alarm policy will be bound to all instances under the current account.
	- **If you select "some objects"**, the alarm policy will be bound to the selected instances.
	- **If you select "instance group"**, the alarm policy will be bound to the selected instance group.
![](https://main.qcloudimg.com/raw/db8f59d5a2ef095604091a17fbc29c40.png)
6. Set the alarm trigger condition. You can either choose a trigger condition template or configure a trigger condition.
	- **Trigger condition template**:
		Enable "Trigger Condition Template" and select a configured template from the drop-down list. For detailed configurations, please see [Configuring Trigger Condition Templates](https://intl.cloud.tencent.com/document/product/248/32817). If a newly created template is not displayed, click **Refresh** on the right.
		![](https://main.qcloudimg.com/raw/db91be6d990263d8dc1882425a34c240.png)
	- **Configure trigger conditions**:
    Enable "Configure trigger conditions", which includes "Indicator alarm" and "Event Alarm".
    An alarm trigger condition is a semantic condition consisting of metric, comparison, threshold, statistical period, and duration. <br>For example, if the metric is CPU utilization, the comparison is `>`, the threshold is `80%`, the statistical period is `5 minutes`, and the duration is `2 periods`, then CPU utilization data of a CVM instance will be collected once every 5 minutes, and an alarm will be triggered if the CPU utilization exceeds 80% for three consecutive periods.
    You can set a repeated notification policy for each alarm rule so that an alarm notification will be sent repeatedly at specified frequency when an alarm is triggered.
    Frequency options: do not repeat, once every 5 minutes, once every 10 minutes, and other exponentially increased frequencies.
    Exponential increase means that when an alarm is triggered for the first time, second time, fourth time, eighth time, ..., or 2 to the power of Nth time, alarm notification will be sent to you. In other words, the alarm notification will be sent less and less frequently with longer time intervals in between, reducing the disturbance caused by repeated alarm notifications.
![](https://main.qcloudimg.com/raw/11936b16676c8ee4ccc75bfaa5430788.png)
>The default logic for repeated alarm notifications is as follows:
>- The alarm notification will be sent to you at the configured frequency within 24 hours after an alarm is triggered.
>- Following 24 hours after an alarm is triggered, the alarm notification will be sent once every day by default.
>- Following 72 hours after an alarm is triggered, the alarm notification will be sent for the last time and will not be sent again.
7. Configure the alarm channel.
   Configure the recipient group, the valid time period, and the receipt channel (email, SMS, and WeChat) as needed.
	 ![](https://main.qcloudimg.com/raw/c2b4f77f20135aa24ecaa2822d87ab9a.png)
>CVM alarms will be sent once [Agent](/doc/product/248/6211) has been installed on CVM instances and reports monitoring metric data. On the Cloud Monitor page, you can view CVM instances that do not have Agent installed and download the IP list.
8. You can configure an existing policy as the default alarm policy, which will be automatically associated with newly purchased CVM instances.
![](https://main.qcloudimg.com/raw/7aacfbd99a276ac04e0b90d53c32bbd0.png)
>
> - Only one default policy is allowed for each policy type in each project.
> - The default alarm policy cannot be deleted.
> - For your convenience, Cloud Monitor will automatically create a default CVM alarm policy (alarms will be triggered when disks become read-only or pings become unreachable) and a default TencentDB policy (alarms will be triggered if the used disk capacity is greater than 90 MB or disk utilization exceeds 80% for 5 minutes).
> - Currently, the default alarm policy is only supported by the following cloud products: CVM, TencentDB for MySQL, TencentDB for Redis, TencentDB for SQL Server, TencentDB for MongoDB, TencentDB for MariaDB, API Gateway, and Direct Connect.
