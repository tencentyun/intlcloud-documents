
Relying on Tencent's many years of experience in audio/video processing and cutting-edge infrastructure, Tencent Cloud Video on Demand (VOD) provides one-stop VPaaS (Video Platform as a Service) solutions for capturing and upload, storage management, automated transcoding, content delivery, asset resource management, and communications of audio/video files to customers that operate audio/video applications. Thanks to its flexible, fast, high-quality video distribution features and ability to quickly build stable and reliable video distribution capabilities, VOD enables you to focus on the business itself, select appropriate services as needed, and respond to market changes with agility.

## Product Architecture
<img src="https://main.qcloudimg.com/raw/6eca7588b39959a7ca3242491a57e503.png" width="750"><br>
Cloud Video Storage, Video Transcoding Service, and Video Playback Acceleration are the core components of VOD.

- **Cloud video storage**
  This service uploads or pulls video content through the console for storage on the media asset management backend. It can perform various operations on the stored videos as needed, such as cold/hot backup, media asset management, and video information retrieval.
- **Video transcoding service**
  In the [VOD Console](https://console.cloud.tencent.com/vod/overview), you can perform intelligent audits such as video audit and content recognition on the obtained source video data. You can also transcode, take screenshots of, add watermarks to, encrypt, and set covers for videos and do much more.
- **Video playback acceleration**
  With the aid of thousands of CDN cache nodes across China, this service distributes and manages your audio/video resources to deliver a multi-channel, flexible, and smooth viewing experience. You can use your own or Tencent Cloud's player SDKs to integrate with your existing business. You can also generate dedicated WeChat Official Account links to your videos for video release through your WeChat Official Account.
