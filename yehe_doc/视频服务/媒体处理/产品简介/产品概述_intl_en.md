MPS is a cloud-based audio/video processing service. Built on Tencent's many years of experience in audio/video technologies, it provides ultimate encoding capabilities that enable you to play back audio/video files on various platforms at greatly reduced storage and bandwidth costs. It provides a rich set of features including video screencapturing, audio/video enhancement, content discovery, and content moderation, satisfying your video processing needs in a range of different scenarios.

## Product Architecture
You can upload source video files to a COS bucket through the console, SDKs, or APIs. You can use the **scheme** mechanism of MPS to trigger the automatic execution of video processing tasks and send event notifications to CMQ. This helps you stay informed of the status of transcoding tasks. The architecture of MPS is shown below:

<img src="https://qcloudimg.tencent-cloud.cn/raw/4efd48508c63bb8169f9cad585240ce0.png" style="box-shadow: none;">