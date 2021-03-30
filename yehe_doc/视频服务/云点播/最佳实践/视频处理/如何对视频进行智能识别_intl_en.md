User-generated content (UGC) and professionally generated content (PGC) platforms are two common scenarios in the video industry where video content can be freely uploaded and shared. However, there may be a high number of uploaded videos that contain inappropriate information. Therefore, it is necessary to assist users in building a green and healthy social network environment.

## Causes of Inappropriate Videos

Generally, a UGC or PGC video platform interacts with content providers, content consumers, and VOD in the following ways (for more information on steps 1–3, please see [Upload from Client](https://intl.cloud.tencent.com/document/product/266/33921)):
1. The video application backend authenticates the content provider and distributes to them a [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922) after authentication is passed.
2. The content provider uploads the content to be shared to VOD.
3. VOD notifies the application backend of [relevant information](https://intl.cloud.tencent.com/document/product/266/33950) such as the `FileId` and playback URL of the uploaded video.
4. The content consumer requests the playback URL from the video application backend.
5. The content consumer accelerates video playback via VOD through the URL.

After getting upload information of the video in step 3, the application platform will publish the video. Then, the user in step 4 can get the video playback URL and play back the video. In this way, inappropriate videos can be directly exposed to content consumers.

## Introduction of Intelligent Video Recognition
VOD provides a [video content recognition](https://intl.cloud.tencent.com/zh/document/product/266/33946) feature to initiate intelligent content recognition on a video and offer a suggestion (human review or approval) in the recognition result. After the application backend gets the result, it can determine whether to publish the video based on the suggestion:
* If the recognition result is "block" (blocking suggested), the application backend will intelligently recognize the video.
* If the recognition result is "pass" (approval suggested), the application backend will directly publish the video.
* If the recognition result is "review" (human review suggested), the application backend will leave the video for human review to determine whether to publish the video.

After video content recognition is enabled in VOD, the application backend can efficiently recognize and filter out inappropriate videos. The recommended use process is as follows:

1. The video application backend authenticates the content provider and distributes to them a [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922) after authentication is passed.
2. The content provider uploads the content to be shared to VOD.
3. VOD notifies the application backend of [relevant information](https://intl.cloud.tencent.com/document/product/266/33950) such as the `FileId` and playback URL of the uploaded video.
4. VOD executes the intelligent video recognition task configured with the `procedure` parameter during generation of the upload signature.
5. VOD notifies the application backend of the recognition result through [ProcedureStateChanged](https://intl.cloud.tencent.com/document/product/266/33953).
6. The application backend publishes videos tagged as "pass" and those that are tagged as "review" and pass human review.
7. The content consumer requests the playback URL for the published video from the application backend.
8. The content consumer accelerates video playback via VOD through the URL.

After steps 4–6 are added, the process above can ensure that the video obtained by the content consumer in step 7 is verified as compliant by intelligent recognition.

>! The process here takes the "review before release" approach, i.e., only videos that pass intelligent recognition can be published. You can also use the "release before review" mode based on your needs, i.e., videos are published upon successful upload and will be removed if they are identified as inappropriate after intelligent recognition.


