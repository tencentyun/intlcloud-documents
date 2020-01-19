VOD provides an upload SDK for Android for uploading videos on the Android platform. For more information on the upload process, please see [Uploading Videos from Client](/document/product/266/9219).

## Downloading Source Code

1. Click [here](http://ugc-upload-1252463788.file.myqcloud.com/LiteAVSDK_UGC_Upload_Android_1.1.0.0.zip) to download the Android Upload Demo and source code.
2. You can see the Demo directory after decompressing the downloaded zip package. The upload source code is in the `Demo/app/src/main/java/com/tencent/ugcupload/demo/videoupload` directory.

## Integrating Upload Library and Source Code

1. Copy the upload source code directory `Demo/app/src/main/java/com/tencent/ugcupload/demo/videoupload` to your project directory and rename the package manually.
2. Integrate all the jar packages under the `Demo/app/libs/upload` directory into your project. You are recommended to retain the upload directory structure for convenient library update in the future.
3. Certain access permissions related to network and storage are required for uploading videos. You can add the following permission declarations in `AndroidManifest.xml`:
	```xml
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
	<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>``
	<receiver android:name=".videoupload.impl.TVCNetWorkStateReceiver">
		<intent-filter>
			// Action to detect network changes
			<action android:name="android.net.conn.CONNECTIVITY_CHANGE"/>
			<category android:name="android.intent.category.DEFAULT" />
		</intent-filter>
	</receiver>
	```

## Simple Video Upload
#### Initializing an upload object

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

#### Constructing upload parameter

```java
TXUGCPublishTypeDef.TXPublishParam param = new TXUGCPublishTypeDef.TXPublishParam();

param.signature = "xxx";
param.videoPath = "xxx";
```
For the rule of signature calculation, please see [Signature for Upload from Client](/document/product/266/9221).

#### Calling upload

```java
int publishCode = mVideoPublish.publishVideo(param);
```

## Simple Image Upload

#### Initializing an upload object

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

#### Constructing upload parameter

```java
TXUGCPublishTypeDef.TXMediaPublishParam param = new TXUGCPublishTypeDef.TXMediaPublishParam();

param.signature = "xxx";
param.mediaPath = "xxx";
```

For the rule of signature calculation, please see [Signature for Upload from Client](/document/product/266/9221).

#### Calling upload

```java
int publishCode = mVideoPublish.publishMedia(param);
```

>The upload method automatically selects simple upload or multipart upload based on the file size, eliminating your need to take care of every step in multipart upload.

## Advanced Features

#### Uploading a cover

Include the path to a cover in the upload parameter.

```java
TXUGCPublishTypeDef.TXPublishParam param = new TXUGCPublishTypeDef.TXPublishParam();
param.signature = "xxx";
param.videoPath = "xxx";
param.coverPath = "xxx";
```
For the rule of signature calculation, please see [Signature for Upload from Client](/document/product/266/9221).

#### Canceling and resuming upload

To cancel an upload, call the `canclePublish()` API of `TXUGCPublish`.

```java
mVideoPublish.canclePublish();
```

To resume an upload, call `publishVideo` of `TXUGCPublish` again using the same upload parameter, with the paths to the video and cover unchanged.

#### Resumable upload

During the video upload process, VOD supports resumable upload, that is, when the upload is terminated unexpectedly, you can upload the file again from where it left off, which helps reduce the upload time.

The effective time for resumption is 1 day, i.e., if the upload of a video is interrupted and then resumed within 1 day, it can be directly resumed; otherwise, the full video will be uploaded again by default.

`enableResume` in the upload parameter is the switch for resumable upload, which is enabled by default.

#### Pre-upload

In the actual upload process, most of errors are caused by failures or timeout of the network connection. To fix such problems, we have added the optimized pre-upload logic, including resolving HTTPDNS, getting the recommended upload target region, and detecting the optimal upload target region.

You are recommended to call `TXUGCPublishOptCenter.getInstance().prepareUpload(signature)` when the application is started. The pre-upload module will cache the mapping table of `<domain name, IP>` and the optimal upload target region locally, and automatically purge and refresh the cache when a network switch is detected.

>Be sure to register the network monitoring module in `AndroidManifest.xml`:
```xml
<receiver android:name=".videoupload.impl.TVCNetWorkStateReceiver">
  <intent-filter>
    // Action to detect network changes
    <action android:name="android.net.conn.CONNECTIVITY_CHANGE"/>
    <category android:name="android.intent.category.DEFAULT" />
  </intent-filter>
</receiver>
```

For the rule of signature calculation, please see [Signature for Upload from Client](/document/product/266/9221).


## Video Upload API Description

Initialize upload object: `TXUGCPublish`

| Parameter Name | Description | Type | Required |
| --------- | ---------------------- | ------- | ---- |
| context | Application context. | Context | Yes |
| customKey | Used to distinguish between different users. You are recommended to use an application account ID as the value of this parameter to facilitate subsequent troubleshooting. | String | No |

Set VOD appId: `TXUGCPublish.setAppId`

| Parameter Name | Description | Type | Required |
| --------- | ---------------------- | ------- | ---- |
| appId | VOD appId. | int | Yes |


Upload video: `TXUGCPublish.publishVideo`

| Parameter Name | Description | Type | Required |
| ----- | ---- | ---------------------------------- | ---- |
| param | Upload parameter. | TXUGCPublishTypeDef.TXPublishParam | Yes |

Upload parameter: `TXUGCPublishTypeDef.TXPublishParam`

| Parameter Name | Description | Type | Required |
| ------------ | ---------------------------------- | ------- | ---- |
| signature | [Signature for upload from client](/document/product/266/9221) | String | Yes |
| videoPath | Path to a local video file. | String | Yes |
| coverPath | Path to a local cover file. No cover file is uploaded by default. | String | No |
| enableResume | Whether to enable resumable upload, which is enabled by default. | boolean | No |
| enableHttps | Whether to enable HTTPS, which is disabled by default. | boolean | No |
| fileName | Name of a video file uploaded to Tencent Cloud. If this parameter is left empty, the local filename will be used by default. | String | No |

Set upload callback: `TXUGCPublish.setListener`

| Parameter Name | Description | Type | Required |
| -------- | ----------- | ---------------------------------------- | ---- |
| listener | Listener on the upload progress and result callback. | TXUGCPublishTypeDef.ITXVideoPublishListener | Yes |


Progress callback: `TXUGCPublishTypeDef.ITXVideoPublishListener.onPublishProgress`

| Variable Name | Description | Type |
| ----------- | -------- | ---- |
| uploadBytes | Number of uploaded bytes. | long |
| totalBytes | Total number of bytes. | long |

Result callback: `TXUGCPublishTypeDef.ITXVideoPublishListener.onPublishComplete`

| Variable Name | Description | Type |
| ------ | ---- | ----------------------------------- |
| result | Upload result. | TXUGCPublishTypeDef.TXPublishResult |

Upload result: `TXUGCPublishTypeDef.TXPublishResult`

| Member Variable Name | Description | Type |
| -------- | --------- | ------ |
| retCode | Result code. | int |
| descMsg | Error description of a failing upload. | String |
| videoId | VOD video file ID. | String |
| videoURL | Video storage address. | String |
| coverURL | Cover storage address. | String |

Pre-upload: `TXUGCPublishOptCenter.prepareUpload`

| Parameter Name | Description | Type | Required |
| --------- | ---------------------- | ------- | ---- |
| signature | [Signature for upload from client](/document/product/266/9221). | String | Yes |

## Image Upload API Description

Initialize upload object: `TXUGCPublish`

| Parameter Name | Description | Type | Required |
| --------- | --------------------------------------------------------- | ------- | ---- |
| context | Application context. | Context | Yes |
| customKey | Used to distinguish between different users. You are recommended to use an application account ID as the value of this parameter to facilitate subsequent troubleshooting. | String | No |

Set VOD appId: `TXUGCPublish.setAppId`

| Parameter Name | Description | Type | Required |
| -------- | --------- | ---- | ---- |
| appId | VOD appId. | int | Yes |

Upload image: `TXUGCPublish.publishMedia`

| Parameter Name | Description | Type | Required |
| -------- | -------- | --------------------------------------- | ---- |
| param | Upload parameter. | TXUGCPublishTypeDef.TXMediaPublishParam | Yes |

Upload parameter: `TXUGCPublishTypeDef.TXMediaPublishParam`

| Parameter Name | Description | Type | Required |
| ------------ | -------------------------------------------------- | ------- | ---- |
| signature | [Signature for upload from client](/document/product/266/9221). | String | Yes |
| mediaPath | Path to a local image file. | String | Yes |
| enableResume | Whether to enable resumable upload, which is enabled by default. | boolean | No |
| enableHttps | Whether to enable HTTPS, which is disabled by default. | boolean | No |
| fileName | Name of a video file uploaded to Tencent Cloud. If this parameter is left empty, the local filename will be used by default. | String | No |

Set upload callback: `TXUGCPublish.setListener`

| Parameter Name | Description | Type | Required |
| -------- | ---------------------- | ------------------------------------------- | ---- |
| listener | Listener on the upload progress and result callback. | TXUGCPublishTypeDef.ITXMediaPublishListener | Yes |

Progress callback: `TXUGCPublishTypeDef.ITXMediaPublishListener.onPublishProgress`

| Variable Name | Description | Type |
| ----------- | ---------------- | ---- |
| uploadBytes | Number of uploaded bytes. | long |
| totalBytes | Total number of bytes. | long |

Result callback: `TXUGCPublishTypeDef.ITXMediaPublishListener.onPublishComplete`

| Variable Name | Description | Type |
| -------- | -------- | ----------------------------------- |
| result | Upload result. | TXUGCPublishTypeDef.TXPublishResult |

Upload result: `TXUGCPublishTypeDef.TXMediaPublishResult`

| Member Variable Name | Description | Type |
| ------------ | ------------------ | ------ |
| retCode | Result code. | int |
| descMsg | Error description of a failing upload. | String |
| mediaId | VOD media file ID. | String |
| mediaURL | Media resource storage address. | String |

Pre-upload: `TXUGCPublishOptCenter.prepareUpload`

| Parameter Name | Description | Type | Required |
| --------- | -------------------------------------------- | ------ | ---- |
| signature | [Signature for upload from client](/document/product/266/9221). | String | Yes |

## Error Codes

The SDK listens on the video upload status through the `TXUGCPublishTypeDef.ITXVideoPublishListene\ITXMediaPublishListener` API; therefore, you can check the video upload status with the `retCode` in `TXUGCPublishTypeDef.TXPublishResult\TXMediaPublishResult`.

| Status Code | Constant in TVCConstants | Description |
| :--: | :----------------------------- | :--------------------- |
| 0 | NO_ERROR | Uploaded successfully. |
| 1001 | ERR_UGC_REQUEST_FAILED | The upload request failed. This is usually because that the signature of the client has expired or is invalid. You need to apply for a signature for the application again. |
| 1002 | ERR_UGC_PARSE_FAILED | Failed to parse the request information. |
| 1003 | ERR_UPLOAD_VIDEO_FAILED | Failed to upload the video. |
| 1004 | ERR_UPLOAD_COVER_FAILED | Failed to upload the cover. |
| 1005 | ERR_UGC_FINISH_REQUEST_FAILED | The request to end the upload failed. |
| 1006 | ERR_UGC_FINISH_RESPONSE_FAILED | An error occurred when responding to the upload ending request. |
| 1007 | ERR_CLIENT_BUSY | The client is busy (the object cannot process more requests). |
| 1008 | ERR_FILE_NOEXIT | The file to be uploaded does not exist. |
| 1009 | ERR_UGC_PUBLISHING | The video is being uploaded. |
| 1010 | ERR_UGC_INVALID_PARAM | The upload parameter is empty. |
| 1012 | ERR_UGC_INVALID_SIGNATURE | The signature for video upload is empty. |
| 1013 | ERR_UGC_INVALID_VIDOPATH | The path to the video file is empty. |
| 1014 | ERR_UGC_INVALID_VIDEO_FILE | The video file does not exist under the current path. |
| 1015 | ERR_UGC_FILE_NAME | The filename of the video to be uploaded is too long (over 40 characters) or contains special characters. |
| 1016 | ERR_UGC_INVALID_COVER_PATH | Invalid path to the cover of the video file. The file does not exist. |
| 1017 | ERR_USER_CANCEL | Upload canceled by user. |
| 1018 | ERR_UPLOAD_VOD | Failed to upload a file of less than 5 MB directly to VOD. |
