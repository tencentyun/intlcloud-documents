## Overview
This document describes how to create a topic in the console.

## Directions
>!You need to use the root account to create a topic subscription; otherwise, message delivery may fail.

1. Log in to the [CMQ Console](https://console.cloud.tencent.com/cmq) and click **Topic Subscription** on the left sidebar.
2. In the top-left corner of the topic subscription page, select a region.
3. On the topic subscription page, click **Create** and enter the information as prompted.
4. Click **Submit** to create a topic in the specified region.

You need to specify the following attributes when creating a topic:

| Attribute | Description | 
|---------|---------|
| Region | It sets the topic region and can be selected at the top of the topic subscription page. |
| Topic name | You need to enter the topic name, which cannot be modified once the topic is created. <br>It can contain 3–64 bytes of letters, digits, hyphens (-), and underscores (_). Excessive bytes will be automatically truncated. The name is case-sensitive. To avoid confusion, topics that have the same name in the same letter case cannot be created. | 
| Maximum message size | `MaximumMessageSize` attribute of topic. It specifies the maximum length of the message body that can be sent to the topic. It is measured in bytes and ranges from 1 to 1,024 KB. The default value is 64 KB. |
| Message lifecycle | It specifies the maximum period of time during which a message can be retained in the topic. After the period specified by this parameter has elapsed since a message is sent to the queue, the message will be deleted no matter whether it has been fetched. It is measured in seconds and defaulted to 86,400 seconds, which cannot be modified. |
| Message retention | It is enabled by default. Messages that are produced by a producer but have not triggered push to subscribers or failed to be received by subscribers will be retained in the topic temporarily. <br>In the topic list, you can view the approximate total number of currently retained messages. |
| Message filter type | Tag: for more information, please see [Tag Matching Feature Description](https://intl.cloud.tencent.com/document/product/406/6906).<br>Routing matching: for more information, please see [Routing Key Matching Feature Description](https://intl.cloud.tencent.com/document/product/406/8127). |

