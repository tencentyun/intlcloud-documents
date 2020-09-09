
## Feature Overview

Content filtering uses natural language processing (NLP) technologies to determine whether user profiles, group profiles, one-to-one chat text messages, and group chat text messages in the IM system comply with regulations. This ensures automatic and intelligent message review, significantly reduces labor costs for content review, and enhances the product experience.
>! Currently, content filtering does not support passed-through custom messages.

## Content Filtering – Basic Edition
The content filtering basic edition is enabled by default. It only provides some politically sensitive word libraries and does not support word library customization. To customize sensitive words, click **Upgrade** in the IM console and purchase the content filtering professional edition on the [purchase page](https://buy.cloud.tencent.com/avc?position=1400399435).


## Content Filtering – Professional Edition
The content filtering professional edition provides sensitive word customization, query, and other features.

### How to enable
1. Log in to the [IM console](https://console.cloud.tencent.com/im), click a target application card, and click **Content Filtering** in the left sidebar.
2. Click **Upgrade** to go to the purchase page.
3. Select **Enable content filtering** and complete payment.

### Sensitive word customization
After you enable the content filtering professional edition, sensitive word customization is available for the content filtering module in the IM console. Then, you can select **Custom List** to customize sensitive words.
Click **Add Sample**, enter keywords, select tags, and click **Submit**.

>! A maximum of 50 custom sensitive words can be added at a time. The total number of sensitive words cannot exceed 3,000, and a single sensitive word cannot exceed 10 characters in length.


Tags for custom sensitive words include general, political, pornographic, violence and terrorism, abuse, drug-related, and ads.

### Sensitive word query
After you enable the content filtering professional edition, you can click a target application card in the IM console, click **Content Filtering** in the left sidebar, and click **Detail Query** to query sensitive words.

You can query content filtering details for sensitive words with certain tags within the past 7, 14, or 30 days. The content filtering details include the filtered content, keywords, review results, review identifiers, and review time.


## Custom Message Filtering
To provide custom message filtering, IM needs to use a third-party content filtering service.

The following figure shows the detailed process of custom message filtering. First, the IM SDK sends a message to the IM backend. The IM backend then calls a callback ([Invoke a Callback Before Sending One-to-One Messages](https://intl.cloud.tencent.com/document/product/1047/34364) or [Invoke a Callback Before Delivering Group Messages](https://intl.cloud.tencent.com/document/product/1047/34374)) before sending the message to the third-party content filtering service. Second, the business backend copies the content of the message to the third-party content filtering service. After the third-party content filtering service returns the content filtering result, the business backend forwards the result to the IM backend. Lastly, the IM backend determines whether to deliver the message.
![](https://main.qcloudimg.com/raw/34bdd4f7adcb4919c8ef8dc68930ecf2.png)

## Image, Short Video, and Voice Filtering
To provide image, short video, and voice filtering, IM needs to use a third-party content filtering service.

The following figure shows the detailed process for image, short video, and voice filtering. First, the IM SDK sends a message to the IM backend. The IM backend then calls a callback ([Invoke a Callback Before Sending One-to-One Messages](https://intl.cloud.tencent.com/document/product/1047/34364) or [Invoke a Callback Before Delivering Group Messages](https://intl.cloud.tencent.com/document/product/1047/34374)) before sending the message to the third-party content filtering service. Second, the business backend copies the content of the message to the third-party content filtering service. After the third-party content filtering service returns the content filtering result, the business backend forwards the result to the IM backend. Lastly, the IM backend determines whether to recall the [one-to-one chat message](https://intl.cloud.tencent.com/document/product/1047/35015) or [group chat message](https://intl.cloud.tencent.com/document/product/1047/34965).
![](https://main.qcloudimg.com/raw/f934c972855307282bba88f77ddbaf47.png)
