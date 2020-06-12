## Overview

This document provides an overview of APIs and SDK code samples related to COS inventory.

| API | Operation Name | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | Creating an inventory job | Creates an inventory job for a bucket |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | Querying inventory jobs | Queries inventory jobs of a bucket |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | Deleting inventory jobs | Deletes inventory jobs from a bucket |


## Creating an Inventory Job

#### Feature

This API (PUT Bucket inventory) is used to create an inventory job for a bucket. For more information, see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622).

>
> - Up to 1,000 inventory jobs can be created in one COS bucket.
> - You must write a bucket policy to the destination bucket for COS to put the result file of the inventory job in it.
> - To call this API, make sure that you have adequate permission for the bucket's inventory jobs, which is granted to the bucket owner by default. If you do not have such permission, apply for it to the bucket owner first. 


#### Request samples

Sample 1. Create an inventory job with server-side encryption.

```js
cos.putBucketInventory({
    Bucket: 'sourcebucket-1250000000',  /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Id: 'inventory_test',               /* Required */
    InventoryConfiguration: {
        Id: 'inventory_test',
        IsEnabled: 'true',
        Destination: {
            COSBucketDestination: {
                Format: 'CSV',
                AccountId: '100000000001',
                Bucket: 'qcs::cos:ap-beijing::targetbucket-1250000000',
                Prefix: 'inventory_test_prefix',
                Encryption: {
                    SSECOS: ''
                }
            }
        },
        Schedule: {
            Frequency: 'Daily'
        },
        Filter: {
            Prefix: 'filter_prefix'
        },
        IncludedObjectVersions: 'All',
        OptionalFields: [
            'Size',
            'LastModifiedDate',
            'StorageClass',
            'ETag'
        ]
    }
}, function(err, data) {
    console.log(err || data);
});
```

Sample 2. Create an inventory job without server-side encryption.

```js
cos.putBucketInventory({
    Bucket: 'sourcebucket-1250000000',  /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Id: 'inventory_test',       /* Required */
    InventoryConfiguration: {
        Id: 'inventory_test',
        IsEnabled: 'true',
        Destination: {
            COSBucketDestination: {
                Format: 'CSV',
                AccountId: '100000000001',
                Bucket: 'qcs::cos:ap-beijing::targetbucket-1250000000',
                Prefix: 'inventory_test_prefix'
            }
        },
        Schedule: {
            Frequency: 'Daily'
        },
        Filter: {
            Prefix: 'filter_prefix'
        },
        IncludedObjectVersions: 'All',
        OptionalFields: [
            'Size',
            'LastModifiedDate',
            'StorageClass',
            'ETag'
        ]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Name of the bucket for which the inventory job is configured in the format `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Id | ID of the inventory job.<br>Default: None<br>Valid characters: `a-z，A-Z，0-9，-，_，.`                               | String      | Yes   |
| InventoryConfiguration | Contains inventory configuration parameters                               | Object      | Yes   |
| - Id | ID of the inventory job.<br>Default: None<br>Valid characters: `a-z，A-Z，0-9，-，_，.`                               | String      | Yes   |
| - IsEnabled             | Indicates whether inventory is enabled. `true` indicates it is enabled; `false` indicates no inventory list to be generated.                                           | String      | Yes   |
| - IncludedObjectVersions | Indicates whether to include object versions in the inventory<br>If this is set to `All`, the inventory will include all object versions and additional fields `VersionId`, `IsLatest`, and `DeleteMarker`.<br>If this is set to `Current`, no object versions will be included in the inventory. | String | Yes |
| - Filter             | Filters objects to be inventoried with the prefix specified in this field                                           | Object      | No   |
| - - Prefix | Prefix of the objects to be inventoried | String | No |
| - OptionalFields | Optional fields that are included in the inventory results, including Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, and ReplicationStatus | Array | No |
| - Schedule             | Schedule for the inventory job                                           | Object      | Yes   |
| - - Frequency             | Frequency of the inventory job. Enumerated values: Daily, Weekly                                           | String      | Yes   |
| - Destination             | Destination that stores the inventory results                                           | Object      | Yes   |
| - - COSBucketDestination             | Destination bucket that stores the exported inventory results                                           | Object      | Yes   |
| - - - Bucket             | Name of the bucket that stores the inventory results                                           | String      | Yes   |
| - - - AccountId             | ID of the bucket owner, e.g. 100000000001                                           | String      | No   |
| - - - Prefix             | The prefix for shipping inventory reports. COS automatically adds a '/' after the prefix you specify. For example, if you specify 'Prefix' as the prefix, COS will ship inventory reports to the path 'Prefix/inventory_report'.                                           | String      | No   |
| - - - Format             | Format of the inventory results. Value: CSV                                           | String      | Yes   |
| - - - Encryption             | The option of server-side encryption for inventory results                                           | Object      | No   |
| - - - - SSECOS             | Encryption with COS-managed key. Left empty.                                           | String      | No   |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

## Querying Inventory Jobs

#### Feature

This API (GET Bucket inventory) is used to query the inventory jobs for a bucket. To initiate this request, you need to provide the inventory job ID, and a request signature that indicates that the request has been permitted. For more information, see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622).

>
> - To call this API, make sure that you have adequate permission for the bucket's inventory jobs.
> The bucket owner has such permission by default. If you do not have the permission, apply for it to the bucket owner first.  

#### Request samples

```js
cos.getBucketInventory({
    Bucket: 'sourcebucket-1250000000',  /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Id: 'inventory_test'                /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample response

```json
{
    "InventoryConfiguration": {
        "Id":"inventory_test",
        "IsEnabled":"true",
        "Destination":{
            "COSBucketDestination": {
                "Format":"CSV",
                "AccountId":"100000000001",
                "Bucket":"qcs::cos:ap-beijing::targetbucket-1250000000",
                "Prefix":"inventory_test_prefix",
                "Encryption": {
                    "SSECOS":""
                }
            }
        },
        "Schedule": {
            "Frequency":"Daily"
        },
        "Filter": {
            "Prefix":"filter_prefix"
        },
        "IncludedObjectVersions":"All",
        "OptionalFields": [
            "Size",
            "LastModifiedDate",
            "StorageClass",
            "ETag"
        ]
    }
    "statusCode": 200,
    "headers": {}
}
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Name of the bucket for which the inventory job is queried in the format `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Id | ID of the inventory job.<br>Default: None<br>Valid characters: `a-z，A-Z，0-9，-，_，.`                               | String      | Yes   |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - InventoryConfiguration | Contains inventory configuration parameters                               | Object      |
| - - Id | ID of the inventory job.<br>Default: None<br>Valid characters: `a-z，A-Z，0-9，-，_，.`                               | String      |
| - - IsEnabled             | Indicates whether inventory is enabled. `true` indicates it is enabled; `false` indicates no inventory list to be generated. |    String      | 
| - - IncludedObjectVersions | Indicates whether to include object versions in the inventory<br>If this is set to `All`, the inventory will include all object versions and additional fields `VersionId`, `IsLatest`, and `DeleteMarker`.<br>If this is set to `Current`, no object versions will be included in the inventory. | String |
| - - Filter             | Filters objects to be inventoried with the prefix specified in this field                                           | Object      |
| - - - Prefix | Prefix of the objects to be inventoried | String |
| - - OptionalFields | Optional fields that are included in the inventory results, including Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, and ReplicationStatus | Array |
| - - Schedule             | Schedule for the inventory job                                           | Object      | 
| - - - Frequency             | Frequency of the inventory job. Enumerated values: Daily, Weekly                                           | String      |
| - - Destination             | Destination that stores the inventory results                                           | Object      |
| - - - COSBucketDestination             | Destination bucket that stores the exported inventory results                                           | Object      |
| - - - - Bucket             | Name of the bucket that stores the inventory results                                           | String      |
| - - - - AccountId             | ID of the bucket owner, e.g. 100000000001                                           | String      |
| - - - - Prefix             | The prefix for shipping inventory reports. COS automatically adds a '/' after the prefix you specify. For example, if you specify 'Prefix' as the prefix, COS will ship inventory reports to the path 'Prefix/inventory_report'.                                           | String      |
| - - - - Format             | Format of the inventory results. Value: CSV                                           | String      |
| - - - - Encryption             | The option of server-side encryption for inventory results                                           | Object      |
| - - - - - SSECOS             | Encryption with COS-managed key. Left empty.                                           | String      |

## Deleting Inventory Jobs

#### Feature

This API (DELETE Bucket inventory) is used to delete an inventory job from a bucket with the inventory job ID you specify.
For more information, please see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622).

>
> - To call this API, make sure that you have adequate permission for the bucket's inventory jobs, which is granted to the bucket owner by default.
> - The bucket owner has such permission by default. If you do not have the permission, apply for it to the bucket owner first.

#### Request samples

```js
cos.deleteBucketInventory({
    Bucket: 'sourcebucket-1250000000',  /* Required */
    Region: 'ap-beijing',                                  /* Required */
    Id: 'inventory_test'                /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Name of the bucket from which the inventory job is deleted in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Id | ID of the inventory job. Default: None<br/>Valid characters: `a-z，A-Z，0-9，-，_，.`                               | String      | Yes   |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
