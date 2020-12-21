### What do I do if an error message such as "Request has expired" is displayed when I call an API?

There are two possible causes:
- The signature has expired when you initiate the request.
- Your local system time is out of sync with the local time in your time zone.

For the former case, you are advised to get a new valid request signature before using the API. For the latter case, you need to sync your system time with the time in your time zone.

### How do I call an API to delete an object that is not uploaded completely?

First, call the `ListMultipartUploads` API to list the multipart uploads. Then, call `Abort Multipart upload` to abort the multipart upload and delete the uploaded parts.

### What do I do if a success response is returned for the batch deletion API, while the object failed to be deleted?

Check the object path, which should not start with a `/`.


### How do I modify the storage class for an object using an API?

You can call the `PUT Object - Copy` API to modify `x-cos-storage-class`. For more information, please see [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881).

### How do I set the COS signature to be permanent?

A timestamp is used to determine whether the COS signature has expired and it cannot be set to permanent. If you use a permanent key to generate the signature and want the signature to be permanent, you can set the timestamp to be a long time (for example, 50 years) after the current time. If your signature is generated using a temporary key, which is valid for only up to 2 hours, your signature will also be valid for only 2 hours.