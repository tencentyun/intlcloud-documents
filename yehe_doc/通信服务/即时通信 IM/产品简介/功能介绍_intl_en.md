### Supported Platforms

The following platforms can communicate with each other and provide services across devices and platforms.

| Platform | SDK and Compatibility | Demo | Source Code | UI Component |
| ------- | --------------| -------- | -------- | -------- |
| Android | Compatible with JDK 1.6 and Android SDK version 14 and later | Supported | Supported | Supported |
| iOS | Compatible with iOS 8.0 and later | Supported | Supported | Supported |
| Mac | Compatible with OS X 10.10 and later | Supported | Supported | - |
| Windows | C and C++ are included. Compatible with Windows 7, Windows 8 and 8.1, and Windows 10. Both 32-bit and 64-bit programs can be connected. | - | - | - |
| Web | Support IE 9+, Chrome 7+, FireFox 3.6+, Opera 12+, and Safari 6+ | Supported | - | - |
| Mini Program | Supported | Supported | - | - |



### Global Access

| Feature Type | Description |
| -------------- | -------------- |
| Global access overview | IM provides reliable and secure network connections with global coverage. With its proprietary multi-level optimal addressing algorithm, IM can perform scheduling throughout the network. When terminals log in from outside Mainland China, the IM SDK connects to the nearest access node or cache node. |
| China | South China, North China, East China, Hong Kong, and more |
| Global | Asia: Japan, South Korea, Singapore, India, Thailand, Malaysia, Vietnam, Philippines, and UAE<br>Europe: Germany, United Kingdom, France, Russia, Italy, Norway, and Spain<br>North America: United States, Canada, and Mexico<br>South America: Brazil<br>Oceania: Australia<br>Africa: South Africa and more |


### Account Features

| Feature Type | Description |
| ------------ | -------------------------------------- |
| Import accounts | Import accounts in batches |
| Deactivate accounts | Invalidate UserSig |
| Delete accounts | Delete accounts in batches |
| User online status | Manage the online and offline statuses of logged-in users |

### Multi-Device Login

| Feature Type | Description |
| ------------- | --------------- |
| Single-client login | Single-client login is allowed only for Windows, web, Android, and iOS platforms. |
| Dual-client login (default) | Single-client login for Windows, Android, and iOS with a web client online simultaneously is allowed. |
| Triple-client login | Single-client login for Android and iOS with one Windows device and one web client online simultaneously is allowed. |
| Multi-client online | Multiple Windows, web, Android, and iOS clients can be online simultaneously. |

> You can configure multi-client login by logging in to the [IM console](https://console.cloud.tencent.com/im) and clicking **App Configuration** for the target application to open the **Feature Configuration** page.

### Message Types

| Feature Type | Description |
| ------------ | ----------------- |
| Text | The message content is in plain text. |
| Image | The message content includes image URLs, dimensions, and sizes. |
| Emoji | Emoji messages are customized by developers. |
| Audio | The duration (in seconds) must be provided for audio data. |
| Location | The message content includes the caption, longitude, and latitude of the location. |
| File | The message content includes the URL, size, and format of the file. There are no file format restrictions, and the maximum supported file size is 28 MB. |
| UGSV | The message content includes the URL, duration, size, and format of the short video. The maximum supported file size is 28 MB. |
| Custom | Message types that are customized by developers, such as gift envelope and rock-paper-scissor |
| System notification | This type of message includes built-in system notification messages and system notification messages customized by developers. |



### Message Features

| Feature Type | Description |
| -------- | -------- |
| Download messages | The app admin can use this API to obtain all one-to-one or group chat messages for a specified hour of a specified day. |
| Offline messages | IM supports offline push when a user logs in, the app switches to work in the background, and other users send messages. |
| Roaming messages | When an account is logged in on a new device, historical messages of the account (stored in the server in the cloud) are synchronized to the new device. Roaming messages are retained for 7 days by default. You can pay to increase the retention period of roaming messages. |
| Multi-device synchronization | Messages are synchronized and received across multiple devices. |
| Historical messages | Both local and cloud historical messages are supported. |
| Recall messages | Recall a message that has been delivered. Messages that were delivered more than 2 minutes ago cannot be recalled. Only one-to-one and group chat messages can be recalled. Messages sent in audio-and-video chat rooms (AVChatRoom groups) cannot be recalled. |
| Read receipts | Users can check if messages have been read in a one-to-one chat. |
| Forward messages | Users can forward messages to other users or groups. |
| @ feature | There is no essential difference between an in-group @ message and an ordinary message, although the user specified by @ will see a special UI effect. |
| Typing status indicator | This feature can be implemented in online messaging scenarios. |
| Offline push | APNs and push services on Xiaomi, Huawei, MEIZU, OPPO, and Vivo mobile phones are supported. |
| Delete messages | Use the remove method for messages to delete messages locally. |
| Red packets | Red packet messages are similar to @ messages and can be implemented through TIMCustomElem. |


### Profile Features

| Feature Type | Description |
| ------------------ | ---------------- |
| Set user profiles | Users can set information including the nickname, verification method, profile photo, gender, age, signature, and location. |
| Obtain user profiles | Users can query their own profiles and the profiles of friends and strangers. |
| Obtain user information by fields | This feature can obtain user information based on specific fields. |
| Custom user information | Up to 20 custom user profile fields are supported. |



### Relationship Chain Features

| Feature Type | Description |
| -------------------- | ---------------------- |
| Search for friends | Search for a friend by account ID. |
| Apply to add friends | Specify whether an application reason is required. The default is no. |
| Add friends | Send friend requests. |
| Delete friends | Friends can be deleted after they are added to the contact list. |
| Obtain all friends | This feature can obtain all friends. Only the basic information of friends is pulled by default. |
| Accept/Reject friend requests | Accept or reject a friend request after receiving a friend request system notification. |
| Add to the blacklist | Blacklist any user. If you blacklist friends, you also unfriend them. |
| Remove from the blacklist | Remove a user from the blacklist. |
| Obtain the blacklist | Pull the blacklist of users. |
| Remarks | Add remarks for a friend. |
| Set custom friend profile fields | Up to 20 custom fields can be set. |
| Create a friend group | When creating a group, you can choose group members. A user can be added to multiple groups. |
| Delete a friend group | Delete a friend group. |
| Add a friend to a group | Add a friend to a group. |
| Delete a friend from a group | Remove a friend from a group. |
| Rename a friend group | Rename a friend group. |
| Obtain friend group information | Obtain the information of a specific friend group. |
| Obtain all friend groups | Obtain the information of all friend groups. This can also be achieved by obtaining all friends. |
| Relationship chain storage | The SDK can store relationship chain information. |
| System notifications on friend profile changes | When a friend’s profile changes, you will receive a system notification. |
| System notification on relationship chain changes | When a relationship chain change occurs, you will receive a system notification. |



### Group Features
IM configures the following default group types based on common use cases:
- Work group: is similar to an ordinary WeChat group. After a work group is created, only a group member can invite other users to join this group, and the invitation does not need to be approved by the invitee or group owner.
- Public group: is similar to a QQ group. After a public group is created, the group owner can specify a group admin. When a user searches the group ID and applies to join the group, the application must be approved by the group owner or admin before the user can join the group.
- Meeting group: after a meeting group is created, a user can join and exit the group as desired, and view messages sent before the user joins the group. This group type is suitable for scenarios where Tencent Real-Time Communication (TRTC) is used, for example, audio-and-video conferencing and online education.
- Audio-and-video chat room (AVChatRoom): after an AVChatRoom group is created, a user can join and exit the group as desired. This group type does not limit the number of members, but it does not support the storage of historical messages. It can be used together with Live Video Broadcasting (LVB) to support on-screen comments.

The following table lists the differences between the default features of each group type:

| Feature Type | <div style="width:100px">Work Group </div>(Work) | <div style="width:20%">Public Group </div>(Public) | <div style="width:20%">Meeting Group </div>(Meeting) | <div style="width:20%">Audio-and-video chat room </div>(AVChatRoom) | 
| ---------- | --------------------- | --------------------- | --------------------- | -------------------------- | 
| Maximum Number of Members | 6,000 | 6,000 | 6,000 | No limit |               
| Obtain group member profiles | Show all | Show all | Show all | Show the first 300 group members |
| Set an admin | Not supported | Supported | Supported | Not supported |   
| Group profile modification permissions |<li>Any group member can modify<li>Backend app admin | <li>Group owner<li>Group admin<li>Backend app admin | <li>Group owner<li>Group admin<li>Backend app admin | <li>Group owner <li>Backend app admin | 
| Group disbandment permissions | Backend app admin | <li>Group owner<li>Backend app admin| <li>Group owner<li>Backend app admin | <li>Group owner<li>Backend app admin |
| Exit the group by the group owner | Supported | Not supported | Not supported | Not supported | 
| Apply to join the group | Not supported | Supported. An approval from the group owner or group admin is needed. | Supported. Approval is not needed. | Supported. Approval is not needed. |
| Invite others to the group by a group member | Supported | Not supported | Not supported | Not supported | 
| Member removal permissions | <li>Group owner<li>Backend app admin | <li>Group owner<li>Group admin<li>Backend app admin | <li>Group owner<li>Group admin<li>Backend app admin | Members cannot be removed. The muting feature can be used for fulfilling the same purpose. | 
| Muting permissions | Not supported | <li>Group owner<li>Group admin (can only mute ordinary members)<li>Backend app admin | <li>Group owner<li>Group admin (can only mute ordinary members)<li>Backend app admin | <li>Group owner<li>Backend app admin |   
| View historical messages sent before the member joined the group by a group member | Not supported | Not supported | Supported | Not supported |
| Member change notification (for joining the group, exiting the group, or other changes) | For all members | For all members | For none | For all members | 
| Message activation after group creation | Needed | Not needed | Not needed | Not needed | 
| Unread message counting | Supported | Supported | Not supported | Not supported | 
| Import groups (group members, basic profiles, and others) | Supported | Supported | Supported | Not supported | 



### IM Console

You can log in to the Tencent Cloud [IM console](https://console.cloud.tencent.com/im) to configure the app based on your needs.

| Feature Type | Description |
| -------------- | ------------------------ |
| Create an app | Create an app |
| Download the SDK | Download the client SDK |
| App configuration | Configure apps |
| Statistics | View operational data |
| View crashes | View reported errors |
| Callback configuration | Configure third-party callbacks |
| Feature configuration | Add custom fields and online instances |
| Developer tool | Generate UserSig on the webpage |



### Statistics

The [Statistics and Analytics](https://console.cloud.tencent.com/im) feature in the IM console allows you to view operational data in various dimensions.

| Statistic Type | Description |
| ---------------- | -------------------------------- |
| Active users | Number of users that have connected to and interacted with the server (de-duplicated) |
| New sign-ups | Number of newly registered IDs |
| Total sign-ups | Query the total number of registered users. |
| Upstream messages | Specify a time period and query the number of upstream messages within the period. |
| Message senders | Specify a time period and query the number of message senders within the period. |
| Peak concurrent online users | Specify a time period and query the number of concurrent online users within the period. |
| One-to-one chat upstream messages | Specify a time period and query the number of one-to-one chat upstream messages within the period. |
| One-to-one chat message senders | Specify a time period and query the number of one-to-one chat message senders within the period. |
| Group chat upstream messages | Specify a time period and query the number of group upstream messages within the period. |
| Group chat message senders | Specify a time period and query the number of group message senders within the period. |
| Message sending groups | Specify a time period and query the number of groups that sent messages within the period. |
| New groups | Specify a time period and query the number of new groups within the period. |
| Total groups | Specify a time period and query the total number of groups within the period. |
| Export data | Specify a time period and export data for the period. |
