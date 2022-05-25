## Overview

This document provides an overview of APIs and SDK code samples for submitting a voice/sound separation job.

| API | Description |
| ------------- |  ---------------------- |
| Submitting voice/sound separation job | Submits voice/sound separation job |


## Submitting Voice/Sound Separation Job

#### Feature description

This API is used to submit a voice/sound separation job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model createMediaVoiceSeparateJobs(array $args = array());
```

#### Sample request

#### Sample 1. Using a template

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
    $result = $cosClient->createMediaVoiceSeparateJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'VoiceSeparate',
        'QueueId' => '',
        'CallBack' => '',
        'Input' => array(
            'Object' => 'test.mp3'
        ),
        'Operation' => array(
            'TemplateId' => '',
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
                'Object' => 'VoiceSeparate01.mp3',
                'AuObject' => 'VoiceSeparate02.mp3',
            ),
        ),
    ));
    // Request successful
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
    $result = $cosClient->createMediaVoiceSeparateJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'VoiceSeparate',
        'QueueId' => '',
        'CallBack' => '',
        'Input' => array(
            'Object' => 'test.mp3'
        ),
        'Operation' => array(
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
                'Object' => 'VoiceSeparate01.mp3',
                'AuObject' => 'VoiceSeparate02.mp3',
            ),
            'VoiceSeparate' => array(
                'AudioMode' => 'AudioAndBackground',
                'AudioConfig' => array(
                    'Codec' => 'mp3',
                    'Samplerate' => '11025',
                    'Bitrate' => '256',
                    'Channels' => '2',
                ),
            ),
        ),
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
| :----------------- | :------ | :---------------------------- | :-------- | :------- |
| Tag                | Request | Job type: VoiceSeparate                              | String    | Yes   |
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule                                  | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |
| CallBack           | Request | Callback address                                                | String    | No   |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :--------- | :----- | :------- |
| Object             | Request.Input | Media filename | String | Yes   |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :---------------- | :--------------- | :-------- | :------- |
| VoiceSeparate                | Request.Operation | Transcoding template parameter                                    | Container | No   |
| TemplateId                   | Request.Operation | Template ID                                        | String    | No  |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |

> !
>
> `TemplateId` is used with priority. If `TemplateId` is unavailable, the corresponding job type parameter is used.

`VoiceSeparate` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------------------------ | :----------------------------------------------------------- | :-------- | :------- |
| AudioMode        | Request.Operation.VoiceSeparate | Same as `Request.AudioMode` in the voice/sound separation template creation API `CreateMediaTemplate`.  | Container | No   |
| AudioConfig        | Request.Operation.VoiceSeparate | Same as `Request.AudioConfig` in the voice/sound separation template creation API `CreateMediaTemplate`.  | Container | No   |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------------------- | :----------------------------------------- | :----- | :------- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Background audio result filename. This node and `AuObject` cannot be empty at the same time.                  | String | No   |
| AuObject             | Request.Operation.AuObject | Voice/Sound result filename. This node and `Object` cannot be empty at the same time.                  | String | No   |

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

    [RequestId] => NjI2MjIyOTHADOHDOADJHOjQ0OV8yMmU0OWM=
    [ContentType] => application/xml
    [ContentLength] => 857
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-beijing.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-22T11:35:47+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-1250000000
                            [Object] => test.mp3
                            [Region] => ap-beijing
                        )

                    [JobId] => j4c70446zxc780z98xc09zxc6eb232
                    [Message] => 
                    [Operation] => Array
                        (
                            [Output] => Array
                                (
                                    [AuObject] => VoiceSeparate02.mp3
                                    [Bucket] => examplebucket-1250000000
                                    [Object] => VoiceSeparate01.mp3
                                    [Region] => ap-beijing
                                )

                            [TemplateId] => t1456ea89fczx8c0z8c09z8c0985
                            [TemplateName] => VoiceSeparate-1
                        )

                    [QueueId] => p81e648af2azc709zx8c09z8xc0z7be086
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => VoiceSeparate
                )

        )

)
```

