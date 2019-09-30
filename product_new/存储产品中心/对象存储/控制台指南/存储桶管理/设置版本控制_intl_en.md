## Overview
With versioning, you can store multiple versions of an object in a bucket and retrieve, delete, or restore a specified version. This can help you recover from data loss caused by accidental deletion or application failure.

>- Once versioning is enabled for the bucket, it cannot be disabled. However, you can suspend versioning to stop object versioning.
>- After versionning is enabled, newly uploaded objects will generate multiple versions and take up storage space, so these versions of the object will also charge for storage.

## Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Click the bucket to be configured to enter the bucket details page.
![](https://main.qcloudimg.com/raw/b54f229b4f6ae656b124bff914e83ae3.png)
3. Click **Advanced Configuration** on the left to enter the advanced configuration page of the bucket, scroll down to **Versioning**, and click **Edit** on the right.
![](https://main.qcloudimg.com/raw/8a7d2f60286820abce82a072291ed46e.png)
4. Click Enable in “Status” and save the change. In the pop-up window, click OK to enable versioning. When you no longer need versioning, you can simply click Disable to disable it.
![](https://main.qcloudimg.com/raw/63dc4bd4b571c2a2a79407d4ed4cdc1f.png)
