User-generated content (UGC) and professionally generated content (PGC) platforms are two common scenarios in the video industry where video content can be freely uploaded and shared. However, there may be a large number of uploaded videos that contain porn, terrorism, and politically sensitive information. If the video platform does not restrict the illegal content, it will face serious legal risks and damage to its brand image.

## Causes of Violations

Generally, a UGC or PGC video platform interacts with content providers, content consumers, and VOD in the following ways (for more information on steps 1–3, please see [Upload from Client](https://intl.cloud.tencent.com/document/product/266/33921)):
<img src="https://main.qcloudimg.com/raw/1583662375b390c774d1298e41cda9fd.png" width="400">
1. The video application backend authenticates the content provider and distributes to them a [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922) after authentication is passed.
2. The content provider uploads the content to be shared to VOD.
3. VOD notifies the application backend of [relevant information](https://intl.cloud.tencent.com/document/product/266/33950) such as the `FileId` and playback URL of the uploaded video.
4. The content consumer requests the playback URL from the video application backend.
5. The content consumer accelerates video playback via VOD through the URL.

After getting upload information of the video in step 3, the application platform will publish the video. Then, the user in step 4 can get the video playback URL and play back the video. In this way, illegal videos can be directly exposed to content consumers.

## Introduction of Video Content Audit
VOD provides a [video content audit](https://intl.cloud.tencent.com/document/product/266/33944) feature to initiate content audit on a video and offer a suggestion (blocking, human audit, or approval) in the audit result. After the application backend gets the audit result, it can decide whether to publish the video based on the suggestion:
* If the audit result is "block" (blocking suggested), the application backend will block the video.
* If the audit result is "pass" (approval suggested), the application backend will directly publish the video.
* If the audit result is "review" (human audit suggested), the application backend will leave the video for human audit to determine whether to publish the video.

After video content audit is enabled in VOD, the application backend can efficiently recognize and filter out illegal videos. The recommended use process is as follows:
<img src="https://main.qcloudimg.com/raw/3696b553b4d21a221e83cd537d7df8f2.png" width="550">

1. The video application backend authenticates the content provider and distributes to them a [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922) after authentication is passed.
2. The content provider uploads the content to be shared to VOD.
3. VOD notifies the application backend of [relevant information](https://intl.cloud.tencent.com/document/product/266/33950) such as the `FileId` and playback URL of the uploaded video.
4. VOD executes the video content audit task configured with the `procedure` parameter during generation of the upload signature.
5. VOD notifies the application backend of the audit result through [ProcedureStateChanged](https://intl.cloud.tencent.com/document/product/266/33953).
6. The application backend publishes videos labeled as "pass" and those that are labeled as "review" and pass human audit.
7. The content consumer requests the playback URL for the published video from the application backend.
8. The content consumer accelerates video playback via VOD through the URL.

After steps 4–6 are added, the process above can ensure that the video obtained by the content consumer in step 7 is audited and legal.

> The process here takes the "audit before release" approach, i.e., only videos that pass audit can be published. You can also use the "release before audit" mode based on your needs, i.e., videos are published upon successful upload and will be taken down if they are identified as illegal after audit.
