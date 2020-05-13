## Overview

This document provides an overview of APIs and SDK sample codes related to simple operations, multipart operations, and other object operations.

**Simple operations**

| API | Operation Name | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/7734) | Querying an object list | Queries some or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object using simple upload | Uploads an object to a bucket |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploads an object using a form | Uploads an object by using a form request |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [Options Object](https://intl.cloud.tencent.com/document/product/436/8288) | Configuring pre-flight requests for cross-origin access | Sends a pre-flight request to check whether a real cross-origin access request can be sent |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Setting object replication | Copies a file to the destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting one object | Deletes a specified object in a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |


**Multipart upload operations**

| API | Operation Name | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries the information of a multipart upload in progress |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload job |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading a part | Uploads a file part in multiple parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation Name | Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting an object ACL | Sets the ACL for a specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Getting an object ACL | Gets the ACL of an object |

## Simple Operations

### Querying an object list

## Feature description

This API is used to query some or all objects in a bucket.

#### Method prototype

```java
GetBucketResult getBucket(GetBucketRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketAsync(GetBucketRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket)
```java
String bucketName = "examplebucket-1250000000";  // Format: BucketName-APPID;
GetBucketRequest getBucketRequest = new GetBucketRequest(bucketName);

// Prefix match is used to specify the prefix address of the returned object
getBucketRequest.setPrefix("prefix");

// If this is the first request, you do not need to set a marker. COS will list the objects from the beginning
// If you need to list another page of objects, then you need to set a marker with the GetBucketResult.listBucket.nextMarker value returned from the last request
// If the returned GetBucketResult.listBucket.isTruncated value is false, this indicates that all the objects that satisfy the conditions have been listed.
// getBucketRequest.setMarker(marker);

// The maximum number of entries returned at a time; the default value is 1,000
getBucketRequest.setMaxKeys(100);

// The delimiter is a sign. If the prefix exists,
// identical paths between the prefix and delimiter are grouped as the same type and defined as a common prefix,
// and then all common prefixes are listed. If there is no prefix, the listing starts from the beginning of the path
getBucketRequest.setDelimiter('/');

// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
getBucketRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    GetBucketResult getBucketResult = cosXmlService.getBucket(getBucketRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests 
cosXmlService.getBucketAsync(getBucketRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketResult getBucketResult = (GetBucketResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Get Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});

// If you need to list all objects, see the reference code below:

bucketName = "examplebucket-1250000000";
getBucketRequest = new GetBucketRequest(bucketName);

// Prefix indicates that the object keys to be listed begin with a prefix
getBucketRequest.setPrefix("images/");
// The delimiter indicates the separator. Set "/" to list objects in the current directory; set to null to list all objects.
getBucketRequest.setDelimiter("/");
// Set the maximum number of objects to be traversed, which can be up to 1,000 in one listobject operation
getBucketRequest.setMaxKeys(100);
GetBucketResult getBucketResult = null;
do {
    try {
        getBucketResult = cosXmlService.getBucket(getBucketRequest);
    } catch (CosXmlClientException e) {
        e.printStackTrace();
        return;
    } catch (CosXmlServiceException e) {
        e.printStackTrace();
        return;
    }
    // commonPrefixs indicates the path truncated by the delimiter. If the delimiter is set to "/", commonPrefixs indicates the paths of subdirectories.
    List<ListBucket.CommonPrefixes> commonPrefixs = getBucketResult.listBucket.commonPrefixesList;

    // contents indicates the object list
    List<ListBucket.Contents> contents = getBucketResult.listBucket.contentsList;

    String nextMarker = getBucketResult.listBucket.nextMarker;
    getBucketRequest.setMarker(nextMarker);
} while (getBucketResult.listBucket.isTruncated);
```


>When initiating a request, you can use a calculated signature string by calling `getBucketRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| prefix | set method | Limits the returned result objects to those prefixed with a given prefix. By default, there is no limit, that is, the default is all members of the bucket | String |
| marker | set method | Marks the starting position of the list, which can be set to empty for the first request, and subsequent requests need to be set to the nextMarker in the previous  returned listObjects value | String |
| delimiter | set method | Indicates that the path that starts with "prefix" and ends with the first instance of the delimiter will be returned. | String |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | getBucketAsync                                                | Result callback        | CosXmlResultListener   |


#### Response description


The result of the request is returned through GetBucketResult.

| Member Variable | Type | Description |
| ---------- | ------------------------------------------------------------ | --------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| listBucket | [ListBucket](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/ListBucket.java) | The list of objects in a bucket is returned |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Uploading an object usng simple upload

## Feature description

This API is used to upload an object to a specified bucket. The uploaded object must not be larger than 5GB. Please use [Multipart Upload] (#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [Advanced APIs] (#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) to upload objects larger than 5GB.

#### Method prototype

```java
PutObjectResult putObject(PutObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void putObjectAsync(PutObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-put-object)
```java
String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. For example, cosPath = "text.txt";
String srcPath = new File(context.getExternalCacheDir(), "exampleobject").toString();//" Absolute path of the local file ";
PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);

putObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
putObjectRequest.setSignParamsAndHeaders(null, headerKeys);
// Upload using the sync method
try {
    PutObjectResult putObjectResult = cosXmlService.putObject(putObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Upload using asynchronous callback
cosXmlService.putObjectAsync(putObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        PutObjectResult putObjectResult = (PutObjectResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Put object failed because of CosXmlClientException or CosXmlServiceException...
    }
});


// Upload byte array
byte[] data = "this is a test".getBytes(Charset.forName("UTF-8"));
putObjectRequest = new PutObjectRequest(bucket, cosPath, data);
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


// Upload byte stream
InputStream inputStream = new ByteArrayInputStream("this is a test".getBytes(Charset.forName("UTF-8")));
putObjectRequest = new PutObjectRequest(bucket, cosPath, inputStream);
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
>When initiating a request, you can use a calculated signature string by calling `putObjectRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath | Location identifier of the object in the bucket, i.e. the [object key](https://intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.cloud.tencent.com/document/product/436/13324) | String                      |
| srcPath | Constructor | Absolute path to the local file uploaded to COS | string |
| data | Constructor | The byte array of the file uploaded to COS | byte[] |
|inputStream          | Constructor               | The byte stream of the file uploaded to COS                                     | InputStream                 |
| progressCallback    | setProgressListener | Sets the upload progress callback                                             | CosXmlProgressListener |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | putObjectAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through PutObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | string | Returns the eTag of an object |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Uploading an object using a form

## Feature description

This API is used to upload an object using a form.

#### Method prototype

```java
PostObjectResult postObject(PostObjectRequest request) throws CosXmlClientException, CosXmlServiceException；

void postObjectAsync(PostObjectRequest request, CosXmlResultListener cosXmlResultListener)；
```

#### Sample request

[//]: # (.cssg-snippet-post-object)
```java
String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. For example, cosPath = "text.txt";
String srcPath = new File(context.getExternalCacheDir(), "exampleobject").toString();//" Absolute path of the local file ";

PostObjectRequest postObjectRequest = new PostObjectRequest(bucket, cosPath, srcPath);

postObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
postObjectRequest.setSignParamsAndHeaders(null, headerKeys);
// Upload using the sync method
try {
    PostObjectResult postObjectResult = cosXmlService.postObject(postObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Upload using asynchronous callback
cosXmlService.postObjectAsync(postObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        PutObjectResult putObjectResult = (PutObjectResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Put object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath | Location identifier of the object in the bucket, i.e. the [object key](https://intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.cloud.tencent.com/document/product/436/13324) | String                      |
| srcPath | Constructor | Absolute path to the local file uploaded to COS | string |
| data | Constructor | The byte array of the file uploaded to COS | byte[] |
|inputStream          | Constructor               | The byte stream of the file to be uploaded to COS                                     | InputStream                 |
| progressCallback    | setProgressListener | Sets the upload progress callback                                             | CosXmlProgressListener |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | postObjectAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through PostObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | string | Returns the eTag of an object |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Querying object metadata

## Feature description

This API (HEAD Object) is used to query object metadata.

#### Method prototype

```java
HeadObjectResult headObject(HeadObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void headObjectAsync(HeadObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-head-object)
```java
String bucket = bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. 
HeadObjectRequest headObjectRequest = new HeadObjectRequest(bucket, cosPath);
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
headObjectRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    HeadObjectResult headObjectResult = cosXmlService.headObject(headObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests
cosXmlService.headObjectAsync(headObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        HeadObjectResult headObjectResult = (HeadObjectResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Head Bucket failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

>When initiating a request, you can use a calculated signature string by calling `headObjectRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.


#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | --------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath | Location identifier of the object in the bucket, i.e. the [object key](https://intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.cloud.tencent.com/document/product/436/13324) | String                      |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | headObjectAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through HeadObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | string | Returns the eTag of an object |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Downloading an object

## Feature description

This API is used to download an object.

#### Method prototype

```java
GetObjectResult getObject(GetObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void getObjectAsync(GetObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-get-object)
```java
String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. 
String savePath = context.getExternalCacheDir().toString(); // Local path

GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath, savePath);
getObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
getObjectRequest.setSignParamsAndHeaders(null, headerKeys);
// Download using the sync method
try {
    GetObjectResult getObjectResult = cosXmlService.getObject(getObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests 
cosXmlService.getObjectAsync(getObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult cosXmlResult) {
        GetObjectResult getObjectResult = (GetObjectResult) cosXmlResult;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Get Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

>When initiating a request, you can use a calculated signature string by calling `getObjectRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath | Location identifier of the object in the bucket, i.e. the [object key](https://intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.cloud.tencent.com/document/product/436/13324) | String                      |
| localDir | Constructor | The absolute path to the folder where the file was downloaded and stored locally | string |
| localDir | Constructor | The name of the file downloaded and stored locally | string |
| progressCallback    | setProgressListener | Sets the upload progress callback                                             | CosXmlProgressListener |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | getObjectAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through GetObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | string | Returns the eTag of an object |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Configuring pre-flight requests for cross-origin access

## Feature description
This API is used to get the CORS configuration for a pre-flight request.

#### Method prototype

```java
OptionObjectResult optionObject(OptionObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void optionObjectAsync(OptionObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-option-object)
```java
String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. 
String origin = "https://cloud.tencent.com";
String accessMethod = "PUT";
OptionObjectRequest optionObjectRequest = new OptionObjectRequest(bucket, cosPath, origin, accessMethod);
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
optionObjectRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    OptionObjectResult result = cosXmlService.optionObject(optionObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests 
cosXmlService.optionObjectAsync(optionObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        OptionObjectResult optionObjectResult = (OptionObjectResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo OptionOb Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
>When initiating a request, you can use a calculated signature string by calling `optionObjectRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.


#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath | Location identifier of the object in the bucket, i.e. the [object key](https://intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.cloud.tencent.com/document/product/436/13324) | String                      |
| origin | Constructor or SetOrigin | Simulates the origin from which the request for cross-origin access is sent | string |
| accessMthod | Constructor or SetAccessControlMethod | Simulates the HTTP method of the request for cross-origin access | string |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | optionObjectAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through DeleteObjectResult.

| Member Variable | Type | Description |
| ------------------------------- | -------------- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| accessControlAllowHeaders | `List<String>` | Allowed request headers for cross-origin access |
| accessControlAllowMethods | `List<String>` | Allowed HTTP request methods for cross-origin access |
| accessControlAllowExposeHeaders | `List<String>` | Allowed custom request headers for cross-origin access |
| accessControlMaxAge | long | The validity period of the results obtained by OPTIONS |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Setting object replication

This API is used to copy files to the destination path.

#### Method prototype

```java
CopyObjectResult copyObject(CopyObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void copyObjectAsync(CopyObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-copy-object)
```java
string sourceAppid = "1250000000"; // Account appid
string sourceBucket = "sourcebucket-1250000000"; // Source object bucket
string sourceRegion = "COS_REGION"; // Source object bucket region
String sourceCosPath = "sourceObject"; // Source object key
// Construct source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct = new CopyObjectRequest.CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceCosPath);
String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. 

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath, copySourceStruct);
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
copyObjectRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    CopyObjectResult copyObjectResult = cosXmlService.copyObject(copyObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests
cosXmlService.copyObjectAsync(copyObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        CopyObjectResult copyObjectResult = (CopyObjectResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Copy Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
>When initiating a request, you can use a calculated signature string by calling `copyObjectRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ------------------------ | ------------------------------------------------------------ | -------------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| cosPath                 | Constructor  | Location identifier of the object in the bucket, i.e. the [object key](https://intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.cloud.tencent.com/document/product/436/13324) | String                      |
| copySourceStruct          |  Constructor            | Describes the source path of the copied data                                         | CopySourceStruct     |
| metaDataDirective | SetCopyMetaDataDirective | Indicates whether to copy or update the metadata of the source object | MetaDataDirective |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | copyObjectAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through CopyObjectResult.

| Member Variable | Type | Description |
| ---------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| copyObject | [CopyObject](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/main/java/com/tencent/cos/xml/model/tag/CopyObject.java) | Returns the information of the successfully copied object |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


### Deleting a single object

## Feature description

This API is used to delete a specified object.

#### Method prototype

```java
DeleteObjectResult deleteObject(DeleteObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteObjectAsync(DeleteObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-delete-object)
```java
String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. 

DeleteObjectRequest deleteObjectRequest = new DeleteObjectRequest(bucket, cosPath);
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
deleteObjectRequest.setSignParamsAndHeaders(null, headerKeys);
//  Delete using the sync method
try {
    DeleteObjectResult deleteObjectResult = cosXmlService.deleteObject(deleteObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests
cosXmlService.deleteObjectAsync(deleteObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        DeleteObjectResult deleteObjectResult = (DeleteObjectResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Delete Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
>When initiating a request, you can use a calculated signature string by calling `deleteObjectRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath | Location identifier of the object in the bucket, i.e. the [object key](https://intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.cloud.tencent.com/document/product/436/13324) | String                      |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | getBucketLocationAsync                                                | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through DeleteObjectResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Deleting multiple objects

## Feature description

This API is used to delete multiple specified objects.

#### Method prototype

```java
DeleteMultiObjectResult deleteMultiObject(DeleteMultiObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteMultiObjectAsync(DeleteMultiObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-delete-multi-object)
```java
String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
List<String> objectList = new ArrayList<String>();
objectList.add("exampleobject"); // The location identifier of the object in the bucket, i.e., the object key

DeleteMultiObjectRequest deleteMultiObjectRequest = new DeleteMultiObjectRequest(bucket, objectList);
deleteMultiObjectRequest.setQuiet(true);
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
deleteMultiObjectRequest.setSignParamsAndHeaders(null, headerKeys);
//  Delete using the sync method
try {
    DeleteMultiObjectResult deleteMultiObjectResult = cosXmlService.deleteMultiObject(deleteMultiObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests 
cosXmlService.deleteMultiObjectAsync(deleteMultiObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        // Delete Multi Object success...
        DeleteMultiObjectResult deleteMultiObjectResult = (DeleteMultiObjectResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        //  Delete Multi Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
>When initiating a request, you can use a calculated signature string by calling `deleteMultiObjectRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| quiet | true: Only the information of the file that failed to be deleted is returned; false: The deletion result of each file is returned | Boolean | Yes |
| objectList                | List of the [object keys] (https://intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.cloud.tencent.com/document/product/436/13324) to be deleted | `List<String>`      | Yes  |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | getBucketLocationAsync                                                | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through DeleteMultiObjectResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


## Multipart operations


- Uploading objects with multipart upload: initialize the multipart upload, upload the parts, and complete the multipart upload
- Resuming a multipart upload: query the uploaded parts, upload the remaining parts, and complete the multipart upload
- Deleting uploaded parts



### Querying multipart uploads

## Feature description

This API is used to query ongoing multipart uploads in a specified bucket.

#### Method prototype

```java
ListMultiUploadsResult listMultiUploads(ListMultiUploadsRequest request) throws CosXmlClientException, CosXmlServiceException;

void listMultiUploadsAsync(ListMultiUploadsRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-list-multi-upload)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
ListMultiUploadsRequest listMultiUploadsRequest = new ListMultiUploadsRequest(bucket);
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
listMultiUploadsRequest.setSignParamsAndHeaders(null, headerKeys);
try {
    // Use the sync method
    ListMultiUploadsResult listMultiUploadsResult = cosXmlService.listMultiUploads(listMultiUploadsRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests 
cosXmlService.listMultiUploadsAsync(listMultiUploadsRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        // Delete Multi Object success...
        ListMultiUploadsResult listMultiUploadsResult = (ListMultiUploadsResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        //  Delete Multi Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | -------- | ---------------------------------- | -------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | getBucketLocationAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through ListMultiUploadsResult.

| Member Variable | Type | Description |
| -------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| listMultipartUploads | [ListMultipartUploads](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/ListMultipartUploads.java) | Returns the information on all ongoing multipart uploads in the bucket |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### <span id = "INIT_MULIT_UPLOAD">Initializing multipart upload </span>

## Feature description

This API initializes a multipart upload task and obtains the uploadID.

#### Method prototype

```java
InitMultipartUploadResult initMultipartUpload(InitMultipartUploadRequest request) throws CosXmlClientException, CosXmlServiceException;

void initMultipartUploadAsync(InitMultipartUploadRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-init-multi-upload)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. For example, cosPath = "text.txt";

InitMultipartUploadRequest initMultipartUploadRequest = new InitMultipartUploadRequest(bucket, cosPath);
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
initMultipartUploadRequest.setSignParamsAndHeaders(null, headerKeys);
// Request using the sync method
try {
    InitMultipartUploadResult initMultipartUploadResult = cosXmlService.initMultipartUpload(initMultipartUploadRequest);
    uploadId = initMultipartUploadResult.initMultipartUpload.uploadId;
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests 
cosXmlService.initMultipartUploadAsync(initMultipartUploadRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        String uploadId = ((InitMultipartUploadResult) result).initMultipartUpload.uploadId;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Init Multipart Upload failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
>When initiating a request, you can use a calculated signature string by calling `initMultipartUploadRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.


#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath | Location identifier of the object in the bucket, i.e. the [object key](https://intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.cloud.tencent.com/document/product/436/13324) | String                      |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | getBucketLocationAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through InitMultipartUploadResult.

| Member Variable | Type | Description |
| ------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| initMultipartUpload | [InitiateMultipartUpload](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/main/java/com/tencent/cos/xml/model/tag/InitiateMultipartUpload.java)| Returns the object's uploadId when the multipart upload is initialized |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.



### <span id = "MULIT_UPLOAD_PART"> Uploading parts</span>

This API uploads object parts.

#### Method prototype

```java
UploadPartResult uploadPart(UploadPartRequest request) throws CosXmlClientException, CosXmlServiceException;

void uploadPartAsync(UploadPartRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-upload-part)
```java
String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. 
string uploadId = "exampleUploadId"; // uploadId is returned when multipart upload is initialized
int partNumber = 1; // Part number, increases incrementally starting from 1
String srcPath = new File(context.getExternalCacheDir(), "exampleobject").toString(); // Absolute path to the local file
UploadPartRequest uploadPartRequest = new UploadPartRequest(bucket, cosPath, partNumber, srcPath, uploadId);

uploadPartRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
uploadPartRequest.setSignParamsAndHeaders(null, headerKeys);
// Upload using the sync method
try {
    UploadPartResult uploadPartResult = cosXmlService.uploadPart(uploadPartRequest);
    eTag = uploadPartResult.eTag; //Get the eTag of the part
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}


// Use async callback to make requests 
cosXmlService.uploadPartAsync(uploadPartRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        String eTag = ((UploadPartResult) result).eTag;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Upload Part failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ------------------------- | ------------------------------------------------------------ | --------------------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath | Location identifier of the object in the bucket, i.e. the [object key](https://intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.cloud.tencent.com/document/product/436/13324) | String                      |
| uploadId | Constructor or SetUploadId | Identifies the uploadId of a specified multipart upload | string |
| partNumber | Constructor or SetPartNumber | Identifies the number of the specified part; this value should be ≥ 1. | int |
| srcPath | Constructor | Absolute path to the local file uploaded to COS | string |
| data | Constructor | The byte array of the file uploaded to COS | byte[] |
| progressCallback | SetCosProgressCallback | Sets the upload progress callback | Callback.OnProgressCallback |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | uploadPartAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through UploadPartResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | string | Returns the eTag of an object part |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Copying parts

## Feature description

This API is used to copy an object as a part.

#### Method prototype

```java
UploadPartCopyResult copyObject(UploadPartCopyRequest request) throws CosXmlClientException, CosXmlServiceException;

void copyObjectAsync(UploadPartCopyRequest request,final CosXmlResultListener cosXmlResultListener);
```
#### Sample request

[//]: # (.cssg-snippet-upload-part-copy)
```java
// Follow the steps below:
// 1. Call cosXmlService.initMultipartUpload(InitMultipartUploadRequest) to initialize the multipart upload. See [InitMultipartUploadRequest](#InitMultipartUploadRequest) for details.
// 2. Call cosXmlService.copyObject(UploadPartCopyRequest) to complete part replication.
// 3. Call cosXmlService.completeMultiUpload(CompleteMultiUploadRequest) to complete part replication. See [CompleteMultiUploadRequest](#CompleteMultiUploadRequest) for details.

string sourceAppid = "1250000000"; // Account appid
string sourceBucket = "sourcebucket-1250000000"; // Source object bucket
string sourceRegion = "COS_REGION"; // Source object bucket region
String sourceCosPath = "sourceObject"; // Source object key
// Construct source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct = new CopyObjectRequest.CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceCosPath);

String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. 

String uploadId = "exampleUploadId";
int partNumber = 1; // Part number
long start = 0; // Replication starting point of the source object
long end = 1023; // Replication ending point of the source object

UploadPartCopyRequest uploadPartCopyRequest = new UploadPartCopyRequest(bucket, cosPath, partNumber, uploadId, copySourceStruct, start, end);
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
uploadPartCopyRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    UploadPartCopyResult uploadPartCopyResult = cosXmlService.copyObject(uploadPartCopyRequest);
    eTag = uploadPartCopyResult.copyObject.eTag;
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests 
cosXmlService.copyObjectAsync(uploadPartCopyRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        UploadPartCopyResult uploadPartCopyResult = (UploadPartCopyResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Copy Object failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
>When initiating a request, you can use a calculated signature string by calling `uploadPartCopyRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ------------------------ | ------------------------------------------------------------ | -------------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| cosPath                 | Constructor  | Location identifier of the object in the bucket, i.e. the [object key](https://intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.cloud.tencent.com/document/product/436/13324) | String                      |
| copySourceStruct          |  Constructor            | Describes the source path of the copied data                                         | CopySourceStruct     |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | copyObjectAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through CopyObjectResult.

| Member Variable | Type | Description |
| ---------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| copyObject | [CopyObject](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/main/java/com/tencent/cos/xml/model/tag/CopyObject.java) | Returns the information of the successfully copied object |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


### <span id = "LIST_MULIT_UPLOAD"> Querying a multipart upload </span>

## Feature description

This API is used to query the uploaded parts of a specific multipart upload.

#### Method prototype

```java
ListPartsResult listParts(ListPartsRequest request) throws CosXmlClientException, CosXmlServiceException;

void listPartsAsync(ListPartsRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-list-parts)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. For example, cosPath = "text.txt";
String uploadId = "exampleUploadId";

ListPartsRequest listPartsRequest = new ListPartsRequest(bucket, cosPath, uploadId);
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
listPartsRequest.setSignParamsAndHeaders(null, headerKeys);
// Request using the sync method
try {
    ListPartsResult listPartsResult = cosXmlService.listParts(listPartsRequest);
    ListParts listParts = listPartsResult.listParts;
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests 
cosXmlService.listPartsAsync(listPartsRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        ListParts listParts = ((ListPartsResult) result).listParts;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo List Part failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
>When initiating a request, you can use a calculated signature string by calling `listPartsRequest.setSignn ("calculated signature string")`. The signature string will be calculated by the SDK by default.


#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ----------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath | Location identifier of the object in the bucket, i.e. the [object key](https://intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.cloud.tencent.com/document/product/436/13324) | String                      |
| uploadId | Constructor or SetUploadId | Identifies the uploadId of a specified multipart upload | string |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | listPartsAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through ListPartsResult.

| Member Variable | Type | Description |
| --------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| listParts | [ListParts](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/main/java/com/tencent/cos/xml/model/tag/ListParts.java) | Returns the information on the uploaded parts of a specified multipart upload |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.



### <span id = "COMPLETE_MULIT_UPLOAD"> Completing a multipart upload </ span>

## Feature description

This API is used to complete the entire multipart upload.

#### Sample request
[//]: # (.cssg-snippet-complete-multi-upload)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. For example, cosPath = "text.txt";
String uploadId = "exampleUploadId";
int partNumber = 1;
String etag = "exampleETag";
Map<Integer, String> partNumberAndETag = new HashMap<>();
partNumberAndETag.put(partNumber, etag);

CompleteMultiUploadRequest completeMultiUploadRequest = new CompleteMultiUploadRequest(bucket, cosPath, uploadId, partNumberAndETag);
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
completeMultiUploadRequest.setSignParamsAndHeaders(null, headerKeys);
// Request using the sync method
try {
    CompleteMultiUploadResult completeMultiUploadResult = cosXmlService.completeMultiUpload(completeMultiUploadRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests 
cosXmlService.completeMultiUploadAsync(completeMultiUploadRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        CompleteMultiUploadResult completeMultiUploadResult = (CompleteMultiUploadResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Complete Multi Upload failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
>When initiating a request, you can use a calculated signature string by calling `completeMultiUploadRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.


#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ----------------------- | ------------------------------------------------------------ | -------------------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath | Location identifier of the object in the bucket, i.e. the [object key](https://intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.cloud.tencent.com/document/product/436/13324) | String                      |
| uploadId | Constructor or SetUploadId | Identifies the uploadId of a specified multipart upload | string |
| partNumber | SetPartNumberAndETag | Identifies the number of the specified part; this value should be ≥ 1. | int |
| eTag | SetPartNumberAndETag | Identifies the eTag returned when the specified part is uploaded | string |
| partNumberAndETags | SetPartNumberAndETag | Identifies the part number and the eTag returned when the part is uploaded |  `Dictionary<int, String> ` |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | completeMultiUploadAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through CompleteMultipartUploadResult.

| Member Variable | Type | Description |
| -------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| CompleteResult | [CompleteMultipartUploadResult](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/main/java/com/tencent/cos/xml/model/tag/CompleteMultipartUploadResult.java) | Returns a success notification when all parts are uploaded. |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### <span id = "ABORT_MULIT_UPLOAD"> Aborting a multipart upload </ span>

## Feature description

This API is used to abort a multipart upload operation and delete the uploaded parts.

#### Method prototype

```java
AbortMultiUploadResult abortMultiUpload(AbortMultiUploadRequest request) throws CosXmlClientException, CosXmlServiceException;

void abortMultiUploadAsync(AbortMultiUploadRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-abort-multi-upload)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. For example, cosPath = "text.txt";
String uploadId = "exampleUploadId";

AbortMultiUploadRequest abortMultiUploadRequest = new AbortMultiUploadRequest(bucket, cosPath, uploadId);
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
abortMultiUploadRequest.setSignParamsAndHeaders(null, headerKeys);
// Request using the sync method
try {
    AbortMultiUploadResult abortMultiUploadResult = cosXmlService.abortMultiUpload(abortMultiUploadRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
    //
}

// Use async callback to make requests 
cosXmlService.abortMultiUploadAsync(abortMultiUploadRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        // todo Abort Multi Upload success...
        AbortMultiUploadResult abortMultiUploadResult = (AbortMultiUploadResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Abort Multi Upload failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
>When initiating a request, you can use a calculated signature string by calling `abortMultiUploadRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.

#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ----------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath | Location identifier of the object in the bucket, i.e. the [object key](https://intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.cloud.tencent.com/document/product/436/13324) | String                      |
| uploadId | Constructor or SetUploadId | Identifies the uploadId of a specified multipart upload | string |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | abortMultiUploadAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through AbortMultipartUploadResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.


**Other operations**

### Restoring an archived object 

## Feature description

This API is used to restore an archived object.

#### Method prototype

```java
RestoreResult restoreObject(RestoreRequest request) throws CosXmlClientException, CosXmlServiceException;

void restoreObjectAsync(RestoreRequest request,  CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-restore-object)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. For example, cosPath = "text.txt";
RestoreRequest restoreRequest = new RestoreRequest(bucket, cosPath);
restoreRequest.setExpireDays(5); // Retain for 5 days
restoreRequest.setTier(RestoreConfigure.Tier.Standard); // Standard restoration mode
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
restoreRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    RestoreResult restoreResult = cosXmlService.restoreObject(restoreRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests 
cosXmlService.restoreObjectAsync(restoreRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // todo Get Bucket ACL success
        RestoreResult restoreResult = (RestoreResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Get Bucket ACL failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
>When initiating a request, you can can use a calculated signature string by calling `restoreRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.


#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | --------------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath | Location identifier of the object in the bucket, i.e. the [object key](https://intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.cloud.tencent.com/document/product/436/13324) | String                      |
| days | SetExpireDays | Sets the validity period of the temporary replica | int |
| tier | SetTier | When restoring data, Tier can be specified as three types of restoration supported by CAS: Expedited, Standard, and Bulk. | RestoreConfigure.Tier |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | restoreObjectAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through RestoreObjectResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Setting object ACL

## Feature description

This API is used to set the access control list (ACL) of an object in a specific bucket.

#### Method prototype

```java
PutObjectACLResult putObjectACL(PutObjectACLRequest request) throws CosXmlClientException, CosXmlServiceException;

void putObjectACLAsync(PutObjectACLRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-put-object-acl)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. For example, cosPath = "text.txt";
PutObjectACLRequest putObjectACLRequest = new PutObjectACLRequest(bucket, cosPath);

// Set bucket's access permission
putObjectACLRequest.setXCOSACL("public-read");

// Grant read permission to an authorized user
ACLAccount readACLS = new ACLAccount();
readACLS.addAccount("100000000001", "100000000001");
putObjectACLRequest.setXCOSGrantRead(readACLS);

// Grant read and write permissions to an authorized user
ACLAccount writeandReadACLS = new ACLAccount();
writeandReadACLS.addAccount("100000000001", "100000000001");
putObjectACLRequest.setXCOSReadWrite(writeandReadACLS);
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
putObjectACLRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    PutObjectACLResult putObjectACLResult = cosXmlService.putObjectACL(putObjectACLRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests 
cosXmlService.putObjectACLAsync(putObjectACLRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutObjectACLResult putObjectACLResult = (PutObjectACLResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Put Bucket ACL failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```

>When initiating a request, you can use a calculated signature string by calling `putObjectACLRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.


#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | --------------------------------------------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath | Location identifier of the object in the bucket, i.e. the [object key](https://intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.cloud.tencent.com/document/product/436/13324) | String                      |
| cosAcl | SetCosAcl | Sets the ACL permissions for a bucket | string |
| grantAccount | SetXCosGrantRead  or SetXCosReadWrite | Grants users read and write permissions | GrantAccount |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | putObjectACLAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through PutObjectACLResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

### Querying object ACL

## Feature description

This API is used to query the ACL of an object.

#### Method prototype

```java
GetObjectACLResult getObjectACL(GetObjectACLRequest request) throws CosXmlClientException, CosXmlServiceException;

void getObjectACLAsync(GetObjectACLRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Sample request

[//]: # (.cssg-snippet-get-object-acl)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. For example, cosPath = "text.txt";
GetObjectACLRequest getBucketACLRequest = new GetObjectACLRequest(bucket, cosPath);
// Set the signature verification host, verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
getBucketACLRequest.setSignParamsAndHeaders(null, headerKeys);
// Use the sync method
try {
    GetObjectACLResult getObjectACLResult = cosXmlService.getObjectACL(getBucketACLRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Use async callback to make requests
cosXmlService.getObjectACLAsync(getBucketACLRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetObjectACLResult getObjectACLResult = (GetObjectACLResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException) {
        // todo Get Bucket ACL failed because of CosXmlClientException or CosXmlServiceException...
    }
});
```
>When initiating a request, you can use a calculated signature string by calling `getBucketACLRequest.setSign ("calculated signature string")`. The signature string will be calculated by the SDK by default.


#### Parameter description

| Parameter Name | Setting Method | Description | Type |
| ------------------- | ---------------------- | ------------------------------------------------------------ | -------------- |
| bucket | Constructor | Bucket name in the format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath | Location identifier of the object in the bucket, i.e. the [object key](https://intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.intl.cloud.tencent.com/document/product/436/13324) | String                      |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether the signature verifies the header                | `Set<String>` |
| queryParameterKeys | setSignParamsAndHeaders | Indicates whether the signature verifies the query parameters in the request URL | `Set<String>` |
| cosXmlResultListener      | getObjectACLAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description

The result of the request is returned through GetObjectACLResult.

| Member Variable | Type | Description |
| ------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code within the range of [200, 300) indicates a successful operation. Other values indicate a failure. |
| accessControlPolicy | [AccessControlPolicy](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/AccessControlPolicy.java) | Returns the ACL information of an object |

>If the operation fails, the SDK will throw a  [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/30599) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/30599) exception.

## Advanced APIs (Recommended)

### Uploading an object

**TransferManager** and **COSXMLUploadTask** encapsulate async requests for simple upload and multipart upload APIs and support pausing, resuming, and canceling upload requests. We recommend using this method for object upload. The sample code is as follows:

[//]: # (.cssg-snippet-transfer-upload-object)
```java
// Initialize TransferConfig
TransferConfig transferConfig = new TransferConfig.Builder().build();

If you have special requirements, you can customize the initialization as follows. For example, for an object >= 2 MB in size, use a multipart upload where each part is 1 MB in size. For a source object larger than 5 MB, use a multipart copy operation where each part is 5 MB in size.
transferConfig = new TransferConfig.Builder()
        .setDividsionForCopy(5 * 1024 * 1024) // Minimum object size for multipart copying
        .setSliceSizeForCopy(5 * 1024 * 1024) // The size of each part for multipart copying
        .setDivisionForUpload(2 * 1024 * 1024) // Minimum object size for multipart upload
        .setSliceSizeForUpload(1024 * 1024) // The size of each part for multipart upload
        .build();

// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService, transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. 
String srcPath = new File(context.getExternalCacheDir(), "exampleobject").toString(); // Absolute path to the local file
String uploadId = null; // If there is an uploadId for an initialized multipart upload, assign the value of the uploadId here to resume the upload; otherwise, assign null.
// Upload the object
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath, srcPath, uploadId);

/**
 * To upload a byte array, you can call the upload(string, string, byte[]) method of TransferManager:
 * byte[] bytes = "this is a test".getBytes(Charset.forName("UTF-8"));
 * cosxmlUploadTask = transferManager.upload(bucket, cosPath, bytes);
 */

/**
 * To upload a byte stream, you can call the upload(String, String, InputStream) method of TransferManager:
 * InputStream inputStream = new ByteArrayInputStream("this is a test".getBytes(Charset.forName("UTF-8")));
 * cosxmlUploadTask = transferManager.upload(bucket, cosPath, inputStream);
 */

// Set the upload progress callback
cosxmlUploadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long complete, long target) {
        // todo Do something to update progress...
    }
});
// Set the return result callback
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLUploadTask.COSXMLUploadTaskResult cOSXMLUploadTaskResult = (COSXMLUploadTask.COSXMLUploadTaskResult) result;
    }

    @Override
    public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
        // todo Upload failed because of CosXmlClientException or CosXmlServiceException...
    }
});
// Set the task status callback where you can view the task process
cosxmlUploadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});

/**
 If you have special requirements, please see the following operations:
 PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);
 putObjectRequest.setRegion(region); // Sets the bucket region 
 putObjectRequest.setNeedMD5(true); // Sets whether to enable MD5 checksum
 COSXMLUploadTask cosxmlUploadTask = transferManager.upload(putObjectRequest, uploadId);
 */

// Cancel upload
cosxmlUploadTask.cancel();


// Pause upload
cosxmlUploadTask.pause();

// Resume upload
cosxmlUploadTask.resume();
```

### Downloading an object

**TransferManager** and **COSXMLDownloadTask** encapsulate async requests for the download API and support pausing, resuming, and canceling download requests. It also supports resuming interrupted downloads. The sample code is as follows:

[//]: # (.cssg-snippet-transfer-download-object)
```java
Context applicationContext = context.getApplicationContext(); // application context
String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. 
String savePathDir = context.getExternalCacheDir().toString(); // Local directory path
String savedFileName = "exampleobject";// Filename of the locally-saved file. If left blank (null), then the COS filename will be used by default
// Download the object
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService, transferConfig);
COSXMLDownloadTask cosxmlDownloadTask = transferManager.download(applicationContext, bucket, cosPath, savePathDir, savedFileName);
// Set the download progress callback
cosxmlDownloadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long complete, long target) {
        // todo Do something to update progress...
    }
});
// Set the return result callback
cosxmlDownloadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLDownloadTask.COSXMLDownloadTaskResult cOSXMLDownloadTaskResult = (COSXMLDownloadTask.COSXMLDownloadTaskResult) result;
    }

    @Override
    public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
        // todo Download failed because of CosXmlClientException or CosXmlServiceException...
    }
});
// Set the task status callback where you can view the task process
cosxmlDownloadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});

/**
 If you have special requirements, please see the following operations:
 GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath, localDir, localFileName);
 getObjectRequest.setRegion(region); // Sets the  bucket region
 COSXMLDownloadTask cosxmlDownloadTask = transferManager.download(context, getObjectRequest);
 */

// Cancel download
cosxmlDownloadTask.cancel();

// Pause download
cosxmlDownloadTask.pause();

// Resume download
cosxmlDownloadTask.resume();
```

> Advanced download APIs support checkpoint restart. HEAD requests will be sent to obtain file information before download. If you are using a temporary key or accessing with a sub-account, please make sure that you have HeadObject permission.  

- Replicating oibjects

**TransferManager** and **COSXMLDownloadTask** encapsulate async requests for simple replication and multipart replication APIs and support pausing, resuming, and canceling replication requests. The sample code is as follows:

[//]: # (.cssg-snippet-transfer-copy-object)
```java
String sourceAppid = ""; // Account appid
string sourceBucket = "sourcebucket-1250000000"; // Source object bucket
string sourceRegion = "COS_REGION"; // Source object bucket region
String sourceCosPath = ""; // Source object key
// Construct source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct = new CopyObjectRequest.CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceCosPath);

String bucket = "examplebucket-1250000000"; // Bucket, format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. 

TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService, transferConfig);
// Copy Objects
COSXMLCopyTask cosxmlCopyTask = transferManager.copy(bucket, cosPath, copySourceStruct);
// Set the return result callback
cosxmlCopyTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLCopyTask.COSXMLCopyTaskResult cOSXMLCopyTaskResult = (COSXMLCopyTask.COSXMLCopyTaskResult) result;
    }

    @Override
    public void onFail(CosXmlRequest request, CosXmlClientException exception, CosXmlServiceException serviceException) {
        // todo Copy failed because of CosXmlClientException or CosXmlServiceException...
    }
});
// Set the task status callback where you can view the task process
cosxmlCopyTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
/**
 If you have special requirements, please see the following operations:
 CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath, copySourceStruct);
 copyObjectRequest.setRegion(region);  // Set the region where the bucket resides
 COSXMLCopyTask cosxmlCopyTask = transferManager.copy(copyObjectRequest);
 */

// Cancel object replication
cosxmlCopyTask.cancel();


// Pause object replication
cosxmlCopyTask.pause();

// Resume object replication
cosxmlCopyTask.resume();
```
