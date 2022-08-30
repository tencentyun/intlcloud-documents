## Overview
Community is a powerful tool for entertainment collaboration. It supports the **community**-**group**-**topic** hierarchy where messages are isolated and a high number of members share the same set of friend relationships. In addition, it allows you to group members and set group permissions for viewing, speaking, and managing things.
![](https://qcloudimg.tencent-cloud.cn/raw/7429b1c2a707a4f4f553cd7c2cbcb0db.jpg)
![](https://qcloudimg.tencent-cloud.cn/raw/8db16f94e4ab49ede5dc4207e9b20075.jpg)

## Use Cases
### Finding like-minded people: a new way to grow the number of users
- Community supports the accommodation of a high number of enthusiasts in the **community**-**group**-**topic** hierarchy.
- A large, open community provides more refined topics, so that users can talk and interact more freely and proactively.
![](https://qcloudimg.tencent-cloud.cn/raw/38f61b81280afed8df7cd699bbb204fb.jpg)

### Game-based social networking: higher user stickiness and engagement
Various community topics allow game players to access news, look for teammates, discuss plots, and share tips. Before the game, users can search for advice; during the game, they can always talk to others (through an always online chat room); after the game, they can dig deeper into the topics.
![](https://qcloudimg.tencent-cloud.cn/raw/e613a51181f771a6309731f8f5b5a09a.jpg)

### Fan marketing: an efficient operations tool
The diversified topics in a community can perfectly replace endless groups (such as group 1 of Shenzhen users, group 2 of Shenzhen users, group 1 of Guangzhou users, and group 1 of Shanghai users), eliminating the need to operate a number of tiring groups and making fan marketing more precise.
![](https://qcloudimg.tencent-cloud.cn/raw/45d3d5e8818cea79dd65b3b7abbb8d86.jpg)

### Organization management: a clear and layered communication method
All the members in an organization can join the same community, which supports hierarchical communication through the community hierarchy and permission settings. For example, topic A is only available for members in department A, and topic B is only available for members in department B.
![](https://qcloudimg.tencent-cloud.cn/raw/aa633c15337fbb8befe6c3f9a9a4f890.jpg)

## Technical Strengths
### A super large number of community members
The Tencent IM community is nearly ten thousand times larger than ordinary QQ and WeChat groups, perfectly meeting your needs to accommodate massive members in use cases such as finding like-minded people, fan marketing, game-based social networking, and organization management.
### Message reliability
The Tencent IM community greatly increases the number of members while incorporating Tencent's powerful messaging capabilities. With the complete and reliable messaging system built on over 20 years of technology accumulation, it delivers over 99.99% message sending/receiving success rate and service availability, helping you easily handle hundreds of millions of concurrent requests.
### Message push performance
The Tencent IM community adopts a new message push architecture with "fast and slow channels" plus "two-level push". This special type of architecture can well balance time and space for higher system push performance and lower terminal performance consumption. Users can enjoy the same message interaction experience in super-large groups as in general ones.

### Message status and user permission management
The Tencent IM community offers extended capabilities such as message editing, recall, and forwarding. It allows setting muting, enabling do-not-disturb, counting unread messages, and editing profiles globally or by community or topic.

## Native SDK Integration Guide
>!The community topic feature is supported only by the IM native SDK Enhanced edition on v6.2.2363 or later. To use it, purchase the Ultimate edition as instructed in [Creating and Upgrading an Application](https://www.tencentcloud.com/document/product/1047/34577) and apply for activation as instructed in [Configuration Change Ticket](https://intl.cloud.tencent.com/document/product/1047/44322).

The following describes community topic APIs for Android.

### Downloading and configuring the demo source code
For a quick tryout of the IM features, see [Android](https://intl.cloud.tencent.com/document/product/1047/45914). More UI components of the community topic are under development.
The following describes how to use the community topic feature by calling the APIs:

### Calling a community topic API
1. Call the `createGroup` API to create a topic-enabled community as instructed in the [Community Management](https://intl.cloud.tencent.com/document/product/1047/48172).
2. Call the `getJoinedCommunityList` API to get the list of created and joined communities.
>!A community is used for managing group members but doesn't support sending or receiving messages. For more information on other community features, see the list of "other management APIs".
>
3. After the community is created successfully, call the `createTopicInfoCommunity` API to create topics as instructed in [Topic Management](https://intl.cloud.tencent.com/document/product/1047/48172).
4. Topic management includes deleting a topic, modifying the topic information, getting the topic list, and listening for topic callbacks. In addition, topics support message sending and receiving for user communication. For more information on the APIs, see [Topic Message](https://intl.cloud.tencent.com/document/product/1047/48172).

## Web SDK Integration Guide
>!The community topic feature is supported only by the IM web SDK on v2.19.1 or later. To use it, purchase the Ultimate edition as instructed in [Creating and Upgrading an Application](https://www.tencentcloud.com/document/product/1047/34577) and apply for activation as instructed in [Configuration Change Ticket](https://intl.cloud.tencent.com/document/product/1047/44322).
>
The features of the community topic APIs are as follows:
### Downloading and configuring the demo source code
For a quick tryout of the IM features, see [Web](https://intl.cloud.tencent.com/document/product/1047/45912).
The following describes how to use the community topic feature by calling the APIs:

### Calling a community topic API
1. Call the `createGroup` API to create a topic-enabled community as instructed in [Community Management](https://intl.cloud.tencent.com/document/product/1047/48171).
2. Call the `getJoinedCommunityList` API to get the list of created and joined communities. A community is used for managing group members but doesn't support sending or receiving messages. For more information on other community features, see the ordinary group APIs.
3. After the community is created successfully, call the `createTopicInfoCommunity` API to create topics as instructed in [Topic Management](https://intl.cloud.tencent.com/document/product/1047/48171).
4. Topic management includes deleting a topic, modifying the topic information, getting the topic list, and listening for topic callbacks. In addition, topics support message sending and receiving for user communication. For more information on the APIs, see [createTextMessage](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#createTextMessage).

## References
- [Group Management](https://intl.cloud.tencent.com/document/product/1047/33530)
- [Group System](https://intl.cloud.tencent.com/document/product/1047/33529)
- [SDK and Demo Source Code](https://intl.cloud.tencent.com/document/product/1047/33996)
- [SDK Manual](https://web.sdk.qcloud.com/im/doc/zh-cn/TIM.html)
- [Android](https://intl.cloud.tencent.com/document/product/1047/34306)
- [SDK Integration (iOS)](https://intl.cloud.tencent.com/document/product/1047/34307)
- [SDK Integration (Web)](https://intl.cloud.tencent.com/document/product/1047/34309)

## Contact Us
If you have any questions, [contact us](https://intl.cloud.tencent.com/document/product/1047/41676).
