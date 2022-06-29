## Overview

This document provides an overview of APIs and SDK code samples for digital watermark jobs.

| API | Description |
| ------------- |  ---------------------- |
| Adding digital watermark | Submits digital watermark adding job. |
| Extracting digital watermark | Submits digital watermark extracting job. |


## Digital Watermark Adding Job

#### Feature description

This API is used to submit a digital watermark adding job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model createMediaDigitalWatermarkJobs(array $args = array());
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
    // Digital watermark adding job 
    $result = $cosClient->createMediaDigitalWatermarkJobs(array(
        'Bucket' => 'examplebucket-125000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'DigitalWatermark',
        'QueueId' => 'p81e648af2aee496885707caxxxxxxxxxxxx',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
            'DigitalWatermark' => array(
                'Message' => '123456789ab',
                'Type' => 'Text',
                'Version' => 'V1',
            ),
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-125000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
                'Object' => 'DigitalWatermark.mp4',
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
| Tag                | Request | Job type: DigitalWatermark | String    | Yes       |
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
| :----------------- | :---------------- | :----------- | :-------- | :------- |
| Output                       | Request.Operation | Result output address                                | Container | Yes   |
| DigitalWatermark   | Request.Operation | Digital watermark configuration | Container | Yes       |

`DigitalWatermark` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| :----------------- | :--------------------------------- | :----------------------- | :----- | :------- | :----- | :-------------------------------------------------- |
| Message            | Request.Operation.DigitalWatermark | The string embedded by the digital watermark | string | Yes       |        | It can contain up to 64 letters, digits, underscores (\_), hyphens (-), and asterisks (*). |
| Type               | Request.Operation.DigitalWatermark | Watermark type                 | String | Yes       |        | Text                                                |
| Version            | Request.Operation.DigitalWatermark | Watermark version                 | String | Yes       |        | V1                                                  |

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

    [RequestId] => NjI2N2JlMDFfZmNjYAJSDIOAJDOIAJD9lZDYxOA==
    [ContentType] => application/xml
    [ContentLength] => 828
    [Bucket] => examplebucket-125000000
    [Location] => examplebucket-125000000.ci.ap-guangzhou.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-26T17:40:17+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-125000000
                            [Object] => video01.mp4
                            [Region] => ap-guangzhou
                        )

                    [JobId] => je1dc03f0c544as09d8as09d8a09dec25a93
                    [Message] => 
                    [Operation] => Array
                        (
                            [DigitalWatermark] => Array
                                (
                                    [Message] => 123456789ab
                                    [Type] => Text
                                    [Version] => V1
                                )

                            [Output] => Array
                                (
                                    [Bucket] => examplebucket-125000000
                                    [Object] => DigitalWatermark.mp4
                                    [Region] => ap-guangzhou
                                )

                        )

                    [QueueId] => p81e648af2aee49688570s8a90d80a9d86
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => DigitalWatermark
                )

        )

)
```




## Digital Watermark Extracting Job

#### Feature description

This API is used to submit a digital watermark extracting job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model createMediaExtractDigitalWatermarkJobs(array $args = array());
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
    // Digital watermark extracting job 
    $result = $cosClient->createMediaExtractDigitalWatermarkJobs(array(
        'Bucket' => 'examplebucket-125000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'ExtractDigitalWatermark',
        'QueueId' => 'p81e648af2aee496885707caxxxxxxxxx',
        'Input' => array(
            'Object' => 'DigitalWatermark.mp4'
        ),
        'Operation' => array(
            'ExtractDigitalWatermark' => array(
                'Type' => 'Text',
                'Version' => 'V1',
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
| :----------------- | :------ | :------------------------------------- | :-------- | :------- |
| Tag                | Request | Job type: ExtractDigitalWatermark | String    | Yes       |
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule                                  | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |
| CallBack           | Request | Callback address                                                | String    | No   |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :----------------------------------------------------------- | :----- | :------- |
| Object             | Request.Input | Media object name. For object naming conventions, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes       |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :---------------------- | :---------------- | :----------- | :-------- | :------- |
| ExtractDigitalWatermark | Request.Operation | Digital watermark configuration | Container | Yes       |

`ExtractDigitalWatermark` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| :----------------- | :---------------------------------------- | :------- | :----- | :------- | :----- | :--- |
| Type               | Request.Operation.ExtractDigitalWatermark | Watermark type | String | Yes       |        | Text |
| Version            | Request.Operation.ExtractDigitalWatermark | Watermark version | String | Yes       |        | V1   |

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

    [RequestId] => NjI2OGI4YmZfZmNjYTNiAOISDAOIDUOMjU4ZjE=
    [ContentType] => application/xml
    [ContentLength] => 680
    [Bucket] => examplebucket-125000000
    [Location] => examplebucket-125000000.ci.ap-guangzhou.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-27T11:30:07+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-125000000
                            [Object] => DigitalWatermark.mp4
                            [Region] => ap-guangzhou
                        )

                    [JobId] => j56038a4cc5da1a8s0d98a90sd806cf06
                    [Message] => 
                    [Operation] => Array
                        (
                            [ExtractDigitalWatermark] => Array
                                (
                                    [Type] => Text
                                    [Version] => V1
                                )

                        )

                    [QueueId] => p81e648af2aee4z9x8c09z8xc09zbe086
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => ExtractDigitalWatermark
                )

        )

)
```

