## Overview
Tencent is the earliest and biggest instant messaging developer in China. QQ and WeChat, both developed by Tencent, have become indispensable apps for every Internet user. In conformity with the trend of industrial digital transformation, Tencent now shares its high-concurrency and highly reliable instant messaging capabilities. With SDKs provided by Tencent, you can easily integrate instant messaging features into your apps to meet various business needs.
For developer requirements and scenarios in different phases, the Instant Messaging (IM) team provides a series of solutions, including the Android, iOS, Windows, and web SDK components, as well as capabilities for integrating [RESTful APIs](https://intl.cloud.tencent.com/document/product/1047/34620) and [Third-Party Callback APIs](https://intl.cloud.tencent.com/document/product/1047/34354) on the server. With these components and capabilities, developers can construct reliable and stable IM products for free and global communication.

## Architecture
IM features a comprehensive suite of solutions including global access, one-to-one chat, group chat, message push, profile and relationship chain hosting, and account authentication. It also provides complete app access and backend management APIs.
![](https://main.qcloudimg.com/raw/6537f6e705289419963ee647ae851c94.png)

## Services
### Access service
The access service provides IM with highly interconnected, reliable, and secure global network connection channels and proprietary multi-level optimal addressing algorithms to implement scheduling across private and public networks. Technologies including intelligent compatibility for passing through gateway policies, persistent connection multiplexing, transport-layer protocol optimization, and channel encryption allow businesses to establish simple and reliable communication with business backends without concerns about network details.
When terminals log in, the IM SDK connects to the nearest access nodes. IM access nodes include the following:

- China: South China, North China, East China, Hong Kong, and Taiwan
- Other regions:
 - Asia: Singapore, Indonesia, UAE, Thailand, Malaysia, Japan, Vietnam, India, South Korea, and Philippines
 - Europe: United Kingdom, Netherlands, France, Germany, Italy, Norway, France, Russia, and Spain
 - South America: Brazil
 - North America: United States, Canada, and Mexico
 - Oceania: Australia
 - Africa: South Africa and Nigeria


### One-to-one chat
One-to-one chat supports various message types including text, emojis, locations, images, audio, short video, and custom message. It provides special features such as red packets, chatbots, read receipt, and message recall as well as services such as offline messages and roaming messages. For more information, see [One-to-One Messages](https://intl.cloud.tencent.com/document/product/1047/33523).

### Group chat
A group chat involves multiple participants. IM supports the following four group types based on group joining and organization management methods to meet the requirements of different group chat scenarios.

- A **work group for friends (Work)** is like an ordinary WeChat group. After a work group is created, a user can only join the group by being invited by a friend who is a member of the group. The invitation does not need to be accepted by the invitee or approved by the group owner.
- A **public group (Public)** is like a QQ group. After a public group is created, the group owner can designate group admins. To join the group, a user needs to search for the group ID and send a request, and the request needs to be approved by the group owner or an admin before the user can join the group.
- A **meeting group (Meeting)** allows users to join and exit freely and supports viewing message history from before the user joined the group. Meeting groups are ideal for scenarios that integrate Tencent Real-Time Communication (TRTC), such as audio and video conferences and online education.
- An **audio-video group (AVChatRoom)** allows users to join and exit freely, supports an unlimited number of members, and does not store message history. Audio-video groups can be used with Cloud Streaming Services (CSS) to support on-screen comment chat scenarios.

Groups are highly customizable, supporting custom group types, group fields, group member fields, group IDs, and event callbacks. You can fully customize your group based on the needs of your app. For more information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).
>!Although audio-video groups (AVChatRoom) support unlimited group members, if a spike in group members is expected within a short time (in scenarios such as large online events where the number of members in a single group reaches 50,000 or above), contact sales representatives in advance and report service resource usage by providing the SDKAppID and the scheduled event time.



### Profile and relationship chain hosting
IM provides a holistic solution for profile and relationship chain management, storing user profiles (for example, nicknames, profile photos, and custom profile fields), friend lists, blacklists, and other information. IM's profile and relationship chain hosting service provides a backup service with up to 12 copies and multi-data center remote deployment to improve service quality and disaster recovery performance. For more information, see [Profile Management](https://intl.cloud.tencent.com/document/product/1047/33520) and [Relationship Chain Management](https://intl.cloud.tencent.com/document/product/1047/33521).

### Account authentication
Data security is ensured with asymmetric encryption ECDSA-SHA256 and hash encryption HMAC-SHA256 (HMAC-SHA256 is recommended). Developers can directly use the app’s own account to quickly integrate IM services, freeing themselves from tedious account mapping work. With simple SDK integration and convenient API calls, it is easy to authenticate user accounts (UserID) and passwords (UserSig). For more information, see [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517).

## Management and Monitoring
In addition to basic instant messaging features, IM provides a convenient, easy-to-use console, which allows you to create apps, download IM SDKs, query app configurations, perform joint app testing, and integrate instant messaging capabilities. IM console also supports various features such as backend message delivery, group management, and statistics. For more information, see [Console Guide](https://intl.cloud.tencent.com/document/product/1047/34577).

## Advanced Features
### RESTful APIs
RESTful APIs are HTTP management APIs that provide the app backend with a management entry at the backend. For the list of RESTful APIs currently supported by IM, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

In addition to RESTful APIs, IM Console also provides simple features such as data management and one-to-one and one-to-many messaging. Developers can manage, view, and test data in IM Console. In contrast, RESTful APIs are less user-friendly, but they can provide more powerful management capabilities.


### Third-party callbacks
When IM initiates a [third-party callback](https://intl.cloud.tencent.com/document/product/1047/34354), it sends requests to the app backend before or after an event. Then, the app backend synchronizes data accordingly or intervenes in the subsequent processing of the event.
IM provides a diverse set of callback APIs, which are free of charge. For more information, see the [List of Callback Commands](https://intl.cloud.tencent.com/document/product/1047/34355).

## Support for Private Deployment
Private deployment allows an enterprise to deploy systems directly to its own servers and save data locally. IM provides the private deployment feature to assist enterprises in the deployment, implementation, and OPS of the private version. If needed, please apply for the [IM private service](https://intl.cloud.tencent.com/apply/p/itvi76h023).
>?To apply for the IM private service, you need to log in with your root account of Tencent Cloud.

## Security and Compliance
Compliance is the foundation for the development of Tencent Cloud IM, which meets the compliance requirements of different countries and industries. In addition to ensuring the **security, compliance, availability, confidentiality, and privacy** of the services it provides, IM also provide relevant support for its customers to **meet their and their customers' compliance requirements, reduce repeated investment in audit work, and improve auditing and management efficiency**.

**IM has passed SOC reports (including SOC 1, SOC 2, and SOC 3), Cybersecurity Classified Protection 2.0, and ISO certifications (including ISO 9001 and ISO 20000).**
