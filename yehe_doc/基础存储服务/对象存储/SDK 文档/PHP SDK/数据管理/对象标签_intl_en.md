
## Overview

This document provides an overview of APIs and SDK code samples for object tagging.

| API | Operation | Description |
| :----------------------------------------------------------- | :----------- | :--------------------------- |
| [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | Tagging an object | Tags an uploaded object. |
| [GET Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | Querying object tags | Queries all tags of an object. |
| [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | Deleting object tags | Deletes all tags of an object. |

## Tagging an Object

#### Feature description

This API (`PUT Object tagging`) is used to tag an object.


#### Method prototype

```
public Guzzle\Service\Resource\Model PutObjectTagging(array $args = array());
```

#### Sample request


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
    $result = $cosClient->putObjectTagging(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key'    => 'exampleobject',
        'TagSet' => array(
            array('Key'=>'key1',
                  'Value'=>'value1',
            ),  
            array('Key'=>'key2',
                  'Value'=>'value2',
            ),  
        ),  
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter description

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Bucket | Bucket of the object to tag in the format of `BucketName-APPID`. For more information, see [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| Key | Key of the object to tag. Object key is the unique identifier of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| TagSet    | Tags to add to the object                                                     | Array |

Description of the `TagSet` member:

| Parameter | Description | Type |
| ----- | ---- | ---- |
| Key | Tag key | String |
| Value | Tag value | String |

## Querying Object Tags

#### Feature description

This API (`GET Object tagging`) is used to query the existing tags of an object.

#### Method prototype

```
public Guzzle\Service\Resource\Model GetObjectTagging(array $args = array());
```

#### Sample request

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
    $result = $cosClient->getObjectTagging(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key'    => 'exampleobject',
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Bucket | Bucket of the object to query in the format of `BucketName-APPID`. For more information, see [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| Key | Key of the object to query. Object key is the unique identifier of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |



#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [TagSet] => Array
        (
            [0] => Array
                (
                    [Key] => key1
                    [Value] => value1
                )

            [1] => Array
                (
                    [Key] => key2
                    [Value] => value2
                )

        )
    [RequestId] => NWRmMWVkMjFfMjJiMjU4NjRfNWQ3X2EwMWVj****
)
```

#### Response description

| Member Variable | Description | Type |
| -------- | -------- | ------ |
| Key      | Key of the tag                                                     | String |
| Value    | Value of the tag                                                     | String |

## Deleting Object Tags

#### Feature description

This API (`DELETE Object tagging`) is used to delete the existing tags of an object.

#### Method prototype

```
public Guzzle\Service\Resource\Model DeleteObjectTagging(array $args = array());
```

#### Sample request

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
    $result = $cosClient->deleteObjectTagging(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Key'    => 'exampleobject',
    );
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Bucket | Bucket of the object to delete in the format of `BucketName-APPID`. For more information, see [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| Key | Key of the object to delete Object key is the unique identifier of an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |


