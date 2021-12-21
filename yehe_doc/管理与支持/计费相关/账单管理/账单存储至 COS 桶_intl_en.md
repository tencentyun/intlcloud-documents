## Overview

Tencent Cloud allows you to save bill data as files to COS buckets on a regular basis. If the volume of your bill data is high (for example, if over 200,000 bill entries are generated for a month), bill data query via APIs may be slow. In this case, we recommend you enable bill storage so that you can obtain bill files from COS buckets for analysis.

>? You may incur fees for using this feature. For details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871).
>


## Enabling Bill Storage to COS

1. On the [Bill Overview](https://console.cloud.tencent.com/expense/bill/overview) page, set **Bill Storage** to ![](https://main.qcloudimg.com/raw/48d005ca49e683a3370212a71599ddd4.png).
![](https://main.qcloudimg.com/raw/867d2593c09f06dc3fd80b525d0c1f5e.png)
2. Grant access to the service role.
In the pop-up window, click **Authorize** and, on the authorization page, click **Grant**.
<img src="https://main.qcloudimg.com/raw/30d935403805ae73cdb1763300666cef.png" style="width: 70%"/></br>
3. Set storage information.
Select a bill type and a COS bucket to save bill files. You can also save the bill files of your member accounts to a COS bucket.
<img src="https://main.qcloudimg.com/raw/f1f27951392a135d9304cf9186d54066.png" style="width: 70%"/></br>
Bill Type
 - Daily bills: If you select daily bills, at 3:00 AM each day, new bill details for the period between the first day of the month and the previous day will be saved to the specified COS bucket. However, on the first day (billing day) of a month, bill data is saved to COS at 8:00 PM.
 For example, on April 6, a bill summary for the period from April 1 to April 5 will be added, and on April 8, a bill summary for the period from April 1 to April 7 will be added.
 - Monthly bills: If you select monthly bills, on the second day of each month, bill details for the previous month will be saved to the specified COS bucket. Data will be saved as multiple CVS files if the volume is high.


## Other Operations

- **To disable bill storage**, follow the steps below.
 1. Set **Bill Storage** to ![](https://main.qcloudimg.com/raw/ab69e4e4f7e979b04d67ea3d55b2a718.png).
 2. In the pop-up window, click **Disable Storage**.
 3. Click **Confirm** to disable bill storage. Existing data in the bucket will be kept, but new bill data will no longer be saved to the bucket.
-**To change the bucket**, select the new bucket you want to use and click **Save**. Existing data in the old bucket will be kept, while new bill data will be saved to the new bucket.


## Related Topics
- Querying the names of bill files via a COS API: [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614)
- Downloading bill files via a COS API: [GET Object](https://intl.cloud.tencent.com/document/product/436/7753)
