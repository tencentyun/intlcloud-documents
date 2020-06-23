## Product Introduction
Tencent is the first and the largest instant messaging developer in China. QQ and WeChat, both developed by Tencent, have become indispensable apps for every internet user. In keeping with the trend of industrial digital transformation, Tencent now shares its high-concurrency and highly reliable instant messaging capabilities. With SDKs provided by Tencent, you can easily integrate instant messaging features into your apps to meet various business needs.
For developer requirements in different phases and scenarios, Tencent's IM team provides a series of solutions, including Android, iOS, Windows, and web SDK components, as well as capabilities for integrating [RESTful APIs](https://intl.cloud.tencent.com/document/product/1047/34620) and [third-party callback APIs](https://intl.cloud.tencent.com/document/product/1047/34354) on the server. With these components and capabilities, developers can construct reliable and stable instant messaging products for free and global communication.

## Architecture
Instant Messaging (IM) features a comprehensive suite of solutions including global access, one-to-one chat, group chat, message push, profile and relationship chain management, and account authentication. It also provides complete app access and backend management APIs.
 ![](https://main.qcloudimg.com/raw/6537f6e705289419963ee647ae851c94.png)

## Services
### Access service
The access service provides IM with highly interconnected, reliable, and secure global network connections and proprietary multi-level optimal addressing algorithms to implement scheduling across private and public networks. Technologies including intelligent compatibility for gateway passthrough policies, persistent connection multiplexing, transport-layer protocol optimization, and channel encryption allow businesses to establish simple and reliable communication with business backends without the need to worry about network details.
When terminals log in, the IM SDK connects to the nearest access nodes or cache nodes. Global access and cache nodes include the following:

- China: South China, North China, East China, and Hong Kong
- Other countries (regions):
 - Asia: Singapore, Indonesia, UAE, Thailand, Japan, Vietnam, and India
 - Europe: United Kingdom, Netherlands, Germany, Italy, Norway, France, and Russia
 - South America: Brazil
 - North America: United States, Canada, and Mexico
 - Oceania: Australia
 - Africa: South Africa


### One-to-one chat
One-to-one chat supports various message types including text, emojis, locations, images, audio, user generated short videos, and custom messages. It provides special features such as red packets, chatbots, read receipts, and message recall as well as services such as offline messages and roaming messages. For more information, see [One-to-One Chat Messages](https://intl.cloud.tencent.com/document/product/1047/33523).

### Group chat
A group chat involves multiple participants. IM provides four predefined group types tailored to different group communication scenarios, which pertain to different group joining modes and management and organizing modes.

- **Work group**: similar to a common WeChat group. After a work group is created, only a group member can invite other users to join this group, and the invitation does not need to be approved by the invited user or group owner.
- **Public group**: similar to a QQ group. After a public group is created, the group owner can specify a group admin. When a user searches the group ID and initiates a request to join the group, the request must be approved by the group owner or admin before the user can join the group.
- **Meeting group**: after a meeting group is created, a user can join and quit the group as desired, and view messages before the user joins the group. This group type is suitable for scenarios where real-time audio/video services are used, for example, audio and video conferencing and online education.
- **Audio-video chat room (AVChatRoom)**: after an AVChatRoom is created, a user can join and quit the group as desired. This group type does not limit the number of members, but it does not support storage of historical messages. It can be used together with Tencent's Live Video Broadcasting service to support on-screen comments.

Groups are highly customizable, allowing you to use custom group types, group member fields, group IDs, and event callbacks. You can fully customize your group based on the needs of your app. For more information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).
> Though AVChatRooms support unlimited group members, if a spike in group members within a short time is expected (in scenarios such as large online events where members in a single group exceed 50,000), contact Tencent Cloud customer service or sales representatives in advance and report the service resource usage by providing the SDKAppID and the scheduled event time.



### Profile and relationship chain management
IM provides a holistic solution for profile and relationship chain management, storing user profiles (for example, nicknames, profile photos, and custom profile fields), friend lists, blacklists, and other information. The IM profile and relationship chain management service provides a backup service with up to 12 copies and multi-data center remote deployment to improve service quality and disaster recovery performance. For more information, see [Profile Management](https://intl.cloud.tencent.com/document/product/1047/33520) and [Relationship Chain Management](https://intl.cloud.tencent.com/document/product/1047/33521).

### Account authentication
Data security is ensured with asymmetric encryption ECDSA-SHA256 and hash encryption HMAC-SHA256 (HMAC-SHA256 is recommended). Developers can directly use the app's own account to quickly integrate IM services, freeing themselves from tedious account mapping work. With simple SDK integration and convenient API calls, it is easy to authenticate user accounts (`UserID`) and passwords (`UserSig`). For more information, see [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517).

## Management and Monitoring
In addition to basic instant messaging features, IM provides a convenient and easy-to-use console, which allows you to create apps, download IM SDKs, query app configurations, perform joint app testing, and integrate instant messaging capabilities. The IM Console also supports various features such as backend message delivery, user management, group management, and statistics. For more information, see [Console Guide](https://intl.cloud.tencent.com/document/product/1047/34577).

## Advanced Features
### RESTful APIs
RESTful APIs are HTTP management APIs that provide the app backend with a management entry at the backend. For the list of RESTful APIs currently supported by IM, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

In addition to RESTful APIs, the IM console also provides simple features such as data management and one-to-one and one-to-many messaging. Developers can manage, view, and test data in the IM Console. In contrast, RESTful APIs are less user-friendly, but they provide more powerful management capabilities.


### Third-party callbacks
When IM initiates a [third-party callback](https://intl.cloud.tencent.com/document/product/1047/34354), it sends requests to the app backend before or after an event. Then the app backend synchronizes data accordingly or intervenes in the subsequent processing of the event.
IM provides a diverse set of callback APIs, which are free of charge. For more information, see the [Callback Command List](https://intl.cloud.tencent.com/document/product/1047/34355).
