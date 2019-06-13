## FAQs About Deletion

### What should I do if buckets fail to be deleted via the console with a message "The directory is not empty" or "Please delete the valid data in the bucket"?

1. Verify whether your console version is V4 or V5. If you're using version V4, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=83&level2_id=84&source=0&data_title=%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20COS&level3_id=91&radio_title=%E6%8E%A7%E5%88%B6%E5%8F%B0%E9%97%AE%E9%A2%98&queue=28&scene_code=14471&step=2) to apply for upgrading to V5.
2. Log in to the [COS Console V5](https://console.cloud.tencent.com/cos5), go to the details page of the bucket to be deleted, and click **Incomplete Upload** to delete the file fragments.
3. Return to the **Bucket List** to delete the bucket.

## FAQs About Static Website

### I want the request result to be displayed directly in the browser without being downloaded? How do I realize this?

You can realize this by configuring the static website feature. For more information, see [Hosting Static Website](https://intl.cloud.tencent.com/document/product/436/9512).

### When accessing an object, I want the object to be displayed directly in the browser without being downloaded? How do I realize this?

You can realize this by configuring the static website feature. For more information, see [Hosting Static Website](https://intl.cloud.tencent.com/document/product/436/9512).

### What should I do if the images cannot be displayed even after I enable the static website feature?

1. If you want the objects (images) to be displayed directly when you access the COS, you need to enable the static website feature, instead of setting Content-Disposition:inline in the object headers.
2. Check browser or CDN for cached data. You can use the curl and wget commands to avoid browser caching. The cached CDN URL can be purged in the [CDN Console](https://console.cloud.tencent.com/cdn).

### Both the static website feature and the CDN acceleration are enabled, but I cannot access COS using the CDN accelerated domain name. What should I do?

COS supports HTTPS access, but CDN uses HTTP for origin-pull. Check whether the **Force HTTPS** configuration item in the static website settings is enabled. If so, disable it.

## FAQs About Cross-Origin Settings

### How do I configure the file headers in the bucket to return "Access-Control-Allow-Origin:* "?

Set Origin to `*` when configuring CORS. For more information, see [Configuring CORS](https://intl.cloud.tencent.com/document/product/436/11488).

### What should I do if the error "get ETag error, please add "ETag" to CORS ExposeHeader setting." occurs during an upload operation?

Configure the cross-origin rule as shown below and try switching browser to test if it works. For more information, see [Configuring CORS](https://intl.cloud.tencent.com/document/product/436/11488).
![](https://main.qcloudimg.com/raw/5a5ad33e9f66b2b2d11d34376ea27644.png)

### What should I do if both COS and CDN are used but COS does not work in cross-origin access?

If you're using a CDN accelerated domain name, configure CORS in the CDN Console. For more information, see [Configuring CORS](https://intl.cloud.tencent.com/document/product/228/6296#.E8.B7.A8.E5.9F.9F.E9.85.8D.E7.BD.AE).

### Is fuzzy match of Origin supported in CORS configuration?

The V5 Console (XML) supports fuzzy match of second-level domain names, and the V4 Condole (JSON) does not support second-level wildcard domain names.

## FAQs About Custom Header

### Why does the custom header Content-Disposition I set not take effect?
Any custom headers other than Content-Disposition take effect immediately after being set. Content-Disposition only takes effect after the static website feature is enabled.
If you want the file to be opened by default, instead of being downloaded, configure the static website feature. For more information, see [Configuring Static Website](https://intl.cloud.tencent.com/document/product/436/14984).

## FAQs About Origin-Pull Settings

### What does an origin server address do?

An origin server address is used for data migration. If a resource requested by the user does not exist on COS, it is pulled from the origin server address.

### If no resource or directory from the origin server address exists on the COS when I configure origin-pull, will COS automatically create the directory after I access it for the first time?

Yes. COS will automatically pull and create the directory.

## FAQs About Other Features

### Does COS support setting callbacks? For example, creating a thumbnail for each image uploaded and save it to another bucket?

You can realize this by using COS with SCF. For more information, see [Acquire Image on COS and Create a Thumbnail](https://intl.cloud.tencent.com/document/product/583/9734).

### Does COS support and provide statistics on directory size?

 COS does not provide statistics on the size and number of files under a directory. You can LIST the files under the directory to perform a traversal and generate statistics.

