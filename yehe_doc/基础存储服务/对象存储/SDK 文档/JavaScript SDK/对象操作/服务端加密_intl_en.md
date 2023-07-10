
## Overview

This document describes how to enable server-side encryption when uploading objects. There are three types of keys that can be used for server-side encryption:

* COS-managed key
* Customer-provided key
* KMS-managed key

### Using server-side encryption with COS-managed encryption keys (SSE-COS) to protect data

With this method, your master key and data are managed by COS. COS can automatically encrypt your data when written into the IDC and automatically decrypt it when accessed. Currently, COS supports AES-256 encryption using a COS master key pair.

In JavaScript SDK, you need to configure the encryption by passing in the `ServerSideEncryption` parameter when calling the API.

[//]: # (.cssg-snippet-put-object-sse)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    Body: 'hello!',
    ServerSideEncryption: 'AES256',
}, function(err, data) {
    console.log(err || data);
});
```

### Using server-side encryption with customer-provided encryption keys (SSE-C) to protect data

The encryption key is provided by the customer. When you upload an object, COS will apply AES-256 encryption to your data using the customer-provided encryption key pair. In JavaScript SDK, you need to configure the encryption by passing in the `SSECustomerKey` parameter when calling the API.

> !
>- This type of encryption requires using HTTPS requests.
>- customerKey: the key provided by the user; this key should be a base64-encoded 32-byte string that contains numbers, letters, and special characters, but not Chinese characters.
>- If this encryption method was used when you uploaded a file (putObject), you should also use it when you perform such operations on this file as headObject (query), getObject (download), multipartInit (initialize multipart upload), multipartUpload (upload parts), and putObjectCopy (copy).

[//]: # (.cssg-snippet-put-object-sse-c)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    Body: 'hello!',
    SSECustomerAlgorithm: 'AES256',
    SSECustomerKey: 'MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY',
    SSECustomerKeyMD5: 'U5L61r7jcwdNvT7frmUG8g==',
}, function(err, data) {
    console.log(err || data);
});
```


### Using server-side encryption with KMS-managed encryption keys (SSE-KMS) to protect data

SSE-KMS encryption is server-side encryption using keys managed by KMS, a Tencent Cloud security management service. KMS is designed to generate and protect your keys using third-party-certified hardware security modules (HSM). It allows you to easily create and manage keys for use in multiple applications and services, while meeting regulatory and compliance requirements. For information on how to activate KMS service, see [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).

[//]: # (.cssg-snippet-put-object-sse-kms)
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* Your bucket name. Required. */
    Region: 'COS_REGION',  /* Bucket region, such as `ap-beijing`. Required. */
    Key: '1.jpg',  /* Object key stored in the bucket (such as `1.jpg` and `a/b/test.txt`). Required. */
    Body: 'hello!',
    ServerSideEncryption: 'cos/kms',  /* Required when you upload or copy objects (including simple upload/copy and multipart upload/copy). This header cannot be specified when you download objects */
    // SSEKMSKeyId: specifies the customer master key (CMK) of KMS. If this field is not specified, the default CMK created by COS will be used. For more information, please see "SSE-KMS Encryption".
    SSEKMSKeyId: 'xxxx', /* Enter your key. Optional. */
    // SSEContext: specifies the Base64-encoded encryption context (key-value pairs in JSON format)
    SSEContext: 'eyJhIjoiYXNkZmEiLCJiIjoiMTIzMzIxIn0=', /* Specify the encryption context (Base-64 encoding required). Optional. */
}, function(err, data) {
    console.log(err || data);
});
```
