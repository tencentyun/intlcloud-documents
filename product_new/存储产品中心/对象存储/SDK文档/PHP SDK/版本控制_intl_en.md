## Overview

This document provides an overview of APIs and SDK code samples related to versioning.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets the versioning feature of a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

## Setting Versioning

#### Feature description

This API (PUT Bucket versioning) is used to set the versioning feature of a specified bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model putBucketVersioning(array $args = array());
```

#### Sample request

**Enable versioning**

[//]: # (.cssg-snippet-put-bucket-versioning)

```php
try {
    $result = $cosClient->putBucketVersioning(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Status' => 'Enabled'
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

**Suspend versioning**

```php
try {
    $result = $cosClient->putBucketVersioning(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Status' => 'Suspended'
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
| -------- | ------ | -------------------------------------------------- | -------- |
| Bucket | String | Bucket for which to enable or suspend versioning in the format of `BucketName-APPID` | Yes |
| Status |  String | Versioning policy. Valid values: Suspended, Enabled  | Yes |

## Querying Versioning

#### Feature description

This API (GET Bucket versioning) is used to query the versioning information of a specified bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model getBucketVersioning(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-versioning)

```php
try {
    $result = $cosClient->getBucketVersioning(array(
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
| -------- | ------ | -------------------------------------------- | -------- |
| Bucket | String | Bucket for which to query versioning in the format of `BucketName-APPID` | Yes |

#### Returned result description

| Parameter name | Type | Description | Parent Node |
| -------- | ------ | --------------------------------------------- | ------ |
| Status |  String | Versioning policy. Valid values: Suspended, Enabled, null | None |
