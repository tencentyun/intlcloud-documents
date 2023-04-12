## Overview

This document provides an overview of APIs and SDK code samples for media processing queues.

| API | Description |
| ------------- |  ---------------------- |
| Searching for a media processing queue | Searches for a media processing queue. |
| Updating a media processing queue | Updates a media processing queue. |


## Searching for Media Processing Queue

#### Feature description

This API is used to search for media processing queues.

#### Method prototype

```php
public Guzzle\Service\Resource\Model describeMediaQueues(array $args = array());
```

#### Sample request

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual `region`, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    // https://cloud.tencent.com/document/product/436/54045: Searching for Media Processing Queue
    $result = $cosClient->describeMediaQueues(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
//        'QueueIds' => '', // Queue ID (optional). If you enter multiple IDs, separate them by comma.
//        'Category' => 'Transcoding', // Category (optional). `CateAll`: All types. `Transcoding`: Media processing queue. `SpeedTranscoding`: Media processing and accelerated transcoding queue. Default value: `Transcoding`.
//        'State' => 'Paused', // Status (optional). 1. `Active`: Jobs in the queue will be scheduled and executed for transcoding by the media transcoding service. 2. `Paused`: The queue is paused, and jobs in it will no longer be scheduled and executed. All jobs in the queue will remain in the `Paused` status, while jobs being executed will continue without being affected.
//        'PageNumber' => '1', // Page number (optional)
//        'PageSize' => '2', // Number of entries per page (optional)
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

Request parameters are as described below:

| Parameter Name (Keyword) | Description                                                         | Type   | Required |
| :----------------- | :----------------------------------------------------------- | :----- | :------- |
| QueueIds | Queue ID. If you enter multiple IDs, separate them by comma. | String | No |
| State              | <li> Active: Jobs in the queue will be scheduled and executed by the media processing service. <li>Paused: The queue is paused, and jobs in it will no longer be scheduled and executed. All jobs in the queue will remain in the `Paused` status, while jobs being executed will not be affected. | String | No     |
| Category | <li> CateAll: All types. <li> Transcoding: Media processing queue. <li> SpeedTranscoding: Media processing and accelerated transcoding queue. <li> Default value: `Transcoding`. | String | No |
| PageNumber         | Page number. Default value: `1`.   | String | No     |
| PageSize           | Number of entries per page. Default value: `10`. | String | No     |

#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjNkOGM2NmVfZTYxNmY5MSAASJPOJCIANSIDNAI=
    [ContentType] => application/xml
    [ContentLength] => 751
    [TotalCount] => 1
    [PageNumber] => 1
    [PageSize] => 10
    [QueueList] => Array
        (
            [0] => Array
                (
                    [BucketId] => examplebucket-1250000000
                    [QueueId] => pcc3ae89sa9d807fs89dg789sdg
                    [Name] => queue-1
                    [State] => Active
                    [MaxSize] => 10000
                    [MaxConcurrent] => 10
                    [Category] => Transcoding
                    [UpdateTime] => 2022-07-13T10:41:34+0800
                    [CreateTime] => 2022-07-13T10:41:34+0800
                    [NotifyConfig] => Array
                        (
                            [Url] => 
                            [State] => Off
                            [Type] => 
                            [Event] => 
                            [ResultFormat] => XML
                        )

                )

        )

    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/queue
)
```



## Updating Media Processing Queue

#### Feature description

This API is used to update a media processing queue.

#### Method prototype

```php
public Guzzle\Service\Resource\Model updateMediaQueue(array $args = array());
```

#### Sample request

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual `region`, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    // https://cloud.tencent.com/document/product/436/54046: Updating Media Processing Queue
    $result = $cosClient->updateMediaQueue(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'xxx', // queueId
        'Name' => '', // Template name. Length limit: 100 characters.
        'State' => 'Active', // Pipeline status
        'NotifyConfig' => array(
            'State' => 'Off',
//            'Event' => '',
//            'ResultFormat' => '',
//            'Type' => '',
//            'Url' => '',
//            'MqMode' => '',
//            'MqRegion' => '',
//            'MqName' => '',
        ),
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

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| :----------------- | :------ | :----------------------------------------------------------- | :-------- | :------- | :----- | :--- |
| Name             | Request | Queue name, which can contain up to 128 bytes.             | String    | Yes       | None     |  None   |
| State              | Request |<li> Active: Jobs in the queue will be scheduled and executed by the media processing service. <li> Paused: The queue is paused, and jobs in it will no longer be scheduled and executed. All jobs in the queue will remain in the `Paused` status, while jobs being executed will not be affected. | String      | Yes | None | None |
| NotifyConfig     | Request | Callback configuration                          | Container | Yes       | None     |  None   |

`NotifyConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| :----------------- | :------------------- | :--------------- | :----- | :--------------------------------- | :----- | :----------------------------------------------------------- |
| State        | Request.NotifyConfig | Callback status: `Off` or `On`. | String | No                 | Off  | On/Off |
| Event        | Request.NotifyConfig | Callback event         | String | Yes if `State` is `On`  | None   | Job completion: `TaskFinish`; workflow completion: `WorkflowFinish`. |
| ResultFormat | Request.NotifyConfig | Callback format         | String | No | XML   | JSON/XML |
| Type         | Request.NotifyConfig | Callback type         | String | Yes if `State` is `On` | None   | `Url` or `TDMQ` |
| Url          | Request.NotifyConfig | Callback address         | String | Yes if `State` is `On` and `Type` is `Url` | None   | The callback address cannot be a private network address. |
| MqMode       | Request.NotifyConfig | TDMQ queue mode    | String | Yes if `State` is `On` and `Type` is `TDMQ` | Queue | Topic: Topic subscription. Queue: Queue service. |
| MqRegion     | Request.NotifyConfig | TDMQ region    | String | Yes if `State` is `On` and `Type` is `TDMQ` | None   | Valid values: `sh` (Shanghai), `bj` (Beijing), `gz` (Guangzhou), `cd` (Chengdu), `hk` (Hong Kong, China). |
| MqName       | Request.NotifyConfig | TDMQ topic name    | String | Yes if `State` is `On` and `Type` is `TDMQ` | None   | None |

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

    [RequestId] => NjNkOGM2NmVfZTYxNmY5MSAASJPOJCIANSIDNAI=
    [ContentType] => application/xml
    [ContentLength] => 668
    [Key] => fcd32dbdaa13b11esa9ds8g0d98gd0h85
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/queue/fcd32dbdaa13b11esa9ds8g0d98gd0h85
    [Response] => Array
        (
            [RequestId] => NjNkOGM2NmVfZTYxNmY5MSAASJPOJCIANSIDNAI=
            [Queue] => Array
                (
                    [QueueId] => fcd32dbdaa13b11esa9ds8g0d98gd0h85
                    [Name] => media-queue-1
                    [State] => Active
                    [NotifyConfig] => Array
                        (
                            [Url] => 
                            [Event] => 
                            [Type] => 
                            [State] => Off
                            [ResultFormat] => XML
                            [MqMode] => 
                            [MqName] => 
                            [MqRegion] => 
                        )

                    [MaxSize] => 10000
                    [MaxConcurrent] => 10
                    [CreateTime] => 2022-07-13T10:41:34+0800
                    [UpdateTime] => 2023-01-31T17:32:18+0800
                    [BucketId] => examplebucket-1250000000
                    [Category] => Transcoding
                )

        )

)
```
