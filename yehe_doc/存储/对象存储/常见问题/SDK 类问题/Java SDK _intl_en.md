
### What do I do if the client network is normal, while the access to COS over HTTP is very slow, or the error message “Connection reset” is reported?
In some regions, carriers may hijack COS endpoints. Therefore, you are advised to access COS over HTTPS.

### What do I do if `java.lang.NoSuchMethodError` is reported when I run the SDK?

This is usually caused by a JAR package conflict. For example, if the JAR package the SDK depends on uses method A, but the JAR package in the HttpClient library in your project does not have method A, then, the HttpClient library in your project will be loaded due to the runtime load order, throwing `NoSuchMethodError`.
Solution: Change the version of the package in your project that has caused `NoSuchMethodError` to the version of the corresponding library in `pom.xml` in the SDK.

### What do I do if the upload with SDK is slow and `IOException` is frequently printed in the log?

Causes and solutions:

1. Check whether you are accessing COS through a public network. Currently, CVM instances that are in the same region as COS can access COS through a private network (the IP ranges resolved by the private endpoint are 10, 100, and 169). For more information about COS endpoints, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). If a public network is used, check whether the egress bandwidth is too small or whether bandwidth resources are occupied by other programs.
2. Ensure that the logs in the production environment are not set to DEBUG level. The INFO level is recommended.
3. Currently, the simple upload speed is up to 10 MB/s, and the speed of 32 concurrent uploads using advanced APIs can reach 60 MB/s. If the speed is far lower than these two values, see 1 and 2.
4. If `IOException` is printed in the WARN level logs, it can be ignored, and the SDK will retry. `IOException` may be caused by a slow network connection. For possible causes, see 1 and 2.

### What do I do if there is a plus sign (+) in the requested upload path, throwing "403 SignatureDoesNotMatch"?
Possible cause: The version of HttpClient in the Java environment leads to the URLEncode error.
You can troubleshoot using either of the following ways:
Solution 1: Use the 4.5.3 version of HttpClient.
```
<groupId>org.apache.httpcomponents</groupId>
       <artifactId>httpclient</artifactId>
 <version>4.5.3</version> 
```

Solution 2: Replace `cos-java-sdk` with `cos_api-bundle`. In this case, all dependencies of `cos-java-sdk` are installed independently and thus more space will be used.
```
<groupId>com.qcloud</groupId>
       <artifactId>cos_api-bundle</artifactId>
<version>5.6.35</version>
```

### How do I create a directory in the SDK?

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
// Initialize user authentication information (secretId and secretKey).
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

If you need to use a proxy to access COS, you can configure a proxy IP (or an endpoint) and port in the `ClientConfig` class. Below is the sample code:

```java
// Initialize user authentication information (secretId and secretKey).
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
In scenarios where the endpoint needs to be specified for an API request, you need to implement the `buildGeneralApiEndpoint` and ` buildGetServiceApiEndpoint` functions in the `EndpointBuilder` API to specify the remote endpoints for a general API request and `GETService` request, respectively. Below is the sample code:
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
>!Do not pass in a key prefixed with `/` in a batch delete request. Otherwise, the object deletion may fail.
