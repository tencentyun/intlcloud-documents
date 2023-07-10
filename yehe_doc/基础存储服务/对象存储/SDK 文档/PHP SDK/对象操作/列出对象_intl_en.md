## Overview

This document provides an overview of APIs and SDK code samples for listing objects.

| API                                                          | Operation                   | Description                                       |
| ------------------------------------------------------------ | ------------------------ | ---------------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying objects | Queries some or all the objects in a bucket. |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | Querying objects and their version history | Queries some or all the objects in a bucket and their version history. |


## Querying an Object List

#### Feature description

This API (`List Objects`) is used to query all the objects in a specified bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model listObjects(array $args = array());
```

#### Sample request

#### Sample 1. Querying a list of objects with the specified prefix starting from a specified object

[//]: # (.cssg-snippet-get-bucket-comp)

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual `region`, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    $result = $cosClient->listObjects(array(
        'Bucket' => 'examplebucket-125000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Delimiter' => '/', // Delimiter: "/". // Set the delimiter to "/" to list objects in the current directory. To list all objects, leave this parameter empty.
        'EncodingType' => 'url',// Encoding format, which indicates the `encoding-type` in requests
        'Marker' => 'prefix/picture.jpg',// Marker of the starting object key
        'Prefix' => 'prfix/', // Set a prefix to indicate that the key of the listed object starts with the prefix.
        'MaxKeys' => 1000, // Set the maximum number of traversed objects (up to 1,000 per `listObjects` request)
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| ------------ | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Delimiter | String | Separator, left empty by default. For example, you can set it to `/` to indicate folders. | No |
| EncodingType | String | Encoding method of the returned value. The value is not encoded by default. Valid value: `url`  | No |
| Marker | String | The object after which the returned list begins. Objects are listed in UTF-8 binary order by default.  | No |
| Prefix | String | Key prefix to query objects by, left empty by default | No |
| MaxKeys | Int | The maximum number of returned objects, which is `1000` (the maximum value allowed) by default | No |

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Name] => examplebucket-1250000000
            [Prefix] => doc
            [Marker] => doc/picture.jpg
            [MaxKeys] => 10
            [IsTruncated] => 1
            [NextMarker] => doc/exampleobject
            [Contents] => Array
                (
                    [0] => Array
                        (
                            [Key] => doc/exampleobject
                            [LastModified] => 2019-02-14T12:20:40.000Z
                            [ETag] => "e37b429559d82e852af0b2f5b4d078ab72b90208"
                            [Size] => 6532594
                            [Owner] => Array
                                (
                                    [ID] => 100000000001
                                    [DisplayName] => 100000000001
                                )

                            [StorageClass] => STANDARD
                        )

                    [1] => Array
                        (
                            [Key] => doc/exampleobject2
                            [LastModified] => 2019-03-04T06:34:43.000Z
                            [ETag] => "988f9f28e68eba9b8c1f5f98ccce0a3c"
                            [Size] => 28
                            [Owner] => Array
                                (
                                    [ID] => 100000000001
                                    [DisplayName] => 100000000001
                                )

                            [StorageClass] => STANDARD
                        )
                )
            [RequestId] => NWNhMzM0MmZfOWUxYzBiMDlfOTk2YV83ZWE3ODE=
        )

)
```

#### Response description

| Parameter | Type | Description | Parent Node | 
| ------------ | ------ | ------------------------------------------------------------ | -------- |
| Name | String | Bucket name in the format of `BucketName-APPID`                         | None |
| Delimiter | String | Separator. For example, you can set it to `/` to indicate folders. | None |
| EncodingType | String | Encoding method of the returned value | None |
| Marker | String | The object after which the returned list begins. Objects are listed in UTF-8 binary order by default. Set the returned `Key` to `Marker` to turn pages | None |
| Prefix | String | Key prefix by which objects are queried       | None |
| MaxKeys | Int | The maximum number of returned objects, which is `1000` (the maximum value allowed) by default | None |
| IsTruncated | Int    | Whether the returned objects are truncated | None |
| Contents     | Array  | Returned object list                                              | None       |
| Content | Array | List of the metadata (attributes) of all returned objects, including 'ETag', 'StorageClass', 'Key', 'Owner', 'LastModified', and 'Size' | Contents |

## Querying objects and their version history 

#### Feature description

This API is used to query some or all the objects in a bucket and their version history.

#### Method prototype

```
public Guzzle\Service\Resource\Model listObjectVersions(array $args = array());
```

#### Sample request

#### Sample 1. Querying objects and their version history

[//]: # (.cssg-snippet-list-object-versioning)

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual `region`, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    $result = $cosClient->listObjectVersions(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Delimiter' => '',
        'EncodingType' => 'url',
        'KeyMarker' => 'doc/picture.jpg',
        'VersionIdMarker' => 'MTg0NDUxODMyMTE2ODY0OTExOTk3W',
        'Prefix' => 'doc',
        'MaxKeys' => 1000,
    )); 
    print_r($result);
} catch (\Exception $e) {
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| --------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket   | String | Bucket name in the format of `BucketName-APPID`     | Yes |
| Prefix | String  | Key prefix to query objects by, which is left empty by default | No |
| Delimiter | String | Separator, left empty by default. For example, you can set it to `/` to indicate folders. | No |
| KeyMarker | String      | The key of the object after which the returned object list begins. Entries are listed in UTF-8 binary order by default. | No   |
| VersionIdMarker | String  | The version ID of the object after which the returned object list begins. Entries are listed in UTF-8 binary order by default. | No |
| MaxKeys | Int  | The maximum number of returned objects, which is `1000` (the maximum value allowed) by default | No |
| EncodingType | String | Encoding method of the returned value. The value is not encoded by default. Valid value: `url`  | No |

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Name] => examplebucket-1250000000
            [Prefix] => doc
            [KeyMarker] => string
            [VersionIdMarker] => string
            [MaxKeys] => 10
            [IsTruncated] => 1
            [NextKeyMarker] => string
            [NextVersionIdMarker] => string
            [Versions] => Array
                (
                    [0] => Array
                        (
                            [Key] => doc/exampleobject1
                            [VersionId] => null
                            [IsLatest] => 1
                            [LastModified] => 2019-06-13T09:24:52.000Z
                            [ETag] => "96e79218965eb72c92a549dd5a330112"
                            [Size] => 6
                            [StorageClass] => STANDARD
                            [Owner] => Array
                                (
                                    [UID] => 1250000000
                                )
                        )

                    [1] => Array
                        (
                            [Key] => doc/exampleobject2
                            [VersionId] => MTg0NDUxODMyMTE2ODY0OTExOTk
                            [IsLatest] => 1
                            [LastModified] => 2019-06-18T12:47:03.000Z
                            [ETag] => "698d51a19d8a121ce581499d7b701668"
                            [Size] => 3
                            [StorageClass] => STANDARD
                            [Owner] => Array
                                (
                                    [UID] => 1250000000
                                )
                        )
                    )
            [RequestId] => NWQwOGVkZGRfMjViMjU4NjRfODNjN18xMTE5YWI4
        )

)
```

#### Response description

| Parameter Name | Type | Description | Parent Node | 
| ------------------- | ------ | ------------------------------------------------------------ | -------- |
| Name | String | Bucket name in the format of `BucketName-APPID`                         | None |
| Delimiter | String | Separator, left empty by default. For example, you can set it to `/` to indicate folders. | None |
| EncodingType | String | Encoding method of the returned value | None |
| KeyMarker | String  | The key of the object after which the returned object list begins. Entries are listed in UTF-8 binary order by default.  | None |
| VersionIdMarker | String |  The version ID of the object after which the returned object list begins. Entries are listed in UTF-8 binary order by default.   |  None |
| NextKeyMarker | String | The key of the object after which the next returned list begins if `IsTruncated` is `true` | None |
| NextVersionIdMarker | String | The version ID of the object after which the next returned list begins if `IsTruncated` is `true` | None |
| Prefix | String | Key prefix by which objects are queried       | None |
| MaxKeys | Int | The maximum number of returned objects, which is `1000` (the maximum value allowed) by default | None |
| IsTruncated | Int    | Whether the returned objects are truncated | None |
| Versions            | Array  | List of the metadata of all objects with multiple versions                            | None       |
| Version | Array | List of the metadata of all objects with multiple versions, including `ETag`, `StorageClass`, `Key`, `VersionId`, `IsLatest`, `Owner`, `LastModified`, and `Size` | Versions |
| CommonPrefixes | Array  | All objects starting with the specified prefix and ending with the specified delimiter | None |
