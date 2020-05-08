## Overview

File decompression feature is a data processing solution that Tencent Cloud COS provides based on [Serverless Cloud Function (SCF)] (https://intl.cloud.tencent.com/document/product/583). Once you configure this feature, when a compressed file is uploaded to COS, the SCF provisioned by COS will be triggered automatically to decompress the file into the specified bucket and directory.


## Description

- **DO NOT** delete the file decompression function in [SCF](https://console.cloud.tencent.com/scf/index?rid=1), or the rules you set may be invalidated.
- Decompressing ZIP packages is supported for all the regions with SCF activated, namely, ap-guangzhou, ap-shanghai, ap-beijing, ap-chengdu, ap-hongkong, ap-singapore, ap-mumbai, na-toronto, and na-siliconvalley.
- You must use only UTF-8 or GB 2312 encoding for the directory or file name in your compressed package; otherwise, it may result in a garbled file or directory name after the decompression, or an interruption during the decompression. If an error is reported, you can go to [SCF Console] (https://console.cloud.tencent.com/scf/index?rid=1) to view the error details in the running log.
- The decompression service is not supported for archived files. To decompress an archived package, please restore it first. For restoration information, see [Restoring Archived Objects] (https://intl.cloud.tencent.com/document/product/436/30961).
The maximum output time for decompressing a single compressed package is 900 seconds, beyond which the decompression task fails. This feature is subject to SCF quota limits. For more limits, see [SCF Quota Limits] (https://intl.cloud.tencent.com/document/product/583/11637).
- No file can be larger than 5 G in a compressed package; otherwise, the decompression fails.
-The decompression feature depends on the SCF service which provides users with [free tier] (https://intl.cloud.tencent.com/document/product/583/12282). You will be billed for the part exceeding the quota according to [SCF Product Pricing] (https://intl.cloud.tencent.com/document/product/583/12281). With decompression, the larger your compressed package, the more your resource usage; the more often you decompress packages, the more invocations you will need to use.

![Decompression Flow](https://main.qcloudimg.com/raw/eb066cbca365d489e335d1f53dd8c405.jpg)

## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Bucket List**, and then the bucket for which to create a decompression rule, and enter the bucket management page.
3. Click **Function Service** in the left sidebar to enter the file decompression page.
4. Click **Add File Decompression Function**, and configure the following in the pop-up window:
	-**Function Name**: the only unique identification of a function. It cannot be modified after creation.
	- **Event Type**: an event is an operation that triggers SCF. Take upload as an example. You can initiate an upload by calling the `PUT Object” or `POST Object` API. If you choose **Create using PUT method** as the event, decompression is triggered only by an upload of package via the `PUT Object` API.
	- **Trigger Condition**: indicates which directory a package should be uploaded to for triggering SCF. If you select **Specified prefix**, SCF is triggered only when the package is uploaded to a path with the specified prefix. If you choose **The whole bucket**, it is triggered when the package is uploaded to any location across the bucket.
> If the destination file prefix you configured overlaps with the trigger condition, it may cause a cyclic trigger, so please try to avoid it. For example, if the destination prefix is `prefix`, and the trigger condition is` pre`, a cyclic decompression is triggered when you upload a `pref` package.
	- **Decompression Format**: the decompression formats you are allowed to use, currently with only ZIP files supported.
	- **Destination Bucket**: the bucket where a decompressed package is stored.
	- **Destination File Prefix**: the specified directory where a decompressed package is stored; if not set, defaults to the root directory of the bucket.
	- **SCF Authorization**: this authorization is required because to decompress a compressed package, the SCF service should be authorized to read it from your bucket, and upload the uncompressed files to the location you specify.

  ![](https://main.qcloudimg.com/raw/e2fc13641b0b9250a55c63e12be9f290.png)
5. Then, you can click **View Log** to check the decompression history. To delete a file decompression rule you don’t need, you can click **Delete**.
   ![](https://main.qcloudimg.com/raw/3fecc15a6508508c8bc8e074d6b5bef4.png)
