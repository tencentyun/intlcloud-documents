## Overview

This document provides an overview of APIs and SDK sample codes related to uploading and replicating objects.


**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object | Uploads an object to a bucket. |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using an HTML form | Uploads an object using an HTML form. |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object (modifying object attributes) | Copies a file to a destination path |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload operation | Initializes a multipart upload operation |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads an object in multiple parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying an object part | Copies a part of an object. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a multipart upload. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of a file. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts. |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Advanced APIs (Recommended)

### Uploading an object

The advanced APIs encapsulate the simple upload and multipart upload APIs and can intelligently select the upload method based on file size. They also support checkpoint restart for resuming interrupted operations.

#### Sample code 1. Uploading a local file

[//]: # (.cssg-snippet-transfer-upload-file)
```java
// Initialize TransferConfig. The default configuration is used here. To customize the configuration, please see the SDK API documentation.
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize TransferManager.
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket, formatted as `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
String srcPath = new File(context.getCacheDir(), "exampleobject")
        .toString(); // Absolute path of the local file
// If there is an uploadId for the initialized multipart upload, assign the value of uploadId here to resume the upload. Otherwise, assign null
String uploadId = null;
PutObjectRequest putObjectRequest= new PutObjectRequest(bucket, cosPath, srcPath);
// Set the storage class for the object to upload.
putObjectRequest.setStroageClass(COSStorageClass.STANDARD);
// Upload the object
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(putObjectRequest, uploadId);

// Set the upload progress callback
cosxmlUploadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long complete, long target) {
        // todo Do something to update progress...
    }
});
// Set the response callback
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLUploadTask.COSXMLUploadTaskResult cOSXMLUploadTaskResult =
                (COSXMLUploadTask.COSXMLUploadTaskResult) result;
    }

    @Override
    public void onFail(CosXmlRequest request,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
// Set the job status callback to view the job progress
cosxmlUploadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
```

>?
>- For the complete sample, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java).
>- You can generate a download URL for the uploaded file using the same key. For detailed directions, please see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

#### Sample code 2. Uploading binary data

[//]: # (.cssg-snippet-transfer-upload-bytes)
```java
TransferConfig transferConfig = new TransferConfig.Builder().build();
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket, formatted as `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key

// Upload a byte array
byte[] bytes = "this is a test".getBytes(Charset.forName("UTF-8"));
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath,
        bytes);

// Set the response callback
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLUploadTask.COSXMLUploadTaskResult cOSXMLUploadTaskResult =
                (COSXMLUploadTask.COSXMLUploadTaskResult) result;
    }

    @Override
    public void onFail(CosXmlRequest request,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?
>- For the complete sample, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java).
>- You can generate a download URL for the uploaded file using the same key. For detailed directions, please see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

#### Sample code 3. Stream upload

[//]: # (.cssg-snippet-transfer-upload-stream)
```java
TransferConfig transferConfig = new TransferConfig.Builder().build();
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket, formatted as `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key

// Stream upload
InputStream inputStream =
        new ByteArrayInputStream("this is a test".getBytes(Charset.forName(
                "UTF-8")));
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath,
        inputStream);

// Set the response callback
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLUploadTask.COSXMLUploadTaskResult cOSXMLUploadTaskResult =
                (COSXMLUploadTask.COSXMLUploadTaskResult) result;
    }

    @Override
    public void onFail(CosXmlRequest request,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?
>- For the complete sample, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java).
>- You can generate a download URL for the uploaded file using the same key. For detailed directions, please see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

#### Sample code 4. Uploading using a URI

[//]: # (.cssg-snippet-transfer-upload-uri)
```java
TransferConfig transferConfig = new TransferConfig.Builder().build();
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket, formatted as `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key

// URI of the file
Uri uri = Uri.parse("exampleObject");
// If there is an `uploadId` for an initialized multipart upload, assign the value of the `uploadId` here to resume the upload; otherwise, assign `null`
String uploadId = null;
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath,
        uri, uploadId);

// Set the response callback
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLUploadTask.COSXMLUploadTaskResult cOSXMLUploadTaskResult =
                (COSXMLUploadTask.COSXMLUploadTaskResult) result;
    }

    @Override
    public void onFail(CosXmlRequest request,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?
>- For the complete sample, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java).
>- You can generate a download URL for the uploaded file using the same key. For detailed directions, please see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

#### Sample code 5. Setting the threshold for smart multipart upload

By default, TransferManager automatically executes multipart upload for files whose sizes are equal to or greater than 2 MB. You can use the following code to change the multipart upload threshold:

```
TransferConfig transferConfig = new TransferConfig.Builder()
	.setDivisionForUpload(2 * 1024 * 1024) // Set multipart upload for files whose sizes are equal to or greater than 2 MB 
	.build();
	
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);	
```


#### Sample code 6. Suspending, resuming, and canceling an upload

To suspend an upload, use the code below:

[//]: # (.cssg-snippet-transfer-upload-pause)
```java
// If the final Complete Multipart Upload request has been initiated, the suspension will fail.
boolean pauseSuccess = cosxmlUploadTask.pauseSafely();
```

To resume a suspended download, use the code below:

[//]: # (.cssg-snippet-transfer-upload-resume)
```java
// A suspended upload can be resumed.
if (pauseSuccess) {
    cosxmlUploadTask.resume();
}
```

To cancel an upload, use the code below:

[//]: # (.cssg-snippet-transfer-upload-cancel)
```java
cosxmlUploadTask.cancel();
```

>?
>- For the complete sample, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java).

#### Sample code 7. Uploading multiple objects

[//]: # (.cssg-snippet-transfer-batch-upload-objects)
```java
// Absolute paths to the local files
File[] files = new File(context.getCacheDir(), "exampleDirectory").listFiles();

// Initiate a batch upload
for (File file : files) {
    // If there is an uploadId for the initialized multipart upload, assign the value of uploadId here to resume the upload. Otherwise, assign null
    String uploadId = null;

    // Upload the object
    COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath,
            file.getAbsolutePath(), uploadId);

    // Set the response callback
    cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
        @Override
        public void onSuccess(CosXmlRequest request, CosXmlResult result) {
            COSXMLUploadTask.COSXMLUploadTaskResult cOSXMLUploadTaskResult =
                    (COSXMLUploadTask.COSXMLUploadTaskResult) result;
        }

        @Override
        public void onFail(CosXmlRequest request,
                           CosXmlClientException clientException,
                           CosXmlServiceException serviceException) {
            if (clientException != null) {
                clientException.printStackTrace();
            } else {
                serviceException.printStackTrace();
            }
        }
    });
}
```

#### Sample code 8. Creating a directory

[//]: # (.cssg-snippet-create-directory)
```java
String bucket = "examplebucket-1250000000"; // Bucket, formatted as `BucketName-APPID`
// The location identifier of a directory in a bucket (i.e., the object key), which must end with a slash (/).
String cosPath = "exampleobject/";
PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, new byte[0]);
cosXmlService.putObjectAsync(putObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutObjectResult putObjectResult =
                (PutObjectResult) result;
    }

    @Override
    public void onFail(CosXmlRequest request,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?
>- For the complete sample, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java).
>- You can generate a download URL for the uploaded file using the same key. For detailed directions, please see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

### Setting a low-priority task

You can call `setPriorityLow()` to set a task to a low-priority one (for example, for a task that uploads logs in the backend). In this way, you can prevent tasks from being suspended due to threads being occupied.


```
PutObjectRequest putObjectRequest= new PutObjectRequest(bucket, key, filePath);
putObjectRequest.setPriorityLow(); // Set the priority of the task to low.
final COSXMLUploadTask uploadTask = transferManager.upload(putObjectRequest, null);
uploadTask.setCosXmlResultListener(new CosXmlResultListener() {
      @Override
      public void onSuccess(CosXmlRequest request, CosXmlResult result) {}
			

     @Override
      public void onFail(CosXmlRequest request, CosXmlClientException clientException, CosXmlServiceException serviceException) {}
});
```


### Setting a timeout

You can use the `startTimeoutTimer()` method to start a timer. In this way, if a task is not performed within the specified period, it will be canceled, and the `onFailed` method will be called back.


```
PutObjectRequest putObjectRequest= new PutObjectRequest(bucket, key, filePath);
final COSXMLUploadTask uploadTask = transferManager.upload(putObjectRequest, null);
uploadTask.startTimeoutTimer(1000); // Set the timeout to 1,000 ms (1 second).
uploadTask.setCosXmlResultListener(new CosXmlResultListener() {
      @Override
      public void onSuccess(CosXmlRequest request, CosXmlResult result) {}
			

     @Override
      public void onFail(CosXmlRequest request, CosXmlClientException clientException, CosXmlServiceException serviceException) {}
});
```



### Copying objects

The advanced APIs encapsulate async requests for the simple copy and multipart copy APIs and support pausing, resuming, and canceling copy requests.

#### Sample code

[//]: # (.cssg-snippet-transfer-copy-object)
```java
// Initialize TransferConfig. The default configuration is used here. To customize the configuration, please see the SDK API documentation.
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String sourceAppid = "1250000000"; // Account APPID
String sourceBucket = "sourcebucket-1250000000"; // Bucket of the source object
String sourceRegion = "COS_REGION"; // Region where the bucket of the source object resides
String sourceCosPath = "sourceObject"; // Key of the source object
// Construct the source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
                sourceAppid, sourceBucket, sourceRegion, sourceCosPath);
// Destination bucket
String bucket = "examplebucket-1250000000"; // Bucket, formatted as `BucketName-APPID`
// Destination object
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key

// Copy the object
COSXMLCopyTask cosxmlCopyTask = transferManager.copy(bucket, cosPath,
        copySourceStruct);

// Set the response callback
cosxmlCopyTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLCopyTask.COSXMLCopyTaskResult cOSXMLCopyTaskResult =
                (COSXMLCopyTask.COSXMLCopyTaskResult) result;
    }

    @Override
    public void onFail(CosXmlRequest request,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
// Set the job status callback to view the job progress
cosxmlCopyTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferCopyObject.java).

## Simple Operations

### Uploading an object using simple upload

#### Description

This API (PUT Object) is used to upload an object smaller than 5 GB to a specified bucket. To call this API, you need to have permission to write the bucket. If the object size is larger than 5 GB, please use [Multipart Upload](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [Advanced APIs](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) for the upload.

> !
> 1. The Key (filename) cannot end with `/`; otherwise, it will be identified as a folder.
> 2. Each root account (`AAPID`) can have up to 1,000 bucket ACLs and an unlimited number of object ACLs. If you do not need an ACL for an object, you can choose not to configure an ACL for the object during upload. In this way, the object will inherit the permissions of its bucket by default.

#### Sample code

[//]: # (.cssg-snippet-put-object)
```java
String bucket = "examplebucket-1250000000"; // Bucket, formatted as `BucketName-APPID`
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key
String srcPath = new File(context.getCacheDir(), "exampleobject")
        .toString(); // The absolute path of the local file
PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath,
        srcPath);

putObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});
cosXmlService.putObjectAsync(putObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        PutObjectResult putObjectResult = (PutObjectResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?
>- For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/PutObject.java).
>- You can generate a download URL for the uploaded file using the same key. For detailed directions, please see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

### Uploading an object using an HTML form

#### Description

This API is used to upload an object using an HTML form.

#### Sample code

[//]: # (.cssg-snippet-post-object)
```java
String bucket = "examplebucket-1250000000"; // Bucket, formatted as BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key
String srcPath = new File(context.getCacheDir(), "exampleobject")
        .toString(); // The absolute path of the local file

PostObjectRequest postObjectRequest = new PostObjectRequest(bucket, cosPath,
        srcPath);

postObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});
cosXmlService.postObjectAsync(postObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        PutObjectResult putObjectResult = (PutObjectResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/PostObject.java).

### Copying an object (modifying object attributes)

This API (PUT Object-Copy) is used to copy an object to a destination path.

#### Sample code 1: Copying an object with its attributes preserved

[//]: # (.cssg-snippet-copy-object)
```java
String sourceAppid = "1250000000"; // Account APPID
String sourceBucket = "sourcebucket-1250000000"; // Bucket of the source object
String sourceRegion = "COS_REGION"; // Region where the bucket of the source object resides
String sourceCosPath = "sourceObject"; // Key of the source object
// Construct the source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
        sourceAppid, sourceBucket, sourceRegion, sourceCosPath);

String bucket = "examplebucket-1250000000"; // Bucket, formatted as `BucketName-APPID`
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath,
        copySourceStruct);

cosXmlService.copyObjectAsync(copyObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        CopyObjectResult copyObjectResult = (CopyObjectResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/CopyObject.java).

#### Sample code 2: Copying an object while replacing its attributes

[//]: # (.cssg-snippet-copy-object-replaced)
```java
String sourceAppid = "1250000000"; // Account APPID
String sourceBucket = "sourcebucket-1250000000"; // Bucket of the source object
String sourceRegion = "COS_REGION"; // Region where the bucket of the source object resides
String sourceCosPath = "sourceObject"; // Key of the source object
// Construct the source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
        sourceAppid, sourceBucket, sourceRegion, sourceCosPath);

String bucket = "examplebucket-1250000000"; // Bucket, formatted as `BucketName-APPID`
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath,
        copySourceStruct);
copyObjectRequest.setCopyMetaDataDirective(MetaDataDirective.REPLACED);
copyObjectRequest.setXCOSMeta("x-cos-metadata-oldKey", "newValue");

cosXmlService.copyObjectAsync(copyObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        CopyObjectResult copyObjectResult = (CopyObjectResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/CopyObject.java).

#### Sample code 3: Modifying object metadata

[//]: # (.cssg-snippet-modify-object-metadata)
```java
String appId = "1250000000"; // Account APPID
String bucket = "examplebucket-1250000000"; // Bucket, formatted as `BucketName-APPID`
String region = "COS_REGION"; // Region where the bucket of the source object resides
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key
// Construct the source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
        appId, bucket, region, cosPath);

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath,
        copySourceStruct);
copyObjectRequest.setCopyMetaDataDirective(MetaDataDirective.REPLACED);
// Replace metadata
copyObjectRequest.setXCOSMeta("x-cos-metadata-oldKey", "newValue");

cosXmlService.copyObjectAsync(copyObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        CopyObjectResult copyObjectResult = (CopyObjectResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ModifyObjectProperty.java).

#### Sample code 4: Modifying the storage class of an object

[//]: # (.cssg-snippet-modify-object-storage-class)
```java
String appId = "1250000000"; // Account APPID
String bucket = "examplebucket-1250000000"; // Bucket, formatted as `BucketName-APPID`
String region = "COS_REGION"; // Region where the bucket of the source object resides
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key
// Construct the source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
        appId, bucket, region, cosPath);

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath,
        copySourceStruct);
// Set the storage class to STANDARD_IA
copyObjectRequest.setCosStorageClass(COSStorageClass.STANDARD_IA);

cosXmlService.copyObjectAsync(copyObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        CopyObjectResult copyObjectResult = (CopyObjectResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ModifyObjectProperty.java).

## Multipart Operations

The multipart upload process is outlined below.

#### Multipart upload/copy process

1. Initialize the multipart upload with `Initiate Multipart Upload` and get the `UploadId`.
2. Use the `UploadId` to upload parts with `Upload Part` or copy parts with `Upload Part Copy`
3. Complete the multipart upload with `Complete Multipart Upload`.

#### How to resume a multipart upload/copy operation

1. If you did not record the `UploadId` of the multipart upload, you can query the multipart upload job with `List Multipart Uploads` to get the `UploadId` of the corresponding file.
2. Use the `UploadId` to list the uploaded parts with `List Parts`.
3. Use the `UploadId` to upload the remaining parts with `Upload Part` or copy the remaining parts with `Upload Part Copy`.
4. Complete the multipart upload with `Complete Multipart Upload`.

#### How to abort a multipart upload/copy operation

1. If you did not record the `UploadId` of the multipart upload, you can query the multipart upload job with `List Multipart Uploads` to get the `UploadId` of the corresponding file.
2. Abort the multipart upload and delete the uploaded parts with `Abort Multipart Upload`.

### Querying multipart uploads

#### Description

This API (`List Multipart Uploads`) is used to query in-progress multipart uploads in a specified bucket.

#### Sample code

[//]: # (.cssg-snippet-list-multi-upload)
```java
String bucket = "examplebucket-1250000000"; // Bucket, formatted as BucketName-APPID
ListMultiUploadsRequest listMultiUploadsRequest =
        new ListMultiUploadsRequest(bucket);
cosXmlService.listMultiUploadsAsync(listMultiUploadsRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        ListMultiUploadsResult listMultiUploadsResult =
                (ListMultiUploadsResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/MultiPartsUploadObject.java).

### Initializing a multipart upload

#### Description

This API is used to initialize a multipart upload operation and get its `uploadId`.

#### Sample code
g
[//]: # (.cssg-snippet-init-multi-upload)
```java
String bucket = "examplebucket-1250000000"; // Bucket, formatted as BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key

InitMultipartUploadRequest initMultipartUploadRequest =
        new InitMultipartUploadRequest(bucket, cosPath);
cosXmlService.initMultipartUploadAsync(initMultipartUploadRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        // UploadId of the multipart upload
        uploadId = ((InitMultipartUploadResult) result)
                .initMultipartUpload.uploadId;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/MultiPartsUploadObject.java).

###  Uploading parts

This API (`Upload Part`) is used to upload an object in parts.

#### Sample code

[//]: # (.cssg-snippet-upload-part)
```java
String bucket = "examplebucket-1250000000"; // Bucket, formatted as `BucketName-APPID`
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key
UploadPartRequest uploadPartRequest = new UploadPartRequest(bucket, cosPath,
        partNumber, srcFile.getPath(), offset, PART_SIZE, uploadId);

uploadPartRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});

cosXmlService.uploadPartAsync(uploadPartRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        String eTag = ((UploadPartResult) result).eTag;
        eTags.put(partNumber, eTag);
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/MultiPartsUploadObject.java).

### Copying an object part

#### Description

This API is used to copy an object as a part.

#### Sample code

[//]: # (.cssg-snippet-upload-part-copy)
```java
String sourceAppid = "1250000000"; // Account APPID
String sourceBucket = "sourcebucket-1250000000"; // Bucket of the source object
String sourceRegion = "COS_REGION"; // Region where the bucket of the source object resides
String sourceCosPath = "sourceObject"; // Key of the source object
// Construct the source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
        sourceAppid, sourceBucket, sourceRegion, sourceCosPath);

String bucket = "examplebucket-1250000000"; // Bucket, formatted as `BucketName-APPID`
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key

String uploadId = "exampleUploadId";
int partNumber = 1; // Part number
long start = 0; //The starting part of the source object to be copied
long end = 1023; //The ending part of the source object to be copied

UploadPartCopyRequest uploadPartCopyRequest =
        new UploadPartCopyRequest(bucket, cosPath,
        partNumber, uploadId, copySourceStruct, start, end);
cosXmlService.copyObjectAsync(uploadPartCopyRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        UploadPartCopyResult uploadPartCopyResult =
                (UploadPartCopyResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/MultiPartsCopyObject.java).

### Querying uploaded parts

#### Description

This API (`List Parts`) is used to query the uploaded parts of a multipart upload.

#### Sample code

[//]: # (.cssg-snippet-list-parts)
```java
String bucket = "examplebucket-1250000000"; // Bucket, formatted as BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key

ListPartsRequest listPartsRequest = new ListPartsRequest(bucket, cosPath,
        uploadId);
cosXmlService.listPartsAsync(listPartsRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        ListParts listParts = ((ListPartsResult) result).listParts;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/MultiPartsUploadObject.java).

### Completing a multipart upload

#### Description

This API (`Complete Multipart Upload`) is used to complete the multipart upload of a file.

#### Sample code
[//]: # (.cssg-snippet-complete-multi-upload)
```java
String bucket = "examplebucket-1250000000"; // Bucket, formatted as BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key

CompleteMultiUploadRequest completeMultiUploadRequest =
        new CompleteMultiUploadRequest(bucket,
        cosPath, uploadId, eTags);
cosXmlService.completeMultiUploadAsync(completeMultiUploadRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        CompleteMultiUploadResult completeMultiUploadResult =
                (CompleteMultiUploadResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/MultiPartsUploadObject.java).

### Aborting a multipart upload

#### Description

This API (`Abort Multipart Upload`) is used to abort a multipart upload and delete the uploaded parts.

#### Sample code

[//]: # (.cssg-snippet-abort-multi-upload)
```java
String bucket = "examplebucket-1250000000"; // Bucket, formatted as BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key

AbortMultiUploadRequest abortMultiUploadRequest =
        new AbortMultiUploadRequest(bucket,
        cosPath, uploadId);
cosXmlService.abortMultiUploadAsync(abortMultiUploadRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        AbortMultiUploadResult abortMultiUploadResult =
                (AbortMultiUploadResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/AbortMultiPartsUpload.java).

