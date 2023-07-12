## Overview

This document provides an overview of APIs and SDK code samples for file decompression in CI.

>! The COS JavaScript SDK version must be v1.3.1 or later.
>

| API | Description  |
|--------------------------------------------------------------------------------| --------------------------------- |
| [Submitting a file decompression job](https://intl.cloud.tencent.com/document/product/436/53993)   | Creates a file decompression job.        |
| [Querying the result of a file decompression job](https://intl.cloud.tencent.com/document/product/436/53994)  | Queries the result of a specified file decompression job. |

## Submitting a File Decompression Job

#### Feature description

This API is used to submit a job to perform file decompression and asynchronously return decompressed files.

#### Sample code

```javascript
function postFileUnCompressTask() {
  var config = {
    // Replace with your own bucket information
    Bucket: 'examplebucket-1250000000', /* Bucket. Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
  };
  var host = config.Bucket + '.ci.' + config.Region + '.myqcloud.com/file_jobs';
  var url = 'https://' + host;
  var body = COS.util.json2xml({
    Request: {
      Tag: 'FileUncompress', // Required
      Input: {
        Object: 'compressed.zip', // Filename, which is the full name of the file in the bucket.
      },
      Operation: {
        FileUncompressConfig: {
          Prefix: '', // Prefix of the input file after decompression. If this parameter is left empty, the file is stored in the root directory of the bucket by default.
          PrefixReplaced: '0', // Whether to replace the prefix of the directory of the decompressed file. Default value: `0`.
        },
        Output: {
          Bucket: config.Bucket, // Bucket where the decompressed files are stored
          Region: config.Region, // Region of the bucket where the decompressed files are stored
        },
      },
      // QueueId: '', // ID of the queue where the job is in
      // CallBack: 'http://callback.demo.com', // Job callback address
      // CallBackFormat: 'JSON', // Job callback format
      // CallBackType: 'Url', // Job callback type, which can be `Url` (default) or `TDMQ`.
    }
  });
  cos.request({
      Method: 'POST',
      Key: 'file_jobs',
      Url: url,
      Body: body,
      ContentType: 'application/xml',
  },
  function(err, data){
      console.log(err || data);
  });
}
postFileUnCompressTask();
```

#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:-----------------| :------ | :----------------------------------------------------------- | :-------- | :------- |
| Tag                | Request | Job type. It is `FileUncompress` for file decompression by default.               | String    | Yes       |
| Input              | Request | Information about the file to be operated                                         | Container | Yes   |
| Operation          | Request | File decompression rule.                                 | Container | Yes       |
| QueueId            | Request | ID of the queue where the job is in                                         | String    | Yes   |
| CallBackFormat     | Request | Job callback format, which can be `JSON` or `XML` (default). It takes priority over that of the queue. | String | No |
| CallBackType       | Request | Job callback type, which can be `Url` (default) or `TDMQ`. It takes priority over that of the queue.                    | String | No |
| CallBack           | Request | Job callback address. It takes higher priority over that of the queue.                    | String    | No       |
| CallBackMqConfig   | Request | TDMQ configuration for job callback as described in [Structure > CallBackMqConfig](https://www.tencentcloud.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:----------| :------------ | :------------------------------------------- | :----- | :------- |
| Object             | Request.Input | Filename, which is the full name of the file in the bucket.  | String | Yes       |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---------------------| :---------------- | :---------------------------------------------- | :-------- | :------- |
| FileUncompressConfig | Request.Operation | File decompression rule                        | Container | Yes       |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| Output             | Request.Operation | Information about the bucket where the decompressed file is stored            | Container | Yes       |

`FileUncompressConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---------------| :------------------------------------- | :----------------------------------------------------------- | :----- | :------- |
| Prefix             | Request.Operation.FileUncompressConfig | Prefix of the input file after decompression. If this parameter is left empty, the file is stored in the root directory of the bucket by default.     | String | No       |
| PrefixReplaced     | Request.Operation.FileUncompressConfig | Whether to replace the prefix of the directory of the decompressed file. Valid values: <br><li>`0`: No additional prefix is added. The decompressed files are saved in the directory specified by `Prefix` (the name of the compressed package is not retained, and the file in the compressed package is saved to the specified directory only). <br><li>`1`: The name of the compressed package is used as the prefix. The decompressed files are saved in the directory specified by `Prefix`. <br><li>`2`: The full directory of the compressed package is used as the prefix. If `Prefix` is not specified, the file is decompressed to the current directory (including the name of the compressed package) of the compressed package. <br><li>Default value: `0` | String | No       |
>? If the compressed package is named `test.zip`, contains the `image.jpg` file, and is stored in the `123` directory in bucket A, the full directory of the compressed package is `123/test.zip`.
> Decompress the package to bucket A with `Prefix` set to `456`. The storage directory of the decompressed file varies depending on the value of `PrefixReplaced`:
- `0`: The `image.jpg` file is stored in the `456` directory and its full directory is `456/image.jpg`.
- `1`: The `image.jpg` file is stored in the `456` directory with prefix `test` and its full directory is `456/test/image.jpg`.
- `2`: The `image.jpg` file is stored in the `456` directory with prefix `123/test` and its full directory is `456/123/test/image.jpg`.

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:----------| :----------------------- | :----------------------- | :----- | :------- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Bucket where the decompressed files are stored                                             | String | Yes   |

#### Response description

For more information, see [Submitting a File Decompression Job](https://intl.cloud.tencent.com/document/product/436/53993).


## Querying File Decompression Result

#### Feature description

This API is used to query the details of a file processing job by job ID.

#### Sample code

```javascript
function getFileUnCompressTask() {
  var config = {
    // Replace with your own bucket information
    Bucket: 'examplebucket-1250000000', /* Bucket. Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
  };
  var jobId = 'xxxxxx'; // After the file decompression job is submitted, its `jobId` will be returned.
  var host = config.Bucket + '.ci.' + config.Region + '.myqcloud.com/file_jobs/' + jobId;
  var url = 'https://' + host;
  cos.request({
    Method: 'GET',
    Key: 'file_jobs/' + jobId,
    Url: url,
  },
  function(err, data){
      console.log(err || data);
  });
}
getFileUnCompressTask();
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------- |----------------------------------------------------------------------------------------------------| ------ |-----|
| jobId | ID of the job to be queried. | String | Yes |

#### Response description

For more information, see [Querying File Decompression Result](https://intl.cloud.tencent.com/document/product/436/53994).
