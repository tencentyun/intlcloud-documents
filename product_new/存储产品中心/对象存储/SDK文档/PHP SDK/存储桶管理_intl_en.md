## Introduction
This document provides an overview of APIs and SDK code samples related to cross-origin access, lifecycle, versioning, and cross-region replication.

**Cross-origin Access**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------------------- |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets cross-origin access permissions for a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries cross-origin access configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes cross-origin access configuration of a bucket |

**Lifecycle**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------------------- |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets lifecycle management for a bucket | 
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management  configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

**Versioning**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets versioning configuration for a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region Replication**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets cross-region replication rules for a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rules of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rules of a bucket |


## Cross-Origin Access
### Setting Cross-origin Access Configuration

#### Feature Description

This API (PUT Bucket cors) is used to set the cross-origin access configuration of a bucket.

#### Method Prototype
```php
public Guzzle\Service\Resource\Model putBucketCors(array $args = array());
```

#### Sample Request
```php
try {
    $result = $cosClient->putBucketCors(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
        'CORSRules' => array(
            array(
                'AllowedHeaders' => array('*',),
                'AllowedMethods' => array('Put', ),
                'AllowedOrigins' => array('*', ),
                'ExposeHeaders' => array('*', ),
                'MaxAgeSeconds' => 1,
            ),  
            // ... repeated
        )   
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter Description

| Parameter Name | Type | Description | Required |
| -------------- | ------ | ------------------------------------------------------------ | --------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| CORSRules      | Array  | CORS configuration list                                                 | Yes |
| CORSRule     | Array  | CORS configuration                                                | Yes |
| AllowedMethods | String | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE       | Yes  |
| AllowedOrigins | String | | Allowed source origins. Wildcard `*` is supported. Format: `Protocol://domain name[:port]`, e.g. `http://www.qq.com` | Yes |
| AllowedHeaders | String | Tells the server side when sending the `OPTIONS` request what user-defined HTTP request headers can be used for subsequent requests. Wildcard `*` is supported | No |
| ExposeHeaders  | String | Sets the user-defined header information from the server side that the browser can receive | No |
| MaxAgeSeconds  | Int    | Sets the validity period of the `OPTIONS` request result                      | No  |
| ID             | String |  Configures the rule ID | Yes |


### Querying Cross-origin Access Configuration

#### Feature Description

This API (GET Bucket cors) is used to query the cross-origin access configuration of a bucket.

#### Method Prototype
```php
public Guzzle\Service\Resource\Model getBucketCors(array $args = array());
```

#### Sample Request
```php
try {
    $result = $cosClient->getBucketCors(array(
        'Bucket' => 'examplebucket-1250000000' //Format: BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter Description

| Parameter Name | Type | Description | Required |
| -------- | ------ | ---------------------------------- | ------ |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |

#### Sample Response
```php
Guzzle\Service\Resource\Model Object
(
    [data:protected] => Array
        (
            [CORSRules] => Array
                (
                    [0] => Array
                        (
                            [ID] => 1234
                            [AllowedHeaders] => Array
                                (
                                    [0] => *
                                )
                            [AllowedMethods] => Array
                                (
                                    [0] => PUT
                                )
                            [AllowedOrigins] => Array
                                (
                                    [0] => http://www.qq.com
                                )
                        )
                )
            [RequestId] => NWE3YzhkMmRfMTdiMjk0MGFfNTQzZl8xNWUwMGU=
        )
)
```
#### Response Description


| Parameter Name | Type | Description | Parent Node | 
| -------------- | ------ | ------------------------------------------------------------ | --------- |
| CORSRules      | Array  | CORS configuration list list                                                 |None |
| CORSRule     | Array  | CORS configuration                                                | CORSRules |
| AllowedMethods | String | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE       | CORSRule |
| AllowedOrigins | String | | Allowed source origins. Wildcard `*` is supported. Format: `Protocol://domain name[:port]`, e.g. `http://www.qq.com` | CORSRule |
| AllowedHeaders | String | Tells the server side when sending the `OPTIONS` request what user-defined HTTP request headers can be used for subsequent requests. Wildcard `*` is supported | CORSRule |
| ExposeHeaders  | String | Sets the user-defined header information from the server side that the browser can receive | CORSRule |
| MaxAgeSeconds  | Int    | Sets the validity period of the `OPTIONS` request result                      | CORSRule  |
| ID             | String |  Configures the rule ID | CORSRule |


### Deleting Cross-origin Access Configuration

#### Feature Description

This API (DELETE Bucket cors) is used to delete the cross-origin access configuration of a bucket.

#### Method Prototype
```php
public Guzzle\Service\Resource\Model deleteBucketCors(array $args = array());
```

#### Sample Request
```php
try {
    $result = $cosClient->deleteBucketCors(array(
        'Bucket' => 'examplebucket-1250000000' //Format: BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter Description

| Parameter Name | Type | Description | Required |
| -------- | ------ | ---------------------------------- | ------ |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |


## Lifecycle
### Setting Lifecycle

#### Feature Description

This API (PUT Bucket lifecycle) is used to set the lifecycle configuration of a bucket.

#### Method Prototype
```php
public Guzzle\Service\Resource\Model putBucketLifecycle(array $args = array());
```

#### Sample Request
```php
try {
    $result = $cosClient->putBucketLifecycle(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
        'Rules' => array(
            array(
                'Expiration' => array(
                    'Days' => integer,
                ),  
                'ID' => 'string',
                'Filter' => array(
                    'Prefix' => 'string'
                ),  
                'Status' => 'string',
                'Transitions' => array(
                    array(
                        'Days' => integer,
                        'StorageClass' => 'string'
                    ),  
                    // ... repeated
                ),  
            ),  
            // ... repeated
        )
    ));  
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter Description

| Parameter Name | Type | Description | Required |
| ------------ | ------------ | ------------------------------------------------------------ | ----------------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Rules        | Array        | Lifecycle configuration list                                             | Yes |
| Rules        | Array        | Lifecycle configuration                                            | Yes |
| Expiration   | Array        | Object expiration rule. You can specify an expiry date (`Date`) or the number of days before the objects expire (`Days`) | No |
| Transition   | Array        | Object transitioning rule                               | No |
| Filter       | Array        | Specifies which objects are subject to the rule                               | Yes |
| Prefix | String | Prefix used to filter objects | Yes |
| Status | String | Sets whether the rule is enabled or not. Valid values: `Enabled`, `Disabled` | Yes |
| ID             | String |  Configures the rule ID | Yes |
| Days         | Int          | Sets the number of days before the rule takes effect                                            | No |
| Date        | Int / String  | Sets the rule effective date                                             | No |
| StorageClass | String | Sets the object storage class to which objects are transitioned. Valid values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD`  | Yes |

### Querying Lifecycle

#### Feature Description

This API (GET Bucket lifecycle) is used to query the lifecycle configuration of a bucket.

#### Method Prototype
```php
public Guzzle\Service\Resource\Model getBucketLifecycle(array $args = array());
```

#### Sample Request
```php
try {
    $result = $cosClient->getBucketLifecycle(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter Description

| Parameter Name | Type | Description | Required |
| -------- | ------ | ---------------------------------- | ------ |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |

#### Sample Response
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
#### Response Description


| Parameter Name | Type | Description | Parent Node | 
| ------------ | ------------ | ------------------------------------------------------------ | ----------------------- |
| Rules        | Array        | Lifecycle configuration list                                             |None |
| Rules        | Array        | Lifecycle configuration                                          | Rules |
| Expiration   | Array        | Object expiration rule. You can specify an expiry date (`Date`) or the number of days before the objects expire (`Days`) | Rule|
| Transition   | Array        | Object transitioning rule                               | Rule |
| Filter       | Array        | Specifies which objects are subject to the rule                               | Rule |
| Prefix | String | Prefix used to filter the objects | Filter |
| Status | String | Sets whether the rule is enabled or not. Valid values: `Enabled`, `Disabled` | Rule |
| ID             | String |  Configures the rule ID | Rule |
| Days         | Int          | Sets the number of days before the rule takes effect                                              | Expiration / Transition |
| Date         | Int / String  |  Sets the rule effective date                                              | Expiration / Transition |
| StorageClass | String | Sets the object storage class to which objects are transitioned. Valid values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD`  | Transition |



### Deleting Lifecycle

#### Feature Description

This API (DELETE Bucket lifecycle) is used to delete the lifecycle configuration of a bucket.

#### Method Prototype
```php
public Guzzle\Service\Resource\Model deleteBucketLifecycle(array $args = array());
```

#### Sample Request
```php
try {
    $result = $cosClient->deleteBucketLifecycle(array(
        'Bucket' => 'examplebucket-1250000000' //Format: BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter Description

| Parameter Name | Type | Description | Required |
| -------- | ------ | ---------------------------------- | ------ |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |

## Versioning
### Setting Versioning

#### Feature Description

This API (PUT Bucket versioning) is used to set versioning for a bucket.

#### Method Prototype
```
public Guzzle\Service\Resource\Model putBucketVersioning(array $args = array());
```

#### Sample Request

**Enable Versioning**

```php
try {
    $result = $cosClient->putBucketVersioning(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
        'Status' => 'Enabled'
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

**Suspend Versioning**

```php
try {
    $result = $cosClient->putBucketVersioning(array(
        'Bucket' => 'examplebucket-125000000', //Format：BucketName-APPID
        'Status' => 'Suspended'
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter Description

| Parameter Name | Type | Description | Required |
| -------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |
| Status | String | Versioning status. Valid values: `Suspended`, `Enabled` | Yes |


### Querying Versioning

#### Feature Description

This API (GET Bucket versioning) is used to query the versioning configuration of a bucket.

#### Method Prototype
```
public Guzzle\Service\Resource\Model getBucketVersioning(array $args = array());
```

#### Sample Request
```
try {
    $result = $cosClient->getBucketVersioning(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter Description

| Parameter Name | Type | Description | Required |
| -------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |


#### Response Description
| Parameter Name | Type | Description | Parent Node | 
| -------------- | -------- | ---------------------------------- | ------------- |
| Status | String | Versioning status. Valid values: `Suspended`, `Enabled`. This parameter may be empty |None |


## Cross-region Replication
### Setting Cross-region Replication

#### Feature Description

This API (PUT Bucket replication) is used to set cross-region replication rules for a bucket.

#### Method Prototype
```
public Guzzle\Service\Resource\Model putBucketReplication(array $args = array());
```

#### Sample Request
```
try {
    $result = $cosClient->putBucketReplication(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
        'Role' => 'qcs::cam::uin/100000000001:uin/100000000001',
        'Rules'=>array(
            array(
                'Status' => 'Enabled',
                'ID' => 'string',
                'Prefix' => 'string',
                'Destination' => array(                    'Bucket' => 'qcs::cos:ap-guangzhou::examplebucket2-125000000',
                    'StorageClass' => 'standard',                ),  
                // ...repeated            ),  
        ),      )); 
    // Request succeeded   print_r($result);
} catch (\Exception $e) {    // Request failed
    echo "$e\n";
}
```

#### Parameter Description
| Parameter Name | Type | Description | Required |
| -------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Source bucket name. Format: BucketName-APPID | Yes |
| Role | String | Identifies the replication initiator. Format：`qcs::cam::uin/:uin/` | Yes |
| Rule | Array | Configures rule information, including its `ID`, `Status`, `Prefix`, and `Destination` | Yes |
| ID | String | Sets rule ID.  | Yes |
| Status | String | Sets whether the rule is enabled or not. Valid values: `Enabled`, `Disabled` | Yes |
| Prefix | String |  Prefix used to filter objects that are subject to the rule. If it is left empty, it means that the rule applies to all objects in the bucket | Yes |
| Destination | String |   Describes information on object copies, including `Bucket` and `StorageClass` | Yes |
| Bucket | String | Sets the destination bucket of the cross-region replication. Format: `qcs::cos:[region]::[BucketName-APPID]` | Yes |
| StorageClass | String | Sets the storage class of the object copies. Valid values: `STANDARD`, `STANDARD_IA` | No |



### Querying Cross-region Replication

#### Feature Description

This API (GET Bucket replication) is used to query the cross-region replication rules of a bucket.

#### Method Prototype
```
public Guzzle\Service\Resource\Model getBucketReplication(array $args = array());
```

#### Sample Request
```
try {
    $result = $cosClient->getBucketReplication(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter Description

| Parameter Name | Type | Description | Required |
| -------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |

#### Sample Response
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
                                    [Bucket] => qcs::cos:ap-guangzhou::examplebucket2-125000000
                                    [StorageClass] => 
                                )
                        )
                )
            [RequestId] => NWQwOGI5MGVfNWFiMjU4NjRfNDUzY19mNzRhMTU=
        )
)
```


#### Response Description

| Parameter Name | Type | Description | Parent Node | 
| -------------- | -------- | ---------------------------------- | ------------- |
| Role | String | Identifies the replication initiator. Format：`qcs::cam::uin/:uin/` |None |
| Rules | Array | Configures rule information, including its `ID`, `Status`, `Prefix`, and `Destination` |None |
| Rule | Array | Configures rule information, including its `ID`, `Status`, `Prefix`, and `Destination` | Rules |
| ID | String | Sets rule ID. | Rule |
| Status | String | Sets whether the rule is enabled or not. Valid values: `Enabled`, `Disabled` | Rule |
| Prefix | String |  Prefix used to filter objects that are subject to the rule. If it is left empty, it means that the rule applies to all objects in the bucket | Rule |
| Destination | String |  Describes information on object copies, including `Bucket` and `StorageClass` | Rule |
| Bucket | String | Sets the destination bucket of the cross-region replication. Format: `qcs::cos:[region]::[BucketName-APPID]` | Destination |
| StorageClass | String | Sets the storage class of the object copies. Valid values: `STANDARD`, `STANDARD_IA` | Destination |


## Deleting Cross-region Replication

#### Feature Description

This API (DELETE Bucket replication) is used to delete the cross-region replication rules of a bucket.

#### Method Prototype
```
public Guzzle\Service\Resource\Model deleteBucketReplication(array $args = array());
```

#### Sample Request
```
try {
    $result = $cosClient->deleteBucketReplication(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter Description
| Parameter Name | Type | Description | Required |
| -------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |

