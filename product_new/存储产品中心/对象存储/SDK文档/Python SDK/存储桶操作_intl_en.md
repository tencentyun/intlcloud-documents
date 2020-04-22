## Overview

This document provides an overview of APIs and SDK sample codes related to the basic operations and the access control list (ACL) for a bucket.

**Basic operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets in a specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under a specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permission | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under the specified account |

**ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | --------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL for a specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL of a bucket |

## Basic Operations

### Querying bucket list

#### Feature

This API (GET Service) is used to query the list of all buckets in an account.

#### Method prototype

```
list_buckets()
```

#### Request sample

[//]: # (.cssg-snippet-get-service)
```python
response = client.list_buckets(
)
```

#### Response

Query the list of buckets in Dict format.

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
| Buckets   | Storage list  | Dict |
| Bucket   | Storage list | List |
| Name   |  Bucket name  | String|
| Location   | Bucket region name  | String|                                     
| CreationDate   |  Bucket creation time  | String|
| Owner   |  Bucket owner  | Dict|
| - - - DisplayName | Bucket owner name | String |
| ID   | Bucket owner’s ID | String|


### Creating a bucket

#### Feature

This API (Put Bucket) is used to create a bucket.

#### Method prototype

```
delete_bucket_cors(Bucket, **kwargs)
```
#### Request sample

[//]: # (.cssg-snippet-put-bucket-comp)
```python
response = client.create_bucket(
    Bucket='examplebucket-1250000000'
)
```
#### Request sample for all parameters

```python
response = client.create_bucket(
    Bucket='examplebucket-1250000000',
    //private，public-read，public-read-write
    GrantFullControl='string',
    GrantRead='string',
    'GrantWrite' => 'string',    
)
```
#### Parameter description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| ACL | Set the bucket ACL, such as 'private', 'public-read', 'public-read-write' | String | No |
| GrantFullControl | Grants the grantee full permission in the format of `id="OwnerUin"`| String | No |
|GrantRead | Grants the grantee Read access in the format of `id="OwnerUin"`| String | No |
| GrantWrite| Grants the grantee Write access in the format of `id="OwnerUin"`| String | No |

#### Response
This method returns None.


### Extracting a bucket and its permissions

#### Feature

This API (HEAD Bucket) is used to verify whether a bucket exists and if you have the permission to access it.

#### Method prototype

```
head_bucket(Bucket)
```
#### Request sample

[//]: # (.cssg-snippet-head-bucket)
```python
response = client.create_bucket(
    Bucket='examplebucket-1250000000'
)
```
#### Parameter description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |

#### Response
This method returns None.


### Deleting a bucket

#### Feature

This API (DELETE Bucket) is used to delete the specified empty bucket.

#### Method prototype

```
delete_bucket(Bucket)
```
#### Request sample

[//]: # (.cssg-snippet-delete-bucket)
```python
response = client.delete_bucket_cors(
    Bucket='examplebucket-1250000000'
)
```
#### Parameter description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |

#### Response
This method returns None.


## ACL

### Setting bucket ACL

#### Feature

The API (PUT Object acl) is used to set the ACL for an object in a bucket. The `AccessControlPolicy` parameter and other permission parameters cannot be specified at the same time.

#### Method prototype

```
put_object_acl(Bucket, Key, AccessControlPolicy={}, **kwargs)
```
#### Request sample

[//]: # (.cssg-snippet-put-bucket-acl)
```python
response = client.put_bucket_cors(
    Bucket='examplebucket-1250000000',
    {"acl": "public-read" },
)
```
#### Request sample for all parameters

```python
response = client.put_bucket_cors(
    Bucket='examplebucket-1250000000',
    //private，public-read，public-read-write
    GrantFullControl='string',
    GrantRead='string',
    'GrantWrite' => 'string',
    AccessControlPolicy={
        'AccessControlList': {
            'Grant': [
                {
                    'Grantee': {
                        'DisplayName': 'string',
                        'Type': 'CanonicalUser'|'Group',
                        'ID': 'string',
                        'URI': 'string'
                    },
                    'Permission': 'FULL_CONTROL'|'WRITE'|'READ'
                },
            ]
        },
        'Owner': {
            'DisplayName': 'string',
            'ID': 'string'
        }
    }
)
```

#### Parameter description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| ACL | Set the bucket ACL, such as 'private', 'public-read', 'public-read-write' | String | No |
| GrantFullControl | Grants the grantee full permission in the format of `id="OwnerUin"`| String | No |
|GrantRead | Grants the grantee Read access in the format of `id="OwnerUin"`| String | No |
| GrantWrite| Grants the grantee Write access in the format of `id="OwnerUin"`| String | No |
| AccessControlPolicy | Grants the grantee access to the bucket. For the format, see the response description of `GET Bucket acl` | Dict | No |

#### Response
This method returns None.

### Querying bucket ACL

#### Feature

This API (GET Bucket ACL) is used to get the ACL of the specified bucket.

#### Method prototype

```
get_bucket_cors(Bucket, **kwargs)
```
#### Request sample

[//]: # (.cssg-snippet-get-bucket-acl)
```python
response = client.get_bucket_cors(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |


#### Response

This response contains bucket ACL information in Dict format.
```python
{
    'Owner': {
        'DisplayName': 'string',
        'ID': 'string'
    },
    'Grant': [
        {
            'Grantee': {
                'DisplayName': 'string',
                'Type': 'CanonicalUser'|'Group',
                'ID': 'string',
                'URI': 'string'
            },
            'Permission': 'FULL_CONTROL'|'WRITE'|'READ'
        },
    ]
}
```

| Parameter Name | Description | Type | 
| -------------- | -------------- |---------- | 
| Owner | Information on the object owner, including `DisplayName` and `ID` | Dict |
| Grant | Information on the user to which a permission is granted, including `Grantee` and `Permission` | List |
| Grantee | Information on the grantee, including `DisplayName`, `Type`, `ID` and `URI` | Dict |
| DisplayName | Name of the grantee | string |
| Type | Type of the grantee: `CanonicalUser` or `Group` | string |
| ID | ID of the grantee when `Type` is `CanonicalUser` | string |
| URI | URI of the grantee when `Type` is `Group` | String |
| Permission | Bucket permissions granted to the grantee. Valid values: `FULL_CONTROL` (full access), `WRITE` (Write access), and `READ` (Read access) | string |
