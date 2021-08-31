### Why can't I receive alarm notifications through some alarm channels?

- **Alarm notifications cannot be received through SMS**:
	- In the user list in the [CAM console](https://console.cloud.tencent.com/cam), click a username to enter the user details page and check whether the user's mobile number has been verified.
	- In the [alarm policy](https://console.cloud.tencent.com/monitor/policylist) list, check whether the SMS channel is blocked in the corresponding alarm policy.
	- On the right of the [monitoring overview](https://console.cloud.tencent.com/monitor/overview) page, check whether the free tier of SMS messages has been used up. For more information, please see [SMS Alarm Channel](https://intl.cloud.tencent.com/document/product/248/38908).
- **Alarm notifications cannot be received through email**:
	- In the user list in the [CAM console](https://console.cloud.tencent.com/cam), click a username to enter the user details page and check whether the user's email address has been verified.
	- In the [alarm policy](https://console.cloud.tencent.com/monitor/policylist) list, check whether the email channel is blocked in the corresponding alarm policy.

### Why can't some recipients in the alarm recipient group receive alarm notifications?

Their information for relevant alarm channels (SMS and email) has not been verified. Please verify the information in the [CAM console](https://console.cloud.tencent.com/cam).

### If a user is in multiple recipient groups which are all bound to an alarm policy, will the user receive multiple alarm notifications?

Yes. You can create a new recipient group based on your business needs to prevent individual users from receiving repeated alarm notifications.

### When will an alarm notification expire? Why can't an alarm notification be received if it is not resolved for several days?

- Non-repeated alarm notifications: only one alarm notification will be received through each alarm channel.
- Default logic for repeated alarm notifications (once every 5 minutes, hour, or day):
	- The alarm notification will be sent to you at the configured frequency for 24 hours after an alarm is triggered.
	- Following 24 hours after an alarm is triggered, the alarm notification will be sent once every day by default.

### Will an alarm notification be received if the corresponding alarm is resolved?

Yes. An alarm notification will be sent to the recipients after the corresponding alarm is resolved.

### Will a CVM instance be automatically associated with the default policy on the backend after a user disassociates it from the default policy on the alarm object association page?

No. After a user disassociates a CVM instance from the default policy, it will not be automatically associated again on the backend.

### Can I resolve an alarm by disabling it?

No. The alarm switch is only used to disable a no longer needed alarm policy and will not change the alarm status.

### What is the default alarm policy?

There is only one default policy for each project in each policy type. The default policy is automatically created after you purchase an instance, which can be modified but not deleted.
Cloud Monitor will automatically create a default CVM alarm policy (alarms will be triggered when disks become read-only or unreachable ping occurs) and a default TencentDB policy (alarms will be triggered if the used disk capacity is greater than 90 MB or disk utilization exceeds 80% for 5 minutes).

### Why can't alarm notifications be received under the default alarm policy?

For the default alarm policy created by the system, you need to associate it with an alarm recipient group before alarm notifications can be received.

### Which Tencent Cloud products support the default alarm policy?

Currently, the default alarm policy is supported only by CVM, TencentDB for MySQL, TencentDB for Redis, TencentDB for SQL Server, TencentDB for MongoDB, TencentDB for MariaDB, API Gateway, and Direct Connect. Other Tencent Cloud products will support it in the future. If you have any questions, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance. 

### Why are alarm notifications still received after a CVM instance is disassociated?

The system's data monitoring has a certain latency. It is normal to still receive alarm notifications for a short period of time after the alarm policy is disassociated from a CVM instance.

### Where can I modify the alarm notification message template?

Currently, it cannot be modified.

### Why can't the configured alarm recipients be read in custom monitoring alarming?

Basic Tencent Cloud resource monitoring and custom monitoring use different sub-account permissions. A sub-account has no permission to query information of other sub-accounts by default. After the Cloud Monitor root account grants the `QcloudMonitorFullAccess` permission to a sub-account, alarm recipients configured in basic Tencent Cloud resource monitoring cannot be synced to custom monitoring. If the sub-account needs to read configured alarm recipients in custom monitoring, you need to log in to the [CAM module](https://console.cloud.tencent.com/cam/policy) with the root account and grant the `QcloudCamReadOnlyAccess` permission to the sub-account.

### How many alarm states are available in monitoring and what do they mean?

<escape>
<table>
<tr>
<th>Alarm Status</th>
<th>Description</th>
</tr>
<tr>
<td>Not resolved</td>
<td>An alarm has not been processed or is being processed.</td>
</tr>
<tr>
<td>Resolved</td>
<td>Normal status has been restored</td>
</tr>
<tr>
<td>Insufficient data</td>
<td><ul style="margin:0;list-style-type:disc;"><li>The alarm policy that triggered an alarm has been deleted.</li><li>The CVM instance has been migrated from one project to another.</li><li>No data is reported because Agents have not been installed or have been uninstalled.</li></ul></td>
</tr>
<tr>
<td>Expired</td>
<td><ul style="margin:0;list-style-type:disc;"><li>The alarm policy has changed.</li><li>The latest triggering time of the alarm has not been updated for more than 24 hours.</li></ul></td>
</tr>
</table>
</escape>


### What alarm changes will occur if the CDN domain name alarm policy of project A is associated with the domain name `a.com` which then is migrated to project B?

The CDN domain name policy of project A will be automatically disassociated from the domain name `a.com`. If the domain name `a.com` is not associated with any CDN domain name alarm policy, no alarm will be triggered. The automatic disassociation logic is implemented once every day, so it is normal if the data on the console is not up-to-date.

