### Will an alarm recipient only receive one message upon an alarm, or will the message be sent again after a certain period of time?
No. Alarms are converged so an alarm will be sent to a user only once. If the CVM instance does not recover, the alarm will not be sent repeatedly. However, if the instance recovers from the alarm, the recipient will receive a new message if the alarm is triggered again.

### Will a CVM be automatically associated with a default policy in the backend after a user disassociates the CVM from the default policy on the alarm object association page?
No. After a user disassociates a CVM from a default policy, it will not be automatically associated again in the backend.

### How many alarm statuses are available in cloud monitoring and what do they mean?
Not recovered: An alarm has not been processed or is being processed.
Recovered: An alarm has been recovered to normal state.
Insufficient data: The alarm policy for generating an alarm has been deleted, the CVM is migrated from one project to another, or no data is submitted because Agent is not installed or is uninstalled.

### Can a CVM instance be associated with only one alarm policy?
Yes. A CVM instance can be associated with only one alarm policy. For example, assume CVM instance 1.1.1.1 is associated with alarm policy A. If you associate CVM 1.1.1.1 with alarm policy B, CVM 1.1.1.1 is automatically disassociated from alarm policy A.

### Which cloud products are supported by the default alarm policies?

Currently, default alarm policies support CVM and TencentDB for MySQL. Other cloud products will be gradually supported in the future. If you have any questions, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for consultation.

### What alarm changes occur If the CDN domain name alarm policy of project A is associated with domain name a.com, but domain name a.com Is migrated to project B?
The CDN domain name policy of project A is automatically disassociated from domain name a.com. If domain name a.com is not associated with any CDN domain name alarm policy, no alarm will be generated. The automatic disassociation logic is implemented once every day, so it is normal if the data on the console is not up-to-date.

### Why are alarms still received after a CVM instance is disassociated?
The system’s data monitoring has a certain latency. It is normal to receive alarms for a short time after the alarm policy is disassociated from a CVM instance.
