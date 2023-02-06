## Overview

This document provides an overview of APIs and SDK code samples for video tagging.

| API | Description |
| ------------------------------------------------------------ | ---------------- |
| [Submitting a video tagging job](https://intl.cloud.tencent.com/document/product/436/49062) | Submits a video tagging job. |


## Submitting Video Tagging Job

#### Feature description

This API is used to submit a video tagging job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model createMediaVideoTagJobs(array $args = array());
```

#### Sample request

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    // Submit a video tagging job. For more information, visit https://cloud.tencent.com/document/product/436/67202.
    $result = $cosClient->createMediaVideoTagJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Tag' => 'VideoTag',
        'QueueId' => 'p81e648af2aee496885707ca0xxxxxxxxx',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
            'VideoTag' => array(
                'Scenario' => 'Stream',
            ),
//            'UserData' => 'xxx', // The user information passed through.
//            'JobLevel' => '0', // Job priority. The greater the value, the higher the priority. Valid values: `0`, `1`, `2`. Default value: `0`.
        ),
        'CallBack' => '',
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :----------------------------------------------------------- | :-------- | :------- |
| Tag                | Request | Job tag: VideoTag                                   | String    | Yes   |
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule                                  | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |
| CallBackFormat     | Request | Job callback format, which can be `JSON` or `XML` (default value). It takes priority over that of the queue. | String | No |
| CallBackType       | Request | Job callback type, which can be `Url` (default value) or `TDMQ`. It takes priority over that of the queue.                    | String | No |
| CallBack           | Request | Job callback address, which takes priority over that of the queue. If it is set to `no`, no callbacks will be generated at the callback address of the queue. | String | No |
| CallBackMqConfig   | Request | TDMQ configuration for job callback as described in [Structure](https://intl.cloud.tencent.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :----------------------------------------------------------- | :----- | :------- |
| Object             | Request.Input | Name of the media file on which to perform the video tagging job. Currently, .mp4, .avi, .mkv, .wmv, .rmvb, .flv, and .mov formats are supported. For videos longer than 30 minutes, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance. | String | Yes |


`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :---------------------------- | :----------------------------------------------------------- | :-------- | :------- |
| VideoTag            | Request.Operation | `VideoTag` job parameter                                             | Container | Yes  |
| JobLevel            | Request.Operation | Job priority. The greater the value, the higher the priority. Valid values: `0`, `1`, `2`. Default value: `0`. | String | No |
| UserData           | Response.JobsDetail.Operation | The user information passed through.                      | String | No |

`VideoTag` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| :----------------- | :------------------------- | :----------------------------------------------------------- | :----- | :------- | :------------------------- |
| Scenario           | Request.Operation.VideoTag | Scenario type. You can select the application scenario of the video tag. The used algorithm, input, and output vary by scenario. | string | Yes | The current version is only adapted to the `Stream` scenario |

#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [Body] => GuzzleHttp\Psr7\Stream Object
        (
            [stream:GuzzleHttp\Psr7\Stream:private] => Resource id #88
            [size:GuzzleHttp\Psr7\Stream:private] => 
            [seekable:GuzzleHttp\Psr7\Stream:private] => 1
            [readable:GuzzleHttp\Psr7\Stream:private] => 1
            [writable:GuzzleHttp\Psr7\Stream:private] => 1
            [uri:GuzzleHttp\Psr7\Stream:private] => php://temp
            [customMetadata:GuzzleHttp\Psr7\Stream:private] => Array
                (
                )

        )

    [RequestId] => NjI2OTI2ZTdfZaOAUSIODUJAIODJAIODViNWQ=
    [ContentType] => application/xml
    [ContentLength] => 610
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-27T19:20:07+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-1250000000
                            [Object] => video01.mp4
                            [Region] => ap-guangzhou
                        )

                    [JobId] => jfe591374c61b11ec9ad8a098sd09asd8aa
                    [Message] => 
                    [Operation] => Array
                        (
                            [VideoTag] => Array
                                (
                                    [Scenario] => Stream
                                )
                            [UserData] => xxx
                            [JobLevel] => 0
                        )

                    [QueueId] => p81e648af2aeea8d90a8s90d8a0de086
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => VideoTag
                )

        )

)
```



