## Overview
Versioning enables you to store multiple versions of an object in a COS bucket, and extract, delete, or restore a specific version of an object. With versioning, you can recover data that is lost due to accidental deletion or application failures. This document describes how to enable versioning for a bucket via the console. For more information about versioning, see [Versioning Overview](https://intl.cloud.tencent.com/document/product/436/19883).

>!
>- Once versioning is enabled for a bucket, it cannot return to the prior status (initial status). However, you can suspend versioning for the bucket. In this way, subsequent uploads of objects whose name already exists in the bucket will not generate multiple versions.
>- Once versioning is enabled, multiple versions will be generated for any uploaded object whose name already exists in the bucket. Each of these versions occupies your storage capacity and is billed for storage equally.
>- To permanently delete a historical version, specify an ID.
>

## Directions
1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the bucket that you want to enable versioning for.
4. Click **Fault Tolerance and Disaster Recovery** > **Versioning**, set the status to **Enable**, and click **Save**.
5. In the pop-up window, click **OK**.
To disable versioning, set the status to **Disable**.
6. If you upload an object whose name already exists to a versioning-enabled bucket, you can click **List Historical Versions** on the **File List** page to view all historical versions uploaded at different time points. You can also perform multiple operations on the latest versions, historical versions, and delete marker versions.
7. You can **restore**, **download**, **view details about**, or **delete** a historical version of an object.
>? If you need to permanently delete a historical version via the console, go to the **File List** page of the bucket, click **List Historical Versions**, and delete the desired version of an object.
>
8. If you delete objects, there will be delete records, meaning that the deleted object will be preserved. You can delete or restore specified versions of objects as needed.
![](https://main.qcloudimg.com/raw/115cf04687fb375105eddbb9bd883809.png)
