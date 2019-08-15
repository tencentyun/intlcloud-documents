## Overview

This document provides an overview of APIs related to basic bucket operations and access control list (ACL) and corresponding SDK sample code.

**Basic operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets under the specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under the specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permission | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under the specified account |

**ACL**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | --------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL configuration of a bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL configuration of a bucket |

## Basic Operations

### Querying Bucket List

#### Feature Description

This API is used to query the list of all buckets under the specified account.

#### Method Prototype

```java
public List<Bucket> listBuckets() throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

None

#### Return Result Descriptions

- Success: A list of all bucket classes is returned. A bucket class contains information such as bucket member and location.
- Failure: An error (e.g., the bucket does not exist) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
List<Bucket> buckets = cosClient.listBuckets();
for (Bucket bucketElement : buckets) {
    String bucketName = bucketElement.getName();
    String bucketLocation = bucketElement.getLocation();
}
```

### Creating a Bucket

#### Feature Description

This API is used to create a bucket under the specified account. You can create up to 200 buckets in total in all regions under one account. There is no limit on the number of objects in a bucket. Creating a bucket is a low-frequency operation. It is generally recommended to create buckets in the console and create objects in the SDK.

#### Method Prototype

```java
public Bucket createBucket(String  bucketName) throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName  | Bucket name in the format of BucketName-APPID. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Return Result Descriptions

- Success: A bucket class containing bucket  description (bucket name, owner, and creation date).
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String bucketName = "examplebucket-1250000000";
Bucket bucket = cosClient.createBucket(bucketName);
```

### Checking a Bucket and Its Permission

#### Feature Description

This API is used to check whether a bucket exists and you have permission to access it.

#### Method Prototype

```java
public boolean doesBucketExist(String bucketName) 
  throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName  | Bucket name in the format of BucketName-APPID. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Return Result Descriptions

- Success: If it exists, true is returned; otherwise, false is returned.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String bucketName = "examplebucket-1250000000";
boolean bucketExistFlag = cosClient.doesBucketExist(bucketName);
```

### Deleting a Bucket

#### Feature Description

This API is used to delete an empty bucket under the specified account.

#### Method Prototype

```java
public void deleteBucket(String bucketName) throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName  | Bucket name in the format of BucketName-APPID. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Return Result Descriptions

- Success: No return value.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String bucketName = "examplebucket-1250000000";
cosClient.deleteBucket(bucketName);
```

## ACL

### Setting Bucket ACL

#### Feature Description

This API is used to set the access control list (ACL) for the specified bucket. The Set Bucket ACL is an overriding operation that overrides existing permission settings. The ACL can be divided into predefined ACL (CannedAccessControlList) and custom ACL (AccessControlList). When both types of ACLs are set at the same time, the predefined ACL will be ignored and the custom one will prevail.

#### Method Prototype

```java
// Method 1 (setting a custom ACL)
public void setBucketAcl(String bucketName, AccessControlList acl)
  throws CosClientException, CosServiceException;
// Method 2 (setting a predefined ACL)
public void setBucketAcl(String bucketName, CannedAccessControlList acl) throws CosClientException, CosServiceException;
// Method 3 (encapsulating both methods above, i.e., containing two types of ACLs; if set simultaneously, the custom ACL will prevail)
public void setBucketAcl(SetBucketAclRequest setBucketAclRequest) 
  throws CosClientException, CosServiceException;
```

#### Parameter Descriptions

Method 3 covers the parameters of methods 1 and 2 and thus is used here as an example.

| Parameter Name | Description | Type |
| ------------------- | -------------- | ------------------- |
| setBucketAclRequest | Permission setting request class | SetBucketAclRequest |

Request member description:

| Request Member | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ----------------------- |
| bucketName  | Constructor or set method | Bucket name in the format of BucketName-APPID. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| acl | Constructor or set method | Custom ACL | AccessControlList |
| cannedAcl | Constructor or set method | Predefined ACL such as public read, public read/write, and private read | CannedAccessControlList |

| Member Name | Description | Type |
| -------------- | ------------------------------- | -------- |
| List&lt;Grant> | Contains all the information to be authorized | Array |
| owner | Represents the owner of the object or owner | Owner class |

Grant class member description:

| Member Name | Description | Type |
| ---------- | ------------------------------------------ | ---------- |
| Grantee | Grantee's identity | Grantee |
| Permission | Granted permission information (e.g., read, write, and read/write) | Permission |

Owner class member description:

| Member Name | Description | Type |
| ----------- | ------------------------------ | ------ |
| id | Owner ID | String |
| displayname | Owner name (currently the same as ID) | String |

CannedAccessControlList represents a predefined ACL for everyone and is an enumeration class with the following enumerated values:

| Enumerated Value | Description |
| --------------- | ------------------------------------------------ |
| Private | Private read/write (i.e., only the owner can read and write) |
| PublicRead | Public read and private write (i.e, owner can read and write and other users can read) |
| PublicReadWrite | Public read/write (i.e., everyone can read and write) |

#### Return Result Descriptions

- Success: No return value.
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String bucketName = "examplebucket-1250000000";
// Set a custom ACL
AccessControlList acl = new AccessControlList();
Owner owner = new Owner();
owner.setId("qcs::cam::uin/2779643970:uin/2779643970");
acl.setOwner(owner);
String id = "qcs::cam::uin/2779643970:uin/734505014";
UinGrantee uinGrantee = new UinGrantee("qcs::cam::uin/2779643970:uin/734505014");
uinGrantee.setIdentifier(id);
acl.grantPermission(uinGrantee, Permission.FullControl);
cosClient.setBucketAcl(bucketName, acl);

// Set a predefined ACL
// Set private read/write (all newly created buckets are private read/write by default)
cosClient.setBucketAcl(bucketName, CannedAccessControlList.Private);
// Set public read and private write
cosClient.setBucketAcl(bucketName, CannedAccessControlList.PublicRead);
// Set public read/write
cosClient.setBucketAcl(bucketName, CannedAccessControlList.PublicReadWrite);
```

### Querying Bucket ACL

#### Feature Description

This API is used to query the access control list (ACL) for the specified bucket.

#### Method Prototype

```java
public AccessControlList getBucketAcl(String bucketName)
       throws CosClientException, CosServiceException
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | String |

#### Return Result Descriptions

- Success: The ACL of a bucket is returned. 
- Failure: An error (e.g., authentication failed) occurred and a CosClientException or CosServiceException exception was thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample Request

```java
// Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format
String bucketName = "examplebucket-1250000000";
AccessControlList acl = cosClient.getBucketAcl(bucketName);
```
