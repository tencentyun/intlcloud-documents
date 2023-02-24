## Overview

A bucket tag is a key-value pair (key = value), where the tag key and tag value are connected by an equal sign (=), for example, group = IT. It can be used to manage buckets in groups. You can set, query, and delete the tags for a specified bucket via the console.

## Notes
- Each bucket can have up to 50 different bucket tags.
- `qcs:` and `project` are reserved fields. Therefore, do not use them in tag keys or tag values. For more limits, see [Bucket Tag Overview](https://cloud.tencent.com/document/product/460/79236).

## Directions

### Adding a tag when binding a bucket

You can add a bucket tag when [binding a bucket](https://intl.cloud.tencent.com/document/product/1045/33440).
![img](https://main.qcloudimg.com/raw/86b35b870b813bfbd1d80e0d897ff6bb.png)

### Adding a tag when creating a bucket

You can add a bucket tag when [creating a bucket](https://intl.cloud.tencent.com/document/product/1045/33440).
![img](https://main.qcloudimg.com/raw/e0fc632d6a18544bc261dec6a8783332.png)

### Adding a tag to a bound bucket

If you didn't add a tag when binding a bucket, you can perform the following steps to add a tag for your bucket:
1. On the [Bucket List](https://console.cloud.tencent.com/ci/bucket) page, click the name of the desired bucket to enter the bucket configuration page.
2. Click **Bucket Configuration** on the left, find the **Tagging** configuration item, and click **Add Tags**.
![img](https://qcloudimg.tencent-cloud.cn/raw/b674047d324ea8b0e85de809603bd3de.png)
3. Enter the tag key and tag value. Then, click **Save**.
