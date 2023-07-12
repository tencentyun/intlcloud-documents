## Overview

This document describes how to limit the speed on a single URL when calling the upload or download API.

## Notes

The speed range is **819200 to 838860800** (in bit/s), that is, 100 KB/s to 100 MB/s. If a value is not within this range, 400 will be returned.
The speed is limited by the `trafficLimit` parameter passed in when the `upload` and `download` methods are called.

#### Sample 1. Limiting single-URL speed on uploads

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
    // Set the bandwidth limit for a single URL in bit/s. In the example, the limit is set to 1 Mbit/s
    int _trafficLimit = 1024 * 1024 * 8;
    // Start the upload
    TransferTask transferTask = await transferManager.upload(bucket, cosPath,
        filePath: srcPath,
        uploadId: _uploadId,
        trafficLimit: _trafficLimit,
        resultListener: ResultListener(successCallBack, failCallBack),
        stateCallback: stateCallback,
        progressCallBack: progressCallBack,
        initMultipleUploadCallback: initMultipleUploadCallback
    );
```

#### Sample 2. Limiting single-URL speed on downloads

```dart
    // The advanced download API supports checkpoint restart. Therefore, a HEAD request will be sent before the download to obtain the file information.
    // If you are using a temporary key or accessing with a sub-account, ensure that your permission list includes HeadObject.

    // `TransferManager` supports checkpoint restart for download. You only need to ensure the consistency of parameters `bucket`, `cosPath`, and `savePath`.
    // Then the SDK will resume the download from where interrupted.

    // Get the `TransferManager`
    CosTransferManger transferManager = Cos().getDefaultTransferManger();
    //CosTransferManger transferManager = Cos().getTransferManger("newRegion");
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    String bucket = "examplebucket-1250000000";
    String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
    String downliadPath = "Absolute path of the local file"; // Absolute path of the local file

    // Callback for successful download
    successCallBack(result) {
      // TODO: Logic after successful download
    }
    // Callback for failed download
    failCallBack(clientException, serviceException) {
      // TODO: Logic after failed download
      if (clientException != null) {
        print(clientException);
      }
      if (serviceException != null) {
        print(serviceException);
      }
    }
    // Callback for the download status, through which you can check the task process
    stateCallback(state) {
      // todo notify transfer state
    }
    // Callback for the download progress
    progressCallBack(complete, target) {
      // todo Do something to download progress...
    }
    // Set the bandwidth limit for a single URL in bit/s. In the example, the limit is set to 1 Mbit/s
    int _trafficLimit = 1024 * 1024 * 8;
    // Start the download
    TransferTask transferTask = await transferManager.download(bucket, cosPath, downliadPath, 
        trafficLimit: _trafficLimit,
        resultListener: ResultListener(successCallBack, failCallBack),
        stateCallback: stateCallback,
        progressCallBack: progressCallBack
    );
    // Pause the task
    transferTask.pause();
    // Resume the task
    transferTask.resume();
    // Cancel the task
    transferTask.cancel();
```
