## Product Introduction
Tencent is the oldest and biggest instant messaging developer in China. QQ and WeChat, both developed by Tencent, have become indispensable apps for every Internet user. Following the trend of industrial digital transformations, Tencent shares its highly concurrent and reliable instant messaging capabilities. With SDKs provided by Tencent, you can easily integrate instant messaging features into your apps to meet various business needs.
To meet developers' requirements and scenarios in different phases, the Instant Messaging (IM) team provides a series of solutions, including the Android, iOS, Windows, and web SDK components, as well as capabilities for integrating [RESTful APIs](https://intl.cloud.tencent.com/document/product/1047/34620) and [Third-Party Callback APIs](https://intl.cloud.tencent.com/document/product/1047/34354) on the server. With these components and capabilities, developers can construct reliable and stable IM products for free and global communication.

## Architecture
IM provides a comprehensive suite of solutions, including global access, one-to-one chat, group chat, message push, profile and relationship chain hosting, and account authentication. It also provides complete app access and backend management APIs.
![](https://main.qcloudimg.com/raw/6537f6e705289419963ee647ae851c94.png)

## Services
### Access service
The access service provides IM with highly interconnected, reliable, and secure global network connection channels and proprietary multi-level optimal addressing algorithms to implement scheduling across private and public networks. Technologies, including intelligent compatibility for passing through gateway policies, persistent connection multiplexing, transport-layer protocol optimization, and channel encryption allow business personnel to establish simple and reliable communication with business backends without concerning about network details.

### One-to-one chat
One-to-one chat supports various message types, including text, emoji, location, image, audio, short video, and custom messages. It provides special features such as red packets, chatbots, read receipt, and message recall as well as services such as offline messages and roaming messages. For more information, please see [One-to-One Chat Messages](https://intl.cloud.tencent.com/document/product/1047/33523).

### Group chat
Group chat supports the following four group types based on group joining and organization management methods to meet the requirements of different group chat scenarios.

- **Work group for friends (Work)**: this is like an ordinary WeChat group. After a work group is created, users can join the group only after being invited by a friend who is a member of the group. The invitation does not need to be accepted by the invitee or approved by the group owner.
- **Public group (Public)**: this is like a QQ group. After a public group is created, the group owner can specify a group admin. When a user searches for the group ID and initiates a request to join the group, the request must be approved by the group owner or admin before the user can join the group.
- **Temporary meeting group (Meeting)**: after a temporary meeting group is created, users can join and exit the group freely and view group messages generated before they join the group. It applies to scenarios that involve real-time audio and video products, such as voice and video conferences and online education.
- **Audio-video chat room (AVChatRoom)**: after an audio-video chat room is created, users can join and exit the chat room freely. An audio-video chat room does not limit the number of members and does not support message history storage. Audio-video chat rooms can be used with Live Video Broadcasting (LVB) to support on-screen comment scenarios.

Groups are highly customizable, allowing you to use custom group types, fields, group IDs, and event callbacks. You can fully customize your group based on the needs of your app. For more information, please see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).
> Audio-video chat rooms (AVChatRoom) support unlimited group members. If a spike in group members is expected within a short time (such as large online events where members in a single group may exceed 50,000), contact Tencent Cloud customer service or sales representatives in advance and provide the SDKAppID and scheduled event time to apply for service resources.



### Profile and relationship chain hosting
IM provides a holistic solution for profile and relationship chain management, which can store user profiles (for example, nicknames, profile photos, and custom profile fields), friend lists, blocklists, and other information. IM's profile and relationship chain hosting service provides backup with up to 12 copies and multi-data center remote deployment to improve its service quality and disaster recovery performance. For more information, please see [Profile Management](https://intl.cloud.tencent.com/document/product/1047/33520) and [Relationship Chain Management](https://intl.cloud.tencent.com/document/product/1047/33521).

### Account authentication
Data security is ensured with asymmetric encryption ECDSA-SHA256 and hash encryption HMAC-SHA256 (HMAC-SHA256 is recommended). Developers can directly use the app's own account to quickly integrate IM services, avoiding the tedious account mapping work. With simple SDK integration and convenient API calls, it is easy to authenticate user accounts (UserID) and passwords (UserSig). For more information, please see [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517).

## Management and Monitoring
In addition to basic instant messaging features, IM provides a convenient and easy-to-use console, which allows you to create apps, download IM SDKs, query app configurations, perform joint app debugging, and integrate instant messaging capabilities. The IM console also provides various features such as backend message delivery, group management, and data statistics. For more information, please see [Console Guide](https://intl.cloud.tencent.com/document/product/1047/34577).

## Advanced Features
### RESTful APIs
RESTful APIs are HTTP management APIs that provide the app backend with a management entry at the backend. For more information about the RESTful APIs currently supported by IM, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

In addition to RESTful APIs, the IM console also provides features such as simple data management and one-to-one and one-to-many messaging. Developers can manage, view, and test data in the IM console. In contrast, RESTful APIs are less user-friendly, but they can provide more powerful management capabilities.


### Third-party callbacks
When IM initiates a [third-party callback](https://intl.cloud.tencent.com/document/product/1047/34354), it sends requests to the app backend before or after an event. Then, the app backend synchronizes data accordingly or intervenes in subsequent event processing.
IM provides a diverse set of callback APIs, which are free of charge. For more information, please see the [Callback Command List](https://intl.cloud.tencent.com/document/product/1047/34355).
