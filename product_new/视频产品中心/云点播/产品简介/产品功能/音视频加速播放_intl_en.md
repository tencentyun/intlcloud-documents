## System Architecture
<img src="https://main.qcloudimg.com/raw/146d801f4900734b8faa0435b34ea6cc.png" width="650">

## Features
### Customizing domain names
- VOD supports the use of Tencent Cloud domain names or custom playback domain names.
- VOD supports setting different hotlink protection and release rules for different playback domain names.

### Hotlink protection
- VOD supports the configuration of referer hotlink protection, which implements access control via the `referer` field in HTTP requests to protect websites against hotlinking.
- VOD supports configuration of IP blocklist/allowlist to filter access source IPs and effectively defend against malicious users.
- VOD supports key and timestamp hotlink protection to control the expiration time of access.
- The innovative hotlink protection feature for member video preview in VOD allows configuration of the time limit for video preview. The playback will end when the time limit for preview is reached and will be resumed after successful membership payment.

### Player SDK
- VOD offers player SDKs for iOS, Android, and web that support pre-roll, mid-roll, and post-roll images, on-screen comments (for web player only), customization of player logo, and configuration of player password.
- VOD supports quick release through iframe and progressive loading of video files.
- VOD offers APIs for getting playback status and setting events.

### Business statistical analysis
- VOD provides statistical analysis service for video business, allowing you to keep track of traffic, bandwidth, and clicks by time, region, and ISP.
- VOD provides statistical analysis service for all the video files and supports viewing playback count and traffic of an individual video.
