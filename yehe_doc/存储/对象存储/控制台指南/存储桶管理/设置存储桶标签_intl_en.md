## Overview

A bucket tag is a key-value pair (key = value), where the tag key and tag value are connected by an equal sign (=), for example, group = IT. It can be used to manage buckets in groups. You can set, query, and delete the tags for a specified bucket via the console.



## Adding a Tag When Creating a Bucket

You can add a bucket tag when [creating a bucket](https://intl.cloud.tencent.com/document/product/436/13309), as shown in the following figure:
![](https://qcloudimg.tencent-cloud.cn/raw/02d9832d2244e4010d67dc49dee490bf.png)

## Adding a Tag to an Existing Bucket

If you didn’t add a tag when creating a bucket, you can perform the following steps to add a tag for your bucket:

1. On the [Bucket List](https://console.cloud.tencent.com/cos5/bucket) page, click the name of the desired bucket to enter the bucket configuration page.
2. Click **Basic Configurations** on the left, find the **Tagging** configuration item, and click **Add Tags**.
![](https://qcloudimg.tencent-cloud.cn/raw/ad3d20fe1e2738de4bb326a8b51b8b36.png)
The configuration items are described as follows:
 - Tag key: It is case-sensitive and can contain uppercase/lowercase letters, digits, and symbols (+, -, _, =, /, ., :, @).
 - Tag value: It is case-sensitive and can contain uppercase/lowercase letters, digits, and symbols (+, -, _, =, /, ., :, @).
>!
>- Each bucket can have up to 50 different bucket tags.
>- `qcs:` and `project` are reserved fields. Therefore, do not use them in tag keys or tag values. For more limits, see [Bucket Tag Overview](https://intl.cloud.tencent.com/document/product/436/31509).
>
3. Enter the tag key and tag value. Then, click **Save**.
