### What should I do if errors such as "error code:-97, error message:ERROR_PROXY_AUTH_FAILED" occur when uploading files?

You can only download (rather than upload) files via custom domain names. It is recommended to avoid uploading files via custom domain names.

### When I upload a new file to the bucket in which another file with the same name exists, will the another file be overwritten or the new file be saved with a different version name?

Version control is not supported now. The another file with the same name will be overwritten.

### What is the multipart upload threshold in COS?

1 MB. For more information, see [Specifications and Limits](https://cloud.tencent.com/document/product/436/14518).

### When uploading large files using multipart upload, can I change the signature to continue the multipart upload when the signature is invalid?

Yes.

### What should I do if the error "403 Forbidden" occurs or the permission is rejected when I perform upload/download and other operations?

Troubleshoot the problems by following the steps below:

1. Check that your following configuration information is correct:
   BucketName, APPID, Region, SecretId, SecretKey, etc.
2. If the above information is correct, check whether a sub-account is used for operation. If a sub-account is used, check whether the sub-account has been authorized by the primary account. If not yet, log in using the primary account to authorize the sub-account. For more information on authorization, see [Cases of Permission Settings](https://cloud.tencent.com/document/product/436/12514).
3. If a temporary key is used for operation, check whether the current operation is in the Policy set when obtaining the temporary key. Otherwise, modify the relevant Policy settings.
4. If the problem persists after all the above steps are completed, contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=83&level2_id=84&source=0&data_title=%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20COS&step=1).
