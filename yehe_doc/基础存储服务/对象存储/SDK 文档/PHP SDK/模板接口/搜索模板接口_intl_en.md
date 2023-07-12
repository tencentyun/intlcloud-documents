## Overview

This document provides an overview of APIs and SDK code samples for template search.

| API | Description |
| ------------- |  ---------------------- |
| Searching for animated image templates | Searches for animated image templates. |
| Searching for screenshot templates | Searches for screenshot templates. |
| Searching for watermark templates | Searches for watermark templates. |
| Searching for transcoding templates | Searches for transcoding templates. |
| Searching for splicing templates | Searches for splicing templates. |
| Searching for top speed codec transcoding templates | Searches for top speed codec transcoding templates. |
| Searching for video montage templates | Searches for video montage templates. |
| Searching for voice/sound separation templates | Searches for voice/sound separation templates. |
| Searching for video enhancement templates | Searches for video enhancement templates. |
| Searching for image processing templates | Searches for image processing templates. |
| Searching for super resolution templates | Searches for super resolution templates. |

## Searching for Template

#### Feature description

This API is used to search for templates of diverse types, such as `Animation`, `Snapshot`, `Watermark`, `Transcode`, `Concat`, `HighSpeedHd`, `VideoMontage`, `VoiceSeparate`, `VideoProcess`, `PicProcess`, and `SuperResolution`.

#### Method prototype

```php
public Guzzle\Service\Resource\Model describeMediaTemplates(array $args = array());
```

#### Sample request

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; // Replace it with your actual `secretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$secretKey = "SECRETKEY"; // Replace it with your actual `secretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is `http` by default.
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    // Query the template list
    $result = $cosClient->describeMediaTemplates(array(
        'Bucket' => 'examplebucket-125000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
        'Tag' => '', // Template tag. Valid values: `Animation`, `Snapshot`, `Watermark`, `Transcode`, `Concat`, `HighSpeedHd`, `VideoMontage`, `VoiceSeparate`, `VideoProcess`, `PicProcess`.
        'Category' => 'Custom',
        'Ids' => '',
        'Name' => '',
        'PageNumber' => '',
        'PageSize' => '',
    ));
    // The request succeeded.
    print_r($result);
} catch (\Exception $e) {
    // The request failed.
    echo($e);
}
```

#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :------------------------------- | :------ | :--- |
| Tag           | None        | Template tag       | String    | Yes |
| Category      | None        | Template category: Custom (default value) or Official  | String  | No |
| Ids           | None        | Template ID. If you enter multiple IDs, separate them by comma.  | String     |No|
| Name          | None        | Template name prefix              | String     |No|
| PageNumber    | None        | Page number                   | Integer     |No|
| PageSize      | None        | Number of entries per page                 | Integer     |No|

#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjJhOTRlZDFfNzgwYzdkAOIUDOAIUDTA4ZWE=
    [ContentType] => application/xml
    [ContentLength] => 782
    [TotalCount] => 1
    [PageNumber] => 1
    [PageSize] => 10
    [TemplateList] => Array
        (
            [0] => Array
                (
                    [TemplateId] => t1456ea89fcbdf45basd7fa98sd97a5
                    [Name] => VoiceSeparate-Name
                    [State] => Normal
                    [Tag] => VoiceSeparate
                    [CreateTime] => 2021-12-27T22:19:15+0800
                    [UpdateTime] => 2021-12-27T22:19:15+0800
                    [BucketId] => examplebucket-125000000
                    [Category] => Custom
                    [VoiceSeparate] => Array
                        (
                            [AudioMode] => AudioAndBackground
                            [AudioConfig] => Array
                                (
                                    [Codec] => mp3
                                    [Samplerate] => 44100
                                    [Bitrate] => 128
                                    [Channels] => 2
                                )

                        )

                )

        )

    [Bucket] => examplebucket-125000000
    [Location] => examplebucket-125000000.ci.ap-guangzhou.myqcloud.com/template
)
```
