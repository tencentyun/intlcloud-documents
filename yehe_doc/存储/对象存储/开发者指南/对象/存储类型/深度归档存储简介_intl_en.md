## Overview

DEEP ARCHIVE is a COS storage class that provides long-term storage for large amounts of archival data at tape-archival-level prices. It enables you to manage your data easily with extremely low costs through the diverse set of COS APIs, SDKs, tools and console. Therefore, you do not need to consider complex on-premises tape library configuration, nor how the underlying storage media evolve.

DEEP ARCHIVE is well suited for use cases which involve extremely low access frequency, and long-term data retention. In some cases, businesses may need cold backups of daily logs in compliance with local laws and regulations, and for traceability and analysis purposes. In other cases, businesses may need long-term archival of massive media files such as images and videos that have been used in security monitoring, auto-driving, and other services. DEEP ARCHIVE allows such businesses to reduce their storage costs and operation management difficulties by restoring in-cloud data for use only when needed.

DEEP ARCHIVE is designed for 99.999999999% (11 9s) durability and 99.95% availability. You can also use versioning, cross-region replication and other COS features to further enhance your data security.

## Directions

1. Uploading through the console
   Log in to [COS console](https://console.cloud.tencent.com/cos5), click **Bucket List**, and create a bucket in one of the supported regions, for example, Beijing. Once created, click on the bucket name, select **File List** , and click **Upload Files**. Then, select a local file to upload, and set **Storage Class** to DEEP ARCHIVE in Step 2 **Set Properties**. For more information, please see [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/13321).
   ![](https://main.qcloudimg.com/raw/fd3d5c061007c71dfd382b75a9982fee.png)
2. Uploading through APIs
   In the API [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749), [POST Object](https://intl.cloud.tencent.com/document/product/436 /14690) or [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746), set the `x-cos-storage-class` to `DEEP_ARCHIVE` to upload objects directly to DEEP ARCHIVE.

>!The APPEND Object API does not support direct upload to DEEP ARCHIVE.

3. Uploading through SDKs
   Currently, all COS SDKs support direct upload to DEEP ARCHIVE by configuring `StorageClass` to `DEEP_ARCHIVE`.
4. Uploading through tools
   The COS tools, COSBrowser and COSCMD, support direct upload to DEEP ARCHIVE by adding the header `x-cos-storage-class` and setting it to `DEEP_ARCHIVE`.

## Use Limits

Please note that DEEP ARCHIVE has the following limits that may affect your storage cost and performance:

- **Minimum storage size**: 64 KB. If an object is smaller than 64 KB, you are billed for 64 KB.
- **Minimum storage duration**: 180 days. If an object is stored fewer than 180 days, you are billed for 180 days.

>?The storage days are counted with 24 hours as 1 day, starting from the time the object was modified.

- **QPS for restoration requests**: 100 requests/sec.
- **Region**: currently, DEEP ARCHIVE is only available in Beijing, Shanghai, Guangzhou, Chengdu,and Tokyo regions. Many more regions will open up in the future.
- **Use**: currently, DEEP ARCHIVE cannot be used for MAZ-enabled buckets.
- **Operation**: objects cannot be uploaded to DEEP ARCHIVE using the APPEND Object API.
- **Restore requests**: each restore request can use only one of the three restoration mode. If there are multiple restore requests sent for the same object for which a restore request is already being executed, COS will automatically choose the request with the fastest mode to execute among all of them.
