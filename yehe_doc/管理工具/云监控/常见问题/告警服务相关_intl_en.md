### Why cannot I receive alarm notifications through some alarm channels?

- **Alarm notifications cannot be received via SMS**:
	- In the user list in the [CAM Console](https://console.cloud.tencent.com/cam), click a username to access the user details page and check that the user's phone number has been verified.
	- In the [alarm policy](https://console.cloud.tencent.com/monitor/policylist) list, check whether the SMS channel is blocked in the corresponding alarm policy.
	- On the right of the [Monitoring Overview](https://console.cloud.tencent.com/monitor/overview) page, check whether the free quota of SMS messages has been used up. For more information, please see [SMS Alarm Channel](https://intl.cloud.tencent.com/zh/document/product/248/38908).
- **Alarm notifications cannot be received via email**:
	- In the user list in the [CAM Console](https://console.cloud.tencent.com/cam), click a username to access the user details page and check that the user's email address has been verified.
	- In the [Alarm Policy](https://console.cloud.tencent.com/monitor/policylist) list, check whether the email channel is blocked in the corresponding alarm policy.

### Why cannot some recipients in the alarm recipient group receive alarm notifications?

The alarm recipients’ information for relevant alarm channels (SMS, and email) has not been verified. Please verify the information in the [CAM Console](https://console.cloud.tencent.com/cam).

### If a user is in multiple recipient groups that are all bound to an alarm policy, will the user receive multiple alarm notifications?

Yes. You can create a new recipient group based on your business needs to prevent individual users from receiving repeated alarm notifications.

### When will an alarm notification expire? Why cannot an alarm notification be received if it has not been restored for a few days?

- Non-repeated alarm notifications: only one alarm notification will be received through each alarm channel.
- Default logic for repeated (once every 5 minutes, hour, or day) alarm notifications:
	- The alarm notification will be sent to you at the configured frequency within 24 hours after an alarm is triggered.
	- Following 24 hours after an alarm is triggered, the alarm notification will be sent once every day by default.
	- Following 72 hours after an alarm is triggered, the alarm notification will be sent for the last time.

### Will an alarm notification be received if the corresponding alarm is restored?

Yes. An alarm notification will be sent to the recipients after the corresponding alarm is restored.

### Will a CVM instance be automatically associated with the default policy on the backend after a user disassociates it from the default policy on the alarm object association page?

No. After a user disassociates a CVM instance from the default policy, it will not be automatically associated again on the backend.

### Can I restore an alarm by stopping and restarting it?

No. Stopping and restarting an alarm are only useful for disabling a no longer needed alarm policy and will not change the alarm status.

### What is the default alarm policy?

There is only one default policy for each project in each policy type. The default policy will be automatically created after you purchase an instance, which can be modified but not deleted.
Cloud Monitor will automatically create a default CVM alarm policy (alarms will be triggered when disks become read-only or ping becomes unreachable) and a default TencentDB policy (alarms will be triggered if the used disk capacity is greater than 90 MB or disk utilization exceeds 80% for 5 minutes).

### Why cannot alarm notifications be received under the default alarm policy?

For the default alarm policy created by the system, you need to associate it with an alarm recipient group before alarm notifications can be received.

### Which Tencent Cloud products support the default alarm policy?

Currently, the default alarm policy is only supported by CVM, TencentDB for MySQL, TencentDB for Redis, TencentDB for SQL Server, TencentDB for MongoDB, TencentDB for MariaDB, API Gateway, and Direct Connect. Other Tencent Cloud products will support the default alarm policy in the future. If you have any questions, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance. 

### Why are alarm notifications still received after a CVM instance is disassociated?

Because the system's data monitoring has latency, it is normal to still receive alarm notifications for a short period of time after the alarm policy is disassociated from a CVM instance.

### Where can I modify the alarm notification message template?

Currently, it cannot be modified.

### Why cannot the configured alarm recipients be read in custom alarm monitoring?

Basic Tencent Cloud resource monitoring and custom monitoring use different sub-account permissions. A sub-account does not have permission to query information about other sub-accounts by default. After the Cloud Monitor root account grants the `QcloudMonitorFullAccess` permission to a sub-account, the configured alarm recipients of basic Tencent Cloud resources monitoring cannot be synced with the alarm recipients of custom monitoring. If the sub-account needs to read configured alarm recipients in custom monitoring, you need to log in to the [CAM Module](https://console.cloud.tencent.com/cam/policy) with the root account and grant the `QcloudCamReadOnlyAccess` permission to the sub-account.

### How many alarm states are there and what do they mean?

Not restored: an alarm has not been processed or is being processed.
Restored: an alarm has been restored to its normal state.
Insufficient data: either the alarm policy that generated the alarm has been deleted, the CVM instance has migrated from one project to another, or no data is reported as Agent is not installed or has been uninstalled.

### What alarm changes will occur if the CDN domain name alarm policy of project A is associated with the domain `a.com`, which is then migrated to project B?

The CDN domain name policy of project A will automatically be disassociated from the domain `a.com`. After disassociation, if the domain `a.com` is not associated with any other CDN domain name alarm policies, no alarm will be triggered. The automatic disassociation logic will be implemented once every day. The console data may have an update delay, which is normal.

