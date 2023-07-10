## Overview

This document provides an overview of APIs and SDK code samples for submitting multiple jobs.

| API | Description |
| ------------- |  ---------------------- |
| Submitting multiple jobs | Submits multiple jobs |


## Submitting Multiple Jobs

#### Feature description

This API is used to submit multiple jobs.

#### Method prototype

```php
public Guzzle\Service\Resource\Model createMediaJobs(array $args = array());
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
    // Multi-job APIs: https://cloud.tencent.com/document/product/436/58335
    $result = $cosClient->CreateMediaJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'Transcode', // If `Operation` has no `Tag` parameter, this optional parameter is valid. If there is only one job, use `Operation.Tag` with priority.
        'QueueId' => 'paaf4fce5521a40888a303xxxxxxxxxxxxxx',
        'CallBack' => '',
        'Input' => array(
            'Object' => 'example.mp4'
        ),
        'Operation' => array(
            array(
                'Tag' => 'Transcode',
                'TemplateId' => 't04e1ab86554984f1aa17cxxxxxxxxxxxxxx',
                'Output' => array(
                    'Region' => $region,
                    'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
                    'Object' => 'video01.mp4',
                ),
                'WatermarkTemplateId' => array(
                    't112d18d9b2a9b430e91dxxxxxxxxxxxxxx',
                ),
            ),
            array(
                'Tag' => 'Transcode',
                'TemplateId' => 't04e1ab86554984f1aa17xxxxxxxxxxxxxx',
                'Output' => array(
                    'Region' => $region,
                    'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
                    'Object' => 'video02.mp4',
                ),
                'WatermarkTemplateId' => array(
                    't1bf713bb5c6a5496e859axxxxxxxxxxxxxx',
                ),
            ),
        ),
    ));
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
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule. Up to six operation rules are supported.                                  | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :--------- | :----- | :------- |
| Object             | Request.Input | Media filename | String | Yes   |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :---------------- | :--------------------------------------------------- | :-------- | :------- |
| Tag                          | Request.Operation | Job type. Valid values: Animation, Transcode, SmartCover, Snapshot | Container | Yes   |
| TemplateId                   | Request.Operation | Template ID                                        | String    | Yes  |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |

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

    [RequestId] => NjI2MTAJOIDSjoiajsdoSDOASDHJoimY2YTQ=
    [ContentType] => application/xml
    [ContentLength] => 1731
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-beijing.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [0] => Array
                        (
                            [Code] => Success
                            [CreationTime] => 2022-04-21T18:03:31+0800
                            [EndTime] => -
                            [Input] => Array
                                (
                                    [BucketId] => examplebucket-1250000000
                                    [Object] => video01.mp4
                                    [Region] => ap-beijing
                                )

                            [JobId] => j4c211cas9a87sd90d80a988627cb30
                            [Message] =>  
                            [Operation] => Array
                                (
                                    [Output] => Array
                                        (
                                            [Bucket] => examplebucket-1250000000
                                            [Object] => Transcode-01.flv
                                            [Region] => ap-beijing
                                        )

                                    [TemplateId] => t0b6128z8c098z09xcsd89s0a5dca38
                                    [TemplateName] => FLV-SD
                                    [WatermarkTemplateId] => t185z90x8c9z0da5sd67a5a19c
                                )

                            [Progress] => 0
                            [QueueId] => pzx8c09za90sd890a8d09aa0757be086
                            [StartTime] => -
                            [State] => Submitted
                            [Tag] => Transcode
                        )

                    [1] => Array
                        (
                            [Code] => Success
                            [CreationTime] => 2022-04-21T18:03:31+0800
                            [EndTime] => -
                            [Input] => Array
                                (
                                    [BucketId] => examplebucket-1250000000
                                    [Object] => video01.mp4
                                    [Region] => ap-beijing
                                )

                            [JobId] => j4cz9x7c8z9xcsda98sd09ad80627cb30
                            [Message] => 
                            [Operation] => Array
                                (
                                    [Output] => Array
                                        (
                                            [Bucket] => examplebucket-1250000000
                                            [Object] => Transcode-02.flv
                                            [Region] => ap-beijing
                                        )

                                    [TemplateId] => t0bz98xc789zxs9d80a8sd90asd37f83c
                                    [TemplateName] => FLV-HD
                                    [WatermarkTemplateId] => t18zc8z90csd876a78sdas87d8a19c
                                )

                            [Progress] => 0
                            [QueueId] => p81zxc908zaf2aee496a09s8d90as8d90
                            [StartTime] => -
                            [State] => Submitted
                            [Tag] => Transcode
                        )

                )

        )

)
```
