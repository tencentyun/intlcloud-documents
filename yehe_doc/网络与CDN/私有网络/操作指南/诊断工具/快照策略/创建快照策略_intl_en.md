When you need to back up security group rules to meet subsequent business needs or roll back to the original rules due to new rule exceptions, you can configure a snapshot policy.
>!Authorize the COS service: As snapshot records are stored in a COS bucket, you need to perform read and write operations on COS. If you have not authorized the COS service when creating the snapshot policy, the system will automatically pop up a window for you to perform authorization as prompted. After performing the authorization, you can refresh the page to go to the snapshot policy page. No more authorization is required after that.
>

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/) and choose **Diagnostic Tools** > **Snapshot policy** in the left sidebar.
2. Click **Create**.
3. In the **Create snapshot policy** pop-up window, configure the parameters.
<table>
<tr>
<th width="20%">Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>Name</td>
<td>Customize the snapshot policy name, which can contain digits, letters, and special symbols.</td>
</tr>
<tr>
<td>Backup Policy</td>
<td>Operation-triggered backup and scheduled backup are supported:<ul><li><b>Operation-triggered backup</b>: A backup is triggered each time the security group rule is "operated".
<dx-alert infotype="notice" title="">
Currently, you can perform up to five operations per ten seconds. More frequent operations will not be recorded.
</dx-alert>
<li><b>Scheduled backup</b>: Backups are performed at fixed time points.</td>
</tr>
<tr>
<td>Backup start time</td>
<td>This parameter is displayed only when you select <b>Scheduled Backup</b>. The date ranges from Monday to Sunday, and the time can be accurate to the second. Up to five backup times can be added, and at least one is retained.
<dx-alert infotype="notice" title="">
The backup operation is affected by the data volume. When the data volume is large, there may be some deviation between the selected time point and the actual time point.
</dx-alert>
</td>
</tr>
<tr>
<td>Snapshot Retention</td>
<td>You can customize the retention period of backup records, after which the records will be deleted automatically. The maximum value is 365 days.</td>
</tr>
<tr>
<td>Creating COS Bucket</td>
<td><ul><li ><b>Yes</b>: Create a COS bucket.<li><b>No</b>: Use an existing COS bucket.</td>
</tr>
<tr>
<td>COS Bucket</td>
<td><ul><li>If you choose to create a COS bucket, select the region and enter the COS bucket name, which cannot be changed once set. The name can contain lowercase letters, digits, and hyphens, and the access domain name must contain less than 60 characters.<li>If you select an existing COS bucket, select the region and the bucket name, which cannot be changed once selected.<p>
<dx-alert infotype="notice" title="">
The backup information is stored in a COS bucket. After the bucket is deleted, the snapshot information cannot be queried or restored.
</dx-alert>
</td>
</tr>
<tr>
<td>COS bucket name</td>
<td>A COS bucket name is in the format of <b>Custom name - Developer app ID</b>. A COS bucket name can contain up to 60 characters, including letters, digits, and hyphens (-). A COS bucket name cannot be changed once set.</td>
</tr>
</table>
4. Click **OK**.

## Related Operations
[Associating Security Group](https://intl.cloud.tencent.com/document/product/215/46790)