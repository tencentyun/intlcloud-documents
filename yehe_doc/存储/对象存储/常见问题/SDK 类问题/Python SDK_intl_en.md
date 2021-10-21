### What should I do if I cannot move objects after upgrading the Python SDK?

You can call [PUT Object](https://intl.cloud.tencent.com/document/product/436/10881) and [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) to move objects. You are advised to check the data consistency before deleting an object. For more information, please see [MD5 Verification](https://intl.cloud.tencent.com/document/product/436/32467).

### How can I obtain a temporary download URL with the Python SDK?

The Python SDK provides APIs to obtain requests, pre-signed URLs, and pre-signed download URLs. The calling method to obtain a pre-signed URL using a permanent key or temporary key is the same, except that if you use a temporary key, you need to add `x-cos-security-token` to the header or `query_string`. For more information, please see [Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/31548).

### What should I do if the Python SDK throws an exception?

If an XML Python SDK operation is successful, a dict or None will be returned. If you failed to request a COS service using an SDK API, the system will throw `CosClientError` or `CosServiceError`.

- CosServiceError: errors returned due to client requests not meeting the requirements, such as accessing an object that does not exist or accessing an object that the user is not authorized. For more information about the error codes returned by the server, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- CosClientError: network errors, I/O errors during file reads/writes, parameter verification failures, etc.

