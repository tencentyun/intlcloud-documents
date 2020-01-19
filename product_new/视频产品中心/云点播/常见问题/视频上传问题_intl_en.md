### What media file formats are supported for upload to VOD?

Supported formats for upload to VOD include:
- Video: MP4, TS, FLV, WMV, ASF, RM, RMVB, MPG, MPEG, 3GP, MOV, WEBM, AVI.
- Audio: MP3, M4A, FLAC, OGG, WAV.

### What are the ways to upload files to VOD? Is upload resumable?
Files can be uploaded to VOD in the following ways: [upload through console](https://cloud.tencent.com/document/product/266/2841), [upload from server](https://cloud.tencent.com/document/product/266/9759), and [upload from client](https://cloud.tencent.com/document/product/266/9219). Among them, upload from client supports resumable upload.

### How do I upload a video to VOD in the console?
For more information, please see [Uploading Videos](https://cloud.tencent.com/document/product/266/2841).


### How do I get the upload progress in VOD?

Upload progress cannot be obtained currently.

### How long will it take before an uploaded video can be watched?
The preparation time after upload is subject to the video duration and transcoding bitrate.

### Does VOD allow video upload by using an application or visiting a webpage?

VOD allows end users to upload files directly. For more information, please see [Guide for Upload from Client](https://cloud.tencent.com/document/product/266/9219).

### What are the upload directories on the VOD backend?
Currently, there is no directory feature. You can use the category structure as the directory and upload files to the corresponding categories. For more information, please see [Modifying Video Categories](https://cloud.tencent.com/document/product/266/36449).

### Can the uploaded videos be compressed?
Currently, compression is not supported, and only original video files can be uploaded.

### How do I upload a large number of video files to VOD?

VOD uses a queuing upload method to ensure sequential uploading of video files. If you have special needs (for example, you need to upload terabytes to petabytes of files), please call 95716.
### The upload return URL is in HTTP. How do I set it to HTTPS?
For more information, please see [Primary Distribution URL Configuration](https://cloud.tencent.com/document/product/266/33373).

### What are the development environment requirements of VOD's web upload SDK?
- The browser needs to support HTML5.
- The application server needs to distribute a signature for upload from client. For the method of generating a signature, please see [Simple Video Upload](https://cloud.tencent.com/document/product/266/9239#.E7.AE.80.E5.8D.95.E8.A7.86.E9.A2.91.E4.B8.8A.E4.BC.A0).

### What upload SDKs does VOD provide for mobile devices?

Currently, VOD provides Android SDK and iOS SDK for mobile devices.
In addition to the APIs used to upload videos, mobile SDKs also provide a rich set of video editing APIs (e.g., video clipping, splicing, filtering, and subtitling) to meet your diverse needs.

### Can I specify an encrypted transcoding template in the signature for video upload?
No. This feature is under development and will be available in the future.

### Do the video upload APIs of VOD support Go, PHP, and .NET?
You can use TencentCloud API 3.0 that supports SDKs for Go, PHP, and .NET. For more information, please see [ApplyUpload API documentation](https://cloud.tencent.com/document/product/266/31767#SDK).



### How do I share a link to an uploaded video?
You can share a link after the video is uploaded in the following steps:
1. Apply for release in the console.
2. After the application is approved, a sharable link will be returned.
3. Use the link to share the video.

For more information, please see [Video Release Steps](https://cloud.tencent.com/document/product/266/36452#.E8.A7.86.E9.A2.91.E5.8F.91.E5.B8.83.E6.AD.A5.E9.AA.A4).
