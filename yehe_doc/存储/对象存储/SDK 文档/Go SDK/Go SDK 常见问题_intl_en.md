### How do I read all attributes of a file with Go SDK?

You can use the [GET Object](https://www.tencentcloud.com/document/product/436/43549) API to obtain file attributes from `Response.Header`.

### Does Go SDK support file stream upload?

Go SDK allows you to upload file or byte streams. For more information, see [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/44063).


### What should I do if the Go SDK reports the error "403 AccessDenied(Message: Request has expired, RequestId: xxx, TraceId: xxx)"?


If the error is caused by the expiration of the signature, simply generate a new signature. If the error persists, check whether the local time of the server is set to the local standard time.


