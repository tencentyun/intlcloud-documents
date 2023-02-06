## Overview

This document provides an overview of APIs and SDK code samples for submitting a splicing job.

| API | Description |
| ------------- |  ---------------------- |
| [Submitting a splicing job](https://intl.cloud.tencent.com/document/product/436/49046) | Submits a splicing job. |


## Submitting Splicing Job

#### Feature description

This API is used to submit a splicing job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model createMediaConcatJobs(array $args = array());
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
    $result = $cosClient->createMediaConcatJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Tag' => 'Concat',
        'QueueId' => 'asdadadfafsdkjhfjghdfjg',
        'CallBack' => 'https://example.com/callback',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
            'TemplateId' => 'asdfafiahfiushdfisdhfuis',
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
                'Object' => 'concat-video02.mp4',
            ),
//            'UserData' => 'xxx', // The user information passed through.
//            'JobLevel' => '0', // Job priority. The greater the value, the higher the priority. Valid values: `0`, `1`, `2`. Default value: `0`.
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
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    $result = $cosClient->createMediaConcatJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Tag' => 'Concat',
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
                'Object' => 'concat-video03.mp4',
            ),
            'ConcatTemplate' => array(
                'ConcatFragments' => array(
                    array(
                        'Url' => 'https://example.com/video01.mp4',
                        'Mode' => 'Start',
//                        'StartTime' => '0',
//                        'EndTime' => '7',
                    ),
                    array(
                        'Url' => 'https://example.com/video02.mp4',
                        'Mode' => 'Start',
//                        'StartTime' => '0',
//                        'EndTime' => '10',
                    ),
                    // ... repeated
                ),
                'Index' => 1,
                'Container' => array(
                    'Format' => 'mp4'
                ),
                'Audio' => array(
                    'Codec' => 'mp3',
                    'Samplerate' => '',
                    'Bitrate' => '',
                    'Channels' => '',
                ),
                'Video' => array(
                    'Codec' => 'H.264',
                    'Bitrate' => '1000',
                    'Width' => '1280',
                    'Height' => '',
                    'Fps' => '30',
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
| Tag                | Request | Job tag: Concat                                   | String    | Yes   |
| Input              | Request | Information of the media file to be processed                                         | Container | No   |
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
| ConcatTemplate     | Request.Operation | Splicing parameter.                                                 | Container | No       |
| TemplateId                   | Request.Operation | Template ID                                        | String    | No  |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |
| JobLevel            | Request.Operation | Job priority. The greater the value, the higher the priority. Valid values: `0`, `1`, `2`. Default value: `0`. | String | No |

>!
>
> `TemplateId` is used first. If `TemplateId` is unavailable, `ConcatTemplate` is used.

`ConcatTemplate` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| :----------------- | :-------------------------------- | :----------------------------------------------------------- | :------------- | :------- | :----- | :-------------------------------- |
| ConcatFragment     | Request.Operation. ConcatTemplate | Splicing node                                                    | Container array | No       | None     | Multiple files can be spliced in sequence. |
| Audio              | Request.Operation. ConcatTemplate | Audio parameter. Same as `Request.ConcatTemplate.Audio` in the splicing template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49907).  | Container    | No   | None  | None |
| Video              | Request.Operation. ConcatTemplate | Video parameter. Same as `Request.ConcatTemplate.Video` in the splicing template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49907).  | Container    | No   | None  | None |
| Container          | Request.Operation. ConcatTemplate | Container format. Same as `Request.ConcatTemplate.Container` in the splicing template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49907).   | Container    | Yes   | None  | None |
| AudioMix           | Request.Operation. ConcatTemplate | Audio mix parameter as described in [Structure](https://intl.cloud.tencent.com/document/product/1045/49945).                                    | Container array | No   | None | Valid only if `Audio.Remove` is `false` |
| Index              | Request.Operation. ConcatTemplate | Index of the `Input` node in the `ConcatFragment` sequence    | String    | No   | 0  | The number of indexes configured cannot be greater than the number of fragments specified by `ConcatFragment`. |
| DirectConcat       | Request.Operation. ConcatTemplate | Simple splicing (without transcoding). Other video and audio parameters become invalid. | String | No | false | true, false |

`ConcatFragment` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| :----------------- | :------------------------------------------------ | :----------------- | :----- | :------- | :------- | :------------------- |
| Url                | Request.Operation. ConcatTemplate. ConcatFragment | Splicing object address   | String    | Yes   | None   | Same as the address of the bucket object file. |
| FragmentIndex      | Request.Operation. ConcatTemplate. ConcatFragment | Index position of the spliced object    | String    | No   | 0   | An integer greater than or equal to 0 |
| StartTime          | Request.Operation. ConcatTemplate. ConcatFragment | Start time   | String    | No   | Video start time   | [0, video duration] seconds |
| EndTime            | Request.Operation. ConcatTemplate. ConcatFragment | End time   | String    | No   | Video end time   | [0, video duration] seconds |

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

    [RequestId] => NjI2MjFhOTHASIUDHAUISDHl8yMjMxNmE=
    [ContentType] => application/xml
    [ContentLength] => 792
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-beijing.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-22T11:01:42+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-1250000000
                            [Object] => video01.mp4
                            [Region] => ap-beijing
                        )

                    [JobId] => j898f573asd780a8sd90a8sd09e30cf31f
                    [Message] => 
                    [Operation] => Array
                        (
                            [Output] => Array
                                (
                                    [Bucket] => examplebucket-1250000000
                                    [Object] => concat-video01.mp4
                                    [Region] => ap-beijing
                                )

                            [TemplateId] => t17b9c2e7a0s8d0a8d0a9d43552f648e
                            [TemplateName] => concat-1
                            [UserData] => xxx
                            [TemplateName] => 0
                        )

                    [QueueId] => p81e648af2aeas78d0a8d09a8d09757be086
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => Concat
                )

        )

)
```

