## Overview

This document provides an overview of APIs and SDK code samples for the private M3U8 API.

| API | Description |
| ------------- |  ---------------------- |
| GetPrivateM3U8 | Gets the download authorization for M3U8 and TS resources (requests are forwarded to CI by COS). |


## GetPrivateM3U8

#### Feature description

This API is used to get the download authorization for M3U8 and TS resources (requests are forwarded to CI by COS).

#### Method prototype

```php
public Guzzle\Service\Resource\Model getPrivateM3U8(array $args = array());
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
    $result = $cosClient->GetPrivateM3U8(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'xxx.m3u8', // Bucket file
        'ci-process' => 'pm3u8', // Operation type, which is fixed at `pm3u8`
        'expires' => '3600', // Relative validity period of the download credential for the private TS resource URL in seconds. Value range: [3600, 43200]
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

| Parameter | Description | Type | Required |
| :--------- | :----------------------------------------------------------- | :----- | :------- |
| ci-process | Operation type, which is fixed at `pm3u8`. | String | Yes |
| expires | Relative validity period of the download credential for the private TS resource URL in seconds. Value range: [3600, 43200]. | String | Yes |

#### Sample response

```php
 GuzzleHttp\Command\Result Object
(
    [Body] => GuzzleHttp\Psr7\Stream Object
        (
            [stream:GuzzleHttp\Psr7\Stream:private] => Resource id #89
            [size:GuzzleHttp\Psr7\Stream:private] => 
            [seekable:GuzzleHttp\Psr7\Stream:private] => 1
            [readable:GuzzleHttp\Psr7\Stream:private] => 1
            [writable:GuzzleHttp\Psr7\Stream:private] => 1
            [uri:GuzzleHttp\Psr7\Stream:private] => php://temp
            [customMetadata:GuzzleHttp\Psr7\Stream:private] => Array
                (
                )

        )

    [RequestId] => NjI2MTFjYSDHIUsdsdSJDOIDTRfMjVjYzcw
    [ContentType] => application/x-mpegURL
    [ContentLength] => 4310
    [Key] => xxx.m3u8
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/xxx.m3u8
    [Data] => M3U8 file content
)
```
