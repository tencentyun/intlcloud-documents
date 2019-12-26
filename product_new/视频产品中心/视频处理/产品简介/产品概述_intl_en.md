Tencent Cloud Media Processing Service (MPS) provides cloud-based transcoding and processing services for massive amounts of audio/video data. In addition to performing various operations such as watermarking and screencapturing, it can transcode audio and video files to different formats suitable for playback through OTT and on computers or mobile devices, helping you adjust the bitrate and resolution of audio/video data for different platforms with ease.

## Product Architecture
You can upload source video files to a Cloud Object Storage (COS) bucket through the console, SDKs, or APIs. The workflow mechanism of MPS will trigger automatic execution of video processing tasks for such files and send event notifications to Cloud Message Queue (CMQ), so that you can be promptly informed of the execution status of the transcoding tasks. The product architecture of MPS is as shown below.
![](https://main.qcloudimg.com/raw/97b9e397152a18a921011f7a489c6ce0.png)
