## Introduction
As the earliest and biggest instant messaging developer, Tencent now shares its high-concurrency and highly reliable messaging capabilities to empower enterprises in their digital transformation efforts. With SDKs provided by Tencent, you can easily integrate instant messaging features into your apps to meet various business needs.
For developer requirements and scenarios in different phases, the Instant Messaging (IM) team provides a series of solutions, including the Android, iOS, Windows, and web SDK components, as well as capabilities for integrating [RESTful APIs](https://cloud.tencent.com/document/product/269/1519) and [Third-Party Callback APIs](https://cloud.tencent.com/document/product/269/1522) on the server. With these components and capabilities, developers can construct reliable and stable IM products for free and global communication.

## Architecture
IM features a comprehensive suite of solutions including global access, one-to-one chat, group chat, message push, profile and relationship chain hosting, and account authentication. It also provides complete app access and backend management APIs.
![](https://main.qcloudimg.com/raw/f603d5267b6404db1094dac0b4f5f01e.png)

## Services
### Access service
The access service provides IM with highly interconnected, reliable, and secure global network connection channels and proprietary multi-level optimal addressing algorithms to implement scheduling across private and public networks. Technologies including intelligent compatibility for passing through gateway policies, persistent connection multiplexing, transport-layer protocol optimization, and channel encryption allow businesses to establish simple and reliable communication with business backends without concerning about network details.

### One-to-one chat
One-to-one chat supports various message types including text, emojis, location markters, images, audio, short video, and custom message. It provides special features such as red packets, chatbot, read receipt, and message recall as well as services such as offline messages and roaming messages. For more information, see [One-to-One Messages](https://cloud.tencent.com/document/product/269/3662).

### Group chat
A group chat involves multiple participants. IM provides five built-in group types, including private group (private), public group (public), chat room (ChatRoom), audio-and-video chat room (AVChatRoom), and broadcasting chat room (BChatRoom). These group types are tailored to different group communication scenarios.

1. **Private group**: This group type is suitable for more private chat scenarios, where group information is not made public and users can only join the group through invitation by an existing group member.
2. **Public group**: This group type is suitable for public chat scenarios and has a strict management and admission mechanism.
3. **Chat room**: This group type has a less stringent management mechanism and allows users to join and exit the room freely. In addition, members can view the messages sent before they joined the chat room.
4. **Audio-and-video chat room**: This group type is similar to a chat room, but it does not impose a limit on the number of room members. It allows users to receive messages as guests on web clients.
5. **Broadcasting chat room**: This group type does not impose a limit on the number of room members and allows users to receive messages as guests on web clients. It is suitable for scenarios where messages need to be pushed to all online members on the app.

Groups are highly customizable, allowing you to use custom group types, fields, group IDs, and event callbacks. You can fully customize group types based on the needs of your app. For more information, see [Group System](https://cloud.tencent.com/document/product/269/1502).
>Audio-and-video chat rooms and broadcasting chat rooms support an unlimited number of participants. However, if the number of group members is expected to exceed 10,000, please contact [Tencent Cloud customer service](https://cloud.tencent.com/about/connect) or sales reps to apply for service resources.

### Profile and relationship chain hosting
IM provides a holistic solution for profile and relationship chain management, storing user profiles (for example, nickname, profile photos, and custom profile fields), friend lists, and blacklists. IM's profile and relationship chain hosting service provides a backup service with up to 12 copies and multi-data center remote deployment to improve service quality and disaster recovery performance. For more information, see [Profile Management](https://cloud.tencent.com/document/product/269/1500) and [Relationship Chain Management](https://cloud.tencent.com/document/product/269/1501).

### Account authentication
Data security is ensured with asymmetric encryption ECDSA-SHA256 and hash encryption HMAC-SHA256 (HMAC-SHA256 is recommended). Developers can directly use the app’s own account to quickly integrate IM services, freeing them from tedious account mapping work. With simple SDK integration and convenient API calls, it is easy to authenticate user accounts (UserID) and passwords (UserSig). For more information, see [Login Authentication](https://cloud.tencent.com/document/product/269/31999).

## Management and Monitoring
In addition to basic instant messaging features, IM provides a convenient and easy-to-use console, which allows you to create apps, download IM SDKs, query app configurations, perform joint app testing, and integrate instant messaging capabilities. IM Console also supports various features such as backend message delivery, user management, group management, and statistics. For more information, see [Console Guide](https://cloud.tencent.com/document/product/269/32577).

## Advanced Features
### RESTful APIs
RESTful APIs are HTTP management APIs that provide the app backend with a management entry at the backend. For the list of RESTful APIs currently supported by IM, see [RESTful API Overview](https://cloud.tencent.com/document/product/269/1519).

In addition to RESTful APIs, IM Console also provides simple features such as data management and one-to-one and one-to-many messaging. Developers can manage, view, and test data in IM Console. In contrast, RESTful APIs are less user-friendly, but they can provide more powerful management capabilities.


### Third-party callbacks
When IM initiates a [third-party callback](https://cloud.tencent.com/document/product/269/1522), it sends requests to the app backend before or after an event. Then, the app backend synchronizes data accordingly or intervenes in the subsequent processing of the event.
IM provides a diverse set of callback APIs, which are free of charge. For more information, see the [List of Callback Commands](https://cloud.tencent.com/document/product/269/1523).
