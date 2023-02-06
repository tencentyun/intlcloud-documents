## Overview

This document provides an overview of APIs and SDK code samples for super resolution.

| API | Description |
| ------------------------------------------------------------ | ---------------- |
| [Submitting a super resolution job](https://intl.cloud.tencent.com/document/product/436/49057) | Submits a super resolution job. |


## Submitting Super Resolution Job

#### Feature description

Submitting a Super Resolution Task

#### Method prototype

```php
public Guzzle\Service\Resource\Model createMediaSuperResolutionJobs(array $args = array());
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
    $result = $cosClient->createMediaSuperResolutionJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Tag' => 'SuperResolution',
        'QueueId' => 'p81e648af2aee49688570xxxxxxxxxxx',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
            'TemplateId' =>'t19ea5e0c0b7054d7b904axxxxxxxxxxx',
            'TranscodeTemplateId' =>'t0b612860a293f41078xxxxxxxxxxx',
            'WatermarkTemplateId' =>'t185e2e24551b24259a02xxxxxxxxxxx',
            'DigitalWatermark' => array(
                'Message' => 'xxx',
                'Type' => 'Text',
                'Version' => 'V1',
                'IgnoreError' => 'true',
            ),
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
                'Object' => 'SuperResolution.flv',
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
    $result = $cosClient->createMediaSuperResolutionJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Tag' => 'SuperResolution',
        'QueueId' => 'p81e648af2aee49688570xxxxxxxxxxx',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
            'SuperResolution' => array(
                'Resolution' => '',
                'EnableScaleUp' => '',
            ),
            'Transcode' => array(
                'Tag' => '',
                'Name' => '',
                'Container' => array(
                    'Format' => '',
                ),
                'Video' => array(
                    'Codec' => '',
                    'Width' => '',
                    'Height' => '',
                    'Fps' => '',
                    'Remove' => '',
                    'Profile' => '',
                    'Bitrate' => '',
                    'Crf' => '',
                    'Gop' => '',
                    'Preset' => '',
                    'Bufsize' => '',
                    'Maxrate' => '',
                    'HlsTsTime' => '',
                    'Pixfmt' => '',
                    'LongShortMode' => '',
                ),
                'TimeInterval' => array(
                    'Start' => '',
                    'Duration' => '',
                ),
                'Audio' => array(
                    'Codec' => '',
                    'Samplerate' => '',
                    'Bitrate' => '',
                    'Channels' => '',
                    'Remove' => '',
                    'KeepTwoTracks' => '',
                    'SwitchTrack' => '',
                    'SampleFormat' => '',
                ),
                'TransConfig' => array(
                    'AdjDarMethod' => '',
                    'IsCheckReso' => '',
                    'ResoAdjMethod' => '',
                    'IsCheckVideoBitrate' => '',
                    'VideoBitrateAdjMethod' => '',
                    'IsCheckAudioBitrate' => '',
                    'AudioBitrateAdjMethod' => '',
                    'DeleteMetadata' => '',
                    'IsHdr2Sdr' => '',
                    'HlsEncrypt' => array(
                        'IsHlsEncrypt' => '',
                        'UriKey' => '',
                    ),
                ),
            ),
            'Watermark' => array(
                'Type' => '',
                'Pos' => '',
                'LocMode' => '',
                'Dx' => '',
                'Dy' => '',
                'StartTime' => '',
                'EndTime' => '',
                'Image' => array(
                    'Url' => '',
                    'Mode' => '',
                    'Width' => '',
                    'Height' => '',
                    'Transparency' => '',
                    'Background' => '',
                ),
                'Text' => array(
                    'FontSize' => '',
                    'FontType' => '',
                    'FontColor' => '',
                    'Transparency' => '',
                    'Text' => '',
                ),
            ),
            'DigitalWatermark' => array(
                'Message' => '',
                'Type' => '',
                'Version' => '',
                'IgnoreError' => '',
            ),
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
                'Object' => 'SuperResolution.flv',
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
| Tag                | Request | Job tag: SuperResolution                            | String    | Yes   |
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
| :------------------ | :---------------- | :----------------------------------------------------------- | :------------- | :------- |
| SuperResolution    | Request.Operation | Super resolution template parameter. This node and `TemplateId` cannot be empty at the same time.                                         | Container | No   |
| TemplateId                   | Request.Operation | Super resolution template ID, which is used first. This node and `SuperResolution` cannot be empty at the same time.                                        | String    | No  |
| Transcode          | Request.Operation | Transcoding template parameter. This node and `TranscodeTemplateId` cannot be empty at the same time.             | Container | No   |
| TranscodeTemplateId | Request.Operation | Transcoding template ID. This node and `Transcode` cannot be empty at the same time. Use this node first.           | String  | No|
| Watermark          | Request.Operation | Watermark template parameter. Same as `Request.Watermark` in the watermark template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49917). Up to three watermarks can be passed in. | Container array | No |
| WatermarkTemplateId| Request.Operation | Watermark template ID. Up to three watermark template IDs can be passed in. If `Watermark` and `WatermarkTemplateId` exist at the same time, use `WatermarkTemplateId` first.          | String array    | No |
| DigitalWatermark   | Request.Operation | Specifies the digital watermark parameter                                                         | Container | No   |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| JobLevel            | Request.Operation | Job priority. The greater the value, the higher the priority. Valid values: `0`, `1`, `2`. Default value: `0`. | String | No |

>?
>
> To submit a super resolution job, you must pass in the transcoding parameter. For the super resolution parameter, `TemplateId` is used first, and if `TemplateId` is unavailable, `SuperResolution` is used. For the transcoding parameter, `TranscodeTemplateId` is used first, and if `TranscodeTemplateId` is unavailable, `Transcode` is used. For the watermark parameter, `WatermarkTemplateId` or `Watermark` can be used for configuration, and `WatermarkTemplateId` is used first.

`SuperResolution` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :-------------------------------- | :----------------------------------------------------------- | :----- | :--- |
| Resolution         | Request.Operation.SuperResolution | Same as `Request.Resolution` in the super resolution template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49910).    | String | Yes |
| EnableScaleUp         | Request.Operation.SuperResolution | Same as `Request.EnableScaleUp` in the super resolution template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49910).    | String | No |
| Version         | Request.Operation.SuperResolution | Same as `Request.Version` in the super resolution template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49910).    | String | No |

`Transcode` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :-------------------------- | :----------------------------------------------------------- | :------------- | :--- |
| TimeInterval          | Request.Operation.Transcode | Same as `Request.TimeInterval` in the transcoding template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911).    | Container | No   |
| Container          | Request.Operation.Transcode | Same as `Request.Container` in the transcoding template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911).    | Container | No   |
| Video          | Request.Operation.Transcode | Same as `Request.Video` in the transcoding template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911).    | Container | No   |
| Audio          | Request.Operation.Transcode | Same as `Request.Audio` in the transcoding template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911).    | Container | No   |
| TransConfig          | Request.Operation.Transcode | Same as `Request.TransConfig` in the transcoding template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911).    | Container | No   |
| AudioMix           | Request.Operation.Transcode     | Audio mix parameter as described in [Structure](https://intl.cloud.tencent.com/document/product/1045/49945).                                    | Container array | No |

`DigitalWatermark` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :--------------------------------- | :----------------------------------------------------------- | :----- | :--- |
| Message            | Request.Operation.DigitalWatermark | The string embedded by the digital watermark, which can contain up to 64 letters, digits, underscores (\_), hyphens (-), and asterisks (*).    | String | Yes   |
| Type               | Request.Operation.DigitalWatermark | Watermark type, which currently can be set to `Text` only      | String | Yes |
| Version            | Request.Operation.DigitalWatermark | Watermark version, which currently can be set to `V1` only       | String | Yes |
| IgnoreError        | Request.Operation.DigitalWatermark | Whether to ignore the watermarking failure and continue the job. Valid values: `true`, `false` (default).  | string | No   |

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

    [RequestId] => NjI2OGY4ZDdfZmNjYTNiMGAJODIJAOIDJAOMmVmNDU=
    [ContentType] => application/xml
    [ContentLength] => 1170
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-27T16:03:35+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-1250000000
                            [Object] => video01.mp4
                            [Region] => ap-guangzhou
                        )

                    [JobId] => j89be22b8c60011ec9070fasd8a09d80a9b8
                    [Message] => 
                    [Operation] => Array
                        (
                            [DigitalWatermark] => Array
                                (
                                    [IgnoreError] => true
                                    [Message] => xxx
                                    [State] => Running
                                    [Type] => Text
                                    [Version] => V1
                                )

                            [Output] => Array
                                (
                                    [Bucket] => examplebucket-1250000000
                                    [Object] => SuperResolution.flv
                                    [Region] => ap-guangzhou
                                )

                            [TemplateId] => t19ea5e0c0b7b904a8sd09a8sd09a80sd10
                            [TemplateName] => SuperResolution-1
                            [TranscodeTemplateId] => t19ea5e0c0b7b904a8sd09a8sd09a80sd10
                            [WatermarkTemplateId] => t19ea5e0c0b7b904a8sd09a8asdasddsd10
                            [UserData] => xxx
                            [JobLevel] => 0
                        )

                    [QueueId] => p81e648af2aee49688570asd8a90sd6
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => SuperResolution
                )

        )

)
```



