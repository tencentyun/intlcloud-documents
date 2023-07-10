## Overview

Object tagging is designed to help you group and manage objects in your bucket by adding a key-value pair as an object tag. An object tag consists of a `tagKey`, a `=`, and a `tagValue`, such as `group = IT`. You can set, query, and delete tags on the specified object.

## Notes

- Object tagging is a paid feature. For detailed pricing, see [Pricing | Cloud Object Storage](https://intl.cloud.tencent.com/pricing/cos?lang=en&pg=).
- You can add up to ten unique tags for an object.
- Tag keys and tag values are case-sensitive. Both of them can contain 1–127 UTF-8 letters, spaces, digits, or special symbols `+ - = ._ : / @ `.
For more restrictions, see [Object Tag Overview](https://intl.cloud.tencent.com/document/product/436/35665).

## Directions

### Adding tag during object upload

1. You can add a tag when [uploading an object](https://intl.cloud.tencent.com/document/product/436/13321) as shown below:
![](https://main.qcloudimg.com/raw/f9ed9a4b46cf8299c9f5cc2e14415765.png)
2. After successful upload, the object tag will be added.
You can go to the **File List** page of the bucket, find the tagged object, and click **More** > **Add Tags** to view, edit, or delete the added tag.
![](https://main.qcloudimg.com/raw/b49fa4a5d1df2b40fe7caf2f5b453f9f.png)


### Adding tag uploaded object

If you did not add tags when uploading a new object, follow the steps below to add them subsequently.

1. Go to the **File List** page as instructed in [Viewing Object Information](https://intl.cloud.tencent.com/document/product/436/13326).
2. Find the target object and click **More** > **Add Tags**.
3. In the pop-up window, click **Add Tags**, enter the tag key and value, and save.

To modify or delete the tag, click **Edit** or **Delete** in this window.

## Related Operations

### Using object tag

After the object tag is set, you can set a lifecycle rule for objects with the same object tag. For more information, see [Setting Lifecycle](https://intl.cloud.tencent.com/document/product/436/14605).


