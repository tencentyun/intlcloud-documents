
## Connection Process 

Short video release: upload a .mp4 file to Tencent Video Cloud and get the online watch URL. Tencent Video Cloud can meet various video watch needs such as nearby scheduling, instant live streaming and playback, dynamic acceleration, and global connection, delivering a smooth watch experience.
![](https://main.qcloudimg.com/raw/860e8f3b3c3e6f6910421c47b7b134b6.png)

- Step 1. Use the `TXUGCRecord` API to shoot a short video, and a .mp4 short video file will be generated after the shoot ends and be called back.
- Step 2. Your application applies for an upload signature ("credential" for the application to upload the .mp4 file to VOD) to your business server. To ensure the security, upload signatures should be distributed by your business server but not generated by the client application.
- Step 3. Use the `TXUGCPublish` API to publish the video. After the video is successfully published, the SDK will call back the watch URL to you.

## Notes

- You should never write the `SecretID` or `SecretKey` for upload signature calculation into the client code of the application, as their disclosure will cause security risks. If attackers get such information by cracking the application, they can misappropriate your traffic and storage service.
- The correct practice is to generate a one-time upload signature by using the `SecretID` and `SecretKey` on your server and send the signature to the application.
- When publishing a short video, please make sure that the `Signature` field is correctly passed in; otherwise, the release will fail.

## Connection Directions

Integrate the short video upload feature as instructed in [Upload SDK for Android](https://intl.cloud.tencent.com/document/product/266/33925).
<span id="step1"></span>
### 1. Select a video
Uploaded a shot, edited, or spliced video or select a local video for upload.
<span id="step2"></span>
### 2. Compress the video
 - Video compression can reduce the short video file size but will also reduce the video definition. You can determine whether to compress videos as needed.
 - Use the [`TXVideoEditer.generateVideo(int videoCompressed, String videoOutputPath)`](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#af3f16bcb21f26c608c980b91671e386e) API to compress the video. Four resolutions are supported for compression currently, and compression with customizable bitrate will be supported in the future.
<span id="step3"></span>
### 3. Publish the video
Publish the generated .mp4 file to Tencent Cloud. The application needs to get the upload signature with a short validity period for file upload as instructed in [Signature Distribution](https://intl.cloud.tencent.com/document/product/1069/38015). `TXUGCPublish` (in `TXUGCPublish.java`) is used to publish .mp4 files to VOD so as to meet various video watch needs such as nearby scheduling, instant live streaming and playback, dynamic acceleration, and global connection.
```java
mVideoPublish = new TXUGCPublish(TCVideoPublisherActivity.this.getApplicationContext());
// Checkpoint restart is used for file release by default
TXUGCPublishTypeDef.TXPublishParam param = new TXUGCPublishTypeDef.TXPublishParam();
param.signature = mCosSignature;						// Enter the upload signature calculated in step 4
// Video file path generated by shoot, which can be obtained through the `onRecordComplete` callback of `ITXVideoRecordListener`
param.videoPath = mVideoPath;
// First-frame video preview generated by shoot, which can be obtained through the `onRecordComplete` callback of `ITXVideoRecordListener`
param.coverPath = mCoverPath;
mVideoPublish.publishVideo(param);
```
The release process and result will be returned through the `TXRecordCommon.ITXVideoPublishListener` API (in the `TXRecordCommon.java` header file):
- `onPublishProgress` is used to return the release progress, the `uploadBytes` parameter indicates the number of uploaded bytes, and the `totalBytes` parameter indicates the total number of bytes that need to be uploaded.
```java
void onPublishProgress(long uploadBytes, long totalBytes);
```
- `onPublishComplete` is used to return the release result.
```java
void onPublishComplete(TXPublishResult result);
```
 The fields in the `TXPublishResult` parameter and their descriptions are as detailed below:
 <table border=0 cellpadding="0" cellspacing="0">
 <thead><tr><th>Field</th><th align="center">Description</th></tr></thead>
 <tbody><tr>
 <td>errCode</td>
 <td >Error code.</td>
	</tr> <tr>
 <td>descMsg</td>
 <td >Error message.</td>
	</tr> <tr>
 <td>videoURL</td>
 <td >VOD address of short video.</td>
	</tr> <tr>
 <td>coverURL</td>
 <td >Cloud storage address of video cover.</td>
	</tr> <tr>
 <td>videoId</td>
 <td >Cloud storage ID of video file, through which you can call VOD's <a href = "https://intl.cloud.tencent.com/document/product/266/7788">server APIs</a>.</td>
 </tr>
 </tbody></table> 
- You can check the short video release result against the [error code table](https://intl.cloud.tencent.com/document/product/1069/38042).
<span id="step4"></span>
### 4. Play back the video

After the video is successfully uploaded in [step 3](#step3), the video `fileId`, playback URL, and cover URL will be returned. You can directly pass in the `fileId` or playback URL to the [VOD player](https://intl.cloud.tencent.com/document/product/1069/38027) for video playback.
