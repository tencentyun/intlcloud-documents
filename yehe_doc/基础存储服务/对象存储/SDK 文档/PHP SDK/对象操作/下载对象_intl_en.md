## Overview

This document provides an overview of APIs and SDK code samples for downloading an object.

| API | Operation | Description |
| ------------------------------------------------------------ | -------- | ------------------ |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system. |

## Advanced APIs (Recommended)

### Downloading an object (checkpoint restart)

#### Feature description

This API is used to download an object. It calls the `GET Object` API to download a small file in whole and a large file by byte range. For the parameters required, see those of the `GET Object` API.

#### Method prototype

```php
public Qcloud\Cos\Client download(string $bucket, string $key, string $saveAs, array $options = array());
```

| Parameter | Type | Description | Required |
| -------- | ------ | ---------------------------------- | -------- |
| bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| key      | String | Object key                             | Yes       |
| saveAs     | String | Local path to save the file   | Yes       |
| options     | Array | Additional configuration items            | No       |



| options Parameter | Type   | Description | Required |
| -------- | ------ | ---------------------------------- | -------- |
| Progress         | Function      | Progress callback. `$totalSize` indicates the total size, and `$downloadedSize` indicates the downloaded size. | No       |
| PartSize         | Int      | Minimum part size. Default value: 5 MB | No       |
| Concurrency         | Int      | Concurrency. Default value: 10 | No       |
| ResumableDownload         | Bool      | Whether to enable checkpoint restart. Default value: `False` | No       |
| ResumableTaskFile         | String       | Checkpoint file path. Default value: `&lt;saveAs.cosresumabletask>` | No       |


#### Sample request

[//]: # (.cssg-snippet-download-object)

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

$printbar = function($totalSize, $downloadedSize) {
    printf("downloaded [%d/%d]\n", $downloadedSize, $totalSize);
};

try {
    $result = $cosClient->download(
        $bucket = 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        $key = 'exampleobject',
        $saveAs = $local_path,
        $options= array(
            'Progress' => $printbar, // Specify the progress
            'PartSize' => 10 * 1024 * 1024, //Part size
            'Concurrency' => 5, //Number of concurrent parts
            'ResumableDownload' => true, //Whether to enable checkpoint restart. It’s disabled by default.
            'ResumableTaskFile' => 'tmp.cosresumabletask' //Checkpoint file path. Default value: `<localpath>.cosresumabletask`
        )
    );
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

### Batch downloading files (downloading a COS directory)

#### Feature description

This API is used to download a COS directory and the files in it to the local disk.

#### Sample request

[//]: # (.cssg-snippet-download-folder)

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

$cos_path = 'cos/folder';
$nextMarker = '';
$isTruncated = true;

while ($isTruncated) {
    try {
        $result = $cosClient->listObjects(array(
                'Bucket' => 'examplebucket-125000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
                'Delimiter' => '/', //Delimiter: "/". Set the delimiter to "/" to list objects in the current directory. To list all objects, leave this parameter empty.
                'EncodingType' => 'url',// Encoding format, which indicates the `encoding-type` in requests
                'Marker' => 'prefix/picture.jpg',//Identifier of the initial object key
                'Prefix' => 'prfix/', //Set a prefix to indicate that the key of the listed object starts with the prefix.
                'MaxKeys' => 1000, // Set the maximum number of traversed objects (up to 1000 per `listObjects` request).
        ));
    } catch (\Exception $e) {
        echo($e);
    }
    $isTruncated = $result['IsTruncated'];
    $nextMarker = $result['NextMarker'];
    foreach ( $result['Contents'] as $content ) {
        $cos_file_path = $content['Key'];
        $local_file_path = $content['Key'];
        // Splice a download path as needed
        try {
            $result = $cosClient->download(
                $bucket = 'examplebucket-1250000000', //Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
                $key = $cos_file_path,
                $saveAs = $local_file_path
            );
            echo ($cos_file_path . "\n");
        } catch ( \Exception $e ) {
            echo($e);
        }
    }
}
```

## Simple Download

### Downloading an object

#### Feature description

This API (`GET Object`) is used to download an object.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getObject(array $args = array());
```

#### Sample request

#### Sample 1. Downloading a file

[//]: # (.cssg-snippet-get-object)

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual `region`, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
$local_path = "/Users/xxx/Desktop/exampleobject.txt"; //Save it to the user’s local path

try {
    $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'SaveAs' => $local_path,
    )); 
    // Request succeeded
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 2. Getting file content within a certain byte range

[//]: # (.cssg-snippet-get-object-range)

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
    $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'Range' => 'bytes=0-10'
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 3. Downloading a specified version of a file

[//]: # (.cssg-snippet-get-object-with-versionId)

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
    $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'VersionId' => 'exampleVersionId'
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample 4. Downloading an object (limiting single-connection bandwidth)
>?For more information about the speed limits on object downloads, see [Single-Connection Bandwidth Limit](https://intl.cloud.tencent.com/document/product/436/34072).

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
   $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-125000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'SaveAs' => '/data/exampleobject',
        'TrafficLimit' => 8 * 1024 * 1024 // Limit the speed to 1 MB/s
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```
