## Overview
With versioning, you can store multiple versions of an object in a bucket and retrieve, delete, or restore a specified version. This can help you recover from data loss caused by accidental deletion or application failure.

>- Once versioning is enabled for the bucket, it cannot be disabled. However, you can suspend versioning to stop object versioning.
>- After versionning is enabled, newly uploaded objects will generate multiple versions and take up storage space, so these versions of the object will also charge for storage.

## Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Click the bucket to be configured to enter the bucket details page.
3. Click **Advanced Configuration** > **Versioning**, and then click **Edit**.
![](https://main.qcloudimg.com/raw/8a7d2f60286820abce82a072291ed46e.png)
4. Toggle **Status** on, and click **Save**. In the pop-up window, click **OK**. If you don't need versioning any more, simply toggle **Status** off.
![](https://main.qcloudimg.com/raw/63dc4bd4b571c2a2a79407d4ed4cdc1f.png)
