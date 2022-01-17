This document helps you get started with Game Multimedia Engine (GME).

## 1. Basic GME Knowledge

- [What services does GME provide?](https://intl.cloud.tencent.com/document/product/607/10835)
- [What advantages does GME have?](https://intl.cloud.tencent.com/document/product/607/10837)
- [What are some typical GME use cases?](https://intl.cloud.tencent.com/document/product/607/10838).
- [Basic Concepts](https://intl.cloud.tencent.com/document/product/607/30259)

## 2. GME Billing Modes

GME currently provides multiple services, such as voice chat, voice messaging, and speech-to-text features. For billing details, see [Daily Pay-as-You-Go Billing Mode](https://intl.cloud.tencent.com/document/product/607/36276).

## 3. Free Demo

You can scan the QR code in [Free Demo](https://intl.cloud.tencent.com/document/product/607/38535) to download the mobile application or download the executable program for the Windows platform to experience the 3D sound effect.

## 4. Getting Started

#### 4.1 Activate the service

Before using GME, you need to [sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and activate the GME service. For more information, please see [Voice Service Activation Guide](https://intl.cloud.tencent.com/document/product/607/39698).

#### 4.2 Obtaining the access parameter

After activating the GME service, you can find the AppID and permission key in the details page of the created application.
- The AppID and permission key are required in the Demo as parameters.
- During the usage of SDK, the initialization API “Init” needs to use AppID as a parameter. The authentication APIs “QAVAuthBuffer.GenAuthBuffer” (voice chat) and “ApplyPTTAuthbuffer” (speech-to-text) all require permission key as parameters.

![](https://main.qcloudimg.com/raw/a63f14a7092169c8c9b54cfd21ce4c12.png)
#### 4.3 Downloading SDK

You can download the GME SDKs for different platforms. For details, see [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521). **Currently, GME supports Windows, Mac, Android, and iOS, and GSE supports UnrealEngine4, Unity3D, and Cocos2DX**.

GME also supports the real-time audio call on H5 and listening to the voice chat in the room on the mini program.

#### 4.4 Accessing SDK
To access the SDK of each platform, you can refer to the [project configuration](https://intl.cloud.tencent.com/document/product/607/10783) document of each platform to configure the project, and then check the [API Documentation](https://intl.cloud.tencent.com/document/product/607/15228) of the corresponding platform to call the APIs to use GME services. The calling sequence of voice chat APIs is **Init API (for initialization)** > **Poll API (for callback trigger)** > **EnterRoom API (for entering a voice chat room)** > **EnableMic API (for enabling the mic)** > **EnableSpeaker API (for enabling the speaker)** > **ExitRoom API (for exiting the room)** > **Unit API (for uninitialize)**.

**The room entry process of voice chat is shown as follows:**
<img src="https://main.qcloudimg.com/raw/d23fd88b9d0ff2f044f7549168be9d79.png"  width="60%" /></img>

## 5. Console Operation Guide
For the background data of voice chat, voice message and voice analysis, see [Operation Guide](https://intl.cloud.tencent.com/document/product/607/17448).

## 6. Document Description

<table>
<thead>
<tr>
<th>Desired Operation</th>
<th>Reference Document</th>
</tr>
</thead>
<tbody><tr>
<td>Download SDK files.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/18521" target="_blank">SDK Download Guide</a></td>
</tr>
<tr>
<td>Scan the QR code to download the application and try out GME.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/38535" target="_blank">Free Demo</a></td>
</tr>
<tr>
<td>Access the SDK to the project and check the configuration required when the SDK is exported from the project. (Take Unity platform as an example)</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/10783" target="_blank">Unity Project Configuration</a></td>
</tr>
<tr>
<td>Access the SDK to the project, check all APIs, and realize voice chat and speech-to-text service. (Take Unity platform as an example)</td> 
<td><a href="https://intl.cloud.tencent.com/document/product/607/15228" target="_blank">Unity API Documentation</a></td>
</tr>
<tr>
<td>Access the SDK to the project and quickly access voice chat service. (Take Unity platform as an example)</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/18248" target="_blank">Unity Quick Start</a></td>
</tr>
<tr>
<td>Realize the range voice effect in voice chat (similar to "Team Only" and "Everyone" audio modes in PUBG)</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/17972" target="_blank">Range Voice</a></td>
</tr>
<tr>
<td>Realize the 3D real-time sound effect in the game.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/18218" target="_blank">3D Sound Effect</a></td>
</tr>
<tr>
<td>Play back the accompaniment in the voice chat room by using GME.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/31504" target="_blank">Accompaniment in Voice Chat</a></td>
</tr>
<tr>
<td>Learn about the difference between different room types in voice chat service.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/18522" target="_blank">Sound Quality selection</a></td>
</tr>
<tr>
<td>Learn more about the details of authentication and the backend deployment scheme.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/12218" target="_blank">Authentication Key</a></td>
</tr>
<tr>
<td>Analyze the error codes generated in the usage of SDK and query the solutions.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/33223" target="_blank">Error Codes</a></td>
</tr>
<tr>
<td>Learn about the product FAQs of GME.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/30254" target="_blank">General FAQ</a></td>
</tr>
<tr>
<td>Check the billing rules before purchasing the service.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/30255" target="_blank">FAQs About Billing</a></td>
</tr>
<tr>
<td>Check the FAQs about the voice chat room.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/35611" target="_blank">FAQs About Voice Chat Room</a></td>
</tr>
<tr>
<td>Check the FAQs about audio during the usage of SDK.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/30257" target="_blank">FAQs About Voice Chat Audio</a></td>
</tr>
</tbody></table>


## 7. FAQs
#### Consultation
[What is the traffic consumption when using the voice chat of GME?](https://intl.cloud.tencent.com/document/product/607/39519)
[What features does GME have?](https://intl.cloud.tencent.com/document/product/607/39520)


#### Demo
[Does GME allow using only one OpenId across multiple devices?](https://intl.cloud.tencent.com/document/product/607/30256)
[How do I use a downloaded demo?](https://intl.cloud.tencent.com/document/product/607/30256)
[How do I get logs?](https://intl.cloud.tencent.com/document/product/607/39521)
[What should I do if the screen goes black when I try to open an application after integrating the GME SDK and exporting an APK file?](https://intl.cloud.tencent.com/document/product/607/39522)
[What should I do if an error occurs during compilation when I try to export an executable file from Xcode after adding the GMESDK.framework library?](https://intl.cloud.tencent.com/document/product/607/39522)


#### Voice Chat
[When should the Poll function in the GME SDK be invoked?](https://intl.cloud.tencent.com/document/product/607/30254)
[Is there a limit on the number of voice chat rooms or members in GME?](https://intl.cloud.tencent.com/document/product/607/35611)
[Why room entry fails even if 0 is returned when the EnterRoom API is called?](https://intl.cloud.tencent.com/document/product/607/39523)
[How do I troubleshoot network problems?](https://intl.cloud.tencent.com/document/product/607/39519)
[What should I do if a client is disconnected from a voice chat room?](https://intl.cloud.tencent.com/document/product/607/35611)
[I can normally use the range voice but there is no attenuation. I set the 3D sound effect file but the return value is still 0. Why did this happen?](https://intl.cloud.tencent.com/document/product/607/39523)
[What should I do if the mobile phone volume level becomes very low after room entry but becomes very high after the mic turns on?](https://intl.cloud.tencent.com/document/product/607/39524)
[What should I do if the sound comes out of the receiver instead of the speaker after the microphone is enabled on Android?](https://intl.cloud.tencent.com/document/product/607/30257)

## 8. Feedback and Suggestion
If you have any doubts or suggestions when using Tencent Cloud GME products and services, you can submit your feedback through the following channels. Dedicated personnel will contact you to solve your problems.
- If you find product documentation problems, such as links, content, or API errors, you can click **Send Feedback** at the bottom of the document to select the content that has problems.
- If you encounter product-related problems, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

>? Please provide the information of SDK version and the used platform when you submit a ticket.
