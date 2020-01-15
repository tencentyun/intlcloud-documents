## FAQs About Deletion

### What should I do if a bucket fails to be deleted in the console with an error message "The directory is not empty" or "Please delete the valid data in the bucket"?
1. Log in to the [COS Console v5](https://console.cloud.tencent.com/cos5), go to the details page of the bucket to be deleted, and click **Incomplete Uploads** to delete the incomplete multipart uploads.
2. Return to the **Bucket List** and delete the bucket.

## FAQs About Static Website

### What should I do if an image cannot be displayed after I enable the static website feature?

Check the browser or CDN for cached data. You can use the curl and wget commands to avoid browser caching. If you use a CDN domain name, you can purge cache in the [CDN Console](https://console.cloud.tencent.com/cdn).

### What if I can't access the configured static website using a CDN domain name?

Check the configuration of the CDN-accelerated domain name by following the steps below.

1. Select "static website" for the origin server type.
2. Origin-pull authentication and CDN service authorization need to be set based on the bucket permission:
 - If the bucket permission is private-read, authorize the CDN service and enable origin-pull authentication.
 - If the bucket permission is public-read, there is no need to authorize the CDN service or enable origin-pull authentication.
3. CDN authentication needs to be set based on the bucket permission:

a. If the bucket permission is private-read:

| CDN Authentication | CDN-accelerated Domain Name | COS Domain Name | Common Scenario |
| ------------ | ---------------- | --------------- | ----------------------------------- |
| Disabled (default) | Accessible | COS authentication is required | Direct access to CDN domain names is allowed to protect the data on the origin server |
| Enabled | URL authentication is required | COS authentication is required | Access is protected through the linkage and hotlink protection based on CDN authentication is supported. |

b. If the bucket permission is public-read:

| CDN Authentication | CDN-accelerated Domain Name | COS Domain Name | Common Scenario |
| ------------ | ---------------- | ------------ | ---------------------------------------- |
| Disabled (default) | Accessible | Accessible | Public access to the entire website via CDN or origin server is allowed. |
| Enabled | URL authentication is required | Accessible | Hotlink protection is enabled for access via CDN but not for access via origin server (not recommended) |

4. After confirming that the above configurations are correct, check the protocol used to access the CDN-accelerated domain name and the **forced HTTPS** configuration of the static website:

   - If you are using the HTTP protocol to access the CDN-accelerated domain name, **do not enable Forced HTTPS**.
   - If you are using the HTTPS protocol to access the CDN-accelerated domain name, you are recommended to **enable Follow 301/302** in the CDN-accelerated domain name configuration. For more information, see [Follow 302 Configuration](https://intl.cloud.tencent.com/document/product/228/7183).
5. If the problem persists after all the above steps are completed, contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=83&level2_id=84&source=0&data_title=%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20COS&step=1) for further troubleshooting.

## FAQs About Cross-Origin Settings

### How do I configure the file headers in the bucket to return "Access-Control-Allow-Origin:* "?

Set the origin to `*` when configuring cross-origin access. For more information, see [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/11488).

### What should I do if the error message "get ETag error, please add "ETag" to CORS ExposeHeader setting." is displayed during an upload?

Configure the cross-origin rule as shown below and try using a different browser to test whether it works. For more information, see [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/11488).
![](https://main.qcloudimg.com/raw/1edeac65e26be225bb50328c5b6e5610.png)

### What should I do if both COS and CDN are used but cross-origin access does not work in COS?

If you're using a CDN-accelerated domain name, configure cross-origin access in the CDN Console. For more information, see [Cross-domain Configurations](https://intl.cloud.tencent.com/document/product/228/6296#.E8.B7.A8.E5.9F.9F.E9.85.8D.E7.BD.AE).

### Is fuzzy match of origin supported in the cross-origin access configuration?

The XML console v5 supports fuzzy match of second-level domain names. The JSON console v4 does not support second-level wildcard domain names.

## FAQs About Custom Headers

### Can object headers be customized in batches?

No.

## FAQs About Origin-Pull Settings

### What does an origin-pull address do?

An origin server address is used for data migration. If a requested resource does not exist in COS, it will be pulled from the origin-pull address in real time.

### If no resource or directory from the origin-pull address exists in the COS when I configure origin-pull, will COS automatically create the directory when I access it for the first time?

Yes. COS will automatically pull and create the directory.

## FAQs About Other Features

### Does COS support setting callbacks such as creating thumbnails for each image uploaded and saving them to another bucket?

You can do this by using COS together with SCF. For more information, see [Acquire Image on COS and Create a Thumbnail](https://intl.cloud.tencent.com/document/product/583/9734).

### Does COS allow me to view the size of a folder?

COS allows you to view the number and size of objects in the current folder. For more information, see [Viewing Folder Details](https://intl.cloud.tencent.com/document/product/436/31633).

