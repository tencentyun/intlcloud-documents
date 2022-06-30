## Overview

This document provides an overview of APIs and SDK code samples for SDR-to-HDR jobs.

| API | Description |
| ------------------------------------------------------------ | -------------------- |
| [Submitting SDR-to-HDR job](https://intl.cloud.tencent.com/document/product/436/47252) | Submits SDR-to-HDR job. |


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
    // Submit an SDR-to-HDR job: https://intl.cloud.tencent.com/document/product/436/47252
    $result = $cosClient->createMediaSDRtoHDRJobs(array(
        'Bucket' => 'examplebucket-125000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
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
                'Bucket' => 'examplebucket-125000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
                'Object' => 'SDRtoHDR.flv',
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
| Tag                | Request | Job type: SDRtoHDR                                   | String    | Yes   |
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule. Up to six jobs can be performed on the same file.                                                | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |
| CallBack           | Request | Callback address                                                | String    | No   |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :--------- | :----- | :------- |
| Object             | Request.Input | Media filename | String | Yes   |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :------------------ | :---------------- | :----------------------------------------------------------- | :-------- | :------- |
| SDRtoHDR             | Request.Operation | SDR-to-HDR parameter                                             | Container | Yes   |
| Transcode          | Request.Operation | Transcoding template parameter. This node and `Transcode` cannot be empty at the same time.             | Container | No   |
| TranscodeTemplateId | Request.Operation | Transcoding template ID. This node and `TranscodeTemplateId` cannot be empty at the same time. Use this node with priority.           | String  | No|
| Watermark          | Request.Operation | Watermark template parameter. Same as `Request.Watermark` in the watermark template creation API `CreateMediaTemplate`. Up to three watermarks can be passed in. | Container | No |
| WatermarkTemplateId| Request.Operation | Watermark template ID. Up to three watermark template IDs can be passed in. If `Watermark` and `WatermarkTemplateId` exist at the same time, use `WatermarkTemplateId` with priority.          | String    | No |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |

`SDRtoHDR` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| :----------------- | :------------------------- | :------- | :----- | :------- | :-------------- |
| HdrMode            | Request.Operation.SDRtoHDR | HDR mode | string | Yes       | 1. HLG 2. HDR10 |

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

    [RequestId] => NjI2N2I1NWFfZmNjYTNHDOASJDOIA1Yw==
    [ContentType] => application/xml
    [ContentLength] => 902
    [Bucket] => examplebucket-125000000
    [Location] => examplebucket-125000000.ci.ap-guangzhou.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-26T17:03:22+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-125000000
                            [Object] => video01.mp4
                            [Region] => ap-guangzhou
                        )

                    [JobId] => jb9289626c53f11ec8a9c4f3d8d099dcb
                    [Message] => 
                    [Operation] => Array
                        (
                            [Output] => Array
                                (
                                    [Bucket] => examplebucket-125000000
                                    [Object] => SDRtoHDR.flv
                                    [Region] => ap-guangzhou
                                )

                            [SDRtoHDR] => Array
                                (
                                    [HdrMode] => HLG
                                )

                            [TranscodeTemplateId] => t0b612860a293f410785ba7s8d09a8d09a38
                            [WatermarkTemplateId] => t185e2e24551b242d09a80d8a0d80428a19c
                        )

                    [QueueId] => t185e2e24551b242d09a80d8a0d80428a19c
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => SDRtoHDR
                )

        )

)
```



