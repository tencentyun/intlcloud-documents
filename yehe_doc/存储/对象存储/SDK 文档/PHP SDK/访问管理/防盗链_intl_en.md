## Overview

This document provides an overview of APIs and SDK code samples related to bucket referer allowlist or blocklist.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | Setting a bucket referer | Sets a bucket referer allowlist or blocklist |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | Querying a bucket referer | Queries a bucket referer allowlist or blocklist |

### Setting a bucket referer

#### API description

This API (PUT Bucket referer) is used to set the referer allowlist/blocklist for a bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model putBucketReferer(array $args = array());
```

#### Sample request

```php
try {
    $result = $cosClient->putBucketReplication(array(
            'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
            'Status' => 'Enabled', // Whether to enable hotlink protection. Enumerated values: “Enabled”, “Disabled”
            'RefererType' => 'White-List', // Hotlink protection type. Enumerated values: “Black-List”, “White-List”
            'DomainList' => array(
                'Domains' => array(
                     '*.qq.com', // A single domain
                     '*.qcloud.com', // A single domain
                )
            ), // Domain list
            'EmptyReferConfiguration' => 'Allow', // Whether to allow access with an empty referer. Enumerated values: “Allow”, “Deny” (default)
        ),      
    ); 
    // Request successful    
    print_r($result);
} catch (\Exception $e) {   
    // Request failed
    echo($e);
}
```
#### Parameter description

| Parameter | Description | Type | Required |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID`. | String | Yes |
| Status         | Whether to enable hotlink protection. Enumerated values: `Enabled`, `Disabled`           | String | Yes   |
| RefererType    | Hotlink protection type. Enumerated values: `Black-List`, `White-List`          | String | Yes   |
| DomainList | Domain list | Array | Yes  |
| EmptyReferConfiguration | Whether to allow access with an empty referer. Enumerated values: `Allow`, `Deny` (default) | String | No |

### Querying a bucket referer

#### API description

This API (GET Bucket referer) is used to query the referer allowlist/blocklist of a bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getBucketReferer(array $args = array());
```

#### Sample request

```php
try {
    $result = $cosClient->getBucketReferer(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
    )); 
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID`. | String | Yes |

#### Sample response
```php
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjE0NTk2ZWVfZmQzNDJjMGJfMWNiNmVfN2Y1MWQx
    [ContentType] => application/xml
    [ContentLength] => 260
    [Status] => Enabled
    [RefererType] => White-List
    [EmptyReferConfiguration] => Allow
    [DomainList] => Array
        (
            [Domain] => Array
                (
                    [0] => *.qq.com
                    [1] => *.qcloud.com
                )

        )

    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/
)
```
