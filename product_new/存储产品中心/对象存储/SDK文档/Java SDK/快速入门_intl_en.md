## Download and Installation

### Relevant Resources
- The resources of COS XML Java SDK can be downloaded [here](https://github.com/tencentyun/cos-java-sdk-v5).
- The sample demo can be download [here](<https://github.com/tencentyun/cos-java-sdk-v5/tree/master/src/main/java/com/qcloud/cos/demo>).

### Environment Requirements
- The SDK supports JDK v1.7 and higher.
- For more information on JDK installation, see [Java Installation and Configuration](https://cloud.tencent.com/document/product/436/10865).

>- For the definitions of “SecretId”, “SecretKey”, “Bucket” and other terms, see [COS Glossary](https://intl.cloud.tencent.com/document/product/436/18507).
>- You can find the common classes in the COS Java SDK in the following packages:
>  1. The classes related to client configuration are in the package com.qcloud.cos.
>  2. The classes related to permissions are in the sub-package com.qcloud.cos.auth.
>  3. The classes related to exceptions are in the sub-package com.qcloud.cos.exception. 
>  4. The classes related to requests are in the sub-package com.qcloud.cos.model.
>  5. The classes related to regions are in the sub-package com.qcloud.cos.region.
>  6. The classes related to advanced APIs are in the sub-package com.qcloud.cos.transfer.
### Installing the SDK
You can install the SDK through Maven or source code:

- Install through Maven
  Add relevant dependencies to the pom.xml file of the Maven project as follows:
```shell
<dependency>
        <groupId>com.qcloud</groupId>
        <artifactId>cos_api</artifactId>
        <version>5.6.18</version>
</dependency>
```

- Install through source code
  Download the source code from [XML Java SDK](https://github.com/tencentyun/cos-java-sdk-v5) and import it via Maven. For example, in Eclipse, select **File** > **Import** > **Maven** > **Existing Maven Projects**.

### Uninstalling the SDK

Uninstall the SDK by removing the pom dependencies or source code.

## Getting Started

The section below describes how to perform basic operations with COS Java SDK, such as initializing a client, creating a bucket, querying the bucket list, uploading an object, querying the object list, downloading an object, and deleting an object.


### Importing Classes

The package name of COS Java SDK is `com.qcloud.cos.*`, and you can import the classes needed for program execution with IDE tools such as Eclipse and IntelliJ.

### Initializing a Client

Before executing any COS requests, an object of the COSClient class, which is used to call COS APIs, needs to be generated. Once a COSClient instance is generated, it is reusable and thread-safe. When the program or service exits, you need to close the client.

If you use a permanent key to initialize COSClient, you need to obtain your SecretId and SecretKey on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in the CAM Console. A permanent key can be used for most application scenarios. Below is a sample:

```java
// 1. Initialize the user credentials (secretId, secretKey)
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// 2. Set the bucket region. For abbreviations of COS regions, see https://cloud.tencent.com/document/product/436/6224
// clientConfig contains the set methods to set region, HTTPS (HTTP by default), timeout, proxy, etc. For details, see the source code or the FAQs about Java SDK
Region region = new Region("ap-guangzhou");
ClientConfig clientConfig = new ClientConfig(region);
// 3. Generate a COS client.
COSClient cosClient = new COSClient(cred, clientConfig);

```

You can also use a temporary key to initialize COSClient. For more information on how to generate and use a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048). Below is a sample:
```java
// 1. Pass in the obtained temporary key (tmpSecretId, tmpSecretKey, sessionToken)
String tmpSecretId = "COS_SECRETID";
String tmpSecretKey = "COS_SECRETKEY";
String sessionToken = "COS_TOKEN";
BasicSessionCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);
// 2. Set the bucket region. For abbreviations of COS regions, see https://cloud.tencent.com/document/product/436/6224
// clientConfig contains the set methods to set region, HTTPS (HTTP by default), timeout, and proxy, etc. For details, see the source code or the FAQs about Java SDK
Region region = new Region("ap-guangzhou");
ClientConfig clientConfig = new ClientConfig(region);
// 3. Generate a COS client
COSClient cosClient = new COSClient(cred, clientConfig);

```


The ClientConfig class is a configuration information class containing the following main members:

| Member Name | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------- |
| region | Constructor or set method | Bucket region. For abbreviations of COS regions, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | Region |
| httpProtocol | set method | The protocol used by the request. By default, HTTP is used to interact with COS | HttpProtocol |
| signExpired | set method | Validity period of the request signature, which is one hour by default | int |
| connectionTimeout | set method | Timeout period for connection with the COS service, which is 30 seconds by default | int |
| socketTimeout | set method | Timeout period for data reading by the client, which is 30 seconds by default | int |
| httpProxyIp | set method | Proxy server IP | String |
| httpProxyPort | set method | Proxy server port | int |


### Creating a Bucket

After determining the region and bucket name, refer to the sample below to create a bucket:

```java
Region region = new Region("ap-guangzhou");
ClientConfig clientConfig = new ClientConfig(region);
COSClient cosClient = new COSClient(cred, clientConfig);
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

### Querying the Bucket List

Refer to the sample below to query the bucket list:

```java
try {
    List<Bucket> buckets = cosClient.listBuckets();
    System.out.println(buckets);
} catch (CosServiceException serverException) {
    serverException.printStackTrace();
} catch (CosClientException clientException) {
    clientException.printStackTrace();
}
```

### Uploading an Object

Upload a local file or input stream with a known length to COS. This is applicable to uploading small image files below 20 MB. The maximum file size allowed is 5 GB. For files over 5 GB, you need to use multipart upload or advanced APIs.

- If most of your local files are over 20 MB, you are recommended to upload them with advanced APIs.
- If an object with the same key already exists in COS, it will be overwritten by the newly-uploaded one..
- To create a directory object, see [How to Create a Directory with the SDK](https://intl.cloud.tencent.com/document/product/436/10687).
- An object key (Key) is a unique ID for an object in a bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/images/picture.jpg`, the object key is images/picture.jpg. For more information, see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324#.E5.AF.B9.E8.B1.A1.E9.94.AE).


Below is a sample of uploading a file below 5 GB:

```java
try {
    // Specify the file to be uploaded
    File localFile = new File("exampleobject");
    // Specify the destination bucket
    String bucketName = "examplebucket-1250000000";
    // Specify the key of the object to be uploaded to COS
    String key = "exampleobject";
    PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
    PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
} catch (CosServiceException serverException) {
    serverException.printStackTrace();
} catch (CosClientException clientException) {
    clientException.printStackTrace();
}
```

### Querying the Object List

Refer to the sample below to query the list of objects in a bucket:

```java
try {
    String bucket = "examplebucket-1250000000";
    ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
    // Set the bucket name
    listObjectsRequest.setBucketName(bucket);
    // Prefix indicates that the object keys to be listed begin with prefix
    listObjectsRequest.setPrefix("");
    // Set the maximum number of objects to be traversed, which can be up to 1,000 in one listobject operation
    listObjectsRequest.setMaxKeys(1000);
    listObjectsRequest.setDelimiter("/");
    ObjectListing objectListing = cosClient.listObjects(listObjectsRequest);
    for (COSObjectSummary cosObjectSummary : objectListing.getObjectSummaries()) {
        // Object path key
        String key = cosObjectSummary.getKey();
        // Object etag
        String etag = cosObjectSummary.getETag();
        // Object length
        long fileSize = cosObjectSummary.getSize();
        // Object storage class
        String storageClass = cosObjectSummary.getStorageClass();
        System.out.println("key:" + key + "; etag:" + etag + "; fileSize:" + fileSize + "; storageClass:" + storageClass);
    }
} catch (CosServiceException serverException) {
    serverException.printStackTrace();
} catch (CosClientException clientException) {
    clientException.printStackTrace();
}
```

### Downloading an Object
After an object is uploaded, you can use the same key to call the GetObject API to download the object. You can also generate a pre-signed link. (For a download operation, specify the method as GET. For more information, see [Pre-signed URL](https://intl.cloud.tencent.com/document/product/436/31536)). This link can be shared for download. However, please be sure to check the validity period of the pre-signed link if your file is private-read.
Refer to the sample below to download a file to a specified local path:

```java
try{
    // Specify the bucket where the object is stored
    String bucketName = "examplebucket-1250000000";
    // Specify the key of the object in COS
    String key = "exampleobject";
    // Specify the destination local path
    File downFile = new File("D:\\exampleobject");
    GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
    ObjectMetadata downObjectMeta = cosClient.getObject(getObjectRequest, downFile);
} catch (CosServiceException serverException) {
    serverException.printStackTrace();
} catch (CosClientException clientException) {
    clientException.printStackTrace();
}
```

### Deleting an Object

Delete an object in a specified path in COS with the following code:

```java
try {
    // Specify the bucket where the object is stored
    String bucketName = "examplebucket-1250000000";
    // Specify the key of the object in COS
    String key = "exampleobject";
    cosClient.deleteObject(bucketName, key);
} catch (CosServiceException serverException) {
    serverException.printStackTrace();
} catch (CosClientException clientException) {
    clientException.printStackTrace();
}
```

### Closing a Client

Close cosClient and release the backend management thread connected to HTTP with the following code:

```java
// Close the client (close the backend thread)
cosClient.shutdown();
```
