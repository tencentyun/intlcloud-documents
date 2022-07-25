## Overview

This document provides an overview of APIs and SDK code samples for image QR codes.

| API | Description |
| :----------------------------------------------------------- | :--------- |
| QR code recognition | Recognizes the location and content of valid QR codes in an image, outputs the text information (URL or text) contained in the QR codes, and pixelates the recognized QR codes. |
| QR code generation | Generates QR codes or barcodes based on the specified text information (URL or text). |

## QR Code Recognition

#### Feature description

The QR code recognition feature recognizes the location and content of valid QR codes in an image, outputs the text information (URL or text) contained in the QR codes, and pixelates the recognized QR codes.

#### Sample request 1: Recognizing during upload

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
        $imageQrcodeTemplate = new Qcloud\Cos\ImageParamTemplate\ImageQrcodeTemplate();// Create an instance of the QR code recognition parameter template
        $imageQrcodeTemplate->setMode(0);// Pixelate the recognized QR code. Valid values: 0 (no), 1 (yes). Default value: 0.
        $picOperationsTemplate = new \Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();// Create an instance of the persistent image processing parameter template
        $picOperationsTemplate->setIsPicInfo(1);// Set whether to return the input image information. Valid values: 0 (no), 1 (yes). Default value: 0.
        $picOperationsTemplate->addRule($imageQrcodeTemplate, "resultobject");// Set persistent image processing parameters
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
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
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
            [ContentLength] => 238186
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
                            [CodeStatus] => 1
                            [QRcodeInfo] => Array
                            (
                                    [0] => Array
                                    (
                                            [CodeUrl] => xxxxxxxxxxxxx
                                            [CodeLocation] => Array
                                            (
                                                    [Point] => Array
                                                    (
                                                            [0] => 100,100
                                                            [1] => 100,200
                                                            [2] => 200,200
                                                            [3] => 200,100
                                                    )
                                             )
                                    )
                            )
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
| Data                 | Array      | Image processing result (QR code information)                     | None     |

#### Sample request 2: Recognizing during download

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
        $result = $cosClient->Qrcode(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'Cover' => 1,// QR code pixelation feature
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
| Cover            | Int      | Pixelates the recognized QR code. Valid values: 0 (no), 1 (yes). Default value: 0. | Yes        |


#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
    (
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [ContentLength] => 238186
            [Key] => exampleobject
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
            [CodeStatus] => 1
            [QRcodeInfo] => Array
            (
                    [0] => Array
                    (
                            [CodeUrl] => xxxxxxxxxxxxx
                            [CodeLocation] => Array
                            (
                                    [Point] => Array
                                    (
                                            [0] => 100,100
                                            [1] => 100,200
                                            [2] => 200,200
                                            [3] => 200,100
                                    )
                             )
                    )
            )
            [ResultImage] =>
            
    )
)

```

#### Response description

| Parameter | Type | Description | Parent Node |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| RequestId             | String      | Request ID                                | None     |
| ContentLength | Int | Length of the response body | None |
| Key                  | String      | Object key                                    | None     |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Location             | String      | Address of the requested resource                                 | None     |
| CodeStatus           | Int         | Whether QR codes are recognized. 0: no; 1: yes. | None     |
| QRcodeInfo           | Array      | Recognized QR code. There may be multiple ones.                        | None     |
| ResultImage          | String    | Base64-encoded result image data, which will be returned if the request parameter `cover` is 1.    | None     |

## QR Code Generation

#### Feature description

The QR code generation feature generates QR codes or barcodes based on the specified text information (URL or text).

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
        $result = $cosClient->QrcodeGenerate(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'QrcodeContent' => '<https://www.example.com>',// Recognizable QR code text information
        'QrcodeMode' => 0 // Type of the QR code to be generated. Valid values: 0 (QR code), 1 (barcode). Default value: 0.
        'QrcodeWidth' => '200',// Width of the QR code or barcode to be generated. The height will be compressed proportionally.
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
| -------------------- | ----------- | ------------------------------------------- | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| QrcodeContent        | String      | Recognizable QR code text information                         |     Yes   |
| QrcodeMode          | Int         | Type of the QR code to be generated. Valid values: 0 (QR code), 1 (barcode). Default value: 0.   | Yes   |
| QrcodeWidth         | String      | Width of the QR code or barcode to be generated. The height will be compressed proportionally.      | Yes       |


#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
    (
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/
            [ResultImage] =>
    )
)

```

#### Response description

| Parameter | Type | Description | Parent Node |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| RequestId             | String      | Request ID                                | None     |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Location             | String      | Address of the requested resource                                 | None     |
| ResultImage          | String    | Base64-encoded result image data                          | None     |
