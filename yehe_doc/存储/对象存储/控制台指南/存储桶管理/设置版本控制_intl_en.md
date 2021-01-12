## Overview
Versioning enables you to store multiple versions of an object in a COS bucket, and also retrieve, delete, or restore a specific version of an object. This helps to recover data lost due to accidental deletion or application failures. This document describes how to enable versioning for a bucket in the console. For more information on versioning, please see [Versioning Overview](https://intl.cloud.tencent.com/document/product/436/19883).

>- Once versioning is enabled for the bucket, it cannot be disabled. However, you can suspend versioning to stop object versioning.
>- After versionning is enabled, newly uploaded objects will generate multiple versions and take up storage space, so these versions of the object will also charge for storage.

## Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Click the bucket to be configured to enter the bucket details page.
3. Under **Fault and disaster tolerance management** > **Versioning**, click **Edit**, toggle **Status** on, and click **Save**. In the pop-up window, click **OK** to enable versioning. To disable it as needed, simply set **Status** to off.
![](https://main.qcloudimg.com/raw/63dc4bd4b571c2a2a79407d4ed4cdc1f.png)
4. Once versioning is enabled, you can click **Display** at the top of **File List** window to display all object versions. If you upload objects that already exist, they will all be displayed as different versions with specific datetime under the same name. If you delete an object in **Hide** mode, you can still find it in addition to a new delete marker in **Display** mode. In this way, COS allows you to delete or retrieve different versions of an object.
![](https://main.qcloudimg.com/raw/1d63352df91ebf844c60bbe085724ae6.png)
