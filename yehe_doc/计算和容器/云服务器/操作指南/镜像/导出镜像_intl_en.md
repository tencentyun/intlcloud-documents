## Overview
Tencent Cloud allows you to export created custom images to [COS](https://intl.cloud.tencent.com/document/product/436/6222) buckets.

## Prerequisites
- Currently, before using the feature, you need to [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) to apply for it.
- You have activated the COS service in the [COS console](https://console.cloud.tencent.com/cos).
- You have created a bucket for the region where the custom image to export resides. For more information, see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).


## Limits
- Currently, Windows custom images cannot be exported.
- For a custom image, the capacity of a system disk or data disk cannot be greater than 500 GB.
- When the image of an entire CVM instance is exported, the CVM instance cannot contain more than 5 data disks.


## Directions
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index) and choose **Images** on the left sidebar.
2. In the upper part of the **Images** page, select the region where the custom image to export resides and click the **Custom Image** tab.
3. Locate the image to export and choose **More** > **Export Image**.
![](https://qcloudimg.tencent-cloud.cn/raw/67a493d7ae96d92b514f5c124619821c.png)
4. In the pop-up **Export Image** window, set parameters as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/b82204f85356dd94966fcfae846795d4.png)
 - **COS Bucket**: select the bucket where the image to export resides. Make sure that the bucket is in the same region as the image to export.
 - **Export File Prefix**: customize the prefix of the file to export.
 Select to **agree to authorize CVM to access my COS bucket**.
5. Click **OK** to start exporting the image.
6. In the pop-up window, click **OK**.
The export duration depends on the size of the image file and the length of the export task queue. After the export task is completed, the image file will be stored in the destination bucket. You can go to the **[Bucket List](https://console.cloud.tencent.com/cos/bucket)** page and click the ID of the destination bucket to go to the bucket details page. On the bucket details page, the image file just exported is displayed as `Custom prefix_xvda.raw`.
