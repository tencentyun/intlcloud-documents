## Pay-As-You-Go

### Overdue payment reminder

| Reminder Type | Description |
| ------------ | ------------------------------------------------------------ |
| **Overdue payment reminder** | Pay-as-you-go clusters are billed on the hour. When your account balance becomes negative, your Tencent Cloud account creator, global resource collaborators, and financial collaborators will be notified through email and SMS. |
| **Overdue payment alert** | This feature is disabled by default. |

### Overdue payment policy
When your account balance becomes negative, the pay-as-you-go cluster can be used and fees will be deducted for 2 more hours. After 2 hours, the cluster will be moved to the recycle bin and become unavailable, and we will also stop billing you for service.

<table>
<tr>
<th>Time After Service Suspension</th>
<th>Description</th>
</tr>
<tr>
<td rowspan="2">≤ 15 days</td>
<td>If your account is topped up to a positive balance, the billing will continue, and the cluster will be automatically recovered.</td>
</tr>
<tr>
<td>If your account balance remains negative, the cluster cannot be recovered.</td>
</tr>
<tr>
<td >> 15 days</td>
<td>If your account is not topped up to a positive balance, your pay-as-you-go cluster resources will be repossessed and released. All data will be erased and cannot be recovered. When your cluster resources are repossessed, your Tencent Cloud account creator and all collaborators will be notified through email and SMS.</td>
</tr>
</table>

>!
>- When you no longer need to use pay-as-you-go clusters, please terminate them as soon as possible to avoid further fee deductions.
>- After a cluster is terminated, the data in it will be cleared and cannot be recovered.
>- Since your actual resource consumption may change over time, some balance alerts may be inaccurate.
