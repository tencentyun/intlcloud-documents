## Querying Bills of Partner and Reseller's Customer

Step 1. Add the bucket to the allowlist. To enable this feature, contact your sales rep. For allowed UINs, the "Bill Storage" button will appear on the bill overview page.

![img](https://docimg9.docs.qq.com/image/FYi6VKGmXyNz1ZKDk6fPbA?w=2712&h=1004)

Step 2. Authorize the service role. After you click **Bill Storage**, a pop-up window will display a prompt for authorization. After clicking **Authorize**, you will be redirected to the role authorization page, where you need to click **Agree**.

Step 3. Select a bucket. If there are no buckets, click **Create Bucket**, and you will be redirected to the bucket creation page.

Step 4. Select **Store Custom Bills** to authorize the Tencent Cloud sales team to store the consolidated bills of customer accounts in your COS bucket.

<img src="https://docimg10.docs.qq.com/image/nQ3lziYhPbxeqOwvVzUclw?w=855&h=964&_type=png" alt="img" style="zoom: 50%;" />

>? 
> - The system sends the daily and monthly bills of your UINs to the COS bucket by default. In addition, after confirming the bills every month, the Tencent Cloud sales team will manually trigger the storage of the consolidated bills of customer accounts in your COS bucket.
> - Bills of sub-accounts can also be stored in the bucket. If you select a sub-account UIN, you can store the bills of the sub-account in your COS bucket.

### 1. Enable bill storage

After bill storage is enabled, the updated data will be stored in the specified COS bucket every day. There are three types of bills. For the reseller mode, pay attention to **Reseller bills**.

1) Daily bills (self use): on day+2, the new bill details will be stored in the COS bucket. For example, on April 6, a consolidated bill covering April 1–4 will be generated; on April 8, a consolidated bill covering April 1–6 will be generated.

2) Monthly bills (self use): the details of a complete monthly bill will be updated on the 2nd day of every month. If the data volume is too high, the bill will be split and zipped into a zip file.

3) Reseller bills: after confirming the bills on the 9th day of every month, the Tencent Cloud sales team will store the reseller bills in the bucket for download.

*File name sample: **100010445724-2021-03--by_used_time-bill-details-consolidated_bill-61121cbd9017a16285769571173521960.zip*

![img](https://docimg5.docs.qq.com/image/pc9K4lOvvMZBLjSwjgb78A?w=1704&h=396&_type=png)

### 2. Disable bill storage

To disable the bill feature, click the entry and click "Disable Bucket" in the pop-up window. After the feature is disabled, legacy data will be retained, but no new data will be written.

### 3. Change the bucket

To change the bucket, click the entry, select a different bucket, and click "Save Settings". Legacy data will be retained in the old bucket, while new data will be written into the new bucket on day+1.

