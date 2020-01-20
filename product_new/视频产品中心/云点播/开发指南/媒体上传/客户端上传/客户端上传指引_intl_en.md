## Operation Scenarios
Video upload from client refers to uploading local videos to the VOD platform by an end user of application. This document describes how to upload videos using a client.
![](https://main.qcloudimg.com/raw/cb72789083e25a1759c446ec4f2356f9.jpg)

## Prerequisites

#### 1. Activate the service

Activate VOD. <!--doc For more information, please see [Purchase Guide](https://intl.cloud.tencent.com/document/product/266/2839).-->

#### <span id = "p3"></span>2. Get TencentCloud API key
 
Get the security credentials (i.e., `SecretId` and `SecretKey`) required to call the server API in the following steps:
1. Log in to the console and select **Cloud Products** > **Cloud Access Management** > **[API Key Management](https://console.cloud.tencent.com/cam/capi)** to enter the "API Key Management" page.
2. Get the TencentCloud API key. If you have not created a key, click **Create Key** to create a pair of `SecretId` and `SecretKey`.


## Directions
### 1. Apply for upload signature
The client needs to apply to the signature distribution server of the application for an upload signature. For detailed directions, please see [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922). Below are samples of generating signatures in different programming languages:
- [Sample of Signature in PHP](https://intl.cloud.tencent.com/document/product/266/33923#php-.E7.AD.BE.E5.90.8D.E7.A4.BA.E4.BE.8B)
- [Sample of Signature in Java](https://intl.cloud.tencent.com/document/product/266/33923#java-.E7.AD.BE.E5.90.8D.E7.A4.BA.E4.BE.8B)
- [Sample of Signature in Node.js](https://intl.cloud.tencent.com/document/product/266/33923#node.js-.E7.AD.BE.E5.90.8D.E7.A4.BA.E4.BE.8B)
- [Sample of Signature in C#](https://intl.cloud.tencent.com/document/product/266/33923#c.23-.E7.AD.BE.E5.90.8D.E7.A4.BA.E4.BE.8B)
- [Sample of Signature in Python](https://intl.cloud.tencent.com/document/product/266/33923#python-.E7.AD.BE.E5.90.8D.E7.A4.BA.E4.BE.8B)

>
>- Upload from client is to directly upload video files from a client to the VOD platform, without the need to relay files through the application server. Therefore, VOD has to authenticate the client that initiates the request.
>- The application shall not disclose `SecretKey`, which has ultimate permissions, to the client in order to avoid serious security breaches. Therefore, before initiating a request, the client needs to apply for an upload signature.


### 2. Use the SDK to upload video

VOD provides SDKs for multiple platforms to help upload videos from client with ease. For more information, please see:
- [Upload SDK for Android](https://intl.cloud.tencent.com/document/product/266/33925)
- [Upload SDK for iOS](https://intl.cloud.tencent.com/document/product/266/33926)
- [Upload SDK for Web](https://intl.cloud.tencent.com/document/product/266/33924)

#### Advanced features

- <span id = "p1"></span>**Specify a task flow during upload**
If you want to automatically initiate a [video processing task flow](https://intl.cloud.tencent.com/document/product/266/33931#.E4.BB.BB.E5.8A.A1.E6.B5.81) such as transcoding and screencapturing upon video upload completion, you can set the `procedure` parameter when generating the [upload signature](https://intl.cloud.tencent.com/document/product/266/33922#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0), and the parameter value should the name of the desired task flow template. VOD supports [creating task flow templates](https://intl.cloud.tencent.com/document/product/266/14058) and naming them. When initiating a task flow, you can use the task flow template name to indicate the desired task.
- **Specify a storage region during upload**
The storage region provided by VOD is "Chongqing" by default. If you want to store files in another region, you need to activate it in the console. For more information, please see [Upload Storage Settings](https://intl.cloud.tencent.com/document/product/266/18874). After the settings are made, the storage region can be specified by the `storageRegion` parameter when the [upload signature](https://intl.cloud.tencent.com/document/product/266/33922#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0) is generated, and the parameter value should be a [region abbreviation](https://intl.cloud.tencent.com/document/product/266/33910).
- **Upload a video with cover**
VOD allows you to upload a video with its cover by entering the path to the cover in the upload SDK API. For more information, please see:
	- [Upload SDK for Android](https://intl.cloud.tencent.com/document/product/266/33925)
	- [Upload SDK for iOS](https://intl.cloud.tencent.com/document/product/266/33926)
	- [Upload SDK for Web](https://intl.cloud.tencent.com/document/product/266/33924)
- <span id = "p4"></span>**One-time signature**
During video upload, the signature distributed by the application backend can be used multiple times within its validity period. If the application has high requirements for video upload security, you can use the one-time signature feature.
How to use one-time signature: you just need to set `oneTimeValid` to 1 when the application backend distributes the signature. For more information, please see [Signature for Upload from Client](https://intl.cloud.tencent.com/document/product/266/33922).
>The one-time signature can be used only once. Though this approach is more secure, the application has to perform extra processing. For example, when upload fails, you cannot simply use the SDK to upload the video again; instead, you need to apply for a new upload signature.
- **Resumable upload**
During the video upload process, when the upload is terminated unexpectedly, you can upload the file again from where it left off.
>The effective time for resumption is 1 day, i.e., if the upload of a video is interrupted and then resumed within 1 day, it can be directly resumed; otherwise, the full video will be uploaded again by default.
>
You can enable the resumable upload feature for the application as shown below:
	- For the [upload SDK for Android](https://intl.cloud.tencent.com/document/product/266/33925), set `enableResume` to `True` during upload.
	- For the [upload SDK for iOS](https://intl.cloud.tencent.com/document/product/266/33926), set `enableResume` to `True` during upload.
	- For the [upload SDK for Web](https://intl.cloud.tencent.com/document/product/266/33924), resumable upload is a built-in feature with no additional operation needed.
- **Pause/resume/cancel upload**
During video upload, the VOD SDK allows you to pause, resume, or cancel upload. For more information, please see:
	- [Upload SDK for Android](https://intl.cloud.tencent.com/document/product/266/33925)
	- [Upload SDK for iOS](https://intl.cloud.tencent.com/document/product/266/33926)
	- [Upload SDK for Web](https://intl.cloud.tencent.com/document/product/266/33924)

#### FAQs 
- **How do I enable automatic transcoding after video upload is completed?**
You can use the `procedure` parameter in the signature for upload from client to specify the video processing method after video upload is completed. For more information, please see [Specifying a Task Flow During Upload](#p1).
- **How does the application backend identify which client uploaded the video when it receives the video upload completion notification?**
You can add the `sourceContext` parameter to the signature for upload from client to carry the user identity information. The video upload completion notification will pass this parameter to the application backend. For more information, please see [Event Notification](#p2).

### <span id = "p2"></span>3. Event notification

After a video upload is completed, VOD will initiate an [event notification - video upload completion](https://intl.cloud.tencent.com/document/product/266/33950) to the application backend, through which the application backend can become aware of the video upload event. To receive event notifications, you need to go to [Console - Callbacks](https://console.cloud.tencent.com/vod/callback) to enable event notification. [Event notification - video upload completion](https://intl.cloud.tencent.com/document/product/266/33950) mainly contains the following information:
- `FileId` and URL of the uploaded video.
- VOD supports specifying passthrough fields during video upload, which will be sent to the application backend upon event completion. The following fields are in the event notification:
	- `SourceType`: this field is always `ServerUpload`, indicating that the upload originates from a server.
	- `SourceCopntext`: this is a custom passthrough field specified by the application backend during signature distribution, which corresponds to the `sourceContext` parameter in the signature.
- VOD supports automatic video processing upon video upload completion. If a [video processing task flow](https://intl.cloud.tencent.com/document/product/266/33931#.E4.BB.BB.E5.8A.A1.E6.B5.81) is specified during upload, the task ID will also be included in the event notification content, i.e., the `data.procedureTaskId` field.

For more information, please see:
- [Task Management and Event Notification](https://intl.cloud.tencent.com/document/product/266/33931#.E7.BB.93.E6.9E.9C.E9.80.9A.E7.9F.A5)
- [Event Notification - Video Upload Completion](https://intl.cloud.tencent.com/document/product/266/33950)





