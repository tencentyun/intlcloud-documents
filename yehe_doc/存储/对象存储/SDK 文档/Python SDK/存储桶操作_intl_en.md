## Overview

This document provides an overview of APIs and SDK code samples related to basic bucket operations.


| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets under the specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under the specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permission | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under the specified account |



### Querying bucket list

#### Feature

This API (GET Service) is used to query the list of all buckets in an account.

#### Method prototype

```
list_buckets()
```

#### Request samples

[//]: # (.cssg-snippet-get-service)
```python
response = client.list_buckets(
)
```

#### Response

Query a bucket list in Dict format.

```python
{
    'Buckets': {
        'Bucket': [
            {
                'Name': 'string',
                'Location': 'string',
                'CreationDate': 'string'
            },
        ],
    },
    'Owner': {
        'DisplayName': 'string',
        'ID': 'string'
    }
}
```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- |
| Buckets   | A buckets list  | Dict |
| Bucket   | A buckets list | List |
| Name   |  Bucket name  | String|
| Location   | Name of bucket region | String|                                     
| CreationDate   |  Time of Bucket creation | String|
| Owner   |  Bucket owner information  | Dict|
| DisplayName | Bucket owner name | String |
| ID   | Bucket owner ID | String|


### Creating a bucket

#### Feature

This API (PUT Bucket) is used to create a bucket under a specified account.

#### Method prototype

```
create_bucket(Bucket, **kwargs)
```
#### Request samples

[//]: # (.cssg-snippet-put-bucket-comp)
```python
response = client.create_bucket(
    Bucket='examplebucket-1250000000'
)
```
#### Sample request for all parameters

```python
response = client.create_bucket(
    Bucket='examplebucket-1250000000',
    ACL='private'|'public-read'|'public-read-write',
    GrantFullControl='string',
    GrantRead='string',
    GrantWrite='string',    
)
```
#### Parameter description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | The name of a bucket to create, must be in the format: BucketName-APPID | String | Yes |
| ACL | Sets the bucket ACL, such as 'private', 'public-read', 'public-read-write' | String | No |
| GrantFullControl | Grants a specified account full Read/Write permission for a bucket in the format of `id="OwnerUin"`| String | No |
|GrantRead | Grants a specified account Read permission for a bucket in the format of `id="OwnerUin"`| String | No |
| GrantWrite| Grants a specified account Write permission for a bucket in the format of `id="OwnerUin"`| String | No |

#### Response
This method returns None.


### Retrieving information on a bucket and its permission

#### Feature

This API (HEAD Bucket) is used to verify whether a bucket exists and if you have the permission to access it.

#### Method prototype

```
head_bucket(Bucket)
```
#### Request samples

[//]: # (.cssg-snippet-head-bucket)
```python
response = client.head_bucket(
    Bucket='examplebucket-1250000000'
)
```
#### Parameter description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | The name of a bucket to query. Format: BucketName-APPID | String | Yes |

#### Response
This method returns None.


### Deleting a bucket

#### Feature

This API (DELETE Bucket) is used to delete an empty bucket under a specified account.

#### Method prototype

```
delete_bucket(Bucket)
```
#### Request samples

[//]: # (.cssg-snippet-delete-bucket)
```python
response = client.delete_bucket(
    Bucket='examplebucket-1250000000'
)
```
#### Parameter description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | The name of a bucket to delete. Format: BucketName-APPID | String | Yes |

#### Response
This method returns None.


