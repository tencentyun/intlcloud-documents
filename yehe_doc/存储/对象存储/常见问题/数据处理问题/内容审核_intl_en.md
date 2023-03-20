### How is content moderation billed?

**Image, video, audio, text, document, and webpage moderation services** are billed by CI. For billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1045/33431).

### Is the text moderation feature supported?

Yes. It can check text content for pornographic, illegal, advertising, and abusive information. For detailed directions, see [Setting Text Moderation](https://www.tencentcloud.com/document/product/436/52101).


### What should I do if a callback URL has been configured for text moderation but callback fails due to network errors?

After callback is enabled, the system will return the text moderation result to you. If the callback fails due to network errors, the callback will be retried once every 30 minutes for 24 hours.

### How do I create an audio moderation job?

You can call the `CreateAudioAuditingJobs` API to submit an audio moderation job as detailed in [Submitting Audio Moderation Job](https://intl.cloud.tencent.com/document/product/436/48262).

### How do I submit a video moderation job?

You can call the `CreateVideoAuditingJob` API to submit a video moderation job as detailed in [Submitting Video Moderation Job](https://intl.cloud.tencent.com/document/product/436/48249).

### How do I submit a webpage moderation job?

For detailed directions, see [Submitting Webpage Moderation Job](https://intl.cloud.tencent.com/document/product/436/48282).


### How long does it take to call a content moderation API normally?

It normally takes 1 second to call a content moderation API.

### How do I set to only moderate incremental images for content moderation?

For detailed directions, see [Setting Image Moderation](https://www.tencentcloud.com/document/product/436/52098).

### How do I view the content moderation result?

Log in to the COS console, click the target bucket name to enter the bucket configuration page, and select **Sensitive Content Moderation** > **Moderation Details** to view the content moderation result. For detailed directions, see [Moderation Details](https://www.tencentcloud.com/document/product/436/52093).

### Does image moderation support customizing non-compliant content for moderation?

No. Currently, it can moderate images for pornographic, illegal, and advertising content. For more information, see [Moderation Details](https://www.tencentcloud.com/document/product/436/52093).

### What are the confirmed part and uncertain part in image moderation?

Image moderation adopts a scoring mechanism, with a score between 0 and 100 returned for each image. A value in the range of 0–60, 61–90, or 91–100 means the image is normal, suspiciously sensitive, or sensitive respectively. Confirmed part refers to normal and sensitive images, while uncertain part refers to suspiciously sensitive images.

### Are sensitive image, text, audio, and video moderation features available?

Yes. The COS content moderation service intelligently moderates the multimedia content of images, videos, speeches, and text. It helps you effectively identify non-compliant content such as pornographic, vulgar, illegal, disgusting, and offensive information to avoid operational risks. For more information, see [Content Moderation Overview](https://www.tencentcloud.com/document/product/436/53946).

### How do I unblock an image through an API?

Blocking an image is actually to set the image access to private read/write. Currently, you cannot unblock an image through an API. We recommend that you unblock the image on the **Moderation Details** page in the console as detailed in [Moderation Details](https://www.tencentcloud.com/document/product/436/52093).




