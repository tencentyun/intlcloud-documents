Media upload refers to upload of media files such as videos, audios, and thumbnail images to VOD so that they can be processed or distributed.

## Upload Methods

VOD supports the following upload methods:

- [Local upload through console](https://console.cloud.tencent.com/vod/media/upload)
Use the VOD console to upload local media files to VOD. This method is fast and easy. You can use this method if you are managing a small number of media files.
- [Pull through console](https://console.cloud.tencent.com/vod/media/upload)
Use the VOD console to pull data from URLs. VOD will pull data offline from the URLs you specify.
- [Upload from server](https://intl.cloud.tencent.com/document/product/266/33912)
Upload media files stored on your backend server to VOD. This method is suitable for automated and systematic production environments. VOD provides the following server upload SDKs for different programming languages:
    - [Java SDK](https://intl.cloud.tencent.com/document/product/266/33914)
    - [C# SDK](https://intl.cloud.tencent.com/document/product/266/33915)
    - [PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916)
    - [Python SDK](https://intl.cloud.tencent.com/document/product/266/33917)
    - [Node.js SDK](https://intl.cloud.tencent.com/document/product/266/33918)
    - [Golang SDK](https://intl.cloud.tencent.com/document/product/266/33919)
- [Upload from client](https://intl.cloud.tencent.com/document/product/266/33921)
Upload videos from the client to VOD. This method is suitable for UGC and PGC applications. VOD provides the following client upload SDKs:
    - [Android upload SDK](https://intl.cloud.tencent.com/document/product/266/33925)
    - [iOS upload SDK](https://intl.cloud.tencent.com/document/product/266/33926)
    - [Web upload SDK](https://intl.cloud.tencent.com/document/product/266/33924)
- [API upload](https://intl.cloud.tencent.com/document/product/266/34118)
Use VOD’s server-side API to pull media from URLs. VOD will pull data offline from the URLs you specify. This method is suitable for the migration of a large number of media files or automated data migration.
- [Live recording](https://intl.cloud.tencent.com/document/product/267/31563)
If you use the live recording feature of CSS, the live streams recorded will be saved to VOD for archiving, editing, and replay.

## Storage Regions
[](id:Storage)
### Supported regions

VOD has storage nodes around the globe. Your media files are uploaded to one of these storage nodes. Currently, VOD supports the following storage regions:

| Region       | Value           |
| ---------- | ---------------- |
| Beijing     | ap-beijing       |
| Shanghai     | ap-shanghai      |
| Guangzhou     | ap-guangzhou     |
| Chongqing     | ap-chongqing     |
| Tianjin         | ap-beijing-1     |
| Nanjing     | ap-nanjing       |
| Chengdu     | ap-chengdu       |
| Hong Kong (China)  | ap-hongkong      |
| Taipei (China) | ap-taipei        |
| Singapore | ap-singapore |
| Mumbai (India) | ap-mumbai |
| Jakarta (Indonesia)   | ap-jakarta       |
| Seoul (Korea) | ap-seoul |
| Bangkok (Thailand) | ap-bangkok |
| Tokyo (Japan)     | ap-tokyo         |
| Silicon Valley (West US) | na-siliconvalley|
| Virginia (East US) | na-ashburn |
| São Paulo (Brazil)   | sa-saopaulo       |
| Toronto (Canada) | na-toronto |
| Frankfurt (Germany) | eu-frankfurt |
| Moscow (Russia) | eu-moscow |

### Enabling storage regions

A big advantage of having multiple storage regions is that it can improve upload performance (upload speed and success rate). This is because upload performance is affected by the distance between the upload source and the storage node. The shorter the distance, the better.

After you activate the VOD service, the **Singapore** storage region will be enabled for you automatically. You can enable other storage regions based on your actual needs. For detailed directions, see [Upload Storage Settings](https://intl.cloud.tencent.com/document/product/266/18874). **Once enabled, a storage region cannot be disabled.**

### Default storage region

You can have only one default region. If you have enabled only one storage region (i.e., Singapore), this region will be the default region. If you have enabled multiple storage regions, you can specify the default region in the console. For detailed directions, see [Configuring Storage Regions](https://www.tencentcloud.com/document/product/266/18874#configuring-storage-regions).

The default region is given a higher priority than the others in certain scenarios. For details, see the explanation below.

### Selecting a storage region

When you upload media files to VOD, by default, VOD will select a storage region automatically. You can also specify a region in your upload request.

- Automatic selection:
  - If you have only one storage region, i.e., Singapore, all media files will be uploaded to this region.
  - If you have enabled multiple storage regions, VOD will select a region as follows:
<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th>Upload Method</th>
<th>Region Selection Policy</th>
</tr>
</thead>
<tbody>
<tr>
<td>Local upload through console</td>
<td >The storage region closest to the upload source.</td>
</tr>
<tr>
<td>Pull through console</td>
<td>The default storage region.</td>
</tr>
<tr>
<td>Upload from server</td>
<td >The storage region closest to the upload source.</td>
</tr>
<tr>
<td>Upload from client</td>
<td>The storage region closest to the upload source.</td>
</tr>
<tr>
<td>Pull through API</td>
<td>The default storage region.</td>
</tr>
<tr>
<td>Live recording</td>
<td>The storage region closest to the live streaming source.</td>
</tr>
</tbody></table>
- You can also use the methods below to specify a storage region:
<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th>Upload Method</th>
<th>Region Designation Method</th>
</tr>
</thead>
<tbody>
<tr>
<td>Local upload through console</td>
<td >Not supported</td>
</tr>
<tr>
<td>Pull through console</td>
<td>Not supported</td>
</tr>
<tr>
<td>Upload from server</td>
<td><ul style="margin:0;"><li><a href="https://intl.cloud.tencent.com/document/product/266/33914">Java SDK</a></li><li><a href="https://intl.cloud.tencent.com/document/product/266/33915#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F">C# SDK</a></li><li><a href="https://intl.cloud.tencent.com/document/product/266/33916#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F">PHP SDK</a></li><li><a href="https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F">Python SDK</a></li><li><a href="https://intl.cloud.tencent.com/document/product/266/33918#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F">Node.js SDK</a></li><li><a href="https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F">Go SDK</a></li> </ul>  </td>
</tr>
<tr>
<td>Upload from client</td>
<td><a href="https://intl.cloud.tencent.com/document/product/266/33922">Using an upload signature parameter</a></td>
</tr>
<tr>
<td>Pull through API</td>
<td><a href="https://intl.cloud.tencent.com/document/product/266/34118">Using the `StorageRegion` parameter of the API</a> </td>
</tr>
<tr>
<td>Live recording</td>
<td>Not supported</td>
</tr>
</tbody></table>

## Features and Limits

### Media types

VOD supports the following file formats:

- Video: WMV, RM, MOV, MPEG, MP4, 3GP, FLV, AVI, RMVB, TS, ASF, MPG, WEBM, MKV, M3U8, WM, ASX, RAM, MPE, VOB, DAT, MP4V, M4V, F4V, MXF, QT, and OGG.
- Audio: MP3, M4A, FLAC, OGG, WAV, RA, AAC, and AMR.
- Thumbnail: JPG, JPEG, PNG, GIF, BMP, TIFF, AI, CDR, EPS, and TIF.

### Event notification

VOD can send you a notification after a media file is uploaded. For more information on how event notifications work and how to configure them, see [Event Notification](https://intl.cloud.tencent.com/document/product/266/33948) and [Callback Settings](https://intl.cloud.tencent.com/document/product/266/14055).
The event notification types of different upload methods are as below:

| Upload Method                                                  | Event Notification Type                                       |
| --------------------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| <ul style="margin:0;"><li>Local upload through console</li><li>Upload from server</li><li>Upload from client</li><li>Live recording</li></ul> | [NewFileUpload](https://intl.cloud.tencent.com/document/product/266/33950)         |
| <ul style="margin:0;"><li>Pull through console</li><li>API pull  </li>                                      | [PullComplete](https://intl.cloud.tencent.com/document/product/266/33951) |

### Additional features

VOD offers other features related to media upload, including media management, video processing, notifications, and upload control.

#### Media management

- Thumbnail: You can upload an image together with a video. This image will be used as the video’s thumbnail in VOD.
- Expiration time: You can specify the expiration time of a media file. After the file expires, VOD will automatically delete it and its associated files (transcoding outputs and screenshots).
- Categorization: You can specify the category for a media file you upload.

Support for the above features by different upload methods are as follows:

| Feature         | Local upload through console                                                                                | Pull through console | Upload from server                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Upload from client                                                                                                                                                                                                                                                                                                                                                                                | API pull                                                                      | Live recording                                |
| ------------ | --------------------------------------------------------------------------------------------- | -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- | --------------------------------------- |
| Thumbnail     | Not supported                                                                                        | Not supported         | <ul style="margin:0;"><li>[Java SDK](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[C# SDK](https://intl.cloud.tencent.com/document/product/266/33915#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[Python SDK](https://intl.cloud.tencent.com/document/product/266/33917#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[Node.js SDK](https://intl.cloud.tencent.com/document/product/266/33918#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[Go SDK](https://intl.cloud.tencent.com/document/product/266/33919#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)                                                                                                                                                                                         | <ul style="margin:0;"><li> [Web SDK](https://intl.cloud.tencent.com/document/product/266/33924)</li><li>[Android SDK](https://intl.cloud.tencent.com/document/product/266/33925)</li><li>[iOS SDK](https://intl.cloud.tencent.com/document/product/266/33926)</li> | The `CoverUrl` parameter of the [PullUpload API](https://intl.cloud.tencent.com/document/product/266/34118).                         | Not supported                                  |
| Expiration time | Not supported                                                                                        | Not supported         | <ul style="margin:0;"><li>The `ExpireTime` parameter of the [Java SDK upload API](https://intl.cloud.tencent.com/document/product/266/33914).</li><li>The `ExpireTime` parameter of the [C# SDK upload API](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0).</li><li>The `ExpireTime` parameter of the [PHP SDK upload API](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0).</li><li>The `ExpireTime` parameter of the [Python SDK upload API](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0).</li><li>The `ExpireTime` parameter of the [Node.js SDK upload API](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0).</li><li>The `ExpireTime` parameter of the [Go SDK upload API](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0).         | Not supported                                                                                                                                                                                                                                                                                                                                                                                    | The `ExpireTime` parameter of the [PullUpload API](https://intl.cloud.tencent.com/document/product/266/34118)                       | [Live recording configuration](https://intl.cloud.tencent.com/document/product/267/34223). |
| Categorization     | [Specifying the category](https://intl.cloud.tencent.com/document/product/266/33890) | Not supported         | <ul style="margin:0;"><li> The `ClassId` parameter of the [Java SDK upload API](https://intl.cloud.tencent.com/document/product/266/33914).</li><li>The `ClassId` parameter of the [C# SDK upload API](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0).</li><li>The `ClassId` parameter of the [PHP SDK upload API](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0).</li><li>The `ClassId` parameter of the [Python SDK upload API](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0).</li><li>The `ClassId` parameter of the [Node.js SDK upload API](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0).</li><li>The `ClassId` parameter of the [Go SDK upload API](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0). | The [upload signature](https://intl.cloud.tencent.com/document/product/266/33922) parameter `classId`.                                                                                                                                                                                                                  | The `ClassId` parameter of the [PullUpload API](https://intl.cloud.tencent.com/document/product/266/34118). | Not supported                                  |

#### Video processing and notifications

- Automatic video processing: You can specify a [task flow](https://intl.cloud.tencent.com/document/product/266/33931) for an uploaded media file. After upload, VOD will automatically execute this task flow. Common processing tasks include capturing the first video frame as the thumbnail, transcoding, and content moderation.
- Pass-through field for video processing: If automatic video processing is enabled, after the video is processed, VOD will pass through this field when sending the video processing notification.
- Pass-through field for upload: After upload is completed, VOD will pass through this field when sending the upload notification.

Support for the above features by different upload methods are as follows:

| Feature         | Local Upload Through Console                                               | Pull Through Console | Upload from Server                                                   | Upload from Client                                                   | Pull Through API                                                | Live Recording                                |
| ------------------------ | ----------------------------------------------------------------------------------------------------------- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------- | -------- |
| Automatic video processing             | [Auto-processing after upload](https://intl.cloud.tencent.com/document/product/266/33890) | Not supported         | <ul style="margin:0;"><li>[Java SDK](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[C# SDK](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[Python SDK](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[Node.js SDK](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[Go SDK](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)                                                                                                                                             | The [upload signature](https://intl.cloud.tencent.com/document/product/266/33922) parameter `procedure`.     | The `procedure` parameter of the [PullUpload API](https://intl.cloud.tencent.com/document/product/266/34118)      | Not supported   |
| Pass-through field for video processing | Not supported                                                       | Not supported         | Not supported                                                       | The upload signature parameter `sessionContext`.                           | The `SessionContext` parameter of the [PullUpload API](https://intl.cloud.tencent.com/document/product/266/34118) | Not supported   |
| Pass-through field for upload     | Not supported                                                                                                      | Not supported         | <ul style="margin:0;"><li>The `SourceContext` parameter of the [Java SDK upload API](https://intl.cloud.tencent.com/document/product/266/33914).</li><li>The`SourceContext` parameter of the [C# SDK upload API](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0).</li><li>The `SourceContext` parameter of the [PHP SDK upload API](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0).</li><li>The `SourceContext` parameter of the [Python SDK upload API](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0).</li><li>The `SourceContext` parameter of the [Node.js SDK upload API](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0).</li><li>The `SourceContext` parameter of the [Go SDK upload API](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0). | The [upload signature](https://intl.cloud.tencent.com/document/product/266/33922) parameter `sourceContext`. | Not supported                                                          | Not supported   |

#### Upload control

- Checkpoint restart: If an upload is interrupted due to a disconnection, closing of the browser, or other reasons, when the user resumes the upload, VOD can start from where the user left off.
- Pausing/Resuming upload: You can pause or resume an upload.
- Canceling upload: You can cancel an upload.
- Getting the upload progress: You can get the percentage of data that has already been uploaded.
- Multipart upload: A media file can be segmented into multiple parts and uploaded separately. Under poor network conditions, this can reduce interruptions. In case of high-bandwidth connections, uploading multiple parts at the same time makes better use of bandwidth resources.

Support for the above features by different upload methods are as follows:

| Feature         | Local upload through console                                               | Pull through console | Upload from server                                                   | Upload from client                                                   | API pull                                                | Live recording                                |
| -------------- | -------------------- | -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------ | ------------------------------------------------------------ |
| Checkpoint restart       | Not supported               | N/A         | Not supported                                                       | <ul style="margin:0;"><li>[Web SDK](https://intl.cloud.tencent.com/document/product/266/33924)</li><li>[Android SDK](https://intl.cloud.tencent.com/document/product/266/33925)</li><li>[iOS SDK](https://intl.cloud.tencent.com/document/product/266/33926)</li> | N/A       | N/A                                                       |
| Pausing/Resuming upload | Not supported               | N/A         | Not supported                                                       | <ul style="margin:0;"><li>[Web SDK](https://intl.cloud.tencent.com/document/product/266/33924)</li><li>[Android SDK](https://intl.cloud.tencent.com/document/product/266/33925#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>[iOS SDK](https://intl.cloud.tencent.com/document/product/266/33926#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li> | N/A       | N/A                                                       |
| Canceling upload       | Refresh or close the webpage | N/A         | Not supported                                                       | <ul style="margin:0;"><li>[Web SDK](https://intl.cloud.tencent.com/document/product/266/33924)</li><li>[Android SDK](https://intl.cloud.tencent.com/document/product/266/33925#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>[iOS SDK](https://intl.cloud.tencent.com/document/product/266/33926#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li> | N/A       | [StopLiveRecord](https://intl.cloud.tencent.com/document/product/267/30837) |
| Getting the upload progress   | Progress shown by default     | Not supported         | Not supported                                                       | <ul style="margin:0;"><li>[Web SDK](https://intl.cloud.tencent.com/document/product/266/33924)</li><li>[Android SDK](https://intl.cloud.tencent.com/document/product/266/33925)</li><li>[iOS SDK](https://intl.cloud.tencent.com/document/product/266/33926)</li> | Not supported       | N/A                                                       |
| Multipart upload       | Enabled               | N/A         | <ul style="margin:0;"><li> [Java SDK](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[C# SDK](https://intl.cloud.tencent.com/document/product/266/33915#.E8.B0.83.E7.94.A8.E4.B8.8A.E4.BC.A0)</li><li>[PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916#.E8.B0.83.E7.94.A8.E4.B8.8A.E4.BC.A0)</li><li>[Python SDK](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E5.88.86.E7.89.87.E5.B9.B6.E5.8F.91.E6.95.B0)</li><li>[Node.js SDK](https://intl.cloud.tencent.com/document/product/266/33918#.E8.B0.83.E7.94.A8.E4.B8.8A.E4.BC.A0)</li><li>[Go SDK](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E5.88.86.E7.89.87.E5.B9.B6.E5.8F.91.E6.95.B0) | <ul style="margin:0;"><li> Enabled by default for the web SDK</li><li>Enabled by default for the Android SDK</li><li>Enabled by default for the iOS SDK</li> | N/A       | N/A                                                       |

### Limits

- The limits on media file size are as below:
<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th>Upload Method</th>
<th>Maximum File Size</th>
</tr>
</thead>
<tbody>
<tr>
<td><ul style="margin:0;"><li>Local upload through console</li><li>Upload from client - web SDK</td>
<td >60 GB</td>
</tr>
<tr>
<td><ul style="margin:0;"><li>Upload from server</li><li>Pull through console</li><li> Pull through API</td>
<td>48.82 TB (50,000 GB)</td>
</tr>
<tr>
<td><ul style="margin:0;"><li>Upload from client - Android SDK</li><li>Upload from client - iOS SDK</td>
<td>10 GB </td>
</tr>
<tr>
<td>Live recording</td>
<td><ul style="margin:0;"><li>48.82 TB (50,000 GB) for MP4 and FLV</li><li>No limit for HLS</li><li>Other limits depend on your <a href="https://intl.cloud.tencent.com/document/product/267/3156">live recording settings</a>.</td>
</tr>
</tbody></table>

- There isn’t a limit on the number of files that can be uploaded.

