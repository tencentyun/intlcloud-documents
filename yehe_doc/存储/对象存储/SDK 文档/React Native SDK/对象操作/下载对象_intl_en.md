## Overview

This document provides an overview of APIs and SDK code samples for downloading an object.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Object](https://www.tencentcloud.com/document/product/436/7753) | Downloading an object | Downloads an object to local |
| [HEAD Object](https://www.tencentcloud.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |

### Downloading an object

The download API allows you to pause, resume (via checkpoint restart), or cancel a download task.

#### Sample code:

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

    // Start the download
    let transferTask:TransferTask = await cosTransferManger.download(
      bucket,
      cosPath,
      downliadPath,
      {
        resultListener: {
          successCallBack: successCallBack,
          failCallBack: failCallBack
        },
        stateCallback: stateCallBack,
        progressCallback: progressCallBack
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

| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ | ------ |
| bucket    | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| cosPath | Object key, which uniquely identifies an object in a bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, its key is `doc/picture.jpg`. | String | Yes |
| savePath | Absolute local path to save the downloaded file | String | Yes |
| versionId | Version ID of the object to be downloaded | String | No |
| trafficLimit | Bandwidth limit for a single request in bit/s. Value range: 819200–838860800, i.e., 100 KB/s - 100 MB/s. | Int | No |
| ResultListener | Callback for the download result (including success and failure) | ResultListener | No |
| StateCallBack | Callback for the download status | StateCallBack | No |
| ProgressCallBack | Callback for the download progress | ProgressCallBack | No |

#### Response description

- Success: `TransferTask` is returned. You can pause, resume, or cancel the `TransferTask`.
- Failure: An error (such as authentication failure) occurs, with a `CosXmlClientError` or `CosXmlServiceError` exception reported in ResultListener's callback for failure. For more information, see [Troubleshooting](https://www.tencentcloud.com/document/product/436/53970).
