## Overview
COS supports direct upload to COS archive storage using the console, APIs, SDK, or COSCMD. Alternatively, you can use the lifecycle feature of COS to transition your objects to the ARCHIVE or DEEP ARCHIVE storage class. For more information about archive, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).


## Supported Methods

- Uploading via the console
 In the [COS console](https://console.cloud.tencent.com/cos5), click **Upload Files** and then select the object to upload. In the **Set Properties** step, set **Storage Class** to **ARCHIVE** or **DEEP ARCHIVE**. For more information, please see [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/13321).
![](https://main.qcloudimg.com/raw/8f3b05d1407a9017c54c86c9cec693c7.png)

- Uploading via APIs
You can set `x-cos-storage-class` to `ARCHIVE` or `DEEP_ARCHIVE` in the `PUT Object`, `POST Object`, or `Initiate Multipart Upload` API to implement direct upload to COS ARCHIVE storage.
>! The `Append Object` API does not support direct upload to COS ARCHIVE storage.
>

- Uploading via SDKs
Currently, all COS SDKs support direct upload to COS ARCHIVE storage. You can set `StorageClass` to `ARCHIVE` or `DEEP_ARCHIVE` during the upload.

- Uploading via COSCMD
You can add the header field `x-cos-storage-class` and set it to `ARCHIVE` or `DEEP_ARCHIVE` during the upload.

#### Restoring and downloading archived data
Unlike STANDARD/STANDARD_IA, objects in ARCHIVED or DEEP ARCHIVED can only be downloaded after being restored. The following 3 restoration modes are provided:
- Expedited mode: restores an object within 1-5 minutes (fastest).
- Standard mode: restores an object within 3-5 hours.
- Bulk mode: restores multiple objects within 5-12 hours (lowest cost)

>?Objects in DEEP ARCHIVE cannot be restored using the expedited mode. The object can be restored within 12-24 hours using standard mode, and 24-48 hours using bulk mode.

Note that the console, APIs, SDKs, and COSCMD all support the restoration and download for archived objects.

#### Restrictions
- Objects in ARCHIVE or DEEP ARCHIVE need to be restored before being downloaded.
- To copy an object in ARCHIVE or DEEP ARCHIVE, you need to restore it first.
- Objects in ARCHIVE and DEEP ARCHIVE do not support cross-bucket replication.
- Objects in ARCHIVE and DEEP ARCHIVE cannot be changed to a storage class that is more frequently accessed, such as STANDARD and STANDARD_IA.

