## Overview

This document provides an overview of APIs and SDK code samples for uploading an object.

**Simple upload**

| API                                                          | Operation                   | Description                                       |
| ------------------------------------------------------------ | ------------------------ | ---------------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object in whole | Uploads an object in whole to a bucket. |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object (modifying object attributes) | Copies a file to a destination path |
| [APPEND Object](https://intl.cloud.tencent.com/document/product/436/7741) | Appending parts | Appends object parts to a bucket.                      |

**Multipart upload**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload. |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads an object in multiple parts. |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a multipart upload. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of an object. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts. |


## Advanced APIs (Recommended)

This section is about the advanced upload and copy APIs COS provides. Pass in the parameters required, and the APIs will determine whether to upload (copy) an object in whole or in parts based on the file size. Before using the APIs, make sure you have completed the initialization step in [Getting Started](https://intl.cloud.tencent.com/document/product/436/12266).

### Uploading an object (checkpoint restart)

#### Method prototype

```php
public Qcloud\Cos\Client upload(string $bucket, string $key, $body, array $options = array());
```
#### Feature description

This API is used to upload an object. It calls the `PUT Object` API for small files, and the `Upload Part` API for large files. For the parameters required, see those of the `PUT Object` and `Upload Part` APIs.

#### Parameter description

| Parameter | Type | Description | Required |
| -------- | ------ | ---------------------------------- | -------- |
| bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| key      | String | Object key                             | Yes       |
| body                 | Stream/String | Content to upload                                                   | Yes       |
| options     | Array | Additional configuration items            | No       |



| options Parameter | Type   | Description | Required |
| -------- | ------ | ---------------------------------- | -------- |
| Progress         | Function      | Progress callback. `$totalSize` indicates the total size, and `$uploadedSize` indicates the uploaded size. | No       |
| PartSize         | Int      | Minimum part size. Default value: 5 MB | No       |
| Concurrency         | Int      | Concurrency. Default value: 10 | No       |
| ACL | String | ACL of the object, such as `private` or `public-read` | No |
| CacheControl | String | Cache policy | No |
| ContentDisposition | String | File name | No |
| ContentEncoding | String | Encoding format | No |
| ContentLanguage | String | Language type | No |
| ContentLength | Int | Length of the content | No |
| ContentType | String | Content type | No |
| Expires | String | `Content-Expires` | No |
| Metadata             | Array       | User-defined file metadata                                       | No       |
| StorageClass | String | Storage class of the object, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | No |
| ContentMD5           | Boolean      | Whether to upload the MD5 checksum of the file for verification                                  | No       |
| ServerSideEncryption | String | Server-side encryption method | No |

#### Sample request

#### Sample 1. Uploading a local object

[//]: # (.cssg-snippet-transfer-upload-file)

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
$local_path = "/Users/xxx/Desktop/exampleobject.txt"; //Save it to the user’s local path

try {
    $result = $cosClient->upload(
        $bucket = 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        $key = 'exampleobject', // Object key
        $body = fopen($local_path, 'rb')
    );
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 2. Uploading an object to ARCHIVE

[//]: # (.cssg-snippet-transfer-upload-file-archive)

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
$local_path = "/Users/xxx/Desktop/exampleobject.txt"; //Save it to the user’s local path

try {
    $result = $cosClient->upload(
        $bucket = 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        $key = 'exampleobject', // Object key
        $body = fopen($local_path, 'rb'),
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

#### Sample 3. Uploading an object with specified part size and metadata

[//]: # (.cssg-snippet-transfer-upload-file-with-meta)

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
$local_path = "/Users/xxx/Desktop/exampleobject.txt"; //Save it to the user’s local path

try {
    $result = $cosClient->upload(
        $bucket = 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        $key = 'exampleobject', // Object key
        $body = fopen($local_path, 'rb'),
        $options = array(
            'Metadata' => array(
                'string' => 'string',
            ),
            'PartSize' => 10 * 1024 * 1024
        )
    );
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 4. Object of the checkpoint restart
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
$local_path = "/Users/xxx/Desktop/exampleobject.txt"; //Save it to the user’s local path

try {
    // Generate a random string as the `body` to upload
    $characters = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ';
    $randomString = '';
    for ($i = 0; $i < 10; $i++) {
        $randomString .= $characters[rand(0, strlen($characters) - 1)];
    }
    //Part size
    $partSize = 1024 x 1024 + 1;
    // Initialize the multipart upload
    $rt = $this->cosClient->CreateMultipartUpload(array(
        'Bucket' => $this->bucket,
        'Key' => $this->key
    ));
    // Obtain the upload ID
    $uploadId = $rt['UploadId'];
    // Upload the parts
    $this->cosClient->uploadPart(array(
        'Bucket' => $this->bucket,
        'Key' => $this->key,
        'Body' => substr($body, 0, $partSize),
        'UploadId' => $uploadId,
        'PartNumber' => 1
    ));
    // Checkpoint restart
    $this->cosClient->resumeUpload(
        $bucket=$this->bucket,
        $this->key,
        $body,
        $uploadId,
        array('PartSize'=>$partSize)
    );
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

### Batch uploading files (uploading a local folder)

#### Feature description

This API is used to upload all files in a local folder to COS.

#### Sample request

[//]: # (.cssg-snippet-transfer-upload-folder)

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
            
function uploadfiles( $path, $cosClient ) {
    foreach ( scandir( $path ) as $afile ) {
        if ( $afile == '.' || $afile == '..' ) continue;
        if ( is_dir( $path.'/'.$afile ) ) {
            uploadfiles( $path.'/'.$afile, $cosClient );
        } else {
            $local_file_path = $path.'/'.$afile;
            $cos_file_path = $local_file_path;
            // Splice an upload path as needed
            try {
                $cosClient->upload(
                    $bucket = 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
                    $key = $cos_file_path,
                    $body = fopen( $cos_file_path, 'rb' )
                );
            } catch ( \Exception $e ) {
                echo( $e );
            }
        }
    }
}

$local_path = '/data/home/folder';
uploadfiles( $local_path, $cosClient );
```

## Simple Upload

### Uploading an object using simple upload

#### Feature description

This API (PUT Object) is used to upload an object to a specified bucket. You can upload objects up to 5 GB in size. Please use [Multipart Upload](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [Advanced APIs](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) to upload objects greater than 5 GB.

#### Method prototype

```php
public Guzzle\Service\Resource\Model putObject(array $args = array())
```

#### Sample request

#### Sample 1. Uploading a local file

[//]: # (.cssg-snippet-put-object)

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `secretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
$local_path = "/Users/xxx/Desktop/exampleobject.txt"; //Save it to the user’s local path

try { 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket 
        'Key' => 'exampleobject', 
        'Body' => fopen($local_path, 'rb'), 
    )); 
    // Request succeeded 
    print_r($result);
} catch (\Exception $e) { 
    // Request failed 
    echo($e); 
}
```

#### Sample 2. Uploading a file to ARCHIVE

[//]: # (.cssg-snippet-put-object-archive)

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
$local_path = "/Users/xxx/Desktop/exampleobject.txt"; //Save it to the user’s local path

try { 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket 
        'Key' => 'exampleobject', 
        'Body' => fopen($local_path, 'rb'), 
        'StorageClass' => 'Archive'
    )); 
    // Request succeeded 
    print_r($result); 
} catch (\Exception $e) { 
    // Request failed 
    echo($e); 
}
```

#### Sample 3. Uploading a file with a specified `Content-type`

[//]: # (.cssg-snippet-put-object-with-content-type)

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
$local_path = "/Users/xxx/Desktop/exampleobject.txt"; //Save it to the user’s local path

try { 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket 
        'Key' => 'exampleobject', 
        'Body' => fopen($local_path, 'rb'), 
        'ContentType' => 'text/xml'
    )); 
    // Request succeeded 
    print_r($result); 
} catch (\Exception $e) { 
    // Request failed 
    echo($e); 
}
```

#### Sample 4. Creating an empty virtual directory

[//]: # (.cssg-snippet-put-object-with-new-foler)

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
    $result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'folder/',
        'Body' => "",
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}

```

#### Sample 5. Uploading a ContentMD5-verified local file

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
$local_path = "/Users/xxx/Desktop/exampleobject.txt"; //Save it to the user’s local path

try { 
    $result = $cosClient->putObject(array( 
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket 
        'Key' => 'exampleobject', 
        'Body' => fopen($local_path, 'rb'), 
        'ContentMD5' => true, 
    )); 
    // Request succeeded 
    print_r($result);
} catch (\Exception $e) { 
    // Request failed 
    echo($e); 
}
```

#### Sample 6. Uploading an object (limiting single-connection bandwidth)
>? For more information about the speed limits on object uploads, see [Single-Connection Bandwidth Limit](https://intl.cloud.tencent.com/document/product/436/34072).

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
$local_path = "/Users/xxx/Desktop/exampleobject.txt"; //Save it to the user’s local path

try {
$result = $cosClient->putObject(array(
        'Bucket' => 'examplebucket-125000000', // Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'Body' => fopen($local_path, 'rb'),
        'TrafficLimit' => 8 * 1024 * 1024 // Limit the speed to 1 MB/s.
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
| Key | String | Object key is the unique identifier of an object in a bucket. For example, in the object’s access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the `Key` is `doc/pic.jpg`.  | No |
| ACL | String | ACL of the object, such as private or public-read | No |
| Body                 | Stream/String | Uploaded content                                                   | Yes       |
| CacheControl | String | Cache policy | No |
| ContentDisposition | String | File name | No |
| ContentEncoding | String | Encoding format | No |
| ContentLanguage | String | Language type | No |
| ContentLength | Int | Length of the content | No |
| ContentType | String | Content type | No |
| Expires | String | `Content-Expires` | No |
| Metadata             | Array       | User-defined file metadata                                       | No       |
| StorageClass | String | Storage class of the object, such as `STANDARD` (default), `STANDARD_IA`, and `ARCHIVE`. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | No |
| ContentMD5           | Boolean      | Whether to upload the MD5 checksum of the file for verification                                  | No       |
| ServerSideEncryption | String | Server-side encryption method | No |

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [ETag] => "698d51a19d8a121ce581499d7b701668"
            [VersionId] => MTg0NDUxODMyMTE2ODY0OTExOTk
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [Location] => http://examplebucket-1250000000.cos.ap-chengdu.myqcloud.com/123
            [CRC] => 16749565679157681890
        )

)

```

#### Response description

| Parameter Name | Type | Description | Parent Node | 
| --------- | ------ | -------------------------- | ------ |
| ETag | String | MD5 checksum of the uploaded file  | None |
| VersionId | String | Version ID of the file if versioning is enabled. | None  |
| CRC     | String | [CRC64 check](https://intl.cloud.tencent.com/document/product/436/34078) code for data verification | No |

### Appending parts

#### Feature description

This API (`APPEND Object`) is used to append object parts to a bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model appendObject(array $args = array());
```

#### Sample request

#### Sample 1. Appending input stream
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
    $result = $cosClient->appendObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'Position' => 0,
        'Body' => "hello,world",
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 2. Appending local file stream
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
$local_path = "/Users/xxx/Desktop/exampleobject.txt"; //Save it to the user’s local path

try {
    $result = $cosClient->appendObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'Position' => 0,
        'Body' => fopen($local_path, 'rb'),
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 3. Appending multiple data

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
$local_path = "/Users/xxx/Desktop/exampleobject.txt"; //Save it to the user’s local path

try {
    $result = $cosClient->appendObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'Position' => 0, // Position to append the object
        'Body' => fopen($local_path, 'rb'),// Read the file content
    ));
    
    $result = $cosClient->appendObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'Position' => (integer)$result['Position'], // Append to the position of the last append
        'Body' => "hello, world", 
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
| Key | String | Object key is the unique identifier of an object in a bucket. For example, in the object’s access domain name <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the `Key` is `doc/pic.jpg`. | Yes |
| Position | Integer | Starting point for the append operation. For the first append, the value of this parameter is 0. For subsequent appends, the value is the `content-length` of the current object. | Yes |
| Body | File/String | Content of the uploaded part, which can be file stream or byte stream     | Yes |

#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [ETag] => "9a74ded332531da4c295934ba5a9cf8b"
    [Position] => 4
    [RequestId] => NjExNWU4NTlfZDIyZjJjMGJfM2Q2ZV8xMzJjZThhZg==
    [Key] => exampleobject
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject
)
```

#### Response description

| Parameter Name | Type | Description | Parent Node | 
| -------------------- | ------ | -------------------------------------------------- | ------ |
| ETag | String | MD5 checksum of the file | None |
| Position              | Integer | Starting point of the append operation | None  |

### Querying object metadata

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
| Key | String | Object key is the unique identifier of an object in a bucket. For example, in the object’s access domain name <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the `Key` is `doc/pic.jpg`. | Yes |
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
| StorageClass | String | Storage class of the object, such as `STANDARD`, `STANDARD_IA`, and `ARCHIVE`. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | None |
| ServerSideEncryption | String | Server-side encryption method | None |
| ETag | String | MD5 checksum of the file | None |
| Restore | String | Restoration information of the archived file | None |
| CRC     | String | [CRC64 check](https://intl.cloud.tencent.com/document/product/436/34078) code for data verification | No |


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

#### Sample 3. Changing the storage class to `ARCHIVE`

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
| CopySource | String | Path of the source object, which contains `APPID`, `Bucket`, `Key`, and `Region`, <br>for example, `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` | Yes |
| MetadataDirective | String | Valid values: `Copy`: ignores the configured metadata and copies the file directly; `Replaced`: modifies the metadata according to the configured metadata. If the destination path is identical to the source path, this parameter must be set to `Replaced`. | No |


## Multipart upload

Multipart operations include:

- Uploading an object in parts: initializing a multipart upload, uploading parts, and completing a multipart upload
- Resuming a multipart upload: querying uploaded parts, uploading remaining parts, and completing a multipart upload
- Deleting uploaded parts

### Querying multipart uploads

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
| Delimiter | String | Separator, left empty by default. For example, you can set it to `/` to indicate folders. | No |
| EncodingType | String | Encoding method of the returned value. The value is not encoded by default. Valid value: `url`  | No |
| KeyMarker | String | The key of the object after which the returned part list begins | No |
| UploadIdMarker | String | The upload ID of the object after which the returned part list begins                            | No |
| Prefix | String | Key prefix to query parts by, left empty by default   | No |
| MaxUploads  | Int | Maximum number of returned parts, which is `1000` (the maximum value allowed) by default | No |

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Bucket] => examplebucket-1250000000
            [EncodingType] => 
            [KeyMarker] => 
            [UploadIdMarker] => 
            [MaxUploads] => 1000
            [Prefix] => 
            [IsTruncated] => 
            [Uploads] => Array
                (
                    [0] => Array
                        (
                            [Key] => exampleobject
                            [UploadId] => 1551693693b1e6d0e00eec30c534059865ec89c9393028b60bfaf167e9420524b25eeb2940
                            [Initiator] => Array
                                (
                                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                                    [DisplayName] => 100000000001
                                )

                            [Owner] => Array
                                (
                                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                                    [DisplayName] => 100000000001
                                )

                            [StorageClass] => STANDARD
                            [Initiated] => 2019-03-04T10:01:33.000Z
                        )

                    [1] => Array
                        (
                            [Key] => exampleobject
                            [UploadId] => 155374001100563fe0e9d37964d53077e54e9d392bce78f630359cd3288e62acee2b719534
                            [Initiator] => Array
                                (
                                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                                    [DisplayName] => 100000000001
                                )

                            [Owner] => Array
                                (
                                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                                    [DisplayName] => 100000000001
                                )

                            [StorageClass] => STANDARD
                            [Initiated] => 2019-03-28T02:26:51.000Z
                        )

                )

            [RequestId] => NWNhNDJmNzBfZWFhZDM1MGFfMjYyM2FfMWIyNzhh
        )

)
```

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



### Initializing a multipart upload

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
| Key | String | Object key is the unique identifier of an object in a bucket. For example, in the object’s access domain name <br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is `doc/pic.jpg`. | Yes |
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

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Bucket] => examplebucket-1250000000
            [Key] => exampleobject
            [UploadId] => 1554277569b3e83df05c730104c325eb7b56000449fb7d51300b0728aacde02a6ea7f6c033
            [RequestId] => NWNhNDY0YzFfMmZiNTM1MGFfNTM2YV8xYjliMTg=
        )

)
```

#### Response description

| Parameter Name | Type | Description | Parent Node | 
| -------- | ------ | ---------------------------------- | ------ |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Key  | String | Object key | None |
| UploadId  | String | ID of the multipart upload | None |




### Uploading parts

This API (`Upload Part`) is used to upload an object in parts.

#### Method prototype

```php
public Guzzle\Service\Resource\Model uploadPart(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-upload-part)

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
    $result = $cosClient->uploadPart(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject', 
        'Body' => 'string',
        'UploadId' => 'exampleUploadId', // `UploadId` is the ID of the multipart upload, which you can get in the response returned after multipart upload initialization 
        'PartNumber' => 1, // `PartNumber` is the sequential number of a part, which COS uses to reassemble parts
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
| ------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key | Yes |
| UploadId | String | ID of the multipart upload, which can be found in the response returned after the initialization of the multipart upload | Yes |
| Body | File/String | Uploaded content | Yes |
| PartNumber | Int | Sequential number of a part, which COS uses to reassemble parts | Yes |
| ContentLength | Int | Length of the content | No |
| ContentMD5           | Boolean      | Whether to upload the MD5 checksum of the file for verification                                  | No       |

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [ETag] => "96e79218965eb72c92a549dd5a330112"
            [RequestId] => NWNhNDdjYWFfNjNhYjM1MGFfMjk2NF8xY2ViMWM=
            [CRC] => 16749565679157681890
        )

)
```

#### Response description

| Parameter Name | Type | Description | Parent Node | 
| -------- | ------ | ------------- | ------ |
| ETag | String | MD5 checksum of the part | None |
| CRC     | String | [CRC64 check](https://intl.cloud.tencent.com/document/product/436/34078) code for data verification | No |

### Querying uploaded parts

#### Feature description

This API (`List Parts`) is used to query the uploaded parts of a multipart upload.

#### Method prototype

```php
public Guzzle\Service\Resource\Model listParts(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-list-parts)

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
    $result = $cosClient->listParts(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'UploadId' => 'exampleUploadId',
        'PartNumberMarker' => 1,
        'MaxParts' => 1000,
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
| ---------------- | ------ | --------------------------------------- | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key | Yes |
| UploadId  | String | ID of the multipart upload | Yes |
| PartNumberMarker | Int | The number of the part after which the returned list begins | No |
| MaxParts | Int | Maximum number of returned parts, which is `1000` (the maximum value allowed) by default | No |

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Bucket] => examplebucket-1250000000
            [Key] => exampleobject
            [UploadId] => 1554279643cf19d71bb5fb0d29613e5541131f3a96387d9e168cd939c23a3d608c9eb94707
            [Owner] => Array
                (
                    [ID] => 1250000000
                    [DisplayName] => 1250000000
                )
            [PartNumberMarker] => 1
            [Initiator] => Array
                (
                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                    [DisplayName] => 100000000001
                )
            [StorageClass] => Standard
            [MaxParts] => 1000
            [IsTruncated] => 
            [Parts] => Array
                (
                    [0] => Array
                        (
                            [PartNumber] => 2
                            [LastModified] => 2019-04-03T08:21:28.000Z
                            [ETag] => "b948e77469189ac94b98e09755a6dba9"
                            [Size] => 1048576
                        )
                    [1] => Array
                        (
                            [PartNumber] => 3
                            [LastModified] => 2019-04-03T08:21:22.000Z
                            [ETag] => "9e5060e2994ec8463bfbebd442fdff16"
                            [Size] => 1048576
                        )                       
                )
            [RequestId] => NWNhNDZkNTJfOGNiMjM1MGFfMTRlYl8xYmJiOTU=
        )

)
```

#### Response description

| Parameter Name | Type | Description | Parent Node | 
| ---------------- | ------ | --------------------------------------- | ------ |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Key | String | Object key | None |
| UploadId  | String | ID of the multipart upload | None |
| IsTruncated | Int    | Whether the returned objects are truncated | None |
| PartNumberMarker | Int | The number of the part after which the returned list begins | None |
| MaxParts | Int | Maximum number of returned parts, which is `1000` (the maximum value allowed) by default | None |
| Initiator | String | Initiator of the multipart upload | None  |
| Parts | Array  | List of returned parts | None |
| Part | Array  | Attributes of the returned parts                          | Parts |
| PartNumber | Int | Part number  | Part |
| LastModified | String | Time when the part was last modified | Part |
| ETag | String | MD5 checksum of the part | Part |
| Size | String | Size of the part | Part |



### Completing a multipart upload

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

### Aborting a multipart upload

#### Feature description

This API (`Abort Multipart Upload`) is used to abort a multipart upload and delete the uploaded parts.

#### Method prototype

```php
public Guzzle\Service\Resource\Model abortMultipartUpload(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-abort-multi-upload)

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
    $result = $cosClient->abortMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject', 
        'UploadId' => 'exampleUploadId',
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
| -------- | ------ | ---------------------------------- | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key      | String | Object key                             | Yes       |
| UploadId  | String | ID of the multipart upload | Yes |




