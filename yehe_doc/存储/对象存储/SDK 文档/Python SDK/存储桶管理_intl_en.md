## Introduction
This document provides an overview of APIs and SDK code samples related to cross-origin access, lifecycle, versioning, and cross-region replication.

**Cross-origin Access**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket cors](https://cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets cross-origin access permissions for a bucket |
| [GET Bucket cors](https://cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration of a bucket |
| [DELETE Bucket cors](https://cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration information of a bucket |

**Lifecycle**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket lifecycle](https://cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets lifecycle management for a bucket | 
| [GET Bucket lifecycle](https://cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
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

This API (PUT Bucket cors) is used to set the cross-origin access configuration of a bucket.

#### Method Prototype

```
put_bucket_cors(Bucket, CORSConfiguration={}, **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-put-bucket-cors)
```python
response = client.put_bucket_cors(
    Bucket='examplebucket-1250000000',
    CORSConfiguration={
        'CORSRule': [
            {
                'ID': 'string',
                'MaxAgeSeconds': 100,
                'AllowedOrigin': [
                    'string',
                ],
                'AllowedMethod': [
                    'string',
                ],
                'AllowedHeader': [
                    'string',
                ],
                'ExposeHeader': [
                    'string',
                ]
            }
        ]
    },
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| CORSRule | Sets the appropriate cross-origin access rules, including ID, MaxAgeSeconds, AllowedOrigin, AllowedMethod, AllowedHeader, and ExposeHeader | List | Yes |
| ID | Set rule ID | String | No |
| MaxAgeSeconds | Sets the validity period of the results obtained by OPTIONS | int | No |
| AllowedOrigin | Set allowed access sources, e.g. `"http://cloud.tencent.com"`. The wildcard "*" is supported. | Dict | Yes |
| AllowedMethod | Set allowed methods, including GET, PUT, HEAD, POST, DELETE | Dict | Yes |
| AllowedHeader | Set the custom HTTP request headers that are allowed to be used by requests. The wildcard "*" is supported. | Dict | No |
| ExposeHeader | Configure the custom header information that can be received by the browser from the server end. | Dict | No |

#### Returned Result
The returned value for this method is None.

### Querying Cross-origin Access Configuration

#### Feature Description

This API (GET Bucket cors) is used to query the cross-origin access configuration of a bucket.

#### Method Prototype

```
get_bucket_cors(Bucket, **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-get-bucket-cors)
```python
response = client.get_bucket_cors(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |

#### Returned Result

Bucket cross-origin access configuration. Type is dict.
```python
{
    'CORSRule': [
        {
            'ID': 'string',
            'MaxAgeSeconds': 100,
            'AllowedOrigin': [
                'string',
            ],
            'AllowedMethod': [
                'string',
            ],
            'AllowedHeader': [
                'string',
            ],
            'ExposeHeader': [
                'string',
            ],
        }
    ]
}
```

| Parameter Name | Description | Type |
| -------------- | -------------- |---------- |
| CORSRule | Cross-origin access rule, including ID, MaxAgeSeconds, AllowedOrigin, AllowedMethod, AllowedHeader, and ExposeHeader | List |  
| ID | Rule ID | String | 
| MaxAgeSeconds | Sets the validity period of the `OPTIONS` request result | String | 
| AllowedOrigin | Allowed access sources, e.g. `"http://cloud.tencent.com"`. The wildcard "*" is supported. | Dict | 
| AllowedMethod | Allowed methods, including GET, PUT, HEAD, POST, DELETE | Dict |
| AllowedHeader | The custom HTTP request headers that are allowed to be used by requests. The wildcard "*" is supported. | Dict | 
| ExposeHeader | The custom header information that can be received by the browser from the server end. | Dict | 


### Deleting Cross-origin Access Configuration

#### Feature Description

This API (DELETE Bucket cors) is used to delete the cross-origin access configuration of a bucket.

#### Method Prototype

```
delete_bucket_cors(Bucket, **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-delete-bucket-cors)
```python
response = client.delete_bucket_cors(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |

#### Returned Result

The returned value for this method is None.


## Lifecycle
### Setting Lifecycle

#### Feature Description

This API (Put Bucket LifeCycle) is used to set the lifecycle configuration of a bucket.

#### Method Prototype

```
put_bucket_lifecycle(Bucket, LifecycleConfiguration={}, **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-put-bucket-lifecycle)
```python
from qcloud_cos import get_date
response = client.put_bucket_lifecycle(
    Bucket='examplebucket-1250000000',
    LifecycleConfiguration={
        'Rule': [
            {
                'ID': 'string',
                'Filter': {
                    'Prefix': 'string',
                    'Tag': [
                        {
                            'Key': 'string',
                            'Value': 'string'
                        }
                    ]
                },
                'Status': 'Enabled'|'Disabled',
                'Expiration': {
                    'Days': 100,
                    'Date': get_date(2018, 4, 20)
                },
                'Transition': [
                    {
                        'Days': 100,
                        'Date': get_date(2018, 4, 20),
                        'StorageClass': 'Standard_IA'|'Archive'
                    },
                ],
                'NoncurrentVersionExpiration': {
                    'NoncurrentDays': 100
                },
                'NoncurrentVersionTransition': [
                    {
                        'NoncurrentDays': 100,
                        'StorageClass': 'Standard_IA'
                    },
                ],
                'AbortIncompleteMultipartUpload': {
                    'DaysAfterInitiation': 100
                }
            }
        ]   
    }
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name. Format: BucketName-APPID | String | Yes | 
 | Rule | Sets the corresponding rules, including ID, Filter, Status, Expiration, Transition, NoncurrentVersionExpiration, NoncurrentVersionTransition, AbortIncompleteMultipartUpload | List | Yes |
 | ID | Sets rule ID. | string | No |
 | Filter | Describes a collection of objects that are subject to the rules. To set rules for all objects in the bucket, leave Prefix empty. | Dict | Yes | 
 | Status | Sets whether Rule is enabled. Available values: Enabled or Disabled | Dict | Yes | 
  |  Expiration  | Sets the expiration rule for Object. You can specify the number of days (Days) or a date (Date). The format of Date must be GMT ISO 8601. You can specify the date using get_date method. | Dict | No |
 | Transition | Sets the rule for when an object transitions to a specified storage class. You can specify the number of days (Days) or a specified date (Date). The format of Date must be GMT ISO 8601. You can specify the date using get_date method. Available values for StorageClass: Standard_IA and Archive. Multiple rules can be set at a time. | List | No | 
 | NoncurrentVersionExpiration | Sets the expiration rule for noncurrent object versions. You can specify the number of days (NoncurrentDays). | Dict | No |
 |  NoncurrentVersionTransition  | Sets the transition rule that describes when noncurrent objects transition to another storage class. You can specify the number of days (NoncurrentDays). Available values for StorageClass: Standard_IA. Multiple rules can be set at a time. | List | No | 
 | AbortIncompleteMultipartUpload | Indicates the number of days within which the upload must be completed after the multipart upload starts. | Dict | No | 


#### Returned Result

The returned value for this method is None.


### Querying Lifecycle

#### Feature Description

This API (Put Bucket LifeCycle) is used to set the lifecycle configuration of a bucket.

#### Sample Request

[//]: # (.cssg-snippet-get-bucket-lifecycle)
```python
response = client.get_bucket_lifecycle(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |

#### Returned Result

Bucket lifecycle configuration. Type is dict.
```python
{
    'Rule': [
        {
            'ID': 'string',
            'Filter': {
                'Prefix': 'string',
                'Tag': [
                        {
                            'Key': 'string',
                            'Value': 'string'
                        }
                ]
            },
            'Status': 'string',
            'Expiration': {
                'Days': 100,
                'Date': 'string'
            },
            'Transition': [
                {
                    'Days': 100,
                    'Date': 'string',
                    'StorageClass': 'STANDARD_IA'|'Archive'
                },
            ],
            'NoncurrentVersionExpiration': {
                'NoncurrentDays': 100
            },
            'NoncurrentVersionTransition': [
                {
                    'NoncurrentDays': 100,
                    'StorageClass': 'STANDARD_IA'
                },
            ],
            'AbortIncompleteMultipartUpload': {
                'DaysAfterInitiation': 100
            }
        }
    ]   
}
```

| Parameter Name | Description | Type |
| -------------- | -------------- |---------- | 
| Rule | Corresponding rules, including ID, Filter, Status, Expiration, Transition, NoncurrentVersionExpiration, NoncurrentVersionTransition, AbortIncompleteMultipartUpload | List | 
| ID | Rule ID | String | 
| Filter | Describe a collection of Objects that are subject to the rules. | Dict |
| Status | Whether Rule is enabled. Available values: Enabled or Disabled | Dict |
| Expiration | Expiration rule for Object. You can specify the number of days (Days) or the specified date (Date). | Dict | 
| Transition | Rule for when an object transitions to a specified storage class. You can specify the number of days (Days) or the specified date (Date). Available values for StorageClass: Standard_IA, Archive. | Dict | 
| NoncurrentVersionExpiration | Expiration rule for noncurrent object versions. You can specify the number of days (NoncurrentDays). | Dict |
|  NoncurrentVersionTransition  | Transition rule that describes when noncurrent objects transition to another storage class. You can specify the number of days (NoncurrentDays). Available values for StorageClass: Standard_IA. | List | 
| AbortIncompleteMultipartUpload | Number of days within which the upload must be completed after the multipart upload starts. | Dict |


### Deleting Lifecycle

#### Feature Description

This API (DELETE Bucket lifecycle) is used to delete the lifecycle configuration of a bucket.

#### Method Prototype

```
delete_bucket_lifecycle(Bucket, **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```python
response = client.delete_bucket_lifecycle(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |

#### Returned Result

The returned value for this method is None.


## Versioning
### Setting Versioning

#### Feature Description

This API (Put Bucket versioning) is used to set the versioning information of a bucket.

#### Method Prototype
```
put_bucket_versioning(Bucket, Status, **kwargs)
```

#### Sample Request

##### Enable Versioning
[//]: # (.cssg-snippet-put-bucket-versioning)
```python
response = client.put_bucket_versioning(
    Bucket='examplebucket-1250000000',
    Status='Enabled'
)
```

##### Suspend Versioning
```python
response = client.put_bucket_versioning(
    Bucket='examplebucket-1250000000',
    Status='Suspended'
)
```

#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes | 
| Status | Sets versioning status. Valid values: `Suspended`, `Enabled` | String | Yes |


#### Returned Result

The returned value for this method is None.

### Querying Versioning

#### Feature Description

This API (Get Bucket versioning) is used to get the versioning information of a bucket.

#### Method Prototype

```
get_bucket_versioning(Bucket, **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-get-bucket-versioning)
```python
response = client.get_bucket_versioning(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |

#### Returned Result

Bucket versioning configuration. Type is dict.
```python
{
    'Status': 'Enabled'|'Suspended'
}
```

| Parameter Name | Description | Type |
| -------------- | -------------- |---------- | 
| Status | Versioning status. Valid values: `Suspended`, `Enabled` | String |  


## Cross-region Replication
### Setting Cross-region Replication

#### Feature Description

This API (PUT Bucket replication) is used to set cross-region replication rules for a bucket

#### Method Prototype

```
put_bucket_replication(Bucket, ReplicationConfiguration={}, **kwargs)
```

#### Sample Request

[//]: # (.cssg-snippet-put-bucket-replication)
```python
response = client.put_bucket_replication(
    Bucket='examplebucket-1250000000',
    ReplicationConfiguration={
        'Role': 'qcs::cam::uin/100000000001:uin/100000000001',
        'Rule': [
            {
                'ID': 'string',
                'Status': 'Enabled'|'Disabled',
                'Prefix': 'string',
                'Destination': {
                    'Bucket': 'qcs::cos:ap-beijing::destinationbucket-1250000000',
                    'StorageClass': 'STANDARD'|'STANDARD_IA'
                }
            },
            {
                'ID': 'string',
                'Status': 'Enabled'|'Disabled',
                'Prefix': 'string',
                'Destination': {
                    'Bucket': 'qcs::cos:ap-beijing::destinationbucket2-1250000000',
                    'StorageClass': 'STANDARD'|'STANDARD_IA'
                }
            },
        ]   
    }
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes | 
| Role | Replication initiator identifier：`qcs::cam::uin/<OwnerUin>:uin/<SubUin>`  | string | No |
| Rule | Sets rule ID，Status，Prefix，and Destination | List | Yes |
| ID | Sets rule ID. | string | No |
| Status  | Sets whether the rule is enabled or not. Valid values: `Enabled`, `Disabled` | String| Yes |
| Prefix |  Prefix used to filter objects that are subject to the rule. If it is left empty, it means that the rule applies to all objects in the bucket | String |  Yes |
| Destination |   Describes information on object copies, including `Bucket` and `StorageClass`  | Dict | Yes | 
| Bucket| Sets the destination bucket of the cross-region replication. Format: `qcs::cos:[region]::[BucketName-APPID]`  | String  | Yes |
| StorageClass | Sets the storage class of the object copies. Valid values: `STANDARD`, `STANDARD_IA` | String | No |

#### Returned Result

The returned value for this method is None.

### Querying Cross-region Replication

#### Feature Description

This API (GET Bucket replication) is used to query the cross-region replication rules of a bucket.

#### Method Prototype

```
get_bucket_replication(Bucket, **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-get-bucket-replication)
```python
response = client.get_bucket_replication(
    Bucket='examplebucket-1250000000'
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes | 

#### Returned Result

Bucket cross-region replication configuration. Type is dict.
```python
{
    'Role': 'qcs::cam::uin/100000000001:uin/100000000001',
    'Rule': [
        {
            'ID': 'string',
            'Status': 'Enabled'|'Disabled',
            'Prefix': 'string',
            'Destination': {
                'Bucket': 'qcs::cos:ap-beijing::destinationbucket-1250000000',
                'StorageClass': 'STANDARD'|'STANDARD_IA'
            }
        },
        {
            'ID': 'string',
            'Status': 'Enabled'|'Disabled',
            'Prefix': 'string',
            'Destination': {
                'Bucket': 'qcs::cos:ap-beijing::destinationbucket2-1250000000',
                'StorageClass': 'STANDARD'|'STANDARD_IA'
            }
        },
    ]  
}
```

| Parameter Name | Description | Type |
| -------------- | -------------- |---------- | 
| Role | Replication initiator identifier：`qcs::cam::uin/<OwnerUin>:uin/<SubUin>`  | string | No |
| Rule | Sets rule ID，Status，Prefix，and Destination | List | Yes |
|  ID  |  Cross-region replication rule ID | String |  No |
| Status  | Sets whether the rule is enabled or not. Valid values: `Enabled`, `Disabled` | String| Yes |
| Prefix |  Prefix used to filter objects that are subject to the rule. If it is left empty, it means that the rule applies to all objects in the bucket | String |  Yes |
| Destination |   Describes information on object copies, including `Bucket` and `StorageClass`  | Dict | Yes | 
| Bucket| Sets the destination bucket of the cross-region replication. Format: `qcs::cos:[region]::[BucketName-APPID]`  | String  | Yes |
| StorageClass | Sets the storage class of the object copies. Valid values: `STANDARD`, `STANDARD_IA` | String | No |


## Deleting Cross-region Replication

#### Feature Description

This API (DELETE Bucket replication) is used to delete the cross-region replication rules of a bucket

#### Method Prototype

```
delete_bucket_replication(Bucket, **kwargs)
```
#### Sample Request

[//]: # (.cssg-snippet-delete-bucket-replication)
```python
response = client.delete_bucket_replication(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter Description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |

#### Returned Result

The returned value for this method is None.

