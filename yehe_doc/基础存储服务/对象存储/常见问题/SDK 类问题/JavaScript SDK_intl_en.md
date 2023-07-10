### What should I do if multipart upload using the JavaScript SDK is only successfully the first time, but 403 are returned in subsequent upload requests?

You can troubleshoot by referring to [A 403 Status Code is Returned When You Access COS](https://intl.cloud.tencent.com/document/product/436/40105). If you use a temporary key for multipart upload, check whether you have the [multipart upload permission](https://intl.cloud.tencent.com/document/product/436/30580) and whether the authorized path is correct.

### What should I do if the JavaScript SDK upload speed does not reach the full bandwidth?

You can use the multipart upload API and increase the size of each part. For example, if the current part size is 1 MB, you can try to adjust it to 5 MB or other sizes, and then see how the bandwidth has been using. For more information, please see [Multipart Operations](https://intl.cloud.tencent.com/document/product/436/31538).

### How can I use the JavaScript SDK to obtain the upload progress?

The simple upload API and multipart upload API of the JavaScript SDK can return the upload progress. For more information, please see [Object Operations](https://intl.cloud.tencent.com/document/product/436/31538).

### Can I obtain the progress directly using the List Multipart Uploads API of the JavaScript SDK?

Currently, the `List Multipart Uploads` API needs to use a callback function. Therefore, you cannot obtain the progress directly.

