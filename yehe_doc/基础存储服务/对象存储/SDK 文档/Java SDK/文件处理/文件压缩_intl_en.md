## Overview

This document provides an overview of APIs and SDK code samples for multi-file zipping in CI.

| API | Description  |
|--------------------------------------------------------------------------------| ---------------------------------- |
| [Submitting a multi-file zipping job](https://intl.cloud.tencent.com/document/product/436/53995)   | Creates a multi-file zipping job.        |
| [Querying the result of a multi-file zipping job](https://intl.cloud.tencent.com/document/product/436/53996)  | Queries the result of a specified multi-file zipping job. |

## Submitting a Multi-File Zipping Job

### Feature description

The multi-file zipping feature uses a request to zip multiple files into a compressed file such as a ZIP file. You can submit a job to zip multiple files and asynchronously return the compressed file.

### Method prototype

```java
public FileProcessJobResponse createFileProcessJob(FileProcessRequest request);
```

### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:-----------------| :------ | :----------------------------------------------------------- | :-------- | :------- |
| tag                | Request | Job type. It is `FileCompress` for multi-file zipping by default.               | String    | Yes       |
| operation          | Request | File zipping rule.                                 | Container | Yes       |
| queueId            | Request | ID of the queue where the job is in                                         | String    | Yes   |
| callBackFormat   | Request | Job callback format, which can be `JSON` or `XML` (default). It takes priority over that of the queue. | String | No |
| callBackType     | Request | Job callback type, which can be `Url` (default) or `TDMQ`. It takes priority over that of the queue.                    | String | No |
| callBack           | Request | Job callback address. It takes higher priority over that of the queue.                    | String    | No       |
| callBackMqConfig   | Request | TDMQ configuration for job callback as described in [Structure](https://www.tencentcloud.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:-------------------| :---------------- | :---------------------------------------------- | :-------- | :------- |
| fileCompressConfig | Request.Operation | File zipping rule                    | Container | Yes       |
| userData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| output             | Request.Operation | Address where the compressed file is stored            | Container | Yes       |

`FileCompressConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:----------| :----------------------------------- | :----------------------------------------------------------- | :--------- | :------- |
| flatten            | Request.Operation.FileCompressConfig | Whether to remove the directory structure of the original file during file zipping. Valid values: <br><li>`0`: No. After file zipping, the original directory structure is retained. <br><li>`1`: Yes. After file zipping, the original directory structure is removed and all files are at the same level.<br>Assume that the original file URL is `https://domain/source/test.mp4` and the original file directory is `source/test.mp4`. If this parameter is set to `1`, the file directory in the ZIP file is `test.mp4`. If this parameter is set to `0`, the file directory in the ZIP file is `source/test.mp4`. | String     | Yes       |
| format             | Request.Operation.FileCompressConfig | Zipping type. Valid values: `zip`, `tar`, `tar.gz`                   | String     | Yes       |
| urlList            | Request.Operation.FileCompressConfig | <li>Files to be zipped can be sorted into an index file. The backend zips the files into a compressed file according to the file URL provided in the index file. <li>The index file must be saved in the current bucket, and this field must provide the object address of the index file, for example, `/test/index.csv`. <br><li>Index file format: Only CSV files in which one URL occupies one row (only files in the bucket are supported) are supported. If there are multiple columns, the first column is used as the URL by default. The number of files cannot exceed 10,000 and the total size cannot exceed 50 GB. Otherwise, the job will fail. | String     | No       |
| prefix             | Request.Operation.FileCompressConfig | Files with a specified prefix in the bucket can be zipped. To zip files in a specified directory, add / to the directory. For example, to zip files in the `test` directory, set this parameter to `test/`. The number of files cannot exceed 10,000 and the total size cannot exceed 50 GB. Otherwise, the job will fail. | String     | No       |
| key                | Request.Operation.FileCompressConfig | Multiple files in the bucket can be zipped. The number of files cannot exceed 1,000 and the total size cannot exceed 50 GB. Otherwise, the job will fail. | String array | No       |

> !Only one of UrlList, Prefix, and Key can be selected. They cannot all be empty or do not take effect at the same time. If multiple parameters are specified, the parameter with the highest priority prevails according to the priority UrlList > Prefix > Key.

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:----------| :----------------------- | :----------------------- | :----- | :------- |
| region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| bucket             | Request.Operation.Output | Bucket where the compressed file is stored                                             | String | Yes   |
| object             | Request.Operation.Output | Name of the compressed file                                             | String | Yes   |

### Response description

- Success: The `FileProcessJobResponse` object response information is returned.
- Failure: An error (such as the bucket does not exist) occurs, throwing the "CosClientException" or
  "CosServiceException" exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Sample request

```java
//1. Create a job request object
FileProcessRequest request=new FileProcessRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("demo-1234567890");
request.setTag(FileProcessJobType.FileCompress);
FileCompressConfig fileCompressConfig=request.getOperation().getFileCompressConfig();
fileCompressConfig.setFormat("zip");
fileCompressConfig.setFlatten("0");
List<String> keyList=fileCompressConfig.getKey();
keyList.add("mark/pic-1.jpg");
keyList.add("mark/pic-1.pdf");
//`QueueId` should be obtained in the console.
request.setQueueId("p1ff062b35a494cf0ac4b572df22****");
MediaOutputObject output=request.getOperation().getOutput();
output.setBucket("demo-1234567890");
output.setRegion("ap-shanghai");
output.setObject("output/demo.zip");
//3. Call the API to get the job response object
FileProcessJobResponse response=client.createFileProcessJob(request);
```

## Querying Multi-File Zipping Result

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
FileProcessRequest request = new FileProcessRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("demo-1234567890");
request.setJobId("fda7eb1607b8411ed8c182156726*****");
//3. Call the API to get the job response object
FileProcessJobResponse response = client.describeFileProcessJob(request);
```
