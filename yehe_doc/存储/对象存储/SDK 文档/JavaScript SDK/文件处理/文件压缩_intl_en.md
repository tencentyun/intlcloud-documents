## Overview

This document provides an overview of APIs and SDK code samples for file compression in CI.

>! The COS JavaScript SDK version must be v1.3.1 or later.
>

| API | Description  |
|--------------------------------------------------------------------------------| ---------------------------------- |
| [Submitting a multi-file zipping job](https://intl.cloud.tencent.com/document/product/436/53995)   | Creates a multi-file zipping job.        |
| [Querying the result of a multi-file zipping job](https://intl.cloud.tencent.com/document/product/436/53996)  | Queries the result of a specified multi-file zipping job. |

## Submitting a Multi-File Zipping Job

#### Feature description

The multi-file zipping feature uses a request to zip multiple files into a compressed file such as a ZIP file. You can submit a job to zip multiple files and asynchronously return the compressed file.

#### Sample code

```javascript
function postFileCompressTask() {
  var config = {
    // Replace with your own bucket information
    Bucket: 'examplebucket-1250000000', /* Bucket. Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
  };
  var host = config.Bucket + '.ci.' + config.Region + '.myqcloud.com/file_jobs';
  var url = 'https://' + host;
  var body = COS.util.json2xml({
    Request: {
      Tag: 'FileCompress', // Required
      Operation: {
        FileCompressConfig: {
          Flatten: '0', // Whether to remove the directory structure of the original file during file zipping. Valid values: `0` (no); `1` (yes).
          Format: 'zip', // Zipping type. Valid values: `zip`, `tar`, `tar.gz`.
          // Only one of UrlList, Prefix, and Key can be selected. They cannot all be empty or do not take effect at the same time.
          // UrlList: '', // Object address of the index file
          Prefix: 'testCompress/', // Directory prefix
          // Key: [], // Multiple files in the bucket can be zipped. The number of files cannot exceed 1,000 and the total size cannot exceed 50 GB. Otherwise, the job will fail.
        },
        Output: {
          Bucket: config.Bucket, // Bucket where the compressed file is stored
          Region: config.Region, // Region of the bucket where the compressed file is stored
          Object: 'testCompress/compressed.zip', // Name of the compressed file	
        },
        UserData: '',
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
postFileCompressTask();
```

#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:-----------------| :------ | :----------------------------------------------------------- | :-------- | :------- |
| Tag                | Request | Job type. It is `FileCompress` for multi-file zipping by default.               | String    | Yes       |
| Operation          | Request | File zipping rule.                                 | Container | Yes       |
| QueueId            | Request | ID of the queue where the job is in                                         | String    | No   |
| CallBackFormat     | Request | Job callback format, which can be `JSON` or `XML` (default). It takes priority over that of the queue. | String | No |
| CallBackType       | Request | Job callback type, which can be `Url` (default) or `TDMQ`. It takes priority over that of the queue.                    | String | No |
| CallBack           | Request | Job callback address. It takes higher priority over that of the queue.                    | String    | No       |
| CallBackMqConfig   | Request | TDMQ configuration for job callback as described in [Structure](https://www.tencentcloud.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:-------------------| :---------------- | :---------------------------------------------- | :-------- | :------- |
| FileCompressConfig | Request.Operation | File zipping rule                    | Container | Yes       |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| Output             | Request.Operation | Address where the compressed file is stored            | Container | Yes       |

`FileCompressConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:----------| :----------------------------------- | :----------------------------------------------------------- | :--------- | :------- |
| Flatten            | Request.Operation.FileCompressConfig | Whether to remove the directory structure of the original file during file zipping. Valid values: <br><li>`0`: No. After file zipping, the original directory structure is retained. <br><li>`1`: Yes. After file zipping, the original directory structure is removed and all files are at the same level.<br>Assume that the original file URL is `https://domain/source/test.mp4` and the original file directory is `source/test.mp4`. If this parameter is set to `1`, the file directory in the ZIP file is `test.mp4`. If this parameter is set to `0`, the file directory in the ZIP file is `source/test.mp4`. | String     | Yes       |
| Format             | Request.Operation.FileCompressConfig | Zipping type. Valid values: `zip`, `tar`, `tar.gz`                   | String     | Yes       |
| UrlList            | Request.Operation.FileCompressConfig | <li>Files to be zipped can be sorted into an index file. The backend zips the files into a compressed file according to the file URL provided in the index file. The index file must be saved in the current bucket, and this field must provide the object address of the index file, for example, `/test/index.csv`. <br><li>Index file format: Only CSV files in which one URL occupies one row (only files in the bucket are supported) are supported. If there are multiple columns, the first column is used as the URL by default. The number of files cannot exceed 10,000 and the total size cannot exceed 50 GB. Otherwise, the job will fail. | String     | No       |
| Prefix             | Request.Operation.FileCompressConfig | Files with a specified prefix in the bucket can be zipped. To zip files in a specified directory, add / to the directory. For example, to zip files in the `test` directory, set this parameter to `test/`. The number of files cannot exceed 10,000 and the total size cannot exceed 50 GB. Otherwise, the job will fail. | String     | No       |
| Key                | Request.Operation.FileCompressConfig | Multiple files in the bucket can be zipped. The number of files cannot exceed 1,000 and the total size cannot exceed 50 GB. Otherwise, the job will fail. | String array | No       |

> !Only one of UrlList, Prefix, and Key can be selected. They cannot all be empty or do not take effect at the same time. If multiple parameters are specified, the parameter with the highest priority prevails according to the priority UrlList > Prefix > Key.

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:----------| :----------------------- | :----------------------- | :----- | :------- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Bucket where the compressed file is stored                                             | String | Yes   |
| Object             | Request.Operation.Output | Name of the compressed file                                             | String | Yes   |

#### Response description

For more information, see [Submitting a Multi-File Zipping Job](https://intl.cloud.tencent.com/document/product/436/53995#.E5.93.8D.E5.BA.94).


## Querying Multi-File Zipping Result

#### Feature description

This API is used to query the details of a file processing job by job ID.

#### Sample code

```javascript
function getFileCompressTask() {
  var config = {
    // Replace with your own bucket information
    Bucket: 'examplebucket-1250000000', /* Bucket. Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
  };
  var jobId = 'xxxxxx'; // After the multi-file zipping job is submitted, its `jobId` will be returned.
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
getFileCompressTask();
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------- |----------------------------------------------------------------------------------------------------| ------ |-----|
| jobId | ID of the job to be queried. | String | Yes |

#### Response description

For more information, see [Querying Multi-File Zipping Result](https://intl.cloud.tencent.com/document/product/436/53996).

