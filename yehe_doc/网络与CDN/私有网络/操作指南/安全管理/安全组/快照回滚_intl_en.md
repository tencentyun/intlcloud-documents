If a security group is configured with a snapshot policy, its rules will be backed up according to the configured policy. To roll back its rules, perform a snapshot rollback.
>?The snapshot feature is currently in beta test. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
>

## Prerequisites
The security group is configured with a [snapshot policy](https://intl.cloud.tencent.com/document/product/215/46788), and at least one snapshot backup has been performed.

## Directions
1. Log in to the [Security Group console](https://console.cloud.tencent.com/vpc/securitygroup?rid=1&rid=1) and enter the **Security Group** management page.
3. On the **Security Group** management page, click the ID of the target security group to enter its details page.
4. Click the **Snapshot Rollback** tab, which displays all the snapshot records by time. By default, records from the past seven days are displayed. You can customize the time range for querying snapshot records.
>?If there are many backup records, we recommend you limit the time range to three months; otherwise, the system may become slow.
>
![]()
5. Click **Export** to export the inbound and outbound rules of the security group in the snapshot record, which will be stored in two files.
6. Click **Restore** to enter the security group restoration page, which displays the security group rule preview and comparison.
>?
>+ The `+` sign in the figure identifies the rule entries newly added to the snapshot backup record, while `-` identifies the deleted entries. Note that the current comparison is based on the time period currently selected for comparison preview, during which if rules are changed, the comparison result may be inaccurate.
>+ When a security group is restored, if its source contains parameter template rules and nested security groups, the rules within the parameter template and the associated security group instance will remain in the current status.
>+ Note that restoring a security group is equivalent to importing it, which means all the current rules will be overwritten.
>
![]()
7. After confirming that everything is OK, click **OK**.
