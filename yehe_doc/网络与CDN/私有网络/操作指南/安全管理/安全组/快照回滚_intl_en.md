If a security group is configured with a snapshot policy, its rules will be backed up according to the configured policy. To roll back its rules, perform a snapshot rollback.

## Prerequisites
Configure a [snapshot policy](https://cloud.tencent.com/document/product/215/63324) for the security group and create a snapshot backup.

## Directions
1. Log in to the [Security Group console](https://console.cloud.tencent.com/vpc/securitygroup?rid=1&rid=1) and enter the **Security Group** management page.
2. On the **Security Group** management page, click the ID of the target security group to enter its details page.
3. Click the **Snapshot Rollback** tab, which displays all the snapshot records by time. By default, records from the past seven days are displayed. You can specify a query period.
>?If there are many backup records, we recommend you limit the time range to three months; otherwise, the system may become slow.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Jkdx790_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230330101859.png)
4. Click **Export** to export the inbound and outbound rules saved in this snapshot. Rules are separately in the **Inbound rules** and **Outbound rules** files.
5. Click **Restore** to enter the security group restoration page, which displays the security group rule preview and comparison.
>?
>+ **+** indicates newly-added entries, while **-** means that the entry is deleted. The comparison result is based on the time period currently selected for comparison preview, during which if rules are changed, the comparison result may be inaccurate.
>+ When a security group is restored, if its source contains parameter template rules and nested security groups, the rules within the parameter template and the associated security group instance will remain in the current status.
>+ Note that when you restore a security group with a snapshot, all current rules are overwritten.
>
6. Click **OK** to complete the rollback.
