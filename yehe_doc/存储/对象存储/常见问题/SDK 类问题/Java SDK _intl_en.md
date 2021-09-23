### What do I do if the client network is normal, while the access to COS over HTTP is very slow, or the error message "Connection reset" is reported?
In some regions, carriers may hijack COS endpoints. Therefore, you are advised to access COS over HTTPS.

### What do I do if `java.lang.NoSuchMethodError` is reported when I run the SDK?

This is usually caused by a JAR package conflict. For example, if the JAR package the SDK depends on uses method A, but the JAR package in the HttpClient library in your project does not have method A, then, the HttpClient library in your project will be loaded due to the runtime load order, throwing `NoSuchMethodError`.
Solutions:
Solution 1: change the version of the package in your project that has caused `NoSuchMethodError` to the version of the corresponding library in `pom.xml` in the SDK.
Solution 2: replace `cos-java-sdk` with `cos_api-bundle`. In this case, all dependencies of `cos-java-sdk` are installed independently and thus more space will be used.
```
<groupId>com.qcloud</groupId>
       <artifactId>cos_api-bundle</artifactId>
<version>5.6.35</version>
```

### What is the default timeout duration of the Java SDK?

The default connection timeout duration of the Java SDK is 45,000 ms, and the default read/write timeout duration is 45,000 ms. You can use the `SetConnectionTimeoutMs` and `SetReadWriteTimeoutMs` methods in the SDK to adjust them.

### What do I do if the upload with the Java SDK is slow and `IOException` is frequently printed in the log?

Troubleshoot the problem as follows:

1. Check whether you are accessing COS through a public network. Currently, CVM instances that are in the same region as COS can access COS through a private network (the IP ranges resolved by the private endpoint are 10, 100, and 169). For more information about COS endpoints, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). If a public network is used, check whether the egress bandwidth is too small or whether bandwidth resources are occupied by other programs.
2. Check that the logs in the production environment are not set to DEBUG level. The INFO level is recommended.
3. Currently, the simple upload speed is up to 10 MB/s, and the speed of 32 concurrent uploads using advanced APIs can reach 60 MB/s. If the speed is far lower than these two values, see steps 1 and 2.
4. If `IOException` is printed in the WARN level logs, it can be ignored, and the SDK will retry. `IOException` may be caused by a slow network connection. For the solutions, see steps 1 and 2.

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

### What should I do if the Java SDK reports an error indicating that a certain dependency version is too low?
Cause: the dependency version of your Java environment conflicts with that required by the Java SDK.
Solutions:
Solution 1: Upgrade the dependency to the required version as prompted.
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


### What do I do if the error message "please make sure bucket name must contain legal appid when appid is missing. example: bucektname-1250000000" is reported when I use the Java SDK to upload files?

COS Java SDK of an earlier version supports only app IDs starting with, for example, 125. If you are using an app ID starting with 130, it is recommended that you update the SDK to the latest version. For more information on how to download and install the Java SDK, see [Java SDK documentation](https://intl.cloud.tencent.com/document/product/436/10199).

### What do I do if the COS Java SDK reports an error when I upload large files?

To upload files larger than 5 GB using the Java SDK, you are recommended to use the [advanced upload API](https://intl.cloud.tencent.com/document/product/436/31534). The advanced upload API automatically determines whether to use simple or multipart upload based on the length and data type of your file.

### How do I obtain the file upload progress in the Java SDK?

To obtain the file upload progress, you are recommended to use the [advanced upload API](https://intl.cloud.tencent.com/document/product/436/31534). You can use the `getProgress()` method of `Upload` to obtain the `TransferProgress` class.

### Does Java SDK support calculating the CRC64 checksum of a local file?

No. You need to implement this feature on the business side. For more information, please see [Java issues](https://github.com/tencentyun/cos-java-sdk-v5/issues/63).

### How is the 21-bit CRC64 checksum returned by COS compared with the locally calculated CRC64 checksum?

The long of Java supports only 20 bits. Therefore, you can compare as follows:

```java
CRC64 localCRC = new CRC64();
// Calculate the local CRC64.
localCRC.update();
//...

// Convert the CRC64 returned by COS to long:
cosCRC = crc64ToLong(strCOSCRC);

// Perform comparison.
if (cosCRC == localCRC.getValue()) {
   xxx
}

// Convert the COS-returned CRC64 into a long in Java.
long crc64ToLong(String crc64) {
   if (crc64.charAt(0) == '-') {
       return negativeCrc64ToLong(crc64);
   } else {
       return positiveCrc64ToLong(crc64);
   }
}

long positiveCrc64ToLong(String strCrc64) {
   BigInteger crc64 = new BigInteger(strCrc64);
   BigInteger maxLong = new BigInteger(Long.toString(Long.MAX_VALUE));

   int maxCnt = 0;

   while (crc64.compareTo(maxLong) > 0) {
       crc64 = crc64.subtract(maxLong);
       maxCnt++;
   }

   return crc64.longValue() + Long.MAX_VALUE * maxCnt;
}

long negativeCrc64ToLong(String strCrc64) {
   BigInteger crc64 = new BigInteger(strCrc64);
   BigInteger minLong = new BigInteger(Long.toString(Long.MIN_VALUE));

   int minCnt = 0;

   while (crc64.compareTo(minLong) < 0) {
       crc64 = crc64.subtract(minLong);
       minCnt++;
   }

   return crc64.longValue() + Long.MIN_VALUE * minCnt;
}
```

### Can Java SDK use persistent connections?

The Java SDK uses persistent connections by default.

### How to use the Java SDK to get all the paths to the specified directory and determine whether the paths are files or folders?

You can use the feature of [querying the object list](https://intl.cloud.tencent.com/document/product/436/10199#.E6.9F.A5.E8.AF.A2.E5.AF.B9.E8.B1.A1.E5.88.97.E8.A1.A8) in the Java SDK to list all objects in a bucket. **You can use the `prefix` parameter to specify the directory prefix.**



