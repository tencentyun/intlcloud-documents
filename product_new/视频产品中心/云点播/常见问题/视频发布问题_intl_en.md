### What are the definitions and resolutions of videos published in VOD?

VOD provides a rich set of transcoding features for video release. In order to deliver a better viewing experience in different network environments, you can transcode and publish videos based on the following recommended definition categories:
- LD (mobile): bitrate: 256 Kbps; resolution: around 320 * 240.
- SD: bitrate: 512 Kbps; resolution: around 640 * 480.
- HD: bitrate: 1,024 Kbps; resolution: around 1280 * 720.
- FHD: bitrate: 2,500 Kbps; resolution: around 1920 * 1080.

The detailed specifications and technical parameters of output videos after transcoding are as follows:
![](https://main.qcloudimg.com/raw/478ef85c096df8dec3478b32693045ba.png)

If the resolution of an uploaded video does not match the values above, the video will be transcoded to a resolution with a standard width in the corresponding category and a proportionally scaled height.

If the resolution of the uploaded video is lower than the set transcoding specification (for example, a video with a resolution of 640 * 480 is uploaded, but the transcoding is set to HD), the system will still transcode it according to the set format (i.e., HD here). However, as the video itself has a lower definition, the user experience may be poor and traffic and bandwidth will be consumed.

### Can a video be transcoded from a low resolution to a high resolution? Can video quality be improved by transcoding?
VOD can transcode a video to a resolution higher than the original one, but the video quality will not be improved.


### Does the video release effect vary by time and region?

No, theoretically. The VOD system is enabled for access from anywhere at any time. Please note that the viewing experience is greatly determined by the quality of the network from user device to video server and the device specifications. Therefore, during peak hours of network service, the experience may vary due to the change of network conditions or low device specifications.

### If I modify the player configuration after releasing the "web player code", do I need to release the previously released HTML code again?

You do not need to generate the code again, because it is maintained and updated by the system automatically. After the player configuration is modified, the released player code will take effect immediately.

### In "Media Assets", what is the difference between "Source File URL" and "Video with Web Player Code" displayed in "Video Release"?

The URL of a source file corresponds to a video file of a specific bitrate, which does not contain any player information itself and can be opened directly in a browser for playback.

The web player code corresponds to the code that can be edited on the web, including the Flash address, adaptive HTML code, IFRAME code, player settings information (such as definition, roll content, and sharable link), and security password (optional). This code can be embedded in a user-edited webpage.


### In "Web Players", what will happen if I delete a custom player?
As the custom player has been deleted, video files will be automatically associated with the current default player configuration, but the code that has already been released can continue to be used. If you need to make changes, please define the player and release the code again.


### Why isn't a published video played back automatically?

If no custom configuration is made, the default configuration will be used when a video is uploaded and published, that is, the autoplay feature is disabled. You can modify this setting by checking "Autoplay" when publishing videos.


### Why is an output video not as clear as the source video?

The definition of a video during playback depends on the following two aspects:
- The definition provided by the VOD server after the video is transcoded and published.
- The network environment where the user watches the video. Decrease in definition during video playback may be caused by two factors: one is that a low-definition instead of high-definition video is stored in VOD; the other is that the player may be adapted to a low definition for playback due to poor network connection.

### What is a playback password?

Playback password is a security mechanism ensuring that the video content can only be viewed by authorized users.
Specifically, when you try to play back a video, you need to enter an 8-character case-sensitive password which can contain only letters and digits but not spaces and other characters. The video can be played back normally only if you enter the correct password. Each video file is configured with an individual password when it is published.


### What are blacklist/whitelist?

The blacklist/whitelist can be used to allow or deny the requests for accessing videos published through player code from particular webpages.
These lists are effective to videos published through player code. You can enable this feature globally and specify a blacklist or a whitelist. Each list can contain up to 10 URLs and works by checking the referer of access source. For more information on how to protect video file URLs, please see [Hotlink Protection Overview](https://cloud.tencent.com/document/product/266/11243).

### Does VOD support publishing links on WeChat Official Account?
Yes. For more information, please see [Guide for Publishing Video Link on WeChat Official Account](https://cloud.tencent.com/document/product/266/2876).

### Can I add ads to videos published through an application player?
Adding ads is currently not supported. We will make this feature available as soon as possible.



