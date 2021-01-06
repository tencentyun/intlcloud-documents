
## Feature Overview

The Content Filtering feature uses natural language processing (NLP) technologies to determine whether user profiles, group profiles, one-to-one text messages, and group text messages in the IM system comply with regulations. This ensures automatic identification of unsafe or inappropriate content, reduces operational costs significantly, and enhances the product experience.
>!Currently, Content Filtering does not support passed-through custom messages.

## Content Filtering Basic
The Content Filtering Basic edition only provides some basic dictionaries and does not support adding custom dictionaries. To customize sensitive words, you can click **Upgrade** in the [IM console](https://console.cloud.tencent.com/im).


## Content Filtering Advanced
The Content Filtering Advanced edition supports custom sensitive words, detail query, and other features.

### How to activate
1. Log in to the [IM console](https://console.cloud.tencent.com/im), click the target IM application card, and select **Content Filtering** in the left sidebar.
2. Click **Upgrade**.
![](https://main.qcloudimg.com/raw/0a2bbd7680a1477fbdf58318c972b450.png)
3. In the dialog box, select **Enable Content Filtering Advanced** and complete payment. For pricing information, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350#value-added-service-pricing).
![](https://main.qcloudimg.com/raw/63ece6919e74f17b2056d937dbf7e8ea.png)

### Customizing sensitive words
After enabling Content Filtering Advanced, you can click **Content Filtering** > **Custom List** to customize sensitive words.
![](https://main.qcloudimg.com/raw/b21d4c48b2539fc098b4830af4672b23.png)
Click **Add Sample**, enter keywords, select a tag, and click **Submit**. Then the keywords will be added as sensitive words.

>!Up to 50 custom sensitive words can be added at a time. The total number of sensitive words cannot exceed 3,000, and a single sensitive word cannot exceed 10 characters.

![](https://main.qcloudimg.com/raw/62fc1558e5a9e41a5e69a2e9ff03ceb7.png)
Tags for custom sensitive words include comprehensive, politics, pornography, violence/terrorism, abuse, drug, and advertising.
![](https://main.qcloudimg.com/raw/65c475f9c1652f8fe69fb2f24a684fe2.png)

### Sensitive word detail query
After enabling Content Filtering Advanced, click a target application card, select **Content Filtering** in the left sidebar, and click **Detail Query**.

You can query the content filtering details for sensitive words with certain tags within the past 7, 14, and 30 days. The details include content, keywords, review results, review identifiers, and review time.
![](https://main.qcloudimg.com/raw/9c4c4ddd73a36ef557023b8e36224850.png)


## Custom Message Filtering
To provide custom message filtering, IM needs to use a third-party content filtering service.

The following figure shows the detailed process of custom message filtering. First, the IM SDK sends a message to the IM backend. The IM backend makes a request to the business backend for a callback before sending the [one-to-one message](https://intl.cloud.tencent.com/document/product/1047/34364) or [group message](https://intl.cloud.tencent.com/document/product/1047/34374). Second, the business backend copies the message content to the third-party content filtering service. After the third-party content filtering service returns the content filtering result, the business backend forwards the result to the IM backend. Last, the IM backend determines whether to deliver the message.
![](https://main.qcloudimg.com/raw/34bdd4f7adcb4919c8ef8dc68930ecf2.png)

## Image, Short Video, and Voice Filtering
To provide image, short video, and voice filtering, IM needs to use a third-party content filtering service.

The following figure shows the detailed process for image, short video, and voice filtering. First, the IM SDK sends a message to the IM backend. The IM backend delivers the message and makes a request to the business backend for a callback after sending the [one-to-one message](https://intl.cloud.tencent.com/document/product/1047/34365) or [group message](https://intl.cloud.tencent.com/document/product/1047/34375). Second, the business backend copies the message content to the third-party content filtering service. After the third-party content filtering service returns the content filtering result, the business backend forwards the result to the IM backend. Last, the IM backend determines whether to recall the [one-to-one message](https://intl.cloud.tencent.com/document/product/1047/35015) or [group message](https://intl.cloud.tencent.com/document/product/1047/34965).
![](https://main.qcloudimg.com/raw/f934c972855307282bba88f77ddbaf47.png)
