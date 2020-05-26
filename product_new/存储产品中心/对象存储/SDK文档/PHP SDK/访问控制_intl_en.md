## Overview

This document provides an overview of APIs and SDK code samples related to bucket and object access control lists (ACLs).

**Bucket ACL**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | --------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL for a specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Gets the ACL of a specified bucket |

**Object ACL**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for a specified object (file/object) in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object (file/object) |

## Bucket ACL

### Setting bucket ACL

#### Feature description

This API is used to set the access control list (ACL) for a specified bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model putBucketAcl(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-acl)

```php
try {
    $result = $cosClient->putBucketAcl(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
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

#### Parameter description

| Parameter Name | Type | Description | Parent Node |
| ----------- | ------ | ------------------------------------------------------------ | ------------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID`                         | None |
| Grants | Array | ACL permissions list | None |
| Grant | Array | ACL permission information | Grants |
| Grantee | Array | ACL permission information | Grant |
| Type | String | Owner permission type        | Grantee  |
| Permission | String | Permission type. Valid values: FULL_CONTROL, WRITE, READ | Grant  |
| ACL | String | Overall permission type. Valid values: private, public-read, public-read-write | None |
| Owner | String | Bucket owner information        | None |
| DisplayName | String | Permission owner name      | Grantee/Owner |
| ID | String | Permission owner ID              | Grantee/Owner |



### Querying bucket ACL

#### Feature description

This API is used to get the access control list (ACL) for a specified bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getBucketAcl(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-acl)

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

#### Sample return result

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

#### Returned result description

| Parameter Name | Type | Description | Parent Node |
| ----------- | ------ | ----------------------------------------------- | ------------- |
| Grants | Array | ACL permissions list | None |
| Grant | Array | ACL permission information | Grants |
| Grantee | Array | ACL permission information | Grant |
| Permission | String | Permission type. Valid values: FULL_CONTROL, WRITE, READ | Grant  |
| Owner | String | Bucket owner information        | None |
| DisplayName | String | Permission owner name      | Grantee/Owner |
| ID | String | Permission owner ID              | Grantee/Owner |

## Object ACL

### Setting object ACL

#### Feature description

This API (PUT Object acl) is used to set the access control list (ACL) for a specified object.

#### Method prototype

```php
public Guzzle\Service\Resource\Model putObjectAcl(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-put-object-acl)

```php
try {
    $result = $cosClient->putObjectAcl(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
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

#### Parameter description

| Parameter Name | Type | Description | Required |
| ----------- | ------ | --------------------------------------------- | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key | Yes |
| Grants | Array | ACL permission list | No |
| Grant | Array | ACL permission information | No |
| Grantee | Array | ACL permission information | No |
| Type | String | Owner permission type        | No  |
| Permission | String | Permission type. Valid values: FULL_CONTROL, WRITE, READ | No |
| ACL | String | Overall permission type. Valid values: private, public-read | No |
| Owner | String | Bucket owner information        | No |
| DisplayName | String | Permission owner name      | No |
| ID | String | Permission owner ID | No |

### Querying object ACL

#### Feature description

This API (GET Object acl) is used to query the access control list (ACL) of a specified object.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getObjectAcl(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-get-object-acl)

```php
try {
    $result = $cosClient->getObjectAcl(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key' => 'exampleobject',
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample return result

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

#### Returned result description

| Parameter Name | Type | Description | Parent Node |
| ----------- | ------ | ---------------------------------------------- | --------------- |
| Grants | Array | ACL permissions list | None |
| Grant | Array | ACL permission information | Grants |
| Grantee | Array | ACL permission information | Grant |
| Permission | String | Permission type. Valid values: FULL_CONTROL, WRITE, READ | Grant  |
| Owner | String | Bucket owner information        | None |
| DisplayName | String | Permission owner name      | Grantee / Owner |
| ID | String | Permission owner ID | Grantee / Owner |

