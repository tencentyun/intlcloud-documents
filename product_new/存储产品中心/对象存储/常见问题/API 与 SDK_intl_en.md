## FAQs About APIs and Other SDKs

### What if an error message such as "Time out" is displayed when I call an API?

There are two possible reasons for this:
- The signature has expired when you initiate the request.
- Your system time is different from the local time.

In the former case, you are advised to get a new valid request signature before using the API, while in the latter case, you need to correct your system time according to the local time.

### How do I call an API to delete partially uploaded files?

First, call the ListMultipartUploads API to list the partially uploaded files. Then, call the Abort Multipart upload API to abort the multipart upload and delete parts that are already uploaded.

### What should I do if it returns correctly after calling the batch deletion API but in fact the file deletion failed?

Check the deleted file path, which should not begin with a `/`.

### How do I get a temporary download URL in the SDK for Python?

For more information, see [Pre-signed URL](https://intl.cloud.tencent.com/document/product/436/31548).

### Can I access the SDK with a CDN-accelerated domain name?

Yes. See the [SDK documentation](https://cloud.tencent.com/document/sdk) for your programming language.

## FAQs About the SDK for WeChat Mini Program

### How do I configure and limit the whitelist if multiple domain names are requested in the WeChat Mini Program or the bucket name is unknown?

When you instantiate the SDK, enable the suffix using `ForcePathStyle:true`. If you make a suffixed request in a URL format like `https://cos-ap-beijing.myqcloud.com/<BucketName-APPID>/<Key>`, the bucket name `/<BucketName-APPID>` will also be included in the signature calculation.

### How to save an image in the WeChat Mini Program to the device?

The image URL can be obtained using `cos.getObjectUrl` first. Then, the `wx.downloadFile` API can be called to download the image and obtain the temporary path. When the "Save Image" button appears and the user taps it, the `wx.saveImageToPhotosAlbum` API will be called to save the image to the album on the device.

## FAQs About SDK for Java

### Why does java.lang.NoSuchMethodError appear when I run the SDK?

Typically, it is because a JAR package conflict has occurred: for example, if the JAR package in the HttpClient library in your project does not have method A, but the JAR package that the SDK relies on uses method A, then the HttpClient library in your project will be loaded based on the runtime load order and the runtime will throw the NoSuchMethodError exception.
Solution: change the version of the package in your project that has caused NoSuchMethodError to the version of the corresponding library in pom.xml in the SDK.

### What if upload is slow in the SDK with IOException frequently printed in the log?

Cause and solution:

 a. Check whether you are accessing COS through the public network. Currently, CVM instances in the same region as COS can access COS through the private network (the IP ranges resolved by the private domain name is 10, 100, and 169). For more information on COS domain names, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224). If the public network is used, check whether the egress bandwidth is too small or whether bandwidth resources are occupied by other programs.
 b. Make sure that the logs in the production environment are not at the DEBUG level. INFO logs are recommended.
 c. Currently, the simple upload speed is up to 10 MB/s, and the speed of 32 concurrent uploads using advanced APIs can reach 60 MB/s. If the speed is far lower than those two values, see a and b.
 d. If a WARN log prints IOException, ignore it, as the SDK will retry. IOException may be caused by slow network connection. For possible reasons, see a and b.

### How to create a directory in the SDK?

In COS, both files and directories are objects, where directories are just objects that end with `/`. When creating a file, you don't need to create a directory. For example, when you create a file with the object key of `xxx/yyy/zzz.txt`, set the key to `xxx/yyy/zzz.txt` instead of creating the object `xxx/yyy/`. Directories are separated by `/` to show the hierarchy when displayed in the console. To create a directory object, use the following sample code:

```java
String bucketName = "examplebucket-1250000000";
String key = "folder/images/";
// A directory object is an empty file that ends with /, where a byte stream with a length of 0 is uploaded
InputStream input = new ByteArrayInputStream(new byte[0]);
ObjectMetadata objectMetadata = new ObjectMetadata();
objectMetadata.setContentLength(0);

PutObjectRequest putObjectRequest =
new PutObjectRequest(bucketName, key, input, objectMetadata);
PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
```

### How to use HTTPS in the SDK?

In the SDK, relevant configuration items are put in the ClientConfig class. Below is the sample code:

```java
// Initialize user credentials (secretId and secretKey)
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// Set the bucket region. For abbreviations of COS regions, see https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// Configure HTTPS
clientConfig.setHttpProtocol(HttpProtocol.https);
// Generate a COS client
COSClient cosClient = new COSClient(cred, clientConfig);
```

### How to use a proxy in the SDK?

If you need to use a proxy to access COS, you can configure a proxy IP (or a domain name) and port in the ClientConfig class. Below is the sample code:

```java
// Initialize user credentials (secretId and secretKey)
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// Set the bucket region. For abbreviations of COS regions, see https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// Configure a proxy (you need to set both the IP and port at the same time.)
// Set the proxy IP (or pass in the domain name)
clientConfig.setHttpProxyIp("192.168.2.3");
// Set the proxy port
clientConfig.setHttpProxyPort(8080);
// Generate a COS client
COSClient cosClient = new COSClient(cred, clientConfig);
```

