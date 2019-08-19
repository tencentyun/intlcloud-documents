## Overview
This document provides an overview of APIs related to cross-origin access, lifecycle, versioning, and cross-region replication and corresponding SDK sample code.

**Cross-origin access**

| API | Operation Name | Operation Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets the cross-origin access permission of a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration information of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration information of a bucket |

**Lifecycle**

| API | Operation Name | Operation Description |
| ------------------- | ------------ | ------------------ |
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

```
put_bucket_cors(Bucket, CORSConfiguration={}, **kwargs)
```
#### Sample Request

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
#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes |
| CORSRule | Sets the corresponding cross-origin access rule, including MaxAgeSeconds, AllowedOrigin, AllowedMethod, AllowedHeader, and ExposeHeader | List | Yes |
| ID | Sets the rule ID | String | No |
| MaxAgeSeconds | Sets the validity period of the result of the OPTIONS request | Int | No |
| AllowedOrigin | Sets the allowed origin such as `"http://intl.cloud.tencent.com"`. Wildcard `*` is supported | Dict | Yes |
| AllowedMethod | Sets the allowed method such as GET, PUT, HEAD, POST, and DELETE | Dict | Yes |
| AllowedHeader | Sets the custom HTTP request headers that can be used for the request. Wildcard `*` is supported | Dict | No |
| ExposeHeader | Sets custom header information from the server that the browser can receive | Dict | No |

#### Return Result Descriptions
The return value of this method is None.

### Querying Cross-origin Access Configuration

#### Feature Description

This API (GET Bucket cors) is used to query the cross-origin access configuration information of the specified bucket.

#### Method Prototype

```
get_bucket_cors(Bucket, **kwargs)
```
#### Sample Request

```python
response = client.get_bucket_cors(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes |

#### Return Result Descriptions

Cross-origin access configuration of the bucket in dict type.
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
| MaxAgeSeconds | Validity period of the result of the OPTIONS request | String |
| AllowedOrigin | Allowed origin such as `"http://intl.cloud.tencent.com"`. Wildcard `*` is supported | Dict |
| AllowedMethod | Allowed method such as GET, PUT, HEAD, POST, and DELETE | Dict |
| AllowedHeader | Custom HTTP request headers that can be used for the request. Wildcard `*` is supported | Dict |
| ExposeHeader | Custom header information from the server that the browser can receive | Dict |


### Deleting Cross-origin Access Configuration

#### Feature Description

This API (DELETE Bucket cors) is used to delete the cross-origin access configuration of the specified bucket.

#### Method Prototype

```
delete_bucket_cors(Bucket, **kwargs)
```
#### Sample Request

```python
response = client.delete_bucket_cors(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes |

#### Return Result Descriptions

The return value of this method is None.


## Lifecycle
### Setting Lifecycle

#### Feature Description

This API (PUT Bucket lifecycle) is used to set the lifecycle configuration information of the specified bucket.

#### Method Prototype

```
put_bucket_lifecycle(Bucket, LifecycleConfiguration={}, **kwargs)
```
#### Sample Request

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
#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes |
| Rule | Sets the corresponding rule, including ID, Filter, Status, Expiration, Transition, NoncurrentVersionExpiration, NoncurrentVersionTransition, and AbortIncompleteMultipartUpload | List | Yes |
| ID | Sets the rule ID | String | No |
| Filter | Describes the set of objects subject to the rule. If you want to set for all objects in the bucket, leave Prefix blank '' | Dict | Yes |
| Status | Sets whether a rule is enabled; value range: Enabled, Disabled | Dict | Yes |
| Expiration | Sets the object expiration rule (either a number of days (Days) or a date (Date) in GMT ISO 8601 format can be specified). It is recommended to specify the date using the get_date method | Dict | No |
| Transition | Sets the object transition rule (either a number of days (Days) or a date (Date) in GMT ISO 8601 format can be specified). It is recommended to specify the date using the get_date method. StorageClass value range: Standard_IA, Archive. Multiple rules can be set at the same time | List | No |
| NoncurrentVersionExpiration | Sets the expiration rule for non-current objects by specifying the number of days (NoncurrentDays) | Dict | No |
| NoncurrentVersionTransition | Sets the transition rule for non-current objects by specifying the number of days (NoncurrentDays). StorageClass value range: Standard_IA. Multiple rules can be set at the same time | List | No |
| AbortIncompleteMultipartUpload | Indicates in how many days a multipart upload has to be completed once started | Dict | No |


#### Return Result Descriptions

The return value of this method is None.


### Querying Lifecycle

#### Feature Description

This API (GET Bucket lifecycle) is used to query the lifecycle of the specified bucket.

#### Sample Request

```python
response = client.get_bucket_lifecycle(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes |

#### Return Result Descriptions

Lifecycle configuration of the bucket in dict type.
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
| Rule | Corresponding rule, including ID, Filter, Status, Expiration, Transition, NoncurrentVersionExpiration, NoncurrentVersionTransition, and AbortIncompleteMultipartUpload | List |
| ID | Rule ID | String |
| Filter | Describes the set of objects subject to the rule | Dict |
| Status | Whether a rule is enabled; value range: Enabled, Disabled | Dict |
| Expiration | Object expiration rule (either a number of days (Days) or a date (Date) can be specified) | Dict |
| Transition | Object transition rule (either a number of days (Days) or a date (Date) can be specified). StorageClass value range: STANDARD_IA, Archive | List |
| NoncurrentVersionExpiration | Expiration rule for non-current objects by specifying the number of days (NoncurrentDays) | Dict |
| NoncurrentVersionTransition | Transition rule for non-current objects by specifying the number of days (NoncurrentDays). StorageClass value range: Standard_IA | List |
| AbortIncompleteMultipartUpload | Indicates in how many days a multipart upload has to be completed once started | Dict |


### Deleting Lifecycle

#### Feature Description

This API (DELETE Bucket lifecycle) is used to delete the lifecycle of the specified bucket.

#### Method Prototype

```
delete_bucket_lifecycle(Bucket, **kwargs)
```
#### Sample Request

```python
response = client.delete_bucket_lifecycle(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes |

#### Return Result Descriptions

The return value of this method is None.


## Versioning
### Setting Versioning

#### Feature Description

This API (PUT Bucket versioning) is used to set the versioning feature of the specified bucket.

#### Method Prototype
```
put_bucket_versioning(Bucket, Status, **kwargs)
```

#### Sample Request

##### Enabling Versioning
```python
response = client.put_bucket_versioning(
    Bucket='examplebucket-1250000000',
    Status='Enabled'
)
```

##### Suspending Versioning
```python
response = client.put_bucket_versioning(
    Bucket='examplebucket-1250000000',
    Status='Suspended'
)
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes |
| Status | Sets the status of bucket versioning. Value range: 'Enabled', 'Suspended' | String | Yes |


#### Return Result Descriptions

The return value of this method is None.

### Querying Versioning

#### Feature Description

This API (GET Bucket versioning) is used to query the versioning information of the specified bucket.

#### Method Prototype

```
get_bucket_versioning(Bucket, **kwargs)
```
#### Sample Request

```python
response = client.get_bucket_versioning(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes |

#### Return Result Descriptions

Versioning configuration of the bucket in dict type.
```python
{
    'Status': 'Enabled'|'Suspended'
}
```

| Parameter Name | Description | Type |
| -------------- | -------------- |---------- |
| Status | Bucket versioning status. Value range: 'Enabled', 'Suspended' | String |


## Cross-region Replication
### Setting Cross-region Replication

#### Feature Description

This API (PUT Bucket replication) is used to set the cross-region replication rule for the specified bucket.

#### Method Prototype

```
put_bucket_replication(Bucket, ReplicationConfiguration={}, **kwargs)
```

#### Sample Request

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
                    'Bucket': 'qcs::cos:ap-shanghai::examplebucket1-1250000000',
                    'StorageClass': 'STANDARD'|'STANDARD_IA'
                }
            },
            {
                'ID': 'string',
                'Status': 'Enabled'|'Disabled',
                'Prefix': 'string',
                'Destination': {
                    'Bucket': 'qcs::cos:ap-guangzhou::examplebucket2-1250000000',
                    'StorageClass': 'STANDARD'|'STANDARD_IA'
                }
            },
        ]   
    }
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Source bucket name in the format of BucketName-APPID | String | Yes |
| Role | Initiator ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` | String | No |
| Rule | Sets the corresponding rule, including ID, Status, Prefix, and Destination | List | Yes |
| ID | Sets the rule ID | String | No |
| Status | Sets whether a rule is enabled; value range: Enabled, Disabled | String | Yes |
| Prefix | Sets the prefix matching rule of the rule. If this parameter empty, the rule is applicable to all objects in the bucket | String | Yes |
| Destination | Describes the destination resource, including Bucket and StorageClass | Dict | Yes |
| Bucket | Sets the destination bucket for the cross-region replication in the format of `qcs::cos:[region]::[BucketName-APPID]` | String | Yes |
| StorageClass | Sets the storage class of the destination file. Value range: STANDARD, STANDARD_IA | String | No |

#### Return Result Descriptions

The return value of this method is None.

### Querying Cross-region Replication

#### Feature Description

This API (GET Bucket replication) is used to query the cross-region replication rule of the specified bucket.

#### Method Prototype

```
get_bucket_replication(Bucket, **kwargs)
```
#### Sample Request

```python
response = client.get_bucket_replication(
    Bucket='examplebucket-1250000000'
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes |

#### Return Result Descriptions

Cross-region replication configuration of the bucket in dict type.
```python
{
    'Role': 'qcs::cam::uin/100000000001:uin/100000000001',
    'Rule': [
        {
            'ID': 'string',
            'Status': 'Enabled'|'Disabled',
            'Prefix': 'string',
            'Destination': {
                'Bucket': 'qcs::cos:ap-shanghai::examplebucket1-1250000000',
                'StorageClass': 'STANDARD'|'STANDARD_IA'
            }
        },
        {
            'ID': 'string',
            'Status': 'Enabled'|'Disabled',
            'Prefix': 'string',
            'Destination': {
                'Bucket': 'qcs::cos:ap-guangzhou::examplebucket2-1250000000',
                'StorageClass': 'STANDARD'|'STANDARD_IA'
            }
        },
    ]  
}
```

| Parameter Name | Description | Type |
| -------------- | -------------- |---------- |
| Role | Initiator ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` | String | No |
| Rule | Rule corresponding to the cross-region replication, including ID, Status, Prefix, and Destination | List | Yes |
| ID | Cross-region replication rule ID | String | No |
| Status | Whether the cross-region replication rule is enabled; value range: Enabled, Disabled | String | Yes |
| Prefix | Prefix matching rule of the cross-region replication rule. If this parameter empty, the rule is applicable to all objects in the bucket | String | Yes |
| Destination | Describes the destination resource, including Bucket and StorageClass | Dict | Yes |
| Bucket | Destination bucket for the cross-region replication in the format of `qcs::cos:[region]::[BucketName-APPID]` | String | Yes |
| StorageClass | Storage class of the destination file. Value range: STANDARD, STANDARD_IA | String | No |


### Deleting Cross-region Replication

#### Feature Description

This API (DELETE Bucket replication) is used to delete the cross-region replication rule of the specified bucket.

#### Method Prototype

```
delete_bucket_replication(Bucket, **kwargs)
```
#### Sample Request

```python
response = client.delete_bucket_replication(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes |

#### Return Result Descriptions

The return value of this method is None.

