## Download and Installation

#### Relevant resources
- Download the COS XML Java SDK source code [here](https://github.com/tencentyun/cos-java-sdk-v5).
- Download the XML SDK for Java [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-java-sdk-v5/latest/cos-java-sdk-v5.zip).
- Download the demo [here](https://github.com/tencentyun/cos-java-sdk-v5/tree/master/src/main/java/com/qcloud/cos/demo).
- Find the complete sample code [here](https://github.com/tencentyun/cos-snippets/tree/master/Java).
- For the SDK changelog, please see [Changelog](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/CHANGELOG.md).

#### Environmental dependency
- The SDK supports JDK v1.7, v1.8, and higher.
- For more information on JDK installation, please see [Java Installation and Configuration](https://cloud.tencent.com/document/product/436/10865).

>?
>- For more information on the meanings of parameters such as `SecretId`, `SecretKey`, and `Bucket` contained herein and how to get them, please see [COS Glossary](https://cloud.tencent.com/document/product/436/7751#.E6.9C.AF.E8.AF.AD.E4.BF.A1.E6.81.AF).
>- The common classes in the COS SDK for Java are contained in the following packages:
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
    <version>5.6.35</version>
</dependency>
```

- Using source code
  Download the source code [here](https://github.com/tencentyun/cos-java-sdk-v5) or [from the SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-java-sdk-v5/latest/cos-java-sdk-v5.zip), and import it using Maven. For example, to import it into Eclipse, select **File** > **Import** > **Maven** > **Existing Maven Projects**.

#### Uninstalling SDK

Uninstall the SDK by removing the POM dependencies or source code.

## Getting Started

The following describes how to use the COS Java SDK to complete basic operations, such as initializing the client, creating a bucket, querying a bucket list, uploading an object, querying an object list, downloading an object, and deleting an object. For the classes in the examples, you can click on the class name in your IDE to view more details on all of its fields and functions.


### Importing classes

The COS Java SDK package is named `com.qcloud.cos.*`. You can import the classes required for running your program through your IDE such as Eclipse and IntelliJ.

### Initializing client

Before making any request for COS services, you need to generate a COSClient class object for calling the COS APIs.

>!COSClient is a thread-safe class that allows multi-thread access to the same instance. Because an instance maintains a connection pool internally, creating multiple instances may lead to resource exhaustion. **Please ensure there is only one instance in the program lifecycle**, and call the shutdown method to turn off the instance when no longer needed. If you need to create a new instance, shut down the previous instance first.

If you use a permanent key to initialize a `COSClient`, you need to get your `SecretId` and `SecretKey` on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in the CAM console. A permanent key is suitable for most application scenarios. Below is an example:

[//]: # (.cssg-snippet-global-init)
```java
// 1. Initialize the user credentials (secretId, secretKey).
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// 2. Set the bucket region. For abbreviations of COS regions, please visit https://cloud.tencent.com/document/product/436/6224.
// `clientConfig` contains the set methods to set region, HTTPS (HTTP by default), timeout, and proxy. For detailed usage, please see the source code or the FAQs about the SDK for Java.
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// 3. Generate a COS client.
COSClient cosClient = new COSClient(cred, clientConfig);
```

You can also use a temporary key to initialize the COSClient. For more information on how to generate and use a temporary key, please see [Generating and Using Temporary Keys](https://cloud.tencent.com/document/product/436/14048). An example is shown below:

[//]: # (.cssg-snippet-global-init-sts)
```java
// 1. Pass in the obtained temporary key (tmpSecretId, tmpSecretKey, sessionToken).
String tmpSecretId = "COS_SECRETID";
String tmpSecretKey = "COS_SECRETKEY";
String sessionToken = "COS_TOKEN";
BasicSessionCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);
// 2. Set the bucket region. For abbreviations of COS regions, please visit https://cloud.tencent.com/document/product/436/6224.
// `clientConfig` contains the set methods to set region, HTTPS (HTTP by default), timeout, and proxy. For detailed usage, please see the source code or the FAQs about the SDK for Java.
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// 3. Generate a COS client.
COSClient cosClient = new COSClient(cred, clientConfig);
```


The ClientConfig class is a configuration class containing the following main members:

| Member Name | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------- |
| region | Constructor or set method | Bucket region. For the abbreviations of COS regions, please see [Regions and Access Endpoints](https://cloud.tencent.com/document/product/436/6224) | Region |
| httpProtocol | set method | The protocol used by a request. By default, HTTP is used to interact with COS | HttpProtocol |
| signExpired | set method | Validity period in seconds of the request signature. Default value: 3600s | int |
| connectionTimeout | set method | Timeout duration in milliseconds for connection with COS. Default value: 30000 ms | int |
| socketTimeout | set method | Timeout duration in milliseconds for the client to read data. Default value: 30000 ms | int |
| httpProxyIp | set method | Proxy server IP | String |
| httpProxyPort | set method | Proxy server port | int |


### Creating bucket

After determining the region and bucket name, create a bucket by referring to the sample below:

[//]: # (.cssg-snippet-put-bucket-and-grant-acl)
```java
String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
CreateBucketRequest createBucketRequest = new CreateBucketRequest(bucket);
// Set the bucket permission to Private (private read/write). Other options include public read/private write and public read/write
createBucketRequest.setCannedAcl(CannedAccessControlList.Private);
try{
    Bucket bucketResult = cosClient.createBucket(createBucketRequest);
} catch (CosServiceException serverException) {
    serverException.printStackTrace();
} catch (CosClientException clientException) {
    clientException.printStackTrace();
}
```

### Querying bucket list

Query the bucket list by referring to the sample below:

[//]: # (.cssg-snippet-get-service)
```java
List<Bucket> buckets = cosClient.listBuckets();
for (Bucket bucketElement : buckets) {
    String bucketName = bucketElement.getName();
    String bucketLocation = bucketElement.getLocation();
}
```

### Uploading object

Upload a local file or input stream with a known length to COS. It is most suitable for uploading small image files below 20 MB. The maximum file size allowed is 5 GB. For larger files, you need to use multipart upload or the advanced upload API.

- If most of your local files are over 20 MB, we recommend you upload them with the advanced upload API.
- If an object with the same key already exists in COS, it will be overwritten during the upload.
- To create a directory object, please see [How to Create a Directory in the SDK](https://intl.cloud.tencent.com/document/product/436/38956?lang=en&pg=#how-do-i-create-a-directory-in-the-sdk.3F).
- An object key (Key) is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/images/picture.jpg`, the object key is `images/picture.jpg`. For more information, please see [Object Key](https://cloud.tencent.com/document/product/436/13324#.E5.AF.B9.E8.B1.A1.E9.94.AE).


Below is an example of uploading a file below 5 GB:

[//]: # (.cssg-snippet-put-object)
```java
// Specify the file to be uploaded.
File localFile = new File(localFilePath);
// Specify the destination bucket.
String bucketName = "examplebucket-1250000000";
// Specify the key of the object to be uploaded to COS.
String key = "exampleobject";
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
```

### Querying object list

Query the list of objects in a bucket by referring to the sample below:

[//]: # (.cssg-snippet-get-bucket)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// Set the bucket name.
listObjectsRequest.setBucketName(bucketName);
// The prefix indicates that the key of the object to be listed must start with this value.
listObjectsRequest.setPrefix("images/");
// Set the delimiter to "/" to list objects in the current directory; and leave it empty to list all objects.
listObjectsRequest.setDelimiter("/");
// Set the maximum number of traversed objects (up to 1,000 per listobject request).
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

### Downloading object
Once an object is uploaded, you can download it by calling the GET Object API with the same key, or by generating a [pre-signed URL](https://cloud.tencent.com/document/product/436/35217) (please use the GET method to download) to share to another device for the download. If your file is set to private read, note that the pre-signed URL may be valid only for a limited period.
Download a file to a specified local path by referring to the sample below:

[//]: # (.cssg-snippet-get-object)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
// Method 1. Get the input stream of the downloaded file.
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
COSObject cosObject = cosClient.getObject(getObjectRequest);
COSObjectInputStream cosObjectInput = cosObject.getObjectContent();
// Download the CRC64 value of the object.
String crc64Ecma = cosObject.getObjectMetadata().getCrc64Ecma();
// Close the input stream.
cosObjectInput.close();

// Method 2. Download the file locally.
String outputFilePath = "exampleobject";
File downFile = new File(outputFilePath);
getObjectRequest = new GetObjectRequest(bucketName, key);
ObjectMetadata downObjectMeta = cosClient.getObject(getObjectRequest, downFile);
```

### Deleting object

Delete an object in a specified path of COS with the following code:

[//]: # (.cssg-snippet-delete-object)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
cosClient.deleteObject(bucketName, key);
```

### Closing client

Close the COSClient and release the server threads connected over HTTP with the following code:

```java
// Close the client (release server threads).
cosClient.shutdown();
```
