## Overview

The video moderation feature helps you effectively identify restricted content (including pornography, illegal and non-compliant content, and ad) in videos. At present, CI supports automatic moderation and human moderation by professional teams to secure the platform in an all-around way.

#### Automatic moderation

The video moderation feature captures video frames to get images to be moderated. It is a security service with cutting-edge image recognition algorithms, which are trained with massive amounts of data in non-compliant images/videos to create a model for recognizing videos uploaded by users and live video streams and filtering pornographic, illegal, non-compliant, and advertising content. It delivers a high recognition accuracy and recall rate, meets the needs for content moderation in multiple dimensions, and has been constantly improved in its recognition standards and capabilities in real-time response to the changing regulatory requirements.

#### Human moderation

CI provides a professional human moderation team to verify the machine recognition results of pornographic, illegal, non-compliant, and advertising information, delivering a moderation accuracy of 99%.


## Use Cases

#### Ecommerce platform

More and more sellers upload videos to show their products to attract more customers. However, this also brings risks of non-compliant content such as QR codes and ads. The video moderation feature of CI covers all types of non-compliant content and filters various types of product videos in ecommerce scenarios to effectively guarantee users' browsing experience and protect the platform ecosystem.

#### Live streaming

Various industries are investing in live video streaming and real-time audio/video businesses. When developing live streaming businesses, enterprises and platforms need to pay special attention to content security. The live stream moderation feature of CI can detect pornographic, vulgar, abusive, and advertising content in live video streams.

#### Social media platform

Vlogs have become an important part of UGC on social media platforms, and diverse vlog scenarios also create moderation needs of various types. In addition, the video content on social media platforms is large in size and updated fast, and human moderation can hardly meet the efficiency requirements. The video moderation feature of CI covers various types of non-compliances. You can configure automatic triggering of moderation of incremental content in the console to quickly block the non-compliant content.

#### Online education

As most users of online education are minors, regulation of the platform content compliance by regulators is strict. This creates scene-specific content moderation requirements and more diverse detection tags. The video moderation feature of CI has a very high machine recognition accuracy and supports human moderation, safeguarding the education content security.

#### Video platform

Compared with other platforms where videos are stored, a professional video platform needs to moderate more long videos. As traditional moderation relies on humans to review, annotate, and remove non-compliant clips or entire videos, the moderation is time-consuming, and trending videos can be hardly published quickly. The video moderation feature of CI can quickly locate non-compliant clips and automatically block the videos, effectively improving the video moderation efficiency and guaranteeing the platform security.

## How to Use

#### Automatic moderation during upload

You can activate the service in the CI console. Then, incremental videos in the bucket will be moderated during upload. For more information, see [Configuring Video Moderation](https://cloud.tencent.com/document/product/460/46494).

#### Moderation by scanning historical data

For the historical video data stored in COS, you can configure historical data moderation in the console to moderate the videos in the specified bucket, directory, or time period.

#### Through an API

You can use APIs to moderate the content of images, videos, audios, text, documents, and webpages. For more information, see [Video Moderation](https://cloud.tencent.com/document/product/460/47362).


#### Through the SDK

You can also use the SDKs for diverse programming languages to moderate the content of images, videos, audios, text, documents, and webpages. For more information, see the following SDK documentation:

| SDK            | Integration Guide                                                     |
| :------------- | :----------------------------------------------------------- |
| Android SDK   | [Video Moderation](https://cloud.tencent.com/document/product/436/74520) |
| C SDK          | [Video Moderation](https://cloud.tencent.com/document/product/436/62020) |
| C++ SDK       | [Video Moderation](https://cloud.tencent.com/document/product/436/76276) |
| Go SDK        | [Webpage Moderation](https://cloud.tencent.com/document/product/436/65350) |
| .NET (C##) SDK  | [Video Moderation](https://cloud.tencent.com/document/product/436/63587) |
| iOS SDK        | [Webpage Moderation](https://cloud.tencent.com/document/product/436/74623) |
| JavaScript SDK | [Webpage Moderation](https://cloud.tencent.com/document/product/436/74618) |
| Node.js SDK   | [Webpage Moderation](https://cloud.tencent.com/document/product/436/76141) |
| Python SDK    | [Webpage Moderation](https://cloud.tencent.com/document/product/436/75184) |

>?
> The processing capabilities provided by CI have been fully integrated into the COS SDK, so you can directly use it to process data.

#### Viewing moderation results

- Callback settings: You can set the callback address, moderation type, and threshold to filter callbacks. The moderation result will be sent to your callback address automatically for subsequent operations. For more information on the callback content, see [Configuring Video Moderation](https://cloud.tencent.com/document/product/460/46494#.E5.9B.9E.E8.B0.83.E5.86.85.E5.AE.B9).
- Visual processing: After enabling the video moderation feature, you can view the moderation results by condition on the **Moderation Details** page in the console and manually process them. For more information, see [Moderation Details](https://cloud.tencent.com/document/product/460/46492).
