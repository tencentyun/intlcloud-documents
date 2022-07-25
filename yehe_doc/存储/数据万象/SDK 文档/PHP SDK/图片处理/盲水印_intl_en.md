
## Overview

This document provides an overview of APIs and SDK code samples for blind watermarking.

| API | Description |
| ------------------------------------------ | -------------------------- |
| Blind watermarking | Adds blind watermark to or extracts blind watermark from local image and uploads it to bucket |


## Adding Blind Watermark

### Adding during upload

The specified watermark image must:
1. Be stored in the same bucket as the input image.
2. Be accessible at a URL containing a COS domain name (CDN acceleration domain names such as `examplebucket-1250000000.file.myqcloud.com/shuiyin_2.png` are not supported). If the image watermark is set to privately readable, the URL must carry a signature.
3. Have a URL starting with `http://`. Note that "http://" cannot be omitted or changed to "https://". For example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` and `https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` are invalid watermark URLs.

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
        $blindWatermarkTemplate = new Qcloud\Cos\ImageParamTemplate\BlindWatermarkTemplate();// Create an instance of the blind watermark parameter template
        $blindWatermarkTemplate->setType(3);// Blind watermark type. Valid values: 1 (semi-blind watermark), 2 (blind watermark), 3 (text blind watermark).
        $blindWatermarkTemplate->setImage("imageUrl");// Set the blind watermark image URL
        $blindWatermarkTemplate->setText("Test");// Set the blind watermark text
        $blindWatermarkTemplate->setLevel(3);// Blind watermark level, which only takes effect if `type` is set to `2`. Valid values: 1 (default), 2, 3. The larger the value, the better the blind watermarking effect.
        $picOperationsTemplate = new \Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();// Create an instance of the persistent image processing parameter template
        $picOperationsTemplate->setIsPicInfo(1);// Set whether to return the input image information. Valid values: 0 (no), 1 (yes). Default value: 0.
        $picOperationsTemplate->addRule($blindWatermarkTemplate, "resultobject");// Set persistent image processing parameters
        $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'Body' => fopen('path/to/localFile', 'rb'), 
        'PicOperations' => $picOperationsTemplate->queryString(),// Generate parameters for persistent image processing
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
| -------------------- | ----------- | ------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key       | String | Object key, which is the unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | Yes       |
| Body | File/String | Uploaded content                                                   | Yes |
| PicOperations    | Json/String      | Persistent image processing information                                  | Yes       |


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
            [ContentLength] => 10000
            [Key] => exampleobject
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
            [Data] => Array
            (
                [OriginalInfo] => Array
                (
                    [Key] => exampleobject
                    [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
                    [ETag] => "7037fb6fb4cca43b958a28789605e73d98088720"
                    [ImageInfo] => Array
                    (
                            [Format] => JPEG
                            [Width] => 600
                            [Height] => 500
                            [Quality] => 90
                            [Ave] => 0x46442e
                            [Orientation] => 0
                     )

                )
                [ProcessResults] => Array
                (
                    [Object] => Array
                    (
                        [0] => Array(
                            [Key] => resultobject
                            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/resultobject
                            [Format] => JPEG
                            [Width] => 300
                            [Height] => 200
                            [Size] => 30000
                            [Quality] => 90
                            [ETag] => "87c153bc2909aa0ba111ca126b675c510d36b817"
                        )
                    )
                )
            )
    )
)

```

#### Response description

| Parameter | Type | Description | Parent Node |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| Body                 | File/String | Response body                                    | None     |
| ETag | String | MD5 checksum of the file | None |
| RequestId             | String      | Request ID                                | None     |
| ContentLength | Int | Length of the response body | None |
| Key                  | String      | Object key                                    | None     |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Location             | String      | Address of the requested resource                                 | None     |
| Data                 | Array      | Image processing result                              | None     |


### Adding during download

The specified watermark image must:
1. Be stored in the same bucket as the input image.
2. Be accessible at a URL containing a COS domain name (CDN acceleration domain names such as `examplebucket-1250000000.file.myqcloud.com/shuiyin_2.png` are not supported). If the image watermark is set to privately readable, the URL must carry a signature.
3. Have a URL starting with `http://`. Note that "http://" cannot be omitted or changed to "https://". For example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` and `https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` are invalid watermark URLs.

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
        $blindWatermarkTemplate = new Qcloud\Cos\ImageParamTemplate\BlindWatermarkTemplate();// Create an instance of the blind watermark parameter template
        $blindWatermarkTemplate->setType(3);// Blind watermark type. Valid values: 1 (semi-blind watermark), 2 (blind watermark), 3 (text blind watermark).
        $blindWatermarkTemplate->setImage("imageUrl");// Set the blind watermark image URL
        $blindWatermarkTemplate->setText("Test");// Set the blind watermark text
        $blindWatermarkTemplate->setLevel(3);// Blind watermark level, which only takes effect if `type` is set to `2`. Valid values: 1 (default), 2, 3.
        $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'ImageHandleParam' => $blindWatermarkTemplate->queryString(),// Generate blind watermark parameters
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
| -------------------- | ----------- | ------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key       | String | Object key, which is the unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | Yes       |
| ImageHandleParam    | String      | Blind watermark parameter                                         | Yes   |


#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Body] => 
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [ContentLength] => 100
            [CacheControl] => max-age=2592000
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
| RequestId             | String      | Request ID                                | None     |
| CacheControl | String | Cache policy. Sets `Cache-Control`. | None |
| ContentType | String | Content type. Sets `Content-Type` | None |
| ContentLength | Int | Length of the response body | None |
| Key                  | String      | Object key                                    | None     |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Location             | String      | Address of the requested resource                                 | None     |

## Extracting Blind Watermark

The image URL should be entered according to the blind watermark type:
1. For a semi-blind watermark, the blind watermark image URL is required and must be the URL of the input image.
2. For a blind watermark, the blind watermark image URL is required and must be the URL of the watermark image.
3. For a text blind watermark, the blind watermark image URL is invalid and does not need to be entered.

The specified watermark image must:
1. Be stored in the same bucket as the input image.
2. Be accessible at a URL containing a COS domain name (CDN acceleration domain names such as `examplebucket-1250000000.file.myqcloud.com/shuiyin_2.png` are not supported). If the image watermark is set to privately readable, the URL must carry a signature.
3. Have a URL starting with `http://`. Note that "http://" cannot be omitted or changed to "https://". For example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` and `https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` are invalid watermark URLs.

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
        $blindWatermarkTemplate = new Qcloud\Cos\ImageParamTemplate\BlindWatermarkTemplate();// Create an instance of the blind watermark parameter template
        $blindWatermarkTemplate->setPick();// Set to extract a blind watermark
        $blindWatermarkTemplate->setType(3);// Blind watermark type. Valid values: 1 (semi-blind watermark), 2 (blind watermark), 3 (text blind watermark).
        $blindWatermarkTemplate->setImage("imageUrl");// Set the blind watermark image URL
        $blindWatermarkTemplate->setText("Test");// Set the blind watermark text
        $blindWatermarkTemplate->setLevel(3);// Blind watermark level, which only takes effect if `type` is set to `2`. Valid values: 1 (default), 2, 3. The larger the value, the better the blind watermarking effect.
        $picOperationsTemplate = new \Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();// Create an instance of the persistent image processing parameter template
        $picOperationsTemplate->setIsPicInfo(1);// Set whether to return the input image information. Valid values: 0 (no), 1 (yes). Default value: 0.
        $picOperationsTemplate->addRule($blindWatermarkTemplate, "resultobject");// Set persistent image processing parameters
        $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'Body' => fopen('path/to/localFile', 'rb'), 
        'PicOperations' => $picOperationsTemplate->queryString(),// Generate parameters for persistent image processing
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
| -------------------- | ----------- | ------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key       | String | Object key, which is the unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | Yes       |
| Body | File/String | Uploaded content                                                   | Yes |
| PicOperations    | Json/String      | Persistent image processing information                                  | Yes       |

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
            [ContentLength] => 10000
            [Key] => exampleobject
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
            [Data] => Array
            (
                [OriginalInfo] => Array
                (
                    [Key] => exampleobject
                    [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
                    [ETag] => "7037fb6fb4cca43b958a28789605e73d98088720"
                    [ImageInfo] => Array
                    (
                            [Format] => JPEG
                            [Width] => 600
                            [Height] => 500
                            [Quality] => 90
                            [Ave] => 0x46442e
                            [Orientation] => 0
                     )

                )
                [ProcessResults] => Array
                (
                    [Object] => Array
                    (
                        [0] => Array(
                            [Key] => resultobject
                            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/resultobject
                            [Format] => JPEG
                            [Width] => 300
                            [Height] => 200
                            [Size] => 30000
                            [Quality] => 90
                            [WatermarkStatus] => 90
                            [ETag] => "87c153bc2909aa0ba111ca126b675c510d36b817"
                        )
                    )
                )
            )
    )
)

```

#### Response description

| Parameter | Type | Description | Parent Node |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| Body                 | File/String | Response body                                    | None     |
| ETag | String | MD5 checksum of the file | None |
| RequestId             | String      | Request ID                                | None     |
| ContentLength | Int | Length of the response body | None |
| Key                  | String      | Object key                                    | None     |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Location             | String      | Address of the requested resource                                 | None     |
| Data                 | Array      | Image processing result                              | None     |
