## Overview

This document provides an overview of APIs and SDK code samples for super resolution jobs.

| API | Description |
| ------------------------------------------------------------ | ---------------- |
| [Submitting super resolution job](https://intl.cloud.tencent.com/document/product/436/47105)| Submits super resolution job. |


## Submitting Super Resolution Job

#### Feature description

This API is used to submit a super resolution job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model createMediaSuperResolutionJobs(array $args = array());
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
    $result = $cosClient->createMediaSuperResolutionJobs(array(
        'Bucket' => 'examplebucket-125000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
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
                'Bucket' => 'examplebucket-125000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
                'Object' => 'SuperResolution.flv',
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
    $result = $cosClient->createMediaSuperResolutionJobs(array(
        'Bucket' => 'examplebucket-125000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
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
                'Bucket' => 'examplebucket-125000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
                'Object' => 'SuperResolution.flv',
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
| :----------------- | :------ | :------------------------------ | :-------- | :------- |
| Tag                | Request | Job type: SuperResolution                            | String    | Yes   |
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
| :------------------ | :---------------- | :----------------------------------------------------------- | :-------- | :------- |
| SuperResolution    | Request.Operation | Super resolution template parameter                                         | Container | No   |
| TemplateId                   | Request.Operation | Template ID                                        | String    | No  |
| Transcode          | Request.Operation | Transcoding template parameter. This node and `TranscodeTemplateId` cannot be empty at the same time.             | Container | No   |
| TranscodeTemplateId | Request.Operation | Transcoding template ID. This node and `Transcode` cannot be empty at the same time. Use this node with priority.           | String  | No|
| Watermark          | Request.Operation | Watermark template parameter. Same as `Request.Watermark` in the watermark template creation API `CreateMediaTemplate`. Up to three watermarks can be passed in. | Container | No |
| WatermarkTemplateId| Request.Operation | Watermark template ID. Up to three watermark template IDs can be passed in. If `Watermark` and `WatermarkTemplateId` exist at the same time, use `WatermarkTemplateId` with priority.          | String    | No |
| DigitalWatermark   | Request.Operation | Specifies the digital watermark parameter                                                         | Container | No   |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |

> Note:
>
> `TemplateId` is used with priority. If `TemplateId` is unavailable, the corresponding job type parameter is used.

`SuperResolution` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description |
| :----------------- | :-------------------------------- | :----------------------------------------------------------- |
| Resolution         | Request.Operation.SuperResolution | Same as `Request.Resolution` in the super resolution template creation API `CreateMediaTemplate`. |
| EnableScaleUp      | Request.Operation.SuperResolution | Same as `Request.EnableScaleUp` in the super resolution template creation API `CreateMediaTemplate`. |

`DigitalWatermark` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :--------------------------------- | :----------------------------------------------------------- | :----- | :--- |
| Message               | Request.Operation.DigitalWatermark |  The string embedded by the digital watermark, which can contain up to 64 letters, digits, underscores (\_), hyphens (-), and asterisks (*)    | string | Yes   |
| Type               | Request.Operation.DigitalWatermark | Watermark type, which currently can be set to `Text` only      | String | Yes |
| Version            | Request.Operation.DigitalWatermark | Watermark version, which currently can be set to `V1` only       | String | Yes |
| IgnoreError        | Request.Operation.DigitalWatermark | Whether to ignore the watermarking failure and continue the job. Valid values: true, false (default)  |string | No   |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------- | :--------------- | :----- | :------- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Output result filename                                             | String | Yes   |

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
    [Bucket] => examplebucket-125000000
    [Location] => examplebucket-125000000.ci.ap-guangzhou.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-27T16:03:35+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-125000000
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
                                    [Bucket] => examplebucket-125000000
                                    [Object] => SuperResolution.flv
                                    [Region] => ap-guangzhou
                                )

                            [TemplateId] => t19ea5e0c0b7b904a8sd09a8sd09a80sd10
                            [TemplateName] => SuperResolution-1
                            [TranscodeTemplateId] => t19ea5e0c0b7b904a8sd09a8sd09a80sd10
                            [WatermarkTemplateId] => t19ea5e0c0b7b904a8sd09a8asdasddsd10
                        )

                    [QueueId] => p81e648af2aee49688570asd8a90sd6
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => SuperResolution
                )

        )

)
```



