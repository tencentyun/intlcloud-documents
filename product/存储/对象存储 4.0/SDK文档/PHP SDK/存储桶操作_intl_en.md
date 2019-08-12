## Overview

This document provides an overview of APIs related to basic bucket operations and access control list (ACL) and corresponding SDK sample code.

**Basic operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets under the specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under the specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permission | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under the specified account |

**ACL**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | --------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL for the specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Gets the ACL of the specified bucket |

## Basic Operations

### Querying Bucket List

#### Feature Description

This API (GET Service) is used to query the list of all buckets under the specified account.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model listBucket(array $args = array())
```

#### Sample Request

```php
// Query bucket list
try {
    $result = $cosClient->listBuckets();
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```


#### Return Result Example
```php
Array
(
    [data:protected] => Array
        (
            [Owner] => Array
                (
                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                    [DisplayName] => 100000000001
                )

            [Buckets] => Array
                (
                    [0] => Array
                        (
                            [Name] => examplebucket-1250000000
                            [Location] => ap-beijing
                            [CreationDate] => 2016-07-29T03:09:54Z
                        )

                    [1] => Array
                        (
                            [Name] => examplebucket2-1250000000
                            [Location] => ap-beijing
                            [CreationDate] => 2017-08-02T04:00:24Z
                        )

                )

            [RequestId] => NWE3YzgxZmFfYWZhYzM1MGFfMzc3MF9iOGY5OQ==
        )

)
```
#### Return Result Descriptions

| Parameter name | Type | Description | Parent Node |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Owner | Array | Bucket owner information                         | None |
| ID | String | Bucket owner ID                         | Owner |
| DisplayName | String | Bucket owner name         | Owner |
| Buckets | Array | Bucket list                     | None |
| Bucket | Array | Bucket information                     | Buckets |
| Name | String | Bucket name                         | Bucket |
| Location | String | Bucket region name               | Bucket  |
| CreationDate | String | Bucket creation time             | Bucket  |


### Creating a Bucket

#### Feature Description

This API (PUT Bucket) is used to create a bucket under the specified account.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model createBucket(array $args = array());
```

#### Sample Request

```php
try {
    $result = $cosClient->createBucket(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter Descriptions

| Parameter name | Type | Description | Parent Node |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID                         | None |


### Checking a Bucket and Its Permission

#### Feature Description

This API (HEAD Bucket) is used to confirm whether a bucket exists and you have permission to access it.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model headBucket(array $args = array());
```

#### Sample Request

```php
try {
    $result = $cosClient->headBucket(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter Descriptions

| Parameter name | Type | Description | Parent Node |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID                         | None |


### Deleting a Bucket

#### Feature Description

This API is used to delete an empty bucket under the specified account.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model deleteBucket(array $args = array());
```

#### Sample Request

```php
try {
    $result = $cosClient->deleteBucket(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter Descriptions

| Parameter name | Type | Description | Parent Node |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID                         | None |

## ACL

### Setting Bucket ACL

#### Feature Description

This API is used to set the access control list (ACL) for the specified bucket.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model putBucketAcl(array $args = array());
```

#### Sample Request

```php
try {
    $result = $cosClient->putBucketAcl(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
        'ACL' => 'private',
        'Grants' => array(
            array(
                'Grantee' => array(
                    'DisplayName' => 'qcs::cam::uin/100000000001:uin/100000000001',
                    'ID' => 'qcs::cam::uin/100000000001:uin/100000000001',
                    'Type' => 'CanonicalUser',
                ),  
                'Permission' => 'FULL_CONTROL',
            ),  
            // ... repeated
        ),  
        'Owner' => array(
            'DisplayName' => 'qcs::cam::uin/100000000001:uin/100000000001',
            'ID' => 'qcs::cam::uin/100000000001:uin/100000000001',
        )));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter Descriptions

| Parameter name | Type | Description | Parent Node |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID                         | None |
| Grants | Array | ACL permission list                         | None |
| Grant | Array | ACL permission information         | Grants |
| Grantee | Array | ACL permission information                     | Grant |
| Type | String | Owner permission type        | Grantee  |
| Permission | String | Permission type. Value range: FULL_CONTROL, WRITE, READ | Grant |
| ACL | String | Overall permission type. Value range: private, public-read, public-read-write | None |
| Owner | String | Bucket owner information | None |
| DisplayName | String | Permission owner name      | Grantee/Owner |
| ID | String | Permission owner ID              | Grantee/Owner |



### Querying Bucket ACL

#### Feature Description

This API is used to get the access control list (ACL) for the specified bucket.

#### Method Prototype

```php
public Guzzle\Service\Resource\Model getBucketAcl(array $args = array());
```

#### Sample Request

```php
try {
    $result = $cosClient->getBucketAcl(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Return Result Example
```php
Array
(
    [data:protected] => Array
        (
          [Owner] => Array
              (
                 [ID] => qcs::cam::uin/100000000001:uin/100000000001
                 [DisplayName] => qcs::cam::uin/100000000001:uin/100000000001
              )

          [Grants] => Array
                (
                  [0] => Array
                      (
                        [Grantee] => Array
                           (
                             [ID] => qcs::cam::uin/100000000001:uin/100000000001
                             [DisplayName] => qcs::cam::uin/100000000001:uin/100000000001
                           )

                        [Permission] => FULL_CONTROL
                      )

                )

          [RequestId] => NWE3YzhjMTRfYzdhMzNiMGFfYjdiOF8yYzZmMzU=
        )
)
```
#### Return Result Descriptions


| Parameter name | Type | Description | Parent Node |
| ------------------- | -------- | ---------------------------------- | ------------- |
| Grants | Array | ACL permission list                         | None |
| Grant | Array | ACL permission information         | Grants |
| Grantee | Array | ACL permission information                     | Grant |
| Permission | String | Permission type. Value range: FULL_CONTROL, WRITE, READ | Grant  |
| Owner | String | Bucket owner information | None |
| DisplayName | String | Permission owner name      | Grantee/Owner |
| ID | String | Permission owner ID              | Grantee/Owner |

