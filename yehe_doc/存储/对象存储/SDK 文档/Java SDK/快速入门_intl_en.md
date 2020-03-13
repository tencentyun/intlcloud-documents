## Download and Installation

#### Relevant Resources
- The resources of COS XML Java SDK can be downloaded [here](https://github.com/tencentyun/cos-java-sdk-v5).
- The sample demo can be download [here](<https://github.com/tencentyun/cos-java-sdk-v5/tree/master/src/main/java/com/qcloud/cos/demo>).

#### Environmental Requirements
- The SDK supports JDK v1.7 and higher.
- For more information on JDK installation, see [Java Installation and Configuration](https://cloud.tencent.com/document/product/436/10865).

>
>- For definitions of SecretId, SecretKey, Bucket and other terms, see [COS Glossary](https://cloud.tencent.com/document/product/436/7751#.E6.9C.AF.E8.AF.AD.E4.BF.A1.E6.81.AF).
>- You can find the common classes in the COS Java SDK in the following packages:
 - The classes related to client configuration are in the com.qcloud.cos.\* package.
 - The classes related to permissions are in the com.qcloud.cos.auth.\* sub-package.
 - The classes related to exceptions are in the com.qcloud.cos.exception.\* sub-package.
 - The classes related to requests are in the com.qcloud.cos.model.\* sub-package.
 - The classes related to regions are in the com.qcloud.cos.region.\* sub-package.
 - The classes related to advanced APIs are in the com.qcloud.cos.transfer.\* sub-package.

#### Installing the SDK
You can install Java SDK through Maven or source code:

- Install through Maven
  Add relevant dependencies to the pom.xml file of the Maven project as follows:
```shell
<dependency>
      <groupId>com.qcloud</groupId>
      <artifactId>cos_api</artifactId>
      <version>5.6.8</version>
</dependency>
```

- Install through source code
  Download the source code from [XML Java SDK](https://github.com/tencentyun/cos-java-sdk-v5) and import it via Maven. For example, in Eclipse, select **File** > **Import** > **Maven** > **Existing Maven Projects**.

### Uninstalling SDK

Uninstall the SDK by removing the pom dependencies or source code.

## Getting Started

The following describes how to use COS Java SDK to complete a basic operation, such as initializing the client, creating a bucket, querying the bucket list, uploading an object, querying the object list, downloading an object, and deleting an object. For classes in the example, you can click on the class in IDE to view all of its field and function definitions. There are detailed comments in the class.


### Importing Classes

The package name of COS Java SDK is `com.qcloud.cos.*`, and you can import the classes needed for program execution with IDE tools such as Eclipse and IntelliJ.

### Initializing the client

Before executing any COS requests, an object of the COSClient class, which is used to call COS APIs, needs to be generated. Once a COSClient instance is generated, it is reusable and thread-safe. When the program or service exits, you need to close the client.

>COSClient is a thread-safe class that allows multi-thread access to the same instance. Because an instance maintains a connection pool internally, creating multiple instances may lead to resource exhaustion. **Please ensure there is only one instance in the program lifecycle**, and call the shutdown method to turn off the instance when no longer needed. If you need to create a new instance, shut down the previous instance first.

If you use a permanent key to initialize COSClient, you need to obtain your SecretId and SecretKey on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in the CAM Console. A permanent key can be used for most application scenarios. Below is a sample:

[//]: # (.cssg-snippet-global-init)
```java
// 1. Initialize the user credentials (secretId, secretKey)
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// 2. Set the bucket region. For abbreviations of COS regions, see https://intl.cloud.tencent.com/document/product/436/6224
// clientConfig contains the set methods to set region, HTTPS (HTTP by default), timeout, proxy, etc. For details, see the source code or the FAQs about Java SDK
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// 3. Generate a COS client.
COSClient cosClient = new COSClient(cred, clientConfig);
```

You can also use a temporary key to initialize COSClient. For more information on how to generate and use a temporary key, see [Generating and Using Temporary Keys](https://cloud.tencent.com/document/product/436/14048). Below is a sample:

[//]: # (.cssg-snippet-global-init-sts)
```java
// 1. Pass in the obtained temporary key (tmpSecretId, tmpSecretKey, sessionToken)
String tmpSecretId = "COS_SECRETID";
String tmpSecretKey = "COS_SECRETKEY";
String sessionToken = "COS_TOKEN";
BasicSessionCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);
// 2. Set the bucket region. For abbreviations of COS regions, see https://intl.cloud.tencent.com/document/product/436/6224
// clientConfig contains the set methods to set region, HTTPS (HTTP by default), timeout, and proxy, etc. For details, see the source code or the FAQs about Java SDK
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// 3. Generate a COS client
COSClient cosClient = new COSClient(cred, clientConfig);
```


The ClientConfig class is a configuration information class containing the following main members:

| Member Name | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------- |
| region | Constructor or set method | Bucket region. For abbreviations of COS regions, see [Regions and Access Domain Names](https://cloud.tencent.com/document/product/436/6224) | Region |
| httpProtocol | set method | The protocol used by the request. By default, HTTP is used to interact with COS | HttpProtocol |
| signExpired | set method | Validity period of the request signature, which is one hour by default | int |
| connectionTimeout | set method | Timeout period for connection with the COS service, which is 30 seconds by default | int |
| socketTimeout | set method | Timeout period for data reading by the client, which is 30 seconds by default | int |
| httpProxyIp | set method | Proxy server IP | String |
| httpProxyPort | set method | Proxy server port | int |


### Creating a bucket

After determining the region and bucket name, refer to the sample below to create a bucket:

[//]: # (.cssg-snippet-put-bucket-comp)
```java
String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
CreateBucketRequest createBucketRequest = new CreateBucketRequest(bucket);
// Set the bucket permission to PublicRead (public read and private write). Other options include private read/write and public read/write
createBucketRequest.setCannedAcl(CannedAccessControlList.PublicRead);
try{
    Bucket bucketResult = cosClient.createBucket(createBucketRequest);
} catch (CosServiceException serverException) {
    serverException.printStackTrace();
} catch (CosClientException clientException) {
    clientException.printStackTrace();
}
```

### Querying bucket list

Refer to the sample below to query the bucket list:

[//]: # (.cssg-snippet-get-service)
```java
List<Bucket> buckets = cosClient.listBuckets();
for (Bucket bucketElement : buckets) {
    String bucketName = bucketElement.getName();
    String bucketLocation = bucketElement.getLocation();
}
```

### Uploading an object

Upload a local file or input stream with a known length to COS. This is applicable to uploading small image files below 20 MB. The maximum file size allowed is 5 GB. For files over 5 GB, you need to use multipart upload or advanced APIs.

- If most of your local files are over 20 MB, we recommend you upload them with advanced APIs.
- If an object with the same key already exists in COS, it will be overwritten by the newly-uploaded one..
- To create a directory object, see [How to Create a Directory with the SDK](https://cloud.tencent.com/document/product/436/30746#sdk-.E5.A6.82.E4.BD.95.E5.88.9B.E5.BB.BA.E7.9B.AE.E5.BD.95.EF.BC.9F).
- An object key (Key) is a unique ID for an object in a bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/images/picture.jpg`, the object key is images/picture.jpg. For more information, see [Object Key](https://cloud.tencent.com/document/product/436/13324#.E5.AF.B9.E8.B1.A1.E9.94.AE).


Below is a sample of uploading a file below 5 GB:

[//]: # (.cssg-snippet-put-object)
```java
// Specify the file to be uploaded
File localFile = new File(localFilePath);
// Specify the destination bucket
String bucketName = "examplebucket-1250000000";
// Specify the key of the object to be uploaded to COS
String key = "exampleobject";
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
```

### Query the object list

Refer to the sample below to query the list of objects in a bucket:

[//]: # (.cssg-snippet-get-bucket)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// Setting bucket name
listObjectsRequest.setBucketName(bucket);
// The prefix indicates the key of the listed objects started with the prefix
listObjectsRequest.setPrefix("");
// The delimiter indicates the separator. Set "/" to list objects in the current directory; set to null to list all objects.
listObjectsRequest.setDelimiter("/");
// Setting the maximum number of traversed objects (up to 1000 for one listobject)
listObjectsRequest.setMaxKeys(1000);
ObjectListing objectListing = null;
do {
    try{
        ObjectListing objectListing = cosClient.listObjects(listObjectsRequest);
    } catch (CosXmlServiceException e) {
        e.printStackTrace();
        return;
    } catch (CosXmlClientException e) {
        e.printStackTrace();
        return;
    }
    // The common prefix indicates the path truncated by delimiter. If the delimiter is set to "/", the common prefix indicates the paths of all subdirectories
    List<String> commonPrefixs = objectListing.getCommonPrefixes();

    // The object summary indicates a list of all listed objects
    for (COSObjectSummary cosObjectSummary : objectListing.getObjectSummaries()) {
    for (COSObjectSummary cosObjectSummary : objectListing.getObjectSummaries()) {
        // File path key
        String key = cosObjectSummary.getKey();
        // File etag
        String etag = cosObjectSummary.getETag();
        // File length
        long fileSize = cosObjectSummary.getSize();
        // File storage type
        String storageClass = cosObjectSummary.getStorageClass();
    }

    String nextMarker = objectListing.getNextMarker();
    listObjectsRequest.setMarker(nextMarker);
} while (objectListing.isTruncated());
```

### Downloading an object
After an object is uploaded, you can use the same key to call the GetObject API to download the object. You can also generate a pre-signed link. (For a download operation, specify the method as GET. For more information, see [Pre-signed URL](https://cloud.tencent.com/document/product/436/35217)). This link can be shared for download. However, please be sure to check the validity period of the pre-signed link if your file is private-read.
Refer to the sample below to download a file to a specified local path:

[//]: # (.cssg-snippet-get-object)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
// Method 1: Get the input stream of the downloaded file
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
COSObject cosObject = cosClient.getObject(getObjectRequest);
COSObjectInputStream cosObjectInput = cosObject.getObjectContent();

// Method 2 (Download the file locally)
String outputFilePath = "exampleobject";
File downFile = new File(outputFilePath);
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
ObjectMetadata downObjectMeta = cosClient.getObject(getObjectRequest, downFile);
```

### Deleting an object

Delete an object in a specified path in COS with the following code:

[//]: # (.cssg-snippet-delete-object)
```java
// Enter the bucket name in the format of BucketName-APPID.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
cosClient.deleteObject(bucketName, key);
```

// Shutting down the client

Close cosClient and release the backend management thread connected to HTTP with the following code:

```java
// Shutting down the client (close the backend thread)
cosClient.shutdown();
```
