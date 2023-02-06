## Overview

This document provides an overview of APIs and SDK code samples for SDR-to-HDR jobs.

| API | Description |
| ------------------------------------------------------------ | -------------------- |
| [Submitting an SDR-to-HDR job](https://intl.cloud.tencent.com/document/product/436/49052) | Submits an SDR-to-HDR job. |


## Submitting SDR-to-HDR Job

#### Feature description

This API is used to submit an SDR-to-HDR job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model createMediaSDRtoHDRJobs(array $args = array());
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
    // Submit an SDR-to-HDR job. For more information, visit https://intl.cloud.tencent.com/document/product/436/49052.
    $result = $cosClient->createMediaSDRtoHDRJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Tag' => 'SDRtoHDR',
        'QueueId' => 'p81e648af2aee496885a8d09a8s09d8a0sd6',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
            'TranscodeTemplateId' => '',
            'WatermarkTemplateId' => '',
            'SDRtoHDR' => array(
                'HdrMode' => 'HLG',
            ),
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
                'Object' => 'SDRtoHDR.flv',
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
| Tag                | Request | Job tag: SDRtoHDR                                   | String    | Yes   |
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
| SDRtoHDR             | Request.Operation | SDR-to-HDR parameter                                             | Container | Yes   |
| Transcode          | Request.Operation | Transcoding template parameter. This node and `TranscodeTemplateId` cannot be empty at the same time.             | Container | No   |
| TranscodeTemplateId | Request.Operation | Transcoding template ID. This node and `Transcode` cannot be empty at the same time. Use this node first.           | String  | No|
| Watermark          | Request.Operation | Watermark template parameter. Same as `Request.Watermark` in the watermark template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49917). Up to three watermarks can be passed in. | Container array | No |
| WatermarkTemplateId| Request.Operation | Watermark template ID. Up to three watermark template IDs can be passed in. If `Watermark` and `WatermarkTemplateId` exist at the same time, use `WatermarkTemplateId` first.          | String array    | No |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| JobLevel            | Request.Operation | Job priority. The greater the value, the higher the priority. Valid values: `0`, `1`, `2`. Default value: `0`. | String | No |

>?
>
> To submit an SDR-to-HDR job, you must pass in the transcoding parameter. For the transcoding parameter, `TranscodeTemplateId` is used first, and if `TranscodeTemplateId` is unavailable, `Transcode` is used. For the watermark parameter, `WatermarkTemplateId` or `Watermark` can be used for configuration, and `WatermarkTemplateId` is used first.

`SDRtoHDR` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| :----------------- | :------------------------- | :------- | :----- | :------- | :-------------- |
| HdrMode            | Request.Operation.SDRtoHDR | HDR mode | String | Yes       | 1. HLG. 2. HDR10. |

`Transcode` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :-------------------------- | :----------------------------------------------------------- | :------------- | :--- |
| TimeInterval          | Request.Operation.Transcode | Same as `Request.TimeInterval` in the transcoding template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911).    | Container | No   |
| Container          | Request.Operation.Transcode | Same as `Request.Container` in the transcoding template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911).    | Container | No   |
| Video          | Request.Operation.Transcode | Same as `Request.Video` in the transcoding template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911).    | Container | No   |
| Audio          | Request.Operation.Transcode | Same as `Request.Audio` in the transcoding template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911).    | Container | No   |
| TransConfig          | Request.Operation.Transcode | Same as `Request.TransConfig` in the transcoding template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49911).    | Container | No   |
| AudioMix           | Request.Operation.Transcode     | Audio mix parameter as described in [Structure](https://intl.cloud.tencent.com/document/product/1045/49945).                                    | Container array | No |

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

    [RequestId] => NjI2N2I1NWFfZmNjYTNHDOASJDOIA1Yw==
    [ContentType] => application/xml
    [ContentLength] => 902
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-guangzhou.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-26T17:03:22+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-1250000000
                            [Object] => video01.mp4
                            [Region] => ap-guangzhou
                        )

                    [JobId] => jb9289626c53f11ec8a9c4f3d8d099dcb
                    [Message] => 
                    [Operation] => Array
                        (
                            [Output] => Array
                                (
                                    [Bucket] => examplebucket-1250000000
                                    [Object] => SDRtoHDR.flv
                                    [Region] => ap-guangzhou
                                )

                            [SDRtoHDR] => Array
                                (
                                    [HdrMode] => HLG
                                )

                            [TranscodeTemplateId] => t0b612860a293f410785ba7s8d09a8d09a38
                            [WatermarkTemplateId] => t185e2e24551b242d09a80d8a0d80428a19c
                            [UserData] => xxx
                            [JobLevel] => 0
                        )

                    [QueueId] => t185e2e24551b242d09a80d8a0d80428a19c
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => SDRtoHDR
                )

        )

)
```



