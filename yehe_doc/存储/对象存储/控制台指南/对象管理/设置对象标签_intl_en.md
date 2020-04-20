## Overview

Object tagging feature is designed to help you group and manage objects in your bucket by adding a key-value pair as object identifier. An object tag consists of a `tagKey`, a `=`, and a `tagValue`, such as `group = IT`. You can set, query and delete tags on the specified object.

> You will be billed for using this feature. For more information on its pricing, see [Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239).

To use object tagging feature, note the following restrictions:

- You can add up to 10 different tags for one object.
- A tag key cannot start with `qcs:`, `project`, or any other system reserved characters.
- The tag key and tag values are case-sensitive. Both of them can be 1-127 characters encoded in UTF-8, containing letters, spaces, numbers, and special characters `+, -, =, ., _, :, /, @`.

For more information, see [Object Tagging Overview](https://intl.cloud.tencent.com/document/product/436/35665).

## Adding Tags when Uploading an Object

1. You can add tags when [uploading an object](https://intl.cloud.tencent.com/document/product/436/13321) as shown below:
   ![](https://main.qcloudimg.com/raw/f9ed9a4b46cf8299c9f5cc2e14415765.png)
2. Once the upload succeeds, your object tags will be added instantly. To view them, you can go to **Object Tag** in the object details page:
   ![](https://main.qcloudimg.com/raw/b49fa4a5d1df2b40fe7caf2f5b453f9f.png)
3. To modify or delete a tag, you can click **Edit** or **Delete** on the right side of **Object Tag**.


## Adding Tags to an Uploaded Object

If you did not add tags when uploading a new object, you can follow the steps below to add them subsequently.

1. Enter the details page of the object you want to add tags to. See [Viewing Object Information](https://intl.cloud.tencent.com/document/product/436/13326).
2. In the object details page, find **Object Tag**, and click **Add Tags**.
   ![Adding tags to an existing object](https://main.qcloudimg.com/raw/d4bda3a72248e8ad7c33178e8047075b.png)
3. To modify or delete a tag, you can click **Edit** or **Delete** on the right side of **Object Tags Management**.
