## Overview
This document provides an overview of APIs related to cross-origin access, lifecycle, versioning, and cross-region replication and corresponding SDK sample code.

**Cross-origin access**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | -------------------------------- |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets the cross-origin access permission of a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration information of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration information of a bucket |

**Lifecycle**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | -------------------------------- |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets the lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

**Versioning**

| API | Operation Name | Operation Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets the versioning feature of a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region replication**

| API | Operation Name | Operation Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets the cross-region replication rule of a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rule of a bucket |


## Cross-origin Access
### Setting Cross-origin Access Configuration

#### Feature Description

This API (PUT Bucket cors) is used to set the cross-origin access configuration information of the specified bucket.

#### Method Prototype
```php
public Guzzle\Service\Resource\Model putBucketCors(array $args = array());
```

#### Sample Request
```php
try {
    $result = $cosClient->putBucketCors(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
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

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| -------------- | ------ | ------------------------------------------------------------ | --------- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |
| CORSRules | Array | Cross-origin access information list | Yes |
| CORSRule | Array | Cross-origin access information | Yes |
| AllowedMethods | String | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE | Yes |
| AllowedOrigins | String | Allowed origin in the format of protocol://domain name[:port number], such as `http://www.qq.com`. Wildcard `*` is supported | Yes |
| AllowedHeaders | String | Tells the server what custom HTTP request headers can be used for subsequent requests when the OPTIONS request is sent. Wildcard `*` is supported | No |
| ExposeHeaders  | String | Sets custom header information from the server that the browser can receive | No |
| MaxAgeSeconds | Int | Sets the validity period of the result of the OPTIONS request | No |
| ID             | String | Configures the rule ID                                                | Yes  |


### Querying Cross-origin Access Configuration

#### Feature Description

This API (GET Bucket cors) is used to query the cross-origin access configuration information of the specified bucket.

#### Method Prototype
```php
public Guzzle\Service\Resource\Model getBucketCors(array $args = array());
```

#### Sample Request
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

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| -------- | ------ | ---------------------------------- | ------ |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |

#### Return Result Example
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
#### Return Result Descriptions


| Parameter name | Type | Description | Parent Node |
| -------------- | ------ | ------------------------------------------------------------ | --------- |
| CORSRules | Array | Cross-origin access information list | None |
| CORSRule | Array | Cross-origin access information | CORSRules |
| AllowedMethods | String | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE | CORSRule |
| AllowedOrigins | String | Allowed origin in the format of protocol://domain name[:port number], such as `http://www.qq.com`. Wildcard * is supported | CORSRule |
| AllowedHeaders | String | Tells the server what custom HTTP request headers can be used for subsequent requests when the OPTIONS request is sent. Wildcard `*` is supported | CORSRule |
| ExposeHeaders  | String | Sets custom header information from the server that the browser can receive | CORSRule |
| MaxAgeSeconds | Int | Sets the validity period of the result of the OPTIONS request | CORSRule |
| ID             | String | Configures the rule ID                                                | CORSRule |


### Deleting Cross-origin Access Configuration

#### Feature Description

This API (DELETE Bucket cors) is used to delete the cross-origin access configuration of the specified bucket.

#### Method Prototype
```php
public Guzzle\Service\Resource\Model deleteBucketCors(array $args = array());
```

#### Sample Request
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

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| -------- | ------ | ---------------------------------- | ------ |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |


## Lifecycle
### Setting Lifecycle

#### Feature Description

This API (PUT Bucket lifecycle) is used to set the lifecycle configuration information of the specified bucket.

#### Method Prototype
```php
public Guzzle\Service\Resource\Model putBucketLifecycle(array $args = array());
```

#### Sample Request
```php
try {
    $result = $cosClient->putBucketCors(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
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
    );  
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| ------------ | ------------ | ------------------------------------------------------------ | ----------------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |
| Rules        | Array        | Lifecycle information list                                           | Yes                      |
| Rule         | Array        | Lifecycle information                                                 | Yes                   |
| Expiration | Array | Sets the object expiration rule (either a number of days (Days) or a date (Date) can be specified) | No |
| Transition | Array | Sets the object transition rule | No |
| Filter | Array |  Describes the set of objects subject to the rule | Yes |
| Prefix | String | Prefix of the filtered objects | Yes |
| Status | String | Sets whether a rule is enabled; value range: Enabled, Disabled | Yes |
| ID             | String | Configures the rule ID                                                | Yes  |
| Days | Int | Sets the number of effective days | No |
| Date | Int / String | Sets the effective date | No |
| StorageClass | String | Transitioned file storage class; value range: STANDARD, STANDARD_IA, ARCHIVE; default value: STANDARD | Yes |

### Querying Lifecycle

#### Feature Description

This API (GET Bucket lifecycle) is used to set the lifecycle management configuration for a bucket.

#### Method Prototype
```php
public Guzzle\Service\Resource\Model getBucketLifecycle(array $args = array());
```

#### Sample Request
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

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| -------- | ------ | ---------------------------------- | ------ |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |

#### Return Result Example
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
#### Return Result Descriptions


| Parameter name | Type | Description | Parent Node |
| ------------ | ------------ | ------------------------------------------------------------ | ----------------------- |
| Rules        | Array        | Lifecycle information list                                           | None                       |
| Rule         | Array        | Lifecycle information                                                 | Rules                   |
| Expiration | Array | Sets the object expiration rule (either a number of days (Days) or a date (Date) can be specified) | Rule |
| Transition | Array | Sets the object transition rule | Rule |
| Filter | Array |  Describes the set of objects subject to the rule | Rule |
| Prefix | String | Prefix of the filtered objects | Filter |
| Status | String | Sets whether a rule is enabled; value range: Enabled, Disabled | Rule |
| ID             | String | Configures the rule ID                                                | Rule |
| Days | Int | Sets the number of effective days | Expiration / Transition |
| Date | Int / String | Sets the effective date | Expiration |
| StorageClass | String | Transitioned file storage class; value range: STANDARD, STANDARD_IA, ARCHIVE; default value: STANDARD | Transition |



### Deleting Lifecycle

#### Feature Description

This API (DELETE Bucket lifecycle) is used to delete the lifecycle management configuration of a bucket.

#### Method Prototype
```php
public Guzzle\Service\Resource\Model deleteBucketLifecycle(array $args = array());
```

#### Sample Request
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

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| -------- | ------ | ---------------------------------- | ------ |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |

## Versioning
### Setting Versioning

#### Feature Description

This API (PUT Bucket versioning) is used to set the versioning feature of the specified bucket.

#### Method Prototype
```
public Guzzle\Service\Resource\Model putBucketVersioning(array $args = array());
```

#### Sample Request

**Enable versioning**

```php
try {
    $result = $cosClient->putBucketVersioning(array(
        'Bucket' => 'examplebucket-125000000', // Format: BucketName-APPID
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
        'Bucket' => 'examplebucket-125000000', // Format: BucketName-APPID
        'Status' => 'Suspended'
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| -------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |
| Status |  String | Versioning policy; value range: Suspended, Enabled  | Yes |


### Querying Versioning

#### Feature Description

This API (GET Bucket versioning) is used to query the versioning information of the specified bucket.

#### Method Prototype
```
public Guzzle\Service\Resource\Model getBucketVersioning(array $args = array());
```

#### Sample Request
```
try {
    $result = $cosClient->getBucketVersioning(array(
        'Bucket' => 'examplebucket-125000000', // Format: BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| -------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |


#### Return Result Descriptions
| Parameter name | Type | Description | Parent Node |
| -------------- | -------- | ---------------------------------- | ------------- |
| Status |  String | Versioning policy; value range: Suspended, Enabled, null | None |


## Cross-region Replication
### Setting Cross-region Replication

#### Feature Description

This API (PUT Bucket replication) is used to set the cross-region replication rule for the specified bucket.

#### Method Prototype
```
public Guzzle\Service\Resource\Model putBucketReplication(array $args = array());
```

#### Sample Request
```
try {
    $result = $cosClient->putBucketReplication(array(
        'Bucket' => 'examplebucket-125000000', // Format: BucketName-APPID
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
    // Request succeeded    print_r($result);
} catch (\Exception $e) {    // Request failed
    echo "$e\n";
}
```

#### Parameter Descriptions
| Parameter Name | Type | Description | Required |
| -------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Source bucket name in the format of BucketName-APPID | Yes |
| Role | String | 	Initiator ID in the format of qcs::cam::uin/:uin/ | Yes |
| Rules | Array | 	Sets the corresponding rule, including ID, Status, Prefix, and Destination | Yes |
| ID | String |		 Sets the rule ID | Yes  |
| Status | String |	 Sets whether a rule is enabled; value range: Enabled, Disabled | Yes |
| Prefix | String |	 Sets the prefix matching rule of the rule. If this parameter empty, the rule is applicable to all objects in the bucket | Yes |
| Destination | String | Describes the destination resource, including Bucket and StorageClass | Yes |
| Bucket | String | 	Sets the destination bucket for the cross-region replication in the format of qcs::cos:[region]::[BucketName-APPID] | Yes |
| StorageClass | String |	 Sets the storage class of the destination file. Value range: STANDARD, STANDARD_IA | No |



### Querying Cross-region Replication

#### Feature Description

This API (GET Bucket replication) is used to query the cross-region replication rule of the specified bucket.

#### Method Prototype
```
public Guzzle\Service\Resource\Model getBucketReplication(array $args = array());
```

#### Sample Request
```
try {
    $result = $cosClient->getBucketReplication(array(
        'Bucket' => 'examplebucket-125000000', // Format: BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter Descriptions

| Parameter Name | Type | Description | Required |
| -------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |

#### Return Result Example
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


#### Return Result Descriptions

| Parameter name | Type | Description | Parent Node |
| -------------- | -------- | ---------------------------------- | ------------- |
| Role | String | 	Initiator ID in the format of qcs::cam::uin/:uin/ | None |
| Rules | Array | 	Sets the corresponding rule, including ID, Status, Prefix, and Destination | None |
| Rule | Array | 	Sets the corresponding rule, including ID, Status, Prefix, and Destination | Rules |
| ID | String |		 Sets the rule ID | Rule |
| Status | String |	 Sets whether a rule is enabled; value range: Enabled, Disabled | Rule |
| Prefix | String |	 Sets the prefix matching rule of the rule. If this parameter empty, the rule is applicable to all objects in the bucket | Rule |
| Destination | String | Describes the destination resource, including Bucket and StorageClass | Rule |
| Bucket | String | 	Sets the destination bucket for the cross-region replication in the format of qcs::cos:[region]::[BucketName-APPID] | Destination |
| StorageClass | String |	 Sets the storage class of the destination file. Value range: STANDARD, STANDARD_IA | Destination |


### Deleting Cross-region Replication

#### Feature Description

This API (DELETE Bucket replication) is used to delete the cross-region replication rule of the specified bucket.

#### Method Prototype
```
public Guzzle\Service\Resource\Model deleteBucketReplication(array $args = array());
```

#### Sample Request
```
try {
    $result = $cosClient->deleteBucketReplication(array(
        'Bucket' => 'examplebucket-125000000', // Format: BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter Descriptions
| Parameter Name | Type | Description | Required |
| -------------- | -------- | ---------------------------------- | ------------- |
| Bucket | String | Bucket name in the format of BucketName-APPID | Yes |

