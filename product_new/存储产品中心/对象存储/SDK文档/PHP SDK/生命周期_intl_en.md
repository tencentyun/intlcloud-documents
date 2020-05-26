This document provides an overview of APIs and SDK code samples related to lifecycle.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets the lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

## Setting Lifecycle

#### Feature description

This API (PUT Bucket lifecycle) is used to set the lifecycle configuration information of a specified bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model putBucketLifecycle(array $args = array());
```

#### Sample request

#### Sample 1. Deleting all objects 1 day after generation

[//]: # (.cssg-snippet-put-bucket-lifecycle)

```php
try {
    $result = $cosClient->putBucketLifecycle(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Rules' => array(
            array(
                'Expiration' => array(
                    'Days' => 1,
                ),
                'ID' => 'rule01',
                'Filter' => array(
                    'Prefix' => ''
                ),
                'Status' => 'Enabled',
            ),
        )
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Sample 2. Transitioning objects with a specific prefix to archive storage 1 day after generation

[//]: # (.cssg-snippet-put-bucket-lifecycle-archive)

```php
try {
    $result = $cosClient->putBucketLifecycle(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Rules' => array(
            array(
                'ID' => 'rule01',
                'Filter' => array(
                    'Prefix' => 'prefix01/'
                ),  
                'Status' => 'Enabled',
                'Transitions' => array(
                    array(
                        'Days' => 1,
                        'StorageClass' => 'Archive'
                    ),
                ),  
            ),
        )
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
| --------------------------- | ------------ | ------------------------------------------------------------ | ---- |
| Bucket | String | Bucket for which to set lifecycle in the format of `BucketName-APPID` | Yes |
| Rules        | Array        | Lifecycle information list                                           | Yes                      |
| Rule         | Array        | Lifecycle information                                                 | Yes                   |
| Expiration | Array | Sets the object expiration rule (either a number of days (Days) or a date (Date) can be specified) | No |
| Transition | Array | Sets the object transition rule | No |
| NoncurrentVersionExpiration | Array        | Sets the expiration rule for historical objects                                    | No   |
| NoncurrentVersionTransition | Array        | Set the transition rule for historical objects                            | No   |
| Filter | Array |  Describes the set of objects subject to the rule | Yes |
| Prefix | String | Prefix of the filtered objects | Yes |
| Status | String | Sets whether a rule is enabled. Valid values: Enabled, Disabled | Yes |
| ID             | String | Configures the rule ID                                                | Yes  |
| Days | Int | Sets the number of effective days | No |
| Date | Int / String | Sets the effective date | No |
| NoncurrentDays              | Int          | Sets effective days of noncurrent objects                                   | No   |
| StorageClass | String | Transitioned file storage class. Valid values: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD | Yes |

## Querying Lifecycle

#### Feature description

This API (GET Bucket lifecycle) is used to query the lifecycle management configuration for a bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getBucketLifecycle(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-lifecycle)

```php
try {
    $result = $cosClient->getBucketLifecycle(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
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
| -------- | ------ | -------------------------------------------- | -------- |
| Bucket | String | Bucket for which to query lifecycle configuration in the format of `BucketName-APPID` | Yes |

#### Sample return result

```php
Guzzle\Service\Resource\Model Object
(
    [data:protected] => Array
        (
            [Rules] => Array
                (
                    [0] => Array
                        (
                            [ID] => id1
                            [Filter] => Array
                                (
                                    [Prefix] => documents/
                                )
                            [Status] => Enabled
                            [Transition] => Array
                                (
                                    [Days] => 200
                                    [StorageClass] => Standard_IA
                                )
                            [Expiration] => Array
                                (
                                    [Days] => 1000
                                )
                        )
                )
            [RequestId] => NWE3YzhlZjNfY2FhMzNiMGFfNDVkNF8yZDIxODE=
        )
)
```

#### Returned result description

| Parameter name | Type | Description | Parent Node |
| ------------ | ------------ | ------------------------------------------------------------ | ----------------------- |
| Rules        | Array        | Lifecycle information list                                           | None                       |
| Rule         | Array        | Lifecycle information                                                 | Rules                   |
| Expiration | Array | Sets the object expiration rule (either a number of days (Days) or a date (Date) can be specified) | Rule |
| Transition | Array | Sets the object transition rule | Rule |
| Filter | Array |  Describes the set of objects subject to the rule | Rule |
| Prefix | String | Prefix of the filtered objects | Filter |
| Status | String | Sets whether a rule is enabled. Valid values: Enabled, Disabled | Rule |
| ID             | String | Configures the rule ID                                                | Rule |
| Days | Int | Sets the number of effective days | Expiration / Transition |
| Date | Int / String | Sets the effective date | Expiration |
| StorageClass | String | Transitioned file storage class. Valid values: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD | Transition |



## Deleting Lifecycle

#### Feature description

This API (DELETE Bucket lifecycle) is used to delete the lifecycle management configuration of a bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model deleteBucketLifecycle(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-lifecycle)

```php
try {
    $result = $cosClient->deleteBucketLifecycle(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
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
| -------- | ------ | -------------------------------------------------- | -------- |
| Bucket | String | Bucket for which to delete lifecycle configuration in the format of `BucketName-APPID` | Yes |
