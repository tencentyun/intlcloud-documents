## FAQs About Deletion

### What should I do if buckets fail to be deleted via the console with a message "The directory is not empty" or "Please delete the valid data in the bucket"?

1. Verify whether your console version is V4 or V5. If you're using version V4, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=83&level2_id=84&source=0&data_title=%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20COS&level3_id=91&radio_title=%E6%8E%A7%E5%88%B6%E5%8F%B0%E9%97%AE%E9%A2%98&queue=28&scene_code=14471&step=2) to apply for upgrading to V5.
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

## FAQs About Static Website

### What should I do if the images cannot be displayed even after I enable the static website feature?

Check your browser or CDN for cached data. You can use the curl and wget commands to avoid browser caching. The cached CDN data can be purged in the [CDN Console](https://console.cloud.tencent.com/cdn) if you use a CDN domain name for access.

### What if I can't access the configured static website using a CDN domain name?

Check the configuration of the CDN-acceleration domain name by following the steps below.

1. Select "static website" for the origin server type.
2. Origin-pull authentication and CDN service authorization need to be set based on the bucket permission:
 - If the bucket permission is private-read, authorize the CDN service and enable origin-pull authentication.
 - If the bucket permission is public-read, there is no need to authorize the CDN service or enable origin-pull authentication.
3. CDN authentication needs to be set based on the bucket permission:

a. If the bucket permission is private-read:

| CDN Authentication | CDN Acceleration Domain Name | COS Domain Name | Scenarios |
| ------------ | ---------------- | --------------- | ----------------------------------- |
| Disabled (default) | Denies access | COS authentication is required | Direct access to CDN domain names is allowed to protect the data on origin server. |
| Enabled | URL authentication is required | COS authentication is required | Full stack strict SSL secured connection. Hotlink protection for CDN authentication is supported. |

b. If the bucket permission is public-read:

| CDN Authentication | CDN Acceleration Domain Name | COS Domain Name | Scenarios |
| ------------ | ---------------- | ------------ | ---------------------------------------- |
| Disabled (default) | Allows access | Allows access | Allows public access to the entire website via CDN or origin server |
| Enabled | Requires URL authentication | Allows access | Hotlink protection is enabled for access via CDN access, but not for access via origin server (not recommended) |

4. After confirming that the above configurations are correct, check the protocol used to access the CDN-acceleration domain name and the **forced HTTPS** configuration of the static website:

   - If you are using the HTTP protocol to access the CDN-acceleration domain name, **do not enable Forced HTTPS**.
   - If you are using the HTTPS protocol to access the CDN-acceleration domain name, you are recommended to **enable Follow 301/302** in the CDN-acceleration domain name configuration. For more information, see [Follow 301/302 Configuration](https://intl.cloud.tencent.com/document/product/228/7183).
5. If the problem persists after all the above steps are completed, contact us for further troubleshooting by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=83&level2_id=84&source=0&data_title=%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20COS&step=1).

## FAQs About Cross-Origin Settings

### What is cross-origin access, and how do I enable it?

Cross-origin access is to request resources over HTTP from a domain for another domain. The difference in any one of the protocol, domain name, and port will result in two different domains. For console operation steps, see [Setting Cross Origin Resource Sharing](https://intl.cloud.tencent.com/document/product/436/13318) or the Best Practice documentation [Setting Cross Origin Resource Sharing](https://intl.cloud.tencent.com/document/product/436/11488).


### How do I configure the file headers in the bucket to return "Access-Control-Allow-Origin:* "?

Set the origin to `*` when configuring CORS. For more information, see the Best Practice documentation [Setting Cross Origin Resource Sharing](https://intl.cloud.tencent.com/document/product/436/11488).

### What should I do if the error "get ETag error, please add "ETag" to CORS ExposeHeader setting." occurs during an upload operation?

Configure the CORS rule as shown below and try using a different browser to test whether it works. For more information, see [Setting Cross Origin Resource Sharing](https://intl.cloud.tencent.com/document/product/436/11488).
![](https://main.qcloudimg.com/raw/e2cb8ce626ceaba0058423bb5eb72327.png)

### What should I do if both COS and CDN are used but COS does not work in cross-origin access?

If you are using a CDN acceleration domain name, configure CORS in the CDN console. For more information, see CDN [Custom Response Header Configuration](https://intl.cloud.tencent.com/document/product/228/35320).

### Is fuzzy match of Origin supported in CORS configuration?

The V5 Console (XML) supports fuzzy match of second-level domain names, and the V4 Condole (JSON) does not support second-level wildcard domain names.

## Custom Headers

### Can object headers be customized in batches?

COS supports custom headers. For more information, see [Custom Headers](https://intl.cloud.tencent.com/document/product/436/13361).

## FAQs About Origin-Pull Settings

### What does an origin server address do?

An origin-pull address is used for data migration. If a resource requested by the user does not exist on COS, it is pulled from the origin-pull address in real time.

### If no resource or directory from the origin server address exists on the COS when I configure origin-pull, will COS automatically create the directory after I access it for the first time?

Yes. COS will automatically pull and create the directory.

## FAQs About Other Features

### Does COS support setting callbacks? For example, creating a thumbnail for each image uploaded and save it to another bucket?

You can realize this by using COS with SCF. For more information, see [Acquire Image on COS and Create a Thumbnail](https://intl.cloud.tencent.com/document/product/583/9734).

### Does COS allow me to view the size of a folder?

COS allows you to view the number and size of objects in the current folder. For more information, see [Viewing Folder Details](https://intl.cloud.tencent.com/document/product/436/31633).

### Can I set a COS object back to its last version?

Once you enable [Versioning](https://intl.cloud.tencent.com/document/product/436/19883) on your bucket, you can store multiple versions of an object in the bucket, and extract, delete or recover a specified version of the object. For detailed directions, see [Setting Versioning](https://intl.cloud.tencent.com/document/product/436/19881).

### How do I view the number of files of a certain type (e.g. image) in COS?

To do this, you can enable inventory, and check your generated inventory report. For more information, please see [Enabling Inventory](https://intl.cloud.tencent.com/document/product/436/30624).

