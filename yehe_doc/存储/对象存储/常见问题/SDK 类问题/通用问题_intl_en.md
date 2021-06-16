### What do I do if I upload a file using a file stream/handle, but the uploaded file is truncated or the size is 0?

If the file is uploaded with a file stream/handle, the stream or handle usually contains an offset pointer. If the stream/handle is used before being uploaded, the offset pointer may not point to the starting point of the file. In this case, the SDK uploads the file starting from where the offset points to by default, resulting in the truncated or 0-size file. To solve this problem, you are advised to check the offset, or point the offset to the file’s starting point manually if necessary.

### How do I get the object’s URL after it is successfully uploaded?

URLs of objects in COS are formed using a fixed format. For more information, please see [Object Overview - Object access address](https://intl.cloud.tencent.com/document/product/436/13324).
