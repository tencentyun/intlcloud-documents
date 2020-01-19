### How do I find the cause of playback failures?
There are lots of causes of playback failures. You can locate the problems in the following steps:

1. Configure packet capture and check network requests.
2. Check the error messages in the web console.
3. Find out whether the video format is supported by the browser.


### Are there any limits on the number of online viewers at the same time?

Theoretically no. As the VOD system does not set any limits, it allows an unlimited number of online viewers to watch videos at the same time.


### How do I solve the problem of lagging during playback?

If the video file itself is ruled out as the cause, lagging may be attributable to low device specification or poor network environment (e.g., bandwidth and latency). You can change the device used for playback or the network environment if possible. If the problem persists, please [contact us](https://cloud.tencent.com/document/product/266/19905).

### When I try to play back a video using HTTP on an HTTPS page, it is blocked by the browser. How do I fix this?
The browser blocks the video for security reasons. Please make sure that videos using HTTP are played back on the webpage using the same protocol, and the same is true for HTTPS videos.

### What should I do if a 404 error is returned for a video link and the video does not exist on CDN?
Please [contact us](https://cloud.tencent.com/document/product/266/19905) to help you locate the problem and restore CDN resources.

### What should I do if a 403 error is returned for a video link and the video cannot be loaded?
Please check whether referer or key hotlink protection has been enabled and whether there are authentication parameters during playback.

### How do I solve the problem where a video can be played back normally except on WeChat?
This is because the WeChat browser blocks the video. You need to appeal to WeChat to remove the blockage.

### What should I do if a video cannot be played back on PCs and an error message about cross-domain access appears in the web console?
To play back videos with Flash on PCs, the `crossdomain.xml` file and correct access policy need to be configured and cross-domain access need to be enabled for the video storage server.

**Function of `crossdomain.xml`**
- When an SWF file in the `www.a.com` domain needs to access a file in `www.b.com`, SWF first checks whether the `crossdomain.xml` file is in the root directory of the `www.b.com` server, and if not, the access will fail; if the file is there and access is allowed for the `www.a.com` domain, the communication will be normal.
- `crossdomain.xml` contains the domain name configuration of the SWF file.

To play back videos in HLS or FLV format by using HTML5 in modern PC browsers, [CORS](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS) needs to be configured for the video server.
Generally, the above two policies are configured automatically by Tencent Cloud. If you have any problems, please [contact us](https://cloud.tencent.com/document/product/266/19905).

### How do I solve the problem where the player prompts that the video is not transcoded?
Please transcode the video. For detailed directions, please see [Processing Videos](https://cloud.tencent.com/document/product/266/2841#.E5.A4.84.E7.90.86.E8.A7.86.E9.A2.91). Please make sure that the video encoder is H.264 and container format is MP4 or HLS.

### Can I add different watermarks for different viewers?
VOD only allows specifying image or text watermarks during transcoding and does not support dynamic watermarking for different viewers.

### Does VOD offer video editing features such as dubbing, mixing, brightness adjustment, rotation, or picture-in-picture?
Yes. For more information, please see [media production](https://cloud.tencent.com/document/product/266/37534) in the video processing features of VOD.

### How do I solve the problems such as blurred screen, blank screen, lagging, and playback failures after transcoding?
You need to first find out whether there is any problem with the source video. If the problem is caused by transcoding, please [contact us](https://cloud.tencent.com/document/product/266/19905).

### Are there any prompts if playback is not supported by a browser?
Generally, web playback depends on the decoder of the browser or the Flash decoder. If playback is not supported, error code `3` or `4` will be returned.

### What should I do if videos in RTMP or FLV format cannot be played back or videos cannot be played in IE?
Flash is required for playing back RTMP and FLV videos as well as any videos in IE. Please install and enable it.

### What should I do if videos in HLS or FLV format cannot be played back by using HTML5 when Flash is not supported by a PC browser?
If Flash is not supported, the player will use MSE to play back videos in HLS or FLV format; if MSE is not supported either, you will have to change or upgrade the browser. Currently, browsers that support MSE include Microsoft Edge, Chrome, Mozilla Firefox, and Safari 11+.

### What should I do if a browser does not support decoding H.264 videos or playing back videos in MP4 or HLS format?
Generally, there is no corresponding video decoder in the browser kernel of some PC software programs or applications in integrated or lite editions. Please upgrade the browser kernel in them or integrate with Flash and allow it to be called.

### How do I prevent my videos from being downloaded and played back by others?
To play back a video online is to download it first and then play it back, so it is impossible to prevent a video from being downloaded by others. If you want your videos not to be played back after being downloaded by others, please see [video encryption](https://cloud.tencent.com/document/product/266/9638) in VOD.

### How do I solve the problem where an HLS-encrypted video cannot be played back?
The playback process of an HLS-encrypted video is different from that of ordinary videos. Generally, you need to get the right key. The steps to fix this problem are as follows:
1. Check whether the M3U8 file format is compliant, the address from which to get the key is correct, key API server authentication is normal, and the result can be returned by the key API normally.
2. Check the length of the key and make sure that the key length is 16 bytes and can be decrypted correctly.

### How do I solve the problem where a video cannot be played back normally or returns to the beginning after being dragged to a certain time point?
You are recommended to avoid playing back the source video; instead, transcode it first in VOD. Please select the HTML5 playback mode rather than use Flash. When a video is too short, there is generally only one keyframe, so dragging for playback is not supported.

### How do I solve the problem where a video cannot be played back automatically?
Autoplay of multimedia files is prohibited in many browsers, especially mobile ones. However, some browsers allow autoplay of muted videos or videos with no audio tracks, so you can try to mute the player. If this still does not work, there will be no effective solutions currently.

### How do I solve the problem where autoplay fails in the WebView of a hybrid application?
The multimedia autoplay attribute needs to be set in the WebView:
- iOS: mediaPlaybackRequiresUserAction = NO
- Android: webView.getSettings().setMediaPlaybackRequiresUserGesture(false)

### How do I solve the problem where the video frames are invisible after the player is initialized?
Whether a web player displays the first video frame depends on the support from the browser. Currently, not all browsers support showing the first video frame. You can fix this problem by setting a cover for the video.

### What if a player does not have an adjustable-speed playback option or the feature is unavailable?
Currently, only some modern browsers support adjustable-speed playback in HTML5, and this feature is not supported by Flash. Therefore, adjustable-speed playback is allowed only in browsers that support HTML5.
You can try the HTML5 mode for playback; if the adjustable-speed playback button does not appear, this feature is not supported; if the button appears but the speed cannot be adjusted, the player has detected that the current browser supports setting adjustable-speed playback, but the settings fail to take effect. In this case, you are recommended to hide the adjustable-speed playback button.


### How do I solve the problem where a video cannot be overridden by other elements?
The player controls are the browser's built-in controls. You need to stop pinning the video by using the method provided by the browser vendor. Currently, there are no general solutions.

### How do I solve the problem of unnecessary icons?
You can try to hide the video tag, which can be displayed again when playback starts.

### How do I block ads, downloads, and recommendations in the player?
Ad placement (e.g., ads appear when playing a video on WeChat) is a kind of hijacking by browser vendors. You have to block ads as permitted by browser vendors. Currently, there are no general solutions.

### What should I do if videos fail to move along with the page on Android?
Tests show that there no effective frontend solutions. This is because after hijacking video playback, the browser fails to optimize the viewing experience effectively. You can try to use the video tag directly (not generated by the player) or draw the video by using Canvas. If the problem persists, it can only be solved by upgrading the browser.

### How do I solve the problem of letterboxing (black bars) during video playback?
Please make sure that the aspect ratio of the player is the same as the actual ratio of the video.
For example, if a video's resolution is 1280 * 720, the size of the player can be set to 640 * 360 or 1280 * 720. As long as the ratio equals to 16:9 (1280:720), the video can be fully displayed with no black bars. If the video has black bars itself, they need to be cut off during transcoding to change the resolution.

### How do I solve the problem where landscape/portrait mode switching during a push does not take effect in the player?
Currently, a web player is unable to detect landscape/portrait mode switching during a push, so this problem has to be addressed in other ways.
For example, assume that the portrait mode is used when a push starts, and the aspect ratios of the upstream video and the web player are both 9:16; if the push is not interrupted on the device (depending on the support from the push SDK) and the portrait mode is switched to the landscape mode, the aspect ratio of the upstream video will change to 16:9. If the aspect ratio of the downstream video also changes to 16:9, reconnection to the web player will be needed before the video can be played back at the new aspect ratio. In order to reconnect, the web player needs to be notified by an external API. If the aspect ratio of the downstream video is still 9:16, the video will be played back at 9:16.

### What are the differences between playback password and hotlink protection in VOD?
The playback password is actually implemented on the player, so you must have a correct password to watch a video. 
Hotlink protection is implemented on the domain name, and only requests from the domain names in the whitelist can pull video resources.

### Does a VOD playback address support the DNS protocol of HTTP?
A VOD playback address does not support the DNS protocol of HTTP currently.

### Why can a video be played back in VOD on mobile phones but not on PCs?
Flash needs to be enabled in PC browsers.
