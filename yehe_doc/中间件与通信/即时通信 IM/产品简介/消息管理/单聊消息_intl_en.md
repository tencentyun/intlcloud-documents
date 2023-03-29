## Use Cases
- **One-to-one chat on the app**
One-to-one messages are applicable to one-to-one chats on the app, which are similar to the QQ and WeChat chats between two friends.
- **App administrator sends messages**
One-to-one messages can be sent by the app administrator from the backend, or by the app administrator simulating other users.
- **App administrator sends system messages**
The app administrator can send system messages from the backend. These system messages are notifications delivered to users, and custom messages from the app administrator received by the app will be specially handled.

Instant Messaging (IM) provides comprehensive one-to-one messaging capabilities. At the same time, the permission control and extension capabilities of one-to-one messaging provide features such as getting message history, multi-device synchronization, offline message push, and carrying sender profiles in messages.


## One-to-One Message Types

| Message Type | Description |
| ------------ | ------------------------------------------------------------ |
| Text | The message content is plain text. |
| Emoji | Emoji messages are customized by developers. |
| Location | The message content includes the caption, longitude, and latitude of the location. |
| Image | The message content includes the URL, dimensions, and size of the image. The maximum supported image file size is 28 MB. |
| Audio | The message content includes the URL, size, and duration of the audio. The maximum supported audio file size is 28 MB. |
| File | The message content includes the URL, size, and format of the file. All file formats are allowed, and the maximum supported file size is 100 MB. |
| Short video | The message content includes the URL, duration, size, and format of the short video. The maximum supported short-video file size is 100 MB. |
| Custom | Message types that are customized by developers, such as red packet and rock-paper-scissor. |
| System notification | This type of messages is divided into built-in system notification messages and system notification messages customized by developers. |


## One-to-One Messaging Capabilities

| One-to-One Messaging Capability | Description | Use Cases |
| ------------ | ------------------------------- | ------------------------------------------------------------ |
| Send one-to-one messages | One-to-one messages can be sent through the SDK or RESTful API. | One-to-one chat on the app.<br>App administrator sends messages.<br>App administrator sends system messages. |
| Receive one-to-one messages | One-to-one messages can be received through the SDK. | Receive online messages.<br>Receive offline messages.<br>Query historical messages. |


## One-to-One Messaging Permission Control

| One-to-One Messaging Permission Control | Description | Use Cases |
| ---------------------------------- |------------------------------------- | -------------------------------------------------------- |
| Two app users can send one-to-one messages. | Any two strangers can send messages to each other. | Strangers send messages to each other. |
| App administrator sends one-to-one messages. | App administrator can send one-to-one messages to any user. | App administrator simulates other users to send messages.<br>App administrator sends system messages. |
| Only friends are allowed to send messages to each other. | Only friends can send messages to each other. | Friends send messages to each other. |
| Block messages from someone. | You can add a certain user to blocklist to block their messages. | Unfriend someone.<br>Block messages from someone. |


## One-to-One Messaging Extension Capabilities

| One-to-One Messaging Extension Capability | Description | Use Cases |
| ------------------------ | ----------------------------------------------------------- | --------------------------------------- |
| Obtain chat history | Historical messages can be obtained through the SDK or RESTful API. | Obtain real-time chat history.<br>Download message history on a regular basis. |
| Multi-device synchronization | One-to-one messages can be synchronized across devices. | Users synchronize messages across devices. |
| Offline push of one-to-one messages | Support offline message push on Apple, Huawei, Xiaomi, OPPO, vivo, and Meizu mobile phones. | Push messages offline. |
| One-to-one messages carry sender profiles | Sender profiles can be carried by messages. | Display sender information such as the nickname and profile photo. |

## Processing of Offline One-to-One Messages
![](https://main.qcloudimg.com/raw/d28999fa32da4e5e6750f34117e116bb.png)

#### Offline cache and roaming of one-to-one messages:

1. User A calls `sendMessage` to send messages to user B who is offline.
  - User A is added to user B’s recent contacts, with up to 100 messages cached.
  - Messages are stored in the offline cache for 7 days.
  - Messages are stored on the roaming server for 7 days.
2. User B calls the `login` API to log in to IM.
3. The SDK automatically pulls messages from the offline cache and throws them through the `OnNewMessage` API.
4. The SDK automatically pulls recent contacts and throws them through the `OnNewMessage` API.
5. The user is notified through the `OnRefresh` API when message synchronization is completed.
6. The user calls `getMessage`. If local messages are incomplete, the SDK automatically pulls them from the roaming server.

