## Overview

This document provides an overview of APIs and SDK code samples for submitting an intelligent thumbnail job.

| API | Description |
| ------------- |  ---------------------- |
| [Submitting an intelligent thumbnail job](https://intl.cloud.tencent.com/document/product/436/49054) | Submits an intelligent thumbnail job |


## Submitting Intelligent Thumbnail Job

#### Feature description

This API is used to submit an intelligent thumbnail job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model createMediaSmartCoverJobs(array $args = array());
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
    // Submit an intelligent thumbnail job. For more information, visit https://intl.cloud.tencent.com/document/product/436/49054.
    $result = $cosClient->createMediaSmartCoverJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Tag' => 'SmartCover',
        'QueueId' => 'p81e648afxxxxxxxxxxxxxxxxx',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
//            'TemplateId' => '', // Use a template
            'SmartCover' => array(
                'Format' => '',
                'Width' => '',
                'Height' => '',
                'Count' => '',
                'DeleteDuplicates' => '',
            ),
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
                'Object' => 'SmartCover-${Number}.jpg',
            ),
//            'UserData' => 'xxx', // The user information passed through.
//            'JobLevel' => '0', // Job priority. The greater the value, the higher the priority. Valid values: `0`, `1`, `2`. Default value: `0`.
        ),
        'CallBack' => '',
//        'CallBackFormat' => '',
//        'CallBackType' => '',
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
| Tag                | Request | Job tag: SmartCover                                   | String    | Yes   |
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
| TemplateId         | Request.Operation | Intelligent thumbnail template ID | String | No       |
| SmartCover                   | Request.Operation | Thumbnail configuration        | Container | No   |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| JobLevel            | Request.Operation | Job priority. The greater the value, the higher the priority. Valid values: `0`, `1`, `2`. Default value: `0`. | String | No |

>?
>
> If both `TemplateId` and `SmartCover` are set, `TemplateId` will be used first.

`SmartCover` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| :----------------- | :--------------------------- | :----------- | :----- | :------- | :----- | :--------------------------------- |
| Format             | Request.Operation.SmartCover | Thumbnail image type.    | String | Yes  | None | png, jpg, webp  |
| Width              | Request.Operation.SmartCover | Thumbnail image width    | String | Yes  | None | 1. Value range: [128, 4096]. 2. Unit: px. |
| Height             | Request.Operation.SmartCover | Thumbnail image height    | String | Yes  | None | 1. Value range: [128, 4096]. 2. Unit: px. |
| Count              | Request.Operation.SmartCover | Number of thumbnails.        | String | No  | 3 | 1. Value range: [1, 10]. |
| DeleteDuplicates   | Request.Operation.SmartCover | Whether to deduplicate thumbnails.    | String | No  | false | true/false |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------- | :----------------------------------------------------------- | :----- | :------- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Result filename. <br/>**${Number} must be included in the filename.**<br/> For example, if `Object` is `my-new-cover-${Number}.jpg`, and there are three result files, the output result filenames are as follows: <br/>my-new-cover-0.jpg<br/>my-new-cover-1.jpg<br/>my-new-cover-2.jpg | String | Yes   |

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

    [RequestId] => NjI2MASOIDUAOIDUJIAOJDIOADJyMjNjZDE=
    [ContentType] => application/xml
    [ContentLength] => 832
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-beijing.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-22T11:12:33+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-1250000000
                            [Object] => video01.mp4
                            [Region] => ap-beijing
                        )

                    [JobId] => j0d9bc17z890zx8c9s877z97187147
                    [Message] => 
                    [Operation] => Array
                        (
                            [Output] => Array
                                (
                                    [Bucket] => examplebucket-1250000000
                                    [Object] => SmartCover-${Number}.jpg
                                    [Region] => ap-beijing
                                )

                            [SmartCover] => Array
                                (
                                    [Count] => 
                                    [DeleteDuplicates] => false
                                    [Format] => 
                                    [Height] => 
                                    [Width] => 
                                )
                            [UserData] => xxx
                            [JobLevel] => 0
                        )

                    [QueueId] => p81e648afzx8c09z8xc09zx8c097be086
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => SmartCover
                )

        )

)
```

