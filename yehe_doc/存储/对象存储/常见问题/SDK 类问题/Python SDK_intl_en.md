### What should I do if I cannot move objects after upgrading the Python SDK?

You can call the [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) and [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) APIs to move objects. We recommend you check the data consistency before deleting an object as instructed in [MD5 Verification](https://intl.cloud.tencent.com/document/product/436/32467).

### How do I get a temporary download URL with the Python SDK?

The Python SDK provides APIs for getting request signatures, pre-signed URLs, and pre-signed download URLs. The calling methods to get a pre-signed URL by using a permanent key or temporary key are the same, except that if you use a temporary key, you need to add `x-cos-security-token` to the header or `query_string`. For more information, see [Getting Pre-Signed URLs](https://intl.cloud.tencent.com/document/product/436/31548).

### What should I do if the Python SDK reports an exception?

If an XML Python SDK operation is successful, a dict or None will be returned. If an SDK API for requesting the COS service fails, the system will report a CosClientError or CosServiceError.

- CosServiceError: Errors returned due to client requests not meeting requirements, such as accessing a non-existent or unauthorized object. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- CosClientError: Network exceptions, I/O errors during file reads/writes, parameter verification failures, etc.

