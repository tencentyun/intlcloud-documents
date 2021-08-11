### Supported Platforms

The following platforms can communicate with each other and provide services across devices and platforms.

| Platform | SDK and Compatibility | Demo | Source Code | UI Component |
| ------- | --------------| -------- | -------- | -------- |
| Android | Compatible with JDK 1.6 and Android SDK version 14 and later | Supported | Supported | Supported |
| iOS | Compatible with iOS 8.0 and later | Supported | Supported | Supported |
| Mac | Compatible with OS X 10.10 and later | Supported | Supported | - |
| Windows | C and C++ are included. Compatible with Windows 7, Windows 8 and 8.1, and Windows 10. Both 32-bit and 64-bit programs can be connected. | - | - | - |
| Web | Supports Internet Explorer 9+, Chrome 7+, Firefox 3.6+, Opera 12+ and Safari 6+ | Supported | - | - |
| Mini Program | Supported | Supported | - | - |



### Global Access

| Feature Type | Description |
| -------------- | -------------- |
| Global access overview | IM provides highly reliable and secure network connections with global coverage. With its proprietary multi-level optimal addressing algorithm, IM can perform scheduling across the entire network. When terminals log in from outside the Chinese mainland, IM SDK connects to the nearest access nodes or cache nodes. |
| China | South China, North China, East China, Hong Kong, Taiwan, etc. |
| Global | Asia: Japan, South Korea, Singapore, India, Thailand, Malaysia, Vietnam, Philippines, UAE<br>Europe: Germany, United Kingdom, France, Russia, Italy, Norway, Spain<br>North America: United States, Canada, Mexico<br>South America: Brazil<br><br>Oceania: Australia<br>Africa: South Africa, etc. |


### Account Features

| Feature Type | Description |
| ------------ | -------------------------------------- |
| Import accounts | Import accounts in batches |
| Deactivate accounts | Invalidate UserSig |
| Delete accounts | Delete accounts in batches |
| User online status | Manage the online and offline statuses after users log in |

### Multi-Device Login

| Feature Type | Description |
| ------------- | --------------- |
| Single-device login | Single-device login is allowed only across Windows, web, Android, and iOS platforms. |
| Dual-device login (default) | Single-device login across Windows, Android, and iOS with a web device online simultaneously is allowed. |
| Triple-device login | Single-device login across Android and iOS with one Windows device and one web device online simultaneously is allowed. |
| Multi-device online | Multiple Windows, web, Android, and iOS devices can be online simultaneously. |

>? You can configure multi-device login by logging in to the [IM console](https://console.cloud.tencent.com/im) and clicking **App Configuration** for the target app to open the **Feature Configuration** page.

### Message Types

| Feature Type | Description |
| ------------ | ----------------- |
| Text | The message content is plain text. |
| Image | The message content includes the URL, dimensions, and size of the image. |
| Emoji | Emoji messages are customized by developers. |
| Audio | Audio data must include the duration in seconds. |
| Location | The message content includes the caption, longitude, and latitude of the location. |
| File | The message content includes the URL, size, and format of the file. There are no file format restrictions, and the maximum supported file size is 100 MB. |
| Short video | The message content includes the URL, duration, size, and format of the video file. The maximum supported file size is 100 MB. |
| Custom | Message types that are customized by developers, such as red packet and rock-paper-scissor. |
| System notification | This type of message includes built-in system notification messages and system notification messages customized by developers. |



### Message Features

| Feature Type | Description |
| -------- | -------- |
| Download messages | The app admin can obtain all one-to-one or group messages for a specified hour of a specified day through this API. |
| Offline messages | IM supports offline push when a user logs in, the app switches to work in the background, and other users send messages. |
| Roaming messages | When a user logs in on a new device, the historical message storage recorded (on the cloud) by the server is synchronized to the new device. Roaming messages are stored for 7 days by default. You can pay to increase the roaming message storage period. |
| Multi-device synchronization | Messages are synchronized and received across multiple devices. |
| Historical messages | Both local and cloud historical messages are supported. |
| Recall messages | Recall a message that has been delivered successfully. By default, messages that were delivered more than 2 minutes ago cannot be recalled. Only one-to-one and group chat messages can be recalled. Messages sent in audio-video chat rooms (AVChatRooms) cannot be recalled. |
| Read receipts | Users can check if messages have been read in a one-to-one chat. |
| Forward messages | Users can forward messages to other users or groups. |
| @ feature | There is no essential difference between an in-group @ message and an ordinary message, although the user specified by @ will see a special UI effect. |
| Typing status indicator | This feature can be implemented in online messaging scenarios. |
| Offline push | Apple APNs, Xiaomi push, Huawei push, Meizu push, OPPO push, vivo push, and Google FCM push are supported. |
| Delete messages | Use the remove method for messages to delete messages locally. |
| Red packets | Red packet messages are similar to @ messages and can be implemented through TIMCustomElem. |


### Profile Features

| Feature Type | Description |
| ------------------ | ---------------- |
| Set user profiles | Users can set information including the nickname, verification method, profile photo, gender, age, signature, and location. |
| Obtain user profiles | Users can view their own profiles and the profiles of friends and strangers. |
| Obtain user information by fields | This feature can obtain user information based on specific fields. |
| Custom user information | Up to 20 custom user profile fields are supported. |



### Relationship Chain Features

| Feature Type | Description |
| -------------------- | ---------------------- |
| Search for friends | Search for a friend by account ID. |
| Apply for friend requests | Specify whether a request reason is required. The default is no. |
| Add friends | Send friend requests. |
| Delete friends | Friends can be deleted after they are added to the contact list. |
| Obtain all friends | This feature can obtain all friends. Only basic information of friends is pulled by default. |
| Accept/Reject friend requests | Accept or reject a friend request after receiving a friend request system notification. |
| Add to the blocklist | Blocklist any user. If you blocklist friends, you also unfriend them. |
| Remove from the blocklist | Remove a user from the blocklist. |
| Obtain the blocklist | Pull the blocklist of users. |
| Remarks | Add remarks for a friend. |
| Set custom friend profile fields | Up to 20 custom fields are allowed. |
| Create a friend list | When creating a list, you can choose who goes to the list. A user can be added to multiple lists. |
| Delete a friend list | Delete a friend list. |
| Add a friend to a list | Add a friend to a list. |
| Delete a friend from a list | Remove a friend from a list. |
| Rename a friend list | Rename a friend list. |
| Obtain friend list information | Obtain a specific friend list. |
| Obtain all friend lists | Obtain the information of all friend lists. This can also be achieved by obtaining all friends. |
| Relationship chain storage | The SDK can store relationship chain information. |
| System notifications on friend profile changes | When a friend’s profile changes, you will receive a system notification. |
| System notification on relationship chain changes | When a relationship chain change occurs, you will receive a system notification. |



### Group Features
Based on common use cases, IM has set the following default group types:
- A work group for friends (Work) is like an ordinary WeChat group. After a work group is created, a user can only join the group by being invited by a friend who is a member of the group. The invitation does not need to be accepted by the invitee or approved by the group owner.
- A social networking group for strangers (Public) is like a QQ group. After a public group is created, the group owner can designate group admins. To join the group, a user needs to search for the group ID and send an application, and the application needs to be approved by the group owner or an admin before the user can join the group.
- A temporary meeting group (Meeting) allows users to join and exit freely and supports viewing message history from before the user joined the group. Meeting groups are ideal for scenarios that integrate Tencent Real-Time Communication (TRTC), such as audio and video conferences and online education.
- An audio-video group (AVChatRoom) allows users to join and exit freely, supports an unlimited number of members, and does not store message history. Audio-video groups can be used with Live Video Broadcasting (LVB) to support on-screen comment chat scenarios.

The following table compares the default features of each group type:

| Feature Type | <div style="width:100px"> Work</div> | <div style="width:20%">Public</div> | <div style="width:20%">Meeting</div> | <div style="width:20%">AVChatRoom</div> |
| ---------- | --------------------- | --------------------- | --------------------- | -------------------------- |
| Maximum number of members | 6,000 | 6,000 | 6,000 | No upper limit |
| Restrictions on obtaining member profiles | All available | All available | All available | Only the profiles of the first 300 members are displayed |
| Setting admins | Not supported | Supported | Supported | Not supported |
| Group profile modification permissions |<li>Any group member can modify it.<li>Backend app admin | <li>Group owner<li>Group admins<li>Backend app admin | <li>Group owner<li>Group admins<li>Backend app admin | <li>Group owner <li>Backend app admin |
| Group deletion permissions | Backend app admin | <li>Group owner<li>Backend app admin | <li>Group owner<li>Backend app admin | <li>Group owner<li>Backend app admin |
| Group owner leaving the group | Supported | Not supported | Not supported | Not supported |
| Application to join the group | Not supported | Supported and approval by the group owner or group admin is required | Supported, but no approval is required | Supported, but no approval is required |
| Group members can invite other users to join the group | Supported | Not supported | Not supported | Not supported |
| Removing members from the group | <li>Group owner<li>Backend app admin | <li>Group owner<li>Group admins<li>Backend app admin | <li>Group owner<li>Group admins<li>Backend app admin | Not supported, but the mute feature can be used to achieve a similar effect |
| Muting permissions | Not supported | <li>Group owner<li>Group admins (can only mute ordinary group members)<li>Backend app admin | <li>Group owner<li>Group admins (can only mute ordinary group members)<li>Backend app admin | <li>Group owner<li>Backend app admin |
| Viewing historical messages from before joining the group | Not supported | Not supported | Supported | Not supported |
| Member change notifications (joining/leaving the group, etc.) | All members | All members | None | All members |
| Group activation by sending a message after group creation | Required | Not required | Not required | Not required |
| Unread message count | Supported | Supported | Not supported | Not supported |
| Importing groups (group members/profiles, etc.) | Supported | Supported | Supported | Not supported |



### IM Console

You can log in to Tencent Cloud [IM console](https://console.cloud.tencent.com/im) to configure the app based on your needs.

| Feature Type | Description |
| -------------- | ------------------------ |
| Create an app | Create an app |
| Download the SDK | Download the client SDK |
| App configuration | Configure apps |
| Statistics | View operational data |
| View crashes | Report errors |
| Callback configuration | Perform third-party callbacks |
| Feature configuration | Add custom fields and online instances |
| Developer tool | Generate UserSig on the webpage |



### Statistics

The [statistics and analytics](https://console.cloud.tencent.com/im) feature in the IM console allows you to view operational data in various dimensions.

| Statistic Type | Description |
| ---------------- | -------------------------------- |
| Active users | The number of users that have connected to and interacted with the server (de-duplicated) |
| New sign-ups | The number of newly registered IDs |
| Total sign-ups | View the total number of registered users |
| Upstream messages | Specify a time period and view the number of upstream messages |
| Message senders | Specify a time period and view the number of message senders |
| Peak concurrent online users | Specify a time period and view the number of concurrent online users |
| One-to-one chat upstream messages | Specify a time period and view the number of one-to-one chat upstream messages |
| One-to-one chat message senders | Specify a time period and view the number of one-to-one chat message senders |
| Group upstream messages | Specify a time period and view the number of group upstream messages |
| Group message senders | Specify a time period and view the number of group message senders |
| Message sending groups | Specify a time period and view the number of groups that send messages |
| New groups | Specify a time period and view the number of new groups |
| Total groups | Specify a time period and view the total number of groups |
| Export data | Specify a time period and export data |

### Support for Private Deployment
Private deployment allows an enterprise to deploy systems directly to its own servers and keep data locally. IM provides the private deployment feature to assist enterprises in the deployment, implementation, and operation and maintenance of the private version. If needed, please apply for the [IM private service](https://intl.cloud.tencent.com/apply/p/itvi76h023).
>?To apply for the IM private service, you need to log in with your main account of Tencent Cloud.
