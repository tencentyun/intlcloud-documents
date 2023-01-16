This document helps you get started with Game Multimedia Engine (GME).
## 1. Basic GME Knowledge
- [What services does GME provide? What are its main features?](https://intl.cloud.tencent.com/document/product/607/10835)
- [What advantages does GME have?](https://intl.cloud.tencent.com/document/product/607/10837)
- [What use cases can GME be applied to?](https://www.tencentcloud.com/zh/document/product/607/51558)

## 2. GME Billing Modes
GME currently provides multiple services, such as voice chat and voice messaging. For billing details, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/607/50009).

## 3. Free Demo
Before using GME, you can try it out first:

<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_KuI8ov.gif"    width="37.5%"/></img>


- [Basic feature demo](https://intl.cloud.tencent.com/document/product/607/50219): Try out voice chat, voice messaging, speech-to-text, real-time 3D sound effect, and real-time basic voice changing features.
- [Real-time 3D sound effect demo](https://intl.cloud.tencent.com/document/product/607/50220): Try out the real-time 3D sound effect feature.
- [Advanced voice changing demo](https://intl.cloud.tencent.com/document/product/607/50221): Try out the real-time advanced voice changing feature.


## 4. Service Activation
- Before using GME, you need to sign up for a [Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) first.
- Activate the service in the [GME console](https://console.cloud.tencent.com/gamegme) and enable features as needed. For more information, see [Activating Services](https://intl.cloud.tencent.com/document/product/607/10782).

## 5. Integration Parameter Acquisition

### Client integration parameters


1. In the [GME console](https://console.cloud.tencent.com/gamegme), find the application you just created and click **Settings** in the **Operation** column to enter the application settings page.

2. You can get the corresponding `AppID` and permission key on the page as shown below:

	- When you use the sample project, the `AppID` and permission key are required as parameters.
	- When you use the SDK, the initialization API `Init` requires the `AppID` as a parameter, and the local authentication generation API `QAVAuthBuffer.GenAuthBuffer` requires the permission key as a parameter.

### TencentCloud API integration parameters
If you use TencentCloud API, you need `SecretId` and `SecretKey`, which can be obtained on the [Manage API Key](https://console.cloud.tencent.com/cam/capi) page. We recommend you manage the account access as instructed in [Security Best Practice](https://www.tencentcloud.com/document/product/598/10592).



## 6. Sample Project Run
GME provides SDKs and sample projects for different platforms. You can better understand how to integrate the GME SDK by running the sample project.
### 6.1 Download the sample project
You can download the sample project for the target platform as instructed in [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).


### 6.2 Run the sample project
View corresponding documents for the platform you use:
[Quick Unreal Engine Demo Run](https://intl.cloud.tencent.com/document/product/607/46014)

## 7. Basic Feature Integration
### 7.1 Download the SDK
You can download the required SDK files for the target platform as instructed in [SDK Download Guide](https://intl.cloud.tencent.com/document/product/607/18521).
<img src="https://qcloudimg.tencent-cloud.cn/raw/b04f51788ab7bd527ef1662c5c5f7675.png"  width="50%"/></img>

### 7.2 Configure the project
Refer to the documentation for each platform to configure the project. Only after the configuration is completed can the APIs be called to use the GME service.

| Platform | Configuration Documentation |
|---------|---------|
| Unity | [Integrating SDK](https://intl.cloud.tencent.com/document/product/607/10783) |
| Unreal Engine | [Integrating SDK](https://intl.cloud.tencent.com/document/product/607/44549) |
| Cocos2d | [Project Configuration](https://intl.cloud.tencent.com/document/product/607/15216) |
| Windows | [Project Configuration](https://intl.cloud.tencent.com/document/product/607/19068) |
| Android | [Integrating SDK](https://intl.cloud.tencent.com/document/product/607/40859) |
| iOS | [Integrating SDK](https://intl.cloud.tencent.com/document/product/607/15219) |
| macOS | [Project Configuration](https://intl.cloud.tencent.com/document/product/607/18617) |
| HTML5 | [Project Configuration](https://intl.cloud.tencent.com/document/product/607/30261) |

### 7.3 Quickly integrate the SDK
The quick integration documents simplify the integration process for you to quickly try out features. The features described in such documents include voice chat and streaming speech-to-text.

| Platform | Quick Integration Documentation |
|---------|---------|
| Unity | [Quick Integration of SDK for Unity](https://intl.cloud.tencent.com/document/product/607/44544) |
| Unreal Engine | [Quick Integration of SDK for Unreal Engine](https://intl.cloud.tencent.com/document/product/607/44545) |
| Windows, iOS, macOS, Android | [Quick Integration of Native SDK](https://intl.cloud.tencent.com/document/product/607/40858) |



### 7.4 Integrate basic features
Click [here](https://www.tencentcloud.com/document/product/607/10780) to find the corresponding document for the platform you use.


### 7.5 Integration help documentation
Documents that may be used:

| Document | When to Use |
|---------|---------|
| [Sound Quality](https://intl.cloud.tencent.com/document/product/607/18522) | If it is difficult for you to choose a voice chat room type, refer to this document. |
| [Authentication Key](https://intl.cloud.tencent.com/document/product/607/12218) | If you want the authentication deployment related to the GME service of your application to be more secure, refer to this document |
| [SDK Version Upgrade Guide](https://intl.cloud.tencent.com/document/product/607/32363) | If you upgrade from a previous GME version to a new version, you need to check this document to understand the API changes. |
| [Error Codes](https://intl.cloud.tencent.com/document/product/607/33223) | During the SDK integration debugging process, if you find that APIs or callbacks return an error code, refer to this document for solutions. |

## 8. Advanced Feature Integration


<table>
<thead>
<tr>
<th>Desired Operation</th>
<th>Reference Document</th>
</tr>
</thead>
<tbody>
<tr>
<td>Realize the range voice effect in voice chat (similar to "Team Only" and "Everyone" audio modes in PUBG)</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/17972" target="_blank">Range Voice</a></td>
</tr>
<tr>
<td>Hear a stereo voice with a sense of direction from characters when characters move. The voice also gets weaker as the distance from the source increases, making the game voice more immersive.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/18218" target="_blank">3D Sound Effect</a></td>
</tr>
<tr>
<td>Implement room member management, mic-on/off, and muting. For example, the team leader wants to mute other players in the room, or the game host wants audience members to mic on.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/51115" target="_blank">Integrating GME Chat Room Management</a></td>
</tr>
<tr>
<td>Use GME to play the accompaniment in the voice chat room, adjust the EQ of the accompaniment, and play back local sound effects.</td>
<td ><a href="https://intl.cloud.tencent.com/document/product/607/31504" target="_blank">Accompaniment in Voice Chat</a>, <a href="https://intl.cloud.tencent.com/document/product/607/31503" target="_blank">Real-Time Sound Effect</a>, <a href="https://www.tencentcloud.com/document/product/607/46716" target="_blank">Real-Time Sound Equalizer</a></td>
</tr>
<tr>
<td>Perform voice changing during voice chat. Players can change their tone to that of a middle-aged man, little girl, etc.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/44995" target="_blank">Voice Changing Effects</a></td>
</tr>
<tr>
<td>Make yourself heard only by members in your current team and hear the voices of other stranger players in the matched team in the voice chat room.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/39525" target="_blank">Custom Audio Forwarding Routing</a></td>
</tr>
<tr>
<td>Use voice recognition to detect minor players in team battling, so as to find minors bypassing identity verification and the anti-addiction system.</td>
<td>Minor Speech Recognition</td>
</tr>
<tr>
<td>Recognize pornographic, violent, abusive, advertising, and other sensitive or harmful information in voice chats, audio files, and voice messages.</td>
<td>Voice Chat Moderation, Voice Message Moderation, Third-Party Audio Stream or Audio File Moderation</td>
</tr>
<tr>
<td>Convert players' real-time audio streams into text to present real-time subtitles.</td>
<td>Real-Time Speech-to-Text</td>
</tr>
</tbody></table>


## 9. Console Operation Guide
For the usage data of voice chat, voice messaging, and other services, see [Usage Querying](https://intl.cloud.tencent.com/document/product/607/44548).

## 10. FAQs
#### Features
- [What is the traffic consumption when using the voice chat of GME?](https://intl.cloud.tencent.com/document/product/607/39519)
[What features does GME have?](https://intl.cloud.tencent.com/document/product/607/39520)
[Is there a limit on the number of voice chat rooms or members in GME?](https://intl.cloud.tencent.com/document/product/607/39523)

#### Development
[Does GME allow using only one OpenId across multiple devices?](https://intl.cloud.tencent.com/document/product/607/39521)
[How do I use a downloaded demo?](https://intl.cloud.tencent.com/document/product/607/39521)
[What should I do if the screen goes black when I try to open an application after integrating the GME SDK and exporting an APK file?](https://intl.cloud.tencent.com/document/product/607/39522)
[What should I do if an error occurs during compilation when I try to export an executable file from Xcode after adding the GMESDK.framework library?](https://intl.cloud.tencent.com/document/product/607/39522)
[When should the Poll function in the GME SDK be invoked?](https://intl.cloud.tencent.com/document/product/607/30254)



## 11. Integration

If you encounter problems during integration, troubleshot as follows:

### Determining the issue
You need to determine the type of the issue first and then check the corresponding documents: [Authentication](https://intl.cloud.tencent.com/document/product/607/39824), [Demo](https://intl.cloud.tencent.com/document/product/607/39521), [Network](https://intl.cloud.tencent.com/document/product/607/39519), or [Program Export](https://intl.cloud.tencent.com/document/product/607/39522).

You can also determine the issue document that should be viewed according to the service used:

| Services Used | Document |
|---------|---------|
| Voice chat | [Room Entering Failed](https://intl.cloud.tencent.com/document/product/607/39523), [Sound and Audio](https://intl.cloud.tencent.com/document/product/607/39524) |
| Voice messaging | [Speech-to-text Conversion](https://intl.cloud.tencent.com/document/product/607/39716)|
| Speech-to-text | [Speech-to-text Conversion](https://intl.cloud.tencent.com/document/product/607/39716)|

### Error codes
If a call error occurs, you can check the cause and solution based on the [error code](https://intl.cloud.tencent.com/document/product/607/33223).

For example, when you use the SDK, if the 3D sound effect API returns error 7003, you can check the error code document to know that the cause is that `InitSpatializer` has not been called. Then, check whether `InitSpatializer` is called in your code in the correct sequence.

![](https://qcloudimg.tencent-cloud.cn/raw/1394eb8f4947c28728a00c873b3ecb0c.png)

### Asking for help
If the problem cannot be solved through the documentation and error code, contact us for assistance as instructed in [Troubleshooting Guide](https://www.tencentcloud.com/document/product/607/51562).


## 12. Feedback and Suggestions
If you have any doubts or suggestions when using Tencent Cloud GME products and services, you can submit your feedback through the following channels. Dedicated personnel will contact you to solve your problems.
- For questions about the product documentation, such as links, content, or APIs, click **Send Feedback** on the right of the document page.
- If you encounter problems when using the product, contact [online customer service](https://intl.cloud.tencent.com/contact-sales) for assistance.
