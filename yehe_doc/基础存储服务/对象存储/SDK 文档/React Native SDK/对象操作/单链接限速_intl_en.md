## Overview

This document describes how to limit the speed on a single URL when calling the upload or download API.

## Notes

The speed range is **819200 to 838860800** (in bit/s), that is, 100 KB/s to 100 MB/s. If a value is not within this range, 400 will be returned.
The speed is limited by the `trafficLimit` parameter passed in when the `upload` and `download` methods are called.

#### Sample 1. Limiting single-URL speed on uploads

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
    
    // Set the bandwidth limit for a single URL in bit/s. In the example, the limit is set to 1 Mbit/s
    let _trafficLimit = 1024 * 1024 * 8;

    // Start the upload
    let transferTask:TransferTask = await cosTransferManger.upload(
      bucket,
      cosPath,
      srcPath,
      {
        uploadId: _uploadId,
        trafficLimit: _trafficLimit,
        resultListener: {
          successCallBack: successCallBack,
          failCallBack: failCallBack
        },
        stateCallback: stateCallBack,
        progressCallback: progressCallBack,
        initMultipleUploadCallback: initMultipleUploadCallBack,
      }
    );
```

#### Sample 2. Limiting single-URL speed on downloads

```ts
    // The advanced download API supports checkpoint restart. Therefore, a HEAD request will be sent before the download to obtain the file information.
    // If you are using a temporary key or accessing with a sub-account, ensure that your permission list includes HeadObject.

    // `CosTransferManger` supports checkpoint restart for download. You only need to ensure the consistency of parameters `bucket`, `cosPath`, and `savePath`.
    // Then the SDK will resume the download from where interrupted.

    // Get `CosTransferManger`
    let cosTransferManger: CosTransferManger = Cos.getDefaultTransferManger();
    //let cosTransferManger: CosTransferManger = Cos.getTransferManger(newRegion);
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    let bucket = "examplebucket-1250000000";
    let cosPath = "exampleobject"; //Location identifier of the object in the bucket, i.e., the object key
    let downliadPath = "Path of the local file"; // Path of the local file

    // Callback for successful download
    let successCallBack = (header?: object) => {
      // TODO: Logic after successful download
    };
    // Callback for failed download
    let failCallBack = (clientError?: CosXmlClientError, serviceError?: CosXmlServiceError) => {
      // TODO: Logic after failed download
      if (clientError) {
        console.log(clientError);
      }
      if (serviceError) {
        console.log(serviceError);
      }
    };
    // Callback for the download status, through which you can check the task process
    let stateCallBack = (state: TransferState) => {
      // todo notify transfer state
    };
    // Callback for the download progress
    let progressCallBack = (complete: number, target: number) => {
      // todo Do something to download progress...
    };

    // Set the bandwidth limit for a single URL in bit/s. In the example, the limit is set to 1 Mbit/s
    let _trafficLimit = 1024 * 1024 * 8;

    // Start the download
    let transferTask:TransferTask = await cosTransferManger.download(
      bucket,
      cosPath,
      downliadPath,
      {
        trafficLimit: _trafficLimit,
        resultListener: {
          successCallBack: successCallBack,
          failCallBack: failCallBack
        },
        stateCallback: stateCallBack,
        progressCallback: progressCallBack
      }
    );
```
