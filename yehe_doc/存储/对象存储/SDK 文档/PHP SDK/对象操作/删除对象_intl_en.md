## Overview

This document provides an overview of APIs and SDK code samples for object deletion.

| API | Operation |  Description |
| ------------------------------------------------------------ | ------------ | ---------------------- |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting object | Deletes specified object from bucket. |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from bucket. |


## Deleting One Object

#### Feature description

This API is used to delete a specified object (file) from a bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model deleteObject(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-delete-object)

#### Sample 1. Deleting an object
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
    $result = $cosClient->deleteObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject' // If there are multiple paths, write `folder/exampleobject`. Do not add `/` at the first level; otherwise, the deletion will fail.
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```
#### Sample 2. Deleting an object with a version ID
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
    $result = $cosClient->deleteObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject', // If there are multiple paths, write `folder/exampleobject`. Do not add `/` at the first level; otherwise, the deletion will fail.
        'VersionId' => 'exampleVersionId' // Do not carry this parameter if versioning is not enabled for the bucket.
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```


#### Parameter description

| Parameter | Type | Description | Required |
| --------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key       | String | Object key, which is the unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | Yes       |
| VersionId | String | Version ID of the file to be deleted                                             | No       |

## Deleting Multiple Objects

#### Feature description

This API is used to delete multiple objects (files) from a specified bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model deleteObjects(array $args = array());
```

#### Sample request

#### Sample 1. Deleting multiple objects
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
    $result = $cosClient->deleteObjects(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Objects' => array(
            array(
                'Key' => 'exampleobject', // If there are multiple paths, write `folder/exampleobject`. Do not add `/` at the first level; otherwise, the deletion will fail.
            ),  
            // ... repeated
        ),  
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 2. Deleting multiple objects with version IDs


[//]: # (.cssg-snippet-delete-multi-object)

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
    $result = $cosClient->deleteObjects(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Objects' => array(
            array(
                'Key' => 'exampleobject', // If there are multiple paths, write `folder/exampleobject`. Do not add `/` at the first level; otherwise, the deletion will fail.
                'VersionId' => 'string' // Do not carry this parameter if versioning is not enabled for the bucket.
            ),  
            // ... repeated
        ),  
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

## Deleting Objects with Specified Prefix (Deleting Folder)

#### Feature description

This API is used to delete a folder from a bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model deleteObjects(array $args = array());
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

$cos_prefix = "cos/folder";
$nextMarker = '';
$isTruncated = true;
while ( $isTruncated ) {
    try {
        $result = $cosClient->listObjects(
            ['Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
            'Delimiter' => '',
            'EncodingType' => 'url',
            'Marker' => $nextMarker,
            'Prefix' => $cos_prefix,
            'MaxKeys' => 1000]
        );    
        $isTruncated = $result['IsTruncated'];
        $nextMarker = $result['NextMarker'];
        foreach ( $result['Contents'] as $content ) {
            $cos_file_path = $content['Key'];
            $local_file_path = $content['Key'];
            // Splice a download path as needed
            try {
                $cosClient->deleteObject(array(
                    'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
                    'Key' => $cos_file_path,
                ));
                echo ( $cos_file_path . "\n" );
            } catch ( \Exception $e ) {
                echo( $e );
            }
        }
    } catch ( \Exception $e ) {
        echo( $e );
    }
}
```


#### Parameter description

| Parameter | Type | Description | Required |
| --------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Objects   | Array  | List of objects to be deleted                                                 | Yes       |
| Object   | Array  | Object to be deleted                                                 | Yes       |
| Key       | String | Object key, which is the unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | Yes       |
| VersionId | String | Version ID of the file to be deleted                                             | No       |

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Deleted] => Array
                (
                    [0] => Array
                        (
                            [Key] => exampleobject1
                        )
                )
            [Errors] => Array
                (
                    [0] => Array
                        (
                            [Key] => exampleobject2
                            [Code] => 
                            [Message] => 
                        )
                )
            [RequestId] => NWNhZWYzYWNfMTlhYTk0MGFfNGRjX2MzZTVhOQ==
        )
）
```

#### Response description

| Parameter | Type | Description | Parent Node |
| -------- | ------ | -------------------- | -------------- |
| Deleted | Array | List of successfully deleted objects | None |
| Errors   | Array  | List of objects that failed to be deleted | None |
| Key      | String | Object key | Deleted/Errors |
| Code     | String | Error code for failed operations | Errors |
| Message  | String | Error message for failed operations | Errors |
