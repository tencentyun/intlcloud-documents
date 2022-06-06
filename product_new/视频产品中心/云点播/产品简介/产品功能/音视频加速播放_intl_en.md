## System Architecture
<img src="https://qcloudimg.tencent-cloud.cn/raw/be78076deba4b5996bc6d2f63a892749.png" width="650">

## Features
### Domain name customization
- You can use the default domain name provided by Tencent Cloud or use your own custom domain name for video playback.
- You can configure different hotlink protection and release rules for different playback domain names.

### Hotlink protection
- Referer hotlink protection lets your control the access to your video assets by using the `referer` field in HTTP requests. This allows you to protect your content from being hotlinked by other websites.
- You can configure IP blocklists/allowlists to restrict access from certain IPs and protect media from malicious users.
- VOD also supports key and timestamp hotlink protection so you can set an expiration time for access to videos.
- The hotlink protection feature for member video preview allows you to configure a time limit for video previews. When a user previews a video, the video preview will end when the time limit is reached, and playback can be resumed after the user makes a membership payment.

### Player SDK
- VOD offers player SDKs for iOS, Android, and web. They support pre-roll, mid-roll, and post-roll images, on-screen comments (for web player only), customizing the player logo, and player password configuration.
- VOD supports quick release through iframe and progressive loading of video files.
- VOD offers APIs for getting playback status and setting events.

### Business statistical analysis
- VOD provides tools for you to analyze the statistics of your video services, allowing you to keep track of traffic, bandwidth, and clicks by time, region, and ISP.
- You can view statistics for all the video files, including playback count and traffic of each video.
