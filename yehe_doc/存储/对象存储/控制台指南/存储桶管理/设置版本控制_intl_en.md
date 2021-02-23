## Overview
Versioning enables you to store multiple versions of an object in a COS bucket, and extract, delete, or restore a specific version of an object. With versioning, you can recover data that is lost due to accidental deletion or application failures. This document describes how to enable versioning for a bucket via the console. For more information about versioning, please see [Versioning Overview](https://intl.cloud.tencent.com/document/product/436/19883).

>!
>- Once versioning is enabled for a bucket, it cannot return to the prior status (initial status). However, you can suspend versioning for the bucket. In this way, subsequent uploads of objects whose name already exists in the bucket will not generate multiple versions.
>- Once versioning is enabled, multiple versions will be generated for any uploaded object whose name already exists in the bucket. Each of these versions occupies your storage capacity and is billed for storage equally.

## Directions
1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Click the bucket to be configured to enter the bucket details page.
3. Click **Fault Tolerance and Disaster Recovery** > **Versioning** on the left. Then, click **Edit**, enable **Status**, and click **Save**. If you no longer need to use versioning, you can disable **Status** similarly.
4. If you upload an object whose name already exists to a versioning-enabled bucket, you can click **List Historical Versions** on the **File List** page to view all historical versions uploaded at different time points. Besides, the deletion record of a deleted object can be queried. Object versions before the deletion will be retained, allowing you to delete/restore objects according to the version.
![](https://main.qcloudimg.com/raw/115cf04687fb375105eddbb9bd883809.png)
