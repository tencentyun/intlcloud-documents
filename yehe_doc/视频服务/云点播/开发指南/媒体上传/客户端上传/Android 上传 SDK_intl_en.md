VOD provides an SDK for uploading videos on Android client. For more information on the upload process, please see [Guide - Upload from Client](https://intl.cloud.tencent.com/document/product/266/33921).

## Downloading Source Code

1. Click [here](https://ugcupload-1252463788.file.myqcloud.com/LiteAVSDK_UGC_Upload_Android.zip) to download the Android Upload Demo and source code.
2. After decompressing the downloaded zip file, you can see the demo directory and find the upload source code in `Demo/app/src/main/java/com/tencent/ugcupload/demo/videoupload`.

## Integrating Upload Library and Source Code

1. Copy `Demo/app/src/main/java/com/tencent/ugcupload/demo/videoupload` to your project directory, and modify the package name manually.
2. Refer to `Demo/app/build.gradle` to add dependencies in your project:
    ```
    implementation ('com.tencent.qcloud:cosxml:5.5.3') {
        exclude group: 'com.tencent.qcloud', module: 'mtaUtils' // Disable MTA reporting}
    }
    ```
>?You can also refer to [Manual integration](https://intl.cloud.tencent.com/document/product/436/12159) and integrate corresponding dependent libraries.
3. Network and storage access permissions are required for video uploading. You can add the following permission declarations in `AndroidManifest.xml`:
	```xml
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
	<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
	<receiver android:name=".videoupload.impl.TVCNetWorkStateReceiver">
		<intent-filter>
			<!--Action to detect network changes-->
			<action android:name="android.net.conn.CONNECTIVITY_CHANGE"/>
			<category android:name="android.intent.category.DEFAULT" />
		</intent-filter>
	</receiver>
	```

## Uploading Videos
#### Initializing upload object

```java
TXUGCPublish mVideoPublish = new TXUGCPublish(this.getApplicationContext(), "independence_android")
```

#### Setting upload object callback

```java
mVideoPublish.setListener(new TXUGCPublishTypeDef.ITXVideoPublishListener() {
    @Override
    public void onPublishProgress(long uploadBytes, long totalBytes) {
        mProgress.setProgress((int) (100*uploadBytes/totalBytes));
    }

    @Override
    public void onPublishComplete(TXUGCPublishTypeDef.TXPublishResult result) {
        mResultMsg.setText(result.retCode + " Msg:" + (result.retCode == 0 ? result.videoURL : result.descMsg));
    }
});
```

#### Constructing upload parameters

```java
TXUGCPublishTypeDef.TXPublishParam param = new TXUGCPublishTypeDef.TXPublishParam();

param.signature = "xxx";
param.videoPath = "xxx";
```
For details on how to calculate `signature`, please see [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).

#### Calling upload method

```java
int publishCode = mVideoPublish.publishVideo(param);
```

## Uploading Images

#### Initializing upload object

```java
TXUGCPublish mVideoPublish = new TXUGCPublish(this.getApplicationContext(), "independence_android")
```

#### Setting upload object callback

```java
mVideoPublish.setListener(new TXUGCPublishTypeDef.ITXMediaPublishListener() {
    @Override
    public void onMediaPublishProgress(long uploadBytes, long totalBytes) {
        mProgress.setProgress((int) (100*uploadBytes/totalBytes));
    }
    @Override
    public void onMediaPublishComplete(TXUGCPublishTypeDef.TXMediaPublishResult mediaResult) {
        mResultMsg.setText(result.retCode + " Msg:" + (result.retCode == 0 ? result.videoURL : result.descMsg));
    }
});
```

#### Constructing upload parameters

```java
TXUGCPublishTypeDef.TXMediaPublishParam param = new TXUGCPublishTypeDef.TXMediaPublishParam();

param.signature = "xxx";
param.mediaPath = "xxx";
```

For details on how to calculate `signature`, please see [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).

#### Calling upload method

```java
int publishCode = mVideoPublish.publishMedia(param);
```

>?
>- The upload method automatically selects simple upload or multipart upload based on the file size, eliminating your need to take care of every step in multipart upload.
>- To upload to the specified subapplication, please see [Subapplication System - Upload from client](https://intl.cloud.tencent.com/document/product/266/33987).
>
## Advanced Features

#### Uploading a cover image

Add the path to the cover image as an upload parameter.

```java
TXUGCPublishTypeDef.TXPublishParam param = new TXUGCPublishTypeDef.TXPublishParam();
param.signature = "xxx";
param.videoPath = "xxx";
param.coverPath = "xxx";
```
For details on how to calculate `signature`, please see [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).

#### Canceling and resuming upload

To cancel an upload, call the `cancelPublish()` API of `TXUGCPublish`.

```java
mVideoPublish.cancelPublish();
```

To resume an upload, call `publishVideo` of `TXUGCPublish` again using the same upload parameters and same video and cover image paths.

#### Checkpoint restart

VOD supports checkpoint restart during upload. When the upload terminated unexpectedly, you can resume the upload from the breakpoint, saving time of uploading.

Checkpoint restart is valid within one day. If the upload of a video is interrupted and then resumed within one day, the upload can be resumed; otherwise, the entire video will be uploaded again.

The upload parameter `enableResume` is the switch for checkpoint restart, enabled by default.

#### Pre-upload

Most of errors in upload are caused by network connection failures or timeout. To fix such problems, we have added an optimized pre-upload logic, including resolving HTTPDNS, getting the recommended upload target region, and detecting the optimal upload target region.

We recommend you call `TXUGCPublishOptCenter.getInstance().prepareUpload(signature)` when enabling the app. The pre-upload module will cache the mapping table of `<domain name, IP>` and the optimal upload target region locally, and automatically purge and refresh the cache when a network switch is detected.

>!Be sure to register the network monitoring module in `AndroidManifest.xml`:
```xml
<receiver android:name=".videoupload.impl.TVCNetWorkStateReceiver">
  <intent-filter>
    <!--Action to detect network changes-->
    <action android:name="android.net.conn.CONNECTIVITY_CHANGE"/>
    <category android:name="android.intent.category.DEFAULT" />
  </intent-filter>
</receiver>
```

For details on how to calculate `signature`, please see [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).


## Video Upload API Description

Initialize the upload object: `TXUGCPublish`

| Parameter | Description                   | Type      | Required   |
| --------- | ---------------------- | ------- | ---- |
| context   | Application context.        | Context | Yes    |
| customKey | This parameter is used to distinguish users. We recommend using your app account ID as the value of this parameter for future troubleshooting. | String  | No    |

Set VOD appId: `TXUGCPublish.setAppId`

| Parameter | Description                   | Type      | Required   |
| --------- | ---------------------- | ------- | ---- |
| appId   | VOD appId.        | int | Yes    |


Upload a video: `TXUGCPublish.publishVideo`

| Parameter | Description | Type                                 | Required |
| ----- | ---- | ---------------------------------- | ---- |
| param | Upload parameter. |  TXUGCPublishTypeDef.TXPublishParam | Yes |

Upload parameter: `TXUGCPublishTypeDef.TXPublishParam`

| Parameter | Description                               | Type   | Required   |
| ------------ | ---------------------------------- | ------- | ---- |
| signature | [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922). | String  | Yes    |
| videoPath    | Path to a local video file. | String                           | Yes    |
| coverPath | Path to a local cover image file. No cover file will be used by default.                  | String  | No.    |
| enableResume | Whether to enable checkpoint restart. It is enabled by default.                      | boolean | No    |
| enableHttps | Whether to enable HTTPS, which is disabled by default.                      | boolean | No |
| fileName     | Name of a video file uploaded to Tencent Cloud. If this parameter is left empty, the name of the local file will be used by default. | String  | No    |

Set upload callback: `TXUGCPublish.setListener`

| Parameter | Description        | Type                                       | Required   |
| -------- | ----------- | ---------------------------------------- | ---- |
| listener | Listening callback of upload progress and result. | TXUGCPublishTypeDef.ITXVideoPublishListener | Yes    |


Progress callback: `TXUGCPublishTypeDef.ITXVideoPublishListener.onPublishProgress`

| Variable Name | Description | Type |
| ----------- | -------- | ---- |
| uploadBytes | Number of uploaded bytes. | long |
| totalBytes  | Total number of bytes.     | long |

Result callback: `TXUGCPublishTypeDef.ITXVideoPublishListener.onPublishComplete`

| Variable Name   | Description | Type                                  ||
| ------ | ---- | ----------------------------------- |
| result | Upload result. | TXUGCPublishTypeDef.TXPublishResult |

Upload result: `TXUGCPublishTypeDef.TXPublishResult`

| Member Variable Name | Description | Type |
| -------- | --------- | ------ |
| retCode  | Result code.       | int    |
| descMsg  | Error description of failed upload. | String |
| videoId | VOD file ID. | String |
| videoURL | Address where the video is stored. | String |
| coverURL | Address where the cover is stored. | String |

Pre-upload: `TXUGCPublishOptCenter.prepareUpload`

| Parameter | Description                   | Type      | Required   |
| --------- | ---------------------- | ------- | ---- |
| signature   | [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).        | String | Yes    |

## Image Upload API

Initialize the upload object: `TXUGCPublish`

| Parameter | Description                                                  | Type    | Required |
| --------- | --------------------------------------------------------- | ------- | ---- |
| context   | Application context. | Context                                        | Yes   |
| customKey | This parameter is used to distinguish users. We recommend using your App account ID as the value of this parameter to facilitate subsequent troubleshooting. | String | No   |

Set VOD appId: `TXUGCPublish.setAppId`

| Parameter | Description  | Type | Required |
| -------- | --------- | ---- | ---- |
| appId      | VOD appId.    | int  | Yes   |

Upload image: `TXUGCPublish.publishMedia`

| Parameter | Description | Type                                    | Required |
| -------- | -------- | --------------------------------------- | ---- |
| param | Upload parameter. | TXUGCPublishTypeDef.TXMediaPublishParam | Yes   |

Upload parameter: `TXUGCPublishTypeDef.TXPublishParam`

| Parameter | Description                                            Type    | Required |
| ------------ | -------------------------------------------------- | ------- | ---- |
| signature | [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).       | String  | Yes   |
| mediaPath    | Path to a local image file.                                   | String  | Yes   |
| enableResume | Whether to enable checkpoint restart. It is enabled by default.                         | boolean | No   |
| enableHttps | Whether to enable HTTPS, which is disabled by default.                       | boolean | No |
| fileName     | Name of a video file uploaded to Tencent Cloud. If this parameter is left empty, the name of the local file will be used by default. | String  | No   |

Set upload callback: `TXUGCPublish.setListener`

| Parameter | Description               | Type                                        | Required |
| -------- | ---------------------- | ------------------------------------------- | ---- |
| listener | Listening callback of upload progress and result. | TXUGCPublishTypeDef.ITXVideoPublishListener | Yes   |

Progress callback: `TXUGCPublishTypeDef.ITXMediaPublishListener.onPublishProgress`

| Variable    | Description         | Type |
| ----------- | ---------------- | ---- |
| uploadBytes | Number of uploaded bytes. | long |
| totalBytes  | Total number of bytes.         | long |

Result callback: `TXUGCPublishTypeDef.ITXMediaPublishListener.onPublishComplete`

| Variable Name | Description | Type                                |
| -------- | -------- | ----------------------------------- |
| result   | Upload result. | TXUGCPublishTypeDef.TXPublishResult |

Upload result: `TXUGCPublishTypeDef.TXPublishResult`

| Member Variable Name | Description           | Type   |
| ------------ | ------------------ | ------ |
| retCode      | Result code.           | int    |
| descMsg      | Error description of failed upload | String |
| mediaId        | VOD media file ID. | String |
| mediaURL     | Media resources storage address.   | String |

Pre-upload: `TXUGCPublishOptCenter.prepareUpload`

| Parameter | Description                                     | Type    | Required |
| --------- | -------------------------------------------- | ------ | ---- |
| signature | [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922). | String | Yes    |

## Error Codes

The SDK listens to the video upload status via API `TXUGCPublishTypeDef.ITXVideoPublishListene\ITXMediaPublishListener`. Therefore, you can check the video upload status using `retCode` in `TXUGCPublishTypeDef.TXPublishResult\TXMediaPublishResult`.

| Status Code | TVCConstants         | Description                     |
| :--: | :----------------------------- | :--------------------- |
|  0   | NO_ERROR                       | Uploaded successfully.                   |
| 1001 | ERR_UGC_REQUEST_FAILED         | Upload request failed due to invalid or expired client’s signature. Apply for another signature for the App.                 |
| 1002 | ERR_UGC_PARSE_FAILED           | Failed to parse the request information.               |
| 1003 | ERR_UPLOAD_VIDEO_FAILED        | Failed to upload the video.                 |
| 1004 | ERR_UPLOAD_COVER_FAILED        | Failed to upload the cover image.                 |
| 1005  |  ERR_UGC_FINISH_REQUEST_FAILED  | Cancel upload request failed                |
| 1006 | ERR_UGC_FINISH_RESPONSE_FAILED | An error occurred with the response to ending the upload.               |
| 1007 | ERR_CLIENT_BUSY                | The client is busy (the object cannot process more requests).      |
| 1008 | ERR_FILE_NOEXIT | The file for upload does not exist.                |
| 1009 | ERR_UGC_PUBLISHING                | The video is being uploaded.                |
| 1010 | ERR_UGC_INVALID_PARAM          | The upload parameter is empty.                 |
| 1012 | ERR_UGC_INVALID_SIGNATURE      | The signature for uploading video is empty. |
| 1013 | ERR_UGC_INVALID_VIDOPATH | The video file path is empty.     |
| 1014  |  ERR_UGC_INVALID_VIDEO_FILE     |  The video file does not exist under the current path.           |
| 1015 | ERR_UGC_FILE_NAME               | The file name of the video exceeds 40 characters or contains special symbols. |
| 1016 | ERR_UGC_INVALID_COVER_PATH     | The path to the cover image is invalid. The file does not exist       |
| 1017 | ERR_USER_CANCEL                | The user cancelled the upload.       |
| 1018 | ERR_UPLOAD_VOD                 | Failed to upload a file of less than 5 MB directly to VOD.       |


