## Overview

This document provides an overview of APIs and SDK code samples for copying and moving an object.

| API | Operation | Description |
| ------------------------------------------------------------ | ---------------------------- | ---------------------- |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object (modifying object attributes) | Copies a file to a destination path |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part. |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting an object | Deletes a specified object from a bucket. |

## Advanced APIs (Recommended)

### Copying objects

#### Feature description

This API is used to copy an object. It calls the `PUT Object - Copy` API for small files, and the `Upload Part - Copy` API for large files. This API is usually used to modify object attributes. For the parameters required, see those of the `PUT Object - Copy` and `Upload Part - Copy` APIs.

#### Sample request

#### Sample 1. Copying an object

[//]: # (.cssg-snippet-transfer-copy-object)

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
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        $key = 'exampleobject', // Object key
        $copySorce = array(
            'Region' => 'COS_REGION', 
            'Bucket' => 'sourcebucket-1250000000', 
            'Key' => 'sourceobject', 
        )
    );
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

[//]: # (.cssg-snippet-transfer-copy-object-update-storage-class)

#### Sample 2. Changing the object storage class

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
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        $key = 'exampleobject', // Object key
        $copySorce = array(
            'Region' => 'COS_REGION', 
            'Bucket' => 'examplebucket-1250000000', 
            'Key' => 'exampleobject', 
        ),
        $options = array(
            'StorageClass' => 'Archive'
        )
    );
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

[//]: # (.cssg-snippet-transfer-copy-object-update-metadata)

#### Sample 3. Modifying object storage attributes

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
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        $key = 'exampleobject', // Object key
        $copySorce = array(
            'Region' => 'COS_REGION', 
            'Bucket' => 'sourcebucket-1250000000', 
            'Key' => 'sourceObject', 
        ),
        $options = array(
            'MetadataDirective' => 'Replaced',
            'Metadata' => array(
                'string' => 'string',
            ),
        )
    );
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```
## Simple Copy
### Copying an object

This API (`PUT Object - Copy`) is used to copy an object to the destination path.

#### Method prototype

```php
public Guzzle\Service\Resource\Model copyObject(array $args = array());
```

#### Sample request

#### Sample 1. Copying an object

[//]: # (.cssg-snippet-copy-object)

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
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 2. Copying a specified version of an object

[//]: # (.cssg-snippet-copy-object-with-versionId)

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
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject?versionId=MTg0NDUxNjI3NTM0ODE2Njc0MzU',
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 3. Modifying the storage class to `ARCHIVE`

[//]: # (.cssg-snippet-copy-object-update-storage-class)

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
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
        'StorageClass' => 'Archive'
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 4. Modifying metadata

[//]: # (.cssg-snippet-copy-object-update-metadata)

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
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
        'MetadataDirective' => 'Replaced',
        'Metadata' => array(
            'key1' => 'value1',
            'key2' => 'value2',
        )
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
| ----------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key is the unique identifier of an object in a bucket. For example, in the object’s access domain name <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the `Key` is `doc/pic.jpg`. | Yes |
| CopySource | String | Path of the source object, which contains `APPID`, `Bucket`, `Key`, and `Region`, <br>such as `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` | Yes |
| MetadataDirective | String | Valid values: `Copy`: ignores the configured metadata and copies the file directly; `Replaced`: modifies the metadata according to the configured metadata. If the destination path is identical to the source path, this parameter must be set to `Replaced`. | No |

## Multipart Copy

>? This section presents all relevant APIs which are the same as those in **Uploading Objects**.
>

### Querying a part

#### Feature description

This API (`List Multipart Uploads`) is used to query in-progress multipart uploads in a specified bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model listMultipartUploads(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-list-multi-upload)

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
    $result = $cosClient->listMultipartUploads(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Delimiter' => '/',
        'EncodingType' => 'url',
        'KeyMarker' => 'prfixKeyMarker',
        'UploadIdMarker' => 'string',
        'Prefix' => 'prfix',
        'MaxUploads' => 1000,
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
| -------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Delimiter | String | Delimiter, left empty by default. For example, you can set it to `/` to indicate folders. | No |
| EncodingType | String | Encoding method of the returned value. The value is not encoded by default. Valid value: `url`  | No |
| KeyMarker | String | The key of the object after which the returned part list begins | No |
| UploadIdMarker | String | The upload ID of the object after which the returned part list begins                            | No |
| Prefix | String | Key prefix to query parts by, left empty by default   | No |
| MaxUploads  | Int | Maximum number of returned parts, which is `1000` (the maximum value allowed) by default | No |


#### Response description

| Parameter Name | Type | Description | Parent Node | 
| ------------ | ------ | ---------------------------------- | ------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| IsTruncated | Int    | Whether the returned objects are truncated | None |
| Uploads | Array  | List of returned parts                     | None |
| Upload | Array  | Attributes of the returned parts | Uploads |
| Key | String | Object key | Upload  |
| UploadId | String | ID of the multipart upload                 | Upload  |
| Initiator    | String | Initiator of the multipart upload | Upload  |
| Owner        | String | Owner of the parts | Upload  |
| StorageClass | String | Storage class of the parts | Upload  |
| Initiated    | String | Initiation time of the multipart upload | Upload  |



### Initializing multipart upload

#### Feature description

This API (`Initiate Multipart Upload`) is used to initialize a multipart upload.

#### Method prototype

```php
public Guzzle\Service\Resource\Model createMultipartUpload(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-init-multi-upload)

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
    $result = $cosClient->createMultipartUpload(array(
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

| Parameter Name | Type | Description | Required |
| -------------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key is the unique identifier of an object in a bucket. For example, in the object’s access domain name <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the `Key` is `doc/pic.jpg`. | Yes |
| CacheControl | String | Cache policy | No |
| ContentDisposition | String | File name | No |
| ContentEncoding | String | Encoding format | No |
| ContentLanguage | String | Language type | No |
| ContentLength | Int | Length of the content | No |
| ContentType | String | Content type | No |
| Expires | String | `Content-Expires` | No |
| Metadata | Array | User-defined file metadata | No |
| StorageClass | String | Storage class of the object, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | No |
| ContentMD5           | Boolean | Whether to upload the MD5 checksum of the file for verification                           | No       |
| ServerSideEncryption | String | Server-side encryption method | No |


#### Response description

| Parameter Name | Type | Description | Parent Node | 
| -------- | ------ | ---------------------------------- | ------ |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Key  | String | Object key | None |
| UploadId  | String | ID of the multipart upload | None |


### Copying an object part

#### Feature description

This API (`Upload Part - Copy`) is used to copy a part of an object.

#### Method prototype

```php
public Guzzle\Service\Resource\Model uploadPartCopy(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-upload-part-copy)

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
    $result = $cosClient->uploadPartCopy(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject', 
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
        'CopySourceRange' => 'bytes=0-1', // Copy only the first 2 bytes
        'UploadId' => 'exampleUploadId', // ID of the multipart upload, which you can get in the response returned after multipart upload initialization 
        'PartNumber' => 1, // Sequential number of a part, which COS uses to reassemble parts
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
| ------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key | Yes |
| UploadId | String | ID of the multipart upload, which you can get in the response returned after multipart upload initialization  | Yes |
| CopySource | String | Path to the source object, which contains `APPID`, `Bucket`, `Key`, and `Region`, <br>for example, `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` | Yes |
| CopySourceRange | String | Byte range of the source object to copy in the format of `bytes=first-last`. If no range is specified, the entire source object will be copied. | No |
| PartNumber | Int | Sequential number of a part, which COS uses to reassemble parts | Yes |
| ContentLength | Int | Length of the content | No |
| ContentMD5           | Boolean | Whether to upload the MD5 checksum of the file for verification                           | No       |

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [ETag] => "96e79218965eb72c92a549dd5a330112"
            [LastModified] => "2017-09-04T04:45:45"
            [RequestId] => NWNhNDdjYWFfNjNhYjM1MGFfMjk2NF8xY2ViMWM=
            [CRC] => 16749565679157681890
        )

)
```

#### Response description

| Parameter Name | Type | Description | Parent Node | 
| ------------ | ------ | ------------------------------ | ------ |
| ETag | String | MD5 checksum of the part | None |
| LastModified | String | Time when the object was last modified, in GMT format | None |
| CRC     | String | [CRC64 check](https://intl.cloud.tencent.com/document/product/436/34078) code for data verification | No |


### Completing multipart upload

#### Feature description

This API (`Complete Multipart Upload`) is used to complete the multipart upload of a file.

#### Method prototype

```php
public Guzzle\Service\Resource\Model completeMultipartUpload(array $args = array());

```

#### Sample request

[//]: # (.cssg-snippet-complete-multi-upload)

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
    $result = $cosClient->completeMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject', 
        'UploadId' => 'exampleUploadId',
        'Parts' => array(
            array(
                'ETag' => 'exampleETag',
                'PartNumber' => 1,
            )), 
            // ... repeated
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
| ---------- | ------ | ---------------------------------- | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key | Yes |
| UploadId  | String | ID of the multipart upload | Yes |
| Parts | Array  | List of parts | Yes |
| Part | Array | Information of the uploaded parts | Yes |
| ETag | String | MD5 checksum of the part | Yes |
| PartNumber | Int | Part number | Yes |

## Moving an Object

Object movement involves copying the source object to the target location and deleting the source object.

Since COS uses the bucket name (`Bucket`) and object key (`ObjectKey`) to identify objects, moving an object will modify the object identifier. COS’s PHP SDK does not provide a stand-alone API to modify object identifiers. However, you can still move the object with a combination of basic operations (**object copy** and **object delete**).

For example, if you want to move the `picture.jpg` object to the “doc” directory that is in the same bucket (`mybucket-1250000000`), you can copy the `picture.jpg` to the “doc” directory (making the object key `doc/picture.jpg`) and then delete the source object.

Likewise, if you need to move `picture.jpg` in the `mybucket-1250000000` bucket to another bucket `myanothorbucket-1250000000`, you can copy the object to the `myanothorbucket-1250000000` bucket first and then delete the source object.



#### Sample code

[//]: #	".cssg-snippet-move-object"

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
    $cosClient->copy(
        $bucket = 'examplebucket-125000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        $key = 'exampleobject',
        $copySource = array(
            'Region' => '<sourceRegion>', 
            'Bucket' => '<sourceBucket>', 
            'Key' => '<sourceKey>', 
        )
    );
    $result = $cosClient->deleteObject(array(
        'Bucket' => 'examplebucket-125000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

