## Overview

The object tagging feature is designed to help you group and manage objects in your bucket. You can add key-value pairs for your object as its tags. An object tag is made up of a `tagKey`, `=`, and `tagValue` (for example, `group = IT`). You can set, query, and delete tags for a specified object.

>! Object tagging is a billable service. For detailed pricing, see [Product Pricing](https://intl.cloud.tencent.com/pricing/cos).

Keep the following restrictions in mind when you use object tagging:

- You can add up to 10 different tags for one object.
- A tag key cannot start with `qcs:`, `project`, or any other system reserved characters.
- Tag keys and tag values are case-sensitive. Both of them can be 1-127 UTF-8 characters in length, containing letters, spaces, digits, and special characters `+ - = . _ : / @`.

For more restrictions, see [Object Tagging Overview](https://intl.cloud.tencent.com/document/product/436/35665).

## Adding Tags When Uploading an Object

1. Add tags when [uploading an object](https://intl.cloud.tencent.com/document/product/436/13321) as shown below:
   ![](https://main.qcloudimg.com/raw/f9ed9a4b46cf8299c9f5cc2e14415765.png)
2. Your object tags will be added upon the upload success. To view them, you can go to **Object Tag** on the **Details** page of the object as follows:
   ![](https://main.qcloudimg.com/raw/b49fa4a5d1df2b40fe7caf2f5b453f9f.png)
3. To modify or delete a tag, you can click **Edit** or **Delete** on the right side of **Object Tag**.


## Adding Tags to an Uploaded Object

If you did not add tags when uploading a new object, follow the steps below to add them subsequently.

1. Go to the **Details** page of the desired object by referring to [Viewing Object Information](https://intl.cloud.tencent.com/document/product/436/13326).
2. On the **Details** page of the object, find **Object Tag** and click **Add Tags**.
   ![](https://main.qcloudimg.com/raw/d4bda3a72248e8ad7c33178e8047075b.png)
3. To modify or delete a tag, you can click **Edit** or **Delete** on the right side of **Object Tag**.

## Using Object Tags

After the object tags are set, you can set a lifecycle rule for objects with the same object key. For more information, see [Setting Lifecycle](https://intl.cloud.tencent.com/document/product/436/14605).


