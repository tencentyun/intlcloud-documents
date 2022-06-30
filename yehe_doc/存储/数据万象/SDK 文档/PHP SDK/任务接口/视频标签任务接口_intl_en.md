## Overview

This document provides an overview of APIs and SDK code samples for video tagging jobs.

| API | Description |
| ------------------------------------------------------------ | ---------------- |
| Submitting video tagging job | Submits video tagging job. |


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

$secretId = "SECRETID"; // Replace it with your real `secretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; // Replace it with your real `secretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with your real region information, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    // Submit a video tagging job: https://cloud.tencent.com/document/product/436/67202
    $result = $cosClient->createMediaVideoTagJobs(array(
        'Bucket' => 'examplebucket-125000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'VideoTag',
        'QueueId' => 'p81e648af2aee496885707ca0xxxxxxxxx',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
            'VideoTag' => array(
                'Scenario' => 'Stream',
            ),
        ),
        'CallBack' => '',
    ));
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :------------------------------------------------------ | :-------- | :------- |
| Tag                | Request | Job type: VideoTag                                   | String    | Yes   |
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule. Up to six jobs can be performed on the same file.                                                | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |
| CallBack           | Request | Callback address                                                | String    | No   |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :--------------------------- | :----- | :------- |
| Object             | Request.Input | Name of the media file to be tagged | String | Yes       |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :---------------- | :----------------------- | :-------- | :------- |
| VideoTag            | Request.Operation | `VideoTag` job parameter                                             | Container | Yes  |

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
    [Bucket] => examplebucket-125000000
    [Location] => examplebucket-125000000.ci.ap-guangzhou.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-27T19:20:07+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-125000000
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

                        )

                    [QueueId] => p81e648af2aeea8d90a8s90d8a0de086
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => VideoTag
                )

        )

)
```



