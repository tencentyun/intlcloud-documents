TIM is the namespace of the IM Web SDK and provides the create() static method, the [EVENT](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html) event constant, and the [TYPES](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-TYPES.html) type constant.

## IM SDK Concepts

| Concept | Description |
| :--- | :---- |
| Message | A [message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html) indicates the information to be sent. It carries multiple properties, which specify whether you are the sender, the sender account, the message generation time, and others. |
| Conversation | There are two types of [conversations](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Conversation.html): <li>Client to Client (C2C): a one-to-one chat with only two participants.</li><li>GROUP: a group chat with more than two participants. |
| Profile | The [profile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Profile.html) describes the basic information of a user, including the nickname, profile photo URL, personal signature, and gender. |
| Group | A [group](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Group.html) is a communication system for group chats. Multiple types of groups are available: Private, Public, ChatRoom, and AVChatRoom. |
| GroupMember (group member) | [GroupMember](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/GroupMember.html) specifies the basic information of each group member, such as the ID, nickname, group role, and joining time. |
| Group notification | A group notification is generated when an event, such as the addition or deletion of a group member, occurs. You can configure whether to display group notifications to group members.<br/>For more information on group notification types, see [Message.GroupTipPayload](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupTipPayload). |
| Group system message | For example, when a user applies for joining a group, the group admin will receive a system message. After the admin accepts or denies the application, the IM SDK returns the application result to the access terminal, and then the user can view the result on the access terminal.<br/>For more information on the types of group system messages, see [Message.GroupSystemNoticePayload](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupSystemNoticePayload). |
| Message on-screen display | This is the process by which messages, including text and images, are displayed on the computer or mobile phone screen after the user clicks send. |


## Supported Platforms
The IM SDK supports IE 9+, Chrome, WeChat, Mobile QQ, QQ Browser, FireFox, Opera, and Safari.

## Calling Sequence
The IM SDK calls APIs in the following sequence.

| Operation | Value | Description |
| :--- | :---- | :---- |
| Create an SDK instance | TIM.create(options) | Creates an SDK instance (which is usually represented by tim) by using a TIM factory function. |
| Set the log level | tim.setLogLevel(level) | Sets the log level. Logs with lower levels will not be output. |
| Register the plugin | tim.registerPlugin(optoins) | [Cloud Object Storage (COS)](https://intl.cloud.tencent.com/document/product/436/6474) must be registered as the upload plugin of the IM SDK to upload images, files, and other media. |
| Listen for events | tim.on(event, handler) | Listens for events and handles data thrown by the SDK in the handler. |
| Login | tim.login(options) | Messages can be sent and received after login succeeds and the SDK is ready. |
| Create a text message | tim.createTextMessage(options) | Creates text messages. This API returns a message instance that can be immediately displayed on the screen by the access terminal. |
| Send a message | tim.sendMessage(message) | Sends message instances that have been created. |
| Obtain the conversation list | tim.getConversationList() | Obtains the conversation list. The access terminal can then process conversation list data and render the conversation list interface. |
| Obtain the group list | tim.getGroupList() | Obtains the group list. The access terminal can then process group list data and render the group list interface. |
| Obtain the blacklist | tim.getBlacklist() | Obtains the blacklist. The access terminal can then process blacklist data and render the blacklist interface. |
| Obtain the personal profile | tim.getMyProfile() | Obtains the user’s personal profile. The access terminal can then process personal profile data and render the personal profile interface. |
| Logout | tim.logout() | Logs users out. |