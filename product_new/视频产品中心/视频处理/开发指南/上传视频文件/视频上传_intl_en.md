
## Video Upload Methods
MPS supports the following video upload methods:

- Upload in the console: You can log in to the [COS Console](https://console.cloud.tencent.com/product/cos) and [upload](https://intl.cloud.tencent.com/document/product/436/6233) local video files to a COS bucket. This method is suitable for uploading a small number of videos.
- Upload through the client: You can upload local video files to a COS bucket through a COS SDK. This method features simple upload for small files and multipart upload for large ones. It supports operations such as upload pause, resumption, and cancellation, making it suitable for scenarios such as user generated content (UGC) or professionally generated content (PGC). The upload methods are as follows:
  - [Simple Upload](https://intl.cloud.tencent.com/document/product/436/14113)
  - [Multipart Upload](https://intl.cloud.tencent.com/document/product/436/14112)
  
## Supported Container Formats of Audio/Video Files

* Video: MP4, TS, FLV, WMV, ASF, RM, RMVB, MPG, MPEG, 3GP, MOV, WEBM, MKV, and AVI
* Audio: MP3, M4A, FLAC, OGG, WAV, and AMR

> MPS will transcode files in the above container formats according to your workflow settings and leave files in other formats alone.
