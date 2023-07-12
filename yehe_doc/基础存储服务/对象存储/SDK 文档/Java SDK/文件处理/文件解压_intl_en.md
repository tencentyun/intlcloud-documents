## Overview

This document provides an overview of APIs and SDK code samples for file decompression in CI.

| API | Description  |
|--------------------------------------------------------------------------------| --------------------------------- |
| [Submitting a file decompression job](https://intl.cloud.tencent.com/document/product/436/53993)   | Creates a file decompression job.        |
| [Querying the result of a file decompression job](https://intl.cloud.tencent.com/document/product/436/53994)  | Queries the result of a specified file decompression job. |

## Submitting a File Decompression Job

### Feature description

This API is used to submit a job to perform file decompression and asynchronously return decompressed files.

### Method prototype

```java
public FileProcessJobResponse createFileProcessJob(FileProcessRequest request);
```

### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:-----------------| :------ | :----------------------------------------------------------- | :-------- | :------- |
| tag                | Request | Job type. It is `FileUncompress` for file decompression by default.               | String    | Yes       |
| input              | Request | Information about the file to be operated                                         | Container | Yes   |
| operation          | Request | File decompression rule.                                 | Container | Yes       |
| queueId            | Request | ID of the queue where the job is in                                         | String    | Yes   |
| callBackFormat   | Request | Job callback format, which can be `JSON` or `XML` (default). It takes priority over that of the queue. | String | No |
| callBackType     | Request | Job callback type, which can be `Url` (default) or `TDMQ`. It takes priority over that of the queue.                    | String | No |
| callBack           | Request | Job callback address. It takes higher priority over that of the queue.                    | String    | No       |
| callBackMqConfig | Request | TDMQ configuration for job callback as described in [Structure](https://www.tencentcloud.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:----------| :------------ | :------------------------------------------- | :----- | :------- |
| object             | Request.Input | Filename, which is the full name of the file in the bucket.  | String | Yes       |

`operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---------------------| :---------------- | :---------------------------------------------- | :-------- | :------- |
| fileUncompressConfig | Request.Operation | File decompression rule                        | Container | Yes       |
| userData             | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| output               | Request.Operation | Information about the bucket where the decompressed file is stored            | Container | Yes       |

`FileUncompressConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---------------| :------------------------------------- | :----------------------------------------------------------- | :----- | :------- |
| prefix             | Request.Operation.FileUncompressConfig | Prefix of the input file after decompression. If this parameter is left empty, the file is stored in the root directory of the bucket by default.     | String | No       |
| prefixReplaced     | Request.Operation.FileUncompressConfig | Whether to replace the prefix of the directory of the decompressed file. Valid values:<br>- `0`: No additional prefix is added. The decompressed files are saved in the directory specified by `Prefix` (the name of the compressed package is not retained, and the file in the compressed package is saved to the specified directory only).<br>- `1`: The name of the compressed package is used as the prefix. The decompressed files are saved in the directory specified by `Prefix`.<br>- `2`: The full directory of the compressed package is used as the prefix. If `Prefix` is not specified, the file is decompressed to the current directory (including the name of the compressed package) of the compressed package.<br>- Default value: `0` | String | No       |

> Example:
> If the compressed package is named `test.zip`, contains the `image.jpg` file, and is stored in the `123` directory in bucket A, the full directory of the compressed package is `123/test.zip`.
> Decompress the package to bucket A with `Prefix` set to `456`. The storage directory of the decompressed file varies depending on the value of `PrefixReplaced`:
> `0`: The `image.jpg` file is stored in the `456` directory and its full directory is `456/image.jpg`.
> `1`: The `image.jpg` file is stored in the `456` directory with prefix `test` and its full directory is `456/test/image.jpg`.
> `2`: The `image.jpg` file is stored in the `456` directory with prefix `123/test` and its full directory is `456/123/test/image.jpg`.

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:----------| :----------------------- | :----------------------- | :----- | :------- |
| region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| bucket             | Request.Operation.Output | Bucket where the decompressed files are stored                                             | String | Yes   |

### Response description

- Success: The `FileProcessJobResponse` object response information is returned.
- Failure: An error (such as the bucket does not exist) occurs, throwing the "CosClientException" or
  "CosServiceException" exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Sample request

```java
//1. Create a job request object
FileProcessRequest request = new FileProcessRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("demo-1234567890");
request.setTag(FileProcessJobType.FileUncompress);
request.getInput().setObject("output/demo.zip");
FileUnCompressConfig fileUnCompressConfig = request.getOperation().getFileUnCompressConfig();
fileUnCompressConfig.setPrefix("output/");
fileUnCompressConfig.setPrefixReplaced("1");
request.setQueueId("p1ff062b35a494cf0ac4b572df22a5650");
MediaOutputObject output = request.getOperation().getOutput();
output.setBucket("demo-1234567890");
output.setRegion("ap-shanghai");
//3. Call the API to get the job response object
FileProcessJobResponse response = client.createFileProcessJob(request);
```

## Querying File Decompression Result

### Description

This API is used to query the details of a file processing job by job ID.

### Method prototype

```java
public FileProcessJobResponse describeFileProcessJob(FileProcessRequest request);
```

### Parameter description

| Parameter | Description | Type | Required |
| ---------- |----------------------------------------------------------------------------------------------------| ------ |-----|
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| jobId | ID of the job to be queried. | String | Yes |

### Response description

- Success: A job details response wrapper class is returned, which contains the job details object `FileProcessJobResponse`.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or
  "CosServiceException" exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Sample request

```java
//1. Create a job request object
FileProcessRequest request=new FileProcessRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("demo-1234567890");
request.setJobId("fda7eb1607b8411ed8c182156726*****");
//3. Call the API to get the job response object
FileProcessJobResponse response=client.describeFileProcessJob(request);
```
