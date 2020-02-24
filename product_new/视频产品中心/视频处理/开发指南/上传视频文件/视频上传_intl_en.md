
## Video Upload Methods
MPS supports the following video upload methods:

- Upload via console: You can log in to the [COS Console](https://console.cloud.tencent.com/product/cos) and [upload](https://intl.cloud.tencent.com/document/product/436/6233) local video files to a COS bucket. This method is suitable for uploading a small number of videos.
- Upload via client: You can upload local video files to a COS bucket through a COS SDK. This method features simple upload for small files and multipart upload for large ones. You can pause, resume or cancel uploads, making it suitable for both user generated content (UGC) and professionally generated content (PGC). The upload methods are as follows:
  - [Simple Upload](https://intl.cloud.tencent.com/document/product/436/14113)
  - [Multipart Upload](https://intl.cloud.tencent.com/document/product/436/14112)
  
## Supported Audio/Video File Formats

* Video: MP4, TS, FLV, WMV, ASF, RM, RMVB, MPG, MPEG, 3GP, MOV, WEBM, MKV, and AVI
* Audio: MP3, M4A, FLAC, OGG, WAV, and AMR

> MPS will transcode files in the above container formats according to your workflow settings. Files not in the above formats will not be touched.
