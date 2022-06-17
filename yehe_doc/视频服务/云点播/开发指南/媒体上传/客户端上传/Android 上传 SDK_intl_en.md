VOD provides an SDK for uploading videos from Android clients. For details about the upload process, see [Guide](https://intl.cloud.tencent.com/document/product/266/33921).

## Downloading the source code

1. Click [here](https://liteav.sdk.qcloud.com/download/ugc/LiteAVSDK_UGC_Upload_Android.zip) to download our Android upload demo and its source code.
2. Decompress the zip file. In the `Demo` folder, find the source code in `Demo/app/src/main/java/com/tencent/ugcupload/demo/videoupload`.

##  Copying the source code and adding dependencies

1. Copy `Demo/app/src/main/java/com/tencent/ugcupload/demo/videoupload` to your project directory (you need to modify the package name).
2. Refer to `Demo/app/build.gradle` to add dependencies in your project:
    ```
    implementation 'com.qcloud.cos:cos-android-nobeacon:5.8.5'
    implementation 'com.qcloud.cos:quic:1.5.38'
    ```
>? You can also [manually integrate](https://intl.cloud.tencent.com/document/product/436/12159) the dependencies.

3. Because network and storage permissions are needed to upload videos, add the following permission declarations in `AndroidManifest.xml`:
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

##  Uploading Videos
#### Initialize an upload object

```java
TXUGCPublish mVideoPublish = new TXUGCPublish(this.getApplicationContext(), "independence_android")
```

#### Set the upload object callback

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

#### Construct upload parameters

```java
TXUGCPublishTypeDef.TXPublishParam param = new TXUGCPublishTypeDef.TXPublishParam();

param.signature = "xxx";
param.videoPath = "xxx";
```
For details on how to calculate `signature`, please see [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).

#### Call the upload API

```java
int publishCode = mVideoPublish.publishVideo(param);
```

## Uploading Images

#### Initialize an upload object

```java
TXUGCPublish mVideoPublish = new TXUGCPublish(this.getApplicationContext(), "independence_android")
```

#### Set the upload object callback

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

#### Construct upload parameters

```java
TXUGCPublishTypeDef.TXMediaPublishParam param = new TXUGCPublishTypeDef.TXMediaPublishParam();

param.signature = "xxx";
param.mediaPath = "xxx";
```

For details on how to calculate `signature`, please see [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).

#### Call the upload API

```java
int publishCode = mVideoPublish.publishMedia(param);
```

>?
>- The upload API automatically selects simple upload or multipart upload based on the file size. You don’t need to manually set up multipart upload.
>- To upload to a subapplication, see [Subapplication System - Upload from client](https://intl.cloud.tencent.com/document/product/266/33987).

## Advanced Features

#### Uploading a thumbnail

To upload a thumbnail, pass in the thumbnail path.

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

To resume an upload, call `publishVideo` of `TXUGCPublish` again, passing in the same upload parameters and video and thumbnail paths.

#### Setting up checkpoint restart

The SDK supports automatic checkpoint restart. If an upload is interrupted, you can resume the upload from where it left off.

With checkpoint restart, if an upload is interrupted, it can be resumed from where it left off within one day. After one day passes, the upload cannot be resumed, and the file can only be reuploaded from the beginning.

You can use the `enableResume` parameter to enable or disable checkpoint start. It’s enabled by default.

#### Pre-upload

Given that most upload errors are caused by network connection failures or timeout, we have added an optimized pre-upload logic, which involves resolving HTTPDNS, getting the recommended upload target region, and detecting the optimal upload target region.

We recommend you call `TXUGCPublishOptCenter.getInstance().prepareUpload(signature)` when launching your app. The pre-upload module will cache the `<domain name, IP>` mapping table, and the optimal upload target region locally, and will purge and refresh the cache when a network change is detected.

>! Make sure you register the network monitoring module in `AndroidManifest.xml`:
```xml
<receiver android:name=".videoupload.impl.TVCNetWorkStateReceiver">
  <intent-filter>
    <!--Action to detect network changes-->
    <action android:name="android.net.conn.CONNECTIVITY_CHANGE"/>
    <category android:name="android.intent.category.DEFAULT" />
  </intent-filter>
</receiver>
```

For details on how to calculate `signature`, see [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).

#### Enabling HTTPS upload
To enable HTTPS upload, set `enableHTTPS` in `TXPublishParam` to `true`.

```java
TXUGCPublishTypeDef.TXPublishParam param = new TXUGCPublishTypeDef.TXPublishParam();
param.enableHttps = true;
```

## Video Upload APIs

`TXUGCPublish`: Initialize an upload object

| Parameter | Description                   | Type      | Required   |
| --------- | ---------------------- | ------- | ---- |
| context   | Application context.        | Context | Yes    |
| customKey | This parameter is used to identify users. We recommend you set it to your app account ID to facilitate troubleshooting. | String  | No    |

`TXUGCPublish.setAppId`: Set the `appId`.

| Parameter | Description                   | Type      | Required   |
| --------- | ---------------------- | ------- | ---- |
| appId   | VOD appId.        | int | Yes    |


`TXUGCPublish.publishVideo`: Upload a video

| Parameter | Description | Type                                 | Required |
| ----- | ---- | ---------------------------------- | ---- |
| param | Upload parameters. |  TXUGCPublishTypeDef.TXPublishParam | Yes |

`TXUGCPublishTypeDef.TXPublishParam`: Upload parameters

| Parameter | Description                               | Type   | Required   |
| ------------ | ---------------------------------- | ------- | ---- |
| signature | [Signature for Upload from Client](https://cloud.tencent.com/document/product/266/33922). | String  | Yes    |
| videoPath    | The path of the local video file. | String                           | Yes    |
| coverPath | The path of a local thumbnail image. This parameter is left empty by default.                  | String  | No    |
| enableResume | Whether to enable checkpoint restart. It is enabled by default.                      | boolean | No    |
| enableHttps | Whether to enable HTTPS. It is disabled by default.                      | boolean | No |
| fileName     | The name of the uploaded file in Tencent Cloud. If this parameter is left empty, the original name of the local file will be used. | String  | No    |

`TXUGCPublish.setListener`: Set the upload callbacks

| Parameter | Description        | Type                                       | Required   |
| -------- | ----------- | ---------------------------------------- | ---- |
| listener | The upload progress and result callbacks. | TXUGCPublishTypeDef.ITXVideoPublishListener | Yes    |


`TXUGCPublishTypeDef.ITXVideoPublishListener.onPublishProgress`: The progress callback

| Variable  | Description | Type                                  |
| ----------- | -------- | ---- |
| uploadBytes | Uploaded bytes. | long |
| totalBytes  | Total bytes.     | long |

`TXUGCPublishTypeDef.ITXVideoPublishListener.onPublishComplete`: The result callback

| Variable Name   | Description | Type                                  |
| ------ | ---- | ----------------------------------- |
| result | The upload result. | TXUGCPublishTypeDef.TXPublishResult |

`TXUGCPublishTypeDef.TXPublishResult`: The upload result

| Member Variable | Description           | Type   |
| -------- | --------- | ------ |
| retCode  | The result code.       | int    |
| descMsg  | The error message. | String |
| videoId | The VOD file ID. | String |
| videoURL | The video URL. | String |
| coverURL | The thumbnail URL. | String |

`TXUGCPublishOptCenter.prepareUpload`: Set up pre-upload

| Parameter | Description                   | Type      | Required   |
| --------- | ---------------------- | ------- | ---- |
| signature   | [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).        | String | Yes    |

## Image Upload APIs

`TXUGCPublish`: Initialize an upload project

| Parameter | Description                                                  | Type    | Required |
| --------- | --------------------------------------------------------- | ------- | ---- |
| context   | Application context. | Context                                        | Yes   |
| customKey | This parameter is used to identify users. We recommend you set it to your app account ID to facilitate troubleshooting. | String  | No    |

`TXUGCPublish.setAppId`: Set VOD `appId`

| Parameter | Description  | Type | Required |
| -------- | --------- | ---- | ---- |
| appId      | VOD appId.    | int  | Yes   |

`TXUGCPublish.publishMedia`: Upload an image

| Parameter | Description | Type                                    | Required |
| -------- | -------- | --------------------------------------- | ---- |
| param | Upload parameters. | TXUGCPublishTypeDef.TXMediaPublishParam | Yes   |

`TXUGCPublishTypeDef.TXMediaPublishParam`: Upload parameters

| Parameter | Description                                            Type    | Required |
| ------------ | -------------------------------------------------- | ------- | ---- |
| signature | [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).       | String  | Yes   |
| mediaPath    | The path of the local image file.                                   | String  | Yes   |
| enableResume | Whether to enable checkpoint restart. It is enabled by default.                         | boolean | No   |
| enableHttps | Whether to enable HTTPS. It is disabled by default.                      | boolean | No |
| fileName     | The name of the uploaded file in Tencent Cloud. If this parameter is left empty, the original name of the local file will be used. | String  | No    |

`TXUGCPublish.setListener`: Set the upload callbacks

| Parameter | Description               | Type                                        | Required |
| -------- | ---------------------- | ------------------------------------------- | ---- |
| listener | The upload progress and result callbacks. | TXUGCPublishTypeDef.ITXVideoPublishListener | Yes   |

`TXUGCPublishTypeDef.ITXMediaPublishListener.onPublishProgress`: The progress callback

| Variable    | Description         | Type |
| ----------- | ---------------- | ---- |
| uploadBytes | Uploaded bytes. | long |
| totalBytes  | Total bytes.         | long |

`TXUGCPublishTypeDef.ITXMediaPublishListener.onPublishComplete`: The result callback

| Variable | Description | Type                                |
| -------- | -------- | ----------------------------------- |
| result   | The upload result. | TXUGCPublishTypeDef.TXPublishResult |

`TXUGCPublishTypeDef.TXPublishResult`: The upload result

| Member Variable | Description           | Type   |
| ------------ | ------------------ | ------ |
| retCode      | The result code.           | int    |
| descMsg  | The error message. | String |
| mediaId        | The VOD file ID. | String |
| mediaURL     | The file URL.   | String |

`TXUGCPublishOptCenter.prepareUpload`: Set up pre-upload

| Parameter | Description                                     | Type    | Required |
| --------- | -------------------------------------------- | ------ | ---- |
| signature | [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).       | String  | Yes   |

## Error Codes

The SDK listens for video upload status using `TXUGCPublishTypeDef.ITXVideoPublishListene\ITXMediaPublishListener`. Therefore, to get the upload status, check `retCode` in `TXUGCPublishTypeDef.TXPublishResult\TXMediaPublishResult`.

| Status Code | TVCConstants         | Description                     |
| :--: | :----------------------------- | :--------------------- |
|  0   | NO_ERROR                       | Uploaded successfully.                   |
| 1001 | ERR_UGC_REQUEST_FAILED         | The upload request failed, usually due to invalid or expired client signature. Please get the signature again.                 |
| 1002 | ERR_UGC_PARSE_FAILED           | Failed to parse the request information.               |
| 1003 | ERR_UPLOAD_VIDEO_FAILED        | Failed to upload the video.                 |
| 1004 | ERR_UPLOAD_COVER_FAILED        | Failed to upload the thumbnail image.                 |
| 1005  |  ERR_UGC_FINISH_REQUEST_FAILED  | Failed to end the upload.                |
| 1006 | ERR_UGC_FINISH_RESPONSE_FAILED | A response error occurred when ending the upload.               |
| 1007 | ERR_CLIENT_BUSY                | The client is busy (the object cannot process more requests).      |
| 1008 | ERR_FILE_NOEXIT | The file to be uploaded does not exist.                |
| 1009 | ERR_UGC_PUBLISHING                | The video is being uploaded.                |
| 1010 | ERR_UGC_INVALID_PARAM          | The upload parameter is empty.                 |
| 1012 | ERR_UGC_INVALID_SIGNATURE      | The signature for uploading video is empty. |
| 1013 | ERR_UGC_INVALID_VIDOPATH | The video file path is empty.     |
| 1014  |  ERR_UGC_INVALID_VIDEO_FILE     |  The video file does not exist under the current path.           |
| 1015 | ERR_UGC_FILE_NAME               | The video file name exceeds 40 characters or contains special characters. |
| 1016 | ERR_UGC_INVALID_COVER_PATH     | The path of the thumbnail image is invalid. The file does not exist       |
| 1017 | ERR_USER_CANCEL                | The user cancelled the upload.       |
| 1018 | ERR_UPLOAD_VOD                 | Failed to upload a file of less than 5 MB directly to VOD.       |


