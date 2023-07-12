## Overview

This document provides an overview of APIs and SDK code samples for object uploading.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object](https://www.tencentcloud.com/document/product/436/7749) | Simply uploading an object | Uploads an object to a bucket |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://www.tencentcloud.com/document/product/436/7736) | Querying multipart uploads | Queries the information on ongoing multipart uploads |
| [Initiate Multipart Upload](https://www.tencentcloud.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload |
| [Upload Part](https://www.tencentcloud.com/document/product/436/7750) | Uploading a part | Uploads a part in multipart upload |
| [List Parts](https://www.tencentcloud.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in a specified multipart upload operation |
| [Complete Multipart Upload](https://www.tencentcloud.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://www.tencentcloud.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

### Uploading an object

It encapsulates the simple upload and multipart upload APIs and can intelligently select the upload method based on file size. It also supports checkpoint restart for resuming interrupted operations.

#### Sample. Uploading a local file

```dart
    // Bucket region abbreviation. For example, "ap-guangzhou" is the abbreviation of the Guangzhou region
    String region = "COS_REGION";
    // Create a `CosXmlServiceConfig` object and modify the configuration parameters as needed
    CosXmlServiceConfig serviceConfig = CosXmlServiceConfig(
        region: region,
        isDebuggable: true,
        isHttps: true,
    );
    // Create a `TransferConfig` object and modify the configuration parameters as needed
    // You can set the object size threshold for multipart upload in `TransferConfig`. By default, the system automatically executes multipart upload for files whose sizes are greater than or equal to 2 MB. You can use the following code to change the threshold:
    TransferConfig transferConfig = TransferConfig(
        forceSimpleUpload: false,
        enableVerification: true,
        divisionForUpload: 2097152, // Set multipart upload for files whose sizes are greater than or equal to 2 MB
        sliceSizeForUpload: 1048576, // Set the default part size to 1 MB
    );
    // Register the default COS TransferManger
    await Cos().registerDefaultTransferManger(serviceConfig, transferConfig);

    // Get the `TransferManager`
    CosTransferManger transferManager = Cos().getDefaultTransferManger();
    //CosTransferManger transferManager = Cos().getTransferManger("newRegion");
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    String bucket = "examplebucket-1250000000";
    String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
    String srcPath = "Absolute path of the local file"; // Absolute path of the local file
    // If there is an uploadId for the initialized multipart upload, assign the value of uploadId here to resume the upload. Otherwise, assign null
    String? _uploadId;

    // Callback for successful upload
    successCallBack(result) {
      // TODO: Logic after successful upload
    }
    // Callback for failed upload
    failCallBack(clientException, serviceException) {
      // TODO: Logic after failed upload
      if (clientException != null) {
        print(clientException);
      }
      if (serviceException != null) {
        print(serviceException);
      }
    }
    // Callback for the upload status, through which you can check the task process
    stateCallback(state) {
      // todo notify transfer state
    }
    // Callback for the upload progress
    progressCallBack(complete, target) {
      // todo Do something to update progress...
    }
    // Callback for the completion of multipart upload initialization
    initMultipleUploadCallback(
        String bucket, String cosKey, String uploadId) {
      //The uploadId required for the subsequent checkpoint restarts
      _uploadId = uploadId;
    }
    // Start the upload
    TransferTask transferTask = await transferManager.upload(bucket, cosPath,
        filePath: srcPath,
        uploadId: _uploadId,
        resultListener: ResultListener(successCallBack, failCallBack),
        stateCallback: stateCallback,
        progressCallBack: progressCallBack,
        initMultipleUploadCallback: initMultipleUploadCallback
    );
    // Pause the task
    transferTask.pause();
    // Resume the task
    transferTask.resume();
    // Cancel the task
    transferTask.cancel();
```

#### Parameter description

`TransferConfig` is used to configure the COS upload service and has the following members:

| Parameter  | Description | Type | Default Value | Supported Platform |
| ---------- | ------------------------------------------------------------ | ------ | ------ |------ |
| divisionForUpload | Sets the minimum object size to enable multipart upload | Int | 2097152 | Android, iOS |
| sliceSizeForUpload | Sets the part size during multipart upload  | Int | 1048576 | Android, iOS |
| enableVerification | Whether to verify the entire object during multipart upload | Bool | true | Android, iOS |
| forceSimpleUpload | Whether to forcibly use simple upload | Bool | false | Android |

Parameters of the `upload` method

| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ | ------ |
| bucket | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| cosPath | Object key, which uniquely identifies an object in a bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, its key is `doc/picture.jpg`. | String | Yes |
| filePath | Path of the local file to be uploaded (either it or `byteArr` must be specified) | String | No |
| byteArr | The byte array to be uploaded (either it or `filePath` must be specified) | Uint8List | No |
| uploadId | Assigns the value of `uploadId` here to resume the upload if there is an `uploadId` for the initialized multipart upload. | String | No |
| stroageClass | Storage class | String | No |
| trafficLimit | Bandwidth limit for a single request in bit/s. Value range: 819200–838860800, i.e., 100 KB/s - 100 MB/s. | Int | No |
| ResultListener | Callback for the upload result (including success and failure) | ResultListener | No |
| StateCallBack | Callback for the upload status | StateCallBack | No |
| ProgressCallBack | Callback for the upload progress | ProgressCallBack | No |
| InitMultipleUploadCallback | Callback for the completion of multipart upload initialization | InitMultipleUploadCallback | No |

#### Response description

- Success: `TransferTask` is returned. You can pause, resume, or cancel the `TransferTask`.
-Failure: An error occurs (such as authentication failure), with a `CosXmlClientException` or `CosXmlServiceException` exception reported in ResultListener's callback for failure. For more information, see [Troubleshooting](https://www.tencentcloud.com/document/product/436/53963).
