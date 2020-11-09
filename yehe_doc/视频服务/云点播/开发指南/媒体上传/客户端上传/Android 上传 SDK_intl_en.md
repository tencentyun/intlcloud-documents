VOD provides an SDK for uploading videos on the Android client. For more information on the upload process, please see [Upload from Client](https://intl.cloud.tencent.com/document/product/266/33921).

## Downloading Source Code

1. Click [here](http://ugcupload-1252463788.file.myqcloud.com/LiteAVSDK_UGC_Upload_Android.zip) to download the Android Upload Demo and source code.
2. You can see the demo directory after decompressing the downloaded zip file. Upload source code is located in `Demo/app/src/main/java/com/tencent/ugcupload/demo/videoupload`.

## Integrating Upload Library and Source Code

1. Copy the upload source code directory `Demo/app/src/main/java/com/tencent/ugcupload/demo/videoupload` to your project directory, and modify the package name manually.
2. Refer to `Demo/app/build.gradle` to add dependencies in your project:
    ```
    implementation 'com.tencent.qcloud:cosxml:5.5.4'
        exclude group:'com.tencent.qcloud', module: 'mtaUtils' // Disable MTA reporting
    }
    ```
    >? You can also refer to [Manual integration](https://intl.cloud.tencent.com/document/product/436/12159) and then integrate dependent libraries of relevant versions.
3. Network and storage access permissions are required for uploading videos. The following permission declarations can be added in `AndroidManifest.xml`:
	```xml
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
	<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
	<receiver android:name=".videoupload.impl.TVCNetWorkStateReceiver">
		<intent-filter>
			<!--Action to detect network changes-->
			<action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
			<category android:name="android.intent.category.DEFAULT" />
		</intent-filter>
	</receiver>
	```

## Simple Upload of Video
### Initializing upload object

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
> For details on how to calculate `signature`, please see [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).

#### Calling upload method

```java
int publishCode = mVideoPublish.publishVideo(param);
```

## Simple Image Upload

#### Initializing upload object

```java
TXUGCPublish mVideoPublish = new TXUGCPublish(this.getApplicationContext(), "independence_android")
```

#### Configuring upload object callback

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

> For details on how to calculate `signature`, please see [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).

### Calling upload method

```java
int publishCode = mVideoPublish.publishMedia(param);
```

>?The upload method automatically selects simple upload or multipart upload based on the file size, saving efforts of users.

## Advanced Features

### Uploading cover image

Include cover image path as one of the upload parameters.

```java
TXUGCPublishTypeDef.TXPublishParam param = new TXUGCPublishTypeDef.TXPublishParam();
param.signature = "xxx";
param.videoPath = "xxx";
param.coverPath = "xxx";
```
> For details on how to calculate `signature`, please see [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).

#### Canceling and resuming upload

To cancel an upload, call `canclePublish()` of `TXUGCPublish`.

```java
mVideoPublish.canclePublish();
```

To resume an upload, call `publishVideo` of `TXUGCPublish` again using the same upload parameters, with video and cover image paths unchanged.

#### Checkpoint restart

VOD supports checkpoint restart during upload, that is, when the upload is terminated unexpectedly, you can upload the file again from where it left off, thus reducing the upload time.

The effective time for resumption is one day. If the upload of a video is interrupted and then resumed within one day, the upload can be directly resumed; otherwise, the full video will be uploaded again by default.

`enableResume` in the upload parameters is the switch for resuming upload from breakpoint. It is enabled by default.

#### Pre-upload

Most of errors in upload are caused by failures or timeout of the network connection. To fix such problems, we have added the optimized pre-upload logic, including resolving HTTPDNS, getting the recommended upload target region, and detecting the optimal upload target region.

We recommend you call `TXUGCPublishOptCenter.getInstance().prepareUpload(signature)` when enabling the application. The pre-upload module will cache the mapping table of `<domain name, IP>` and the optimal upload target region locally, and automatically purge and refresh the cache when a network switch is detected.

>!Be sure to register the network monitoring module in `AndroidManifest.xml`:
```xml
<receiver android:name=".videoupload.impl.TVCNetWorkStateReceiver">
  <intent-filter>
    <!--Action to detect network changes-->
    <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
    <category android:name="android.intent.category.DEFAULT" />
  </intent-filter>
</receiver>
```

> For details on how to calculate `signature`, please see [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).


## Video Upload API

Initialize upload object: `TXUGCPublish`

| Parameter Name | Description | Type | Required |
| --------- | ---------------------- | ------- | ---- |
| context | Application context. | Context | Yes |
| customKey | Used to distinguish between different users. We recommend using an application account ID as the value of this parameter to facilitate subsequent troubleshooting. | String | No    |

Set VOD appId: `TXUGCPublish.setAppId`

| Parameter Name | Description | Type | Required |
| --------- | ---------------------- | ------- | ---- |
| appId   | VOD appId.    | int | AppId    |


Upload video: `TXUGCPublish.publishVideo`

| Parameter Name  | Description | Type                                 | Required   |
| ----- | ---- | ---------------------------------- | ---- |
| param | Upload parameter. | TXUGCPublishTypeDef.TXPublishParam | Yes |

Upload parameter: `TXUGCPublishTypeDef.TXPublishParam`

| Parameter Name | Description | Type | Required |
| ------------ | ---------------------------------- | ------- | ---- |
| signature | [Signature for Upload from Client](https://cloud.tencent.com/document/product/266/9221). | String | Yes    |
| videoPath    | Path of local video file. | String                           | Yes    |
| coverPath | Path of local cover file. No cover file will be uploaded by default | String | No.    |
| enableResume | Whether to resume upload from breakpoint. It is enabled by default | boolean | No    |
| enableHttps | Whether to enable HTTPS, which is disabled by default. | boolean | No |
| fileName | Name of a video file uploaded to Tencent Cloud. If this parameter is left empty, the local filename will be used by default. | String  | No    |

Set upload callback: `TXUGCPublish.setListener`

| Parameter Name     | Description        | Type                                       | Required   |
| -------- | ----------- | ---------------------------------------- | ---- |
| listener | Listen in the callback of upload progress and result. | TXUGCPublishTypeDef.ITXVideoPublishListener | Yes    |


Progress callback: `TXUGCPublishTypeDef.ITXVideoPublishListener.onPublishProgress`

| Variable Name | Description | Type |
| ----------- | -------- | ---- |
| uploadBytes | Uploaded bytes. | long |
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

| Parameter Name      | Description                   | Type      | Required   |
| --------- | ---------------------- | ------- | ---- |
| signature   | [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).        | String | Yes    |

## Image Upload API

Initialize upload object: `TXUGCPublish`

| Parameter Name | Description                                                  | Type    | Required |
| --------- | --------------------------------------------------------- | ------- | ---- |
| context   | Application context. | Context                                        | Yes   |
| customKey | Used to distinguish between different users. We recommend using an application account ID as the value of this parameter to facilitate subsequent troubleshooting. | String | No   |

Set VOD application ID: `TXUGCPublish.setAppId`

| Parameter Name | Description  | Type | Required |
| -------- | --------- | ---- | ---- |
| appId      | VOD application ID    | int  | Yes   |

Upload image: `TXUGCPublish.publishMedia`

| Parameter Name | Description | Type                                    | Required |
| -------- | -------- | --------------------------------------- | ---- |
| param | Upload parameter. | TXUGCPublishTypeDef.TXPublishParam | Yes   |

Upload parameter: `TXUGCPublishTypeDef.TXPublishParam`

| Parameter Name      | Description                                            Type    | Required |
| ------------ | -------------------------------------------------- | ------- | ---- |
| signature | [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).       | String  | Yes   |
| mediaPath    | Path of a local image file.                                   | String  | Yes   |
| enableResume | Whether to resume upload from breakpoint. It is enabled by default                         | boolean | No   |
| enableHttps | Whether to enable HTTPS, which is disabled by default. | boolean | No |
| fileName     | Name of a video file uploaded to Tencent Cloud. If this parameter is left empty, the local filename will be used by default. | String  | No   |

Set upload callback: `TXUGCPublish.setListener`

| Parameter Name | Description               | Type                                        | Required |
| -------- | ---------------------- | ------------------------------------------- | ---- |
| listener | Listen to the callback of upload progress and result. | TXUGCPublishTypeDef.ITXVideoPublishListener | Yes   |

Progress callback: `TXUGCPublishTypeDef.ITXMediaPublishListener.onPublishProgress`

| Variable Name    | Description         | Type |
| ----------- | ---------------- | ---- |
| uploadBytes | Uploaded bytes. | long |
| totalBytes  | Total number of bytes.         | long |

Result callback: `TXUGCPublishTypeDef.ITXMediaPublishListener.onPublishComplete`

| Variable Name | Description | Type                                |
| -------- | -------- | ----------------------------------- |
| result   | Upload result. | TXUGCPublishTypeDef.TXPublishResult |

Upload result: `TXUGCPublishTypeDef.TXPublishResult`

| Member Variable Name | Description           | Type   |
| ------------ | ------------------ | ------ |
| retCode      | Result code.           | int   |
| descMsg      | Error description of failed upload | String |
| mediaId        | VOD media file ID. | String |
| mediaURL     | Media resource storage address.   | String |

Pre-upload: `TXUGCPublishOptCenter.prepareUpload`

| Parameter Name  | Description                                     | Type    | Required |
| --------- | -------------------------------------------- | ------ | ---- |
| signature | [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922). | String | Yes    |

## Error Codes

The SDK listens to the video upload status via API `TXUGCPublishTypeDef.ITXVideoPublishListene\ITXMediaPublishListener`. Therefore, you can check the video upload status using `retCode` in `TXUGCPublishTypeDef.TXPublishResult\TXMediaPublishResult`.

| Status code | TVCConstants         | Description                     |
| :--: | :----------------------------- | :--------------------- |
|  0   | NO_ERROR                       | Uploaded successfully.                   |
| 1001 | ERR_UGC_REQUEST_FAILED         | The upload request failed, because that the client’s signature has expired or is invalid. You need to apply for a signature for the App again. |
| 1002 | ERR_UGC_PARSE_FAILED           | Failed to parse request information.               |
| 1003 | ERR_UPLOAD_VIDEO_FAILED | Failed to upload the video.                  |
| 1004 | ERR_UPLOAD_COVER_FAILED | Failed to upload the cover image.                 |
1005  |  ERR_UGC_FINISH_REQUEST_FAILED |  The request to end the upload failed                |
| 1006 | ERR_UGC_FINISH_RESPONSE_FAILED | An error occurred with the response to ending the upload.               |
| 1007 | ERR_CLIENT_BUSY | The client is busy (object cannot process more requests) |
| 1008 | ERR_FILE_NOEXIT | The file to be uploaded does not exist |
| 1009 | ERR_UGC_PUBLISHING                | The video is being uploaded.                |
| 1010 | ERR_UGC_INVALID_PARAM          | Upload parameter is empty.                 |
| 1012 | ERR_UGC_INVALID_SIGNATURE      | Signature for uploading video is empty. |
| 1013 | ERR_UGC_INVALID_VIDOPATH | The video file path is empty.     |
1014  |  ERR_UGC_INVALID_VIDEO_FILE     |  The video file does not exist under the current path.           |
| 1015 | ERR_UGC_FILE_NAME              | The file name of the video to be uploaded is too long (exceeds 40 characters) or contains special symbols. |
| 1016 | ERR_UGC_INVALID_COVER_PATH     | Invalid path of the cover of the video file. The file does not exist       |
| 1017 | ERR_USER_CANCEL                | Upload is canceled by the user.                                             |
| 1018 | ERR_UPLOAD_VOD                 | Failed to upload a file of less than 5 MB directly to VOD. |


