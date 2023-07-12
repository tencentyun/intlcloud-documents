## Overview

This document provides an overview of APIs and SDK code samples for persistent image processing.

| API | Description |
| :----------------------------------------------------------- | :----------------------------------- |
| [Persistent image processing](https://intl.cloud.tencent.com/document/product/436/40592) | Processes an image during upload, or processes an image stored in COS and saves the processing result to COS. |


## Processing During Upload

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
        $imageMogrTemplate->thumbnailByScale(50);// Scale an image to 50% of its original width and height
        $picOperationsTemplate = new \Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();// Create an instance of the persistent image processing parameter template
        $picOperationsTemplate->setIsPicInfo(1);// Set whether to return the input image information. Valid values: 0 (no), 1 (yes). Default value: 0.
        $picOperationsTemplate->addRule($imageMogrTemplate, "resultobject");// Set the image processing rule
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

## Processing In-Cloud Data

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
        $imageMogrTemplate->thumbnailByScale(50);// Scale an image to 50% of its original width and height
        $picOperationsTemplate = new \Qcloud\Cos\ImageParamTemplate\PicOperationsTransformation();// Create an instance of the persistent image processing parameter template
        $picOperationsTemplate->setIsPicInfo(1);// Set whether to return the input image information. Valid values: 0 (no), 1 (yes). Default value: 0.
        $picOperationsTemplate->addRule($imageMogrTemplate, "resultobject");// Set the image processing rule
        $result = $cosClient->ImageProcess(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
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
| PicOperations    | Json/String      | Persistent image processing information                                  | Yes       |


#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
    (
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [Key] => exampleobject
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
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

```

#### Response description

| Parameter | Type | Description | Parent Node |
| ------------------ | --------- | --------------------------------| ------ |
| RequestId             | String      | Request ID                                | None     |
| Key                  | String      | Object key                                    | None     |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Location             | String      | Address of the requested resource                                 | None     |
| OriginalInfo         | Array      | Input image information                                   | None     |
| ProcessResults       | Array      | Image processing result                             |  None     |

