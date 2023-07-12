### Do COS APIs support the S3 protocol?

COS provides APIs that are compatible with AWS S3. For more information, please see [Accessing COS Using the AWS S3 SDK](https://intl.cloud.tencent.com/document/product/436/32537).

### What do I do if an error message such as "Request has expired" is displayed when I call an API?

There are two possible causes:
- The signature has expired when you initiate the request.
- Your local system time is out of sync with the local time in your time zone.

For the former case, you are advised to get a new valid request signature before using the API. For the latter case, you need to sync your system time with the time in your time zone.

### How do I call an API to delete an object that is not uploaded completely?

First, call the `ListMultipartUploads` API to list the multipart uploads. Then, call `Abort Multipart upload` to abort the multipart upload and delete the uploaded parts.

### What do I do if a success response is returned for the batch deletion API, while the object failed to be deleted?

Check the object path, which should not start with a `/`.



### What do I do if “NoSuchUpload” is returned for the `UploadPart` request?

If the values of `uploadId` and `partNumber` are the same, newly uploaded parts will overwrite previous ones. If `uploadId` does not exist, “404 NoSuchUpload” will be returned. For more information, please see [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750).

### How do I modify the storage class for an object using an API?

You can call the `PUT Object - Copy` API to modify `x-cos-storage-class`. For more information, please see [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881).

### How do I set the COS signature to be permanent?

A timestamp is used to determine whether the COS signature has expired and it cannot be set to permanent. If you use a permanent key to generate the signature and want the signature to be permanent, you can set the timestamp to be a long time (for example, 50 years) after the current time. If your signature is generated using a temporary key, which is valid for only up to 2 hours, your signature will also be valid for only 2 hours.

### Can I call an API to query the COS bill?

No. You can go to the console and view [Bill Details](https://console.cloud.tencent.com/expense/bill/summary). To call APIs to view the bill details, please see [DescribeBillDetail](https://intl.cloud.tencent.com/document/product/555/30756).

### Can I call an API to query the size of an object?

Yes. You can call [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) to query the size of an object.

### Can I call an API to modify the name of an object?

You can call [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) to copy the object and specify a name for the replicas.

### Can I call an API to query the bucket domain name?

You can call the [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) API to query the bucket domain name. The `x-cos-bucket-region` parameter in the response header indicates the region where the bucket resides.

### Can I call an API to query the bucket size?

COS does not provide an API to query the bucket size. You are advised to use [Cloud Monitor APIs](https://intl.cloud.tencent.com/document/product/248/37269) to query the storage by storage class, and then sum up the storage of each storage class to get the bucket size.

### How can I call APIs to query the usage details?

You can:

1. Use the [API request tool](https://console.cloud.tencent.com/api/explorer?Product=billing&Version=2018-07-09&Action=DescribeDosageCosDetailByDate&SignVersion=).

### Does COS provide APIs to operate directories?

Technically speaking, COS does not have directories or folders. In fact, folders displayed in the console are empty objects whose names end with a slash (/).

### How can I create a directory/folder using APIs?

You can call the [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) API and upload an empty object whose name ends with a slash (/).

>?COS does not have the concepts of directories or folders. To make COS more user-friendly, COS simulates folders/directories in GUIs such as the console and COSBrowser. You can create an empty object whose name ends with a slash (/), and it will be displayed as a folder.

### How can I call APIs to delete a directory/folder?

COS APIs support only deleting a single file. If you need to delete the entire directory, you can call the [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) API to obtain the list of all objects that have the same specified prefix. Then, call [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) to delete them.

### How to know on which access tier my INTELLIGENT TIERING object is stored?

You can use `x-cos-storage-tier` returned for the [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) API to query the access tier of your object.

### How can I call APIs to search for an object?

You can call [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) to determine whether the object exists. To search for a specific object, call [Get Bucket](https://intl.cloud.tencent.com/document/product/436/30614) to query all objects in the bucket and find your object.

### When I call the `GET Object` API, can I download the dynamically specified content that is returned as an attachment?

When you call `GET Object`, carry the **response-content-disposition** parameter in the URL and set its value to **attachment**. Note that this kind of `GET Object` requests require a signature carried. You can generate a signature using COS’s signature generation tool.

### What do I do if “NoSuchKey” is returned for the `putObjectCopy` request?

Check whether the file exists. If yes, the error is usually caused because the slash (/) is missing from the folder’s key. You can add the slash and then retry.

### Can I call an API to query how many times an object is requested?

 COS does not provide such an API. However, you can [Set Logging](https://intl.cloud.tencent.com/document/product/436/17040) and then obtain the requested times by analyzing the logs.



