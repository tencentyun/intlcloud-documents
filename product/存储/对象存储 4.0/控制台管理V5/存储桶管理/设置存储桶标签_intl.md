## Overview

A bucket tag is a key-value pair (key = value) consisting of the tag's key, value, and =, such as group = IT. It can be used as an identifier for easier bucket grouping and management. Tags for the specified bucket can be set, queried, and deleted in the console.


## Steps


>- Up to 10 tags can be added to one bucket, and the tag keys cannot be the same.
>- Tag keys and values cannot contain reserved words such as `qcs:` and `project`. For more information about restrictions, see [Bucket Tag Overview](https://intl.cloud.tencent.com/zh/document/product/436/31509).

### Adding a Tag When Creating a Bucket

You can add a bucket tag when [creating a bucket](https://intl.cloud.tencent.com/document/product/436/13309), as shown in the figure below:
![](https://main.qcloudimg.com/raw/54e8243d1ca6ca919c48d3088b452a7c.png)

### Adding a Tag to an Existing Bucket

If you do not add a tag when creating a bucket, you can follow the steps below to add one subsequently.
1. On the [Bucket List](https://console.cloud.tencent.com/cos5/bucket) page, click the name of the bucket to which to add a tag to enter the bucket configuration page.
2. Click **Basic Configuration**, scroll down to find the **Tag Management** configuration item, and add the bucket tag. See the figure below:
![](https://main.qcloudimg.com/raw/5940ce69cbadf6e26f1de32b6d8c8b4a.png)
