## Overview

File decompression is a data processing solution provided by Tencent Cloud COS based on the [Serverless Cloud Function (SCF)](https://intl.cloud.tencent.com/document/product/583). Once you configure a decompression rule, when a compressed file is uploaded to COS, the SCF provisioned by COS will be triggered automatically to decompress the file into the specified bucket and directory, as shown below:

![Decompression Flow](https://main.qcloudimg.com/raw/4899b5c92bb085a0f18a522dfae344ae.jpg)

>! Currently, COS can decompress only ZIP files, and each file contained in the ZIP file must not exceed 5 GB.

## Notes

- If you add a file decompression rule to your bucket on the COS Console, a new file decompression function will appear in the [SCF Console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete this function. Otherwise, your rule may be invalid.
- The regions where SCF has been available all support ZIP file decompression, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong, Singapore, Mumbai, Toronto, and Silicon Valley. For more supported regions, see the [SCF Documentation](https://intl.cloud.tencent.com/document/product/583).
- The directory or file name in your compressed file must be UTF-8 or GB 2312 encoded. Otherwise, it may result in a garbled file name or directory name, or decompression interruption. If an error is reported, you can view it in your log by clicking **View Log** on the right of the function to open the SCF Console.
- The decompression service is not supported for archived files. To decompress an archived package, please restore it first. For restoration information, see [Restoring Archived Objects](https://intl.cloud.tencent.com/document/product/436/30961).
The maximum processing time for decompressing a single compressed package is 900 seconds, beyond which the decompression task will fail. This feature has limits subject to SCF. For more limits, see [SCF Quota Limits](https://intl.cloud.tencent.com/document/product/583/11637).
- No file can be larger than 5 G in a compressed package; otherwise, the decompression fails.
- The decompression feature depends on the SCF service which provides users with a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). You will be billed for the part exceeding the free tier according to [SCF Product Pricing](https://intl.cloud.tencent.com/document/product/583/12281). With decompression, the larger your compressed package, the more your resource usage; the more often you decompress packages, the more invocations you will need to use.



## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Bucket List**, and then the bucket to which you want to add a file decompression rule to open the bucket management page.
3. Click **Function Service**, and find the **ZIP File Decompression Function** section.
> !If you haven’t activated SCF, you can do so by using the [SCF Console](https://console.cloud.tencent.com/scf), and then enabling SCF service authorization as instructed.
4. Click **Add Function**, and configure the following in the pop-up window:
   - **Function Name**: uniquely identifies a function, and cannot be modified after creation. You can view the function on the [SCF](https://console.cloud.tencent.com/scf/list?rid=1&ns=default) console.
   - **Event Type**: an event is an operation that triggers SCF. Take upload as an example. You can initiate an upload by calling the `PUT Object” or `POST Object` API. If you choose **Create using PUT method** as the event, decompression is triggered only by a package uploaded via the `PUT Object` API.
> !If your file is to be uploaded using simple upload, multipart upload or cross-region replication, we recommend selecting **File upload** as the Event Type.
 - **Trigger Condition**: indicates which path a package should be uploaded to for triggering SCF. If you select **Specified prefix**, SCF is triggered only when the package is uploaded to a path with the specified prefix. If you choose **The whole bucket**, it is triggered when the package is uploaded to any location across the bucket.
    !If the destination file prefix you configured overlaps with the trigger condition, it may cause a cyclic trigger, so please try to avoid it. For example, if the destination prefix is `prefix`, and the trigger condition is` pre`, a cyclic decompression is triggered when you upload a `pref` package.
 - **Decompression Format**: the decompression formats you are allowed to use; currently, only ZIP files are supported.
 - **Destination Bucket**: the bucket where a decompressed package is stored.
 - **Destination File Prefix**: the specified path where a decompressed package is stored; if not set, defaults to the root directory of the bucket.
 - **SCF Authorization**: this authorization is required because to decompress a compressed package, the SCF service should be authorized to read it from your bucket, and upload the uncompressed files to the location you specify.
 ![](https://main.qcloudimg.com/raw/33a0d8b1ded5fbc19342bf63f9df4827.png)
5. Once completed, click **OK**, and you can see that the function has been added. The **View Log** option allows you to view your decompression history, and also go to the SCF console to view your decompression error logs. To delete an unwanted function, simply click **Delete**.
   ![](https://main.qcloudimg.com/raw/cb968ff99051f2eb1e515dd74000c1ee.png)
