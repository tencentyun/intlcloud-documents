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
public Guzzle\Service\Resource\Model PutBucketInventory(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-inventory)
```php
try {
    $result = $cosClient->putBucketInventory(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Id' => 'string',
        'Destination' => array(
            'COSBucketDestination'=>array(
                'Format' => 'CSV',
                'AccountId' => '100000000001',
                'Bucket' => 'qcs::cos:ap-chengdu::examplebucket-1250000000',
                'Prefix' => 'string',
            )
        ),      
        'IsEnabled' => 'True',
        'Schedule' => array(
            'Frequency' => 'Daily',
        ),  
        'Filter' => array(
            'Prefix' => 'string',
        ),  
        'IncludedObjectVersions' => 'Current',
        'OptionalFields' => array(
            'Size', 
            'ETag',
        )
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}

```

#### Parameter description

| Parameter Name | Parent Node | Description | Type | Required |
| ---------------------- | -------------------- | ------------------------------------------------------------ | ------------- | -------- |
| Bucket  | None          | Bucket for which to set an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String, Array | Yes |
| Id                     | None                   | Inventory name, corresponding to the ID in the request parameter                           | Array         | Yes       |
| IsEnabled              | None                   | Inventory status flag: <br><li>If this is set to `true`, the inventory is enabled; <br><li>if `false`, no inventories will be generated | String        | Yes       |
| IncludedObjectVersions | None | Whether to include object versions in the inventory <br><li>If this is set to `All`, the inventory will include all object versions and add `VersionId`, `IsLatest`, and `DeleteMarker` fields <br><li>If `Current`, no object version information will be included in the inventory | String | Yes |
| Filter                 | None                   | Filters the objects to be analyzed. The inventory feature will analyze the objects that match the prefix set in `Filter` | Array         | No       |
| Prefix | Filter | Prefix of the objects to be analyzed | String | No |
| OptionalFields         | None                   | Name of the analysis items that can be optionally included in the inventory result. Valid values: Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, ReplicationStatus | Array         | No       |
| Schedule               | None                   | Configures the inventory job frequency                                             | Array         | Yes       |
| Frequency | Schedule | Inventory job frequency. Enumerated values: Daily, Weekly | String | Yes |
| Destination            | None                   | Describes the information of the inventory result storage                                       | Array         | Yes       |
| COSBucketDestination   | Destination          | Information of the bucket where the inventory result is stored after export                               | Array         | Yes       |
| Bucket | COSBucketDestination | Name of the bucket where the inventory result is stored | String | Yes |
| AccountId | COSBucketDestination | Bucket owner UIN such as 100000000001 | String | No |
| Prefix | COSBucketDestination | Prefix of the inventory result | String | No |
| Format | COSBucketDestination | File format of the inventory result. CSV is available | String | Yes |
| Encryption             | COSBucketDestination | Option to provide server-side encryption for the inventory result                               | Array         | No       |
| SSE-COS                | Encryption           | Encryption with COS-managed key. This can be left empty | String        | No       |

For more information on other inventory configuration parameters, please see the API documentation.

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
public Guzzle\Service\Resource\Model GetBucketInventory(array $args = array());

```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-inventory)
```php
try {
    $result = $cosClient->getBucketInvnetory(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Id' => 'string',
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}

```

#### Parameter description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| bucket | Bucket for which to query an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | bucket |
| Id       | Inventory job name. Valid characters: a-z, A-Z, 0-9, -, _, .             | String |

#### Sample return result

```php
GuzzleHttp\Command\Result Object
(
    [Destination] => Array
        (
            [COSBucketDestination] => Array
                (
                    [Format] => CSV
                    [AccountId] => 100000000001
                    [Bucket] => qcs::cos:ap-chengdu::examplebucket-1250000000
                    [Prefix] => String
                )

        )

    [Schedule] => Array
        (
            [Frequency] => Daily
        )

    [OptionalFields] => Array
        (
            [0] => Size
            [1] => ETag
        )

    [IsEnabled] => true
    [Id] => string
    [IncludedObjectVersions] => Current
    [RequestId] => NWRmMzQwMDVfMjNiMjU4NjRfOGQ4MV9iN2Jk****
)
```

#### Returned result description

| Parameter Name | Description | Type |
| ---------------------- | ------------------------------------------------------------ | ------------- |
| Bucket            | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String, Array                                      |
| Id                     | Inventory name, corresponding to the ID in the request parameter                           | Array         |
| IsEnabled              | Inventory status flag: <br><li>If this is set to `True`, the inventory is enabled; <br><li>if `False`, no inventories will be generated | String        |
| IncludedObjectVersions | Whether to include object versions in the inventory <br><li>If this is set to `All`, the inventory will include all object versions and add `VersionId`, `IsLatest`, and `DeleteMarker` fields <br><li>If `Current`, no object version information will be included in the inventory | String |
| Filter                 | Filters the objects to be analyzed. The inventory feature will analyze the objects that match the prefix set in `Filter` | Array         |
| Prefix | Prefix of the objects to be analyzed | String |
| OptionalFields         | Name of the analysis items that can be optionally included in the inventory result. Valid values: Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, ReplicationStatus | Array         |
| Schedule               | Configures the inventory job frequency                                             | Array         |
| Frequency | Inventory job frequency. Enumerated values: Daily, Weekly | String |
| Destination            | Describes the information of the inventory result storage                                       | Array         |
| COSBucketDestination   | Information of the bucket where the inventory result is stored after export                               | Array         |
| Bucket | Name of the bucket where the inventory result is stored | String |
| AccountId | Bucket owner UIN such as 100000000001 | String |
| Prefix | Prefix of the inventory result | String |
| Format | File format of the inventory result | String |
| Encryption             | Option to provide server-side encryption for the inventory result                               | Array         |
| SSE-COS                | Encryption with COS-managed key. This can be left empty | String        |



## Deleting Inventory Job

#### Feature description

This API (DELETE Bucket inventory) is used to delete a specified inventory job of a bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model DeleteBucketInventory(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-inventory)
```php
try {
    $result = $cosClient->deleteBucketInvnetory(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Id' => 'string',
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}

```

#### Parameter description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| bucket            | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                                      |
| Id       | Inventory job name. Valid characters: a-z, A-Z, 0-9, -, _, .             | String |
