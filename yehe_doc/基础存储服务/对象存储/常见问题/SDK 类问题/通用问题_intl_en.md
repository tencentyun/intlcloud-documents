### What do I do if I upload a file using a file stream/handle, but the uploaded file is truncated or the size is 0?

If the file is uploaded with a file stream/handle, the stream or handle usually contains an offset pointer. If the stream/handle is used before being uploaded, the offset pointer may not point to the starting point of the file. In this case, the SDK uploads the file starting from where the offset points to by default, resulting in the truncated or 0-size file. To solve this problem, you are advised to check the offset, or point the offset to the file’s starting point manually if necessary.

### How do I get the object’s URL after it is successfully uploaded?

URLs of objects in COS are formed using a fixed format. For more information, please see [Object Overview - Object access address](https://intl.cloud.tencent.com/document/product/436/13324).


### What do I do if the system reports that the temporary key expired when I upload files?

Please follow the steps below for troubleshooting:
1. Check whether the time of the machine that runs your applications is correct. If the machine time is incorrect, rectify it.
2. Check whether the expiration time (`expirationDate`) that you set is earlier than the current time. The current time being later than the expiration time will cause the signature to expire. In that case, you need to change the expiration time and regenerate a temporary key.
3. The iOS SDK uses the `QCloudSignatureProvider` and `QCloudCredentailFenceQueueDelegate` protocols during initialization. The `QCloudCredentailFenceQueue` scaffolding tool will cache and reuse your temporary key. You can update the cache by reinitializing the `credentialFenceQueue` instance to avoid using a temporary key that has expired. For more information, see [Create a COS instance](https://intl.cloud.tencent.com/document/product/436/11280#2.-create-a-cos-instance).

### How do I determine whether files are successfully uploaded?

In COS, each object corresponds to an `ETag` value. After a file is successfully uploaded, an `ETag` value of the String type will be returned and the `ETag` value is not NULL. You can add a determination condition to determine whether files are successfully uploaded.

### How do I request an object for which hotlink protection is configured?

Add a Header with a specified referer to your request for an object.


### Does generating a pre-signed URL generate network requests and incur fees? Will there be a delay?
Generating a pre-signed URL is local logic and does not generate network requests, causing no additional network latency and no additional cost. You can call the SDK API to generate a pre-signed URL at any time when needed.

### How do I configure a custom domain name for a COS pre-signed URL?

A pre-signed URL contains a fixed default domain name, which can be replaced via encoding.

### How do I create a directory in COS SDK?

A directory in COS is virtual and is actually an object ending with `/`. You can call the object upload API to create an object ending with `/`, which is a directory. For more information, see [Mini Program SDK use case: Create a directory](https://intl.cloud.tencent.com/document/product/436/32457).

### Why are different results returned when I use the same prefix rule and data structure to obtain `ObjectList` via COS SDK?

To make it easier for you to get started, COS simulates the display mode of "folder" or "directory" in the **console and graphical tools such as COS browser**. This is realized by creating an empty object with a key value of `project/` and displaying it as a traditional folder. Therefore, the `objectList` obtained through the SDK will contain empty objects whose object names end with `/`.

