Non-compliant content may expose your business to legal risks and hurt your brand. VOD offers [video moderation](https://intl.cloud.tencent.com/document/product/266/33944) and [image moderation](https://intl.cloud.tencent.com/document/product/266/33944) capabilities to help you ensure the compliance of your content.

## Video Moderation
The [video moderation feature](https://intl.cloud.tencent.com/document/product/266/33944) of VOD analyzes your video content and gives suggestions on whether to pass or block the content.

You can initiate a video moderation task either from the [VOD console](https://intl.cloud.tencent.com/document/product/266/33897) or by calling a [server-side API](https://intl.cloud.tencent.com/document/product/266/33944).

The process of calling a server-side API to initiate video moderation is as follows:
![](https://main.qcloudimg.com/raw/99544692ba8d62874a0f718e805f2d57.png)

1. The app backend authenticates the content provider and distributes a [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922).
2. The content provider uploads the content to VOD.
3. VOD sends [information](https://intl.cloud.tencent.com/document/product/266/33950) including the file ID and playback URL of the uploaded video to the app backend.
4. VOD executes a moderation task according to the `procedure` parameter specified during upload.
5. VOD sends the result to the app backend via the [task flow status change](https://intl.cloud.tencent.com/document/product/266/33953) notification.
 - If the moderation result is “block”, there’s a high chance that the content is non-compliant. We recommend you block the content.
 - If the moderation result is “pass”, the probability of the content being non-compliant is low. We recommend you allow the content to pass.
 - If the moderation result is “review”, human moderation is recommended.
6. The app backend publishes videos whose suggestion is "pass" as well as those that are given a “review” suggestion and have passed human moderation.
7. Viewers request a playback URL for a published video from the app backend.
8. Viewers play the video via the URL (VOD offers acceleration services).

Steps 4-6 ensure that the video obtained in step 7 is compliant.

>! In the above process, videos are moderated before being published (only videos that pass the moderation or review are published). You can also use the post-moderation mode, in which videos are published first before moderation is performed (non-compliant content detected will be removed).

