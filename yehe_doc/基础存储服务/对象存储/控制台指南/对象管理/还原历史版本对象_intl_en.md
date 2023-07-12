## Overview

This document describes how to restore a historical object version as the latest version in the COS console. For more information on versioning, see [Overview](https://intl.cloud.tencent.com/document/product/436/19883).

>? 
>- Object restoration refers to restoring a historical object version as the latest one with the historical version retained.
>- To delete a historical version, see [Setting Versioning](https://intl.cloud.tencent.com/document/product/436/19881) and [Deleting Objects](https://intl.cloud.tencent.com/document/product/436/13323).
>- Currently, you can only restore objects one by one instead of in batches.
>


## Notes

The following describes the scenarios and rules for object restoration.

<table>
	<tr><th>Scenarios</th><td><ul  style="margin: 0;"><li>A bucket with versioning enabled supports object restoration. </li><li>A bucket with versioning enabled and then suspended supports object restoration. </li><li>A bucket with versioning never enabled does not support object restoration. </li></ul></td></tr>
	<tr><th>Restorage rules</th><td><ul  style="margin: 0;"><li>Historical versions can be restored. </li><li>The latest version cannot be restored. </li><li>Versions with delete markers cannot be restored. </li></ul></td></tr>
</table>


## Prerequisites

Before you restore an object, ensure that you have enabled versioning for the bucket. If not, enable it by referring to [Setting Versioning](https://intl.cloud.tencent.com/document/product/436/19881).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket where the object resides and click the bucket name.
4. Click **File List** on the left sidebar.
5. Click **List Historical Versions**, find the object to restore, and click **Restore** in the **Operation** column on the right.

6. In the pop-up window, check the information of the object version to be restored and click **OK**.

7. View the restored version of the object in the file list.


