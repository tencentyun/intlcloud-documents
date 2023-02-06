## Overview

This document provides an overview of APIs and SDK code samples for remuxing.

| API | Description |
| ------------------------------------------------------------ | -------------- |
| [Submitting a remuxing job](https://intl.cloud.tencent.com/document/product/436/49053) | Submits a remuxing job |


## Submitting Remuxing Job

#### Feature description

Submitting Remuxing Job

#### Method prototype

```php
public Guzzle\Service\Resource\Model createMediaSegmentJobs(array $args = array());
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
    // Submit a remuxing job. For more information, visit https://intl.cloud.tencent.com/document/product/436/49053.
    $result = $cosClient->createMediaSegmentJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Tag' => 'Segment',
        'QueueId' => 'p81e648af2aee496885707ca0xxxxxxxxx',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
            'Segment' => array(
                'Format' => 'mkv',
                'Duration' => '5',
                'HlsEncrypt' => array(
                    'IsHlsEncrypt' => 'false',
                    'UriKey' => '',
                ),
            ),
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000',
                'Object' => 'Segment-trans${Number}.mkv',
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
| :----------------- | :------ | :---------------------- | :-------- | :------- |
| Tag                | Request | Task type: Segment                                   | String    | Yes   |
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
| :----------------- | :---------------- | :------------- | :-------- | :------- |
| Segment            | Request.Operation | Remuxing parameter                                             | Container | Yes   |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |

`Segment` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| :----------------- | :------------------------ | :------------------- | :-------- | :------- | :------------------------------------------- |
| Format             | Request.Operation.Segment | Container format             | String    | Yes       | aac, mp3, flac, mp4, ts, mkv, avi, hls, m3u8 |
| Duration           | Request.Operation.Segment  | Remuxing duration in seconds                         | String | No   | The value must be an integer not less than 5. |
| HlsEncrypt         | Request.Operation.Segment        | HLS encryption configuration                            | Container | No       | None. This parameter takes effect only when the container format is `hls`.     |

`HlsEncrypt` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| :----------------- | :----------------------------------- | :---------------- | :----- | :--- | :----- | :------------------------------------------------ |
| IsHlsEncrypt          | Request.Operation.Segment.HlsEncrypt | Whether to enable HLS encryption | String | No   | false        | 1. Valid values: `true`, `false`. 2. Encryption is supported only when `Segment.Format` is `HLS`. |
| UriKey                | Request.Operation.Segment.HlsEncrypt | HLS encryption key    | String | No   | None     | This parameter is valid only when `IsHlsEncrypt` is `true`.                       |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------- | :----------------------------------------------------------- | :----- | :------- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Output result filename. If `Duration` is configured and `Format` is not HLS or m3u8, the `${Number}` parameter must be included in the filename and used as the output sequence number of each audio/video segment after custom remuxing. | String | Yes   |

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

    [RequestId] => NjI2YTA2MzZfZAODIJAIODJAIODZF8xNjc2YTA=
    [ContentType] => application/xml
    [ContentLength] => 866
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-28T11:12:54+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-1250000000
                            [Object] => video01.mp4
                            [Region] => ap-guangzhou
                        )

                    [JobId] => j184996a2c6a111ec954767a8248f19aa
                    [Message] => 
                    [Operation] => Array
                        (
                            [Output] => Array
                                (
                                    [Bucket] => examplebucket-1250000000
                                    [Object] => Segment-trans${Number}.mkv
                                    [Region] => ap-guangzhou
                                )

                            [Segment] => Array
                                (
                                    [Duration] => 10
                                    [Format] => mkv
                                    [HlsEncrypt] => Array
                                        (
                                            [IsHlsEncrypt] => false
                                            [UriKey] => 
                                        )

                                )
                            [UserData] => xxx
                            [JobLevel] => 0
                        )

                    [QueueId] => p81e648af2az8x7ca0898s0dasbe086
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => Segment
                )

        )

)
```
