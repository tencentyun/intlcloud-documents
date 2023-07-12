## Overview

This document provides an overview of APIs and SDK code samples for querying object metadata.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object. |

## Querying Object Metadata

#### Feature description

The API (`HEAD Object`) is used to query object metadata.

#### Method prototype

```php
public Guzzle\Service\Resource\Model headObject(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-head-object)

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
    $result = $cosClient->headObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
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
| --------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key is the unique identifier of an object in a bucket. For example, in the object's access domain name <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is `doc/pic.jpg`. | Yes |
| VersionId | String | Version ID of the specified file if versioning is enabled | No  |

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [DeleteMarker] => 
            [AcceptRanges] => 
            [Expiration] => 
            [Restore] => 
            [LastModified] => Tue, 02 Apr 2019 12:38:09 GMT
            [ContentLength] => 238186
            [ETag] => "af9f3b8eaf64473278909183abba1e31"
            [MissingMeta] => 
            [VersionId] => 
            [CacheControl] => 
            [ContentDisposition] => 
            [ContentEncoding] => 
            [ContentLanguage] => 
            [ContentType] => text/plain; charset=utf-8
            [Expires] => 
            [ServerSideEncryption] => 
            [Metadata] => Array
                (
                    [md5] => af9f3b8eaf64473278909183abba1e31
                )
            [SSECustomerAlgorithm] => 
            [SSECustomerKeyMD5] => 
            [SSEKMSKeyId] => 
            [StorageClass] => 
            [RequestCharged] => 
            [ReplicationStatus] => 
            [RequestId] => NWNhMzU3Y2ZfMzFhYzM1MGFfODdhMF8xOTExM2U=
            [CRC] => 16749565679157681890
        )

)
```

#### Response description

| Parameter Name | Type | Description | Parent Node | 
| -------------------- | ------ | -------------------------------------------------- | ------ |
| CacheControl | String | Cache policy | None |
| ContentDisposition | String | File name | None |
| ContentEncoding | String | Encoding format | None |
| ContentLanguage | String | Language type | None |
| ContentLength | Int | Length of the uploaded content | None |
| ContentType | String | Content type | None |
| Metadata | Array | User-defined file metadata | None | 
| StorageClass | String | Storage class of the object, such as `STANDARD`, `STANDARD_IA`, and `ARCHIVE`. For more information, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | None |
| ServerSideEncryption | String | Server-side encryption method | None |
| ETag | String | MD5 checksum of the file | None |
| Restore | String | Restoration information of the archived file | None |
| CRC     | String | CRC64 for [Data Verification](https://intl.cloud.tencent.com/document/product/436/34078) | No |