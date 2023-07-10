## Overview

The GZIP decompression feature is a data processing solution provided by Tencent Cloud COS based on [Serverless Cloud Function (SCF)](https://intl.cloud.tencent.com/document/product/583). When you upload a compressed file to a bucket with a GZIP decompression rule configured, the SCF preset by COS will be triggered automatically to decompress the file into the specified bucket and directory.

You can use the GZIP decompression feature by the following methods:
- Console: GZIP files uploaded to the bucket will be automatically decompressed after you configure a GZIP decompression function in the console.
- API: You can call the corresponding API to trigger the GZIP decompression operation.

This document describes how to decompress GZIP files in the console. For using API to decompress GZIP files, see [Using API to Decompress GZIP Files](https://intl.cloud.tencent.com/document/product/436/46202).


## Notes

- Currently, COS can decompress .gz and .tgz files. Each file contained in the package must not be larger than 5 GB. If a single file in the package is larger than 5 GB, the decompression will fail.
- If you have added a GZIP decompression rule to your bucket via the COS console, you can view the created GZIP decompression function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default). **Do not** delete the function. Otherwise, your rule may not take effect.
- Regions where SCF is available support GZIP file decompression, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (China), Singapore, Mumbai, Toronto, and Silicon Valley. For more supported regions, see [SCF Documentation](https://intl.cloud.tencent.com/document/product/583).
- The directory or file name in your package must be UTF-8 or GB 2312 encoded. Otherwise, the directory or file name might be garbled after decompression, or the decompression may be interrupted. If an error is reported, you can click **View Log** on the right of the function to redirect to the SCF console to view log details.
- The decompression service is not supported for archived files. To decompress an archived package, please restore it first. For detailed directions, please see [Restoring Archived Objects](https://intl.cloud.tencent.com/document/product/436/30961).
- The maximum processing time for decompressing a single compressed file is 900 seconds, beyond which the decompression task fails. Limits of the COS file decompression feature are subjected to SCF. For more limits, please see [SCF Limits](https://intl.cloud.tencent.com/document/product/583/11637).
- The GZIP decompression feature depends on the SCF service which provides users with a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). You will be billed for the part exceeding the free tier according to [SCF Product Pricing](https://intl.cloud.tencent.com/document/product/583/12281). With decompression, the larger your package, the more your resource usage; the more often you decompress packages, the more invocations you will need to use.

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Choose **Bucket List** on the left sidebar.
3. Click the bucket for which you want to add a GZIP decompression rule.
4. Choose **Function Service** on the left sidebar, and click **GZIP Decompression Function**.
>! If you haven’t activated the SCF service, please go to the [SCF console](https://console.cloud.tencent.com/scf) to activate it and authorize the service as instructed.
> 
5. Click **Add Function** and configure the following parameters: 

 - **Function Name**: Uniquely identifies a function and cannot be modified after it is created. You can view the function in the [SCF console](https://console.cloud.tencent.com/scf/list?rid=1&ns=default).
 - **Event Type**: An event is an operation that triggers SCF. Take upload as an example. You can initiate an upload by calling the `PUT Object` or `POST Object` API. If you choose **Create using Put method** as the event type, decompression will be triggered only by a package uploaded via the `PUT Object` API.
>! If you intend to upload files to the bucket using multiple ways, such as simple upload, multipart upload, and cross-bucket replication, you are advised to choose **File upload** as the event type.
> 
 - **Trigger Condition**: The upload path that will trigger SCF. If you select **Specified prefix**, SCF will be triggered only when the package is uploaded to a path with the specified prefix. If you choose **Not specifying prefix**, SCF will be triggered as long as a package is uploaded to any location of the bucket.
>! If the destination prefix configured overlaps with the trigger condition, a loop may be triggered, which should be avoided. For example, if the destination prefix is `prefix`, and the trigger condition is `pre`, a decompression loop will be triggered when you upload a `pref` package.
> 
 - **SCF Authorization**: Required. To decompress a compressed file, SCF should be authorized to read the package from your bucket and upload the decompressed files to the specified location.
6. Click **Next** and configure the following in the pop-up window: 

 - **Decompression Format**: The decompression formats you are allowed to use. Currently, .gz and .tgz files are supported.
 - **Destination Bucket**: A bucket to store the compressed files
 - **Destination Path**: A path to store the compressed files of the matched packages after decompression. To prevent unnecessary fees from triggering the loop, it is recommended that you set a destination path different from the prefix.
 - **Extra prefix**:
   - Compressed package name: Decompresses the package to a directory named the same as the package itself.
   - Package directory: Decompresses the package to a directory named the same as the directory of the package.
   - Full path of compressed package: Decompresses the package to a prefix that is named the complete path of the package.
   - Empty: Decompresses the package directly to the destination path.
>? Example:
> Upload the package `123` to the `test` directory of the bucket `bucket1-125000000`, and then decompress the package to the root directory of the destination bucket `bucket2-1250000000`. If you have set one of the following extra prefixes, the storage path of the files after decompression will be as follows:
> - Compressed package name: bucket2-1250000000/123
> - Package directory: bucket2-1250000000/test
> - Full path of compressed package: bucket2-1250000000/test/123
> - Empty: bucket2-1250000000
> 
7. Click **Confirm**.

   You can perform the following operations on the created function:
 - Click **Log** to view the historical running status of the GZIP decompression. If an error is reported, you can click **Log** to quickly redirect to the SCF console to view the error log details.
 - Click **Details** to view the GZIP decompression configuration rule.
 - Click **More** > **Edit** to modify the GZIP decompression rule.
 - Click **More** > **Delete** to delete the GZIP decompression rule.
