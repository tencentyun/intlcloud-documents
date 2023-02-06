## Overview

This document provides an overview of APIs and SDK code samples for submitting a transcoding job.

| API | Description |
| ------------- |  ---------------------- |
| [Submitting transcoding job](https://www.tencentcloud.com/document/product/436/49058) | Submits transcoding job |


## Submitting Transcoding Job

#### Feature description

Submitting a Transcoding Task

#### Method prototype

```php
public Guzzle\Service\Resource\Model createMediaTranscodeJobs(array $args = array());
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
    $result = $cosClient->createMediaTranscodeJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Tag' => 'Transcode',
        'QueueId' => 'paaf4fce5521a40888a3034a5de80f6ca',
        'Input' => array(
            'Object' => 'example.mp4'
        ),
        'Operation' => array(
            'TemplateId' => 't04e1ab86554984f1aa17c062fbf6c007c',
//            'UserData' => 'xxx', // The user information passed through.
//            'JobLevel' => '0', // Job priority. The greater the value, the higher the priority. Valid values: `0`, `1`, `2`. Default value: `0`.
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
                'Object' => 'video02.mp4',
            ),
            'Watermark' => array(
                array(
                    'Type' => 'Text',
                    'LocMode' => 'Absolute',
                    'Dx' => '64',
                    'Dy' => '64',
                    'Pos' => 'TopRight',
                    'Text' => array(
                        'Text' => 'The first watermark',
                        'FontSize' => '30',
                        'FontType' => 'simfang.ttf',
                        'FontColor' => '#99ff00',
                        'Transparency' => '100', // Opacity
                     ),
                ),
                array(
                    'Type' => 'Text',
                    'LocMode' => 'Absolute',
                    'Dx' => '64',
                    'Dy' => '64',
                    'Pos' => 'TopLeft',
                    'Text' => array(
                        'Text' => 'The second watermark',
                        'FontSize' => '30',
                        'FontType' => 'simfang.ttf',
                        'FontColor' => '#99ff00',
                        'Transparency' => '100', // Opacity
                     ),
                ),
            ),
        ),
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
        'schema' => 'https', //Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    $result = $cosClient->createMediaTranscodeJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Tag' => 'Transcode',
        'QueueId' => 'asdadadfafsdkjhfjghdfjg',
        'CallBack' => 'https://example.com/callback',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
//            'UserData' => 'xxx', // The user information passed through.
//            'JobLevel' => '0', // Job priority. The greater the value, the higher the priority. Valid values: `0`, `1`, `2`. Default value: `0`.
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
                'Object' => 'video01.mkv',
            ),
            'Transcode' => array(
                'Container' => array(
                    'Format' => 'mp4'
                ),
                'Video' => array(
                    'Codec' => 'H.264',
                    'Profile' => 'high',
                    'Bitrate' => '1000',
                    'Preset' => 'medium',
                    'Width' => '1280',
                    'Fps' => '30',
                ),
                'Audio' => array(
                    'Codec' => 'aac',
                    'Samplerate' => '44100',
                    'Bitrate' => '128',
                    'Channels' => '4',
                ),
                'TransConfig' => array(
                    'AdjDarMethod' => 'scale',
                    'IsCheckReso' => 'false',
                    'ResoAdjMethod' => '1',
                ),
                'TimeInterval' => array(
                    'Start' => '0',
                    'Duration' => '60',
                ),
            ),
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
| Tag                | Request | Job tag: Transcode | String    | Yes       |
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
| :------------------ | :---------------- | :----------------------------------------------------------- | :-------- | :------- |
| TemplateId                   | Request.Operation | Template ID                                        | String    | No  |
| Transcode          | Request.Operation | Transcoding template parameter             | Container | No   |
| WatermarkTemplateId| Request.Operation | Watermark template ID. Multiple watermark template IDs can be passed in.           | String    | No |
| Watermark          | Request.Operation | Watermark template parameter, which is the same as `Request.Watermark` in the watermark template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49917).  | Container | No |
| RemoveWatermark              | Request.Operation | Whether to remove the watermark. This parameter is not supported for H.265 currently.                                                         | Container | No   |
| DigitalWatermark   | Request.Operation | Specifies the digital watermark parameter                                                         | Container | No   |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| JobLevel            | Request.Operation | Job priority. The greater the value, the higher the priority. Valid values: `0`, `1`, `2`. Default value: `0`. | String | No |

>?
>
> For the transcoding parameter, `TemplateId` is used first, and if `TemplateId` is unavailable, `Transcode` is used. For the watermark parameter, `WatermarkTemplateId` or `Watermark` can be used for configuration, and `WatermarkTemplateId` is used first.

`Transcode` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :-------------------------- | :----------------------------------------------------------- | :------------ | :--- |
| TimeInterval          | Request.Operation.Transcode | Same as `Request.TimeInterval` in the transcoding template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911).    | Container | No   |
| Container          | Request.Operation.Transcode | Same as `Request.Container` in the transcoding template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911).    | Container | No   |
| Video          | Request.Operation.Transcode | Same as `Request.Video` in the transcoding template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911).    | Container | No   |
| Audio          | Request.Operation.Transcode | Same as `Request.Audio` in the transcoding template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911).    | Container | No   |
| TransConfig          | Request.Operation.Transcode | Same as `Request.TransConfig` in the transcoding template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911).    | Container | No   |
| AudioMix           | Request.Operation.Transcode     | Audio mix parameter as described in [Structure](https://intl.cloud.tencent.com/document/product/1045/49945).                                    | Container array | No |

`RemoveWatermark` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :-------------------------------- | :------------------------------------- | :----- | :--- |
| Dx                 | Request.Operation.RemoveWatermark |  X-axis offset of the top-left corner origin. Value range: [1, 4096]   | string | Yes   |
| Dy                 | Request.Operation.RemoveWatermark |  Y-axis offset of the top-left corner origin. Value range: [1, 4096]   | string | Yes   |
| Width              | Request.Operation.RemoveWatermark |  Width. Value range: [1, 4096]                 | string | Yes   |
| Height             | Request.Operation.RemoveWatermark |  Height. Value range: [1, 4096]                 | string | Yes   |

`DigitalWatermark` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :--------------------------------- | :----------------------------------------------------------- | :----- | :--- |
| Message               | Request.Operation.DigitalWatermark |  The string embedded by the digital watermark, which can contain up to 64 letters, digits, underscores (\_), hyphens (-), and asterisks (*).    | string | Yes   |
| Type               | Request.Operation.DigitalWatermark | Watermark type, which currently can be set to `Text` only      | String | Yes |
| Version            | Request.Operation.DigitalWatermark | Watermark version, which currently can be set to `V1` only       | String | Yes |
| IgnoreError        | Request.Operation.DigitalWatermark | Whether to ignore the watermarking failure and continue the job. Valid values: `true`, `false` (default value).  | string | Yes   |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------- | :--------------- | :----- | :------- |
| Region             | Request.Operation.Output | Bucket region | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Result file name                                             | String | Yes   |

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

    [RequestId] => NjI2MTAzasdaHUISDHUINzE3YV8xZWVmNjU=
    [ContentType] => application/xml
    [ContentLength] => 1554
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-21T15:10:15+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-1250000000
                            [Object] => video01.mp4
                            [Region] => ap-beijing
                        )

                    [JobId] => j1815a4c81h2kj31231gh31kj2f9e223404e
                    [Message] => Array
                        (
                        )

                    [Operation] => Array
                        (
                            [Output] => Array
                                (
                                    [Bucket] => examplebucket-1250000000
                                    [Object] => Transcode.flv
                                    [Region] => ap-beijing
                                )

                            [TemplateId] => t0b612860as90d8a09sd65dca38
                            [TemplateName] => FLV-SD
                            [UserData] => xxx
                            [JobLevel] => 0
                            [Watermark] => Array
                                (
                                    [0] => Array
                                        (
                                            [Dx] => 64
                                            [Dy] => 64
                                            [EndTime] => Array
                                                (
                                                )

                                            [LocMode] => Absolute
                                            [Pos] => TopRight
                                            [StartTime] => Array
                                                (
                                                )

                                            [Text] => Array
                                                (
                                                    [FontColor] => #99ff00
                                                    [FontSize] => 30
                                                    [FontType] => simfang.ttf
                                                    [Text] => The first watermark
                                                    [Transparency] => 100
                                                )

                                            [Type] => Text
                                        )

                                    [1] => Array
                                        (
                                            [Dx] => 64
                                            [Dy] => 64
                                            [EndTime] => Array
                                                (
                                                )

                                            [LocMode] => Absolute
                                            [Pos] => TopLeft
                                            [StartTime] => Array
                                                (
                                                )

                                            [Text] => Array
                                                (
                                                    [FontColor] => #99ff00
                                                    [FontSize] => 30
                                                    [FontType] => simfang.ttf
                                                    [Text] => The second watermark
                                                    [Transparency] => 100
                                                )

                                            [Type] => Text
                                        )

                                )

                        )

                    [Progress] => 0
                    [QueueId] => p81e648a7s9d88a09sd89a0757be086
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => Transcode
                )

        )

)
```

