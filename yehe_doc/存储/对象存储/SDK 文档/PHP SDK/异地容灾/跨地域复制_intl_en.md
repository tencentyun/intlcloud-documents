## Overview

This document provides an overview of APIs and SDK code samples for cross-region replication.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting a cross-region replication rule | Sets a cross-region replication rule for a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying a cross-region replication rule | Queries the cross-region replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting a cross-region replication rule | Deletes the cross-region replication rule from a bucket |

## Setting Cross-region Replication Rules

#### Feature description

This API (`PUT Bucket replication`) is used to set the cross-bucket replication rule for a bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model putBucketReplication(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-replication)

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
    $result = $cosClient->putBucketReplication(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Role' => 'qcs::cam::uin/100000000001:uin/100000000001',
        'Rules'=>array(
            array(
                'Status' => 'Enabled',
                'ID' => 'string',
                'Prefix' => 'string',
                'Destination' => array(                    
                    'Bucket' => 'qcs::cos:ap-beijing::destinationbucket-1250000000',
                    'StorageClass' => 'standard',                
                ),  
                // ...repeated            ),  
        ),      
    ))); 
    // Request succeeded   print_r($result);
} catch (\Exception $e) {    // Request failed
    echo "$e\n";
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| ------------ | ------ | ------------------------------------------------------------ | -------- |
| Bucket       | String | Source bucket in the format of `BucketName-APPID` | Yes |
| Role         | String | Requester identifier in the format of `qcs::cam::uin/:uin/`                  | Yes       |
| Rule | Array | Sets rule information, including its `ID`, `Status`, `Prefix`, and `Destination` | Yes |
| ID           | String | Sets rule ID | Yes  |
| Status | String | Sets whether `Rule` is enabled. Valid values: `Enabled`, `Disabled` | Yes |
| Prefix | String |  Prefix used to filter objects that are subject to the rule. If it is left empty, it means that the rule applies to all objects in the bucket | Yes |
| Destination | String |  Describes information on object copies, including `Bucket` and `StorageClass` | Yes |
| Bucket | String | Sets the destination bucket of the cross-region replication. Format: `qcs::cos:[region]::[BucketName-APPID]` | Yes |
| StorageClass | String | Sets the storage class of the object copies. Valid values: `STANDARD`; `STANDARD_IA` | No |



## Querying Cross-region Replication Rules

#### Feature description

This API (`GET Bucket replication`) is used to query the cross-bucket replication rule of a bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model getBucketReplication(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-replication)

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
    $result = $cosClient->getBucketReplication(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter description

| Parameter | Type | Description | Required |
| -------- | ------ | ---------------------------------------------- | -------- |
| Bucket   | String | Bucket for which cross-region replication is queried in the format of `BucketName-APPID`  |  Yes   |

#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [data:protected] => Array
        (
            [Role] => qcs::cam::uin/100000000001:uin/100000000001
            [Rules] => Array
                (
                    [0] => Array
                        (
                            [ID] => string
                            [Status] => Enabled
                            [Prefix] => string
                            [Destination] => Array
                                (
                                    [Bucket] => qcs::cos:ap-guangzhou::examplebucket2-1250000000
                                    [StorageClass] => 
                                )
                        )
                )
            [RequestId] => NWQwOGI5MGVfNWFiMjU4NjRfNDUzY19mNzRh****
        )
)
```

#### Response description

| Parameter | Type | Description | Parent Node | 
| ------------ | ------ | ------------------------------------------------------------ | ----------- |
| Role         | String | Requester identifier in the format of `qcs::cam::uin/:uin/`                  | No          |
| Rules | Array | Sets rule information, including its `ID`, `Status`, `Prefix`, and `Destination`  | No |
| Rule | Array | Sets rule information, including its `ID`, `Status`, `Prefix`, and `Destination` | Rules |
| ID             | String |  Sets rule ID | Rule |
| Status | String | Sets whether `Rule` is enabled. Valid values: `Enabled`; `Disabled` | Rule |
| Prefix | String |  Prefix used to filter objects that are subject to the rule. If it is left empty, it means that the rule applies to all objects in the bucket | Rule |
| Destination | String |  Describes information on object copies, including `Bucket` and `StorageClass` | Rule |
| Bucket | String | Sets the destination bucket of the cross-region replication. Format: `qcs::cos:[region]::[BucketName-APPID]` | Destination |
| StorageClass | String | Sets the storage class of the object copies. Valid values: `STANDARD`, `STANDARD_IA` | Destination |

## Deleting Cross-region Replication Rules

#### Feature description

This API (`DELETE Bucket replication`) is used to delete the cross-bucket replication rule from a bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model deleteBucketReplication(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-replication)

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
    $result = $cosClient->deleteBucketReplication(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter description

| Parameter | Type | Description | Required |
| -------- | ------ | ---------------------------------------------- | -------- |
| Bucket   | String |  Bucket for which cross-region replication is deleted in the format of `BucketName-APPID`  |  Yes   |
