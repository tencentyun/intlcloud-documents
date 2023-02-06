## Overview
CI's media processing and file preview APIs are integrated into the COS XML Java SDK.

## Download and Installation

#### Relevant resources
- Download the COS XML Java SDK source code [here](https://github.com/tencentyun/cos-java-sdk-v5).
- Download the XML Java SDK [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-java-sdk-v5/latest/cos-java-sdk-v5.zip).
- Download the demo [here](https://github.com/tencentyun/cos-java-sdk-v5/tree/master/src/main/java/com/qcloud/cos/demo).
- For the complete sample code, please see [SDK Sample Code](https://github.com/tencentyun/cos-snippets/tree/master/Java).

#### Environmental dependencies
- The SDK supports JDK v1.8 and later.
- For the JDK installation, please see [Java Installation and Configuration](https://intl.cloud.tencent.com/document/product/436/10865).

>?
> - For the definitions of terms such as `SecretId`, `SecretKey`, and bucket, see [Introduction](https://intl.cloud.tencent.com/document/product/436/7751).
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
            <version>5.6.97</version>
</dependency>
```
	>?Dependency coordinates may not be on the latest version. Click [here](https://mvnrepository.com/artifact/com.qcloud/cos_api) to get the latest version.

- Using source code
  Download the source code from [GitHub](https://github.com/tencentyun/cos-java-sdk-v5) or [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-java-sdk-v5/latest/cos-java-sdk-v5.zip), and import it using Maven. For example, to import it into Eclipse, select **File** > **Import** > **Maven** > **Existing Maven Projects**.

#### Uninstalling SDK

Uninstall the SDK by removing the POM dependencies or source code.

## Getting Started

The section below describes how to use the Java SDK to perform basic operations, such as initializing a client, creating a bucket, querying a bucket list, uploading an object, querying an object list, downloading an object, or deleting an object. CI's media processing APIs are integrated into the COS XML Java SDK, where you can perform operations related to [templates](https://intl.cloud.tencent.com/document/product/1045/47020), jobs, [workflows](https://intl.cloud.tencent.com/document/product/1045/47022), and queues.

### Importing classes

The COS Java SDK package is named `com.qcloud.cos.*`. You can import the classes required for running your program through your IDE, such as Eclipse and IntelliJ.

### Initializing the client

Before making any request for COS services, you need to generate a COSClient class object for calling the COS APIs.

>!COSClient is a thread-safe class that allows multi-thread access to the same instance. Because an instance maintains a connection pool internally, creating multiple instances may lead to resource exhaustion. **Please ensure that there is only one instance in the program lifecycle**, and call the shutdown method to turn off the instance when it is no longer needed. If you need to create a new instance, shut down the previous instance first.

If you use a permanent key to initialize a `COSClient`, you need to get your `SecretId` and `SecretKey` on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in the CAM console. A permanent key is suitable for most application scenarios. Below is an example:

[//]: # ".cssg-snippet-global-init"
```java
// 1. Initialize the user credentials (secretId, secretKey).
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// 2. Set the bucket region. For the abbreviations of COS regions, see https://intl.cloud.tencent.com/document/product/436/6224.
// `clientConfig` contains the set methods to set region, HTTPS (HTTP by default), timeout, and proxy. For detailed usage, please see the source code or the FAQs about the SDK for Java.
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// 3. Generate a COS client.
COSClient cosClient = new COSClient(cred, clientConfig);
```

You can also use a temporary key to initialize the COSClient. For more information on how to generate and use a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048). An example is shown below:

[//]: # ".cssg-snippet-global-init-sts"
```java
// 1. Pass in the obtained temporary key (tmpSecretId, tmpSecretKey, sessionToken).
String tmpSecretId = "COS_SECRETID";
String tmpSecretKey = "COS_SECRETKEY";
String sessionToken = "COS_TOKEN";
BasicSessionCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);
// 2. Set the bucket region. For the abbreviations of COS regions, see https://intl.cloud.tencent.com/document/product/436/6224.
// `clientConfig` contains the set methods to set region, HTTPS (HTTP by default), timeout, and proxy. For detailed usage, please see the source code or the FAQs about the SDK for Java.
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// 3. Generate a COS client.
COSClient cosClient = new COSClient(cred, clientConfig);
```


The ClientConfig class is a configuration class containing the following main members:

| Member Name | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------- |
| region | Constructor or set method | Bucket region. For the abbreviations of COS regions, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/zh/document/product/436/6224) | Region |
| httpProtocol | Set method | The protocol used by the request. By default, HTTP is used to interact with COS. | HttpProtocol |
| signExpired | Set method | Validity period (in seconds) of the request signature. Default: 3600s | int |
| connectionTimeout | Set method | Timeout duration in milliseconds for connection with COS. Default value: `30000` ms | int |
| socketTimeout | Set method | Timeout duration in milliseconds for the client to read data. Default value: `30000` ms | int |
| httpProxyIp | Set method | Proxy server IP | String |
| httpProxyPort | Set method | Proxy server port | int |


### Querying the list of buckets with media processing enabled

This API is used to query buckets with media processing enabled under the current account.

#### Sample request

```java
 //1. Create a template request object
MediaBucketRequest request = new MediaBucketRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("examplebucket-1250000000");
//3. Call the API to get the bucket response object
MediaBucketResponse response = client.describeMediaBuckets(request);
```

### Creating a task

This API is used to create a media processing job.

#### Sample request

```java
//1. Create a job request object
MediaJobsRequest request = new MediaJobsRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("examplebucket-1250000000");
request.setTag("Transcode");
request.getInput().setObject("1.mp4");
request.getOperation().setTemplateId("t0e09a9456d4124542b1f0e44d501*****");
request.getOperation().getOutput().setBucket("examplebucket-1250000000");
request.getOperation().getOutput().setRegion("ap-chongqing");
request.getOperation().getOutput().setObject("2.mp4");
request.setQueueId("p9900025e4ec44b5e8225e70a521*****");
//3. Call the API to get the job response object
MediaJobResponse response = client.createMediaJobs(request);
```

### Canceling job

#### Feature description
This API is used to cancel a job that is not in progress.

```java
MediaJobsRequest request = new MediaJobsRequest();
request.setBucketName("examplebucket-1250000000");
request.setJobId("jae776cb4ec3011eab2cdd3817d4*****");
Boolean response = client.cancelMediaJob(request);
```

### Querying job

This API is used to query the details of a job by job ID.

```java
//1. Create a job request object
MediaJobsRequest request = new MediaJobsRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("examplebucket-1250000000");
request.setJobId("j29a82fea08ba11ebb54bc9d1c05*****");
//3. Call the API to get the job response object
MediaJobResponse response = client.describeMediaJob(request);
```

### Querying job list
This API is used to query the list of jobs in the queue.

#### Sample request

```java
MediaJobsRequest request = new MediaJobsRequest();
request.setBucketName("examplebucket-1250000000");
request.setQueueId("p9900025e4ec44b5e8225e70a521*****");
request.setTag("Transcode");
MediaListJobResponse response = client.describeMediaJobs(request);
List<MediaJobObject> jobsDetail = response.getJobsDetail();
```

### Shutting down the client

Shut down the COSClient and release the server threads connected over HTTP with the following code:

```java
// Close the client (release server threads).
cosClient.shutdown();
```
