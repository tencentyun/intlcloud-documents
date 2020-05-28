## Overview
This document provides an overview of APIs and SDK code samples related to bucket and object access control lists (ACL).


**Bucket ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | --------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL for the specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL of a bucket |

**Object ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for a specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |

## Bucket ACL

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
#### Sample request for all parameters

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
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| ACL | Sets the bucket ACL, such as 'private', 'public-read', 'public-read-write' | String | No |
| GrantFullControl | Grants a specified account full Read/Write permission for a bucket in the format of `id="OwnerUin"`| String | No |
|GrantRead | Grants a specified account Read permission for a bucket in the format of `id="OwnerUin"`| String | No |
| GrantWrite| Grants a specified account Write permission for a bucket in the format of `id="OwnerUin"`| String | No |
| AccessControlPolicy | Grants a specified account permission to access a bucket. For the specific format, see the response for `GET Bucket acl` | Dict | No |

#### Response description
This method returns None.

### Querying bucket ACL

#### Feature

This API (GET Bucket acl) is used to get the ACL of a specified bucket.

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
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |


#### Response description

This response returns bucket ACL information in Dict format.
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
| DisplayName | Name of the grantee | String |
| Type | Type of the grantee: `CanonicalUser` or `Group` | String |
| ID | ID of the grantee when `Type` is `CanonicalUser` | String |
| URI | URI of the grantee when `Type` is `Group` | String |
| Permission | Bucket permissions granted to the grantee. Valid values: `FULL_CONTROL` (Read/Write permission), `WRITE` (Write permission), and `READ` (Read permission) | String |




## Object ACL

### Setting object ACL

#### Feature

The API (PUT Object acl) is used to set the ACL for an object in a bucket. The `AccessControlPolicy` parameter and other permission parameters cannot be specified at the same time.

#### Method prototype

```
put_object_acl(Bucket, Key, AccessControlPolicy={}, **kwargs)
```
#### Request samples

[//]: # (.cssg-snippet-put-object-acl)
```python
response = client.put_object_acl(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    ACL='public-read'
)
```
#### Sample request for all parameters

```python
response = client.put_object_acl(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    ACL='private'|'public-read',
    GrantFullControl='string',
    GrantRead='string',
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
| key | Object key, the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes | 
| ACL | Sets the object ACL, e.g. 'private'，'public-read'|String| No | 
| GrantFullControl | Grants the grantee full permission in the format of `id="OwnerUin"`| String | No |
|GrantRead |Grants the grantee Read access in the format of `id="OwnerUin"` | String | No |
| AccessControlPolicy   | Grants the grantee access to the object. For the format, see the response description of `GET Object acl` | Dict  | No  | 


#### Response description

This method returns None.

### Querying object ACL

#### Feature

The API (GET Object acl) is used to query the ACL of an object.

#### Method prototype

```
get_object_acl(Bucket, Key, **kwargs)
```
#### Request samples

[//]: # (.cssg-snippet-get-object-acl)
```python
response = client.get_object_acl(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```
#### Parameter description

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name. Format: BucketName-APPID | String | Yes |
| key | Object key, the unique identifier of an object in a bucket. For example, if the access domain name of an object is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |


#### Response description

This response returns bucket ACL information in Dict format:
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
 | Grant | Information on the user to which object permission is granted, including `Grantee` and `Permission` | List | 
 | Grantee | Information on the grantee, including `DisplayName`, `Type`, `ID` and `URI` | Dict | 
 | DisplayName | Name of the grantee | String |
 | Type | Type of the grantee: `CanonicalUser` or `Group` | String |
 | ID | ID of the grantee when `Type` is `CanonicalUser` | String | 
 | URI | URI of the grantee when `Type` is `Group` | String | 
 | Permission | Permissions granted to the grantee. Valid values: `FULL_CONTROL` (full access), `WRITE` (Write access), and `READ` (Read access) | String |
