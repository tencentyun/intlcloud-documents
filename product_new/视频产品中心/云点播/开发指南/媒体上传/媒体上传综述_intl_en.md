Media upload refers to upload of media files such as videos, audios, and cover images to VOD's storage capacity, so that the files can be further processed or distributed.

## Upload Methods

VOD supports the following upload methods:

- [Local upload through console](https://console.cloud.tencent.com/vod/media/upload)
You can upload local media files to VOD on the upload page of the VOD Console. This method allows you to upload files with speed and ease and has no requirement for technical experience, making it suitable for direct management of a small number of media files.
- [Pull through console](https://console.cloud.tencent.com/vod/media/upload)
This method is implemented on the upload page of the VOD Console. You can specify the URL of the media file to be uploaded, and the VOD backend will pull the file offline.
- [Upload from server](https://intl.cloud.tencent.com/document/product/266/33912)
You can upload media files stored on your backend server to VOD. This method is suitable for automated and systematic production environments. VOD provides the following upload from server SDKs for different programming languages:
    - [SDK for Java](https://intl.cloud.tencent.com/document/product/266/33914)
    - [SDK for C#](https://intl.cloud.tencent.com/document/product/266/33915)
    - [SDK for PHP](https://intl.cloud.tencent.com/document/product/266/33916)
    - [SDK for Python](https://intl.cloud.tencent.com/document/product/266/33917)
    - [SDK for Node.js](https://intl.cloud.tencent.com/document/product/266/33918)
    - [SDK for Go](https://intl.cloud.tencent.com/document/product/266/33919)
- [Upload from client](https://intl.cloud.tencent.com/document/product/266/33921)
This method allows end users to upload local videos on the client to VOD, which is suitable for scenarios such as UGC and PGC. VOD provides upload from client SDKs for the following platforms:
    - [Upload SDK for Android](https://intl.cloud.tencent.com/document/product/266/33925)
    - [Upload SDK for iOS](https://intl.cloud.tencent.com/document/product/266/33926)
    - [Upload SDK for Web](https://intl.cloud.tencent.com/document/product/266/33924)
- [Pull through API](https://intl.cloud.tencent.com/document/product/266/34118)
When using the server API for pull, you can specify the URL of the media file to be uploaded, and the VOD backend will pull the file offline. This method is suitable for migration of a large number of files or automated file migration.
- [LVB recording](/document/product/267/32739)
You can use the recording feature of VOD to save video content of LVB streams to VOD for archiving, clipping, and replay.

## Storage Regions

### List of supported regions

VOD has storage nodes in multiple regions around the globe. During media upload, files will be stored in the specified region. Currently, VOD supports the following storage regions:

<table>
    <tr>
        <th>
            Storage Region                
        </th>
        <th>
            Region Abbreviation                
        </th>
    </tr>
    <tr>
    <tr>
        <td>
            Beijing             
        </td>
        <td>
			ap-beijing
        </td>
    </tr>
    <tr>
        <td>
            Shanghai             
        </td>
        <td>
			ap-shanghai
        </td>
    </tr>
    <tr>
        <td>
            Chongqing             
        </td>
        <td>
			ap-chongqing
        </td>
    </tr>
    <tr>
        <td>
            Tianjin             
        </td>
        <td>
			ap-beijing-1
        </td>
    </tr>
</table>

### Activating storage regions

An important purpose of configuring multiple storage regions is to improve media upload quality (success rate and speed), which is subject to the distance between the uploader and storage node. Generally, the shorter the distance, the better the upload quality.

After you activate the VOD service, VOD will automatically assign the **Chongqing** storage region. You can activate other storage regions based on your actual business needs. For detailed directions, please see [Upload Storage Settings](https://intl.cloud.tencent.com/document/product/266/18874). **Once activated, a storage region cannot be deactivated.**

### Default storage region

In all of your activated storage regions, only one will be used as the default region. If you have only one activated region (Chongqing), it will be the default storage region; if you have activated multiple storage regions, you can select another region as the default storage region in the console. For detailed directions, please see [Storage Region Settings](https://intl.cloud.tencent.com/document/product/266/18874#.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F.E6.AD.A5.E9.AA.A4).

Purpose of the default storage region: in some scenarios, this region will be first selected as the target region for media upload. For more information, please see the following section.

### Selecting a storage region

A specified storage region is needed for media upload, which can be automatically selected by the VOD backend by default or be specified in the upload request.

- When the VOD backend automatically selects the storage region:
  - If you have only one storage region, i.e., Chongqing, all uploaded media files will be stored in this region.
  - If you have activated multiple storage regions, the region selection policies for different upload methods are as follows:
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
<td >The VOD backend will select the storage region nearest to the uploader</td>
</tr>
<tr>
<td>Pull through console</td>
<td>The default storage region will always be selected</td>
</tr>
<tr>
<td>Upload from server</td>
<td>The VOD backend will select the storage region nearest to the uploader</td>
</tr>
<tr>
<td>Upload from client</td>
<td>The VOD backend will select the storage region nearest to the uploader</td>
</tr>
<tr>
<td>Pull through API</td>
<td>The default storage region will always be selected</td>
</tr>
<tr>
<td>LVB recording</td>
<td>The VOD backend will select the storage region nearest to the region of the LVB push</td>
</tr>
</tbody></table>
- You can specify the storage region for different upload methods in the following ways:
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
<td >Unsupported</td>
</tr>
<tr>
<td>Pull through console</td>
<td>Unsupported</td>
</tr>
<tr>
<td>Upload from server</td>
<td><ul style="margin:0;"><li><a href="/document/product/266/10276#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F">SDK for Java</a></li><li><a href="https://intl.cloud.tencent.com/document/product/266/33915#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F">SDK for C#</a></li><li><a href="https://intl.cloud.tencent.com/document/product/266/33916#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F">SDK for PHP</a></li><li><a href="https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F">SDK for Python</a></li><li><a href="https://intl.cloud.tencent.com/document/product/266/33918#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F">SDK for Node.js</a></li><li><a href="https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F">SDK for Go</a></li> </ul>  </td>
</tr>
<tr>
<td>Upload from client</td>
<td><a href="/document/product/266/9221">Parameters of signature for upload in a VOD client</a></td>
</tr>
<tr>
<td>Pull through API</td>
<td><a href="/document/product/266/34118">`StorageRegion` parameter of the pull API</a> </td>
</tr>
<tr>
<td>LVB recording</td>
<td>Unsupported </td>
</tr>
</tbody></table>

## Features and Limits

### Media types

VOD supports uploading media files in the following formats:

* Video: MP4, TS, FLV, WMV, ASF, RM, RMVB, MPG, MPEG, 3GP, MOV, WEBM, MKV, and AVI
* Audio: MP3, M4A, FLAC, OGG, and WAV
* Cover image: JPG, JPEG, PNG, GIF, BMP, TIFF, AI, CDR, and EPS

### Event notifications

After a media file is uploaded, the VOD backend can notify you of this event. For more information on how event notifications work and how to configure them, please see [Event Notification](/document/product/266/33779) and [Configuring Event Notification](/document/product/266/33781), respectively.
The event notification types of different upload methods are as below:

| Upload Method                                                  | Event Notification Type                                       |
| --------------------------------------------------------- | -------------------------------------------------- |
|<ul style="margin:0;"><li>Local upload through console</li><li>Upload from server</li><li>Upload from client</li><li>LVB recording</li></ul> | [NewFileUpload](https://intl.cloud.tencent.com/document/product/266/33950)         |
| <ul style="margin:0;"><li>Pull through console</li><li>Pull through API  </li>                         | [PullComplete](/document/product/266/7831) |

### Additional features

VOD media upload provides multiple additional features for media asset management, video processing and event notification, and upload control.

#### Media asset management features

- Adding a cover: you can upload an image together with a video, and this image will be automatically set as video cover in the VOD media asset system.
- Specifying the expiration time: you can specify the expiration time of a media file when uploading it. After the specified time elapses, the VOD backend will automatically delete the media file and its associated files (e.g., output files and screenshots).
- Specifying the category: you can specify the category for the media file after it is uploaded.

Support conditions and usage of different upload methods are as shown below:

| Feature         | Local upload through console                                               | Pull through console | Upload from server                                                   | Upload from client                                                   | Pull through API                                                | LVB recording                                |
| ------------ | ------------------------------------------------------------ | -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ----------------------------------------------------------- | --------------------------------------- |
| Adding a cover     | Unsupported                                                       | Unsupported         | <ul style="margin:0;"><li>[SDK for Java](https://intl.cloud.tencent.com/document/product/266/33914#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[SDK for C#](https://intl.cloud.tencent.com/document/product/266/33915#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[SDK for PHP](https://intl.cloud.tencent.com/document/product/266/33916#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[SDK for Python](https://intl.cloud.tencent.com/document/product/266/33917#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[SDK for Node.js](https://intl.cloud.tencent.com/document/product/266/33918#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[SDK for Go](https://intl.cloud.tencent.com/document/product/266/33919#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2) |<ul style="margin:0;"><li> [SDK for Web](https://intl.cloud.tencent.com/document/product/266/33924#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>[SDK for Android](https://intl.cloud.tencent.com/document/product/266/33925#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>[SDK for iOS](https://intl.cloud.tencent.com/document/product/266/33926#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>[SDK for WeChat Mini Program](https://intl.cloud.tencent.com/document/product/266/33927#.E4.B8.8A.E4.BC.A0.E8.A7.86.E9.A2.91.E6.AD.A5.E9.AA.A4) |  [`CoverUrl` parameter in the `PullUpload` API](https://intl.cloud.tencent.com/document/product/266/34118)   | Unsupported                                  |
| Specifying the expiration time | Unsupported                                                       | Unsupported         | <ul style="margin:0;"><li>[`ExpireTime` parameter in the SDK for Java API](https://intl.cloud.tencent.com/document/product/266/33914#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`ExpireTime` parameter in the SDK for C# API](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`ExpireTime` parameter in the SDK for PHP API](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`ExpireTime` parameter in the SDK for Python API](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`ExpireTime` parameter in the SDK for Node.js API](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`ExpireTime` parameter in the SDK for Go API](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0) | [`expireTime` parameter in the signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922#.3Cspan-id-.3D.22p2.22.3E.3C.2Fspan.3E.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0.E8.AF.B4.E6.98.8E) | [`ExpireTime` parameter in the `PullUpload` API](https://intl.cloud.tencent.com/document/product/266/34118) | [Recording configuration](/document/product/267/20384) |
| Specifying the category     | [Specifying the category](https://intl.cloud.tencent.com/document/product/266/33890#.E6.9C.AC.E5.9C.B0.E4.B8.8A.E4.BC.A0.E6.AD.A5.E9.AA.A4) | Unsupported         |<ul style="margin:0;"><li> [`ClassId` parameter in the SDK for Java API](https://intl.cloud.tencent.com/document/product/266/33914#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`ClassId` parameter in the SDK for C# API](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`ClassId` parameter in the SDK for PHP API](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`ClassId` parameter in the SDK for Python API](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`ClassId` parameter in the SDK for Node.js API](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`ClassId` parameter in the SDK for Go API](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0) | [`classId` parameter in the signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922#.3Cspan-id-.3D.22p2.22.3E.3C.2Fspan.3E.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0.E8.AF.B4.E6.98.8E) | [`ClassId` parameter in the `PullUpload` API](https://intl.cloud.tencent.com/document/product/266/34118)    | Unsupported                                  |

#### Video processing and event notification

- Automatic video processing: you can specify a [task flow](/document/product/266/33475#.E4.BB.BB.E5.8A.A1.E6.B5.81) for media upload. After upload is completed, VOD will automatically execute this task flow. Common scenarios of this feature are screencapturing the first video frame as cover, transcoding, and content audit.
- Passthrough field in video processing event notification: if automatic video processing is enabled, after video is processed, the VOD backend will initiate an event notification to pass through this field to you.
- Passthrough field in upload event notification: after upload is completed, the VOD backend will initiate an event notification to pass through this field to you.

Support conditions and usage of different upload methods are as shown below:

| Feature         | Local upload through console                                               | Pull through console | Upload from server                                                   | Upload from client                                                   | Pull through API                                                | LVB recording                                |
| ------------------------ | ------------------------------------------------------------ | -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- |
| Automatic video processing             | [Automatic video processing after upload](https://intl.cloud.tencent.com/document/product/266/33890#.E6.9C.AC.E5.9C.B0.E4.B8.8A.E4.BC.A0.E6.AD.A5.E9.AA.A4) | Unsupported         | <ul style="margin:0;"><li>[SDK for Java](https://intl.cloud.tencent.com/document/product/266/33914#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[SDK for C#](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[SDK for PHP](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[SDK for Python](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[SDK for Node.js](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[SDK for Go](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81) | [`procedure` parameter in the signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922#.3Cspan-id-.3D.22p2.22.3E.3C.2Fspan.3E.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0.E8.AF.B4.E6.98.8E) | [`Procedure` parameter in the `PullUpload` API](https://intl.cloud.tencent.com/document/product/266/34118)   | Unsupported   |
| Passthrough field in video processing event notification | Unsupported                                                       | Unsupported         | Unsupported                                                       | `sessionContext` parameter in the signature for upload from client                           | [`SessionContext` parameter in the `PullUpload` API](https://intl.cloud.tencent.com/document/product/266/34118) | Unsupported   |
| Passthrough field in upload event notification     | Unsupported                                                       | Unsupported         | <ul style="margin:0;"><li>[`SourceContext` parameter in the SDK for Java API](https://intl.cloud.tencent.com/document/product/266/33914#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`SourceContext` parameter in the SDK for C#](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`SourceContext` parameter in the SDK for PHP](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`SourceContext` parameter in the SDK for Python](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`SourceContext` parameter in the SDK for Node.js](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`SourceContext` parameter in the SDK for Go](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0) | [`sourceContext` parameter in the signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922#.3Cspan-id-.3D.22p2.22.3E.3C.2Fspan.3E.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0.E8.AF.B4.E6.98.8E) | Unsupported                                                       | Unsupported   |

#### Upload control

- Resumable upload: if the upload is terminated unexpectedly due to causes such as network disconnection and closing of the browser, you can upload the file again from where it left off without the need to upload the entire file again.
- Pausing/resuming upload: during the upload, you can proactively pause or resume the upload.
- Canceling upload: during the upload, you can proactively cancel the upload.
- Getting upload progress: you can get the upload progress, i.e., the size ratio of the part already uploaded to VOD to the full file size.
- Multipart upload: during the upload, a media file will be divided into multiple parts for separated upload. If you are on a weak network, this feature can reduce the affect of disconnection caused by network exceptions. If your bandwidth is high, this feature can concurrently upload multiple parts to make full use of the network bandwidth.

Support conditions and usage of different upload methods are as shown below:

| Feature         | Local upload through console                                               | Pull through console | Upload from server                                                   | Upload from client                                                   | Pull through API                                                | LVB recording                                |
| -------------- | -------------------- | -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------ | ------------------------------------------- |
| Resumable upload       | Unsupported               | N/A         | Unsupported                                                       | <ul style="margin:0;"><li>[SDK for Web](https://intl.cloud.tencent.com/document/product/266/33924#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>[SDK for Android](https://intl.cloud.tencent.com/document/product/266/33925#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>[SDK for iOS](https://intl.cloud.tencent.com/document/product/266/33926#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>The SDK for WeChat Mini Program is unsupported | N/A       | N/A                                      |
| Pausing/resuming upload | Unsupported               | N/A         | Unsupported                                                       | <ul style="margin:0;"><li>[SDK for Web](https://intl.cloud.tencent.com/document/product/266/33924#.E5.B8.B8.E8.A7.81.E9.97.AE.E9.A2.98)</li><li>[SDK for Android](https://intl.cloud.tencent.com/document/product/266/33925#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>[SDK for iOS](https://intl.cloud.tencent.com/document/product/266/33926#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>The SDK for WeChat Mini Program is unsupported | N/A       | N/A                                      |
| Canceling upload       | Refresh or close the page in browser | N/A         | N/A                                                       | <ul style="margin:0;"><li>[SDK for Web](https://intl.cloud.tencent.com/document/product/266/33924#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>[SDK for Android](https://intl.cloud.tencent.com/document/product/266/33925#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>[SDK for iOS](https://intl.cloud.tencent.com/document/product/266/33926#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>The SDK for WeChat Mini Program is unsupported| N/A       | StopLiveRecord|
| Getting upload progress   | The progress is displayed on the page by default     | Unsupported         | Unsupported                                                       | <ul style="margin:0;"><li>[SDK for Web](https://intl.cloud.tencent.com/document/product/266/33924#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>[SDK for Android](https://intl.cloud.tencent.com/document/product/266/33925#.E8.A7.86.E9.A2.91.E4.B8.8A.E4.BC.A0.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[SDK for iOS](https://intl.cloud.tencent.com/document/product/266/33926#.E8.A7.86.E9.A2.91.E4.B8.8A.E4.BC.A0.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[SDK for WeChat Mini Program](https://intl.cloud.tencent.com/document/product/266/33927#.E4.B8.8A.E4.BC.A0.E8.A7.86.E9.A2.91.E6.AD.A5.E9.AA.A4) | Unsupported       | N/A                                      |
| Multipart upload       | Enabled               | N/A         |<ul style="margin:0;"><li> [SDK for Java](https://intl.cloud.tencent.com/document/product/266/33914#.E6.8C.87.E5.AE.9A.E5.88.86.E7.89.87.E5.B9.B6.E5.8F.91.E6.95.B0)</li><li>[SDK for C#](https://intl.cloud.tencent.com/document/product/266/33915#.E8.B0.83.E7.94.A8.E4.B8.8A.E4.BC.A0)</li><li>[SDK for PHP](https://intl.cloud.tencent.com/document/product/266/33916#.E8.B0.83.E7.94.A8.E4.B8.8A.E4.BC.A0)</li><li>[SDK for Python](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E5.88.86.E7.89.87.E5.B9.B6.E5.8F.91.E6.95.B0)</li><li>[SDK for Node.js](https://intl.cloud.tencent.com/document/product/266/33918#.E8.B0.83.E7.94.A8.E4.B8.8A.E4.BC.A0)</li><li>[SDK for Go](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E5.88.86.E7.89.87.E5.B9.B6.E5.8F.91.E6.95.B0) | <ul style="margin:0;"><li> It is enabled for the SDK for Web by default</li><li>It is enabled for the SDK for Android by default</li><li>It is enabled for the SDK for iOS by default</li><li>The SDK for WeChat Mini Program is unsupported | N/A       | N/A                                      |

### Limits

- The limits on media file size are as below:
<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th>Upload Method</th>
<th>Maximum Media File Size</th>
</tr>
</thead>
<tbody>
<tr>
<td><ul style="margin:0;"><li>Local upload through console</li><li>Upload from client - SDK for Web</td>
<td >60 GB</td>
</tr>
<tr>
<td><ul style="margin:0;"><li>Upload from server</li><li>Pull through console</li><li> Pull through API</td>
<td>48.82 TB (50,000 GB)</td>
</tr>
<tr>
<td><ul style="margin:0;"><li>Upload from client - SDK for Android</li><li>Upload from client - SDK for iOS</td>
<td>10 GB </td>
</tr>
<tr>
<td>LVB recording</td>
<td><ul style="margin:0;"><li>For MP4/FLV formats, the upper limit is 48.82 TB (50,000 GB)</li><li>There is no upper limit for files in HLS format</li><li> Other restrictions are subject to <a href="/document/product/267/32739">LVB recording</a></td>
</tr>
</tbody></table>

- Number of files: unlimited.
