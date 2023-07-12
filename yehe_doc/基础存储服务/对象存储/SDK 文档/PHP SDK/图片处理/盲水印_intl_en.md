
## Overview

This document provides an overview of APIs and SDK code samples related to COS blind watermarking.

| API | Description    |
| ------------------------------------------ | -------------------------- |
| Blind watermarking | Adds blind watermarks to or extracts blind watermarks from local images and uploads them to a bucket |


## Adding Blind Watermarks

### Adding a blind watermark upon upload

The specified watermark image must:
1. Be stored in the same bucket as the input image.
2. Have a URL containing a COS domain name (a CDN acceleration domain name such as `examplebucket-1250000000.file.myqcloud.com/shuiyin_2.png` is unsupported) and be accessible. If the image watermark is set to private-read, it must carry a signature.
3. Have a URL starting with `http://`. Note that "http://" cannot be omitted or changed to "https://". For example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` and `https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` are invalid watermark URLs.

#### Sample code
```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
        $blindWatermarkTemplate = new Qcloud\Cos\ImageParamTemplate\BlindWatermarkTemplate(); //Create a blind watermark parameter template instance
        $blindWatermarkTemplate->setType(3); //Blind watermark type. Valid values: `1` (semi-blind), `2` (perfectly blind), `3` (text)
        $blindWatermarkTemplate->setImage("imageUrl"); //Set the blind watermark image URL
        $blindWatermarkTemplate->setText("Test"); //Set the blind watermark text
        $blindWatermarkTemplate->setLevel(3); //Perfectly blind watermark level, which only takes effect when `type` is set to `2`. Valid values: `1` (default), `2`, `3`. The larger the value, the better the blind watermarking effect.
        $picOperationsTemplate = new \Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation(); //Create a parameter template instance for persistent image processing
        $picOperationsTemplate->setIsPicInfo(1); //Set whether to return the input image information. `0` (default): no; `1`: yes
        $picOperationsTemplate->addRule($blindWatermarkTemplate, "resultobject"); //Set presistent image processing parameters
        $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'Body' => fopen('path/to/localFile', 'rb'), 
        'PicOperations' => $picOperationsTemplate->queryString(), //Generate parameters for presistent image processing
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
| Key | String | Uniquely identifies an object in a bucket. For example, if the object access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg`.  | Yes |
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


### Adding a blind watermark upon download

The specified watermark image must:
1. Be stored in the same bucket as the input image.
2. Have a URL containing a COS domain name (a CDN acceleration domain name such as `examplebucket-1250000000.file.myqcloud.com/shuiyin_2.png` is unsupported) and be accessible. If the image watermark is set to private-read, it must carry a signature.
3. Have a URL starting with `http://`. Note that "http://" cannot be omitted or changed to "https://". For example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` and `https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` are invalid watermark URLs.

#### Sample code
```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
        $blindWatermarkTemplate = new Qcloud\Cos\ImageParamTemplate\BlindWatermarkTemplate(); //Create a blind watermark parameter template instance
        $blindWatermarkTemplate->setType(3); //Blind watermark type. Valid values: `1` (semi-blind), `2` (perfectly blind), `3` (text)
        $blindWatermarkTemplate->setImage("imageUrl"); //Set the blind watermark image URL
        $blindWatermarkTemplate->setText("Test"); //Set the blind watermark text
        $blindWatermarkTemplate->setLevel(3); //Perfectly blind watermark level, which only takes effect when `type` is set to `2`. Valid values: `1` (default), `2`, `3`
        $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'ImageHandleParam' => $blindWatermarkTemplate->queryString(), //Generate blind watermark parameters
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
| Key | String | Uniquely identifies an object in a bucket. For example, if the object access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg`.  | Yes |
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

## Extracting Blind Watermarks

The image URL must be entered according to the blind watermark type:
1. For a semi-blind watermark, the blind watermark image URL is required and must be the original image URL.
2. For a perfectly blind watermark, the blind watermark image URL is required and must be the watermark image URL.
3. For a text blind watermark, the blind watermark image URL is invalid and does not need to be entered.

The specified watermark image must:
1. Be stored in the same bucket as the input image.
2. Have a URL containing a COS domain name (a CDN acceleration domain name such as `examplebucket-1250000000.file.myqcloud.com/shuiyin_2.png` is unsupported) and be accessible. If the image watermark is set to private-read, it must carry a signature.
3. Have a URL starting with `http://`. Note that "http://" cannot be omitted or changed to "https://". For example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` and `https://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/shuiyin_2.png` are invalid watermark URLs.

#### Sample code

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
            
try {
        $blindWatermarkTemplate = new Qcloud\Cos\ImageParamTemplate\BlindWatermarkTemplate(); //Create a blind watermark parameter template instance
        $blindWatermarkTemplate->setPick(); //Enable blind watermark extraction
        $blindWatermarkTemplate->setType(3); //Blind watermark type. Valid values: `1` (semi-blind), `2` (perfectly blind), `3` (text)
        $blindWatermarkTemplate->setImage("imageUrl"); //Set the blind watermark image URL
        $blindWatermarkTemplate->setText("Test"); //Set the blind watermark text
        $blindWatermarkTemplate->setLevel(3); //Perfectly blind watermark level, which only takes effect when `type` is set to `2`. Valid values: `1` (default), `2`, `3`. The larger the value, the better the blind watermarking effect.
        $picOperationsTemplate = new \Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation(); //Create a parameter template instance for persistent image processing
        $picOperationsTemplate->setIsPicInfo(1); //Set whether to return the input image information. `0` (default): no; `1`: yes
        $picOperationsTemplate->addRule($blindWatermarkTemplate, "resultobject"); //Set presistent image processing parameters
        $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'Body' => fopen('path/to/localFile', 'rb'), 
        'PicOperations' => $picOperationsTemplate->queryString(), //Generate parameters for presistent image processing
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
| Key | String | Uniquely identifies an object in a bucket. For example, if the object access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg`.  | Yes |
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
