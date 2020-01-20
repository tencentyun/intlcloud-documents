## Operation Scenarios
Video upload from server refers to uploading videos to the VOD platform by the application backend. This document describes how to upload videos using server APIs.

## Prerequisites

#### 1. Activate the service

Activate VOD. <!--doc For more information, please see [Purchase Guide](https://intl.cloud.tencent.com/document/product/266/2839).-->

#### 2. Get TencentCloud API key
 
Get the security credentials (i.e., `SecretId` and `SecretKey`) required to call the server API in the following steps:
1. Log in to the console and select **Cloud Products** > **Cloud Access Management** > **[API Key Management](https://console.cloud.tencent.com/cam/capi)** to enter the "API Key Management" page.
2. Get the TencentCloud API key. If you have not created a key, click **Create Key** to create a pair of `SecretId` and `SecretKey`.

## Directions
### 1. Initiate upload

An upload can be initiated through the SDK or API.

#### Initiating upload through SDK

To facilitate the upload feature in your development environment, VOD provides SDKs for different programming languages. The SDK for each language comes with a corresponding Demo. For more information, please see:
- [SDK for PHP](https://intl.cloud.tencent.com/document/product/266/33916)
- [SDK for Java](https://intl.cloud.tencent.com/document/product/266/33914)
- [SDK for Python](https://intl.cloud.tencent.com/document/product/266/33917)
- [SDK for Node.js](https://intl.cloud.tencent.com/document/product/266/33918)
- [SDK for Go](https://intl.cloud.tencent.com/document/product/266/33919)
- [SDK for C#](https://intl.cloud.tencent.com/document/product/266/33915)

#### Initiating upload through API

If the upload SDK provided by VOD does not apply to the programming language used by your application backend, the application backend needs to call VOD server APIs for video upload (this method is more complicated and not recommended). The business flow of API-based upload is as follows:
![](https://main.qcloudimg.com/raw/f0c04e9da4d3aafcaf2ba68302814c72.jpg)
API-based upload requires you to implement steps such as applying for upload and uploading file on your own, which is not so convenient as SDK-based upload. Plus, you need to develop multipart upload logic for uploading large files. <!--api For more information, please see:
- [Server API - ApplyUpload](/document/product/266/31767)
- [Server APIs - Uploading File](/document/product/266/31784)
- [Server API - CommitUpload](/document/product/266/31766)
-->
#### Advanced features

- **Specify a task flow during upload**
If you want to automatically initiate a [video processing task flow](https://intl.cloud.tencent.com/document/product/266/33931#.E4.BB.BB.E5.8A.A1.E6.B5.81) such as transcoding and screencapturing upon video upload completion, you can specify the `Procedure` parameter when calling the server API [ApplyUpload](/document/product/266/31767), and the parameter value should the name of the desired task flow template. VOD supports [creating task flow templates](https://intl.cloud.tencent.com/document/product/266/14058) and naming them. When initiating a task flow, you can use the task flow template name to indicate the desired task. All the SDKs provided by VOD for different programming languages support specifying the task flow parameter. For more information, please see:
	- [SDK for PHP](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
	- [SDK for Java](https://intl.cloud.tencent.com/document/product/266/33914#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
	- [SDK for Python](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
	- [SDK for Node.js](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
	- [SDK for Go](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
	- [SDK for C#](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8C.87.E5.AE.9A.E4.BB.BB.E5.8A.A1.E6.B5.81)
- **Specify a storage region during upload**
The storage region provided by VOD is "Chongqing" by default. If you want to store files in another region, you need to activate it in the console. For more information, please see [Upload Storage Settings](https://intl.cloud.tencent.com/document/product/266/18874). After the settings are made, the storage region can be specified by the `StorageRegion` parameter when the server API [ApplyUpload](/document/product/266/31767) is called, and the parameter value should be a [region abbreviation](https://intl.cloud.tencent.com/document/product/266/33910). All the SDKs provided by VOD for different programming languages support specifying the storage region during upload. For more information, please see:
	- [SDK for PHP](https://intl.cloud.tencent.com/document/product/266/33916#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	- [SDK for Java](https://intl.cloud.tencent.com/document/product/266/33914#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	- [SDK for Python](https://intl.cloud.tencent.com/document/product/266/33917#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	- [SDK for Node.js](https://intl.cloud.tencent.com/document/product/266/33918#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	- [SDK for Go](https://intl.cloud.tencent.com/document/product/266/33919#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	- [SDK for C#](https://intl.cloud.tencent.com/document/product/266/33915#.E6.8C.87.E5.AE.9A.E5.AD.98.E5.82.A8.E5.9C.B0.E5.9F.9F)
	
### 2. Event notification

After a video upload is completed, VOD will initiate an [event notification - video upload completion](https://intl.cloud.tencent.com/document/product/266/33950) to the application backend, through which the application backend can become aware of the video upload event. To receive event notifications, you need to go to [Console - Callbacks](https://console.cloud.tencent.com/vod/callback) to enable event notification. [Event notification - video upload completion](https://intl.cloud.tencent.com/document/product/266/33950) mainly contains the following information:
- `FileId` and URL of the uploaded video;
- VOD supports specifying passthrough fields during video upload, which will be sent to the application backend upon event completion. The following fields are in the event notification:
	- `SourceType`: this field is always `ServerUpload`, indicating that the upload originates from a server.
	- `SourceCopntext`: this is a custom passthrough field specified by the application backend during signature distribution, which corresponds to the `sourceContext` parameter in the signature.
- VOD supports automatic video processing upon video upload completion. If a [video processing task flow](https://intl.cloud.tencent.com/document/product/266/33931#.E4.BB.BB.E5.8A.A1.E6.B5.81) is specified during upload, the task ID will also be included in the event notification content, i.e., the `data.procedureTaskId` field.

- For more information, please see:
- [Task Management and Event Notification](https://intl.cloud.tencent.com/document/product/266/33931#.E7.BB.93.E6.9E.9C.E9.80.9A.E7.9F.A5)
- [Event Notification - Video Upload Completion](https://intl.cloud.tencent.com/document/product/266/33950)


