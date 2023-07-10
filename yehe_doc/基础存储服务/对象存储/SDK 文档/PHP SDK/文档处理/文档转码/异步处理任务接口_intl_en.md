## Overview

This document provides an overview of APIs and SDK code samples for async processing jobs.
>! COS PHP SDK v2.4.0 or later is required. Earlier versions may contain bugs and need to be upgraded to the [latest version](https://github.com/tencentyun/cos-php-sdk-v5/releases/) when used.
>


| API | Operation |  Description |
| :--------------- | :------------------ | :--------------------- |
| [CreateDocProcessJobs](https://intl.cloud.tencent.com/document/product/436/49407) | Submitting file preview job | Submits file preview job. |
| [DescribeDocProcessJob](https://intl.cloud.tencent.com/document/product/436/49408) |   Querying file preview job | Queries specified file preview job. |
| [DescribeDocProcessJobs](https://intl.cloud.tencent.com/document/product/436/49409) |  Pulling file preview jobs | Pulls eligible file preview jobs. |


## Submitting File Preview Job

#### Feature description
This API (`CreateDocProcessJobs`) is used to submit a file preview job.
>! 
>- Before using this API, make sure that the file processing feature has been enabled in the data processing section in the console; otherwise, the error `doc bucket unbinded, bucket's host is unavailable` will be reported.
>- To use the file to HTML conversion feature, directly put the request parameters after the URL. The SDK is only responsible for calculating the signature.
>

#### Sample code
```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; // Replace it with your actual `secretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$secretKey = "SECRETKEY"; // Replace it with your actual `secretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is `http` by default.
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    $result = $cosClient->createDocProcessJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'DocProcess', // Job type: DocProcess
        'QueueId' => 'pd8e422a2ea134165a92f2012ea43****', // Queue ID of the job
        'Input' => array(
            'Object' => 'Append Test Feature.pdf' // The object to be processed
        ),
        'Operation' => array(
            'DocProcess' => array(
                'SrcType' => 'pdf', // Source file extension
                'TgtType' => 'png', // Target file extension
                'SheetId' => 0, // Sheet parameter, indicating to convert the xth sheet. Default value: `1`.
                'StartPage' => 1, // Start page number, indicating to convert the file starting from the xth page. Default value: `1`.
                'EndPage' => 3, // End page number, indicating to convert the file till the Xth page. Default value: `-1` (convert all pages).
                'ImageParams' => '', // Image processing parameters after the conversion
                'DocPassword' => '', // Office file password
                'Comments' => 0, // Whether to hide comments and apply track changes. Default value: `0`.
                'PaperDirection' => 0, // Paper orientation of the spreadsheet. Default value: `0`.
                'Quality' => 100, // Quality of the generated preview image. Value range: [1-100]. Default value: `100`.
                'Zoom' => 100, // Scaling parameter of the preview image. Value range: [10-200]. Default value: `100`.
            ),
            'Output' => array(
                'Region' => $region, // Bucket region
                'Bucket' => 'examplebucket-1250000000', // Result storage bucket
                'Object' => 'pic-${Page}.jpg', // Output file path
            ),
        ),
    ));
    // The request succeeded.
    print_r($result);
} catch (\Exception $e) {
    // The request failed.
    echo($e);
}
```

#### Parameter description

`Request` has the following sub-nodes:

| Parameter | Type | Description | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Operation | Array| Operation rule | Yes |
| Tag | String|  Job type, which currently can only be `DocProcess`.	 | Yes |
| Input | Array|  The object to be processed	 | Yes |
| QueueId | String|  Queue ID of the job | Yes |

`Input` has the following sub-nodes:

| Parameter | Type | Description | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- |
| Object               |String|  File URL in COS. `Bucket` is specified by `Host`.	          | Yes       |

`Operation` has the following sub-nodes:

| Parameter | Type | Description | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- |
| DocProcess       | Array | Specifies the parameter for the job, which takes effect only if `Tag` is `DocProcess`.	 | Yes |
| Output | Array| Result output address	 | Yes |

`DocProcess` has the following sub-nodes:

| Parameter | Type | Description | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- |
| srcType        | String | Source data type. Currently, the file conversion feature determines the source data type according to the file extension of the COS object. If the object has no extension, you can set this value. | No |
| tgtType        | String | Type of the output target file. Valid values: `png`, `jpg`, `pdf`. If the input file format cannot be recognized, the `jpg` format will be used by default. You cannot specify pages for the `pdf` format.  | No |
| sheetId        | Integer | Sheet parameter, indicating to convert the xth sheet. Default value: `1`. If this value is set to `0`, all sheets will be converted. | No |
| startPage      | Integer | Starts conversion from page X. A spreadsheet file may be split into multiple pages, with multiple images generated, and `StartPage` indicates to start the conversion from page X of the specified `SheetId`. Default value: `1`. | No |
| endPage        | Integer | Ends conversion on page X. A spreadsheet file may be split into multiple pages, with multiple images generated, and `EndPage` indicates to end the conversion on page X of the specified `SheetId`. Default value: `-1` (converting all pages).  | No |
| imageParams    | String | Processing parameters for the output image. All parameters of [basic image processing](https://www.tencentcloud.com/document/product/436/36365) are supported. To specify multiple parameters, separate them by [pipeline operator](https://intl.cloud.tencent.com/document/product/436/36380). In this way, the image can be processed by multiple parameters in sequence in the same request. | No |
| docPassword    | String | Password to open the Office file. If you need to convert a password-protected file, set this field. | No |
| comments       | Integer | Whether to hide comments and apply track changes. 0: Hide comments and apply track changes; 1: Show comments and track changes. Default value: `0`. | No |
| paperDirection | Integer | Paper orientation of the spreadsheet. 0: Vertical; other values: Horizontal. Default value: `0`. | No |
| quality        | Integer | Quality of the generated preview image. Value range: [1-100]. Default value: `100`. For example, if the value is 100, the quality of the generated image will be 100%. | No |
| zoom           | Integer | Scaling parameter of the preview image. Value range: [10, 200]. Default value: `100`. For example, if the value is 200, the image will be scaled up (enlarged) by 200%. | No |

`Output` has the following sub-nodes:

| Parameter | Type | Description | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- |
| Region               | String | Bucket region                           | Yes       |
| Bucket | String| Result storage bucket | Yes |
| Object | String|  Output file path	 | Yes |


#### Response parameter description

| Parameter                  | Type      | Description                                                |
| ------------ | ------------------------------------------------------------ | ------------------ |
| Code         | String             | Error code, which will be returned only if `State` is `Failed`.                        |
| Message      | String             | Error message, which will be returned only if `State` is `Failed`.                      |
| JobId        | String             | Job ID                                              |
| Tag          | String             | Job type: DocProcess                                 |
| State        | String  | Job status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. |
| CreationTime | String             | Job creation time                                               |
| QueueId      | String             | ID of the queue which the job is in                                            |
| Input        | Array   | Input file path of the job                                         |
| Operation    | Array | Operation rule                                                 |

## Querying Specified File Preview Job

#### Feature description
This API (`DescribeDocProcessJob`) is used to query a specified file preview job.

#### Sample code
```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; // Replace it with your actual `secretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$secretKey = "SECRETKEY"; // Replace it with your actual `secretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is `http` by default.
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    $result = $cosClient->describeDocProcessJob(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'examplejobid', // JobId
    ));
    // The request succeeded.
    print_r($result);
} catch (\Exception $e) {
    // The request failed.
    echo($e);
}
```

#### Parameter description

| Parameter | Type | Description |
| ---------- | -------------- | ------ |
| Bucket | COS bucket name | String |
| Key      | Job ID  | String |

#### Response parameter description

| Parameter | Type | Description |
| ---------- | ------------------ | ------------ |
| jobsDetail | Job details | Array |


## Pulling File Preview Job

#### Feature description
The API (`DescribeDocProcessJobs`) is used to pull file preview jobs that meet specified conditions.

#### Sample code
```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; // Replace it with your actual `secretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$secretKey = "SECRETKEY"; // Replace it with your actual `secretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is `http` by default.
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    $result = $cosClient->getDescribeDocProcessJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'QueueId' => 'pd8e422a2ea134165a92f2012ea43****', // ID of the queue from which jobs are pulled
        'Tag' => 'DocProcess', // Job type: DocProcess
//      'NextToken' => '143486', // Context token for pagination
//      'OrderByTime' => 'Desc', // `Desc` (default) or `Asc`
//      'Size' => 2, // Maximum number of jobs that can be pulled. Default value: `10`. Maximum value: `100`.
//      'States' => 'All', // Status of the jobs to pull. If you enter multiple job statuses, separate them by comma. Valid values: `All` (default), `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`.
//      'StartCreationTime' => '2021-10-10T16:20:07+0800', // Start time of the time range for job pulling
//      'EndCreationTime' => '2021-10-10T16:20:07+0800', // End time of the time range for job pulling
    ));
    // The request succeeded.
    print_r($result);
} catch (\Exception $e) {
    // The request failed.
    echo($e);
}
```

#### Parameter description

| Parameter | Type | Description | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- |
| Bucket            | String  | COS bucket name                                               | Yes |
| QueueId           | String  | ID of the queue from which jobs are pulled      | Yes |
| Tag               | String  | Job type: DocProcess                                       | Yes |
| OrderByTime       | String  | `Desc` (default) or `Asc`                                   | No |
| NextToken         | String  | Context token for pagination                   | No |
| Size              | Integer | Maximum number of jobs that can be pulled. The default value is 10. The maximum value is 100.                        | No |
| States            | String  | Status of the jobs to pull. If you enter multiple job statuses, separate them by comma. Valid values: `All` (default), `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. | No |
| StartCreationTime | String  | Start time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`.  | No |
| EndCreationTime   | String  | End time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`.  | No |


#### Response parameter description

| Parameter | Type | Description |
| ---------------- | ------------------ | ------------------ |
| JobDetail | Array | List of job details       |
| nextToken | String     | Context token for pagination |
