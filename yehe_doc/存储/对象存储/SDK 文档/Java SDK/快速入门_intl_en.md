## Download and Installation

#### Relevant resources
- Download the COS XML Java SDK source code [here](https://github.com/tencentyun/cos-java-sdk-v5).
- Download the XML Java SDK [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-java-sdk-v5/latest/cos-java-sdk-v5.zip).
- Download the demo [here](https://github.com/tencentyun/cos-java-sdk-v5/tree/master/src/main/java/com/qcloud/cos/demo).
- For the complete sample code, please see [SDK Sample Code](https://github.com/tencentyun/cos-snippets/tree/master/Java).
- For the SDK changelog, please see [Changelog](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/CHANGELOG.md).
- For SDK FAQs, please see [Java SDK FAQs](https://intl.cloud.tencent.com/document/product/436/38956).


>? If you encounter errors such as non-existent functions or methods when using the XML version of the SDK, please update the SDK to the latest version and try again.
>


#### Environment requirements
- The SDK supports JDK v1.7, v1.8, or higher.
- For the JDK installation, please see [Java Installation and Configuration](https://intl.cloud.tencent.com/document/product/436/10865).

>?
>- For the definitions of terms such as SecretId, SecretKey, and Bucket, see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/7751).
>- You can find common classes for the COS Java SDK in the following packages:
 - The classes related to client configuration are in the com.qcloud.cos.\* package.
 - The classes related to permissions are in the com.qcloud.cos.auth.\* sub-package.
 - The classes related to exceptions are in the com.qcloud.cos.exception.\* sub-package.
 - The classes related to requests are in the com.qcloud.cos.model.\* sub-package.
 - The classes related to regions are in the com.qcloud.cos.region.\* sub-package.
 - The classes related to advanced APIs are in the com.qcloud.cos.transfer.\* sub-package.

#### Installing SDK
You can install the Java SDK using Maven or source code:

- Using Maven
  Add required dependencies to the pom.xml file of your Maven project as follows:
```shell
<dependency>
       <groupId>com.qcloud</groupId>
       <artifactId>cos_api</artifactId>
       <version>5.6.54</version>
</dependency>
```
- Using source code
  Download the source code from [GitHub](https://github.com/tencentyun/cos-java-sdk-v5) or [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-java-sdk-v5/latest/cos-java-sdk-v5.zip), and import it using Maven. For example, to import it into Eclipse, select **File** > **Import** > **Maven** > **Existing Maven Projects**.

#### Uninstalling SDK

Uninstall the SDK by removing the POM dependencies or source code.

## Getting Started

The following describes how to use the COS Java SDK to complete basic operations, such as initializing the client, creating a bucket, querying a bucket list, uploading an object, querying an object list, downloading an object, and deleting an object. For the classes in the examples, you can click the class name in your IDE to view more details about all its fields and functions.


### Importing classes

The COS Java SDK package is named `com.qcloud.cos.*`. You can import the classes required for running your program through your IDE such as Eclipse and IntelliJ.

### Initializing the client

Before making any request for COS services, you need to generate a COSClient class object for calling the COS APIs.

>!COSClient is a thread-safe class that allows multi-thread access to the same instance. Because an instance maintains a connection pool internally, creating multiple instances may lead to resource exhaustion. **Please ensure that there is only one instance in the program lifecycle**, and call the shutdown method to turn off the instance when it is no longer needed. If you need to create a new instance, shut down the previous instance first.

If you use a permanent key to initialize a `COSClient`, you can get the `APPId`, `SecretId`, and `SecretKey` on the [Manage API Key](https://console.cloud.tencent.com/cam/capi) page of the CAM console. A permanent key is suitable for most application scenarios. Below is an example:

[//]: # ".cssg-snippet-global-init"
```java
// 1. Initialize the user credentials (secretId, secretKey).
// Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) to view and manage the `SecretId` and `SecretKey` of your project.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// 2. Set the bucket region. For the abbreviations for COS regions, please see https://intl.cloud.tencent.com/document/product/436/6224.
// `clientConfig` contains the set methods to set region, HTTPS (HTTP by default), timeout, and proxy. For detailed usage, please see the source code or the FAQs about the SDK for Java.
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// The HTTPS protocol is recommended.
// HTTPS is used by default since v5.6.54.
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3. Generate a COS client.
COSClient cosClient = new COSClient(cred, clientConfig);
```

You can also use a temporary key to initialize the COSClient. For more information on how to generate and use a temporary key, see [Generating and Using Temporary Keys](https://cloud.tencent.com/document/product/436/14048). An example is shown below:

[//]: # ".cssg-snippet-global-init-sts"
```java
// 1. Pass in the obtained temporary key (tmpSecretId, tmpSecretKey, sessionToken).
String tmpSecretId = "SECRETID";
String tmpSecretKey = "SECRETKEY";
String sessionToken = "TOKEN";
BasicSessionCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);
// 2. Set the bucket region. For the abbreviations for COS regions, please see https://intl.cloud.tencent.com/document/product/436/6224.
// `clientConfig` contains the set methods to set region, HTTPS (HTTP by default), timeout, and proxy. For detailed usage, please see the source code or the FAQs about the SDK for Java.
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// 3. Generate a COS client.
COSClient cosClient = new COSClient(cred, clientConfig);
```


The ClientConfig class is a configuration class containing the following main members:

| Member Name | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------- |
| region | Constructor or set method | Bucket region. For the abbreviations for COS regions, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | Region |
| httpProtocol | Set method | The protocol used by the request. By default, HTTP is used to interact with COS. | HttpProtocol |
| signExpired | Set method | Validity period (in seconds) of the request signature. Default: 3600s | int |
| connectionTimeout | Set method | Timeout duration in milliseconds for connection with COS. Default value: 30000 ms | int |
| socketTimeout | Set method | Timeout duration in milliseconds for the client to read data. Default value: 30000 ms | int |
| httpProxyIp | Set method | Proxy server IP | String |
| httpProxyPort | Set method | Proxy server port | int |


### Creating a bucket

The following example creates a bucket for the selected region and bucket:

[//]: # ".cssg-snippet-put-bucket-and-grant-acl"
```java
String bucket = "examplebucket-1250000000"; // Bucket, formatted as BucketName-APPID
CreateBucketRequest createBucketRequest = new CreateBucketRequest(bucket);
// Set the bucket permission to "Private" (private read and write). Other valid values are "PublicRead" (public read/private write) and "PublicReadWrite" (public read and write).
createBucketRequest.setCannedAcl(CannedAccessControlList.Private);
try{
    Bucket bucketResult = cosClient.createBucket(createBucketRequest);
} catch (CosServiceException serverException) {
    serverException.printStackTrace();
} catch (CosClientException clientException) {
    clientException.printStackTrace();
}
```

### Querying the bucket list

The following example queries a bucket list:

[//]: # ".cssg-snippet-get-service"
```java
List<Bucket> buckets = cosClient.listBuckets();
for (Bucket bucketElement : buckets) {
    String bucketName = bucketElement.getName();
    String bucketLocation = bucketElement.getLocation();
}
```

### Uploading an object

Upload a local file or input stream with a known length to COS. It is most suitable for uploading small image files below 20 MB. The maximum file size allowed is 5 GB. For larger files, you need to use multipart upload or an advanced upload API.

>? The classes related to advanced APIs are in the com.qcloud.cos.transfer.\* sub-package.

- If most of your local files are over 20 MB, you are advised to upload them with an advanced upload API.
- If an object with the same key already exists in COS, it will be overwritten by the newly-uploaded one.
- To create a directory object, please see [How to create a directory in the SDK?](https://intl.cloud.tencent.com/document/product/436/38956#sdk-.E5.A6.82.E4.BD.95.E5.88.9B.E5.BB.BA.E7.9B.AE.E5.BD.95.EF.BC.9F).
- An object key (Key) is the unique identifier of an object in a bucket. For example, in the object’s access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/images/picture.jpg`, the object key is `images/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324).


The following example uploads a file up to 5 GB:

[//]: # ".cssg-snippet-put-object"
```java
// Specify the file to be uploaded.
File localFile = new File(localFilePath);
// Specify a bucket to store the file.
String bucketName = "examplebucket-1250000000";
// Specify the COS path (i.e. the object key) to upload the file. For example, if the object key is "folder/picture.jpg", the file "picture.jpg" will be uploaded to the "folder" directory.
String key = "exampleobject";
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
```

### Querying objects

The following example queries the list of objects in a bucket:

[//]: # ".cssg-snippet-get-bucket"
```java
// Enter the bucket name in the format of `BucketName-APPID`
String bucketName = "examplebucket-1250000000";
ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// Set the bucket name.
listObjectsRequest.setBucketName(bucketName);
// The prefix indicates that the key of the object to be listed must start with this value
listObjectsRequest.setPrefix("images/");
// Set the delimiter to "/" to list objects in the current directory. To list all objects, leave it empty.
listObjectsRequest.setDelimiter("/");
// Set the maximum number of traversed objects (up to 1,000 per listobject request)
listObjectsRequest.setMaxKeys(1000);
ObjectListing objectListing = null;
do {
    try {
        objectListing = cosClient.listObjects(listObjectsRequest);
    } catch (CosServiceException e) {
        e.printStackTrace();
        return;
    } catch (CosClientException e) {
        e.printStackTrace();
        return;
    }
    // A common prefix indicates paths that end with the delimiter. If the delimiter is set to "/", the common prefix indicates the paths of all subdirectories.
    List<String> commonPrefixs = objectListing.getCommonPrefixes();

    // The object summary shows all listed objects.
    List<COSObjectSummary> cosObjectSummaries = objectListing.getObjectSummaries();
    for (COSObjectSummary cosObjectSummary : cosObjectSummaries) {
        // File path key
        String key = cosObjectSummary.getKey();
        // File ETag
        String etag = cosObjectSummary.getETag();
        // File size
        long fileSize = cosObjectSummary.getSize();
        // File storage class
        String storageClasses = cosObjectSummary.getStorageClass();
    }

    String nextMarker = objectListing.getNextMarker();
    listObjectsRequest.setMarker(nextMarker);
} while (objectListing.isTruncated());
```

### Downloading an object
Once an object is uploaded, you can download it by calling the GET Object API with the same key, or by generating a [pre-signed URL](https://intl.cloud.tencent.com/document/product/436/31536) (Please specify GET as the download method) to share to another device for download. Note that the pre-signed URL may be valid only for a limited period if your file is set to private-read.
The following example downloads a file to a specified local path:

[//]: #	".cssg-snippet-get-object"
```java
// Enter the bucket name in the format of `BucketName-APPID`
String bucketName = "examplebucket-1250000000";
// Specify the COS path (i.e. the object key) of the file to download. For example, if the object key is "folder/picture.jpg", the file "picture.jpg" in the "folder" directory will be downloaded.
String key = "exampleobject";
// Method 1. Get the input stream of the downloaded file.
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
COSObject cosObject = cosClient.getObject(getObjectRequest);
COSObjectInputStream cosObjectInput = cosObject.getObjectContent();
// Download the CRC64 value of the object.
String crc64Ecma = cosObject.getObjectMetadata().getCrc64Ecma();
// Close the input stream.
cosObjectInput.close();

// Method 2: Download the file to a local directory, e.g. a directory in D drive.
String outputFilePath = "exampleobject";
File downFile = new File(outputFilePath);
getObjectRequest = new GetObjectRequest(bucketName, key);
ObjectMetadata downObjectMeta = cosClient.getObject(getObjectRequest, downFile);
```

### Deleting an object

You can delete an object in a specified path in COS with the following code:

[//]: # ".cssg-snippet-delete-object"
```java
// Enter the bucket name in the format of `BucketName-APPID`
String bucketName = "examplebucket-1250000000";
// Specify the COS path (i.e. the object key) of the file to delete. For example, if the object key is "folder/picture.jpg", the "picture.jpg" file in the "folder" directory will be deleted.
String key = "exampleobject";
cosClient.deleteObject(bucketName, key);
```

### Default retry policy

By default, if requests initiated by COSClient via the SDK return error responses, they will be retried. The retry policy is as follows:
- Number of retries: defaults to `3`. You can set it using `clientConfig.setMaxErrorRetry`.
If set to `0`, no retry will be performed on all types of request errors.
- Error types for retry: all client-side IOException, as well as server-side errors with the status codes 500, 502, 503, and 504

You can also configure a retry policy as needed by referring to the following code:

Setting the number of retries:

[//]: # ".cssg-snippet-error-retry"
```java
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// Set the maximum number of retries to 4.
clientConfig.setMaxErrorRetry = 4;
```

Setting the retry policy:

[//]: # ".cssg-snippet-retry-policy"
```java
// Customize a retry policy.
public class OnlyIOExceptionRetryPolicy extends RetryPolicy {
    @Override
    public <X extends CosServiceRequest> boolean shouldRetry(CosHttpRequest<X> request,
            HttpResponse response,
            Exception exception,
            int retryIndex) {
        // Retry only for client-side IOException.
        if (exception.getCause() instanceof IOException) {
            return true;
        }
        return false;
    }
}

Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
RetryPolicy myRetryPolicy = new OnlyIOExceptionRetryPolicy();
// Configure the custom retry policy.
clientConfig.setRetryPolicy(myRetryPolicy);
```

### Shutting down the client

Shut down the COSClient and release the server threads connected over HTTP with the following code:
```java
// Close the client (release server threads).
cosClient.shutdown();
```

## FAQs

If you have any questions about Java SDK, please see [here](https://intl.cloud.tencent.com/document/product/436/38956).
