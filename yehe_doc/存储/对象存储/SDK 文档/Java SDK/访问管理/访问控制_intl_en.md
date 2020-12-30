## Overview

This document provides an overview of APIs and SDK code samples related to bucket and object access control lists (ACL).

**Bucket ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | --------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting a bucket ACL | Sets the ACL for a specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying a bucket ACL | Gets the ACL of a specified bucket |

**Object ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting an object ACL | Sets an ACL for a specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying an object ACL | Queries the ACL of an object |

## Bucket ACL
### Setting bucket ACL

#### Feature description

This API (PUT Bucket acl) is used to set the access control list (ACL) for a specified bucket. This operation will overwrite existing permission configurations. ACL includes a predefined permission policy (CannedAccessControlList) or a custom permission control (AccessControlList). When two types of permissions are configured at the same time, predefined policies are ignored and custom policies will be used.

#### Method prototype

```java
// Method 1 (Set custom policy)
public void setBucketAcl(String bucketName, AccessControlList acl)
  throws CosClientException, CosServiceException;
// Method 2 (Set predefined policy)
public void setBucketAcl(String bucketName, CannedAccessControlList acl) throws CosClientException, CosServiceException;
// Method 3 (Encapsulation of the two methods above, including setting of these two policies. If both of them are set, the custom policy prevails.)
public void setBucketAcl(SetBucketAclRequest setBucketAclRequest) 
  throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-acl)
```java
// Enter the bucket name in the format of BucketName-APPID
String bucketName = "examplebucket-1250000000";
// Set a custom ACL
AccessControlList acl = new AccessControlList();
Owner owner = new Owner();
owner.setId("qcs::cam::uin/100000000001:uin/100000000001");
acl.setOwner(owner);
String id = "qcs::cam::uin/2779643970:uin/2779643970";
UinGrantee uinGrantee = new UinGrantee("qcs::cam::uin/2779643970:uin/2779643970");
uinGrantee.setIdentifier(id);
acl.grantPermission(uinGrantee, Permission.FullControl);
cosClient.setBucketAcl(bucketName, acl);

// Set a predefined ACL
// Set private read and write (New buckets are configured with private read and write by default)
cosClient.setBucketAcl(bucketName, CannedAccessControlList.Private);
// Set public read and private write
cosClient.setBucketAcl(bucketName, CannedAccessControlList.PublicRead);
// Set public read/write
cosClient.setBucketAcl(bucketName, CannedAccessControlList.PublicReadWrite);
```


#### Parameter description

Parameters in the third method include that in method 1 and 2. Method 3 is used as an example.

| Parameter | Description | Type |
| ------------------- | -------------- | ------------------- |
| setBucketAclRequest | Class for requesting permission configuration | SetBucketAclRequest |

Request member description:

| Request Member | Set Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ----------------------- |
| bucketName  | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, please see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| acl | Constructor or set method | Custom ACL policy | AccessControlList |
| cannedAcl | Constructor or set method | Predefined ACL policy, such as public read, public read and write, private read | CannedAccessControlList |

| Member Name | Description | Type |
| -------------- | ------------------------------- | -------- |
| List&lt;Grant> | Contains information on all granted permissions | Array |
| owner | Owner of the object | Owner class |

Grant class members:

| Member Name | Description | Type |
| ---------- | ------------------------------------------ | ---------- |
| grantee | Grantee identity information | Grantee |
| permission | Authorized permission information (such as readable, writable, readable & writable) | Permission |

Owner class members:

| Member Name | Description | Type |
| ----------- | ------------------------------ | ------ |
| id | Identifies the owner | String |
| displayname | Owner's name (same as id) | String |

CannedAccessControlList represents a preset policy for everyone. It is an enumeration type with the following enumerated values.

| Enumerated Value | Description |
| --------------- | ------------------------------------------------ |
| Private | Private read and write (only the owner can read and write) |
| PublicRead | Public read and private write (the owner can read and write, other users can read) |
| PublicReadWrite | Public read and write (everyone can read and write) |

#### Response description

- Success: no value is returned.
- Failure: an error (such as authentication failure) occurs, with a `CosClientException` or `CosServiceException` exception thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


### Querying bucket ACL

#### Feature description

This API is used to query the access control list of the specified bucket.

#### Method prototype

```plaintext
public AccessControlList getBucketAcl(String bucketName)
       throws CosClientException, CosServiceException
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-acl)
```java
// Enter the bucket name in the format of BucketName-APPID
String bucketName = "examplebucket-1250000000";
AccessControlList accessControlList = cosClient.getBucketAcl(bucketName);
// Change the ACL policy type to predefined ACL. Valid values: Private, PublicRead, PublicReadWrite
CannedAccessControlList cannedAccessControlList = accessControlList.getCannedAccessControl();
```


#### Parameter description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312#.E5.AD.98.E5.82.A8.E6.A1.B6.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83) | String |

#### Response description

- Success: the ACL of a bucket is returned. 
- Failure: an error (such as authentication failure) occurs, with a `CosClientException` or `CosServiceException` exception thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

## Object ACL


### Setting object ACL

#### Feature description

This API is used to set an ACL for a specified object in a bucket.

> !You can configure up to 1,000 bucket ACLs. Do not set object ACL control unless absolutely necessary. The object inherits bucket permissions by default.

There are two types of ACL policies: predefined ACLs (CannedAccessControlList) and custom ACLs (AccessControlList). If both of them are set, the custom ACL prevails over the predefined ACL.

#### Method prototype

```java
// Method 1 (custom policy)
public void setObjectAcl(String bucketName, String key, AccessControlList acl)
       throws CosClientException, CosServiceException
// Method 2 (predefined policy)
public void setObjectAcl(String bucketName, String key, CannedAccessControlList acl)
       throws CosClientException, CosServiceException
// Method 3 (Encapsulate the two methods above, allowing you to set both policies. In this case, the custom policy prevails.)
public void setObjectAcl(SetObjectAclRequest setObjectAclRequest)
  throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-put-object-acl)
```java
// The grantee information must be formatted. The format for root account and sub-account differs as follows:
// In this example, both root_uin and sub_uin below are valid QQ numbers
// The root account "qcs::cam::uin/<root_uin>:uin/<root_uin>" indicates that permission is granted to the root account "root_uin" itself
// For example, "qcs::cam::uin/2779643970:uin/2779643970"
// The sub-account "qcs::cam::uin/<root_uin>:uin/<sub_uin>" indicates that permission is granted by the root account "root_uin" to the sub account "sub_uin"
// For example, qcs::cam::uin/2779643970:uin/73001122 
// Bucket name in the format of BucketName-APPID
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
// Set a custom ACL
AccessControlList acl = new AccessControlList();
Owner owner = new Owner();
// Set the owner, which can only be a root account
owner.setId("qcs::cam::uin/100000000001:uin/100000000001");
acl.setOwner(owner);

// Grant root account 73410000 read and write permissions
UinGrantee uinGrantee1 = new UinGrantee("qcs::cam::uin/2779643970:uin/2779643970");
acl.grantPermission(uinGrantee1, Permission.FullControl);
cosClient.setObjectAcl(bucketName, key, acl);

// Set a predefined ACL
// Set private read and write (The object inherits bucket permissions by default)
cosClient.setObjectAcl(bucketName, key, CannedAccessControlList.Private);
// Set public read and private write
cosClient.setObjectAcl(bucketName, key, CannedAccessControlList.PublicRead);
// Set public read/write
cosClient.setObjectAcl(bucketName, key, CannedAccessControlList.PublicReadWrite);
```


#### Parameter description

- Parameters for **Method 3** are described below because they encapsulate the parameters used in methods 1 and 2.

| Parameter | Description | Type |
| ------------------- | ------ | ------------------- |
| SetObjectAclRequest | Request class | setObjectAclRequest |

Request member description:

| Request Member | Set Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ----------------------- |
| bucketName  | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312#.E5.AD.98.E5.82.A8.E6.A1.B6.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83) | String |
| key | Constructor or set method | Object key (Key), which is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| acl | Constructor or set method | Custom ACL policy | AccessControlList |
| cannedAcl | Constructor or set method | Predefined ACL policy, such as public read, public read and write, private read | CannedAccessControlList |

| Member Name | Description | Type |
| -------------- | ------------------------------- | -------- |
| List&lt;Grant> | Contains information on all granted permissions | Array |
| owner | Owner of the object | Owner class |

Grant class members:

| Member Name | Description | Type |
| ---------- | -------------------------------------------- | ---------- |
| grantee | Grantee information | Grantee |
| permission | Granted permission (such as read, write, read/write) | Permission |

Owner class members:

| Member Name | Description | Type |
| ----------- | ------------------------------ | ------ |
| id | Identifies the owner | String |
| displayname | Owner's name (same as id) | String |

CannedAccessControlList represents a preset policy for everyone. It is an enumeration type with the following enumerated values.

| Enumerated Value | Description |
| --------------- | ------------------------------------------------ |
| Private | Private read and write (only the owner can read and write) |
| PublicRead | Public read and private write (the owner can read and write, other users can read) |
| PublicReadWrite | Public read and write (everyone can read and write) |

#### Response description

- Success: no value is returned.
- Failure: an error (such as authentication failure) occurs, with a `CosClientException` or `CosServiceException` exception thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Querying object ACL

#### Feature description

This API is used to query the ACL of an object.

#### Method prototype

```java
public AccessControlList getObjectAcl(String bucketName, String key)
  throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-get-object-acl)
```java
// Bucket name in the format of BucketName-APPID
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
AccessControlList accessControlList = cosClient.getObjectAcl(bucketName, key);
// Change the ACL policy type to predefined ACL. Value values: Private, PublicRead, Default
CannedAccessControlList cannedAccessControlList = accessControlList.getCannedAccessControl();
```


#### Parameter description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312#.E5.AD.98.E5.82.A8.E6.A1.B6.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83) | String |
| key | Object key (Key), which is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### Response description

- Success: returns the ACL of the object.
- Failure: an error (such as authentication failure) occurs, with a `CosClientException` or `CosServiceException` exception thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
