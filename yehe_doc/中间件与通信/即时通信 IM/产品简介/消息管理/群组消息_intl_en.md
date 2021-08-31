## Application Scenarios
### Sending and receiving messages within a group
Group members can send and receive messages in a group, which is similar to the chat mode of QQ and WeChat groups.

### App admin sends messages
The app admin can send messages from the backend, or simulate users to send messages. In the latter case, even if the app admin or sender is not a group member, the messages will still be delivered.

### App admin simulates system messages
The app admin can simulate system messages by sending messages from the backend. These messages are delivered as system messages to specified online group members, and the app admin’s custom messages that are received on the app can be handled in special ways.

## SEQ Mechanism of Group Messages
Instant Messaging (IM) maintains a message SEQ for each group, which starts from an initial value of 1. Every time an ordinary message is sent in the group chat, the IM backend uses the current SEQ value as the SEQ of the message and then increases the SEQ by 1.
Group ID and SEQ together constitute the unique identifier of a message.

>! IM generates incremental SEQs only for messages that are subject to roaming storage.



### Group message types

| Message Type | Description |
| ------------ | ------------------------------------------------------------ |
| Text | The message content is plain text. |
| Image | The message content includes the URL, dimensions, and size of the image. |
| Emoji | Emoji messages are customized by developers. |
| Audio | Audio data must include the duration in seconds. |
| Location | The message content includes the caption, longitude, and latitude of the location. |
| File | The message content includes the URL, size, and format of the file. There are no file format restrictions, and the maximum supported file size is 100 MB. |
| Short video | The message content includes the URL, duration, size, and format of the short video file. The maximum file size supported is 100 MB. |
| Custom | Message types that are customized by developers, such as red packet and rock-paper-scissor. |
| System notification | This type of message includes built-in system notification messages and system notification messages customized by developers. |


### Group messaging capabilities

| Type | Feature Description | Application Scenario |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Send ordinary group messages | Group members can send messages through the IM SDK APIs. By calling RESTful APIs, app admins can send messages in any group without joining the group. | Group members send messages in the group, and app admins can send messages in any group. |
| Send group system messages | By calling RESTful APIs, app admins can send system messages in any group without joining the group. These system messages are only received by online group members and do not possess roaming capabilities. | App admins push time-sensitive notifications to all or a subset of online group members. |
| Offline push of group messages | Supported by Apple, Huawei, Xiaomi, OPPO, Vivo, and Meizu mobile phones | Offline push of group chat messages |
| Receive online group messages | Group members can receive online group messages through the IM SDK. | Online group members receive group messages in real time. |
| Group members receive offline messages or historical messages | Group members can query message historical messages through the IM SDK. | Group members receive offline messages when they go back online, and group members can view group chat history. |
| App backend obtains group messages | App admins can download all messages generated during a certain time period through RESTful APIs. App admins can also obtain the chat history of any group through RESTful APIs. The app backend can obtain group messages through callback after messages are sent in the group. | Apps back up message history regularly. Apps need to quickly obtain the message history of specific groups. Apps need to obtain group messages in real time. |
| Delete messages | Historical messages can be deleted through RESTful APIs to ensure that they will not be further propagated. | Delete malicious information in a group. |
| Group messages carry sender profiles | Group messages can contain the sender nickname, profile photo, group name card, user-level custom fields, and member-level custom fields. | Display sender information such as the nickname and profile photo. |
| Foul language filtering | When the IM backend detects foul language in a message, it refuses to deliver the message and returns error code 80001 to the sender.<br/>IM configures foul language related to politics and pornography by default. You can also configure custom foul language entries for the app. | Enforce message content filtering. |
| Group message sending control | You can control group message sending by muting and callback before sending group messages. | Prevent a group member from sending messages, prevent all group members from sending messages, and filter or modify messages at the app backend. |
| Group message receiving control | You can set different message receiving options for individual groups: receive and notify, receive without notifying, and block messages. When **receive without notifying** is selected, iOS devices will disable APNs. | A user blocks messages from a group. |
| Group message frequency control | Control the sending frequency of ordinary group messages. The default value is 40 messages per second. Group system messages sent by the app admin through RESTful APIs are not subject to frequency control. For more information, see the message priority and frequency control described below. | Prevent spam messages. |


>! If the sender nickname and profile photo need to be included, import the information in these two fields to user profiles in IM.
> If custom fields need to be included, configure custom fields in the console and submit a ticket to add the corresponding fields to messages.



## Group Message Sending Control

The sending of group messages can be controlled through the following methods:

| Control Method | Description |
| ---------------- | ------------------------------------------------------------ |
| Mute group members | Prevent a group member from sending messages for a certain period of time. This feature is effective within a single group. If the muted user leaves the group and joins again, the user remains muted until the mute time expires. |
| Callback before delivering group messages | Before delivering a message to group members, IM checks with the app backend for permission. If not allowed, the message will not be delivered.<br>After receiving a callback, the app backend can modify the message content and return it to IM, which will deliver the modified message. For more information, see [Callback Before Delivering Group Messages](https://intl.cloud.tencent.com/document/product/1047/34374).<br>After initiating a callback, IM will deliver the message directly if it does not receive a response in 2 seconds, without retrying. |


## Message Priority and Frequency Control
### Group message priority

Group messages are divided into three levels by priority. If a group exceeds the message frequency cap, the backend delivers high-priority messages first. Therefore, select appropriate priorities according to the importance of messages.
The following lists the priorities from high to low:

| Priority | Recommended Message Type |
| ------ | -------------------------- |
| High | Red packet and prize message |
| Normal | Plain text message |
| Low | Like message |

### Group message frequency control

#### Number-based frequency control

>? Number-based frequency control limits the maximum number of messages sent per second in a single group. The default value is 40 messages per second. When the number of sent messages exceeds the limit, the backend will first deliver higher-priority messages, with messages with the same priority delivered randomly.

A message that has been restricted by frequency control is not delivered or stored in the message history, but a success response will be returned to the sender. [Callback before delivering group message](https://intl.cloud.tencent.com/document/product/1047/34374) is triggered, but [callback after delivering group message](https://intl.cloud.tencent.com/document/product/1047/34375) is not triggered.

#### Priority-based frequency control

Priority-based frequency control limits the maximum number of messages with a certain priority sent per second in a single group. A message sending request must first pass the number-based frequency control check before it enters the priority-based frequency control processing.

All messages are subject to the frequency limit of 40 messages per second. You can set 3 levels of priority. Messages with High priority are the top-priority messages, which are not likely to be restricted. However, if the number of high-priority messages sent in a second exceeds 40, high-priority messages will also be discarded.


## Processing of Offline Group Messages
![](https://main.qcloudimg.com/raw/3cffbd86ff1fda0a28221c7700d1718f.png)

#### Offline group messages are processed as follows:
1. User A calls `sendMessage` to send messages to group C when user B is offline.
    1.1 Group C is added to the recent contacts of user B, with up to 100 messages cached.
    1.2 A user updates the message information of the group, including the latest group message seq.
    1.3 Messages are stored on the roaming server for 7 days.
2. User B calls the `login` API to log in to IM.
3. The SDK automatically pulls the seq information of all group messages, including the latest message seq and unread message count.
4. The SDK automatically pulls recent contacts and outputs through the `OnNewMessage` API.
5. Users are notified through the `OnRefresh` API when group message synchronization is completed.
6. Users call `getMessage`, and the SDK automatically pulls the messages from the roaming server.


