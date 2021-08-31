## Overview


This document provides an overview of APIs and SDK code samples related to basic bucket operations.

| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service (List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291) | Querying the bucket list | Queries the list of all buckets under a specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under a specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permissions | Checks whether a bucket exists and whether you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket from a specified account |



## Querying a Bucket List

#### API description

This API is used to query the list of all buckets under a specified account.

#### Method prototype

```java
public List<Bucket> listBuckets() throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-get-service)
```java
// If you only call the “listBuckets” method, set the region to new Region("") when creating cosClient.
List<Bucket> buckets = cosClient.listBuckets();
for (Bucket bucketElement : buckets) {
    String bucketName = bucketElement.getName();
    String bucketLocation = bucketElement.getLocation();
}
```


#### Parameter description

None

#### Response description

- Success: A list of all bucket classes will be returned. The bucket class contains information about bucket members, location, and more.
- Failure: An error (such as the bucket does not exist) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


## Creating a Bucket

#### API description

This API is used to create a bucket under the specified account. You can create multiple buckets under the same user account. The maximum number is 200 (regardless of region). There is no limit to the number of objects in the bucket. Bucket creation is a low-frequency operation. We recommended you create a bucket in the console and perform object operations in the SDK.

#### Method prototype

```java
public Bucket createBucket(String  bucketName) throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket)
```java
String bucket = "examplebucket-1250000000"; // Bucket, formatted as BucketName-APPID
CreateBucketRequest createBucketRequest = new CreateBucketRequest(bucket);
// Set the bucket permission to Private (private read/write). Other options include public read/private write and public read/write.
createBucketRequest.setCannedAcl(CannedAccessControlList.Private);
Bucket bucketResult = cosClient.createBucket(createBucketRequest);
```


#### Parameter description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name, formatted as `BucketName-APPID`. For more information, please see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |

#### Response description

- Success**: the bucket class, including the bucket description (bucket name, owner, and creation date).
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


## Extracting a Bucket and its Permission

#### API description

This API is used to verify whether a bucket exists and whether you have permission to access it.

#### Method prototype

```java
public boolean doesBucketExist(String bucketName) 
  throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-head-bucket)
```java
The bucket name entered must be in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
boolean bucketExistFlag = cosClient.doesBucketExist(bucketName);
```


#### Parameter description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name, formatted as `BucketName-APPID`. For more information, please see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |

#### Response description

- Success: returns `true` if the bucket exists. Otherwise, `false` is returned.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


## Deleting a Bucket

#### API description

This API is used to delete an empty bucket under a specified account.

#### Method prototype

```java
public void deleteBucket(String bucketName) throws CosClientException, CosServiceException;
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket)
```java
The bucket name entered must be in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
cosClient.deleteBucket(bucketName);
```



#### Parameter description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name, formatted as `BucketName-APPID`. For more information, please see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |

#### Response description

- Success: No value is returned.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


