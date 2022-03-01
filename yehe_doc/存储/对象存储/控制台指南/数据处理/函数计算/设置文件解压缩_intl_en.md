## Overview

File decompression is a data processing solution provided by Tencent Cloud COS based on [Serverless Cloud Function (SCF)](https://intl.cloud.tencent.com/document/product/583). When you upload a compressed file to a bucket with a decompression rule configured, the SCF preset by COS will be triggered automatically to decompress the file into the specified bucket and directory. The decompression flow is shown as follows:

![Decompression Flow](https://main.qcloudimg.com/raw/4899b5c92bb085a0f18a522dfae344ae.jpg)


## Notes

- Only ZIP file decompression is supported.
- If you have added a file decompression rule to your bucket in the COS console, a file decompression function will appear in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **DO NOT** delete this function. Otherwise, your rule may not take effect.
- Regions where SCF is available support ZIP file decompression, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (China), Singapore, Mumbai, Toronto, and Silicon Valley, and more. For more supported regions, please see [SCF Documentation](https://intl.cloud.tencent.com/document/product/583).
- The directory or file name in your compressed file must be UTF-8 or GB 2312 encoded. Otherwise, the directory or file name might be garbled, or the decompression might be interrupted. If an error is reported, you can click **View Log** on the right of the function to redirect to the SCF console for viewing the log details.
- The decompression service is not supported for archived files. To decompress an archived package, please restore it first. For detailed directions, please see [Restoring Archived Objects](https://intl.cloud.tencent.com/document/product/436/30961).
- The maximum processing time for decompressing a single compressed file is 900 seconds, beyond which the decompression task fails. Limits of the COS file decompression feature are subjected to SCF. For more limits, please see [SCF Limits](https://intl.cloud.tencent.com/document/product/583/11637).
- The decompression feature depends on the SCF service, which provides users with a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). You will be billed for the part exceeding the free tier according to [SCF Product Pricing](https://intl.cloud.tencent.com/document/product/583/12280). Note that the larger your compressed file, the more resources will be used; the more often you decompress your packages, the more calling times will be incurred.

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** in the left sidebar.
3. Click the bucket you want to add a decompression rule for. 
4. Choose **Function Service** on the left sidebar, and click **ZIP Decompression Function**.
>! If you haven’t activated SCF, please go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
5. Click **Add Function**, and configure the following in the pop-up window:

 - **Function Name**: uniquely identifies a function and cannot be modified after it is created. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Event Type**: an operation that triggers SCF. Take upload as an example. You can initiate an upload by calling the `PUT Object` or `POST Object` API. If you choose **Create using PUT method** as the event type, decompression will only be triggered by a package uploaded via the `PUT Object` API.
>! If you intend to upload files to the bucket using multiple ways, such as simple upload, multipart upload, and cross-bucket replication, you are advised to choose **File upload** as the event type.
>
 - **Trigger Condition**: the upload path that will trigger SCF. If you select **Specified prefix**, SCF will be triggered only when the package is uploaded to a path with the specified prefix. If you choose **Not specifying prefix**, SCF will be triggered as long as a package is uploaded to any location of the bucket.
>! If the destination prefix you configured overlaps with the trigger condition, a loop may be triggered, which should be avoided. For example, if the destination prefix is `prefix`, and the trigger condition is` pre`, a decompression loop will be triggered when you upload a `pref` package.
>
 - **SCF Authorization**: Required. To decompress a compressed file, SCF should be authorized to read the package from your bucket and upload the decompressed files to the specified location.
5. Click **Next** and perform configuration in the pop-up window, as shown below:

 - **Decompression Format**: the decompression formats you are allowed to use. Currently, only ZIP files are supported.
 - **Destination Bucket**: a bucket to store the compressed files
 - **Destination Path**: a path to store the decompressed files of the packages that are matched. To prevent unnecessary fees from triggering the loop, it is recommended that you set a destination path different from the prefix.
 - **Extra Prefix**:
    - Compressed package name: decompresses the package to a prefix that is named the same as the package itself.
    - Full path of the compressed package: decompresses the package to a prefix that is named the complete path of the package.
>?For example, if a compressed package named `123.zip` is stored in the `abc` directory, the compressed package name is `123.zip`, and the full path of the compressed package is `abc/123.zip`.

    - Empty: decompresses the package directly to the destination path.
 - **Forbid Recursive Triggering**: **Enable** does not continue to decompress ZIP packages that are decompressed from the package, while **Disable** does.
6. Click **Confirm**.
![](https://main.qcloudimg.com/raw/cb968ff99051f2eb1e515dd74000c1ee.png)
You can perform the following operations on the created function:
 - Click **View Logs** to view the historical running status of the decompression. If an error is reported, you can click **View Logs** to quickly redirect to the SCF console for viewing the error log details.
 - Click **Edit** to modify the file decompression rule.
 - Click **Delete** to delete the unwanted file decompression rule.
