## Overview

The webpage moderation feature helps you effectively identify restricted content (including pornography, violation, and ad) in webpages. At present, CI supports automatic moderation and human moderation by professional teams to secure the platform in an all-around way.

#### Automatic moderation

The webpage moderation feature gets images and text on a webpage to be moderated. It is a security service with cutting-edge image recognition algorithms and non-compliant text models, which are trained with massive amounts of non-compliant data to create a model for recognizing webpage content uploaded by users and filtering pornographic, advertising, illegal, and non-compliant content. It delivers a high recognition accuracy and recall rate, meets the needs for content moderation in multiple dimensions, and has been constantly improved in its recognition standards and capabilities in real-time response to the changing regulatory requirements.

#### Human moderation

CI provides a professional human moderation team to verify the machine recognition results of pornographic, illegal, non-compliant, and advertising information, delivering a moderation accuracy of 99%.


## Use Cases

#### Webpage platform

Compared with other platforms where webpages are stored, a professional webpage platform needs to moderate more long webpages. As traditional moderation relies on humans to review, annotate, and remove non-compliant webpage elements, moderation is time-consuming, and trending webpages can hardly be processed quickly. CI's webpage moderation feature can quickly locate non-compliant elements and automatically block them, effectively improving the webpage moderation efficiency and guaranteeing the platform security.

#### Ebook

CI's webpage moderation feature can quickly locate non-compliant elements in high amounts of text, book covers, and advertising content on ebook webpages. This helps websites avoid the risk of content non-compliance and improves the reader experience.

## How to Use

### Using APIs

You can use the provided APIs to moderate images and text on webpages. For more information, see [Webpage Moderation](https://www.tencentcloud.com/document/product/1045/52184).

### Using SDKs

You can also use the SDKs for diverse programming languages to moderate the images and text on webpages. For more information, see the following SDK documentation:

| SDK            | Integration Guide                                                     |
| :------------- | :----------------------------------------------------------- |
| Android SDK    | Webpage Moderation |
| C++ SDK        | [Webpage Moderation](https://intl.cloud.tencent.com/document/product/436/52358) |
| Go SDK        | Webpage Moderation|
| iOS SDK        | Webpage Moderation |
| JavaScript SDK | [Webpage Moderation](https://intl.cloud.tencent.com/document/product/436/52201) |
| Node.js SDK   | [Webpage Moderation](https://intl.cloud.tencent.com/document/product/436/52337) |
| Python SDK    | [Webpage Moderation](https://intl.cloud.tencent.com/document/product/436/52130) |

>?
> The processing capabilities provided by CI have been fully integrated into the COS SDK, so you can directly use it to process data.

#### Viewing moderation results

- Callback settings: You can set the callback address, moderation type, and threshold in a request to filter callbacks. The moderation result will be sent to your callback address automatically for subsequent operations.
- Visual processing: After enabling the webpage moderation feature, you can view the moderation results by condition on the **Moderation Details** page in the console and manually process them. For more information, see [Moderation Details](https://intl.cloud.tencent.com/document/product/1045/52106).
