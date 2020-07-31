

## Overview

This document provides an overview of APIs and SDK code samples related to inventory.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | -------------------- |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | Setting an inventory job | Sets an inventory job in a bucket |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | Querying inventory jobs | Queries inventory jobs for a bucket |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | Deleting an inventory job | Deletes an inventory job of a bucket |

## Setting Inventory Job

#### Feature description

This API (PUT Bucket inventory) is used to create an inventory job in a bucket.

#### Method prototype

```
put_bucket_inventory(Bucket, Id, InventoryConfiguration={}, **kwargs)
```

#### Sample request

```python
response = client.put_bucket_inventory(
    Bucket='examplebucket-1250000000'',
    Id='string',
    InventoryConfiguration={
        'Destination': {
            'COSBucketDestination': {
                'AccountId': '100000000001',
                'Bucket': 'qcs::cos:ap-guangzhou::examplebucket-1250000000',
                'Format': 'CSV',
                'Prefix': 'string',
                'Encryption': {
                    'SSECOS': {}
                }
            }
        },
        'IsEnabled': 'true'|'false',
        'Filter': {
            'Prefix': 'string'
        },
        'IncludedObjectVersions':'All'|'Current',
        'OptionalFields': {
            'Field': [
                'Size',
                'LastModifiedDate',
                'ETag',
                'StorageClass',
                'IsMultipartUploaded',
                'ReplicationStatus'
            ]
        },
        'Schedule': {
            'Frequency': 'Daily'|'Weekly'
        }
    }
)
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket  | Bucket for which to set an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String | Yes |
| Id       | Inventory job name. Valid characters: a-z, A-Z, 0-9, -, _, .             | String | Yes |
| Destination            | Inventory job delivery destination information                                      | Dict   | Yes       |
| COSBucketDestination   | Destination bucket information for inventory job result delivery                             | Dict   | Yes       |
| AccountId              | Destination bucket account information                                         | String | No |
| Bucket                 | Destination bucket name                                             | String | Yes       |
| Format                 | File format of the inventory result. Valid value: CSV | String | Yes |
| Prefix                 | Delivery path prefix in the destination bucket                                     | String | No       |
| Encryption             | Encryption information for file delivery to the destination bucket. Valid value: SSECOS                  | Dict   | No       |
| IsEnabled              | Inventory job status flag. Valid values: true, false                   | String | Yes       |
| Filter                 | Filter for inventory analysis objects                                       | Dict   | No       |
| Prefix                 | Filter prefix for inventory analysis objects                                       | String | No       |
| IncludedObjectVersions | Versioning information inclusion status. Valid values: All, Current                        | String | Yes       |
| OptionalFields         | Optional inventory fields                                               | Dict   | No       |
| Field                  | Field name. Valid values: Size, LastModifiedDate, ETag, StorageClass, IsMultipartUploaded, ReplicationStatus | List   | No       |
| Schedule               | Inventory job execution schedule                                           | Dict   | Yes       |
| Frequency              | Inventory job execution frequency. Valid values: Daily, Weekly                     | String | Yes       |

#### Returned result description

The returned value of this method is None.

#### Error code description

Some frequent special errors that may occur with this request are listed below:

| Error code | Description | Status code |
| --------------------- | -------------------------------------------- | -------------------- |
| InvalidArgument | Invalid parameter value | HTTP 400 Bad Request |
| TooManyConfigurations | The number of inventories has reached the upper limit of 1,000 | HTTP 400 Bad Request |
| AccessDenied          | Unauthorized access. You probably do not have access to the bucket. | HTTP 403 Forbidden |

## Querying Inventory Job

#### Feature description

This API (GET Bucket inventory) is used to query the inventory job information in a bucket.

#### Method prototype

```
get_bucket_inventory(Bucket, Id, **kwargs)
```

#### Sample request

```
response = client.get_bucket_inventory(
    Bucket='examplebucket-1250000000',
    Id='string'
)
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket  | Bucket for which to query an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String | Yes |
| Id       | Inventory job name. Valid characters: a-z, A-Z, 0-9, -, _, .             | String | Yes |

#### Returned result description

Inventory job configuration of the bucket in dict type.

```
{
    'Id': 'string',
    'Destination': {
        'COSBucketDestination': {
            'AccountId': '100000000001',
            'Bucket': 'qcs::cos:ap-guangzhou::examplebucket-1250000000',
            'Format': 'CSV',
            'Prefix': 'string',
            'Encryption': {
                'SSECOS': {}
            }
        }
    },
    'IsEnabled': 'true'|'false',
    'Filter': {
        'Prefix': 'string'
    },
    'IncludedObjectVersions':'All'|'Current',
    'OptionalFields': {
        'Field': [
            'Size',
            'LastModifiedDate',
            'ETag',
            'StorageClass',
            'IsMultipartUploaded',
            'ReplicationStatus'
        ]
    },
    'Schedule': {
        'Frequency': 'Daily'|'Weekly'
    }
}
```

| Parameter Name | Description | Type |
| ---------------------- | ------------------------------------------------------------ | ------ |
| Id       | Inventory job name. Valid characters: a-z, A-Z, 0-9, -, _, .             | String |
| Destination            | Inventory job delivery destination information                                      | Dict   |
| COSBucketDestination   | Destination bucket information for inventory job result delivery                             | Dict   |
| AccountId              | Destination bucket account information                                         | String |
| Bucket                 | Destination bucket name                                             | String |
| Format                 | File format of the inventory result. Valid value: CSV | String |
| Prefix                 | Delivery path prefix in the destination bucket                                     | String |
| Encryption             | Encryption information for file delivery to the destination bucket. Valid value: SSECOS                  | Dict   |
| IsEnabled              | Inventory job status flag. Valid values: true, false                   | String |
| Filter                 | Filter for inventory analysis objects                                       | Dict   |
| Prefix                 | Filter prefix for inventory analysis objects                                       | String |
| IncludedObjectVersions | Versioning information inclusion status. Valid values: All, Current                        | String |
| OptionalFields         | Optional inventory fields                                               | Dict   |
| Field                  | Field name. Valid values: Size, LastModifiedDate, ETag, StorageClass, IsMultipartUploaded, ReplicationStatus | List   |
| Schedule               | Inventory job execution schedule                                           | Dict   |
| Frequency              | Inventory job execution frequency. Valid values: Daily, Weekly                     | String |

## Deleting Inventory Job

#### Feature description

This API (DELETE Bucket inventory) is used to delete a specified inventory job of a bucket.

#### Method prototype

```
delete_bucket_inventory(Bucket, Id, **kwargs)
```

#### Sample request

```
response = client.delete_bucket_inventory(
    Bucket='examplebucket-1250000000',
    Id='string'
)
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket   | Bucket for which to delete an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String | Yes |
| Id       | Inventory job name. Valid characters: a-z, A-Z, 0-9, -, _, .             | String | Yes |

#### Returned result description

The returned value of this method is None.
