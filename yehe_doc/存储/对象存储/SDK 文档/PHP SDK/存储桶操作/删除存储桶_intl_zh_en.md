## Overview

This document provides an overview of APIs and SDK code samples related to how to delete a bucket.


| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket from a specified account |


## Deleting a Bucket

#### Description

This API is used to delete a specified bucket.

>! Before deleting a bucket, please make sure that all the data and incomplete multipart uploads in the bucket have been deleted; otherwise, the bucket cannot be deleted.
>
#### Sample code

#### Method prototype

```php
public Guzzle\Service\Resource\Model deleteBucket(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket)

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
    $result = $cosClient->deleteBucket(array(
        'Bucket' => 'examplebucket-125000000' // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Parent Node | Description | Type | 
| -------- | ------ | ---------------------------------- | ------ |
| Bucket | None | Bucket name in the format of `BucketName-APPID` | String |


## Deleting All Buckets

#### Description

This API (`DELETE Buckets`) is used to delete all buckets.

#### Sample code

#### Method prototype

```php
public Guzzle\Service\Resource\Model deleteBuckets(array $args = array());
```

#### Sample request

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
    //List all buckets
    $buckets = $cosClient->listBuckets();

    //If buckets are listed, perform the deletion logic: delete objects from the buckets, delete ongoing upload tasks (if any), and then delete the buckets.
    //You can add the `exclude` logic (for example, create an array of buckets to be retained) in foreach to retain buckets as required.
    if (!empty($buckets['Buckets'][0])) {
        foreach ($buckets['Buckets'][0]['Bucket'] as $key => $value) {
            $result = $cosClient->listObjects(array('Bucket' => $value['Name']));
            if (isset($result['Contents'])) {
                foreach ($result['Contents'] as $content) {
                    $cosClient->deleteObject(array('Bucket' => $value['Name'], 'Key' => $content['Key']));
                }
            }
            while(True){
                $result = $cosClient->ListMultipartUploads(
                    array('Bucket' => $value['Name']));
                if ($result['Uploads'] == array()) {
                    break;
                }
                foreach ($result['Uploads'] as $upload) {
                    try {
                        $cosClient->AbortMultipartUpload(
                            array('Bucket' => $value['Name'],
                                'Key' => $upload['Key'],
                                'UploadId' => $upload['UploadId']));
                    } catch (\Exception $e) {
                        print_r($e);
                    }
                }
            }
            $cosClient->deleteBucket(array('Bucket' => $value['Name']));
        }
    }
    print_r('DELETE ALL BUCKETS SUCCEED!');
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Parent Node | Description | Type | 
| -------- | ------ | ---------------------------------- | ------ |
| Bucket | None | Bucket name in the format of `BucketName-APPID` | String |
