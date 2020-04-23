## Overview

This document provides an overview of APIs and SDK sample codes related to the basic operations and the access control list (ACL) for a bucket.

**Basic operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | Querying a bucket list | Queries the list of all buckets under the specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under the specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permission | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under the specified account |

**ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | --------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL for a specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL of a bucket |

## Basic Operations

### Querying a bucket list

#### Feature

This API (GET Service) is used to query the list of all buckets in a account.

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
| Buckets   | Storage List  | Dict |
| Bucket   | Storage list | List |
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
#### Request sample for all parameters

```python
response = client.create_bucket(
    Bucket='examplebucket-1250000000',
    ACL='private'|'public-read'|'public-read-write',
    GrantFullControl='string',
    GrantRead='string',
    GrantWrite='string'    
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

This API (HEAD Bucket) is used to verify whether a bucket exists and whether you have the permission to access it.

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
| Bucket | The name of a bucket to query, must be in the format: BucketName-APPID | String | Yes |

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
| Bucket | The name of a bucket to delete, must be in the format: BucketName-APPID | String | Yes |

#### Response
This method returns None.


## ACL

### Setting bucket ACL

#### Feature

The API (PUT Bucket acl) is used to set the ACL for a specified bucket. The `AccessControlPolicy` parameter and other permission parameters are mutually exclusive and cannot be specified at the same time.

#### Method prototype

```
put_bucket_acl(Bucket, AccessControlPolicy={}, **kwargs)
```
#### Request samples

[//]: # (.cssg-snippet-put-bucket-acl)
```python
response = client.put_bucket_acl(
    Bucket='examplebucket-1250000000',
    ACL='public-read'
)
```
#### Request sample for all parameters

```python
response = client.put_bucket_acl(
    Bucket='examplebucket-1250000000',
    ACL='private'|'public-read'|'public-read-write',
    GrantFullControl='string',
    GrantRead='string',
    GrantWrite='string',
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
| Bucket | Bucket name in the format: BucketName-APPID | String | Yes |
| ACL | Sets the bucket ACL, such as 'private', 'public-read', 'public-read-write' | String | No |
| GrantFullControl | Grants a specified account full Read/Write permission for a bucket in the format of `id="OwnerUin"`| String | No |
|GrantRead | Grants a specified account Read permission for a bucket in the format of `id="OwnerUin"`| String | No |
| GrantWrite| Grants a specified account Write permission for a bucket in the format of `id="OwnerUin"`| String | No |
| AccessControlPolicy | Grants a specified account permission to access a bucket. For the specific format, see the response for `GET Bucket acl` | Dict | No |

#### Response
This method returns None.

### Querying bucket ACL

#### Feature

This API (GET Bucket ACL) is used to query the ACL of a specified bucket.

#### Method prototype

```
get_bucket_acl(Bucket, **kwargs)
```
#### Request samples

[//]: # (.cssg-snippet-get-bucket-acl)
```python
response = client.get_bucket_acl(
    Bucket='examplebucket-1250000000'
)
```
#### Parameter description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format: BucketName-APPID | String | Yes |


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
| Owner | Information on the bucket owner, including `DisplayName` and `ID` | Dict |
| Grant | Information on the user to which a bucket permission is granted, including `Grantee` and `Permission` | List |
| Grantee | Information on the grantee, including `DisplayName`, `Type`, `ID` and `URI` | Dict |
| DisplayName | Name of the grantee | string |
| Type | Grantee type: `CanonicalUser` or `Group` | string |
| ID | ID of the grantee when `Type` is `CanonicalUser` | string |
| URI | URI of the grantee when `Type` is `Group` | String |
| Permission | Bucket permissions granted to the grantee. Valid values: `FULL_CONTROL` (Read/Write permission), `WRITE` (Write permission), and `READ` (Read permission) | string |
