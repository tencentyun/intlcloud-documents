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

```ts
    // Bucket region abbreviation. For example, "ap-guangzhou" is the abbreviation of the Guangzhou region
    let region = "COS_REGION";
    // Create a `CosXmlServiceConfig` object and modify the configuration parameters as needed
    let serviceConfig = {
        region: region,
        isDebuggable: true,
        isHttps: true,
    };
    // Create a `TransferConfig` object and modify the configuration parameters as needed
    // You can set the object size threshold for multipart upload in `TransferConfig`. By default, the system automatically executes multipart upload for files whose sizes are greater than or equal to 2 MB. You can use the following code to change the threshold:
    let transferConfig = {
        forceSimpleUpload: false,
        enableVerification: true,
        divisionForUpload: 2097152, // Set multipart upload for files whose sizes are greater than or equal to 2 MB
        sliceSizeForUpload: 1048576, // Set the default part size to 1 MB
    };
    // Register the default COS TransferManger
    await Cos.registerDefaultTransferManger(serviceConfig, transferConfig);

    // Get `CosTransferManger`
    let cosTransferManger: CosTransferManger = Cos.getDefaultTransferManger();
    //let cosTransferManger: CosTransferManger = Cos.getTransferManger(newRegion);
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    let bucket = "examplebucket-1250000000";
    let cosPath = "exampleobject"; //Location identifier of the object in the bucket, i.e., the object key
    let srcPath = "Path of the local file"; // Path of the local file
    // If there is an uploadId for the initialized multipart upload, assign the value of uploadId here to resume the upload. Otherwise, assign `undefined`.
    let _uploadId = undefined;

    // Callback for successful upload
    let successCallBack = (header?: object) => {
      // TODO: Logic after successful upload
    };
    // Callback for failed upload
    let failCallBack = (clientError?: CosXmlClientError, serviceError?: CosXmlServiceError) => {
      // TODO: Logic after failed upload
      if (clientError) {
        console.log(clientError);
      }
      if (serviceError) {
        console.log(serviceError);
      }
    };
    // Callback for the upload status, through which you can check the task process
    let stateCallBack = (state: TransferState) => {
      // todo notify transfer state
    };
    // Callback for the upload progress
    let progressCallBack = (complete: number, target: number) => {
      // todo Do something to update progress...
    };
    // Callback for the completion of multipart upload initialization
    let initMultipleUploadCallBack = (bucket: string, cosKey: string, uploadId: string) => {
      //The uploadId required for the subsequent checkpoint restarts
      _uploadId = uploadId;
    };
    
    // Start the upload
    let transferTask:TransferTask = await cosTransferManger.upload(
      bucket,
      cosPath,
      srcPath,
      {
        uploadId: _uploadId,
        resultListener: {
          successCallBack: successCallBack,
          failCallBack: failCallBack
        },
        stateCallback: stateCallBack,
        progressCallback: progressCallBack,
        initMultipleUploadCallback: initMultipleUploadCallBack,
      }
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
| bucket    | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| cosPath | Object key, which uniquely identifies an object in a bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, its key is `doc/picture.jpg`. | String | Yes |
| fileUri | Path of the local file to be uploaded | String | Yes |
| uploadId | If there is an uploadId for the initialized multipart upload, assign the value of uploadId here to resume the upload. | String | No |
| stroageClass | Storage class | String | No |
| trafficLimit | Bandwidth limit for a single request in bit/s. Value range: 819200–838860800, i.e., 100 KB/s - 100 MB/s. | Int | No |
| ResultListener | Callback for the upload result (including success and failure) | ResultListener | No |
| StateCallBack | Callback for the upload status | StateCallBack | No |
| ProgressCallBack | Callback for the upload progress | ProgressCallBack | No |
| InitMultipleUploadCallback | Callback for the completion of multipart upload initialization | InitMultipleUploadCallback | No |

#### Response description

- Success: `TransferTask` is returned. You can pause, resume, or cancel the `TransferTask`.
- Failure: An error (such as authentication failure) occurs, with a `CosXmlClientError` or `CosXmlServiceError` exception reported in ResultListener's callback for failure. For more information, see [Troubleshooting](https://www.tencentcloud.com/document/product/436/53970).
