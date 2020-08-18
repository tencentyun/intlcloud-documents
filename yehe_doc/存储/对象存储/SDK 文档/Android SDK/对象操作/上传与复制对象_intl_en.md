## Overview

This document provides an overview of APIs and SDK code samples related to object upload and replication.


**Simple operations**

| API | Operation Name | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object using simple upload | Uploads an object to bucket |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using a form | Uploads an object using form request |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object (modifying object attributes) | Copies a file to a destination path |

**Multipart upload operations**

| API | Operation Name | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart upload operations | Queries in-progress multipart uploads |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload operation | Initializes a multipart upload operation |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads object parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload operation | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload operation | Aborts a multipart upload operation and deletes the uploaded parts |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Advanced APIs (Recommended)

### Uploading an object

The advanced APIs encapsulate the simple upload and multipart upload APIs and can intelligently select the upload method based on file size. They support checkpoint restart for resuming interrupted operations.

#### Sample 1. Uploading a local file

[//]: # ".cssg-snippet-transfer-upload-file"
```java
// Initialize `TransferConfig`. The default configuration is used here. If you need to customize the configuration, please see the SDK API documentation.
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize `TransferManager`
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket name in the format: `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key.
String srcPath = new File(context.getCacheDir(), "exampleobject")
        .toString(); // Absolute path of the local file
// If there is an `uploadId` for an initialized multipart upload, assign the value of the `uploadId` here to resume the upload; otherwise, assign `null`.
String uploadId = null;

// Upload the file
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(bucket, cosPath,
        srcPath, uploadId);

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
// Set the job status callback where you can view the job progress
cosxmlUploadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
```

>?
>- For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java).
>- After an object is uploaded, you can use the same key to generate a file download link as instructed in [Generating a Pre-signed Link](https://intl.cloud.tencent.com/document/product/436/37680). However, please note that if your file is set to private-read, the download link will only be valid for a certain period of time.

#### Sample 2. Uploading binary data

[//]: # ".cssg-snippet-transfer-upload-bytes"
```java
TransferConfig transferConfig = new TransferConfig.Builder().build();
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket name in the format: `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key.

// Upload the byte array
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
>- For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java) .
>- After an object is uploaded, you can use the same key to generate a file download link as instructed in [Generating a Pre-signed Link](https://intl.cloud.tencent.com/document/product/436/37680). However, please note that if your file is set to private-read, the download link will only be valid for a certain period of time.

#### Sample 3. Stream upload

[//]: # ".cssg-snippet-transfer-upload-stream"
```java
TransferConfig transferConfig = new TransferConfig.Builder().build();
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket name in the format: `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key.

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
>- For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java).
>- After an object is uploaded, you can use the same key to generate a file download link as instructed in [Generating a Pre-signed Link](https://intl.cloud.tencent.com/document/product/436/37680). However, please note that if your file is set to private-read, the download link will only be valid for a certain period of time.

### Copying an object

The advanced APIs encapsulate async requests for the simple copy and multipart copy APIs and support pausing, resuming, and canceling copy requests.

#### Sample code

[//]: # ".cssg-snippet-transfer-copy-object"
```java
// Initialize `TransferConfig`. The default configuration is used here. If you need to customize the configuration, please see the SDK API documentation.
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize `TransferManager`
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String sourceAppid = "1250000000"; // Account `APPID`
String sourceBucket = "sourcebucket-1250000000"; // Source object bucket
String sourceRegion = "COS_REGION"; // Source object bucket region
String sourceCosPath = "sourceObject"; // Source object key
// Construct the source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
        sourceAppid, sourceBucket, sourceRegion, sourceCosPath);
// Destination bucket
String bucket = "examplebucket-1250000000"; // Bucket name in the format: `BucketName-APPID`
// Destination object
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key

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
// Set the job status callback where you can view the job progress
cosxmlCopyTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java).

## Simple Operations

### Uploading an object using simple upload

#### Feature description

This API is used to upload an object to a specified bucket. This operation requires the requester to have WRITE permission for the bucket and can upload a file of up to 5 GB in size. For larger files, please use [multipart upload](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [advanced APIs](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89).

> !
> 1. The `Key` (filename) cannot end in `/`; otherwise, it will be recognized as a folder.
> 2. The total number of bucket ACL rules under a single root account (i.e., under the same `APPID`) cannot exceed 1,000. There is no upper limit on the number of object ACL rules. If you do not need access control for an object, you can choose not to configure an ACL for the object during upload, and the object will inherit the permissions of its bucket by default.

#### Sample code

[//]: # ".cssg-snippet-put-object"
```java
String bucket = "examplebucket-1250000000"; // Bucket name in the format: `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key.
String srcPath = new File(context.getCacheDir(), "exampleobject")
        .toString();//"Absolute path of local file";
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
>- After an object is uploaded, you can use the same key to generate a file download link as instructed in [Generating a Pre-signed Link](https://intl.cloud.tencent.com/document/product/436/37680). However, please note that if your file is set to private-read, the download link will only be valid for a certain period of time.

### Uploading an object using a form

#### Feature description

This API is used to upload an object by using a form.

#### Sample code

[//]: # ".cssg-snippet-post-object"
```java
String bucket = "examplebucket-1250000000"; // Bucket name in the format: `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key.
String srcPath = new File(context.getCacheDir(), "exampleobject")
        .toString();//"Absolute path of local file";

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

### Copying an object (modifying attributes)

This API is used to copy a file to a destination path.

#### Sample 1. Copying an object while retaining its attributes

[//]: # ".cssg-snippet-copy-object"
```java
String sourceAppid = "1250000000"; // Account `APPID`
String sourceBucket = "sourcebucket-1250000000"; // Source object bucket
String sourceRegion = "COS_REGION"; // Source object bucket region
String sourceCosPath = "sourceObject"; // Source object key
// Construct the source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
        sourceAppid, sourceBucket, sourceRegion, sourceCosPath);

String bucket = "examplebucket-1250000000"; // Bucket name in the format: `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
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

#### Sample 2. Copying an object while replacing its attributes

[//]: # ".cssg-snippet-copy-object-replaced"
```java
String sourceAppid = "1250000000"; // Account `APPID`
String sourceBucket = "sourcebucket-1250000000"; // Source object bucket
String sourceRegion = "COS_REGION"; // Source object bucket region
String sourceCosPath = "sourceObject"; // Source object key
// Construct the source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
        sourceAppid, sourceBucket, sourceRegion, sourceCosPath);

String bucket = "examplebucket-1250000000"; // Bucket name in the format: `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
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

#### Sample 3. Modifying object metadata

[//]: # ".cssg-snippet-modify-object-metadata"
```java
String appId = "1250000000"; // Account `APPID`
String bucket = "examplebucket-1250000000"; // Bucket name in the format: `BucketName-APPID`
String region = "COS_REGION"; // Source object bucket region
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
// Construct the source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
        appId, bucket, region, cosPath);

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath,
        copySourceStruct);
copyObjectRequest.setCopyMetaDataDirective(MetaDataDirective.REPLACED);
// Replace the object metadata with new values
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

#### Sample 4. Changing the object storage class

[//]: # ".cssg-snippet-modify-object-storage-class"
```java
String appId = "1250000000"; // Account `APPID`
String bucket = "examplebucket-1250000000"; // Bucket name in the format: `BucketName-APPID`
String region = "COS_REGION"; // Source object bucket region
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
// Construct the source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
        appId, bucket, region, cosPath);

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucket, cosPath,
        copySourceStruct);
// Change to STANDARD_IA storage class
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

#### How to perform a multipart upload/copy operation

1. Initialize a multipart upload through `Initiate Multipart Upload` and get the `UploadId`.
2. Use the `UploadId` to upload parts through `Upload Part` or copy parts through `Upload Part Copy`.
3. Complete the multipart upload with `Complete Multipart Upload`.

#### How to resume a multipart upload/copy operation

1. If you did not record the `UploadId` of the multipart upload, you can query the multipart upload job with `List Multipart Uploads` to get the `UploadId` of the corresponding file.
2. Use the `UploadId` to list the uploaded parts with `List Parts`.
2. Use the `UploadId` to upload the remaining parts with `Upload Part` or copy the remaining parts with `Upload Part Copy`.
3. Complete the multipart upload with `Complete Multipart Upload`.

#### How to abort a multipart upload/copy operation

1. If you did not record the `UploadId` of the multipart upload, you can query the multipart upload job with `List Multipart Uploads` to get the `UploadId` of the corresponding file.
2. Abort the multipart upload and delete the uploaded parts with `Abort Multipart Upload`.

### Querying multipart upload operations

#### Feature description

This API is used to query in-progress multipart uploads in a specified bucket.

#### Sample code

[//]: # ".cssg-snippet-list-multi-upload"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
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

### Initializing a multipart upload operation

#### Feature description

This API is used to initialize a multipart upload operation and get its `uploadID`.

#### Sample code

[//]: # ".cssg-snippet-init-multi-upload"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key

InitMultipartUploadRequest initMultipartUploadRequest =
        new InitMultipartUploadRequest(bucket, cosPath);
cosXmlService.initMultipartUploadAsync(initMultipartUploadRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        // `uploadId` of the multipart upload
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

### Uploading parts

This API is used to upload parts.

#### Sample code

[//]: # ".cssg-snippet-upload-part"
```java
String bucket = "examplebucket-1250000000"; // Bucket name in the format: `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
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

### Copying a part

#### Feature description

This API is used to copy an object as a part.

#### Sample code

[//]: # ".cssg-snippet-upload-part-copy"
```java
String sourceAppid = "1250000000"; // Account `APPID`
String sourceBucket = "sourcebucket-1250000000"; // Source object bucket
String sourceRegion = "COS_REGION"; // Source object bucket region
String sourceCosPath = "sourceObject"; // Source object key
// Construct the source object attributes
CopyObjectRequest.CopySourceStruct copySourceStruct =
        new CopyObjectRequest.CopySourceStruct(
        sourceAppid, sourceBucket, sourceRegion, sourceCosPath);

String bucket = "examplebucket-1250000000"; // Bucket name in the format: `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key

String uploadId = "exampleUploadId";
int partNumber = 1; // Part number
long start = 0; // Starting part of the source object to be copied
long end = 1023; // Ending part of the source object to be copied

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

#### Feature description

This API is used to query the uploaded parts of a specified multipart upload operation.

#### Sample code

[//]: # ".cssg-snippet-list-parts"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key

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

### Completing a multipart upload operation

#### Feature description

This API is used to complete the multipart upload of the entire file.

#### Sample code
[//]: # ".cssg-snippet-complete-multi-upload"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key

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

### Aborting a multipart upload operation

#### Feature description

This API is used to abort a multipart upload operation and delete the uploaded parts.

#### Sample code

[//]: # ".cssg-snippet-abort-multi-upload"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key

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
