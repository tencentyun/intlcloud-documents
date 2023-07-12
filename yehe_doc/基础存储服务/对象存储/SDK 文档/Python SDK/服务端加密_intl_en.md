
You can encrypt objects uploaded to COS in the following ways.

#### Using server-side encryption with COS-managed encryption keys (SSE-COS) to protect data

With this method, your master key and data are managed by COS. COS can automatically encrypt your data when written into the IDC and automatically decrypt it when accessed. Currently, COS supports AES-256 encryption using a COS master key pair.

In this SDK, you need to configure the encryption by calling `put_object`.

[//]: # (.cssg-snippet-put-object-sse)
```py
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'bytes'|file,
    Key='exampleobject',
    ServerSideEncryption='AES256'
)
```

### Using server-side encryption with customer-provided encryption keys (SSE-C) to protect data

With this method, the encryption key is provided by the customer. When you upload an object, COS will apply AES-256 encryption to your data using the customer-provided encryption key pair. In this SDK, you need to configure the encryption by calling the 

> !
>- This type of encryption requires using HTTPS requests.
>- customerKey: the key provided by the user; this key should be a 32-byte string that contains numbers, letters, and special characters, but not Chinese characters.
>- If this encryption method was used when you uploaded a file, you should also use it when you GET (download) or HEAD (query) this file.

[//]: # (.cssg-snippet-put-object-sse-c)
```py
response = client.put_object(
    Bucket='examplebucket-1250000000',
    Body=b'bytes'|file,
    Key='exampleobject',
    SSECustomerAlgorithm='AES256',
    SSECustomerKey='string', // A base64-encoded string of the customer-provided key
    SSECustomerKeyMD5='string' // An MD5 value of the customer-provided key
)
```
