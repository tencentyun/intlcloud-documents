### Supported Platforms

The following platforms can communicate with each other and provide services across devices and platforms.

| Platform | SDK and Compatibility | Demo | Source Code | UI Component |
| ------- | --------------| -------- | -------- | -------- |
| Android | Compatible with JDK 1.6 and Android SDK version 14 and later | Supported | Supported | Supported |
| iOS | Compatible with iOS 8.0 and later | Supported | Supported | Supported |
| Mac | Compatible with OS X 10.10 and later | Supported | Supported | - |
| Windows | C and C++ are included. Compatible with Windows 7, Windows 8 and 8.1, and Windows 10. Both 32-bit and 64-bit programs can be connected. | - | - | - |
| Web | Supports IE 7+ (except for Windows XP and Vista), Chrome 7+, FireFox 3.6+, Opera 12+, and Safari 6+ | Supported | - | - |
| Mini Program | Supported | Supported | - | - |

>Currently, the mini program version of demo only provides the live chat room scenario.


### Global Access

| Feature Type | Description |
| -------------- | -------------- |
| Global access overview | IM provides reliable and secure network connections with global coverage. With its proprietary multi-level optimal addressing algorithm, IM can perform scheduling across the entire network. When terminals log in from outside Mainland China, IM SDK connects to the nearest access nodes. |
| China | South China, North China, East China, Hong Kong, and others |
| Global | Asia: Japan, South Korea, Singapore, India, Thailand, Malaysia, Vietnam, Philippines, UAE<br>Europe: Germany, United Kingdom, France, Russia, Italy, Norway, Spain<br>North America: United States, Canada, Mexico<br>South America: Brazil<br><br>Oceania: Australia<br>Africa: South Africa |


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

>You can configure multi-device login by logging in to [IM Console](https://console.cloud.tencent.com/im) and clicking **App Configuration** for the target application to open the **Feature Configuration** page.

### Message Types

| Message Type | Description |
| ------------ | ----------------- |
| Text | The message content is in plain text. |
| Image | The message content includes image URLs, dimensions, and sizes. |
| Emoji | Emoji messages are customized by developers. |
| Audio | The duration (in seconds) must be provided for audio data. |
| Location | The message content includes the caption, longitude, and latitude of the location. |
| File | The message content includes the URL, size, and format of the file. There are no restrictions on the file format. The maximum supported file size is 28 MB. |
| Short video | The message content includes the URL, duration, size, and format of the short video. The maximum supported file size is 28 MB. |
| Custom | Message types customized by developers, such as red packet and rock-paper-scissor. |
| System notification | This type of message includes built-in system notification messages and system notification messages customized by developers. |



### Message Features

| Feature Type | Description |
| -------- | -------- |
| Download messages | The app admin can obtain all one-to-one or group messages for a specified hour of a specified day through this API. |
| Offline messages | IM supports offline push when a user logs in, the app switches to work in the background, and other users send messages. |
| Roaming messages | When an account is logged in on a new device, roaming messages of the account are synchronized to the new device. Roaming messages are stored for 7 days by default. You can pay to increase the storage period for roaming messages. |
| Multi-device synchronization | Messages are synchronized and received across multiple devices. |
| Historical messages | Both local and cloud historical messages are supported. |
| Recall messages | Recall a message that has been delivered. Messages that were delivered more than 2 minutes ago cannot be recalled. Only one-to-one and group chat messages can be recalled. Messages sent in audio-and-video chat rooms (AVChatRooms) and broadcasting chat rooms (BChatRooms) cannot be recalled. |
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
| Add to the blacklist | Blacklist any user. If you blacklist friends, you also unfriend them. |
| Remove from the blacklist | Remove a user from the blacklist. |
| Obtain the blacklist | Pull the blacklist of users. |
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

| Feature Type | Private Group<br>(Private) | Public Group<br>(Public) | Chat Room<br>(ChatRoom) | Audio-and-Video Chat Room<br>(AVChatRoom) | Broadcasting Chat Room<br>(BChatRoom) |
| ---------- | --------------------- | --------------------- | --------------------- | -------------------------- | ----------------------------- |
| Member limit | 200 | 2,000 | 6,000 | Unlimited | Unlimited |
| Modify the group profile | Group member | Group admin<br>Group owner<br>App admin | Group admin<br>Group owner<br>App admin | Group owner<br>App admin | App admin |
| Member list | Show all | Show all | Show all | Show 300 members | N/A |
| Disband group | App admin | Group owner<br>App admin | Group owner<br>App admin | Group owner<br>App admin | App admin |
| Apply to join | Not supported | Allowed | Allowed | Allowed | Allowed |
| Membership application approval | Not supported | Required | Not required | Not required | Not required |
| Invite to the group | Confirmation by the invitee is not required | Not supported | Not supported | Not supported | Not supported |
| Group owner quits the group | Supported | Not supported | Not supported | Not supported | Not supported |
| Set the admin | Not supported | Supported | Supported | Not supported | Not supported |
| Remove a member | Group owner<br>App admin | Group admin<br>Group owner<br> App admin | Group admin<br>Group owner<br>App admin | Not supported | Not supported |
| View messages from before joining the group | Not supported | Not supported | Supported | Not supported | Not supported |
| Member changes | All members | All members | N/A | All members | N/A |
| Activate a group | Activate through a message | Not Required | Not Required | Not Required | Not Required |
| Mute a member | Not supported | Supported | Supported | Supported | Not supported |
| Unread count | Supported | Supported | Not supported | Not supported | Not supported |
| Import into the group | Supported | Supported | Supported | Not supported | Not supported |



### IM Console

You can log in to Tencent Cloud [IM Console](https://console.cloud.tencent.com/im) to configure the app based on your needs.

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

The [statistics and analytics](https://console.cloud.tencent.com/im) feature in IM Console allows you to view operational data in various dimensions.

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
