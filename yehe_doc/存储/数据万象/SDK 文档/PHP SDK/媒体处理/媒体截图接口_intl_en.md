## Overview

This document provides code samples for screencapturing a media file at some time point.
>! COS PHP SDK v2.3.2 or later is required. Earlier versions may contain bugs and need to be upgraded to the [latest version](https://github.com/tencentyun/cos-php-sdk-v5/releases/) when used.
>

| API | Operation |  Description |
| ------------------------------------------------------------ | --------------------------|---------------------------- |
|   [GetSnapshot](https://intl.cloud.tencent.com/document/product/436/46912)     |  Querying screenshot |   Query the screenshot of media file at some time point     |

## Querying Screenshot

#### Feature description

This API is used to query the screenshot of a media file at some time point.

#### Sample code

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
            
$time = 3.14; // Video frame capturing time point
try {
    $result = $cosClient->getSnapshot(
        array(
            'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
            'Key' => 'exampleobject', // Media file object path, such as `folder/movie.mp4`
            'ci-process' => 'snapshot', // Operation type, which is fixed at `snapshot`
            'Time' => $time, // Video frame capturing time point
            'SaveAs' => '/data/test.jpg', // Local path to save the screenshot
        )
    );
    // Request successful
    echo($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID`. | String  | Yes   |
| Key     | Object key (object name), which is the unique identifier of the object (a media file here) in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| ci-process |  Operation type, which is fixed at `snapshot`. | String | Yes   |
| Time | Video frame capturing time point.                                  | float  | Yes   |
| SaveAs | Local path to save the screenshot.                             | String  | Yes   |


#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [Body] => GuzzleHttp\Psr7\Stream Object
        (
            [stream:GuzzleHttp\Psr7\Stream:private] => Resource id #91
            [size:GuzzleHttp\Psr7\Stream:private] => 
            [seekable:GuzzleHttp\Psr7\Stream:private] => 1
            [readable:GuzzleHttp\Psr7\Stream:private] => 1
            [writable:GuzzleHttp\Psr7\Stream:private] => 1
            [uri:GuzzleHttp\Psr7\Stream:private] => php://temp
            [customMetadata:GuzzleHttp\Psr7\Stream:private] => Array
                (
                )

        )

    [ContentLength] => 153613
    [ContentType] => image/jpeg
    [RequestId] => NjE0NThmNGNfNWIyZjJjMGJfNTE1MV84YmJlODI=
    [Key] => exampleobject
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject
)
```
