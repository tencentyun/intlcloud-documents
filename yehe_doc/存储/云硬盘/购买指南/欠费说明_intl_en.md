## CBS Overdue Policy
<dx-tabs>

::: Pay-as-you-go cloud disks
>!
- After you stop using pay-as-you-go resources, **terminate them as soon as possible** to avoid fee deduction.
- Since your actual resource consumption changes constantly, some slight discrepancies may exist for your stated balance.

![](https://main.qcloudimg.com/raw/becc841c9f150f7ad781da71278fbed3.png)

### Alerts
<table>
<tr>
<th>Type</th><th>Description</th>
</tr>
<tr>
<td><b>Low balance alert</b></td>
<td>The system estimates when your account balance will run out based on the current balance amount and the resource usage is the past 24 hours. When the balance is estimated to run out in 5 days or less, a low balance alert is sent to your Tencent Cloud account creator and collaborators who have subscribed to messages via email, SMS, and the Message Center.</td>
</tr>
<tr>
<td><b>Overdue payment alert</b></td>
<td>Pay-as-you-go resources are billed for every clock-hour. When your account balance goes negative (as Point 1 in the figure above), an alert will be sent to your Tencent Cloud account creator and collaborators who have subscribed to messages via email, SMS, and the Message Center.</td>
</tr>
</table>

### Processing for overdue payment

- You can continue to use the pay-as-you-go cloud disk for 2 hours from the moment your account balance becomes negative. You will be billed for this period. After 2 hours (Point 2 in the figure above), its services will be suspended (cloud disk is unavailable and can only store data). You will still be billed according to the billing standard (even if the account balance is negative) until data is completely erased.
- If your Tencent Cloud account is topped up to a positive balance within 15 days after the cloud disk has its services suspended, the disk can be restored.
- If the balance has been negative for 15 days after the suspension of cloud disks (Point 3 in the figure above), the pay-as-you-go disk will be repossessed. All data will be erased and **cannot be recovered**. Tencent Cloud account creator and all collaborators will be notified via email, SMS, and the Message Center.
:::
</dx-tabs>

## [Snapshot Overdue Policy](id:SnapshotArrears)
### Freezing
Once your Tencent Cloud account becomes overdue, snapshots will go into the **Isolated** status. The snapshot-related operations are not allowed, including the snapshot creation, rollback, cross-region replication, scheduled snapshot policies, etc.
- The isolated snapshots will be retained for 30 days. If your account balance remains negative, all snapshots (except for image snapshots) will be deleted after this period.


### Notes
- Even after your account becomes overdue, the **snapshot storage size exceeding the free tier will still be billed** until being deleted.
- Once snapshots are terminated, the data cannot be restored.
- Once the overdue payment is paid, snapshot operations are automatically resumed.
- If you no longer need a snapshot, delete it to avoid fee deduction. For more information, see [Deleting Snapshots](https://intl.cloud.tencent.com/document/product/362/5758).


