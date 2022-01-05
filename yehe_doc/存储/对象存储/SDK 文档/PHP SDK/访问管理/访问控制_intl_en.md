## Overview

This document provides an overview of APIs and SDK code samples related to the access control lists (ACLs) for buckets and objects.

**Bucket ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | --------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting a bucket ACL | Sets an ACL for a bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying a bucket ACL | Gets the ACL of a specified bucket |

**Object ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting an object ACL | Sets an ACL for an object (file) in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying an object ACL | Queries the ACL of an object (file) |

## Bucket ACL

### Setting a bucket ACL

#### Description

This API is used to set an access control list (ACL) for a specified bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model putBucketAcl(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-acl)

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
    $result = $cosClient->putBucketAcl(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
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

| Parameter | Type | Description | Parent Node |
| ----------- | ------ | ------------------------------------------------------------ | ------------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Grants    | Array  | ACL permission list                                                  | None          |
| Grant       | Array  | ACL permission information                               | Grants          |
| Grantee    | Array  | ACL permission information                                                  | Grant          |
| Type        | String | Permission type of the authorized user                               | Grantee         |
| Permission  | String | Permission type. Valid values: `FULL_CONTROL`, `WRITE`, `READ` | Grant           |
| ACL         | String | Global permission type. Valid values: `private`, `public-read`, `public-read-write` | None              |
| Owner       | String | Information about the bucket owner                               | None              |
| DisplayName | String | Name of the bucket owner                         | Grantee/Owner |
| ID          | String | ID of the bucket owner           | Grantee/Owner |



### Querying a bucket ACL

#### Description

This API is used to query the access control list (ACL) of a specified bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getBucketAcl(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-acl)

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
    $result = $cosClient->getBucketAcl(array(
        'Bucket' => 'examplebucket-1250000000' // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample response

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

#### Response description

| Parameter | Type | Description | Parent Node |
| ----------- | ------ | ----------------------------------------------- | ------------- |
| Grants    | Array  | ACL permission list                                                  | None          |
| Grant       | Array  | ACL permission information                               | Grants          |
| Grantee    | Array  | ACL permission information                                                  | Grant          |
| Permission  | String | Permission type. Valid values: `FULL_CONTROL`, `WRITE`, `READ` | Grant           |
| Owner       | String | Information about the bucket owner                               | None              |
| DisplayName | String | Name of the bucket owner                         | Grantee/Owner |
| ID          | String | ID of the bucket owner           | Grantee/Owner |

## Object ACL

### Setting an object ACL

#### Description

This API is used to set the ACL of an object.

#### Method prototype

```php
public Guzzle\Service\Resource\Model putObjectAcl(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-put-object-acl)

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
    $result = $cosClient->putObjectAcl(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
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

| Parameter | Type | Description | Required |
| ----------- | ------ | --------------------------------------------- | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| Key | String | Object key | Yes |
| Grants    | Array  | ACL permission list                                                  | No          |
| Grant       | Array  | ACL permission information                                                  | No          |
| Grantee    | Array  | ACL permission information                                                  | No          |
| Type        | String | Permission type of the authorized user                                | No         |
| Permission  | String | Permission type. Valid values: `FULL_CONTROL`, `WRITE`, `READ` | No         |
| ACL         | String | Global permission type. Valid values: `private`, `public-read` | No              |
| Owner       | String | Information about the bucket owner                               | No              |
| DisplayName | String | Name of the bucket owner | No |
| ID          | String | ID of the bucket owner                                            | No |

### Querying an object ACL

#### Description

The API is used to query the ACL of an object.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getObjectAcl(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-get-object-acl)

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
    $result = $cosClient->getObjectAcl(array(
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

#### Sample response

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

#### Response description

| Parameter | Type | Description | Parent Node |
| ----------- | ------ | ---------------------------------------------- | --------------- |
| Grants    | Array  | ACL permission list                                                  | None          |
| Grant       | Array  | ACL permission information                               | Grants          |
| Grantee    | Array  | ACL permission information                                                  | Grant          |
| Permission  | String | Permission type. Valid values: `FULL_CONTROL`, `WRITE`, `READ` | Grant         |
| Owner       | String | Information about the bucket owner                               | None              |
| DisplayName | String | Name of the bucket owner                         | Grantee/Owner |
| ID          | String | ID of the bucket owner           | Grantee/Owner |

