## Overview

This document provides an overview of APIs related to simple object operations, multipart upload, and other operations and corresponding SDK sample code.

**Simple operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/30614) | Querying object list | Queries some or all objects in a bucket |
[PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Simply uploading an object | Upload an object (file/object) to a bucket |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using a form | Uploads an object using format request |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Gets the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object (file/object) to the local file system |
| [Options Object](https://intl.cloud.tencent.com/document/product/436/8288) | Pre-requesting cross-origin configuration | Uses a pre-request to confirm whether a real cross-origin request can be sent |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Setting object replication | Copies a file to the destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes the specified object (file/object) in a bucket |
| [DELETE Multiple Object](https://intl.cloud.tencent.com/document/product/436/8289)	 | Deleting multiple objects	 | Deletes objects (files/objects) in a bucket in batches |


**Multipart upload operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying a multipart upload | Queries the information of a multipart upload in progress |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload operation |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads object parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in the specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Retrieves an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for the specified object (file/object) in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Getting object ACL | Gets the ACL of an object (file/object) |

## Simple Operations

### Querying Object List

#### Feature Description

This API is used to query some or all objects in a bucket.

#### Method Prototype

```java
GetBucketResult getBucket(GetBucketRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketAsync(GetBucketRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID;  
GetBucketRequest getBucketRequest = new GetBucketRequest(bucket);

// Prefix match, used to specify the prefix address of the object returned
getBucketRequest.setPrefix("prefix");

// Maximum number of entries returned at a time; 1,000 by default
getBucketRequest.setMaxKeys(100);

// The delimiter is a symbol. If there is a prefix,
// the identical paths between prefix and delimiter are grouped into one class and defined as a common prefix,
// and then all common prefixes are listed. If there is no prefix, it starts at the beginning of the path
getBucketRequest.setDelimiter('/');

// Use the sync method
try {
    GetBucketResult getBucketResult = cosXmlService.getBucket(getBucketRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.getBucketAsync(getBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Get Bucket success
		GetBucketResult getBucketResult = (GetBucketResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `getBucketRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.

#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | String |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | getBucketAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through GetBucketResult.

| Member Variable | Type | Description |
| ---------- | ------------------------------------------------------------ | --------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
| listBucket | [ListBucket](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/ListBucket.java) | Returns the list information of objects in the bucket |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

### Simply Uploading an Object

#### Feature Description

This API is used to upload an object (file/object) to a bucket.

#### Method Prototype

```java
PutObjectResult putObject(PutObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void putObjectAsync(PutObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key, such as cosPath = "text.txt";
String srcPath = Environment.getExternalStorageDirectory().getPath() + "/exampleobject"; // "Absolute path to the local file"; 
PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);

putObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});

// Use the sync method to upload
try {
    PutObjectResult putObjectResult = cosXmlService.putObject(putObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to upload
cosXmlService.putObjectAsync(putObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Put object success...
		PutObjectResult putObjectResult = (PutObjectResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put object failed because of CosXmlClientException or CosXmlServiceException...
    }
});


// Upload the byte array
String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key, such as cosPath = "text.txt";
byte[] data = "this is a test".getBytes(Charset.forName("UTF-8"));
PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, data);
putObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});
try {
    PutObjectResult putObjectResult = cosXmlService.putObject(putObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}


// Upload the byte stream
String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key, such as cosPath = "text.txt";
InputStream inputStream = new ByteArrayInputStream("this is a test".getBytes(Charset.forName("UTF-8")));
PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, inputStream);
putObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});
try {
    PutObjectResult putObjectResult = cosXmlService.putObject(putObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `putObjectRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.

#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | String |
| cosPath | Constructor or SetCosPath | Position identifier of the object in the bucket, i.e., the [object key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| srcPath | Constructor | Absolute path to a local file to be uploaded to COS | String |
| data | Constructor | Byte array to be uploaded to COS | byte[] |
| inputStream | Constructor | Input stream to be uploaded to COS | InputStream |
| progressCallback | setProgressListener | Sets upload progress callback | CosXmlProgressListener |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | putObjectAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through PutObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
| eTag | String | Returns eTag of the object |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

### Uploading an Object Using a Form

#### Feature Description

This API is used to upload an object using a form request.

#### Method Prototype

```java
PostObjectResult postObject(PostObjectRequest request) throws CosXmlClientException, CosXmlServiceException；

void postObjectAsync(PostObjectRequest request, CosXmlResultListener cosXmlResultListener)；
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key, such as cosPath = "text.txt";
String srcPath = Environment.getExternalStorageDirectory().getPath() + "/exampleobject"; // "Absolute path to the local file"; 

PostObjectRequest postObjectRequest = new PostObjectRequest(bucket, cosPath, srcPath);

postObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});

// Use the sync method to upload
try {
    PostObjectResult postObjectResult = cosXmlService.postObject(postObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to upload
cosXmlService.postObjectAsync(postObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Put object success...
		PutObjectResult putObjectResult = (PutObjectResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | String |
| cosPath | Constructor or SetCosPath | Position identifier of the object in the bucket, i.e., the [object key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| srcPath | Constructor | Absolute path to a local file to be uploaded to COS | String |
| data | Constructor | Byte array to be uploaded to COS | byte[] |
| inputStream | Constructor | Input stream to be uploaded to COS | InputStream |
| progressCallback | setProgressListener | Sets upload progress callback | CosXmlProgressListener |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | postObjectAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through PostObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
| eTag | String | Returns eTag of the object |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

### Querying Object Metadata

#### Feature Description

This API is used to query the metadata of an object.

#### Method Prototype

```java
HeadObjectResult headObject(HeadObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void headObjectAsync(HeadObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key
HeadObjectRequest headObjectRequest = new HeadObjectRequest(bucket, cosPath);

// Use the sync method
try {
    HeadObjectResult headObjectResult = cosXmlService.headObject(headObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.headObjectAsync(headObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Head Bucket success
		HeadObjectResult headObjectResult  = (HeadObjectResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Head Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `headObjectRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.


#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | --------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | String |
| cosPath | Constructor or SetCosPath | Position identifier of the object in the bucket, i.e., the [object key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | headObjectAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through HeadObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
| eTag | String | Returns eTag of the object |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

### Downloading an Object

#### Feature Description

This API (GET Object) is used to download an object (file/object) to the local file system.

#### Method Prototype

```java
GetObjectResult getObject(GetObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void getObjectAsync(GetObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key
String savePath = Environment.getExternalStorageDirectory().getPath(); // Local path

GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath, savePath);
getObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});

// Use the sync method to download
try {
    GetObjectResult getObjectResult =cosXmlService.getObject(getObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.getObjectAsync(getObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Get Object success
		GetObjectResult getObjectResult  = (GetObjectResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `getObjectRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.

#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | String |
| cosPath | Constructor or SetCosPath | Position identifier of the object in the bucket, i.e., the [object key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| LocalDir | Constructor | Absolute path to the local folder for storing the downloaded object | String |
| localFileName | Constructor | Local filename of the downloaded object | String |
| progressCallback | setProgressListener | Sets upload progress callback | CosXmlProgressListener |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | getObjectAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through GetObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
| eTag | String | Returns eTag of the object |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

### Pre-requesting Cross-origin Configuration

#### Feature Description
This API (Options Object) is used to pre-request the cross-origin configuration.

#### Method Prototype

```java
OptionObjectResult optionObject(OptionObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void optionObjectAsync(OptionObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key
String origin = "http://intl.cloud.tencent.com";
String accessMthod = "PUT";
OptionObjectRequest optionObjectRequest = new OptionObjectRequest(bucket, cosPath, origin, accessMthod);

// Use the sync method
try {
   OptionObjectResult result = cosXmlService.optionObject(optionObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request 
cosXmlService.optionObjectAsync(deleteObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo OptionOb Object success...
		OptionObjectResult optionObjectResult  = (OptionObjectResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo OptionOb Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `optionObjectRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.


#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | String |
| cosPath | Constructor or SetCosPath | Position identifier of the object in the bucket, i.e., the [object key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| origin | Constructor or SetOrigin | Origin domain name of the simulated cross-origin access request | String |
| accessMthod | Constructor or SetAccessControlMethod | HTTP method of the simulated cross-origin access request | String |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | optionObjectAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through DeleteObjectResult.

| Member Variable | Type | Description |
| ------------------------------- | -------------- | ---------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
| accessControlAllowHeaders | `List<String>` | Request header allowed for cross-origin access |
| accessControlAllowMethods | `List<String>` | Request HTTP method allowed for cross-origin access |
| accessControlAllowExposeHeaders | `List<String>` | Custom request header allowed for cross-origin access |
| accessControlMaxAge | long | Validity period of the result of the OPTIONS request |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

### Setting Object Replication

This API (PUT Object - Copy) is used to copy a file to the destination path.

#### Method Prototype

```java
CopyObjectResult copyObject(CopyObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void copyObjectAsync(CopyObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String sourceAppid = "1250000000"; // Account's appid
String sourceBucket = "sourcebucket-1250000000"; // Bucket of the source object
String sourceRegion = "ap-beijing"; // Bucket region of the source object
String sourceCosPath = "source-exampleobject"; // Source object key
// Construct the source object attribute
CopyObjectRequest.CopySourceStruct copySourceStruct = new CopyObjectRequest.CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceCosPath);
String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath, copySourceStruct);

// Use the sync method
try {
    CopyObjectResult copyObjectResult = cosXmlService.copyObject(copyObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.copyObjectAsync(copyObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Copy Object success
		CopyObjectResult copyObjectResult  = (CopyObjectResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Copy Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `copyObjectRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.

#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ------------------------ | ------------------------------------------------------------ | -------------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | String |
| cosPath | Constructor | Position identifier of the object in the bucket, i.e., the [object key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| copySourceStruct | Constructor | Description of the source path of the copied data | CopySourceStruct |
| metaDataDirective | setCopyMetaDataDirective | Whether to copy or update the metadata of the source object | MetaDataDirective |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | copyObjectAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through CopyObjectResult.

| Member Variable | Type | Description |
| ---------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
| copyObject | [CopyObject](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/main/java/com/tencent/cos/xml/model/tag/CopyObject.java) | Returns information of the successfully copied object |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.


### Deleting a Single Object

#### Feature Description

This API (DELETE Object) is used to delete the specified object.

#### Method Prototype

```java
DeleteObjectResult deleteObject(DeleteObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteObjectAsync(DeleteObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key

DeleteObjectRequest deleteObjectRequest = new DeleteObjectRequest(bucket, cosPath);

// Use the sync method to delete
try {
    DeleteObjectResult deleteObjectResult = cosXmlService.deleteObject(deleteObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request 
cosXmlService.deleteObjectAsync(deleteObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Delete Object success...
		DeleteObjectResult deleteObjectResult  = (DeleteObjectResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Delete Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `deleteObjectRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.

#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | String |
| cosPath | Constructor or SetCosPath | Position identifier of the object in the bucket, i.e., the [object key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | getBucketLocationAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through DeleteObjectResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

### Deleting Multiple Objects

#### Feature Description

This API (Delete Multi Objects) is used to delete multiple objects.

#### Method Prototype

```java
DeleteMultiObjectResult deleteMultiObject(DeleteMultiObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteMultiObjectAsync(DeleteMultiObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
List<String> objectList = new ArrayList<String>();
objectList.add("/exampleobject");// Position identifier of the object in the bucket, i.e., the object key 

DeleteMultiObjectRequest deleteMultiObjectRequest = new DeleteMultiObjectRequest(bucket, objectList);
deleteMultiObjectRequest.setQuiet(true);

// Use the sync method to delete
try {
     DeleteMultiObjectResult deleteMultiObjectResult =cosXmlService.deleteMultiObject(deleteMultiObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request 
cosXmlService.deleteMultiObjectAsync(deleteMultiObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // Delete Multi Object success...
		DeleteMultiObjectResult deleteMultiObjectResult  = (DeleteMultiObjectResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        //  Delete Multi Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `deleteMultiObjectRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.

#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | String |
| quiet | true: only return information of files that failed to be deleted; false: return the deletion result of each object | Boolean | Yes |
| objectList | List of [object keys](https://intl.cloud.tencent.com/document/product/436/13324) to be deleted | `List<String>` | Yes |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | getBucketLocationAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through DeleteMultiObjectResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.


## Multipart Upload Operations

### Querying a Multipart Upload

#### Feature Description

This API (List Multipart Uploads) is used to query multipart uploads in progress in the specified bucket.

#### Method Prototype

```java
ListMultiUploadsResult listMultiUploads(ListMultiUploadsRequest request) throws CosXmlClientException, CosXmlServiceException;

void listMultiUploadsAsync(ListMultiUploadsRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
ListMultiUploadsRequest listMultiUploadsRequest = new ListMultiUploadsRequest(bucket);
try
{
	// Use the sync method
	ListMultiUploadsResult listMultiUploadsResult = cosXmlService.listMultiUploads(request);
}
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request 
cosXmlService.listMultiUploadsAsync(listMultiUploadsResult, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // Delete Multi Object success...
		ListMultiUploadsResult listMultiUploadsResult  = (ListMultiUploadsResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        //  Delete Multi Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | String |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | getBucketLocationAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through ListMultiUploadsResult.

| Member Variable | Type | Description |
| -------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
| listMultipartUploads | [ListMultipartUploads](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/ListMultipartUploads.java) | Returns information of all multipart uploads in progress in the bucket |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

### Uploading an Object in Parts
With multipart upload, you can do the following:

- Upload an object in parts, including initializing a multipart upload, uploading parts, and completing the multipart upload.
- Resume a multipart upload, including querying uploaded parts, uploading parts, and completing the multipart upload.
- Delete uploaded parts.

### <span id = "INIT_MULIT_UPLOAD">Initializing a Multipart Upload</span>

#### Feature Description

This API (Initiate Multipart Upload) is used to initialize a multipart upload operation and get the corresponding uploadId.

#### Method Prototype

```java
InitMultipartUploadResult initMultipartUpload(InitMultipartUploadRequest request) throws CosXmlClientException, CosXmlServiceException;

void initMultipartUploadAsync(InitMultipartUploadRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key, such as cosPath = "text.txt";

InitMultipartUploadRequest initMultipartUploadRequest = new InitMultipartUploadRequest(bucket, cosPath);

// Use the sync method to request
try {
    InitMultipartUploadResult initMultipartUploadResult = cosXmlService.initMultipartUpload(initMultipartUploadRequest);
    String uploadId =initMultipartUploadResult.initMultipartUpload.uploadId;
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// Use the async method to request
cosXmlService.initMultipartUploadAsync(initMultipartUploadRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        String uploadId = ((InitMultipartUploadResult)cosXmlResult).initMultipartUpload.uploadId;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Init Multipart Upload failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `initMultipartUploadRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.


#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | String |
| cosPath | Constructor or SetCosPath | Position identifier of the object in the bucket, i.e., the [object key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | getBucketLocationAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through InitMultipartUploadResult.

| Member Variable | Type | Description |
| ------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
| initMultipartUpload | [InitiateMultipartUpload](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/main/java/com/tencent/cos/xml/model/tag/InitiateMultipartUpload.java) |  Returns the uploadId of the initialized multipart upload |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

### <span id = "LIST_MULIT_UPLOAD">Querying Uploaded Parts</span>

#### Feature Description

This API (List Parts) is used to query uploaded parts in the specified multipart upload operation.

#### Method Prototype

```java
ListPartsResult listParts(ListPartsRequest request) throws CosXmlClientException, CosXmlServiceException;

void listPartsAsync(ListPartsRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key, such as cosPath = "text.txt";
String uploadId = "uploadId returned by the multipart upload initialization";

ListPartsRequest listPartsRequest = new ListPartsRequest(bucket, cosPath, uploadId);

// Use the sync method to request
try {
    ListPartsResult listPartsResult = cosXmlService.listParts(listPartsRequest);
    ListParts listParts = listPartsResult.listParts;
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request 
cosXmlService.listPartsAsync(listPartsRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        ListParts listParts = ((ListPartsResult)cosXmlResult).listParts;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo List Part failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `listPartsRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.


#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ----------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | String |
| cosPath | Constructor or SetCosPath | Position identifier of the object in the bucket, i.e., the [object key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| uploadId | Constructor or SetUploadId | Identifies the uploadId of the specified multipart upload | String |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | listPartsAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through ListPartsResult.

| Member Variable | Type | Description |
| --------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
| listParts | [ListParts](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/main/java/com/tencent/cos/xml/model/tag/ListParts.java) | Returns information of the uploaded parts in the multipart upload with the specified uploadId |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

### <span id = "MULIT_UPLOAD_PART">Uploading Parts</span>

This API (Upload Part) is used to upload an object in parts.

#### Method Prototype

```java
UploadPartResult uploadPart(UploadPartRequest request) throws CosXmlClientException, CosXmlServiceException;

void uploadPartAsync(UploadPartRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key
String uploadId ="xxxxxxxx"; // uploadId returned by the multipart upload initialization
int partNumber = 1; // Part number, which must start from 1
String srcPath = Environment.getExternalStorageDirectory().getPath() + "/exampleobject"; // Absolute path to the local file
UploadPartRequest uploadPartRequest = new UploadPartRequest(bucket, cosPath, partNumber, srcPath, uploadId);

uploadPartRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        float result = (float) (progress * 100.0/max);
        Log.w("TEST","progress =" + (long)result + "%");
    }
});

// Use the sync method to upload
try {
    UploadPartResult uploadPartResult = cosXmlService.uploadPart(uploadPartRequest);
    String eTag = uploadPartResult.eTag; // Get the eTag of a part
    
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

    
// Use the async callback to request
cosXmlService.uploadPartAsync(uploadPartRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        String eTag =((UploadPartResult)cosXmlResult).eTag;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Upload Part failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ------------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | String |
| cosPath | Constructor or SetCosPath | Position identifier of the object in the bucket, i.e., the [object key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| uploadId | Constructor or SetUploadId | Identifies the uploadId of the specified multipart upload | String |
| partNumber | Constructor or SetPartNumber | Identifies the number of the specified part, which must be >= 1 | int |
| srcPath | Constructor | Absolute path to a local file to be uploaded to COS | String |
| data | Constructor | Byte array for uploading to COS | byte[] |
| progressCallback | SetCosProgressCallback | Sets upload progress callback | Callback.OnProgressCallback |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | uploadPartAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through UploadPartResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
| eTag | String | Returns eTag of the object part |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

### Copying Parts

#### Feature Description

This API (Upload Part-Copy) is used to copy an object as a part.

#### Method Prototype

```java
UploadPartCopyResult copyObject(UploadPartCopyRequest request) throws CosXmlClientException, CosXmlServiceException;

void copyObjectAsync(UploadPartCopyRequest request,final CosXmlResultListener cosXmlResultListener);
```
#### Sample Request

```java
// Specific steps:
// 1. Call cosXmlService.initMultipartUpload(InitMultipartUploadRequest) to initialize a multipart upload. For more information, see [InitMultipartUploadRequest](#InitMultipartUploadRequest).
// 2. Call cosXmlService.copyObject(UploadPartCopyRequest) to initiate the multipart copy.
// 3. Call cosXmlService.completeMultiUpload(CompleteMultiUploadRequest) to complete the multipart copy. For more information, see [CompleteMultiUploadRequest](#CompleteMultiUploadRequest).

String sourceAppid = "1250000000"; // Account's appid
String sourceBucket = "sourcebucket-1250000000"; // Bucket of the source object
String sourceRegion = "ap-beijing"; // Bucket region of the source object
String sourceCosPath = "source-exampleobject"; // Source object key
// Construct the source object attribute
CopyObjectRequest.CopySourceStruct copySourceStruct = new CopyObjectRequest.CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceCosPath);

String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key

String uploadId = "uploadId of the multipart upload initialized";
int partNumber = 1; // Part number
long start = 0;// Starting position of the source object to be copied
long end = 100; // Ending position of the source object to be copied

UploadPartCopyRequest uploadPartCopyRequest = new UploadPartCopyRequest(bucket, cosPath, partNumber,  uploadId, copySourceStruct， start, end);

// Use the sync method
try {
    UploadPartCopyResult uploadPartCopyResult = cosXmlService.copyObject(uploadPartCopyRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.copyObjectAsync(uploadPartCopyRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Copy Object success
		UploadPartCopyResult uploadPartCopyResult  = (UploadPartCopyResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Copy Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `uploadPartCopyRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.

#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ------------------------ | ------------------------------------------------------------ | -------------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | String |
| cosPath | Constructor | Position identifier of the object in the bucket, i.e., the [object key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| copySourceStruct | Constructor | Description of the source path of the copied data | CopySourceStruct |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | copyObjectAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through CopyObjectResult.

| Member Variable | Type | Description |
| ---------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
| copyObject | [CopyObject](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/main/java/com/tencent/cos/xml/model/tag/CopyObject.java) | Returns information of the successfully copied object |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

### <span id = "COMPLETE_MULIT_UPLOAD">Completing a Multipart Upload</span>

#### Feature Description

The API (Complete Multipart Upload) is used to complete the multipart upload of the entire file.

#### Method Prototype
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key, such as cosPath = "text.txt";
String uploadId = "uploadId returned by the multipart upload initialization";
int partNumber = 1;
String etag = "partNumber corresponding to the etag returned at the end of the multipart upload";
Map<Integer, String> partNumberAndETag = new HashMap<>();
partNumberAndETag.put(partNumber, etag);

CompleteMultiUploadRequest completeMultiUploadRequest = new CompleteMultiUploadRequest(bucket, cosPath, uploadId, partNumberAndETag);

// Use the sync method to request
try {
    CompleteMultiUploadResult completeMultiUploadResult = cosXmlService.completeMultiUpload(completeMultiUploadRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use the async callback to request
cosXmlService.completeMultiUploadAsync(completeMultiUploadRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Complete Multi Upload success...
		CompleteMultiUploadResult completeMultiUploadResult = (CompleteMultiUploadResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Complete Multi Upload failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `completeMultiUploadRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.


#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ----------------------- | ------------------------------------------------------------ | -------------------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | String |
| cosPath | Constructor or SetCosPath | Position identifier of the object in the bucket, i.e., the [object key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| uploadId | Constructor or SetUploadId | Identifies the uploadId of the specified multipart upload | String |
| partNumber | SetPartNumberAndETag | Identifies the number of the specified part, which must be >= 1 | int |
| eTag | SetPartNumberAndETag | Identifies the eTag returned by the upload of the specified part | String |
| partNumberAndETags | SetPartNumberAndETag | Identifies the part number and the eTag returned by the upload | `Dictionary<int, String> ` |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | completeMultiUploadAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through CompleteMultipartUploadResult.

| Member Variable | Type | Description |
| -------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
| CompleteResult | [CompleteMultipartUploadResult](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/main/java/com/tencent/cos/xml/model/tag/CompleteMultipartUploadResult.java) | Returns the upload success information of all parts |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

### <span id = "ABORT_MULIT_UPLOAD">Aborting a Multipart Upload</span>

#### Feature Description

This API (Abort Multipart Upload) is used to abort a multipart upload operation and delete the uploaded parts.

#### Method Prototype

```java
AbortMultiUploadResult abortMultiUpload(AbortMultiUploadRequest request) throws CosXmlClientException, CosXmlServiceException;

void abortMultiUploadAsync(AbortMultiUploadRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key, such as cosPath = "text.txt";
String uploadId = "uploadId returned by the multipart upload initialization";

AbortMultiUploadRequest abortMultiUploadRequest = new AbortMultiUploadRequest(bucket, cosPath, uploadId);

// Use the sync method to request
try {
    AbortMultiUploadResult abortMultiUploadResult = cosXmlService.abortMultiUpload(abortMultiUploadRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// Use the async callback to request
cosXmlService.abortMultiUploadAsync(abortMultiUploadRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        // todo Abort Multi Upload success...
		AbortMultiUploadResult abortMultiUploadResult = (AbortMultiUploadResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Abort Multi Upload failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `abortMultiUploadRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.

#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ----------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | String |
| cosPath | Constructor or SetCosPath | Position identifier of the object in the bucket, i.e., the [object key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| uploadId | Constructor or SetUploadId | Identifies the uploadId of the specified multipart upload | String |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | abortMultiUploadAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through AbortMultipartUploadResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.


## Other Operations

### Restoring an Archived Object 

#### Feature Description

This API (POST Object restore) is used to retrieve an archived object for access.

#### Method Prototype

```java
RestoreResult restoreObject(RestoreRequest request) throws CosXmlClientException, CosXmlServiceException;

void restoreObjectAsync(RestoreRequest request,  CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key, such as cosPath = "text.txt";
RestoreRequest restoreRequest = new RestoreRequest(bucket, cosPath);
restoreRequest.setExpireDays(5); // Retain for 5 days
restoreRequest.setTier(RestoreConfigure.Tier.Standard); // Standard restoration mode
// Use the sync method
try {
    RestoreResult restoreResult = cosXmlService.restoreObject(restoreRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// Use the async callback to request
cosXmlService.restoreObjectAsync(restoreRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Get Bucket ACL success
		RestoreResult restoreResult = (RestoreResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket ACL failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `restoreRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.


#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | String |
| cosPath | Constructor or SetCosPath | Position identifier of the object in the bucket, i.e., the [object key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| days | SetExpireDays | Sets the expiration time of the temporary copy | int |
| tier | SetTier | For data restoration, Tier can specify the restoration type supported by CAS, including Expedited, Standard, and Bulk | RestoreConfigure.Tier |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | restoreObjectAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through RestoreObjectResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

### Setting Object ACL

#### Feature Description

This API (PUT Object acl) is used to set the ACL for the specified object (file/object) in a bucket.

#### Method Prototype

```java
PutObjectACLResult putObjectACL(PutObjectACLRequest request) throws CosXmlClientException, CosXmlServiceException;

void putObjectACLAsync(PutObjectACLRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key, such as cosPath = "text.txt";
PutObjectACLRequest putObjectACLRequest = new PutObjectACLRequest(bucket, cosPath);

// Set bucket access permission
putObjectACLRequest.setXCOSACL("public-read");

// Grant the grantee read permission
ACLAccount readACLS = new ACLAccount();
readACLS.addAccount("OwnerUin", "OwnerUin");
putObjectACLRequest.setXCOSGrantRead(readACLS);

// Grant the grantee read-write permission
ACLAccount writeandReadACLS = new ACLAccount();
writeandReadACLS.addAccount("OwnerUin", "OwnerUin");
putObjectACLRequest.setXCOSGrantRead(writeandReadACLS);

// Use the sync method
try {
    PutObjectACLResult putObjectACLResult = cosXmlService.putObjectACL(putObjectACLRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// Use the async callback to request
cosXmlService.putObjectACLAsync(putObjectACLRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Put Bucket ACL success
		PutObjectACLResult putObjectACLResult = (PutObjectACLResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Put Bucket ACL failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `putObjectACLRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.


#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | --------------------------------------------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | String |
| cosPath | Constructor or SetCosPath | Position identifier of the object in the bucket, i.e., the [object key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| cosAcl | SetCosAcl | Sets bucket ACL permission | String |
| grandtAccout | SetXCosGrantRead or SetXCosReadWrite | Grants the user read and write permissions | GrantAccount |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | putObjectACLAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through PutObjectACLResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

### Querying Object ACL

#### Feature Description

This API (GET Object acl) is used to query the ACL of an object (file/object).

#### Method Prototype

```java
GetObjectACLResult getObjectACL(GetObjectACLRequest request) throws CosXmlClientException, CosXmlServiceException;

void getObjectACLAsync(GetObjectACLRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample Request

```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key, such as cosPath = "text.txt";
GetObjectACLRequest getBucketACLRequest = new GetObjectACLRequest(bucket, cosPath);

// Use the sync method
try {
    GetObjectACLResult getObjectACLResult = cosXmlService.getObjectACL(getBucketACLRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}
    
// Use the async callback to request
cosXmlService.getObjectACLAsync(getBucketACLRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Get Bucket ACL success
		GetObjectACLResult getObjectACLResult = (GetObjectACLResult)result;
    }
    
    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
        // todo Get Bucket ACL failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
> When initiating a request, if you want to directly set an already calculated signature string, you can do so by calling the `getBucketACLRequest.setSign("already calculated signature string")` method. The signature string is calculated by the SDK by default.


#### Parameter Descriptions

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Constructor | Bucket name in the format of BucketName-APPID | String |
| cosPath | Constructor or SetCosPath | Position identifier of the object in the bucket, i.e., the [object key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| headerKeys          | setSign  | Whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys  | setSign  | Whether the signature verifies the query parameter in the request URL | `Set<String>` |
| cosXmlResultListener | getObjectACLAsync | Result callback | CosXmlResultListener |

#### Return Result Descriptions

The result of the request is returned through GetObjectACLResult.

| Member Variable | Type | Description |
| ------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int  | HTTP code. If the code is within the range of [200, 300), the operation succeeded; otherwise, it failed |
| accessControlPolicy | [AccessControlPolicy](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/AccessControlPolicy.java) | Returns object ACL information |

> If the operation failed, the system throws a [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517) exception.

## Advanced API (Recommended)

### Uploading an Object

**TransferManager** and **COSXMLUploadTask** encapsulate async requests for simple upload and multipart upload APIs and support pausing, resuming, and canceling upload requests, which are the recommended methods for object upload. The sample code is as follows:

```java
// Initialize TransferConfig
TransferConfig transferConfig = new TransferConfig.Builder().build();

/*If you have special requirements, you can customize the initialization as follows. For example, for an object >= 2 MB in size, use multipart upload where part size is 1 MB, and for a source object above 5 MB, use multipart copy where part size is 5 MB.*/
TransferConfig transferConfig = new TransferConfig.Builder()
        .setDividsionForCopy(5 * 1024 * 1024) // Minimum object size for multipart copy
        .setSliceSizeForCopy(5 * 1024 * 1024) // Part size during multipart copy
        .setDivisionForUpload(2 * 1024 * 1024) // Minimum object size for multipart upload
        .setSliceSizeForUpload(1024 * 1024) // Part size during multipart upload
        .build();


// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService, transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key
String srcPath = Environment.getExternalStorageDirectory().getPath() + "/exampleobject"; // "Absolute path to the local file";
String uploadId = null; // If there is an uploadId of an initialized multipart upload, assigning the value of the uploadId here for resumed upload; otherwise, assign null.
// Upload the object
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath, srcPath, uploadId);

/**
* If a byte array is to be uploaded, you can call the upload(string, string, byte[]) method of TransferManager to implement;
* byte[] bytes = "this is a test".getBytes(Charset.forName("UTF-8"));
* cosxmlUploadTask = transferManager.upload(bucket, cosPath, bytes);
*/

/**
* If a byte stream is to be uploaded, you can call the upload(String, String, InputStream) method of TransferManager to implement;
* InputStream inputStream = new ByteArrayInputStream("this is a test".getBytes(Charset.forName("UTF-8")));
* cosxmlUploadTask = transferManager.upload(bucket, cosPath, inputStream);
*/

// Set upload progress callback
cosxmlUploadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
            @Override
            public void onProgress(long complete, long target) {
                float progress = 1.0f * complete / target * 100;
                Log.d("TEST",  String.format("progress = %d%%", (int)progress));
            }
        });
// Set return result callback
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
				COSXMLUploadTaskResult cOSXMLUploadTaskResult = (COSXMLUploadTaskResult)result;
                Log.d("TEST",  "Success: " + cOSXMLUploadTaskResult.printResult());
            }

            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
                Log.d("TEST",  "Failed: " + (exception == null ? serviceException.getMessage() : exception.toString()));
            }
        });
// Set task status callback where you can view the task process
cosxmlUploadTask.setTransferStateListener(new TransferStateListener() {
            @Override
            public void onStateChanged(TransferState state) {
                Log.d("TEST", "Task state:" + state.name());
            }
        });

/**
If you have special requirements, you can do the following:
 PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);
 putObjectRequest.setRegion(region); // Set the bucket region
 putObjectRequest.setNeedMD5(true); // Whether to enable MD5 checksum
 COSXMLUploadTask cosxmlUploadTask = transferManager.upload(putObjectRequest, uploadId);
*/

// Cancel upload
cosxmlUploadTask.cancel();


// Pause upload
cosxmlUploadTask.pause();

// Resume upload
cosxmlUploadTask.resume();

```

### Downloading an Object

**TransferManager** and **COSXMLDownloadTask** encapsulate async requests for the download API and support pausing, resuming, and canceling download requests. The sample code is as follows:

```java
Context applicationContext = getApplicationContext()； // application context
String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key
String savePathDir = Environment.getExternalStorageDirectory().getPath(); // Local directory path
String savedFileName = "exampleobject"；// Name of the locally saved file; if this is null, the filename in COS will be used
// Download the object
COSXMLDownloadTask cosxmlDownloadTask = transferManager.download(applicationContext, bucket, cosPath, savedDirPath, savedFileName);
// Set download progress callback
cosxmlDownloadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
            @Override
            public void onProgress(long complete, long target) {
                float progress = 1.0f * complete / target * 100;
                Log.d("TEST",  String.format("progress = %d%%", (int)progress));
            }
        });
// Set return result callback
cosxmlDownloadTask.setCosXmlResultListener(new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
				COSXMLDownloadTaskResult cOSXMLDownloadTaskResult = (COSXMLDownloadTaskResult)result;
                Log.d("TEST",  "Success: " + cOSXMLDownloadTaskResult.printResult());
            }

            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
                Log.d("TEST",  "Failed: " + (exception == null ? serviceException.getMessage() : exception.toString()));
            }
        });
// Set task status callback where you can view the task process
cosxmlDownloadTask.setTransferStateListener(new TransferStateListener() {
            @Override
            public void onStateChanged(TransferState state) {
                Log.d("TEST", "Task state:" + state.name());
            }
        });

/**
If you have special requirements, you can do the following:
GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath, localDir, localFileName);
getObjectRequest.setRegion(region); // Set the bucket region
COSXMLDownloadTask cosxmlDownloadTask = transferManager.download(context, getObjectRequest);
*/

// Cancel download
cosxmlDownloadTask.cancel();

// Pause download
cosxmlDownloadTask.pause();

// Resume download
cosxmlDownloadTask.resume();

```

### Copying an Object

**TransferManager** and **COSXMLCopyTask** encapsulate async requests for simple copy and multipart copy APIs and support pausing, resuming, and canceling copy requests. The sample code is as follows:

```java
String sourceAppid = "1250000000"; // Account's appid
String sourceBucket = "sourcebucket-1250000000"; // Bucket of the source object
String sourceRegion = "ap-beijing"; // Bucket region of the source object
String sourceCosPath = "source-exampleobject"; // Object key of the source object
// Construct the source object attribute
CopyObjectRequest.CopySourceStruct copySourceStruct = new CopyObjectRequest.CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceCosPath);

String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
String cosPath = "exampleobject"; // Position identifier of the object in the bucket, i.e., the object key
// Copy the object
COSXMLCopyTask cosxmlCopyTask = transferManager.copy(bucket, cosPath, copySourceStruct);
// Set return result callback
cosxmlCopyTask.setCosXmlResultListener(new CosXmlResultListener() {
            @Override
            public void onSuccess(CosXmlRequest request, CosXmlResult result) {
				COSXMLCopyTaskResult cOSXMLCopyTaskResult = (COSXMLCopyTaskResult)result;
                Log.d("TEST",  "Success: " + cOSXMLCopyTaskResult.printResult());
            }

            @Override
            public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
                Log.d("TEST",  "Failed: " + (exception == null ? serviceException.getMessage() : exception.toString()));
            }
        });
// Set task status callback where you can view the task process
cosxmlCopyTask.setTransferStateListener(new TransferStateListener() {
            @Override
            public void onStateChanged(TransferState state) {
                Log.d("TEST", "Task state:" + state.name());
            }
        });
/**
If you have special requirements, you can do the following:
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath, copySourceStruct);
copyObjectRequest.setRegion(region); // Set the bucket region
COSXMLCopyTask cosxmlCopyTask = transferManager.copy(copyObjectRequest);
*/

// Cancel copy
cosxmlCopyTask.cancel();


// Pause copy
cosxmlCopyTask.pause();

// Resume copy
cosxmlCopyTask.resume();
```
