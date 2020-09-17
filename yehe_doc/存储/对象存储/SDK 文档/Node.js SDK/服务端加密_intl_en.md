
You can encrypt objects uploaded to COS in the following ways.

#### Using server-side encryption with COS-managed encryption keys (SSE-COS) to protect data

With this method, your master key and data are managed by COS. COS can automatically encrypt your data when written into the IDC and automatically decrypt it when accessed. Currently, COS supports AES-256 encryption using a COS master key pair.

In this SDK, you need to configure the encryption by passing in the `ServerSideEncryption` parameter when calling the API.

[//]: # (.cssg-snippet-put-object-sse)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    Body: 'hello!',
    ServerSideEncryption: 'AES-256',
}, function(err, data) {
    console.log(err || data);
});
```

### Using server-side encryption with customer-provided encryption keys (SSE-C) to protect data

The encryption key is provided by the customer. When you upload an object, COS will apply AES-256 encryption to your data using the customer-provided encryption key pair. In this SDK, you need to configure the encryption by passing in the `SSECustomerKey` parameter when calling the API.

> !
>- This type of encryption requires using HTTPS requests.
>- customerKey: the key provided by the user; this key should be a base64-encoded 32-byte string that contains numbers, letters, and special characters, but not Chinese characters.
>- If this encryption method was used when you uploaded a file (putObject), you should also use it when you perform such operations on this file as headObject (query), getObject (download), multipartInit (initialize multipart upload), multipartUpload (upload parts), and putObjectCopy (copy).

[//]: # (.cssg-snippet-put-object-sse-c)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',    /* Required */
    Key: 'picture.jpg',              /* Required */
    Body: 'hello!',
    SSECustomerKey: 'MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY',
}, function(err, data) {
    console.log(err || data);
});
```
