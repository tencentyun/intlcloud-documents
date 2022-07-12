
## Overview

This document provides an overview of APIs and SDK code samples for image styles.

| API | Description |
| :----------------------------------------------------------- | :--------- |
| [Adding style](https://intl.cloud.tencent.com/document/product/1045/33708)  | Adds a style to a bucket. |
| [Querying styles](https://intl.cloud.tencent.com/document/product/1045/33707)  | Queries styles set for a bucket.  |
| [Deleting style](https://intl.cloud.tencent.com/document/product/1045/33709)   | Deletes a style from a bucket. |


## Adding Style

#### Feature description

This API is used to add a style to a bucket. This style will be added to images subsequently uploaded to this bucket.

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
        $result = $cosClient->PutBucketImageStyle(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'StyleName' => 'style_name',// Style name
        'StyleBody' => 'imageMogr2/thumbnail/!50px', // Style information
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
| StyleName          | String      | Style name | Yes |
| StyleBody          | String      | Style information | Yes |


#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.pic.ap-beijing.myqcloud.com/
        )
)

```

#### Response description

| Parameter | Type | Description | Parent Node |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| RequestId             | String      | Request ID                                | None     |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Location             | String      | Address of the requested resource                                 | None     |

## Querying Styles

#### Feature description

This API is used to query the styles set for a bucket.

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
        $result = $cosClient->GetBucketImageStyle(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'StyleName' => 'style_name', // Style name
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
| StyleName       | String      | Style name | No |


#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.pic.ap-beijing.myqcloud.com/
            [StyleRule] => Array(
                [0] => Array(
                    [StyleName] => style_name
                    [StyleBody] => imageMogr2/thumbnail/!50px
                )
            )
       )
)

```

#### Response description

| Parameter | Type | Description | Parent Node |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| RequestId             | String      | Request ID                                | None     |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Location             | String      | Address of the requested resource                                 | None     |
| StyleRule             | Array      | List of style information      | None |

## Deleting Style

#### Feature description

This API is used to delete a style from a bucket.

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
        $result = $cosClient->DeleteBucketImageStyle(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'StyleName' => 'style_name', // Style name
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
| StyleName       | String      | Style name     | Yes |


#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.pic.ap-beijing.myqcloud.com/
       )
)

```

#### Response description

| Parameter | Type | Description | Parent Node |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| RequestId             | String      | Request ID                                | None     |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Location             | String      | Address of the requested resource                                 | None     |

