Media upload refers to upload of media files such as videos, audios, and cover images to VOD's storage capacity, so that the files can be further processed or distributed.

## Upload Methods

VOD supports the following upload methods:

- [Local upload through console](https://console.cloud.tencent.com/vod/media/upload)
You can upload local media files to VOD on the upload page of the VOD console. This method allows you to upload files with speed and ease and has no requirement for technical experience, making it suitable for direct management of a small number of media files.
- [Pull through console](https://console.cloud.tencent.com/vod/media/upload)
This method is implemented on the upload page of the VOD console. You can specify the URL of the media file to be uploaded, and the VOD backend will pull the file offline.
- [Upload from server](https://intl.cloud.tencent.com/document/product/266/33912)
You can upload media files stored on your backend server to VOD. This method is suitable for automated and systematic production environments. VOD provides the following upload from server SDKs for different programming languages:
    - [Java SDK](https://intl.cloud.tencent.com/document/product/266/33914)
    - [SDK for C#](https://intl.cloud.tencent.com/document/product/266/33915)
    - [PHP SDK](https://intl.cloud.tencent.com/document/product/266/33916)
    - [Python SDK](https://intl.cloud.tencent.com/document/product/266/33917)
    - [Node.js SDK](https://intl.cloud.tencent.com/document/product/266/33918)
    - [SDK for Go](https://intl.cloud.tencent.com/document/product/266/33919)
- [Upload from client](https://intl.cloud.tencent.com/document/product/266/33921)
This method allows end users to upload local videos on the client to VOD, which is suitable for scenarios such as UGC and PGC. VOD provides upload from client SDKs for the following platforms:
    - [Upload SDK for Android](https://intl.cloud.tencent.com/document/product/266/33925)
    - [Upload SDK for iOS](https://intl.cloud.tencent.com/document/product/266/33926)
    - [Upload SDK for Web](https://intl.cloud.tencent.com/document/product/266/33924)
- [Pull through API](https://intl.cloud.tencent.com/document/product/266/34118)
When using the server API for pull, you can specify the URL of the media file to be uploaded, and the VOD backend will pull the file offline. This method is suitable for migration of a large number of files or automated file migration.
- [Live recording](https://intl.cloud.tencent.com/document/product/267/31563)
You can use the recording feature of VOD to save video content of live streams to VOD for archiving, clipping, and replay.

## Storage Regions
[](id:Storage)
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
    <tr>
        <td>
            Hong Kong, China             
        </td>
        <td>
			ap-hongkong
        </td>
    </tr>
    <tr>
        <td>
            Singapore             
        </td>
        <td>
			ap-singapore
        </td>
    </tr>
    <tr>
        <td>
            Mumbai (India)             
        </td>
        <td>
			ap-mumbai
        </td>
    </tr>
    <tr>
        <td>
            Seoul             
        </td>
        <td>
			ap-seoul
        </td>
    </tr>
    <tr>
        <td>
            Bangkok             
        </td>
        <td>
			ap-bangkok
        </td>
    </tr>
    <tr>
        <td>
            Tokyo             
        </td>
        <td>
			ap-tokyo
        </td>
    </tr>
    <tr>
        <td>
            Silicon Valley (Western US)            
        </td>
        <td>
			na-siliconvalley
        </td>
    </tr>
    <tr>
        <td>
            Virginia (Eastern US)             
        </td>
        <td>
			na-ashburn
        </td>
    </tr>
    <tr>
        <td>
            Toronto             
        </td>
        <td>
			na-toronto
        </td>
    </tr>
    <tr>
        <td>
            Frankfurt             
        </td>
        <td>
			eu-frankfurt
        </td>
    </tr>
    <tr>
        <td>
            Moscow             
        </td>
        <td>
			eu-moscow
        </td>
    </tr>
</table>

### Activating storage regions

An important purpose of configuring multiple storage regions is to improve media upload quality (success rate and speed), which is subject to the distance between the uploader and storage node. Generally, the shorter the distance, the better the upload quality.

After you activate the VOD service, VOD will automatically assign the **Singapore** storage region. You can activate other storage regions based on your actual business needs. For detailed directions, please see [Upload Storage Settings](https://intl.cloud.tencent.com/document/product/266/18874). **Once activated, a storage region cannot be deactivated.**

### Default storage region

In all of your activated storage regions, only one will be used as the default region. If you have only one activated region (Singapore), it will be the default storage region; if you have activated multiple storage regions, you can select another region as the default storage region in the console. For detailed directions, please see [Storage Region Settings](https://intl.cloud.tencent.com/document/product/266/18874#.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F.E6.AD.A5.E9.AA.A4).

Purpose of the default storage region: in some scenarios, this region will be first selected as the target region for media upload. For more information, please see the following section.

### Selecting a storage region

A specified storage region is needed for media upload, which can be automatically selected by the VOD backend by default or be specified in the upload request.

- When the VOD backend automatically selects the storage region:
  - If you have only one storage region, i.e., Singapore, all uploaded media files will be stored in this region.
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
<td>Live recording</td>
<td>The VOD backend will select the storage region nearest to the region of the live push</td>
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
<td><a href="https://intl.cloud.tencent.com/document/product/266/33922">Signature for upload from client</a></td>
</tr>
<tr>
<td>Pull through API</td>
<td><a href="https://intl.cloud.tencent.com/document/product/266/34118">`StorageRegion` parameter in the `PullUpload` API</a> </td>
</tr>
<tr>
<td>Live recording</td>
<td>Not supported</td>
</tr>
</tbody></table>

## Features and Limits

### Media types

VOD supports uploading media files in the following formats:

- Video: WMV, RM, MOV, MPEG, MP4, 3GP, FLV, AVI, RMVB, TS, ASF, MPG, WEBM, MKV, M3U8, WM, ASX, RAM, MPE, VOB, DAT, MP4V, M4V, F4V, MXF, QT, and OGG.
- Audio: MP3, M4A, FLAC, OGG, WAV, RA, AAC, and AMR.
- Cover image: JPG, JPEG, PNG, GIF, BMP, TIFF, AI, CDR, EPS, and TIF.

### Event notification

After a media file is uploaded, the VOD backend can notify you of this event. For more information on how event notifications work and how to configure them, please see [Event Notification](https://intl.cloud.tencent.com/document/product/266/33948) and [Configuring Event Notification](https://intl.cloud.tencent.com/document/product/266/14055), respectively.
The event notification types of different upload methods are as below:

| Upload Method                                                  | Event Notification Type                                       |
| --------------------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| <ul style="margin:0;"><li>Local upload through console</li><li>Upload from server</li><li>Upload from client</li><li>Live recording</li></ul> | [NewFileUpload](https://intl.cloud.tencent.com/document/product/266/33950)         |
| <ul style="margin:0;"><li>Pull through console</li><li>Pull through API  </li>                         | [PullComplete](https://intl.cloud.tencent.com/document/product/266/33951) |

### Additional features

VOD media upload provides multiple additional features for media asset management, video processing and event notification, and upload control.

#### Media asset management features

- Adding a cover: you can upload an image together with a video, and this image will be automatically set as video cover in the VOD media asset system.
- Specifying the expiration time: you can specify the expiration time of a media file when uploading it. After the specified time elapses, the VOD backend will automatically delete the media file and its associated files (e.g., output files and screenshots).
- Specifying the category: you can specify the category for the media file after it is uploaded.

Support conditions and usage of different upload methods are as shown below:

| Feature         | Local Upload Through Console                                               | Pull Through Console | Upload from Server                                                   | Upload from Client                                                   | Pull Through API                                                | Live Recording                                |
| ------------ | ------------------------------------------------------------ | -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Adding a cover     | Not supported                                                       | Not supported         | <ul style="margin:0;"><li>[SDK for Java](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[SDK for C#](https://intl.cloud.tencent.com/document/product/266/33915#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[SDK for PHP](https://intl.cloud.tencent.com/document/product/266/33916#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[SDK for Python](https://intl.cloud.tencent.com/document/product/266/33917#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[SDK for Node.js](https://intl.cloud.tencent.com/document/product/266/33918#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2)</li><li>[SDK for Go](https://intl.cloud.tencent.com/document/product/266/33919#.E6.90.BA.E5.B8.A6.E5.B0.81.E9.9D.A2) | <ul style="margin:0;"><li> [SDK for Web](https://intl.cloud.tencent.com/document/product/266/33924)</li><li>[SDK for Android](https://intl.cloud.tencent.com/document/product/266/33925)</li><li>[SDK for iOS](https://intl.cloud.tencent.com/document/product/266/33926)</li> | [`CoverUrl` parameter in the `PullUpload` API](https://intl.cloud.tencent.com/document/product/266/34118) | Not supported                                                       |
| Specifying the expiration time | Not supported                                                       | Not supported         | <ul style="margin:0;"><li>[`ExpireTime` parameter in the SDK for Java](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[`ExpireTime` parameter in the SDK for C#](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`ExpireTime` parameter in the SDK for PHP](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`ExpireTime` parameter in the SDK for Python](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`ExpireTime` parameter in the SDK for Node.js](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`ExpireTime` parameter in the SDK for Go](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0) | Not supported                                                       | [`ExpireTime` parameter in the `PullUpload` API](https://intl.cloud.tencent.com/document/product/266/34118)  | [Recording configuration](https://intl.cloud.tencent.com/document/product/267/34223) |
| Specifying the category     | [Specifying category](https://intl.cloud.tencent.com/document/product/266/33890) | Not supported         | <ul style="margin:0;"><li> [`ClassId` parameter in the SDK for Java](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[`ClassId` parameter in the SDK for C#](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`ClassId` parameter in the SDK for PHP](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`ClassId` parameter in the SDK for Python](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`ClassId` parameter in the SDK for Node.js](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`ClassId` parameter in the SDK for Go](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0) | [`ClassId` parameter in the signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922) | [`ClassId` parameter in the `PullUpload` API](https://intl.cloud.tencent.com/document/product/266/34118) | Not supported                                  |

#### Video processing and event notification

- Automatic video processing: you can specify a [task flow](https://intl.cloud.tencent.com/document/product/266/33931) for media upload. After upload is completed, VOD will automatically execute this task flow. Common scenarios of this feature include screencapturing the first video frame as cover, transcoding, and intelligent content recognition.
- Passthrough field in video processing event notification: if automatic video processing is enabled, after video is processed, the VOD backend will initiate an event notification to pass through this field to you.
- Passthrough field in upload event notification: after upload is completed, the VOD backend will initiate an event notification to pass through this field to you.

Support conditions and usage of different upload methods are as shown below:

| Feature         | Local Upload Through Console                                               | Pull Through Console | Upload from Server                                                   | Upload from Client                                                   | Pull Through API                                                | Live Recording                                |
| ------------------------ | ----------------------------------------------------------------------------------------------------------- | -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------- | -------- |
| Automatic video processing             | [Automatic video processing after upload](https://intl.cloud.tencent.com/document/product/266/33890) | Not supported         | <ul style="margin:0;"><li>[SDK for Java](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[SDK for C#](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[SDK for PHP](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[SDK for Python](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[SDK for Node.js](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)</li><li>[SDK for Go](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81) | [`procedure` parameter in the signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922) | [`Procedure` parameter in the `PullUpload` API](https://intl.cloud.tencent.com/document/product/266/34118)   | Not supported   |
| Passthrough field in video processing event notification | Not supported                                                       | Not supported         | Not supported                                                       | `sessionContext` parameter in the signature for upload from client                           | [`SessionContext` parameter in the `PullUpload` API](https://intl.cloud.tencent.com/document/product/266/34118) | Not supported   |
| Passthrough field in upload event notification     | Not supported                                                      | Not supported         | <ul style="margin:0;"><li>[`SourceContext` parameter in the SDK for Java](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[`SourceContext` parameter in the SDK for C#](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`SourceContext` parameter in the SDK for PHP](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`SourceContext` parameter in the SDK for Python](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`SourceContext` parameter in the SDK for Node.js](https://cloud.tencent.comhttps://intl.cloud.tencent.com/document/product/266/33918#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0)</li><li>[`SourceContext` parameter in the SDK for Go](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8E.A5.E5.8F.A3.E6.8F.8F.E8.BF.B0) | [`sourceContext` parameter in the signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922) | Not supported                                                       | Not supported   |

#### Upload control

- Checkpoint restart: if the upload is terminated unexpectedly due to causes such as network disconnection and closing of the browser, you can upload the file again from where it left off without the need to upload the entire file again.
- Pausing/resuming upload: during the upload, you can proactively pause or resume the upload.
- Canceling upload: during the upload, you can proactively cancel the upload.
- Getting upload progress: you can get the upload progress, i.e., the size ratio of the part already uploaded to VOD to the full file size.
- Multipart upload: during the upload, a media file will be divided into multiple parts for separated upload. If you are on a weak network, this feature can reduce the affect of disconnection caused by network exceptions. If your bandwidth is high, this feature can concurrently upload multiple parts to make full use of the network bandwidth.

Support conditions and usage of different upload methods are as shown below:

| Feature         | Local upload through console                                               | Pull through console | Upload from server                                                   | Upload from client                                                   | Pull through API                                                | Live recording                                |
| -------------- | -------------------- | -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------ | ------------------------------------------------------------ |
| Checkpoint restart       | Not supported               | N/A         | Not supported                                                       | <ul style="margin:0;"><li>[SDK for Web](https://intl.cloud.tencent.com/document/product/266/33924)</li><li>[SDK for Android](https://intl.cloud.tencent.com/document/product/266/33925)</li><li>[SDK for iOS](https://intl.cloud.tencent.com/document/product/266/33926)</li> | N/A       | N/A                                      |
| Pausing/Resuming upload | Not supported               | N/A         | Not supported                                                       | <ul style="margin:0;"><li>[SDK for Web](https://intl.cloud.tencent.com/document/product/266/33924)</li><li>[SDK for Android](https://intl.cloud.tencent.com/document/product/266/33925#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>[SDK for iOS](https://intl.cloud.tencent.com/document/product/266/33926#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li> | N/A       | N/A                                      |
| Canceling upload       | Refresh or close the page in browser | N/A         | N/A                                                       | <ul style="margin:0;"><li>[SDK for Web](https://intl.cloud.tencent.com/document/product/266/33924)</li><li>[SDK for Android](https://intl.cloud.tencent.com/document/product/266/33925#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li><li>[SDK for iOS](https://intl.cloud.tencent.com/document/product/266/33926#.E9.AB.98.E7.BA.A7.E5.8A.9F.E8.83.BD)</li>| N/A       | [StopLiveRecord](https://intl.cloud.tencent.com/document/product/267/30837) |
| Getting upload progress   | The progress is displayed on the page by default     | Not supported         | Not supported                                                       | <ul style="margin:0;"><li>[SDK for Web](https://intl.cloud.tencent.com/document/product/266/33924)</li><li>[SDK for Android](https://intl.cloud.tencent.com/document/product/266/33925)</li><li>[SDK for iOS](https://intl.cloud.tencent.com/document/product/266/33926)</li> | Not supported       | N/A                                      |
| Multipart upload       | Enabled               | N/A         | <ul style="margin:0;"><li> [SDK for Java](https://intl.cloud.tencent.com/document/product/266/33914)</li><li>[SDK for C#](https://intl.cloud.tencent.com/document/product/266/33915#.E8.B0.83.E7.94.A8.E4.B8.8A.E4.BC.A0)</li><li>[SDK for PHP](https://intl.cloud.tencent.com/document/product/266/33916#.E8.B0.83.E7.94.A8.E4.B8.8A.E4.BC.A0)</li><li>[SDK for Python](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E5.88.86.E7.89.87.E5.B9.B6.E5.8F.91.E6.95.B0)</li><li>[SDK for Node.js](https://intl.cloud.tencent.com/document/product/266/33918)</li><li>[SDK for Go](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E5.88.86.E7.89.87.E5.B9.B6.E5.8F.91.E6.95.B0) | <ul style="margin:0;"><li> It is enabled for the SDK for Web by default</li><li>It is enabled for the SDK for Android by default</li><li>It is enabled for the SDK for iOS by default</li> | N/A       | N/A                                                       |

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
<td>Live recording</td>
<td><ul style="margin:0;"><li>For MP4/FLV formats, the upper limit is 48.82 TB (50,000 GB)</li><li>There is no upper limit for files in HLS format</li><li> Other restrictions are subject to <a href="https://intl.cloud.tencent.com/document/product/267/31563">live recording</a></td>
</tr>
</tbody></table>
- Number of files: unlimited.

