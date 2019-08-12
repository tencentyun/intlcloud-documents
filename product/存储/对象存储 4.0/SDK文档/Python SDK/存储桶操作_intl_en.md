## Overview

This document provides an overview of APIs related to basic bucket operations and access control list (ACL) and corresponding SDK sample code.

**Basic operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | Querying bucket list 	| Queries the list of all buckets under the specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under the specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permission | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under the specified account |

**ACL**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | --------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL for the specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL 	| Queries the ACL of a bucket |

## Basic Operations

### Querying Bucket List

#### Feature Description

This API (GET Service) is used to query the list of all buckets under the specified account.

#### Method Prototype

```
list_buckets()
```

#### Sample Request

```python
response = client.list_buckets()
```

#### Return Result Descriptions

Bucket list in dict type.

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
| Buckets | Bucket list | Dict |
| Bucket | Bucket list | List |
| Name   |  Bucket name  | String |
| Location   |  Bucket region name  | String |
| CreationDate | Bucket creation time | String |
| Owner | Bucket owner information        | Dict |
| DisplayName   |  Bucket owner name  | String |
| ID | Bucket owner ID | String |


### Creating a Bucket

#### Feature Description

This API (PUT Bucket) is used to create a bucket under the specified account.

#### Method Prototype

```
create_bucket(Bucket, **kwargs)
```
#### Sample Request

```python
response = client.create_bucket(
    Bucket='examplebucket-1250000000',
    ACL='private'|'public-read'|'public-read-write',
    GrantFullControl='string',
    GrantRead='string',
    GrantWrite='string'	
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Name of the bucket to be created in the format of BucketName-APPID | String | Yes |
| ACL | Set the bucket ACL such as 'private', 'public-read', and 'public-read-write' | String | No |
| GrantFullControl | Grants the specified account read/write permission to the bucket in the format of `id="[OwnerUin]"` | String | No |
|GrantRead | Grants the specified account read permission to the bucket in the format of `id="[OwnerUin]"` | String | No |
| GrantWrite | Grants the specified account write permission to the bucket in the format of `id="[OwnerUin]"` | String | No |

#### Return Result Descriptions
The return value of this method is None.


### Checking a Bucket and Its Permission

#### Feature Description

This API (HEAD Bucket) is used to check whether a bucket exists and you have permission to access it.

#### Method Prototype

```
head_bucket(Bucket)
```
#### Sample Request

```python
response = client.head_bucket(
    Bucket='examplebucket-1250000000'
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Name of the bucket to be queried in the format of BucketName-APPID | String | Yes |

#### Return Result Descriptions
The return value of this method is None.


### Deleting a Bucket

#### Feature Description

This API (DELETE Bucket) is used to delete an empty bucket under the specified account.

#### Method Prototype

```
delete_bucket(Bucket)
```
#### Sample Request

```python
response = client.delete_bucket(
    Bucket='examplebucket-1250000000'
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Name of the bucket to be deleted in the format of BucketName-APPID | String | Yes |

#### Return Result Descriptions
The return value of this method is None.


## ACL

### Setting Bucket ACL

#### Feature Description

This API (PUT Bucket acl) is used to set the access control list (ACL) for the specified bucket.

#### Method Prototype

```
put_bucket_acl(Bucket, AccessControlPolicy={}, **kwargs)
```
#### Sample Request

```python
response = client.put_bucket_acl(
    Bucket='examplebucket-1250000000',
    ACL='private'|'public-read'|'public-read-write',
    GrantFullControl='string',
    GrantRead='string',
    GrantWrite='string',
    AccessControlPolicy={
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
        ],
        'Owner': {
            'DisplayName': 'string',
            'ID': 'string'
        }
    }
)
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes |
| ACL | Set the bucket ACL such as 'private', 'public-read', and 'public-read-write' | String | No |
| GrantFullControl | Grants the specified account read/write permission to the bucket in the format of `id="[OwnerUin]"` | String | No |
|GrantRead | Grants the specified account read permission to the bucket in the format of `id="[OwnerUin]"` | String | No |
| GrantWrite | Grants the specified account write permission to the bucket in the format of `id="[OwnerUin]"` | String | No |
| AccessControlPolicy| Grants the specified account access to the bucket. For detailed format, see the return result descriptions of GET Bucket acl | Dict | No |

#### Return Result Descriptions
The return value of this method is None.

### Querying Bucket ACL

#### Feature Description

This API (GET Bucket acl) is used to query the access control list (ACL) for the specified bucket.

#### Method Prototype

```
get_bucket_acl(Bucket, **kwargs)
```
#### Sample Request

```python
response = client.get_bucket_acl(
    Bucket='examplebucket-1250000000',
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of BucketName-APPID | String | Yes |


#### Return Result Descriptions

Bucket ACL information in dict type.
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
| Owner | Bucket owner information, including DisplayName and ID | Dict |
| Grant | Bucket permission grantee information, including Grantee and Permission  | List |
| Grantee | Permission grantee information, including DisplayName, Type, ID, and URI | Dict |
| DisplayName | Permission grantee name | String |
| Type | Permission grantee type; CanonicalUser or Group | string |
| ID | If Type is CanonicalUser, this parameter corresponds to the ID of the permission grantee | String |
| URI | If Type is Group, this parameter corresponds to the URI of the permission grantee | String |
| Permission | Permission to the bucket owned by the grantee. Value range: FULL_CONTROL (for read/write permission), WRITE (for write permission), READ (for read permission) | String |
