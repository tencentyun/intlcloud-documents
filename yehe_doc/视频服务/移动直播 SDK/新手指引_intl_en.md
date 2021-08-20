This document offers a tutorial for customers new to MLVB. The video below gives you a quick overview of the MLVB SDK.



## Quick Look

- [Solutions and architecture](https://intl.cloud.tencent.com/document/product/1071/38146)
- [Interactive live streaming solution](https://cloud.tencent.com/document/product/454/35275)
- [Concepts](https://cloud.tencent.com/document/product/454/48439)
- [Application scenarios](https://cloud.tencent.com/document/product/454/48221)



## Billing

You may be charged the following costs for using the MLVB SDK. 

<table>
<tr><th>Cost Item</th><th>Documentation</th></tr>
<tr>
<td>License to use the MLVB SDK</td>
<td><a href="https://cloud.tencent.com/document/product/454/8008#sdklicense">MLVB license</a></td>
</tr><tr>
<td rowspan=3>Cost of other Tencent Cloud services used</td>
<td><a href="https://cloud.tencent.com/document/product/454/8008#LVB">CSS</a></td>
</tr><tr>
<td><a href="https://cloud.tencent.com/document/product/454/8008#IM">IM</a></td>
</tr><tr>
<td><a href="https://cloud.tencent.com/document/product/454/8008#vod">VOD</a></td>
</tr>
<tr>
<td>Cost of additional materials for beauty filters and animated effects (for Enterprise Edition only)</td>
<td><a href="https://cloud.tencent.com/document/product/454/8008#effect">Materials for beauty filters and animated effects</a></td>
</tr>
</tbody></table>

> ? 
> - Before using the MLVB SDK, you must activate [CSS](https://cloud.tencent.com/document/product/267) first.
> - If you have unused packages and want a refund, please see [Refund](https://cloud.tencent.com/document/product/454/43191).



## Development Support

### Trying the demo
MLVB offers a demo app, [Video Cloud Toolkit](https://intl.cloud.tencent.com/document/product/1071/38147), for you to try out its features.



### Obtaining a license
A license allows you to unlock certain features of the MLVB SDK on iOS and Android. For instructions on how to obtain one, please see:
-  [Applying for a Trial License](https://intl.cloud.tencent.com/zh/document/product/1071/39476) 
-  [Purchasing an Official License](https://intl.cloud.tencent.com/zh/document/product/1071/39476) 
-  [Purchasing an Enterprise Edition License](https://intl.cloud.tencent.com/zh/document/product/1071/39476) 

> ? To learn about the licenses required to use different editions of the SDK, please see [SDK and license](https://intl.cloud.tencent.com/document/product/1071/38149).



### Downloading the SDK

We provide three editions of the MLVB SDK, namely **LiteAV_Smart**, **Professional**, and **Enterprise**. You need different licenses to use them. 

| Edition                                                     | Description                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [LiteAV_Smart](https://intl.cloud.tencent.com/document/product/1071/38150) | With a basic edition license, you can use features including publishing, playback, and basic beauty filters (skin brightening and smoothing). |
| [Professional](https://intl.cloud.tencent.com/document/product/1071/38150) | The professional edition integrates multiple audio/video services of Tencent Cloud. Other than the support for LEB, it offers the same MLVB features as LiteAV_Smart, but it is free of the duplicate symbol issue that may arise if you integrate multiple audio/video SDKs. You can use the MLVB features of the professional edition with a basic edition license, but to use the features of other Tencent Cloud services, you need to activate the services first. |
| [Enterprise](https://intl.cloud.tencent.com/document/product/1071/38150) | In addition to the features of the professional edition, the enterprise edition offers advanced beauty filters and special effects. To use them, you need to purchase an enterprise edition license. |

> ? For details on the features supported by different SDK editions, please see [Features](https://intl.cloud.tencent.com/document/product/1071/38149).


## Best Practice

| Practice                                                     | Documentation                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Integrating the MLVB SDK into your project                              | [SDK Integration](https://intl.cloud.tencent.com/document/product/1071/38155) |
| Encoding and publishing the video and audio captured by the camera and mic | [Publishing from Camera](https://intl.cloud.tencent.com/document/product/1071/38157) |
| Streaming the host’s screen plus the camera preview          | [Publishing from Screen]()                                                 |
| Playing published video in real time                       | [LVB Playback](https://intl.cloud.tencent.com/document/product/1071/38159) |
| Using the web superplayer TCPlayerLite for playback on mobile and desktop browsers | [Web (H5) Player](https://intl.cloud.tencent.com/zh/document/product/1071) |
| Creating a room and starting co-anchoring                                 | [Co-anchoring](https://intl.cloud.tencent.com/zh/document/product/1071/39888) |
| Using special effects such as eye enlarging, face slimming, nose slimming, animated stickers, AI keying, and green screen     | [AI-based Face Changing and Widgets]()                                            |
| Setting video quality                                             | [Setting Video Quality](https://intl.cloud.tencent.com/zh/document/product/1071) |
| Viewing statistics on publishing and playback status                              | [Viewing SDK Performance Statistics](https://cloud.tencent.com/document/product/454/9867) |
| Recording and archiving live streaming sessions                                     | [Recording and Replay](https://intl.cloud.tencent.com/zh/document/product/1071) |
| Playing at lower latency                                           | [LEB Playback](https://intl.cloud.tencent.com/zh/document/product/1071/39888) |

> ?
> - For details about the APIs associated with different features, please see [API Documentation > iOS](https://intl.cloud.tencent.com/zh/document/product/1071/38564) and [API Documentation > Android](https://intl.cloud.tencent.com/zh/document/product/1071/38569).
> - If an error occurs during your use of the SDK, you can refer to [Error Codes](https://cloud.tencent.com/document/product/454/17246) to troubleshoot the problem.



## Video Cloud Toolkit

Video Cloud Toolkit is an open-source and comprehensive live streaming solution. It is built on top of CSS, IM, and COS, and uses CVM to provide simple backend services. It offers features including login, sign-up, streaming, room list, co-anchoring, text chat, on-screen comments, etc. For instructions on how to use it, please see:

> ? If you run into a problem while using the demo, try troubleshooting the issue according to [Troubleshooting](https://cloud.tencent.com/document/product/454/8110) and [Error Codes and Logs](https://cloud.tencent.com/document/product/454/8292). If the problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for help.



## FAQs

-   [What push protocols does MLVB support?](https://intl.cloud.tencent.com/document/product/1071/39477) 
-  [Is there an upper limit on the number of concurrent viewers?](https://intl.cloud.tencent.com/document/product/1071/39695) 
-   [I recorded live streams. How can I get the recording files?](https://intl.cloud.tencent.com/document/product/1071/39695) 
-   [Do I have to purchase an MLVB license?](https://intl.cloud.tencent.com/document/product/1071/39476) 
-   [Latency](https://intl.cloud.tencent.com/zh/document/product/1071/39695) 
-   [Publishing Failure](https://intl.cloud.tencent.com/document/product/1071/39360) 
-   [Playback Failure](https://intl.cloud.tencent.com/document/product/1071/39361) 
-   [Video Stutter](https://intl.cloud.tencent.com/document/product/1071/39362) 
-   [Generating UserSig](https://intl.cloud.tencent.com/document/product/1071/39471) 

> ? For more Q&As, please see [FAQs](https://intl.cloud.tencent.com/document/product/1071/39477).


## Feedback and Suggestion

If you have any questions about MLVB, contact us via the following channels.

- If your question is about documents, for example, the content or a link in the documents, click **Send Feedback** in the bottom right of a document to provide your feedback.
- If you have questions about the MLVB service, talk to our [online customer service staff](https://cloud.tencent.com/act/event/Online_service?from=doc_267) or [submit a ticket](https://console.cloud.tencent.com/workorder/category).





