### Permission Control

- Cloud Monitoring (CM) is available to all users with a Tencent Cloud account.
- CM does not have an independent permission control feature. The root account can be used to view the monitoring and alarm information of all services, and collaborators can view all resource monitoring and alarm information of their corresponding projects.

### Storage period of monitoring data

Currently, monitoring data can be stored for a maximum of 6 months. You can query monitoring data from the past 6 months.

| Monitoring Granularity | Storage Period |
| ------------ | -------- |
| Seconds-level | 1 day |
| One minute or five minutes | 31 days |
| One hour | 93 days |
| One day | 186 days |

### Alarm Limits

- Alarm message quotas
  Alarm messages are divided into four types: basic alarms, cloud automated testing alarms, custom messages, and custom monitoring alarms. Each type has a separate quota. Every month, 1,000 free messages of each type are provided to each user. The quota for each type is reset to 1,000 on the first day of each month. If you need additional message quota, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- Quantity limit of alarm policy groups
  A maximum of 15 alarm policy groups can be created for each user under each project.
  A maximum of 15 alarm rules can be created for each policy group.
