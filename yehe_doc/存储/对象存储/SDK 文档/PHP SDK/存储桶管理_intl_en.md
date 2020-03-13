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
| [PUT Bucket lifecycle](https://cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets lifecycle management for a bucket | 
| [GET Bucket lifecycle](https://cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management  configuration of a bucket |
| [DELETE Bucket lifecycle](https://cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

**Versioning**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets versioning configuration for a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region Replication**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets cross-region replication rules for a bucket |
| [GET Bucket replication](https://cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rules of a bucket |
| [DELETE Bucket replication](https://cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rules of a bucket |


## Cross-Origin Access
### Setting Cross-origin Access Configuration

#### Feature Description

This API (Put Bucket CORS) is used to set the configurations on cross-origin access (CORS) of a bucket.

#### Method Prototype
```php
public Guzzle\Service\Resource\Model putBucketCors(array $args = array());
```

#### Sample Request
[//]: # (.cssg-snippet-put-bucket-cors)
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
| CORSRules      | Array  | Cross-origin information list                                                 | Yes |
| CORSRule     | Array  | Cross-origin information                                                | Yes |
| AllowedMethods | String | HTTP operations allowed，Enumerated values: GET，PUT，HEAD，POST，DELETE       | Yes  |
| AllowedOrigins | String | | Allowed source origins. Wildcard `*` is supported. Format: `Protocol://domain name[:port]`, Example: `http://www.qq.com` | Yes |
| AllowedHeaders | String | Tells the server what customized HTTP request headers can be used for following requests when the OPTIONS request is sent. Wildcard `*` is supported | No |
| ExposeHeaders  | String | Sets the customized header information, which can be received by the browser from the server end | No |
| MaxAgeSeconds  | Int    | Sets the validity period of the results obtained by OPTIONS                      | No |
| ID             | String |  Configures the rule ID | Yes |


### Querying Cross-origin Access Configuration

#### Feature Description

This API (Get Bucket CORS) is used to get the configurations on cross-origin access (CORS) of a bucket.

#### Method Prototype
```php
public Guzzle\Service\Resource\Model getBucketCors(array $args = array());
```

#### Sample Request
[//]: # (.cssg-snippet-get-bucket-cors)
```php
try {
    $result = $cosClient->getBucketCors(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
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
#### Returned Result


| Parameter Name | Type | Description | Parent Node | 
| -------------- | ------ | ------------------------------------------------------------ | --------- |
| CORSRules      | Array  | Cross-origin information list                                                 | |
| CORSRule     | Array  | Cross-origin information                                                | CORSRules |
| AllowedMethods | String | HTTP operations allowed，Enumerated values: GET，PUT，HEAD，POST，DELETE       | CORSRule |
| AllowedOrigins | String | | Allowed source origins. Wildcard `*` is supported. Format: `Protocol://domain name[:port]`, Example: `http://www.qq.com` | CORSRule |
| AllowedHeaders | String | Tells the server what customized HTTP request headers can be used for following requests when the OPTIONS request is sent. Wildcard `*` is supported | CORSRule |
| ExposeHeaders  | String | Sets the customized header information, which can be received by the browser from the server end | CORSRule |
| MaxAgeSeconds  | Int    | Sets the validity period of the results obtained by OPTIONS                      | CORSRule  |
| ID             | String |  Configures the rule ID | CORSRule |


### Deleting Cross-origin Access Configuration

#### Feature Description

This API (Delete Bucket CORS) is used to delete the configurations on cross-origin access (CORS) of a bucket.

#### Method Prototype
```php
public Guzzle\Service\Resource\Model deleteBucketCors(array $args = array());
```

#### Sample Request
[//]: # (.cssg-snippet-delete-bucket-cors)
```php
try {
    $result = $cosClient->deleteBucketCors(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
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

This API (Put Bucket LifeCycle) is used to set the lifecycle configuration of a bucket.

#### Method Prototype
```php
public Guzzle\Service\Resource\Model putBucketLifecycle(array $args = array());
```

#### Sample Request
[//]: # (.cssg-snippet-put-bucket-lifecycle)
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
| Rules        | Array        | Lifecycle information list                                             | Yes |
| Rules        | Array        | Lifecycle information                                            | Yes |
| Expiration   | Array        | Sets expiration rule of Object in the format of setting date or days | No |
| Transition   | Array        | Sets storage class transition rules of Object                               | No |
| Filter       | Array        | Shows all Objects to which the Rule applies                               | Yes |
| Prefix | String | Prefix of the objects to be analyzed | Yes |
| Status | String | Sets whether Rule is enabled. Available values: Enabled or Disabled | Yes |
| ID             | String |  Configures the rule ID | Yes |
| Days         | Int          | Sets days of validity                                              | No |
| Date        | Int / String  | Sets the date of validity                                              | No |
| StorageClass | String | Sets the object storage class; Options: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD  | Yes |

### Querying Lifecycle

#### Feature Description

This API (Get Bucket Lifecycle) is used to get the lifecycle configuration of a Bucket.

#### Method Prototype
```php
public Guzzle\Service\Resource\Model getBucketLifecycle(array $args = array());
```

#### Sample Request
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
#### Returned Result


| Parameter Name | Type | Description | Parent Node | 
| ------------ | ------------ | ------------------------------------------------------------ | ----------------------- |
| Rules        | Array        | Lifecycle information list                                             | |
| Rules        | Array        | Lifecycle information                                          | Rules |
| Expiration   | Array        | Sets expiration rule of Object in the format of setting date or days | Rule|
| Transition   | Array        | Sets storage class transition rules of Object                               | Rule |
| Filter       | Array        | Shows all Objects to which the Rule applies                               | Rule |
| Prefix | String | Prefix of the objects to be analyzed | Filter |
| Status | String | Sets whether Rule is enabled. Available values: Enabled or Disabled | Rule |
| ID             | String |  Configures the rule ID | Rule |
| Days         | Int          | Sets days of validity                                              | Expiration / Transition |
| Date         | Int / String  |  Sets the date of validity                                              | Expiration / Transition |
| StorageClass | String | Sets the object storage class; Options: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD  | Transition |



### Deleting Lifecycle

#### Feature Description

This API (Delete Bucket Lifecycle) is used to delete the lifecycle configuration of a Bucket.

#### Method Prototype
```php
public Guzzle\Service\Resource\Model deleteBucketLifecycle(array $args = array());
```

#### Sample Request
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

#### Parameter Description

| Parameter Name | Type | Description | Required |
| -------- | ------ | ---------------------------------- | ------ |
| Bucket | String | Bucket name. Format: BucketName-APPID | Yes |

## Versioning
### Setting Versioning

#### Feature Description

This API (Put Bucket versioning) is used to set the versioning information of a bucket.

#### Method Prototype
```
public Guzzle\Service\Resource\Model putBucketVersioning(array $args = array());
```

#### Sample Request

**Enable Versioning**

[//]: # (.cssg-snippet-put-bucket-versioning)
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

**Suspension of versioning**

```php
try {
    $result = $cosClient->putBucketVersioning(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
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
| Status | String | Status of version control. Options are Suspended, Enabled or empty | Yes |


### Querying Versioning

#### Feature Description

This API (Get Bucket versioning) is used to get the versioning information of a bucket.

#### Method Prototype
```
public Guzzle\Service\Resource\Model getBucketVersioning(array $args = array());
```

#### Sample Request
[//]: # (.cssg-snippet-get-bucket-versioning)
```php
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


#### Returned Result
| Parameter Name | Type | Description | Parent Node | 
| -------------- | -------- | ---------------------------------- | ------------- |
| Status | String | Status of version control. Options are Suspended, Enabled or empty | |


## Cross-region Replication
### Setting Cross-region Replication

#### Feature Description

This API (PUT Bucket replication) is used to set cross-region replication rules for a bucket

#### Method Prototype
```
public Guzzle\Service\Resource\Model putBucketReplication(array $args = array());
```

#### Sample Request
[//]: # (.cssg-snippet-put-bucket-replication)
```php
try {
    $result = $cosClient->putBucketReplication(array(
        'Bucket' => 'examplebucket-1250000000', //Format：BucketName-APPID
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

#### Parameter Description
| Parameter Name | Type | Description | Required |
| -------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Origin Bucket name. Format: BucketName-APPID | Yes |
| Role | String | Replication initiator identifier. Format：`qcs::cam::uin/:uin/` | Yes |
| Rule | Array | Sets rule ID，Status，Prefix，and Destination | Yes |
| ID | String | Sets rule ID.  | Yes |
| Status | String | Sets whether Rule is enabled. Available values: Enabled or Disabled | Yes |
| Prefix | String |  Sets Rule of matching with prefix. Empty string means all objects | Yes |
| Destination | String |   Describes destination resource, including Bucket and StorageClass | Yes |
| Bucket | String | Set cross-region target bucket. Format: `qcs::cos:[region]::[BucketName-APPID]` | Yes |
| StorageClass | String | Set storage class. Options are  'STANDARD'，'STANDARD_IA' | No |



### Querying Cross-region Replication

#### Feature Description

This API (GET Bucket replication) is used to query the cross-region replication rules of a bucket.

#### Method Prototype
```
public Guzzle\Service\Resource\Model getBucketReplication(array $args = array());
```

#### Sample Request
[//]: # (.cssg-snippet-get-bucket-replication)
```php
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


#### Returned Result

| Parameter Name | Type | Description | Parent Node | 
| -------------- | -------- | ---------------------------------- | ------------- |
| Role | String | Replication initiator identifier. Format：`qcs::cam::uin/:uin/` | No |
| Rules | Array | Sets rule ID，Status，Prefix，and Destination | No |
| Rule | Array | Sets rule ID，Status，Prefix，and Destination | Rules |
| ID | String | Sets rule ID. | Rule |
| Status | String | Sets whether Rule is enabled. Available values: Enabled or Disabled | Rule |
| Prefix | String |  Prefix used to filter objects that are subject to the rule. If it is left empty, it means that the rule applies to all objects in the bucket | Rule |
| Destination | String |  Describes destination resource, including Bucket and StorageClass | Rule |
| Bucket | String | Set target bucket. Format: `qcs::cos:[region]::[BucketName-APPID]` | Destination |
| StorageClass | String | Set storage class. Options are  'STANDARD'，'STANDARD_IA' | Destination |


## Deleting Cross-region Replication

#### Feature Description

This API (DELETE Bucket replication) is used to delete the cross-region replication rules of a bucket

#### Method Prototype
```
public Guzzle\Service\Resource\Model deleteBucketReplication(array $args = array());
```

#### Sample Request
[//]: # (.cssg-snippet-delete-bucket-replication)
```php
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

