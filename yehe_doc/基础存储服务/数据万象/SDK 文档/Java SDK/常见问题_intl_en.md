### What do I do if the client network is normal, while the access to COS over HTTP is very slow, or the error message "Connection reset" is reported?

In some regions, ISPs may hijack COS endpoints. Therefore, we recommend you access COS over HTTPS.

### What do I do if `java.lang.NoSuchMethodError` is reported when I run the SDK?

**Cause**: This is usually caused by a JAR package conflict. For example, if the JAR package the SDK depends on uses method A, but the JAR package in the HttpClient library of your project does not have method A, then the HttpClient library will be loaded in the runtime loading order, reporting `NoSuchMethodError`.
**Solution**:
- Solution 1: Change the version of the package in your project that has caused `NoSuchMethodError` to the version of the corresponding library in `pom.xml` in the SDK.
- Solution 2: Replace `cos-java-sdk` with `cos_api-bundle`. In this case, all dependencies of `cos-java-sdk` are installed independently, so more space will be used.
```
<groupId>com.qcloud</groupId>
       <artifactId>cos_api-bundle</artifactId>
<version>5.6.35</version>
```

### What is the default timeout duration of the Java SDK?

Both the default connection and read/write timeout periods of the Java SDK are 30,000 ms. You can use the `SetConnectionTimeoutMs` and `setSocketTimeout` methods in the SDK to adjust them respectively.

### What do I do if the upload with the Java SDK is slow and `IOException` is frequently printed in the log?

Troubleshoot the problem as follows:
1. Check whether you are accessing COS over the public network.
Currently, CVM instances in the same region as COS generally access COS over the private network (the IP ranges resolved by the private endpoint are 10, 100, and 169). For more information on COS endpoints, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). If the public network is used, check whether the egress bandwidth is too small or whether bandwidth resources are occupied by other programs.
2. Check that the logs in the production environment are not set to DEBUG level. The INFO level is recommended.
3. If `IOException` is printed in WARN logs, it can be ignored, and the SDK will retry. `IOException` may be caused by a slow network connection. For solutions, see steps 1 and 2 above.

### What do I do if there is a plus sign (+) in the requested upload path, throwing "403 SignatureDoesNotMatch"?

**Possible cause**: The version of HttpClient in the Java environment leads to a URL-encoding error.
**Solution**:
- Solution 1: Use HttpClient 4.5.3.
```
<groupId>org.apache.httpcomponents</groupId>
       <artifactId>httpclient</artifactId>
 <version>4.5.3</version> 
```
- Solution 2: Replace `cos-java-sdk` with `cos_api-bundle`. In this case, all dependencies of `cos-java-sdk` are installed independently, so more space will be used.
```
<groupId>com.qcloud</groupId>
       <artifactId>cos_api-bundle</artifactId>
<version>5.6.35</version>
```

### What should I do if the Java SDK reports an error indicating that a certain dependency version is too low?

**Cause**: The dependency version of your Java environment conflicts with that required by the Java SDK.
**Solution**:
- Solution 1: Upgrade the dependency to the required version as prompted.
- Solution 2: Replace `cos-java-sdk` with `cos_api-bundle`. In this case, all dependencies of `cos-java-sdk` are installed independently, so more space will be used.
```
<groupId>com.qcloud</groupId>
       <artifactId>cos_api-bundle</artifactId>
<version>5.6.35</version>
```

### How do I create a COS file directory in the SDK?

In COS, both files and directories are objects, where directories are objects that end with `/`. When creating a file, you don't need to create a directory. For example, when you create a file with the object key of `xxx/yyy/zzz.txt`, set the key to `xxx/yyy/zzz.txt` instead of creating the object `xxx/yyy/`. Directories are separated by `/` to show the hierarchy when displayed in the console. To create a directory object, use the following sample code:

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

### How do I use HTTPS in the SDK?

In the SDK, relevant configuration items are put in the `ClientConfig` class. Below is the sample code:

```java
// Initialize user authentication information (`secretId` and `secretKey`).
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// Set the bucket region. For abbreviations of COS regions, please visit https://intl.cloud.tencent.com/document/product/436/6224.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// Configure HTTPS.
clientConfig.setHttpProtocol(HttpProtocol.https);
// Generate a COS client.
COSClient cosClient = new COSClient(cred, clientConfig);
```

### How do I use a proxy in the SDK?

If you need to use a proxy to access COS or CI, you can configure a proxy IP (or domain name) and port in the `ClientConfig` class. Below is the sample code:

```java
// Initialize user authentication information (`secretId` and `secretKey`).
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// Set the bucket region. For abbreviations of COS regions, please visit https://intl.cloud.tencent.com/document/product/436/6224.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// Configure a proxy (both the IP and port need to be set).
// Set the proxy IP (or pass an endpoint).
clientConfig.setHttpProxyIp("192.168.2.3");
// Set the proxy port.
clientConfig.setHttpProxyPort(8080);
// Generate a COS client.
COSClient cosClient = new COSClient(cred, clientConfig);
```

### How do I set up custom `EndpointBuilder`?

In scenarios where the endpoint needs to be specified for an API request, you need to implement the `buildGeneralApiEndpoint` and `buildGetServiceApiEndpoint` functions in the `EndpointBuilder` API to specify the remote endpoints for general API requests and `GETService` requests respectively. Below is the sample code:
```
// Step 1. Implement the two functions in the EndpointBuilder API.
class SelfDefinedEndpointBuilder implements EndpointBuilder {
    @Override
    public String buildGeneralApiEndpoint(String bucketName) {
        return String.format("%s.%s", bucketName, "mytest.com");
    }

    @Override
    public String buildGetServiceApiEndpoint() {
        return "service.mytest.com";
    }
}

// Step 2. Initialize the client.
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
SelfDefinedEndpointBuilder selfDefinedEndpointBuilder = new SelfDefinedEndpointBuilder();
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing"));
clientConfig .setEndpointBuilder(selfDefinedEndpointBuilder);
COSClient cosClient = new COSClient(cred, clientConfig);
```

### Do I need to add the `/` prefix to key values used in SDK operations such as upload, download, and batch delete?

The key value does not need to be prefixed with `/` for COS objects. For example, if you set the key value of a COS object to `exampleobject`, you can access it using the `http://cos.ap-guangzhou.myqcloud.com/exampleobject` URL.
>! Do not pass in a key prefixed with `/` in a batch deletion request; otherwise, object deletion will fail.
>


### What should I do if the error message "please make sure bucket name must contain legal appid when appid is missing. example: bucektname-1250000000" is reported when I use the Java SDK to upload files?

COS Java SDK on an earlier version supports only APPID values starting with 125. If you are using an APPID starting with 130, we recommend you update the SDK to the latest version. For more information on how to download and install the Java SDK, see [Getting Started](https://intl.cloud.tencent.com/document/product/436/10199).

### What should I do if the Java SDK reports an error when I upload large files?

To upload files larger than 5 GB by using the Java SDK, we recommend you use the [advanced upload API](https://www.tencentcloud.com/document/product/436/44015). It automatically determines whether to use simple or multipart upload based on the length and data type of your file.

### How do I obtain the file upload progress in the Java SDK?

To get the file upload progress, we recommend you use the [advanced upload API](https://www.tencentcloud.com/document/product/436/44015). You can use the `getProgress()` method of `Upload` to get the `TransferProgress` class.

### Can Java SDK use persistent connections?

The Java SDK uses persistent connections by default.

### How to use the Java SDK to get all the paths to the specified directory and determine whether the paths are files or folders?

You can use the feature of [querying the object list](https://intl.cloud.tencent.com/document/product/436/10199#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8) in the Java SDK to list all objects in a bucket. **You can use the `prefix` parameter to specify the directory prefix.**

### What should I do if the Java SDK reports the error "java.lang.IllegalStateException: Connection pool shut down"?

1. COSClient is a thread-safe class that allows multi-thread access to the same instance.
Because an instance maintains a connection pool internally, creating multiple instances may lead to resource exhaustion. Make sure that there is only one instance in the program lifecycle, and call the `COSClient.shutdown()` method to shut down the instance when it is no longer needed.
If you need to create a new instance, shut down the previous one first. **We recommend you use only one COSClient in a thread and call `COSClient.shutdown()` after all programs end and exit.**
2. COSClient is also used in the TransferManager encapsulation class of advanced APIs. We recommend you call `TransferManager.shutdownNow(false)` after all programs end and exit.
In addition, if another COSClient is reused when a TransferManager instance is created, add the parameter `false` (i.e., `TransferManager.shutdownNow(false)`) when closing the instance. This avoids closing the reused COSClients and thus causing errors in other places where it is used.



