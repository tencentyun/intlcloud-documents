### Upload
- VOD supports multiple ways to upload media. You can upload media from local storage, a URL, or a client. You can also upload media through an API.
- VOD can convert a live recording to a video on-demand and has various features such as multi-format video upload, large file upload, checkpoint restart, and redundant file backup.
- VOD delivers an industry-leading upload success rate of over 99.5% (upload under poor network conditions and large file upload are taken into account) through various upload acceleration methods, including optimization of scheduling, global multi-storage region coverage, transfer, and protocols as well as linkage supplement.

### Production
- VOD provides a wide range of media production features, including frame-by-frame editing, multi-track production, picture-in-picture, cropping, filters, playback speed adjustment, audio mixing, transitions, audio/video separation, animated text/image effects, and shortcut keys, fully meeting your diverse content production needs.
- VOD features video production in the console, which makes it easy for you to produce videos online.

### Storage
- VOD features redundant storage of video files across architectures and devices to support remote disaster recovery and isolation of resources.
- The smart cold storage feature provides you with more storage options and helps you reduce your storage costs.
- Media files can be deleted upon can be deleted automatically when they expire, saving storage space and reducing storage costs.
- Media files can be partly deleted. Only LD videos will be retained for old videos, and HD videos will be deleted to reduce storage costs.

### Transcoding
- VOD has more than 12,000 distributed transcoding clusters, which can support up to 2,000 concurrent transcoding tasks.
- You can add watermarks to videos as needed and set different transcoding formats to flexibly satisfy your needs in different scenarios.
- VOD supports various screencapturing operations, including thumbnail, image sprite, and animated image generation as well as time point screenshots and sampled screenshots, which can be used for thumbnail preview and video timestamping.

### Distribution
- With access to Tencent Cloud's over 2,800 CDN cache nodes, VOD can provide a smooth, accelerated video content delivery to users around the globe based on BGP networks and more than 17 ISPs across China.
- VOD provides a default domain name for video playback. You can use the default domain name or use your own custom domain name to deliver media.
- VOD provides a complete CDN usage statistics analysis service. In addition, it allows you to download CDN logs of the access status of the connected domain name, making your business operations more effective.

### Media AI
Powered by Tencent Cloud's leading AI technologies and rich experience in content management, VOD offers media AI capabilities including content moderation, content analysis, and content recognition, helping you minimize manual work.
- Content moderation: VOD leverages AI technologies to detect pornographic and other problematic content in images, speech, and text. It can detect various types of sensitive information with different levels of strictness to meet your and your customers' needs, helping you protect your brand image and avoid potential legal risks.
- Content analysis: Intelligent classification, labeling, and thumbnail generation
- Content recognition: Face recognition, speech recognition (smart subtitling is supported), OCR, and opening and closing credits recognition

### Copyright protection
VOD's hotlink protection, digital watermark, and commercial-grade DRM encryption features provide high-level security protection for your content.
- Hotlink protection: VOD provides referer and key hotlink protection solutions to prevent the media content from being hotlinked or downloaded and spread without authorization. This helps to safeguard your copyrighted content and protect your revenue.
- Digital watermarking: VOD offers watermark solutions with high protection levels and low costs to protect your content against piracy. Using a digital watermark, you can extract a user ID from a video to find the user responsible for distributing it without authorization. This deters piracy and enables you to take action against copyright infringement.
- Commercial-grade DRM encryption: VOD offers an easy-to-use DRM scheme that is built on established DRM solutions and integrates a full range of features including DRM encryption, certificate management, license distribution, decryption, and playback.

### Image processing
VOD provides easy-to-use and rich-featured real-time image processing capabilities.
- VOD supports real-time operations such as batch image zoom and cropping and global delivery acceleration based on the VOD acceleration service.
- With the help of AI technology, VOD can detect non-compliant content in video images, helping you manage your content more efficiently.

### Adaptive bitrate streaming
- VOD can automatically select the most appropriate bitstream based on the changes in the user's network speed to play back the video at the optimal definition while guaranteeing a smooth and clear playback experience.
- VOD allows you to associate multilingual subtitles with the output file of adaptive bitrate streaming. During playback, users can switch between subtitles in different languages. This feature helps increase cross-border viewer rates, and allows more viewers in target regions to understand and enjoy video content.

### TSC transcoding
Based on Tencent Cloud's many years of experience in technologies such as audio/video encoding, smart scene recognition, dynamic encoding, and three-level (CTU/line/frame) precise bitrate control model, TSC transcoding offers a higher subjective image quality at a lower bitrate (reduced by nearly 50%), reducing both the network traffic and storage costs.

### Player
VOD provides a free Player SDK, which is compatible with many mainstream platforms, easy to use, and offers rich features and detailed playback quality data.
- The Player SDK is compatible with iOS, Android, web (Flash/HTML5), and Flutter.
- The Player SDK supports adaptive bitrate streaming to automatically play back an appropriate bitstream based on the user's network quality, delivering a smooth playback to viewers.
- The Player SDK provides various features such as instant broadcasting of the first frame, player pre-roll, mid-roll, and post-roll images, buffering while playback, playback speed change, video timestamping, on-screen commenting, and addon subtitles.
- The Player SDK supports various video security solutions such as hotlink protection, URL authentication, HLS encryption, and private protocol encryption.
- High playback quality: The Player SDK utilizes CDN acceleration for the audio/video content to play back media more smoothly. It also supports the QUIC protocol, which delivers a better quality under poor network conditions.
- The playback APIs are simple and can play back media files by media asset ID.
- The Player SDK provides third-party player plugins to play back VOD videos.
- The Player SDK supports monitoring the video playback quality over the entire linkage through multidimensional metrics such as playback performance, user behaviors, and file characteristics, so as to facilitate efficient business operations.

### CSS and VOD combination
A series of CSS-VOD combination solutions are provided based on the unified ecosystem of CSS and VOD.
- CSS recording: It is a service that stores the files generated by muxing original streams (without modifying information such as audio and video data and corresponding timestamps) on the VOD platform. It can be used for ensuring compliance with regulatory requirements for live stream archiving as well as for secondary processing and multiple deliveries of VOD media.
- Time shifting: After a live stream is started, a viewer can choose a previous time point to start watching and switch back to the latest live content whenever they want to. This feature can be used to replay highlights of live streamed sports events.
- Live clipping: You can use live clipping to clip out an earlier portion of an ongoing live stream and generate a video (in HLS format) in real time so it can be shared immediately or stored persistently as a VOD video. This makes it easy to quickly generate highlights during live streaming.
- VOD-to-CSS: This feature allows you to deliver a recorded VOD file as a pseudo-live stream at the specified time with added control features such as "playback time constraint" and "syncing playback progress". This is much more cost-effective and has lower compliance risks that actual live streaming.

### Media compliance
- Smart moderation: VOD intelligently recognizes non-compliant media content, so as to reduce the manual moderation costs, improve the moderation efficiency, and build a robust shield for the platform content security.
- Media playback blocking: VOD allows you to prohibit the playback of non-compliant media content, so as to prevent such content from being further spread.
