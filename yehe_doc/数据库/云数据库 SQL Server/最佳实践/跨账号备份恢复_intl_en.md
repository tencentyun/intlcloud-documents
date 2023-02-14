TencentDB for SQL Server supports intra-region cross-account backup restoration; that is, you can get the backup file download URL of an instance under account A, and then restore data under account B. The following describes how to do this.

## Notes
- After getting the backup file download URL of an instance under account A, perform backup restoration under account B. The two accounts need to be in the same region.
- This backup restoration mode currently supports backup files in .bak format.
- To use intra-region cross-account backup restoration, the form of the backup file obtained in the console must be unarchived file.
- .tar and .zip files will be supported for backup restoration in January 2023, subject to change as displayed in the console.
- Currently, the backup file download URL needs to be decoded as detailed [below](#jmcz).

## Step 1. Get the backup file download URL under account A
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver#/) with account A and click an instance ID in the instance list to enter the instance management page.
2. On the instance management page, select the **Backup Management** tab and click **View Details** in the **Operation** column of the target unarchived file in the data backup list.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/3Tm8501_29.png)
3. Click **Download** in the pop-up window and copy the download URL.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/fuY9370_30.png)

## Step 2. Decode the URL
You need to decode the backup file download URL obtained under account A.
Click [Decode Online](http://www.ab173.com/enc/urlencode.php) and decode the URL obtained in step 1 on the page redirected to.
>?Only the first part of the download URL needs to be decoded.
>**Sample**: Suppose a download URL is:
>`https://sqlserver-bucket-bj-1258415541.cos.ap-beijing.myqcloud.com/1312368346%2fsqlserver%2fmssql-8e5hjaiq%2fbackup%2fautoed_instance_58013012_AdventureWorksDW2012_2022_12_29023915.bak?**********`
>You only need to select the URL part until `.bak?` for decoding. Then, combine the output string with the second part of the URL to get the final URL for cross-account backup restoration.
>For the above sample URL, take the following part for decoding:
>`https://sqlserver-bucket-bj-1258415541.cos.ap-beijing.myqcloud.com/1312368346%2fsqlserver%2fmssql-8e5hjaiq%2fbackup%2fautoed_instance_58013012_AdventureWorksDW2012_2022_12_29023915.bak?`
>It is decoded to:
>`https://sqlserver-bucket-bj-1258415541.cos.ap-beijing.myqcloud.com/1312368346/sqlserver/mssql-8e5hjaiq/backup/autoed_instance_58013012_AdventureWorksDW2012_2022_12_29023915.bak?`
>Then, the final URL for cross-account backup restoration is:
>`https://sqlserver-bucket-bj-1258415541.cos.ap-beijing.myqcloud.com/1312368346/sqlserver/mssql-8e5hjaiq/backup/autoed_instance_58013012_AdventureWorksDW2012_2022_12_29023915.bak?**********`

## Step 3. Restore data under account B
Copy the final URL for backup restoration obtained in step 2.
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver#/) with account B and click an instance ID in the instance list to enter the instance management page.
2. On the instance management page, select **Backup and Restoration** > **Create**.
3. In the pop-up window, configure the following items and click **Create Task**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ECHh168_33.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Task Name</td>
<td>Enter the task name, which can contain up to 60 letters, digits, or underscores.</td></tr>
<tr>
<td>Backup Upload Method</td>
<td>Select **Download File from COS**.</td></tr>
<tr>
<td>Restoration Mode</td>
<td>Select **Full Backup File**.</td></tr>
</tbody></table>
4. In the **Upload Backup File** window, paste the URL and click **Save**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Rs4w297_34.png)
5. Go to the **Backup and Restoration** tab, find the backup task you just created, and click **Start** in the **Operation** column.
6. In the backup and restoration list, check the migration task status. When it becomes **Migration succeeded**, the cross-account backup restoration is completed.
