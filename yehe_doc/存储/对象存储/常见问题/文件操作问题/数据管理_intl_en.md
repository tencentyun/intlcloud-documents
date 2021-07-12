## FAQs About Deletion

### What should I do if buckets fail to be deleted via the console with a message "The directory is not empty" or "Please delete the valid data in the bucket"?

1. Verify whether your console version is V4 or V5. If you're using version V4, [Contact Us](https://intl.cloud.tencent.com/contact-sales?lang=en&pg=) to apply for upgrading to V5.
2. Log in to the [COS Console V5](https://console.cloud.tencent.com/cos5), go to the details page of the bucket to be deleted, and click **Incomplete Upload** to delete the file fragments.
3. Return to the **Bucket List** to delete the bucket.

### Can I restore a file that has been deleted by mistake in my bucket?

Currently, files that users delete manually by mistake cannot be restored. However, you can enable versioning on your bucket to help recover future data lost due to accidental deletion or application failure. It is because versioning allows you to upload and store multiple versions of an object with the same name in your bucket, so that you can extract, delete, or restore a specified version of the object. For more information, see [Setting Versioning](https://intl.cloud.tencent.com/document/product/436/19881).

## FAQs about Incomplete Multipart Upload

### How is an incomplete multipart upload generated, and can I download parts uploaded incompletely?

An incomplete multipart upload is generated when you suspend or cancel an object upload. COS allows you to upload a large file greater than 5 GB in multiple file parts. During a multipart upload job, uploaded parts will be stored as an incomplete multipart upload and cannot be downloaded if you don’t call the Abort Multipart Upload or Complete Multipart Upload API.

### Will the uploaded parts of an incomplete multipart upload take up my storage capacity and incur fees?

Like objects, incomplete multipart uploads consume your storage capacity, and incur storage usage fees.

### How do I (regularly) clear incomplete multipart uploads?

You can delete an incomplete multipart upload directly by using the COS console. For directions, see [Deleting Incomplete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/31632). Alternatively, you can [regularly clear incomplete multipart uploads by configuring a lifecycle](https://intl.cloud.tencent.com/document/product/436/31632#.E9.85.8D.E7.BD.AE.E7.94.9F.E5.91.BD.E5.91.A8.E6.9C.9F.E5.AE.9A.E6.9C.9F.E6.B8.85.E7.90.86.E6.96.87.E4.BB.B6.E7.A2.8E.E7.89.87).

### Will clearing incomplete multipart uploads affect other complete multipart uploads?

No, it won’t. It just deletes the unsuccessful uploads.

## Custom Headers

### Can object headers be customized in batches?

COS supports custom headers. For more information, see [Custom Headers](https://intl.cloud.tencent.com/document/product/436/13361).


## FAQs About Other Features

### Does COS support setting callbacks? For example, creating a thumbnail for each image uploaded and save it to another bucket?

You can realize this by using COS with SCF. For more information, see [Acquire Image on COS and Create a Thumbnail](https://intl.cloud.tencent.com/document/product/583/9734).

### Does COS allow me to view the size of a folder?

COS allows you to view the number and size of objects in the current folder. For more information, see [Viewing Folder Details](https://intl.cloud.tencent.com/document/product/436/31633).

### Can I set a COS object back to its last version?

Once you enable [Versioning](https://intl.cloud.tencent.com/document/product/436/19883) on your bucket, you can store multiple versions of an object in the bucket, and extract, delete or recover a specified version of the object. For detailed directions, see [Setting Versioning](https://intl.cloud.tencent.com/document/product/436/19881).

### How do I view the number of files of a certain type (e.g. image) in COS?

To do this, you can enable inventory, and check your generated inventory report. For more information, please see [Enabling Inventory](https://intl.cloud.tencent.com/document/product/436/30624).

