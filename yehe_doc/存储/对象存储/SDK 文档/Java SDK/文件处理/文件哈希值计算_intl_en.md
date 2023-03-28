## Overview

This document provides an overview of APIs and SDK code samples for hash calculation in CI.

| API | Description  |
|--------------------------------------------------------------------------------| --------------------------------- |
| [Submitting a hash calculation job](https://intl.cloud.tencent.com/document/product/436/53991)   | Creates a hash calculation job.        |
| [Querying the result of a hash calculation job.](https://intl.cloud.tencent.com/document/product/436/53992)  | Queries the result of a specified hash calculation job. |

## Submitting a Hash Calculation Job

#### Feature description

This API is used to submit a job to perform hash calculation and asynchronously return a calculated hash value.

#### Method prototype

```java
public FileProcessJobResponse createFileProcessJob(FileProcessRequest request);
```

#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:-----------------| :------ | :----------------------------------------------------------- | :-------- | :------- |
| tag                | Request | Job type. It is `FileHashCode` for hash calculation.             | String    | Yes       |
| operation          | Request | Hash calculation rule                                   | Container | Yes       |
| queueId            | Request | ID of the queue where the job is in                                         | String    | Yes   |
| callBackFormat   | Request | Job callback format, which can be `JSON` or `XML` (default). It takes priority over that of the queue. | String | No |
| callBackType     | Request | Job callback type, which can be `Url` (default) or `TDMQ`. It takes priority over that of the queue.                    | String | No |
| callBack           | Request | Job callback address. It takes higher priority over that of the queue.                    | String    | No       |
| callBackMqConfig   | Request | TDMQ configuration for job callback as described in [Structure](https://www.tencentcloud.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:----------| :------------ | :------------------------------------------- | :----- | :------- |
| object             | Request.Input | Filename, which is the full name of the file in the bucket.  | String | Yes       |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:-------------------| :---------------- | :---------------------------------------------- | :-------- | :------- |
| fileHashCodeConfig | Request.Operation | Hash calculation rule                      | Container | Yes       |
| userData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |

`FileHashCodeConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:------------| :----------------------------------- | :----------------------------------------------------------- | :----- | :------- |
| type               | Request.Operation.FileHashCodeConfig | Hash algorithm. Valid values: `MD5`, `SHA1`, `SHA256`                | String | Yes       |
| addToHeader | Request.Operation.FileHashCodeConfig | Whether to add the calculated hash value to the custom header in the file. Valid values: `true`, `false` (default)<br>The custom header varies depending on `Type`. For example, if `Type` is `MD5`, the custom header is `x-cos-meta-md5`. | String | No       |


#### Response description

- Success: The `FileProcessJobResponse` object response information is returned.
- Failure: An error (such as the bucket does not exist) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://www.tencentcloud.com/document/product/436/31537).

#### Sample request

```java
//1. Create a job request object
FileProcessRequest request = new FileProcessRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("demo-1234567890");
request.setTag(FileProcessJobType.FileHashCode);
request.getInput().setObject("input/1.mp4");
FileHashCodeConfig fileHashCodeConfig = request.getOperation().getFileHashCodeConfig();
fileHashCodeConfig.setType("MD5");
fileHashCodeConfig.setAddToHeader("true");
request.setQueueId("p1ff062b35a494cf0ac4b572df22a****");
//3. Call the API to get the job response object
FileProcessJobResponse response = client.createFileProcessJob(request);
```

## Querying Hash Calculation Result

#### Feature description

This API is used to query the details of a file processing job by job ID.

#### Method prototype

```java
public FileProcessJobResponse describeFileProcessJob(FileProcessRequest request);
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------- |----------------------------------------------------------------------------------------------------| ------ |-----|
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| jobId | ID of the job to be queried. | String | Yes |

#### Response description

- Success: A job details response wrapper class is returned, which contains the job details object `FileProcessJobResponse`.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://www.tencentcloud.com/document/product/436/31537).

#### Sample request

```java
//1. Create a job request object
FileProcessRequest request = new FileProcessRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("demo-1234567890");
request.setJobId("fda7eb1607b8411ed8c182156726*****");
//3. Call the API to get the job response object
FileProcessJobResponse response = client.describeFileProcessJob(request);
```

