## CBS Overdue Policy
<dx-tabs>
::: Monthly subscription
### Alerts
<table>
<tr>
<th>Type</th><th>Description</th>
</tr>
<tr>
<td><b>Expiration alert</b></td>
<td>We will send you an expiration alert via email, SMS and Message Center every other day starting 7 days (the 7th, 5th, 3rd, and 1st days) before your monthly subscribed resources expire. The collaborators under your account can configure the receipt method in the console > Message Center > <a href="https://console.cloud.tencent.com/message/subscription">Message Subscription</a> and add recipients in the manner instructed in <a herf="https://cloud.tencent.com/document/product/555/35518">Overdue Payment Alert</a>.
</td>
</tr>
<tr>
<td><b>Overdue payment alert</b></td>
<td>On the day your monthly subscribed resources expire (the 1st day of the expiration) and every other day thereafter (the 3rd, 5th, 7th days, etc.), we will send you an overdue payment alert. You can configure the receipt method in the console > Message Center > <a href="https://console.cloud.tencent.com/message/subscription">Message Subscription</a> and add recipients.</td>
</tr>
</table>

### Repossession

The following instructions are only applicable to elastic cloud disks. The lifecycle of non-elastic cloud disks is the same as the associated CVMs. For more information, see [Payment Overdue](https://intl.cloud.tencent.com/document/product/213/2181).
- 7 days before the resources expiration date, you will receive an expiration alert and a renewal reminder.
- If your account balance is sufficient and auto-renewal is enabled, cloud disk will be auto-renewed on the expiry date.
- If your cloud disk is not renewed before expiration (including on the expiry date), it can still be used for 7 days after the expiry date. If your cloud disk is not renewed within 7 days after it expires, it will be **forcibly unmounted** from a CVM (if any) and its services will be suspended (the cloud disk is unavailable and can only store data). The disk will enter the recycle bin, where you can still restore and renew it. However, **the billing cycle of the renewed cloud disk starts on the end date of the previous billing cycle**.
- If your cloud disk is not renewed within 7 days after it enters the recycle bin, resources will be released and data in the expired cloud disk will be erased and **cannot be recovered**.

:::
::: Pay-as-you-go



<dx-alert infotype="notice" title="">
- After you stop using pay-as-you-go resources, **terminate them as soon as possible** to avoid fee deduction.
- Since your actual resource consumption changes constantly, some slight discrepancies may exist for your stated balance.
</dx-alert>




![](https://main.qcloudimg.com/raw/becc841c9f150f7ad781da71278fbed3.png)


### Overdue payment alert

Pay-as-you-go resources are billed by the hour. When your account balance becomes negative (Point 1 in the figure above), the system will send an alert to your Tencent Cloud account creator and all collaborators who have subscribed to messages via email, SMS, and the Message Center.




### Processing for Overdue Payments


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
- Image snapshots are retained permanently unless deleted.
- If you no longer need a snapshot, delete it to avoid fee deduction. For more information, see [Deleting Snapshots](https://intl.cloud.tencent.com/document/product/362/5758).


