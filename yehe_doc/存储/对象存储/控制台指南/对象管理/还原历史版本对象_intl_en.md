## Overview

This document describes how to restore a historical version as the latest version via the COS console. For more information about versioning, please see [Versioning Overview](https://intl.cloud.tencent.com/document/product/436/19883).

>? 
>- Object restoration refers to restoring a historical object version as the latest one with the historical version retained.
>- To delete a historical version, please see [Setting Versioning](https://intl.cloud.tencent.com/document/product/436/19881) and [Deleting an Object](https://intl.cloud.tencent.com/document/product/436/13323).
>- Currently, you can only restore objects one by one instead of in batches.


## Instructions

The following describes the scenarios and rules for object restoration.
- Scenarios:
 - Versioning-enabled buckets support object restoration.
 - If versioning is enabled and then disabled for a bucket, object restoration is not supported.
 - Buckets that have never had versioning enabled do not support object restoration.
- Restoration rules:
	- Historical versions: can be restored
	- Latest versions: cannot be restored
	- Versions with delete markers: cannot be restored


## Prerequisites

Before you restore an object, ensure that you have enabled versioning for the bucket. If not, enable it by referring to [Setting Versioning](https://intl.cloud.tencent.com/document/product/436/19881).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket where the object resides and click the bucket name.
4. Click **File List** on the left sidebar.
5. Click **List Historical Versions**, find the object to restore, and click **Restore** in the **Operation** column.

6. In the pop-up window, check the version information of the object to restore, and click **OK**.

7. After these, you can view the restored version of the object in the file list.


