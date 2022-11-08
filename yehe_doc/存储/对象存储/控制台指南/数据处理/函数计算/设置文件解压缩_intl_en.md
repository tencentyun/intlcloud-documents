## Overview

The file decompression feature is a data processing solution provided by COS based on [Serverless Cloud Function (SCF)](https://intl.cloud.tencent.com/document/product/583). When you upload a compressed file to a bucket with a ZIP decompression rule configured, the SCF function preset by COS will be triggered automatically to decompress the file into the specified bucket and directory.

![Decompression Flow](https://main.qcloudimg.com/raw/4899b5c92bb085a0f18a522dfae344ae.jpg)



## Notes

- File decompression supports decompressing ZIP files only.
- If you have added a file decompression rule to your bucket in the COS console, you can view the created decompression function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **Do not** delete the function; otherwise, your rule may not take effect.
- File decompression is supported in SCF-enabled regions, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (China), Singapore, Mumbai, Toronto, and Silicon Valley. For more supported regions, see [Serverless Cloud Function (SCF)](https://intl.cloud.tencent.com/document/product/583).
- The directory or file name in your package must be UTF-8 or GB 2312 encoded; otherwise, the directory or file name might be garbled after decompression, or the decompression may be interrupted. If an error is reported, you can click **View Log** on the right of the function to redirect to the SCF console to view log details.
- The decompression service is not supported for files stored in the ARCHIVE storage class. To decompress a package stored in the ARCHIVE storage class, restore it first. For detailed directions, see [Restoring Archived Objects](https://intl.cloud.tencent.com/document/product/436/30961).
- The maximum processing time for decompressing a compressed file is 900 seconds, beyond which the decompression task will fail. Limits of the COS file decompression feature are subject to SCF. For more limits, see [Quota Limits](https://intl.cloud.tencent.com/document/product/583/11637).
- The file decompression feature depends on the SCF service, which provides a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). Excessive usage will be billed at SCF prices. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/583/12281). For the decompression feature, the larger your package, the higher your resource usage; the more often you decompress packages, the more invocations you will need to use.

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the target bucket. 
4. Select **Function Service** on the left sidebar and click **ZIP Decompression Function**.
>! If you haven't activated SCF, go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
5. Click **Add Function** and configure the following parameters:

 - **Function Name**: It uniquely identifies a function and cannot be modified after being set. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Event Type**: An event is an operation that triggers SCF. Take upload as an example. You can initiate an upload by calling the `PUT Object` or `POST Object` API. If you select **Create using Put method** as the event type, decompression will be triggered only by a package uploaded via the `PUT Object` API.
>! If you intend to upload files to the bucket in multiple ways, such as simple upload, multipart upload, and cross-region replication, we recommend you select **File upload** as the event type.
>
 - **Trigger Condition**: The upload path that will trigger SCF. If you select **Specified prefix**, SCF will be triggered only when the package is uploaded to a path with the specified prefix. If you select **Not specifying prefix**, SCF will be triggered as long as a package is uploaded to any location of the bucket.
>! If the destination file prefix configured overlaps with the trigger condition, a loop may be triggered, which should be avoided. For example, if the destination file prefix is `prefix`, and the trigger condition is `pre`, a decompression loop will be triggered when you upload a `pref` package.
>
 - **SCF Authorization**: This authorization is required, because decompression requires you to authorize SCF to read the package from your bucket and upload the decompressed files to the specified location.
6. Click **Next** and configure the following in the pop-up window:

 - **Decompression Format**: The supported compression format, which currently can be ZIP only.
 - **Destination bucket**: The bucket to store the decompressed files.
 - **Destination path**: Decompress the matched files into this destination directory. To prevent unnecessary fees from triggering the loop, we recommend you set a destination directory different from the prefix.
 - **Extra prefix**:
    - Compressed package name: You can decompress the compressed package to the prefix named after the compressed package
    - Full path of the compressed package: You can decompress the compressed package to a prefix named after the path of the complete compressed package.
>? For example, if the compressed package is named `123.zip` and is stored in the `abc` directory, then the compressed package name is `123.zip`, and its full path is `abc/123.zip`.
>
    - None: The files in the compressed package will be directly decompressed to the destination path.
 - **Forbid recursive triggering**: Enabling this option does not continue to decompress ZIP packages that are decompressed from the package, while disabling it does.
 - **Callback URL**: Enter the callback URL as needed.
6. Click **Confirm**.
![](https://main.qcloudimg.com/raw/cb968ff99051f2eb1e515dd74000c1ee.png)
You can perform the following operations on the created function:
 - Click **Log** to view the historical running status of decompression. If an error is reported, you can click **Log** to quickly redirect to the SCF console to view its details.
 - Click **More** > **Edit** to modify the file decompression rule.
 - Click **More** > **Delete** to delete the file decompression rule.
