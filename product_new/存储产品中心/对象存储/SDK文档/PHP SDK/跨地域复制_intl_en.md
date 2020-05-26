## Overview

This document provides an overview of APIs and SDK code samples related to cross-region replication.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets the cross-region replication rule of a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rule of a bucket |

## Setting Cross-Region Replication

#### Feature description

This API (PUT Bucket replication) is used to set the cross-region replication rule for a specified bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model putBucketReplication(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-replication)

```php
try {
    $result = $cosClient->putBucketReplication(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
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
    // Request succeeded    print_r($result);
} catch (\Exception $e) {    // Request failed
    echo "$e\n";
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| ------------ | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Source bucket in the format of `BucketName-APPID` | Yes |
| Role         | String | Initiator ID in the format of `qcs::cam::uin/:uin/`                  | Yes |
| Rules | Array | Sets the corresponding rule, including ID, Status, Prefix, and Destination | Yes |
| ID | String | Sets the rule ID | Yes  |
| Status | String | Sets whether a rule is enabled. Valid values: Enabled, Disabled | Yes |
| Prefix | String | Sets the prefix matching rule of the rule. If this parameter empty, the rule is applicable to all objects in the bucket | Yes |
| Destination | String | Describes the destination resource, including Bucket and StorageClass | Yes |
| Bucket       | String | Bucket for which to set cross-region replication in the format of `qcs::cos:[region]::[BucketName-APPID]` | Yes |
| StorageClass | String | Sets the storage class of the destination file. Valid values: STANDARD, STANDARD_IA | No |



## Querying Cross-Region Replication

#### Feature description

This API (GET Bucket replication) is used to query the cross-region replication rule of a specified bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model getBucketReplication(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-replication)

```php
try {
    $result = $cosClient->getBucketReplication(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| -------- | ------ | ---------------------------------------------- | -------- |
| Bucket | String | Bucket for which to query cross-region replication in the format of `BucketName-APPID` | Yes |

#### Sample return result

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

#### Returned result description

| Parameter Name | Type | Description | Parent Node |
| ------------ | ------ | ------------------------------------------------------------ | ----------- |
| Role         | String | Initiator ID in the format of `qcs::cam::uin/:uin/`                  | None |
| Rules | Array | Sets the corresponding rule, including ID, Status, Prefix, and Destination | None |
| Rule | Array | Sets the corresponding rule, including ID, Status, Prefix, and Destination | Rules |
| ID | String | Sets the rule ID | Rule |
| Status | String | Sets whether a rule is enabled. Valid values: Enabled, Disabled | Rule |
| Prefix | String | Sets the prefix matching rule of the rule. If this parameter empty, the rule is applicable to all objects in the bucket | Rule |
| Destination | String | Describes the destination resource, including Bucket and StorageClass | Rule |
| Bucket       | String | Bucket for which to set cross-region replication in the format of `qcs::cos:[region]::[BucketName-APPID]` | Destination |
| StorageClass | String | Sets the storage class of the destination file. Valid values: STANDARD, STANDARD_IA | Destination |

## Deleting Cross-Region Replication

#### Feature description

This API (DELETE Bucket replication) is used to delete the cross-region replication rule of a specified bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model deleteBucketReplication(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-replication)

```php
try {
    $result = $cosClient->deleteBucketReplication(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| -------- | ------ | ---------------------------------------------- | -------- |
| Bucket | String | Bucket for which to delete cross-region replication in the format of `BucketName-APPID` | Yes |
