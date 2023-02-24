## Overview

A bucket tag is a key-value pair (key = value), where the tag key and tag value are connected by an equal sign (=), for example, group = IT. It can be used to manage buckets in groups. You can set, query, and delete the tags for a specified bucket via the console.

## Notes
- Each bucket can have up to 50 different bucket tags.
- `qcs:` and `project` are reserved fields. Therefore, do not use them in tag keys or tag values. For more limits, see [Bucket Tag Overview](https://www.tencentcloud.com/document/product/1045/53780).

## Directions

### Adding a tag when binding a bucket

You can add a bucket tag when [binding a bucket](https://intl.cloud.tencent.com/document/product/1045/33440).


### Adding a tag when creating a bucket

You can add a bucket tag when [creating a bucket](https://intl.cloud.tencent.com/document/product/1045/33440).


### Adding a tag to a bound bucket

If you didn't add a tag when binding a bucket, you can perform the following steps to add a tag for your bucket:
1. On the [Bucket List](https://console.cloud.tencent.com/ci/bucket) page, click the name of the desired bucket to enter the bucket configuration page.
2. Click **Bucket Configuration** on the left, find the **Tagging** configuration item, and click **Add Tags**.

3. Enter the tag key and tag value. Then, click **Save**.
