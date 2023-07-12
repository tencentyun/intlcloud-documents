
## Overview

This document provides an overview of APIs and SDK code samples for image advanced compression.


| API | Description |
| :--------------- |  :--------------------- |
| [Image advanced compression](https://intl.cloud.tencent.com/document/product/1045/40108) | Allows you to easily convert images into formats that provide a high compression ratio, such as TPG and HEIF. This effectively reduces the transfer time, loading time, and the use of bandwidth and traffic. |


## Image Advanced Compression

#### Feature description

CI uses the `imageMogr2` API to provide the image advanced compression feature.


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
            
try {
        $imageMogrTemplate = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate();// Create an instance of the basic image processing parameter template
        $imageMogrTemplate->format('tpg');// Convert the input image to TPG format
        $imageMogrTemplate->format('heif');// Convert the input image to HEIF format
        $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'ImageHandleParam' => $imageMogrTemplate->queryString(),// Generate basic image processing parameters
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Type | Description | Required |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key       | String | Object key, which is the unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | Yes       |
| ImageHandleParam      | String      | CI image processing parameters, such as `imageMogr2/format/tpg`.      | Yes        |

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Body] => 
            [ETag] => "698d51a19d8a121ce581499d7b701668"
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [ContentLength] => 100
            [ContentType] => image/jpeg
            [Key] => exampleobject
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
        )

)

```

#### Response description

| Parameter | Type | Description | Parent Node |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| Body | File/String | Downloaded content                                                   | None |
| ETag | String | MD5 checksum of the file | None |
| ContentLength | Int | Length of the response body | None |
| ContentType | String | Content type. Sets `Content-Type` | None |
| RequestId             | String      | Request ID                                | None     |
| Key                  | String      | Object key                                    | None     |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Location             | String      | Address of the requested resource                                 | None     |
