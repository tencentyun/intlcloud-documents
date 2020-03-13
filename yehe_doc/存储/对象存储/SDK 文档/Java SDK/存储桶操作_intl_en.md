## Introduction

This document provides an overview of APIs and SDK code samples related to basic operations on buckets and bucket access control list (ACL).

**Basic Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://cloud.tencent.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets under the specified account |
| [PUT Bucket](https://cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under the specified account |
| [HEAD Bucket](https://cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permission | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under the specified account |

**ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | --------------------- |
| [PUT Bucket acl](https://cloud.tencent.com/document/product/436/7737) | Sets a bucket ACL | Sets an ACL for a bucket |
| [GET Bucket acl](https://cloud.tencent.com/document/product/436/7733) | Gets the bucket ACL | Gets the ACL of a bucket |

## Basic Operations

### Querying bucket list

#### Feature

This API is used to query the list of all buckets under the specified account.

#### Method Prototype

```java
public List<Bucket> listBuckets() throws CosClientException, CosServiceException;
```

#### Parameter Description

None.

#### Returned Result

-Success: A list of all Bucket classes will be returned. The Bucket class contains information about bucket member, location and more.
-Failure: An error occurs (such as the bucket does not exist), with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-get-service)
```java
List<Bucket> buckets = cosClient.listBuckets();
for (Bucket bucketElement : buckets) {
    String bucketName = bucketElement.getName();
    String bucketLocation = bucketElement.getLocation();
}
```

### Creating a Bucket

#### Feature

This API is used to create a bucket under the specified account. You can create multiple buckets under the same user account. The maximum number is 200 (regardless of region). There is no limit to the number of objects in the bucket. Bucket creation is a low-frequency operation. We recommended you create a bucket in the console and perform object operations in the SDK.

#### Method Prototype

```java
public Bucket createBucket(String  bucketName) throws CosClientException, CosServiceException;
```

#### Parameter Description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket naming rule is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Returned Result

**Successful:** Bucket type, including the description of Bucket (bucket name, owner, and creation date).
-Failure: An error occurs (such as authentication failure), with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-put-bucket)
```java
String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
CreateBucketRequest createBucketRequest = new CreateBucketRequest(bucket);
// Set the bucket permission to PublicRead (public read and private write). Other options include private read/write and public read/write
createBucketRequest.setCannedAcl(CannedAccessControlList.PublicRead);
Bucket bucketResult = cosClient.createBucket(createBucketRequest);
```

### Retrieving information on a bucket and its permission

#### Feature

This API is used to check whether a bucket exists and you have permission to access it.

#### Method Prototype

```java
public boolean doesBucketExist(String bucketName) 
  throws CosClientException, CosServiceException;
```

#### Parameter Description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket naming rule is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Returned Result

- Successful: "true" is returned if the queried bucket exists. Otherwise, "false" is returned.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-head-bucket)
```java
The bucket name entered must be in a format of {name}-{appid}
String bucketName = "examplebucket-1250000000";
boolean bucketExistFlag = cosClient.doesBucketExist(bucketName);
```

### Deleting a bucket

#### Feature

This API is used to delete the empty bucket under the specified account.

#### Method Prototype

```java
public void deleteBucket(String bucketName) throws CosClientException, CosServiceException;
```

#### Parameter Description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket naming rule is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Returned Result

- Successful: No value is returned.
-Failure: An error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-delete-bucket)
```java
The bucket name entered must be in a format of {name}-{appid}
String bucketName = "examplebucket-1250000000";
cosClient.deleteBucket(bucketName);
```

## ACL

### Setting Bucket ACL

#### Feature

This API (PUT Bucket acl) is used to set the access control list (ACL) for a specified bucket. This operation will overwrite existing permission configurations. ACL includes a predefined permission policy (CannedAccessControlList) or a custom permission control (AccessControlList). When two types of permissions are configured at the same time, predefined policies are ignored and custom policies will be used.

#### Method Prototype

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

#### Parameter Description

Parameters in the third method include that in method 1 and 2. Method 3 is used as an example.

| Parameter Name | Description | Type |
| ------------------- | -------------- | ------------------- |
| setBucketAclRequest | Class for requesting permission configuration | SetBucketAclRequest |

Request member description:

| Request Member | Set Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ----------------------- |
| bucketName | Constructor or set method | Bucket naming rule is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| acl | Constructor or set method | Custom permission policy | AccessControlList |
| cannedAcl | Constructor or set method | Predefined policies, such as public read, public read and write, private read | CannedAccessControlList |

| Member Name | Description | Type |
| -------------- | ------------------------------- | -------- |
| List&lt;Grant> | Contains information of all users to be authorized | Array |
| owner | The owner of the Object or Owner | Owner class |

Grant type members description:

| Member Name | Description | Type |
| ---------- | ------------------------------------------ | ---------- |
| grantee | Grantee identity information | Grantee |
| permission | Authorized permission information (such as readable, writable, readable & writable) | Permission |

Owner type member description:

| Member Name | Description | Type |
| ----------- | ------------------------------ | ------ |
| id | Identity information of an owner | String |
| displayname | Owner's name (same as id) | String |

CannedAccessControlList represents a preset policy for everyone. It is an enumeration type with the following enumerated values.

| Enumerated Value | Description |
| --------------- | ------------------------------------------------ |
| Private | Private read and write (only owner can read and write) |
| PublicRead | Public read and private write (owner can read and write, and other users can read) |
| PublicReadWrite | Public read and write (everyone can read and write) |

#### Returned Result

- Successful: No value is returned.
-Failure: An error occurs (such as authentication failure), with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-put-bucket-acl)
```java
The bucket name entered must be in a format of {name}-{appid}
String bucketName = "examplebucket-1250000000";
// Setting a custom ACL
AccessControlList acl = new AccessControlList();
Owner owner = new Owner();
owner.setId("qcs::cam::uin/100000000001:uin/100000000001");
acl.setOwner(owner);
<ID>qcs::cam::uin/100000000002:uin/100000000002</ID>
UinGrantee uinGrantee = new UinGrantee("qcs::cam::uin/2779643970:uin/2779643970");
uinGrantee.setIdentifier(id);
acl.grantPermission(uinGrantee, Permission.FullControl);
cosClient.setBucketAcl(bucketName, acl);

// Setting a predefined ACL
// Setting private read and write (New buckets are configured with private read and write by default)
cosClient.setBucketAcl(bucketName, CannedAccessControlList.Private);
// Setting public read and private write
cosClient.setBucketAcl(bucketName, CannedAccessControlList.PublicRead);
// Setting public read and write
cosClient.setBucketAcl(bucketName, CannedAccessControlList.PublicReadWrite);
```

### Querying bucket ACL

#### Feature

This API is used to query the access control list of the specified bucket.

#### Method Prototype

```java
public AccessControlList getBucketAcl(String bucketName)
       throws CosClientException, CosServiceException
```

#### Parameter Description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Returned Result

- Successful: The ACL of a Bucket is returned. 
-Failure: An error occurs (such as authentication failure), with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/30599).

#### Request Samples

[//]: # (.cssg-snippet-get-bucket-acl)
```java
The bucket name entered must be in a format of {name}-{appid}
String bucketName = "examplebucket-1250000000";
AccessControlList acl = cosClient.getBucketAcl(bucketName);
```
