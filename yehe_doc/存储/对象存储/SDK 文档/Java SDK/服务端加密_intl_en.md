
You can encrypt objects uploaded to COS in the following ways.

#### Using server-side encryption with COS-managed encryption keys (SSE-COS) to protect data

With this method, your master key and data are managed by COS. COS can automatically encrypt your data when written into the IDC and automatically decrypt it when accessed. Currently, COS supports AES-256 encryption using a COS master key pair.

In this SDK, you need to configure the encryption by calling the `setServerSideEncryption` and `setMetadata` methods. The sample code is as follows:

[//]: # (.cssg-snippet-put-object-sse)
```java
 // Initialize user information (secretId, secretKey).
 COSCredentials cred = new BasicCOSCredentials("COS_SECRETID", "COS_SECRETKEY");
 // Set the bucket region. For the abbreviations of COS regions, see https://intl.cloud.tencent.com/document/product/436/6224
 ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
// Generate COS client
COSClient cosclient = new COSClient(cred, clientConfig);
// The bucket name must include APPID
String bucketName = "examplebucket-1250000000";

String key = "aaa/bbb.txt";
File localFile = new File("test.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
ObjectMetadata objectMetadata = new ObjectMetadata();
// Set the encryption algorithm to AES256
objectMetadata.setServerSideEncryption(SSEAlgorithm.AES256.getAlgorithm());
putObjectRequest.setMetadata(objectMetadata);
try {
    PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
    // “putobjectResult” will return Etag, an MD5 value which uniquely identifies the object, and is different from the MD5 of the object data according to the semantics of S3
    String etag = putObjectResult.getETag();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
// Shut down the client
cosclient.shutdown();
```

### Using server-side encryption with customer-provided encryption keys (SSE-C) to protect data

The encryption key is provided by the customer. When you upload an object, COS will apply AES-256 encryption to your data using the customer-provided encryption key pair. In this SDK, you need to configure the encryption by calling the `setServerSideEncryption` and `setMetadata` methods.

> !
>- This type of encryption requires using HTTPS requests.
>- base64EncodedKey: is the base64-encoded customer-provided key for server-side encryption
>- If this encryption method was used when you uploaded a file, you should also use it when you GET (download) or HEAD (query) this file.

[//]: # (.cssg-snippet-put-object-sse-c)
```java
 // Initialize user information (secretId, secretKey).
 COSCredentials cred = new BasicCOSCredentials("COS_SECRETID", "COS_SECRETKEY");
 // Set the bucket region. For the abbreviations of COS regions, see https://intl.cloud.tencent.com/document/product/436/6224.
 ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
// Require use of HTTPS
clientConfig.setHttpProtocol(HttpProtocol.https);
// Generate COS client
COSClient cosclient = new COSClient(cred, clientConfig);
// The bucket name must include APPID
String bucketName = "examplebucket-1250000000";

String key = "aaa/bbb.txt";
File localFile = new File("test.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
String base64EncodedKey = "MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=";
// “sseCustomerKey” is a base64-encoded key
SSECustomerKey sseCustomerKey = new SSECustomerKey(base64EncodedKey);
putObjectRequest.setSSECustomerKey(sseCustomerKey);
ObjectMetadata objectMetadata = cosclient.getObjectMetadata();
objectMetadata.getHttpExpiresDate();
try {
PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
// “putobjectResult” will return Etag, an MD5 value which uniquely identifies the object, and is different from the MD5 of the object data according to the semantics of S3
String etag = putObjectResult.getETag();
} catch (CosServiceException e) {
e.printStackTrace();
} catch (CosClientException e) {
e.printStackTrace();
}
// Shut down the client.
cosclient.shutdown();
```
