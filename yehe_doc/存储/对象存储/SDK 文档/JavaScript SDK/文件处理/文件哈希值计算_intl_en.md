## Overview

This document provides an overview of APIs and SDK code samples for hash calculation in CI.

>! The COS JavaScript SDK version must be v1.3.1 or later.
>

| API | Description  |
|--------------------------------------------------------------------------------| --------------------------------- |
| [Submitting a hash calculation job](https://intl.cloud.tencent.com/document/product/436/53991)   | Creates a hash calculation job.        |
| [Querying the result of a hash calculation job.](https://intl.cloud.tencent.com/document/product/436/53992)  | Queries the result of a specified hash calculation job. |

## Submitting a Hash Calculation Job

#### Feature description

You can submit a job to perform hash calculation and asynchronously return a calculated hash value.

#### Sample code

```javascript
function postFileHashTask() {
  var config = {
    // Replace with your own bucket information
    Bucket: 'examplebucket-1250000000', /* Bucket. Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
  };
  var host = config.Bucket + '.ci.' + config.Region + '.myqcloud.com/file_jobs';
  var url = 'https://' + host;
  var body = COS.util.json2xml({
    Request: {
      Tag: 'FileHashCode', // Required
      Input: {
        Object: 'test/1.pdf', // Filename, which is the full name of the file in the bucket.
      },
      Operation: {
        FileHashCodeConfig: {
          Type: 'MD5', // Hash algorithm. Valid values: `MD5`, `SHA1`, `SHA256`.
          AddToHeader: 'false', // Whether to add the calculated hash value to the custom header in the file. Valid values: `true`, `false` (default).
        },
        // UserData: '', // The user information passed through, which is printable ASCII codes of up to 1,024 in length.
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
postFileHashTask();
```

#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:-----------------| :------ | :----------------------------------------------------------- | :-------- | :------- |
| Tag                | Request | Job type. It is `FileHashCode` for hash calculation.             | String    | Yes       |
| Operation          | Request | Hash calculation rule                                   | Container | Yes       |
| QueueId            | Request | ID of the queue where the job is in                                         | String    | Yes   |
| CallBackFormat     | Request | Job callback format, which can be `JSON` or `XML` (default). It takes priority over that of the queue. | String | No |
| CallBackType       | Request | Job callback type, which can be `Url` (default) or `TDMQ`. It takes priority over that of the queue.                    | String | No |
| CallBack           | Request | Job callback address. It takes higher priority over that of the queue.                    | String    | No       |
| CallBackMqConfig   | Request | TDMQ configuration for job callback as described in [Structure](https://www.tencentcloud.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:----------| :------------ | :------------------------------------------- | :----- | :------- |
| Object             | Request.Input | Filename, which is the full name of the file in the bucket.  | String | Yes       |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:-------------------| :---------------- | :---------------------------------------------- | :-------- | :------- |
| FileHashCodeConfig | Request.Operation | Hash calculation rule                      | Container | Yes       |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |

`FileHashCodeConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:------------| :----------------------------------- | :----------------------------------------------------------- | :----- | :------- |
| Type               | Request.Operation.FileHashCodeConfig | Hash algorithm. Valid values: `MD5`, `SHA1`, `SHA256`                | String | Yes       |
| AddToHeader | Request.Operation.FileHashCodeConfig | Whether to add the calculated hash value to the custom header in the file. Valid values: `true`, `false` (default)<br>The custom header varies depending on `Type`. For example, if `Type` is `MD5`, the custom header is `x-cos-meta-md5`. | String | No       |


#### Response description

For more information, see [Submitting Hash Calculation Job](https://intl.cloud.tencent.com/document/product/436/53991).


## Querying Hash Calculation Result

#### Feature description

This API is used to query the details of a file processing job by job ID.

#### Sample code

```javascript
function getFileHashTask() {
  var config = {
    // Replace with your own bucket information
    Bucket: 'examplebucket-1250000000', /* Bucket. Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
  };
  var jobId = 'xxxxxx'; // After the file has calculation job is submitted, its `jobId` will be returned.
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
getFileHashTask();
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------- |----------------------------------------------------------------------------------------------------| ------ |-----|
| jobId | ID of the job to be queried. | String | Yes |

#### Response description

For more information, see [Querying Hash Calculation Result](https://intl.cloud.tencent.com/document/product/436/53992).
