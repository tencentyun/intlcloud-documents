### What should I do if a CORS error is reported?

The error is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/47bdd8a90f724d577a60f7b8dcb894e4.png)
The reason is that CORS is not correctly set for the bucket. For more information, see [Setting CORS](https://intl.cloud.tencent.com/document/product/436/11488).

### What should I do if error 403 is reported when I perform operations with a temporary key?

Check whether the `action` and `allowPrefix` you entered when applying for the temporary key are correct.

1. For example, if you call `cos.putObject()`, but the `action` does not contain **name/cos:PutObject**, then there is no `putObject` permission, resulting in the error 403.
2. For example, if the key for the operation is `1.jpg`, but the `allowPrefix` is entered as `test/*` (only allowing operations on the `test/*` path), then there is no operation permission for the corresponding path, resulting in the error 403.

If both `action` and `allowPrefix` are correct, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048) and [403 Error for COS Access](https://intl.cloud.tencent.com/document/product/436/40105).
Field description: STS SDKs for different languages use different fields for `action` and `allowPrefix`, such as `allowActions` and `allowPrefixes` in the STS Java SDK. Be sure to check the examples in the STS SDK.

### What should I do if the JavaScript SDK reports the error "Request has expired (Status Code: 403; Error Code: AccessDenied)"?

If the error is caused by the expiration of the signature, simply generate a new signature. If the error persists, check whether the local time of the server is the same as the standard local time.

### What should I do if multipart upload through the JavaScript SDK is only successfully the first time, but error 403 is returned in subsequent upload requests?

You can troubleshoot the problem by referring to [403 Error for COS Access](https://intl.cloud.tencent.com/document/product/436/40105). If you use a temporary key for multipart upload, check whether you have the multipart upload permission as described in [Working with COS API Authorization Policies](https://intl.cloud.tencent.com/document/product/436/30580) and whether the authorized path is correct.

### What should I do if the JavaScript SDK upload speed does not reach the full bandwidth?

You can use the multipart upload API and increase the size of each part. For example, if the current part size is 1 MB, you can try to adjust it to 5 MB and then observe the bandwidth usage. For more information, see [Uploading Object](https://intl.cloud.tencent.com/document/product/436/43861).

### How can I use the JavaScript SDK to obtain the upload progress?

The simple upload API and multipart upload API of the JavaScript SDK can return the upload progress. For more information, see [Uploading Object](https://intl.cloud.tencent.com/document/product/436/43861).

### Can I obtain the progress directly using the List Multipart Uploads API of the JavaScript SDK?

Currently, the `List Multipart Uploads` API needs to use a callback function. Therefore, you cannot obtain the progress directly.
