## Overview

This document provides an overview of APIs and SDK code samples for submitting a screenshot job.

| API | Description |
| ------------- |  ---------------------- |
| [Submitting a screenshot job](https://www.tencentcloud.com/document/product/436/49055) | Submits a screenshot job. |


## Submitting Screenshot Job

#### Feature description

This API is used to submit a screenshot job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model createMediaSnapshotJobs(array $args = array());
```

#### Sample request

#### Sample 1. Using a template

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
    $result = $cosClient->createMediaSnapshotJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Tag' => 'Snapshot',
        'QueueId' => 'asdadadfafsdkjhfjghdfjg',
        'CallBack' => 'https://example.com/callback',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
            'TemplateId' => 'asdfafiahfiushdfisdhfuis',
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
                'Object' => 'snapshot-${Number}.jpg',
//                'SpriteObject' => 'sprite-${Number}.jpg',
            ),
//            'UserData' => 'xxx', // The user information passed through.
//            'JobLevel' => '0', // Job priority. The greater the value, the higher the priority. Valid values: `0`, `1`, `2`. Default value: `0`.
        ),
//        'CallBackMqConfig' => array(
//            'MqRegion' => '',
//            'MqMode' => '',
//            'MqName' => '',
//        ),
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 2. Customizing parameters

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
    $result = $cosClient->createMediaSnapshotJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Tag' => 'Snapshot',
        'QueueId' => 'asdadadfafsdkjhfjghdfjg',
        'CallBack' => 'https://example.com/callback',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
                'Object' => 'snapshot-${Number}.jpg',
            ),
            'Snapshot' => array(
                'Mode' => 'Average',
                'Start' => 3,
                'TimeInterval' => '',
                'Count' => 3,
                'Width' => '1280',
                'Height' => '',
            ),
//            'UserData' => 'xxx', // The user information passed through.
//            'JobLevel' => '0', // Job priority. The greater the value, the higher the priority. Valid values: `0`, `1`, `2`. Default value: `0`.
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

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :----------------------------------------------------------- | :-------- | :------- |
| Tag                | Request | Job tag: Snapshot                              | String    | Yes   |
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule                                  | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |
| CallBackFormat     | Request | Job callback format, which can be `JSON` or `XML` (default value). It takes priority over that of the queue. | String | No |
| CallBackType       | Request | Job callback type, which can be `Url` (default value) or `TDMQ`. It takes priority over that of the queue.                    | String | No |
| CallBack           | Request | Job callback address, which takes priority over that of the queue. If it is set to `no`, no callbacks will be generated at the callback address of the queue. | String | No |
| CallBackMqConfig   | Request | TDMQ configuration for job callback as described in [Structure](https://intl.cloud.tencent.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :--------- | :----- | :------- |
| Object             | Request.Input | Media filename | String | Yes   |


`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :---------------- | :----------------------------------------------------------- | :-------- | :------- |
| Snapshot                     | Request.Operation | Job type parameter. Same as `Request.Snapshot` in the screenshot template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49909).    | Container | No   |
| TemplateId                   | Request.Operation | Template ID                                        | String    | No  |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| JobLevel            | Request.Operation | Job priority. The greater the value, the higher the priority. Valid values: `0`, `1`, `2`. Default value: `0`. | String | No |

>!
>
> `TemplateId` is used first. If `TemplateId` is unavailable, `Snapshot` is used.

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------- | :----------------------------------------------------------- | :----- | :------- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Result filename. **${Number} must be included in the filename.** For example, you can set `Object` to `snapshot-${Number}.jpg`. | String | No   |
| SpriteObject       | Request.Operation.Output | Image sprite name. **${Number} must be included in the filename.** For example, you can set `sprite-${Number}.jpg`. Only the .jpg format is supported. | String | No   |

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

    [RequestId] => NjI2MTNkYAHDUIAHDRfNjQ0OF8yMGI4MjQ=
    [ContentType] => application/xml
    [ContentLength] => 829
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-beijing.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-21T19:19:25+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-1250000000
                            [Object] => video01.mp4
                            [Region] => ap-beijing
                        )

                    [JobId] => je6dcd3d6a80d98a09ds8ac4214b9b
                    [Message] => 
                    [Operation] => Array
                        (
                            [Output] => Array
                                (
                                    [Bucket] => examplebucket-1250000000
                                    [Object] => snapshot-${Number}.jpg
                                    [Region] => ap-beijing
                                    [SpriteObject] => 
                                )

                            [TemplateId] => t0778zc908zc908z0c8z0adcffd54a
                            [TemplateName] => snapshot_1280*720_3
                            [UserData] => xxx
                            [JobLevel] => 0
                        )

                    [QueueId] => p81e648afz7zc08c0z8xc09e086
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => Snapshot
                )

        )

)
```

