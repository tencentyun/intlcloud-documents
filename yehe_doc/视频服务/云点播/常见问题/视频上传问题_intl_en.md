### What media file formats are supported for upload to VOD?

Supported VOD file formats:
- Video: WMV, RM, MOV, MPEG, MP4, 3GP, FLV, AVI, RMVB, TS, ASF, MPG, WEBM, MKV, M3U8, WM, ASX, RAM, MPE, VOB, DAT, MP4V, M4V, F4V, MXF, QT, and OGG
- Audio: MP3, M4A, FLAC, OGG, WAV, RA, AAC, and AMR
- Thumbnail: JPG, JPEG, PNG, GIF, BMP, TIFF, AI, CDR, EPS, and TIF

### How can I upload files to VOD? Is checkpoint restart supported?
Files can be uploaded to VOD in the following ways: [upload through console](https://intl.cloud.tencent.com/document/product/266/33890), [upload from server](https://intl.cloud.tencent.com/document/product/266/33912), and [upload from client](https://intl.cloud.tencent.com/document/product/266/33921). Among them, upload from client supports checkpoint restart.

### How do I upload a video to VOD in the console?
For more information, please see [Uploading Video](https://intl.cloud.tencent.com/document/product/266/33890).


### How do I get the upload progress in VOD?

Currently, upload progress cannot be obtained.

### When will the video be available for viewing after upload?
It depends on the length of the video and transcoding bitrate.

### Does VOD allow video uploads by applications or webpages?

VOD allows end users to upload files directly. For more information, please see [Guide](https://intl.cloud.tencent.com/document/product/266/33921).

### What are the upload directories on the VOD backend?
Currently, VOD doesn't offer upload directories. You can use the category structure as the directory and upload files to the corresponding categories. For more information, please see [Modifying Video Category](https://intl.cloud.tencent.com/document/product/266/33893).

### Can the uploaded videos be compressed?
Currently, video compression is not supported.

### How do I upload a large number of video files to VOD?

VOD uses a queuing upload method to ensure sequential uploading of video files. If you have special needs (for example, you need to upload terabytes to petabytes of files), please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).

### The upload return URL is in HTTP. How do I set it to HTTPS?
For more information, please see [Default Distribution Configuration](https://intl.cloud.tencent.com/document/product/266/35768).

### What are the required development environments for VOD's web upload SDK?
- The browser needs to support HTML5.
- The application server needs to distribute a signature for upload from client. For the method of generating a signature, please see [Simple Upload of Video](https://intl.cloud.tencent.com/document/product/266/33924).

### What upload SDKs does VOD provide for mobile devices?

Currently, VOD provides Android SDK and iOS SDK for mobile devices.
Apart from video upload APIs, mobile SDKs also provide a rich collection of video editing APIs to satisfy customer demands. The collection ranges from video clipping, splicing, filtering to subtitling.

### Can I specify an encrypted transcoding template in the signature for video upload?
No. This feature is under development and will be available in the future.

### Do the video upload APIs of VOD support Go, PHP, and .NET?
TencentCloud API 3.0 supports SDKs for Go, PHP, and .NET. For more information, please see the [ApplyUpload API documentation](https://intl.cloud.tencent.com/document/product/266/34120).



### How do I share the link after uploading a video successfully?
You can share the link by following the steps below:
1. Apply for release in the console.
2. After the application is approved, a sharable link will be returned.
3. Use the link to share the video.

For more information, please see [Managing Video](https://intl.cloud.tencent.com/document/product/266/33896).

### Can a cover be automatically generated for a video uploaded to VOD?

Yes. When a video is uploaded, VOD uses the first frame as the cover or pulls the cover from the video.


### Does video pull in VOD support M3U8 files?

Currently, M3U8 files cannot be pulled.
