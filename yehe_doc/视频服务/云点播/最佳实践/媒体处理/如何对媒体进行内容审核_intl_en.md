Non-compliant content may expose your business to legal risks and hurt your brand. VOD offers [audio/video content moderation](https://intl.cloud.tencent.com/document/product/266/33944) and [image content moderation](https://cloud.tencent.com/document/product/266/73655) capabilities to help you ensure the compliance of your content.

## Audio/Video Content Moderation
The [video moderation feature](https://intl.cloud.tencent.com/document/product/266/33944) of VOD analyzes your video content and gives suggestions on whether to pass or block the content.

You can initiate audio/video content moderation in the following two ways:
1. Initiate it in the [VOD console](https://intl.cloud.tencent.com/document/product/266/33897).
2. Call a server API for [audio/video content moderation](https://intl.cloud.tencent.com/document/product/266/33944).

### Calling a server API for audio/video content moderation
The process of calling a server-side API to initiate video moderation is as follows:
![](https://main.qcloudimg.com/raw/99544692ba8d62874a0f718e805f2d57.png)

1. The app backend authenticates the content provider and distributes a [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922).
2. The content provider uploads the content to VOD.
3. VOD sends [information](https://intl.cloud.tencent.com/document/product/266/33950) including the file ID and playback URL of the uploaded video to the app backend.
4. VOD executes a moderation task according to the `procedure` parameter specified during upload.
5. VOD sends the result to the app backend via the [task flow status change](https://intl.cloud.tencent.com/document/product/266/33953) notification.
 - If the moderation result is “block”, there’s a high chance that the content is non-compliant. We recommend you block the content.
 - If the moderation result is "pass", the probability of the content being non-compliant is low; in this case, we recommend you allow the content to pass.
 - If the moderation result is "review", the probability of the content being non-compliant is high; in this case, manual verification is recommended.
6. The app backend publishes videos whose suggestion is "pass" as well as those that are given a “review” suggestion and have passed manual verification.
7. Viewers request a playback URL for a published video from the app backend.
8. Viewers play the video via the URL (VOD offers acceleration services).

Steps 4-6 ensure that the video obtained in step 7 is compliant.

>! In the above process, videos are moderated before being published (only videos that pass the moderation or review are published). You can also use the post-moderation mode, in which videos are published first before moderation is performed (non-compliant content detected will be removed).



