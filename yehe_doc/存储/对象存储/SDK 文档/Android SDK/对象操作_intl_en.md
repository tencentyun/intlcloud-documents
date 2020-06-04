## Overview

This document provides an overview of APIs for simple and multipart operations, advanced APIs, and SDK sample code related to objects.


**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/7734) | Querying object list | Queries some or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object using simple upload | Uploads an object to a bucket |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using a form | Uploads an object using a form request |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [Options Object](https://intl.cloud.tencent.com/document/product/436/8288) | Cross-origin configuration for a pre-flight request | You can initiate a pre-flight request to determine whether a real cross-origin request can be sent |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies a file to a destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deletes a single object | Deletes the specified object in the bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing multipart upload | Initializes a multipart upload operation |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading a part | Uploads a part in multipart upload |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying parts | Queries uploaded parts in the specified multipart upload |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |



## Simple Operations

### Querying object list

#### Feature

This API (GET Bucket (List Object)) is used to query some or all objects in a bucket.

#### Method prototype

```java
GetBucketResult getBucket(GetBucketRequest request) throws CosXmlClientException, CosXmlServiceException;

void getBucketAsync(GetBucketRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-get-bucket)
```java
String bucketName = "examplebucket-1250000000";  // Format: BucketName-APPID;
GetBucketRequest getBucketRequest = new GetBucketRequest(bucketName);

// Prefix match used to specify the address prefix of objects returned
getBucketRequest.setPrefix("prefix");

// For the first request, you need not set `marker`. Instead, COS will list objects from the beginning
// To get the next list of objects, set `marker` to the GetBucketResult.listBucket.nextMarker value returned from the last request
// If the returned GetBucketResult.listBucket.isTruncated value is false, all the objects that satisfy the conditions have been listed.
// getBucketRequest.setMarker(marker);

// Maximum number of entries returned at a time. Default is 1,000
getBucketRequest.setMaxKeys(100);

// The delimiter is a sign. If Prefix exists,
// the same paths between Prefix and delimiter are grouped as the same type and defined as Common Prefix,
// and then all common prefixes are listed. If there is no prefix, the listing starts from the beginning of the path
getBucketRequest.setDelimiter('/');

// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
getBucketRequest.setSignParamsAndHeaders(null, headerKeys);
// Use sync callback
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

// Prefix indicates that the object keys to be listed begin with this prefix
getBucketRequest.setPrefix("images/");
// Delimiter is a separator. Set it to "/" to list objects in the current directory; set it to null to list all objects
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
| bucket | Constructor | Bucket name. Format: BucketName-APPID | String |
| prefix | set method | Returns objects prefixed with this value. Default: null, which means returning all objects in the bucket| String |
| marker | set method | Marks the starting object of the list. It can be set to `null` for the first request, and to the `nextMarker` in the last returned listObjects value for subsequent requests | String |
| delimiter | set method | Indicates returning paths that start with "prefix" and end with the first delimiter | String |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | getBucketAsync                                                | Result callback        | CosXmlResultListener   |


#### Response description 


The result of the request is returned through GetBucketResult.

| Member Variable | Type | Description |
| ---------- | ------------------------------------------------------------ | --------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| listBucket | [ListBucket](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/ListBucket.java) | The list of objects in a bucket is returned |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).

### Uploading an object using simple upload

#### Feature

This API (PUT Object) is used to upload an object up to 5 GB to a specified bucket. To upload objects larger than 5 GB, please use [Multipart Upload](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [Advanced APIs](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89).

#### Method prototype

```java
PutObjectResult putObject(PutObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void putObjectAsync(PutObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-put-object)
```java
String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
String cosPath = "exampleobject"; //The location identifier of the object in the bucket, i.e. the object key. For example, cosPath = "text.txt";
String srcPath = new File(context.getExternalCacheDir(), "exampleobject").toString();//" Absolute path of the local file ";
PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);

putObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
putObjectRequest.setSignParamsAndHeaders(null, headerKeys);
// Upload using sync callback
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
| bucket | Constructor | Bucket name. Format: BucketName-APPID | String |
| cosPath                 | Constructor or SetCosPath                                    | The location identifier ([object key](https://intl.cloud.tencent.com/document/product/436/13324)) of the object in the bucket | String         |
| srcPath | Constructor | Absolute path to the local file uploaded to COS | String |
| data | Constructor | The array of bytes of the file uploaded to COS | byte[] |
|inputStream          | Constructor               | The byte stream of the file to be uploaded to COS                                     | InputStream                 |
| progressCallback    | setProgressListener | Sets upload progress callback                                             | CosXmlProgressListener |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | putObjectAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description 

The result of the request is returned through PutObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | String | Returns eTag of the object |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).

### Uploading an object using a form

#### Feature

This API (POST Object) is used to upload an object using a form.

#### Method prototype

```java
PostObjectResult postObject(PostObjectRequest request) throws CosXmlClientException, CosXmlServiceException；

void postObjectAsync(PostObjectRequest request, CosXmlResultListener cosXmlResultListener)；
```

#### Request samples

[//]: # (.cssg-snippet-post-object)
```java
String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
String cosPath = "exampleobject"; //The location identifier of the object in the bucket, i.e. the object key. For example, cosPath = "text.txt";
String srcPath = new File(context.getExternalCacheDir(), "exampleobject").toString();//" Absolute path of the local file ";

PostObjectRequest postObjectRequest = new PostObjectRequest(bucket, cosPath, srcPath);

postObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
postObjectRequest.setSignParamsAndHeaders(null, headerKeys);
// Upload using sync callback
try {
    PostObjectResult postObjectResult = cosXmlService.postObject(postObjectRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// Upload using async callback
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
| bucket | Constructor | Bucket name. Format: BucketName-APPID | String |
| cosPath                 | Constructor or SetCosPath                                    | The location identifier ([object key](https://intl.cloud.tencent.com/document/product/436/13324)) of the object in the bucket | String         |
| srcPath | Constructor | Absolute path to the local file uploaded to COS | String |
| data | Constructor | The array of bytes of the file uploaded to COS | byte[] |
|inputStream          | Constructor               | The byte stream of the file to be uploaded to COS                                     | InputStream                 |
| progressCallback    | setProgressListener | Sets upload progress callback                                             | CosXmlProgressListener |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | postObjectAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description 

Request result is returned through PostObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | String | Returns eTag of the object |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).

### Querying object metadata

#### Feature

This API (HEAD Object) is used to query object metadata.

#### Method prototype

```java
HeadObjectResult headObject(HeadObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void headObjectAsync(HeadObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-head-object)
```java
String bucket = bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
String cosPath = "exampleobject"; //The location identifier of the object in the bucket, i.e. the object key. 
HeadObjectRequest headObjectRequest = new HeadObjectRequest(bucket, cosPath);
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
headObjectRequest.setSignParamsAndHeaders(null, headerKeys);
// Use sync callback
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
| bucket | Constructor | Bucket name. Format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath                                    | The location identifier ([object key](https://intl.cloud.tencent.com/document/product/436/13324)) of the object in the bucket | String         |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | headObjectAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description 

Request result is returned through HeadObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | String | Returns eTag of the object |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).

### Downloading an object

#### Feature

This API (Get Object) is used to download an object.

#### Method prototype

```java
GetObjectResult getObject(GetObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void getObjectAsync(GetObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-get-object)
```java
String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
String cosPath = "exampleobject"; //The location identifier of the object in the bucket, i.e. the object key. 
String savePath = context.getExternalCacheDir().toString(); // Local path

GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath, savePath);
getObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
getObjectRequest.setSignParamsAndHeaders(null, headerKeys);
// Download using sync callback
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
| bucket | Constructor | Bucket name. Format: BucketName-APPID | String |
| cosPath                 | Constructor or SetCosPath                                    | The location identifier ([object key](https://intl.cloud.tencent.com/document/product/436/13324)) of the object in the bucket | String         |
| localDir | Constructor | The absolute path to the folder where the file is downloaded and stored locally | string |
| localDir | Constructor | The name of the file downloaded and stored locally | string |
| progressCallback    | setProgressListener | Sets upload progress callback                                             | CosXmlProgressListener |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | getObjectAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description 

The result of the request is returned through GetObjectResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | String | Returns the eTag of an object |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).

### Configuring pre-flight requests for cross-origin access

#### Feature
This API (Options Object) is used to get the cross-origin access configuration for a pre-flight request.

#### Method prototype

```java
OptionObjectResult optionObject(OptionObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void optionObjectAsync(OptionObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-option-object)
```java
String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
String cosPath = "exampleobject"; //The location identifier of the object in the bucket, i.e. the object key. 
String origin = "https://cloud.tencent.com";
String accessMethod = "PUT";
OptionObjectRequest optionObjectRequest = new OptionObjectRequest(bucket, cosPath, origin, accessMethod);
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
optionObjectRequest.setSignParamsAndHeaders(null, headerKeys);
// Use sync callback
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
| bucket | Constructor | Bucket name. Format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath                                    | The location identifier ([object key](https://intl.cloud.tencent.com/document/product/436/13324)) of the object in the bucket | String         |
| origin | Constructor or SetOrigin | Simulates the origin from which the request for cross-origin access is sent | String |
| accessMthod | Constructor or SetAccessControlMethod | Simulates the HTTP method of the request for cross-origin access | String |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | optionObjectAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description 

The result of the request is returned through DeleteObjectResult.

| Member Variable | Type | Description |
| ------------------------------- | -------------- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| accessControlAllowHeaders | `List<String>` | Allowed request headers for cross-origin access |
| accessControlAllowMethods | `List<String>` | Allowed HTTP request methods for cross-origin access |
| accessControlAllowExposeHeaders | `List<String>` | Allowed custom request headers for cross-origin access |
| accessControlMaxAge | long | The validity period of the results obtained by OPTIONS |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).

### Setting object replication

This API (PUT Object-Copy) is used to copy files to the destination path.

#### Method prototype

```java
CopyObjectResult copyObject(CopyObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void copyObjectAsync(CopyObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-copy-object)
```java
string sourceAppid = "1250000000"; // Account appid
string sourceBucket = "sourcebucket-1250000000"; // Source object bucket
string sourceRegion = "COS_REGION"; // Source object bucket region
String sourceCosPath = "sourceObject"; // Source object key
// Construct source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct = new CopyObjectRequest.CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceCosPath);
String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
String cosPath = "exampleobject"; //The location identifier of the object in the bucket, i.e. the object key. 

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath, copySourceStruct);
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
copyObjectRequest.setSignParamsAndHeaders(null, headerKeys);
// Use sync callback
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
| bucket | Constructor | Bucket name. Format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath                                    | The location identifier ([object key](https://intl.cloud.tencent.com/document/product/436/13324)) of the object in the bucket | String         |
| copySourceStruct          |  Constructor            | Describes the source path of the copied data                                         | CopySourceStruct     |
| metaDataDirective | SetCopyMetaDataDirective | Indicates whether to copy or update the metadata of the source object | MetaDataDirective |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | copyObjectAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description 

The result of the request is returned through CopyObjectResult.

| Member Variable | Type | Description |
| ---------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| copyObject | [CopyObject](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/main/java/com/tencent/cos/xml/model/tag/CopyObject.java) | The information of the object copied successfully is returned. |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).


### Deleting a single object

#### Feature

This API (Delete Object) is used to delete a specified object.

#### Method prototype

```java
DeleteObjectResult deleteObject(DeleteObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteObjectAsync(DeleteObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-delete-object)
```java
String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
String cosPath = "exampleobject"; //The location identifier of the object in the bucket, i.e. the object key. 

DeleteObjectRequest deleteObjectRequest = new DeleteObjectRequest(bucket, cosPath);
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
deleteObjectRequest.setSignParamsAndHeaders(null, headerKeys);
//  Delete using the sync callback
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
| bucket | Constructor | Bucket name. Format: BucketName-APPID | String |
| cosPath                 | Constructor or SetCosPath                                    | The location identifier ([object key](https://intl.cloud.tencent.com/document/product/436/13324)) of the object in the bucket | String         |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | getBucketLocationAsync                                                | Result callback        | CosXmlResultListener   |

#### Response description 

The result of the request is returned through DeleteObjectResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).

### Deleting multiple objects

#### Feature

This API is used to delete multiple specified objects.

#### Method prototype

```java
DeleteMultiObjectResult deleteMultiObject(DeleteMultiObjectRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteMultiObjectAsync(DeleteMultiObjectRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-delete-multi-object)
```java
String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
List<String> objectList = new ArrayList<String>();
objectList.add("exampleobject"); // The location identifier of the object in the bucket, i.e., the object key

DeleteMultiObjectRequest deleteMultiObjectRequest = new DeleteMultiObjectRequest(bucket, objectList);
deleteMultiObjectRequest.setQuiet(true);
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
deleteMultiObjectRequest.setSignParamsAndHeaders(null, headerKeys);
//  Delete using the sync callback
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
| bucket | Constructor | Bucket name. Format: BucketName-APPID | string |
| quiet | true: Only the information of the file that failed to be deleted is returned; false: The deletion result of each file is returned | Boolean | Yes |
| objectList                | The list of [object keys](https://intl.cloud.tencent.com/document/product/436/13324) to delete | `List<String>`      | Yes   |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | getBucketLocationAsync                                                | Result callback        | CosXmlResultListener   |

#### Response description 

The result of the request is returned through DeleteMultiObjectResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).


### Restoring an archived object 

#### Feature

This API (POST Object restore) is used to restore an archived object.

#### Method prototype

```java
RestoreResult restoreObject(RestoreRequest request) throws CosXmlClientException, CosXmlServiceException;

void restoreObjectAsync(RestoreRequest request,  CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-restore-object)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. For example, cosPath = "text.txt";
RestoreRequest restoreRequest = new RestoreRequest(bucket, cosPath);
restoreRequest.setExpireDays(5); // Retain for 5 days
restoreRequest.setTier(RestoreConfigure.Tier.Standard); // Standard restoration mode
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
restoreRequest.setSignParamsAndHeaders(null, headerKeys);
// Use sync callback
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
| bucket | Constructor | Bucket name. Format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath                                    | The location identifier ([object key](https://intl.cloud.tencent.com/document/product/436/13324)) of the object in the bucket | String         |
| days | SetExpireDays | Sets the number of days before a temporary copy expires | int |
| tier | SetTier | For data restores, it can be specified as one of the three restore modes supported by CAS: Expedited, Standard, and Bulk. | RestoreConfigure.Tier |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | restoreObjectAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description 

The result of the request is returned through RestoreObjectResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).


## Multipart Operations


- Multipart upload of objects: initializing multipart upload, uploading parts, and completing multipart upload
- Resuming multipart upload: querying parts uploaded, uploading parts, and completing multipart upload
- Deleting uploaded parts



### Querying multipart upload

#### Feature

This API (List Multipart Uploads) is used to query in-progress multipart uploads in the specified bucket.

#### Method prototype

```java
ListMultiUploadsResult listMultiUploads(ListMultiUploadsRequest request) throws CosXmlClientException, CosXmlServiceException;

void listMultiUploadsAsync(ListMultiUploadsRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-list-multi-upload)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
ListMultiUploadsRequest listMultiUploadsRequest = new ListMultiUploadsRequest(bucket);
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
listMultiUploadsRequest.setSignParamsAndHeaders(null, headerKeys);
try {
    // Use sync callback
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
| bucket | Constructor | Bucket name. Format: BucketName-APPID | String |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | getBucketLocationAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description 

The result of the request is returned through ListMultiUploadsResult.

| Member Variable | Type | Description |
| -------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| listMultipartUploads | [ListMultipartUploads](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/normal/java/com/tencent/cos/xml/model/tag/ListMultipartUploads.java) | The information of all in-progress multipart uploads in the bucket is returned. |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).

### <span id = "INIT_MULIT_UPLOAD">Initializing multipart upload </span>

#### Feature

This API (Initiate Multipart Upload) is used to initialize a multipart upload, and gets its uploadID.

#### Method prototype

```java
InitMultipartUploadResult initMultipartUpload(InitMultipartUploadRequest request) throws CosXmlClientException, CosXmlServiceException;

void initMultipartUploadAsync(InitMultipartUploadRequest request, CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-init-multi-upload)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. For example, cosPath = "text.txt";

InitMultipartUploadRequest initMultipartUploadRequest = new InitMultipartUploadRequest(bucket, cosPath);
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
initMultipartUploadRequest.setSignParamsAndHeaders(null, headerKeys);
// Request using sync callback
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
| bucket | Constructor | Bucket name. Format: BucketName-APPID | String |
| cosPath                 | Constructor or SetCosPath                                    | The location identifier ([object key](https://intl.cloud.tencent.com/document/product/436/13324)) of the object in the bucket | String         |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | getBucketLocationAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description 

The result of the request is returned through InitMultipartUploadResult.

| Member Variable | Type | Description |
| ------------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| initMultipartUpload | [InitiateMultipartUpload](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/main/java/com/tencent/cos/xml/model/tag/InitiateMultipartUpload.java)| Returns the object's uploadId when the multipart upload is initialized |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).



### <span id = "MULIT_UPLOAD_PART"> Uploading parts</span>

This API (Upload Part) is used to upload parts.

#### Method prototype

```java
UploadPartResult uploadPart(UploadPartRequest request) throws CosXmlClientException, CosXmlServiceException;

void uploadPartAsync(UploadPartRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-upload-part)
```java
String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
String cosPath = "exampleobject"; //The location identifier of the object in the bucket, i.e. the object key. 
string uploadId = "exampleUploadId"; // uploadId is returned when multipart upload is initialized
int partNumber = 1; // Part number, increases with increments from 1
String srcPath = new File(context.getExternalCacheDir(), "exampleobject").toString(); // Absolute path to the local file
UploadPartRequest uploadPartRequest = new UploadPartRequest(bucket, cosPath, partNumber, srcPath, uploadId);

uploadPartRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
uploadPartRequest.setSignParamsAndHeaders(null, headerKeys);
// Upload using sync callback
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
| bucket | Constructor | Bucket name. Format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath                                    | The location identifier ([object key](https://intl.cloud.tencent.com/document/product/436/13324)) of the object in the bucket | String         |
| uploadId | Constructor or SetUploadId | Identifies the specified uploadId for multipart upload | string |
| partNumber | Constructor or SetPartNumber | Identifies the number of the specified part, which should be ≥ 1. | int |
| srcPath | Constructor | Absolute path to the local file uploaded to COS | string |
| data | Constructor | The array of bytes of the file uploaded to COS | byte[] |
| progressCallback | SetCosProgressCallback | Sets the callback for upload progress | Callback.OnProgressCallback |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | uploadPartAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description 

The result of the request is returned through UploadPartResult.

| Member Variable | Type | Description |
| -------- | ------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| eTag | string | Returns the eTag of an object part |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).

### Copying parts

#### Feature

This API (Upload Part-Copy) is used to copy an object as a part.

#### Method prototype

```java
UploadPartCopyResult copyObject(UploadPartCopyRequest request) throws CosXmlClientException, CosXmlServiceException;

void copyObjectAsync(UploadPartCopyRequest request,final CosXmlResultListener cosXmlResultListener);
```
#### Request samples

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

String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
String cosPath = "exampleobject"; //The location identifier of the object in the bucket, i.e. the object key. 

String uploadId = "exampleUploadId";
int partNumber = 1; // Part number
long start = 0; //The starting part of the source object for replication
long end = 1023; //The ending part of the source object for replication

UploadPartCopyRequest uploadPartCopyRequest = new UploadPartCopyRequest(bucket, cosPath, partNumber, uploadId, copySourceStruct, start, end);
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
uploadPartCopyRequest.setSignParamsAndHeaders(null, headerKeys);
// Use sync callback
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
| bucket | Constructor | Bucket name. Format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath                                    | The location identifier ([object key](https://intl.cloud.tencent.com/document/product/436/13324)) of the object in the bucket | String         |
| copySourceStruct          |  Constructor            | Describes the source path of the copied data                                         | CopySourceStruct     |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | copyObjectAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description 

The result of the request is returned through CopyObjectResult.

| Member Variable | Type | Description |
| ---------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| copyObject | [CopyObject](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/main/java/com/tencent/cos/xml/model/tag/CopyObject.java) | The information of the object copied successfully is returned. |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).


### <span id = "LIST_MULIT_UPLOAD"> Querying parts </span>

#### Feature

This API (List Parts) is used to query the uploaded parts in a specific multipart upload.

#### Method prototype

```java
ListPartsResult listParts(ListPartsRequest request) throws CosXmlClientException, CosXmlServiceException;

void listPartsAsync(ListPartsRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-list-parts)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. For example, cosPath = "text.txt";
String uploadId = "exampleUploadId";

ListPartsRequest listPartsRequest = new ListPartsRequest(bucket, cosPath, uploadId);
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
listPartsRequest.setSignParamsAndHeaders(null, headerKeys);
// Request using sync callback
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
| bucket | Constructor | Bucket name. Format: BucketName-APPID | String |
| cosPath                 | Constructor or SetCosPath                                    | The location identifier ([object key](https://intl.cloud.tencent.com/document/product/436/13324)) of the object in the bucket | String         |
| uploadId | Constructor or SetUploadId | Identifies the specified uploadId for multipart upload | String |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | listPartsAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description 

The result of the request is returned through ListPartsResult.

| Member Variable | Type | Description |
| --------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| listParts | [ListParts](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/main/java/com/tencent/cos/xml/model/tag/ListParts.java) | The information of the parts uploaded to the specified uploadId in a multipart upload is returned |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).



### <span id = "COMPLETE_MULIT_UPLOAD"> Complete multipart upload </ span>

#### Feature

This API (Complete Multipart Upload) is used to complete the entire multipart upload.

#### Request samples
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
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
completeMultiUploadRequest.setSignParamsAndHeaders(null, headerKeys);
// Request using sync callback
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
| bucket | Constructor | Bucket name. Format: BucketName-APPID | string |
| cosPath                 | Constructor or SetCosPath                                    | The location identifier ([object key](https://intl.cloud.tencent.com/document/product/436/13324)) of the object in the bucket | String         |
| uploadId | Constructor or SetUploadId | Identifies the uploadId of the specified multipart upload | String |
| partNumber | SetPartNumberAndETag | Identifies the number of the specified part; this value should be ≥ 1. | int |
| eTag | SetPartNumberAndETag | Identifies the eTag returned when the part is uploaded | String |
| partNumberAndETags | SetPartNumberAndETag | Identifies the part number and the eTag returned when the part is uploaded |  `Dictionary<int, String> ` |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | completeMultiUploadAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description 

The result of the request is returned through CompleteMultipartUploadResult.

| Member Variable | Type | Description |
| -------------- | ------------------------------------------------------------ | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |
| CompleteResult | [CompleteMultipartUploadResult](https://github.com/tencentyun/qcloud-sdk-android/blob/master/QCloudCosXml/cosxml/src/main/java/com/tencent/cos/xml/model/tag/CompleteMultipartUploadResult.java) | Returns the information on the successful upload of all parts |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).

### <span id = "ABORT_MULIT_UPLOAD"> Abort multipart upload </ span>

#### Feature

This API (Abort Multipart Upload) is used to abort a multipart upload and delete the uploaded parts.

#### Method prototype

```java
AbortMultiUploadResult abortMultiUpload(AbortMultiUploadRequest request) throws CosXmlClientException, CosXmlServiceException;

void abortMultiUploadAsync(AbortMultiUploadRequest request, final CosXmlResultListener cosXmlResultListener);
```

#### Request samples

[//]: # (.cssg-snippet-abort-multi-upload)
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. For example, cosPath = "text.txt";
String uploadId = "exampleUploadId";

AbortMultiUploadRequest abortMultiUploadRequest = new AbortMultiUploadRequest(bucket, cosPath, uploadId);
// Set the host for signature verification, which verifies all headers by default
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
abortMultiUploadRequest.setSignParamsAndHeaders(null, headerKeys);
// Request using sync callback
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
| bucket | Constructor | Bucket name. Format: BucketName-APPID | String |
| cosPath                 | Constructor or SetCosPath                                    | The location identifier ([object key](https://intl.cloud.tencent.com/document/product/436/13324)) of the object in the bucket | String         |
| uploadId | Constructor or SetUploadId | Identifies the specified uploadId for multipart upload | String |
| headerKeys          | setSignParamsAndHeaders  | Indicates whether to verify the headers for the signature                | `Set<String>` |
| queryParameterKeys | SetSign | Indicates whether to verify the query parameters in the request URL for the signature | `Set<String>` |
| cosXmlResultListener      | abortMultiUploadAsync                                                 | Result callback        | CosXmlResultListener   |

#### Response description 

The result of the request is returned through AbortMultipartUploadResult.

| Member Variable | Type | Description |
| -------- | ---- | ---------------------------------------------------------- |
| httpCode | int | HTTP Code. A code between [200, 300) indicates a successful operation. Other values indicate a failure. |

>If the operation fails, the SDK will throw [CosXmlClientException](https://intl.cloud.tencent.com/document/product/436/31517) or [CosXmlServiceException](https://intl.cloud.tencent.com/document/product/436/31517).



## Advanced APIs (recommended)

### Uploading an object

**TransferManager** and **COSXMLUploadTask** encapsulate async requests for simple upload and multipart upload APIs and support pausing, resuming, and canceling upload requests. We recommend using this method for object upload. The sample code is as follows:

[//]: # (.cssg-snippet-transfer-upload-object)
```java
// Initialize TransferConfig
TransferConfig transferConfig = new TransferConfig.Builder().build();

If you have special requirements, you can customize the initialization as follows. For example, for an object >= 2 MB in size, use multipart upload where the size of each part is 1 MB. For a source object larger than 5 MB, use multipart copying where the size of each part is 5 MB.
transferConfig = new TransferConfig.Builder()
        .setDividsionForCopy(5 * 1024 * 1024) // Minimum object size for multipart replication
        .setSliceSizeForCopy(5 * 1024 * 1024) // The size of each part for multipart replication
        .setDivisionForUpload(2 * 1024 * 1024) // Minimum object size for multipart upload
        .setSliceSizeForUpload(1024 * 1024) // The size of each part for multipart upload
        .build();

// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService, transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. 
String srcPath = new File(context.getExternalCacheDir(), "exampleobject").toString(); // Absolute path of the local file
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

// Set upload progress callback
cosxmlUploadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long complete, long target) {
        // todo Do something to update progress...
    }
});
// Set response callback
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
// Set task status callback where you can view the task process
cosxmlUploadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});

/**
 If you have special requirements, you can write the following codes:
 PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);
 putObjectRequest.setRegion(region); // Set the region where the bucket resides
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

### Downloading an object

**TransferManager** and **COSXMLDownloadTask** encapsulate async requests for the download API and support pausing, resuming, and canceling download requests. It also supports resuming interrupted downloads. The sample code is as follows:

[//]: # (.cssg-snippet-transfer-download-object)
```java
Context applicationContext = context.getApplicationContext(); // application context
String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key. 
String savePathDir = context.getExternalCacheDir().toString(); // Local directory path
String savedFileName = "exampleobject";// Filename of the locally-saved file. If left blank (null), then the COS filename will be used by default
// Download the object
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService, transferConfig);
COSXMLDownloadTask cosxmlDownloadTask = transferManager.download(applicationContext, bucket, cosPath, savePathDir, savedFileName);
// Set download progress callback
cosxmlDownloadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long complete, long target) {
        // todo Do something to update progress...
    }
});
// Set response callback
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
 If you have special requirements, you can write the following codes:
 GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath, localDir, localFileName);
 getObjectRequest.setRegion(region); // Set the region where the bucket resides
 COSXMLDownloadTask cosxmlDownloadTask = transferManager.download(context, getObjectRequest);
 */

// Cancel download
cosxmlDownloadTask.cancel();

// Pause download
cosxmlDownloadTask.pause();

// Resume download
cosxmlDownloadTask.resume();
```

> Advanced download APIs support checkpoint restart. HEAD requests will be sent to obtain file information before download. If you are using a temporary key or accessing with a sub-account, please make sure that you have HeadObject permissions.  

- Replicating oibjects

**TransferManager** and **COSXMLDownloadTask** encapsulate async requests for simple replication and multipart replication APIs and support pausing, resuming, and canceling replication requests. The sample code is as follows:

[//]: # (.cssg-snippet-transfer-copy-object)
```java
String sourceAppid = ""; // Account appid
string sourceBucket = "sourcebucket-1250000000"; // Source object bucket
string sourceRegion = "COS_REGION"; // Source object bucket region
String sourceCosPath = ""; // Source object key
Construct source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct = new CopyObjectRequest.CopySourceStruct(sourceAppid, sourceBucket, sourceRegion, sourceCosPath);

String bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
String cosPath = "exampleobject"; //The location identifier of the object in the bucket, i.e. the object key. 

TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService, transferConfig);
Copying Objects
COSXMLCopyTask cosxmlCopyTask = transferManager.copy(bucket, cosPath, copySourceStruct);
// Set response callback
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
// Set task status callback where you can view the task process
cosxmlCopyTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
/**
 If you have special requirements, you can write the following codes:
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

