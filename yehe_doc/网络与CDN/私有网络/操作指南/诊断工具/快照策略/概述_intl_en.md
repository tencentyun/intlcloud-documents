A snapshot allows you to back up the associated object data according to the configured backup policy. Currently, it can be associated with a security group, so that you can back up the outbound and inbound rules of the associated security group. This feature is an auxiliary feature which does not affect the operations on security groups.
>?The snapshot feature is currently in beta test. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
>

## Use Cases
If you need to frequently update your security group rules, we recommend you configure a snapshot policy for the security group and promptly back up the security group rules. When the newly modified rules are abnormal, you can use the snapshot rollback feature to roll back to the original rules, thus ensuring the business availability.

## Use Limits
| Resource | Quota |
| ------ | ------ |
| Maximum number of snapshot policies that can be created by a user | 5 |
| Number of time points that can be set in each scheduled snapshot policy | 5 |
| Number of snapshot policies that can be associated with an object (security group) | 1|
| Number of objects (security groups) that can be associated with a snapshot policy | 50 |
| Maximum retention period of the scheduled snapshot policy | 365 days|
| Backup change frequency| Five times per ten seconds |

