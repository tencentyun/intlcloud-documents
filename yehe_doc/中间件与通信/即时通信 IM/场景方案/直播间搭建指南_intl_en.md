As live streaming has become ubiquitous, more and more enterprises and developers are building their own live streaming platforms. During the process, they need to handle complex requirements such as live stream push and pull, live transcoding, live screencapturing, live stream mix, live chat room, live room interaction (like, gift, and co-anchoring), and live room status management. This document takes Tencent Cloud products ([IM](https://console.cloud.tencent.com/im) and [CSS](https://console.cloud.tencent.com/live/livestat)) as examples to describe how to implement a live room, along with possible problems and considerations, giving a glimpse of the live streaming business and requirements.

![](https://qcloudimg.tencent-cloud.cn/raw/91a6136c0b000f0c76b72a890f3e41ac.jpg)



## 1. Preparations

### Creating an Application

To set up a live room in Tencent Cloud, you need to create an IM application in the [console](https://console.cloud.tencent.com/im) as shown below:
![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-081650.png)

### Adding a live push domain and a playback domain

The live streaming feature is required to set up a live room and can be implemented through [CSS](https://console.cloud.tencent.com/live/livestat). You need to add a push domain and a playback domain as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/fb8a00c48c21bd8d8d74b5a83105893d.png)
For detailed directions, see [Adding Your Own Domain](https://intl.cloud.tencent.com/document/product/267/35970).


### Completing basic configuration

The application created during the preparations is the Free edition, which applies only to development. In the production environment, you need to activate the Pro or Ultimate edition as needed. For more information on differences between different editions, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

In live streaming scenarios, you need some extra configurations after creating the application.

#### Calculating the UserSig with a key
In the IM account system, the password required by a user login is calculated by the server with a key provided by IM. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). In the development phase, to avoid holding back development on the client, you can also calculate the `UserSig` in the [console](https://console.cloud.tencent.com/im/tool-usersig) as shown below:
![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-083650.png)

#### Configuring an admin account

During live streaming, an admin may need to send messages to a live room and mute (remove) non-compliant users, which can be done through [IM server APIs](https://intl.cloud.tencent.com/document/product/1047/34621). To call these APIs, you need to [create an IM admin account](https://console.cloud.tencent.com/im/account-management). By default, IM provides an account with the `UserID` of `administrator`. You can also create multiple admin accounts as needed. Note that you can create up to five admin accounts.

#### Configuring the callback address and enabling the callback

To implement lucky draws based on on-screen comments, message statistics collection, sensitive content detection, and other requirements, you need to use the IM callback module, where the IM backend calls back the business backend in certain scenarios. You only need to provide an HTTP API and configure it in the [**Callback configuration**](https://console.cloud.tencent.com/im/callback-setting) module in the console as shown below:

![](https://staticintl.cloudcachetci.com/yehe/backend-news/N73j869_9.png)


### Integrating the client SDK

After completing the preparations, you need to integrate the IM and CSS client SDKs into your project. You can select an integration option as needed.
For IM integration, see [Instant Messaging](https://www.tencentcloud.com/document/product/1047/34552).
For CSS integration, see [User Guide](https://intl.cloud.tencent.com/document/product/1071/41929).

The following describes common features in a live room and provides best practices with implementation code.

## 2. Live Room Feature Development Guide

### Live room status

A live room has the following statuses:
<table selecttype="cells" ><colgroup><col  ><col  ></colgroup>
<tbody>
<tr  ><th style="width:2%">No.</td>
<th>Live Room Status</td>
</tr>
<tr  ><td>1</td>
<td>To be started</td>
</tr><tr  ><td>2</td>
<td>On live</td>
</tr><tr  ><td>3</td>
<td>Paused</td>
</tr><tr><td>4</td>
<td>Ended</td>
</tr><tr  ><td>5</td>
<td>Played back</td>
</tr></tbody>
</table>
Live room statuses have the following characteristics:
<table selecttype="cells" ><colgroup><col  ><col  ></colgroup>
<tbody>
<tr  ><th style="width:2%">No.</td>
<th>Characteristics</td>
</tr><tr  ><td>1</td>
<td>Users in a live room need to be notified in real time of the change of the live room status.</td>
</tr><tr  ><td>2</td>
<td>Users new to a live room need to get the current status of the live room.</td>
</tr></tbody>
</table>
 

Two implementation schemes are provided, and their pros and cons are as analyzed below.

<table selecttype="cells" ><colgroup><col  ><col  ><col  ></colgroup>
<tbody>
<tr  ><th>Implementation Scheme</td>
<th>Pros</td>
<th>Cons</td>
</tr><tr  ><td>The business backend maintains the live room status and uses the IM server API to send <a href="https://intl.cloud.tencent.com/document/product/1047/34959">custom group messages</a> to notify users of the status.</td>
<td>When the live room status needs to be obtained frequently, storing the status on the business backend reduces the frequency to call the IM SDK, compared to storing the status in the IM group profile.<br>This implementation scheme makes it possible to get the live room status when the IM SDK is not integrated.</td>
<td>The business backend needs to provide an extra module for reading and writing the live room status.<br>Exceptions are more likely to occur when the live room data is obtained, as the data comes from both the business backend and IM group profile.<br>Custom messages may be lost when sent. When there are a large number of messages, low-priority ones will be discarded first, which affects the display of the live room status. Therefore, we recommend you use high-priority custom messages.</td>
</tr><tr  ><td>You can store the live room status through a custom group field or group attribute and notify group users through the <a href="https://intl.cloud.tencent.com/document/product/1047/48175">callback for group attribute change</a> of the client SDK.</td>
<td>You don't need to provide an extra module for reading and writing the live room status.<br>Theoretically, the callback for group attribute change won't be lost.<br>Live room data is obtained from the group profile, which serves as a unified data source that reduces exceptions.</td>
<td>You need to get the group profile frequently in the high-exposure module, which increases the pressure on IM.<br>If the IM SDK module is not integrated, you need to call the IM server SDK on the business backend to get the group profile, and the number of calls is limited.</td>
</tr></tbody>
</table>


Based on the analysis above, we recommend you combine the two schemes to maintain the live room status:

1. In the live room, use scheme 1 to get the live room status.
2. Outside the live room, use scheme 2 to get the live room status.
3. After the live room status changes on the business backend, use the [IM server API](https://intl.cloud.tencent.com/document/product/1047/34621) to promptly sync the data to the IM group profile ([group attribute](https://intl.cloud.tencent.com/document/product/1047/44188) and [custom group field](https://intl.cloud.tencent.com/document/product/1047/34962)).

### Group type selection

The user chat section in live streaming scenarios has the following characteristics:

1. Users join and leave a group frequently, and group conversation information (unread count and `lastMessage`) doesn't need to be managed.
2. Users can join a group without approval.
3. Users send messages without caring about the chat history.
4. There are usually a large number of group members.
5. Group member information doesn't need to be stored.

Therefore, you can select **audio-video groups (AVChatRoom)** as the **Group type** for the live room based on the [group characteristics](https://intl.cloud.tencent.com/document/product/1047/33529) of IM.

IM audio-video groups (AVChatRooms) have the following features:
- **Support interactive live streaming scenarios with unlimited group members.**
- Messages (group system notifications) can be pushed to all online members.
- Users can enter the group directly with no admin approval required.

>? The IM SDK for web allows users to join only one audio-video group (AVChatRoom) at a time. If a user logs in to an client and enters live room A, multi-client login is enabled in the [console](https://console.cloud.tencent.com/im/login-message), and the user logs in to another client and enters live room B, the user will be removed from live room A.

### Live room notice

The live room notice (topic) is necessary for each live room and can be seen by users after entering the room. In addition, audio-video group members need to be notified of notice changes in real time. You can store the live room notice on the business backend or in the IM group profile, just like the live room status; however, there are some additional things that require your attention:

1. The **Group Introduction** and **Group notice** fields of the **Group Profile** can contain up to **240** and **300** bytes, respectively.
2. The **Group Introduction** and **Group notice** fields of the **Group Profile` support only the string type. To create a notice with images and text, you can use the JSON string type, and the images must be accessible online URLs.
3. If a notice is set through the editor on the web, more specifically, it contains the HTML tag, it may be not parsed on the Native.

The live room notice can be set through the [server APIs](https://intl.cloud.tencent.com/document/product/1047/34620) or the group attribute in the client SDK. The client gets the current group information through the group attribute and listens for `OnGroupInfoChange` in `GroupListener` to get the changed group attribute.

Sample code:

<dx-tabs>
 ::: Android
```java
// Get the group profile from the client
V2TIMManager.getGroupManager().getGroupsInfo(groupIDList, new V2TIMValueCallback<List<V2TIMGroupInfoResult>>() {
  @Override
  public void onSuccess(List<V2TIMGroupInfoResult> v2TIMGroupInfoResults) {
      // Obtained the group profile successfully
  }

  @Override
  public void onError(int code, String desc) {
      // Failed to obtain the group profile
  }
});
// Modify the group profile on the client
V2TIMGroupInfo v2TIMGroupInfo = new V2TIMGroupInfo();
v2TIMGroupInfo.setGroupID("Group ID of the group to be modified");
v2TIMGroupInfo.setFaceUrl("http://xxxx");
V2TIMManager.getGroupManager().setGroupInfo(v2TIMGroupInfo, new V2TIMCallback() {
  @Override
  public void onSuccess() {
      // Modified the group profile successfully
  }

  @Override
  public void onError(int code, String desc) {
      // Failed to modify the group profile
  }
});
```

::: 

::: iOS and macOS

```swift
[[V2TIMManager sharedInstance] getGroupsInfo:@[@"groupA"] succ:^(NSArray<V2TIMGroupInfoResult *> *groupResultList) {
    // Obtained the group profile successfully
} fail:^(int code, NSString *desc) {
    // Failed to obtain the group profile
}];
V2TIMGroupInfo *info = [[V2TIMGroupInfo alloc] init];
info.groupID = @"Group ID of the group to be modified";
info.faceURL = @"http://xxxx";
[[V2TIMManager sharedInstance] setGroupInfo:info succ:^{
    // Modified the group profile successfully
} fail:^(int code, NSString *desc) {
    // Failed to modify the group profile
}];
```

:::

::: Flutter

```dart
// Get the group profile
V2TimValueCallback<List<V2TimGroupInfoResult>> groupinfos = await groupManager.getGroupsInfo(groupIDList: ['groupid1']);
// Modify the group profile
groupManager.setGroupInfo(info: V2TimGroupInfo.fromJson({
    "groupAddOpt":GroupAddOptTypeEnum.V2TIM_GROUP_ADD_AUTH
    // ...Other profiles
  }));
// Callback
TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: V2TimGroupListener(onGroupInfoChanged: ((groupID, changeInfos) {
    // The group information was changed.
  })));
```

:::

::: Web 

```js
// Get the group profile
let promise = tim.getGroupProfile({ groupID: 'group1', groupCustomFieldFilter: ['key1','key2'] });
promise.then(function(imResponse) {
  console.log(imResponse.data.group);
}).catch(function(imError){
  console.warn('getGroupProfile error:', imError); // Error information
});
// Modify the group profile
let promise = tim.updateGroupProfile({
  groupID: 'group1',
  name: 'new name', // Modify the group name
  introduction: 'this is introduction.', // Modify the group introduction
  // Starting from v2.6.0, group members can receive group messages about group custom field modifications and obtain related content. For more information, see Message.payload.newGroupProfile.groupCustomField.
  groupCustomField: [{ key: 'group_level', value: 'high'}] // Modify the group custom field
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // Detailed group profile after modification
}).catch(function(imError){
  console.warn('updateGroupProfile error:', imError); // Error information
});
// Starting from v2.6.2, the SDK supports muting and unmuting all. Currently, when all users are muted in a group, group notifications cannot be delivered.
let promise = tim.updateGroupProfile({
  groupID: 'group1',
  muteAllMembers: true, // `true`: mute all; `false`: unmute all
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // Detailed group profile after modification
}).catch(function(imError){
  console.warn('updateGroupProfile error:', imError); // Error information
});
```

:::
</dx-tabs>

See the sample code for group profile processing in other SDKs [here](https://intl.cloud.tencent.com/document/product/1047/48185).

### Message priority

A live room features a large number of user messages. Each user may frequently send messages. When the number of messages sent reaches the IM frequency control threshold, the IM backend will discard some messages to ensure the system running stability. It's necessary to apply such a threshold, as messages are less readable when the client receives too many of them.

Group messages are divided into three levels by priority. The backend delivers high-priority messages first. Therefore, select appropriate priorities according to the importance of messages.
The following lists the priorities from high to low:

| Priority | Description     |
| -------- | --------------- |
| High     | High priority   |
| Normal   | Medium priority |
| Low      | Low priority    |

Messages are discarded according to the following policy:

Number-based frequency control limits the maximum number of messages sent per second in a single group. The default value is 40 messages per second. When the number of sent messages exceeds the limit, the backend will first deliver higher-priority messages, with messages with the same priority delivered randomly.

A message that has been restricted by frequency control is not delivered or stored in the message history, but a success response will be returned to the sender. [Callback before delivering group message](https://intl.cloud.tencent.com/document/product/1047/34374) is triggered, but [callback after delivering group message](https://intl.cloud.tencent.com/document/product/1047/34375) is not triggered.

Therefore, it's necessary to set message priorities for a live room.

Live room messages are prioritized based on their importance as follows:

1. Reward and gift messages that are supposed to be seen by all users.
2. Text, audio, and image messages.
3. Like messages.

>? In general, messages sent by client users are displayed on the screen regardless of their priority. When there are a large number of messages, it's acceptable for users to lose a small number of messages from other users.

Sample code for setting message priorities:
<dx-tabs>
::: Android

```java
// Create a custom message
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createCustomMessage("Custom one-to-one message".getBytes());
// Set the message priority to high
v2TIMMessage.setPriority(V2TIMMessage.V2TIM_PRIORITY_HIGH)
// Send the message
V2TIMManager.getMessageManager().sendMessage(v2TIMMessage, "receiver_userID", null, V2TIMMessage.V2TIM_PRIORITY_NORMAL, false, null, new V2TIMSendCallback<V2TIMMessage>() {
    @Override
    public void onProgress(int progress) {
        // The progress is not called back for the custom message.
    }

    @Override
    public void onSuccess(V2TIMMessage message) {
        // The custom group message sent successfully
    }

    @Override
    public void onError(int code, String desc) {
        // Failed to send the custom group message
    }
});
```

:::

::: iOS and macOS

```swift
// Create a text message
V2TIMMessage *message = [[V2TIMManager sharedInstance] createTextMessage:@"content"];
// Send the message
[V2TIMManager.sharedInstance sendMessage:message
                                receiver:@"userID"
                                 groupID:nil
                                priority:V2TIM_PRIORITY_NORMAL
                          onlineUserOnly:NO
                         offlinePushInfo:nil
                                progress:nil
                                succ:^{
    // The text message sent successfully
}
                                fail:^(int code, NSString *desc) {
    // Failed to send the text message
}];
```

:::

::: Flutter

```dart
// Create a text message
V2TimValueCallback<V2TimMsgCreateInfoResult> createTextAtMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createTextAtMessage(
    text: "test",
    atUserList: [],
  );
 if(createTextAtMessageRes.code == 0){
    String id =  createTextAtMessageRes.data.id;

       // Send the text message
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(id: id, receiver: "", groupID: "groupID");
    if(sendMessageRes.code == 0){
      // The message sent successfully
    }
  }
```

:::

::: Web

```js
// Send the text message
// 1. Create a message instance. The returned instance can be displayed on the screen.
let message = tim.createTextMessage({
  to: 'user1',
  conversationType: TIM.TYPES.CONV_C2C,
  // Message priority, which applies to group chats and is supported by v2.4.2 or later. If messages in a group exceed the frequency limit, the backend will deliver high-priority messages first. For more information, see https://cloud.tencent.com/document/product/269/3663#.E6.B6.88.E6.81.AF.E4.BC.98.E5.85.88.E7.BA.A7.E4.B8.8E.E9.A2.91.E7.8E.87.E6.8E.A7.E5.88.B6.
  // Enumerated values supported: TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL (default), TIM.TYPES.MSG_PRIORITY_LOW, TIM.TYPES.MSG_PRIORITY_LOWEST
  // priority: TIM.TYPES.MSG_PRIORITY_NORMAL,
  payload: {
    text: 'Hello world!'
  },
  // The read receipt feature is supported for one-to-one messages by v2.20.0 or later. To use it, purchase the Ultimate edition package and set `needReadReceipt` to `true` when creating a message.
  needReadReceipt: true
  // Message custom data (saved in the cloud, will be sent to the peer end, and can still be pulled after the app is uninstalled and reinstalled; supported from v2.10.2)
  // cloudCustomData: 'your cloud custom data'
});
// 2. Send the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // The message sent successfully
  console.log(imResponse);
}).catch(function(imError){
  // The message failed to be sent
  console.warn('sendMessage error:', imError);
});
```

:::
</dx-tabs>

See the sample code for message priority setting in other SDKs [here](https://intl.cloud.tencent.com/document/product/1047/47994).

### Best practices for gift and like messages

![](https://qcloudimg.tencent-cloud.cn/raw/5c7b5b56d78df30840ff9b0ddad00467.jpg)

#### Gift message

1. Non-persistent connection requests from the client are sent to the business server, which involves the billing logic.
2. After fees are incurred, the sender can see that XXX sent the XXX gift (so that the sender can see the gift sent by himself/herself; when there are a large number of messages, the policy for discarding messages may be triggered).
3. After the fees are settled, you can call the server API to send the custom message (gift).
4. If multiple gifts are sent in a row, you need to merge the messages.
   1. If the number of gifts is selected in advance, for example, 99, you can send a message with `99` included in the parameter.
   2. If gifts are sent multiple times and the total number is uncertain, you can send a message for every 20 gifts (the value can be adjusted) or the clicks within a second. For example, if 99 gifts are clicked in a row, only five messages need to be sent after the optimization.

#### Like message

1. Unlike a gift message, a like message is not billed and directly sent on the client.
2. For like messages that need to be counted on the server, after traffic throttling is performed on the client, likes on the client are counted, and like messages within a short period of time are merged into one. The business server gets the like count in the callback before sending a message.
3. For like messages that don't need to be counted, the logic in step 2 is used, where the business server sends a message after traffic throttling is performed on the client and doesn't need to get the count in the callback before sending a message.

### Identity and level of a live room user

The concept of user level applies to most of the live rooms. You can determine a weighted user level based on the following:

1. Online duration of the live room user
2. The number of ordinary messages successfully sent by the live room user
3. The number of likes and gifts of sent by the live room user
4. Whether the user has membership privilege of the live room
5. ...

For online duration and the number of messages, you need to use the IM callbacks, which can be configured as instructed in the preparations. Callbacks in the [console](https://console.cloud.tencent.com/im/callback-setting) are as shown below:
![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-083830.png)

The flowchart for information collection is as shown below:
![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-091055.png)


Sample data of the callback after sending a message:

```json
{
    "CallbackCommand": "Group.CallbackAfterSendMsg", // Callback command
    "GroupId": "@TGS#2J4SZEAEL", // Group ID
    "Type": "Public", // Group type
    "From_Account": "jared", // Sender
    "Operator_Account":"admin", // Request initiator
    "Random": 123456, // Random number
    "MsgSeq": 123, // Sequence number of the message
    "MsgTime": 1490686222, // Time of the message
    "OnlineOnlyFlag": 1, // The value is `1` if it is an online message and `0` (default) if it’s not. For audio-video groups, the value is `0`.
    "MsgBody": [ // Message body. For more information, see the `TIMMessage` message object.
        {
            "MsgType": "TIMTextElem", // Text
            "MsgContent":{
                "Text": "red packet"
            }
        }
    ],
    "CloudCustomData": "your cloud custom data"
}
```

You can identify ordinary, like, and gift messages based on the message type in `MsgBody`. For more information on all the fields, see [Callback After Sending a Group Message](https://intl.cloud.tencent.com/document/product/1047/34375).

Sample data of the callback for the change of the user online status:

```json
{
    "CallbackCommand": "State.StateChange",
    "EventTime": 1629883332497,
    "Info": {
        "Action": "Login",
        "To_Account": "testuser316",
        "Reason": "Register"
    },
    "KickedDevice": [
        {
            "Platform": "Windows"
        },
        {
            "Platform": "Android"
        }
    ]
}
```

You can identify the user online status based on the field in `Info`, so as to count the online duration. For more information on all the fields, see [State Change Callbacks](https://intl.cloud.tencent.com/document/product/1047/34357).

>?In addition, live room popularity is often displayed and used as a criterion for live room recommendation. It is determined in a similar way to user level and can be implemented through the callback system of IM.

### Historical messages in a live room

Historical messages are not stored by default for audio-video groups (AVChatRoom). When a new user enters the live room, the user can only see messages sent after the entry. To optimize the user experience, you can configure the number of historical messages that can be pulled as shown below:
![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-085957.png)



>? This feature is available only for the Ultimate edition, and up to 20 historical messages in the past 24 hours can be pulled.

Historical messages in audio-video groups are pulled in the same way as others. Sample code:
<dx-tabs>
::: Android

```java
V2TIMMessageListGetOption option = new V2TIMMessageListGetOption();
option.setGetType(V2TIMMessageListGetOption.V2TIM_GET_CLOUD_OLDER_MSG); // Pull older cloud messages
option.setGetTimeBegin(1640966400);         // Start from 2022-01-01 00:00:00
option.setGetTimePeriod(1 * 24 * 60 * 60);  // Pull the messages of the whole day
option.setCount(Integer.MAX_VALUE);         // Return all the messages within the time range
option.setGroupID(#you group id#);          // Pull group messages
V2TIMManager.getMessageManager().getHistoryMessageList(option, new V2TIMValueCallback<List<V2TIMMessage>>() {
    @Override
    public void onSuccess(List<V2TIMMessage> v2TIMMessages) {
        Log.i("imsdk", "success");
    }

    @Override
    public void onError(int code, String desc) {
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```

::: 

::: iOS and macOS

```swift
// Pull historical one-to-one messages
// Set `lastMsg` to `nil` for the first pull
// `lastMsg` can be the last message in the returned message list for the second pull.
[V2TIMManager.sharedInstance getC2CHistoryMessageList:#your user id# count:20 lastMsg:nil succ:^(NSArray<V2TIMMessage *> *msgs) {
    // Record the `lastMsg` for the next pull
    V2TIMMessage *lastMsg = msgs.lastObject;
    NSLog(@"success, %@", msgs);
} fail:^(int code, NSString *desc) {
    NSLog(@"fail, %d, %@", code, desc);
}];
```

::: 

::: Flutter

```dart
// Pull historical one-to-one messages
// Set `lastMsgID` to `null` for the first pull
// `lastMsgID` can be the ID of the last message in the returned message list for the second pull.
TencentImSDKPlugin.v2TIMManager.getMessageManager().getC2CHistoryMessageList(
        userID: "userId",
        count: 10,
        lastMsgID: null,
);
```

::: 

::: Web

```js
/ Pull the message list for the first time when a conversation is opened.
let promise = tim.getMessageList({conversationID: 'C2Ctest', count: 15});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // Message list
  const nextReqMessageID = imResponse.data.nextReqMessageID; // This parameter must be passed in for the next pulling by page.
  const isCompleted = imResponse.data.isCompleted; // It indicates whether all messages have been pulled.
});
// Pull down to see more messages.
let promise = tim.getMessageList({conversationID: 'C2Ctest', nextReqMessageID, count: 15});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // Message list
  const nextReqMessageID = imResponse.data.nextReqMessageID; // This parameter must be passed in for the next pulling by page.
  const isCompleted = imResponse.data.isCompleted; // It indicates whether all messages have been pulled.
});
```

::: 
</dx-tabs>

See the sample code for historical message pulling in other SDKs [here](https://intl.cloud.tencent.com/document/product/1047/47998).

### Number of online users in a live room

Displaying the number of online users in a live room is a common feature. There are two implementation schemes, each with pros and cons.

1. Pull the number of online users in a group in a scheduled polling way through the [getGroupOnlineMemberCount](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a56840105a4b3371eeab2046d8c300bce) API provided by the client SDK.
2. Deliver the data to all group members through the server API, such as [group system notification](https://intl.cloud.tencent.com/document/product/1047/34958) or [custom group message](https://intl.cloud.tencent.com/document/product/1047/34959), based on the callback for joining or leaving a group on the backend.

If there is only one live room, it's sufficient to pull the number of online users through the API of the client SDK. If there are multiple live rooms that require a large number of exposure positions to display the number of online users, the second scheme is recommended.

>? Your server can send the message of online user count statistics to the client in a scheduled manner, for example, once every five seconds. However, this will incur extra network overheads if the number of online users in the live room doesn't change sharply. We recommend you update the number by monitoring its change rate.
>
>You can determine the priority of the accuracy and real-timeness of the number of online users in the live room as needed.

The code for getting the number of online users in a live room is as follows:

<dx-tabs>
::: Android

```java
2TIMManager.getGroupManager().getGroupOnlineMemberCount("group_avchatroom", new V2TIMValueCallback<Integer>() {
  @Override
  public void onSuccess(Integer integer) {
      // Obtained the number of online members in the audio-video group (AVChatRoom) successfully
  }

  @Override
  public void onError(int code, String desc) {
      // Failed to obtain the number of online members in the audio-video group (AVChatRoom)
  }
});
```

::: 

::: iOS and macOS

```swift
[[V2TIMManager sharedInstance] getGroupOnlineMemberCount:@"group_avchatroom" succ:^(NSInteger count) {
    // Obtained the number of online members in the audio-video group (AVChatRoom) successfully
} fail:^(int code, NSString *desc) {
    // Failed to obtain the number of online members in the audio-video group (AVChatRoom)
}];
```

::: 

::: Flutter

```dart
groupManager.getGroupOnlineMemberCount(groupID: '');
```

::: 

::: Web

```js
// Get the number of online users in an audio-video group (supported from v2.8.0)
let promise = tim.getGroupOnlineMemberCount('group1');
promise.then(function(imResponse) {
  console.log(imResponse.data.memberCount);
}).catch(function(imError){
  console.warn('getGroupOnlineMemberCount error:', imError); // Error information
});
```

::: 

</dx-tabs>

### Muting a user in a live room

In a live room, you can mute all or a specified user in different scenarios.

In general, the server SDK is used for muting. To mute all, set the `MuteAllMember` field of the group attribute as instructed in [Modifying the Profile of a Group](https://intl.cloud.tencent.com/document/product/1047/34962). To mute a specified user, set the group member attribute as instructed in [Bulk Muting and Unmuting](https://intl.cloud.tencent.com/document/product/1047/34951).

When the live room admin sets group muting on the backend, the client should put the input box of the target user in the disabled status after receiving the callback event; otherwise, the user will receive the message sending failure prompt when sending a message. After the user is unmuted, the client should also put the input box in the enabled status.

Callback code on the client:

<dx-tabs>
::: Android

```java
// Mute the `userB` group member for one minute
V2TIMManager.getGroupManager().muteGroupMember("groupA", "userB", 60, new V2TIMCallback() {
  @Override
  public void onSuccess() {
      // Muted the group member successfully
  }

  @Override
  public void onError(int code, String desc) {
      // Failed to mute the group member
  }
});

// Mute all members
V2TIMGroupInfo info = new V2TIMGroupInfo();
info.setGroupID("groupA");
info.setAllMuted(true);
V2TIMManager.getGroupManager().setGroupInfo(info, new V2TIMCallback() {
  @Override
  public void onSuccess() {
      // Muted all successfully
  }

  @Override
  public void onError(int code, String desc) {
      // Failed to mute all
  }
});

V2TIMManager.getInstance().addGroupListener(new V2TIMGroupListener() {
  @Override
  public void onMemberInfoChanged(String groupID, List<V2TIMGroupMemberChangeInfo> v2TIMGroupMemberChangeInfoList) {
    // Listen for the muting of a group member
    for (V2TIMGroupMemberChangeInfo memberChangeInfo : v2TIMGroupMemberChangeInfoList) {
      // ID of the muted user
      String userID = memberChangeInfo.getUserID();
      // Muting duration
      long muteTime = memberChangeInfo.getMuteTime();
    }
  }

  @Override
  public void onGroupInfoChanged(String groupID, List<V2TIMGroupChangeInfo> changeInfos) {
    // Listen for the muting of all
    for (V2TIMGroupChangeInfo groupChangeInfo : changeInfos) {
      if (groupChangeInfo.getType() == V2TIMGroupChangeInfo.V2TIM_GROUP_INFO_CHANGE_TYPE_SHUT_UP_ALL) {
        // Whether all members are muted
        boolean isMuteAll = groupChangeInfo.getBoolValue();
      }
    }
  }
});
```

::: 

::: iOS and macOS

```swift
// Mute the group member `user1` for one minute
[[V2TIMManager sharedInstance] muteGroupMember:@"groupA" member:@"user1" muteTime:60 succ:^{
    // Muted the group member successfully
} fail:^(int code, NSString *desc) {
    // Failed to mute the group member
}];

// Mute all members
V2TIMGroupInfo *info = [[V2TIMGroupInfo alloc] init];
info.groupID = @"groupA";
info.allMuted = YES;
[[V2TIMManager sharedInstance] muteGroupMember:@"groupA" member:@"user1" muteTime:60 succ:^{
    // Muted all successfully
} fail:^(int code, NSString *desc) {
    // Failed to mute all
}];

[[V2TIMManager sharedInstance] addGroupListener:self];
- (void)onMemberInfoChanged:(NSString *)groupID changeInfoList:(NSArray <V2TIMGroupMemberChangeInfo *> *)changeInfoList {
    // Listen for the muting of a group member
    for (V2TIMGroupMemberChangeInfo *memberChangeInfo in changeInfoList) {
      // ID of the muted user
      NSString *userID = memberChangeInfo.userID;
      // Muting duration
        uint32_t muteTime = memberChangeInfo.muteTime;
    }
}

- (void)onGroupInfoChanged:(NSString *)groupID changeInfoList:(NSArray <V2TIMGroupChangeInfo *> *)changeInfoList {
    // Listen for the muting of all
    for (V2TIMGroupChangeInfo groupChangeInfo in changeInfoList) {
      if (groupChangeInfo.type == V2TIM_GROUP_INFO_CHANGE_TYPE_SHUT_UP_ALL) {
        // Whether all members are muted
        BOOL isMuteAll = groupChangeInfo.boolValue;
      }
    }
}
```

::: 

::: Flutter

```dart
// Mute the group member `userB` for ten minutes
groupManager.muteGroupMember(groupID: '',userID: 'userB',seconds: 10);

// Mute all members
groupManager.setGroupInfo(info: V2TimGroupInfo(isAllMuted: true,groupID: '',groupType: 'Public'));

TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: V2TimGroupListener(onMemberInfoChanged: (groupID, v2TIMGroupMemberChangeInfoList) {
    // The group member information is changed.
  },
  onGroupInfoChanged: (groupID,info){
    // Group profile modification
  }
  ));
```

::: 

::: Web 

```js
tim.setGroupMemberMuteTime(options);
let promise = tim.setGroupMemberMuteTime({
  groupID: 'group1',
  userID: 'user1',
  muteTime: 600 // The user is muted for ten minutes. If the value is set to `0`, the user is unmuted.
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // New group profile
  console.log(imResponse.data.member); // New group member profile
}).catch(function(imError){
  console.warn('setGroupMemberMuteTime error:', imError); // Error information
});
// Set the period for muting a group member in the topic
let promise = tim.setGroupMemberMuteTime({
  groupID: 'topicID',
  userID: 'user1',
  muteTime: 600 // The user is muted for ten minutes. If the value is set to `0`, the user is unmuted.
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // New group profile
  console.log(imResponse.data.member); // New group member profile
}).catch(function(imError){
  console.warn('setGroupMemberMuteTime error:', imError); // Error information
});
// Starting from v2.6.2, the SDK supports muting and unmuting all. Currently, when all users are muted in a group, group notifications cannot be delivered.
let promise = tim.updateGroupProfile({
  groupID: 'group1',
  muteAllMembers: true, // `true`: mute all; `false`: unmute all
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // Detailed group profile after modification
}).catch(function(imError){
  console.warn('updateGroupProfile error:', imError); // Error information
});
```

::: 
</dx-tabs>

See the sample code for group listening in other SDKs [here](https://intl.cloud.tencent.com/document/product/1047/48466).

Note that the change of the group member muting status will not be delivered to the client by default and needs to be configured in the [console](https://console.cloud.tencent.com/im/qun-setting).
![](https://qcloudimg.tencent-cloud.cn/raw/07c6f6e757a2c05358e7d79ac83b7c68.png)

>?Client SDKs do not support user muting in live rooms at the moment. You can use the corresponding server APIs to [mute](https://intl.cloud.tencent.com/document/product/1047/50296) and [unmute](https://intl.cloud.tencent.com/document/product/1047/50297) users.

### Banning a user in a live room

You can call the [banning](https://intl.cloud.tencent.com/document/product/1047/50296) API on the server to kick users out of a live room and ban them from joining for a certain period of time.

[Configuration items in the console](https://console.cloud.tencent.com/im/callback-setting) are as shown below:


>!**You can use the API for kicking users out of a live room to implement the banning feature in the client SDK on 6.6.x or later or the SDK for Flutter on 4.1.1 or later.**

Sample code:

<dx-tabs>
::: Android

```java
List<String> userIDList = new ArrayList<>();
userIDList.add("userB");
V2TIMManager.getGroupManager().kickGroupMember("groupA", userIDList, "", new V2TIMValueCallback<List<V2TIMGroupMemberOperationResult>>() {
  @Override
  public void onSuccess(List<V2TIMGroupMemberOperationResult> v2TIMGroupMemberOperationResults) {
      // Removed the member successfully
  }

  @Override
  public void onError(int code, String desc) {
      // Failed to remove the member
  }
});

V2TIMManager.getInstance().addGroupListener(new V2TIMGroupListener() {
  @Override
  public void onMemberKicked(String groupID, V2TIMGroupMemberInfo opUser,
  List<V2TIMGroupMemberInfo> memberList) {
      // A group member was removed.
  }
});
```

::: 

::: iOS and macOS

```swift
[[V2TIMManager sharedInstance] kickGroupMember:@"groupA" memberList:@[@"user1"] reason:@"" succ:^(NSArray<V2TIMGroupMemberOperationResult *> *resultList) {
    // Removed the member successfully
} fail:^(int code, NSString *desc) {
    // Failed to remove the member
}];

[[V2TIMManager sharedInstance] addGroupListener:self];
- (void)onMemberKicked:(NSString *)groupID opUser:(V2TIMGroupMemberInfo *)opUser memberList:(NSArray<V2TIMGroupMemberInfo *>*)memberList {
    // A group member was removed.
}
```

::: 

::: Flutter

```dart
groupManager.kickGroupMember(groupID: '',memberList: []);
```

::: 

::: Web

```js
tim.deleteGroupMember(options);
```

::: 

</dx-tabs>

#### Filtering the sensitive content in a live room

Filtering the sensitive content in a live room is another important feature, which can be implemented as follows:

1. Bind the callback before sending a group message.
2. Identify the message type based on the callback data and deliver the message data to Tianyu or another third-party detection service.
3. If the message is an ordinary text message, wait for the detection result of Tianyu and return the data packet indicating whether to deliver the message to the IM backend.
4. If the message is a rich media message, return the data packet for delivering the message to the IM backend. After Tianyu returns the async result, if the message is identified as non-compliant, deliver the message change notification through the message editing API or custom group message API. After receiving the notification, the client will block the non-compliant message.

Sample data of the callback before sending a message:

```json
{
    "CallbackCommand": "Group.CallbackBeforeSendMsg", // Callback command
    "GroupId": "@TGS#2J4SZEAEL", // Group ID
    "Type": "Public", // Group type
    "From_Account": "jared", // Sender
    "Operator_Account":"admin", // Request initiator
    "Random": 123456, // Random number
    "OnlineOnlyFlag": 1, // The value is `1` if it is an online message and `0` (default) if it’s not. For audio-video groups, the value is `0`.
    "MsgBody": [ // Message body. For more information, see the `TIMMessage` message object.
        {
            "MsgType": "TIMTextElem", // Text
            "MsgContent":{
                "Text": "red packet"
            }
        }
    ],
    "CloudCustomData": "your cloud custom data"
}
```

You can identify the message type based on the `MsgType` field in `MsgBody`. For more information on the fields, see [Callback Before Sending a Group Message](https://intl.cloud.tencent.com/document/product/1047/34374).

You can choose to handle a non-compliant message in a specific way, which can be implemented through the data packet in the callback returned to the IM backend.

```json
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // Different `ErrorCode` values have different meanings.
}
```



| ErrorCode | Description                                                  |
| --------- | ------------------------------------------------------------ |
| 0         | Speaking is allowed, and messages can be delivered.          |
| 1         | Speaking is denied, and the client returns `10016`.          |
| 2         | Silent discarding is enabled, and the client returns messages normally. |

You can use them as needed.

The flowchart for detecting sensitive content is as shown below:

![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-091347.png)


### Group member list in a live room

You can call the `getGroupMemberList` API to get the list of online group members in a live room for display. As an audio-video group (AVChatRoom) has a large number of members, the feature of pulling the list of all the members is unavailable. The Ultimate edition and non-Ultimate edition differ in settings:

1. A non-Ultimate edition user can call `getGroupMemberList` to pull the latest 30 group members.
2. An Ultimate edition user can call `getGroupMemberList` to pull the latest 1,000 group members. This feature needs to be enabled in the IM console. If it is not enabled, only the latest 30 group members will be pulled, just as in the non-Ultimate edition.

The configuration in the console is as shown below:

![img](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-090445.png)

If you are a non-Ultimate edition user, you can maintain the list of online group members on the client through `getGroupMemberList` and the `onGroupMemberEnter` and `onGroupMemberQuit` callbacks of the group listening. However, after users leave and re-enter the live room, only the latest 30 group members can be pulled.

<dx-tabs>
::: Android

```java
// Use the `filter` parameter to specify only the profile of the group owner is to be pulled
int role = V2TIMGroupMemberFullInfo.V2TIM_GROUP_MEMBER_FILTER_OWNER;
V2TIMManager.getGroupManager().getGroupMemberList("testGroup", role, 0, 
    new V2TIMValueCallback<V2TIMGroupMemberInfoResult>() {
    @Override
    public void onError(int code, String desc) {
        // Messages failed to be pulled
    }

    @Override
    public void onSuccess(V2TIMGroupMemberInfoResult v2TIMGroupMemberInfoResult) {
        // Conversations pulled successfully
    }
});
```

::: 

::: iOS and macOS

```swift
[[V2TIMManager sharedInstance] getGroupMemberList:@"groupA" filter:V2TIM_GROUP_MEMBER_FILTER_OWNER nextSeq:0 succ:^(uint64_t nextSeq, NSArray<V2TIMGroupMemberFullInfo *> *memberList) {
    // Conversations pulled successfully
} fail:^(int code, NSString *desc) {
    // Messages failed to be pulled
}];
```

::: 

::: Flutter

```dart
// Use the `filter` parameter to specify only the profile of the group owner is to be pulled. You can also set `filter` to `All` to pull the profiles of all group members.
groupManager.getGroupMemberList(count: 10,filter: GroupMemberFilterTypeEnum.V2TIM_GROUP_MEMBER_FILTER_ADMIN,nextSeq: '0',offset: 0,groupID: "",);
```

::: 

::: Web

```js
tim.getGroupMemberList(options);

```

::: 

</dx-tabs>

### Lucky draw based on on-screen comments in a live room

Similar to message statistics, lucky draws in live streaming also require the callback after sending a message. Specifically, the message content is detected, and users that hit the keywords of a lucky draw are added to the pool.

### On-screen comments for live video broadcasting
 Audio-video groups (`AVChatRoom`) support on-screen comments, gifts, and like messages to build a friendly interaction experience.
![](https://imgcache.qq.com/open_proj/proj_qcloud_v2/gateway/product/im-new/css/img/scenes/function2.gif)

### Broadcast in a live room

The broadcast feature is similar to a system notice feature in the live room, but it differs from the latter in that it belongs to messaging. When the system admin delivers a broadcast message, all the live rooms under the `SDKAppID` will receive it.

The broadcast feature is currently available only for the Ultimate edition and needs to be enabled in the console.

For detailed directions on how to send a broadcast message on the business backend, see [Broadcast Messaging of Audio-Video Group](https://intl.cloud.tencent.com/document/product/1047/49440).

>?If you are not an Ultimate edition user, you can implement the feature by sending a custom group message on the server.
>

## 3. Live Audio/Video Stream

- ### Anchor (stream push)

  Currently, CSS offers the following ways to push a stream:

  1. [OBS](https://intl.cloud.tencent.com/document/product/267/31569) (client)
  2. [Web Push](https://console.cloud.tencent.com/live/tools/webpush) (web)
  3. [MLVB SDK](https://intl.cloud.tencent.com/document/product/1071/38158) (app)

  >? Before starting stream push, an anchor needs to configure a push address. Refer to [Push Configuration](https://intl.cloud.tencent.com/document/product/267/31059) or [Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator) to generate a push address.

- ### Client (stream pull)

  The client can get live streams in different ways:

  1. [VLC](https://intl.cloud.tencent.com/document/product/267/32483) for PCs
  2. [MLVB SDK](https://intl.cloud.tencent.com/document/product/1071/38160) for the application

  >? You need to configure a playback address to pull a stream, which can be generated as instructed in [Playback Configuration](https://intl.cloud.tencent.com/document/product/267/31058) or through the [Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator). For more information on SDK integration, see [2. Playback](https://www.tencentcloud.com/document/product/267/51155).

- ### Live director

  To meet more requirements for live streaming, you can use the [live director](https://console.cloud.tencent.com/live/caster) to process live streams. Currently, the live director supports the following features:

  1. Watermark, text, and transition
  2. Video on demand to live streaming
  3. Definition, bitrate, and resolution settings for live streaming
  4. Layout adjustment for live streaming
  5. Live recording
  6. Live on-screen comment adding
  7. Live stream monitoring


- ### More advanced features
  
  CSS has the following advanced features in addition to stream push and pull:
  1. [Top speed codec transcoding](https://intl.cloud.tencent.com/document/product/267/31561) is a unique technology which uses smart scenario recognition and dynamic encoding to implement high-definition live streams at a low bitrate and with a higher image quality.
  2. [Time shifting](https://intl.cloud.tencent.com/document/product/267/31565) allows for pausing and rewinding a live stream.
  3. [Live recording](https://intl.cloud.tencent.com/document/product/267/31563) allows for recording and storing live streams for subsequent editing and distribution.
  4. [Live watermarking](https://intl.cloud.tencent.com/document/product/267/31073) adds visible or digital watermarks to live streams to protect video content from theft.
  5. [Live stream mix](https://intl.cloud.tencent.com/document/product/267/37665) synchronously mixes multiple streams of input sources into a new stream based on the configured stream mix layout for interactive live streaming.
  6. [Relay](https://intl.cloud.tencent.com/document/product/267/42524) supports pushing live streams or streaming on-demand videos, that is, pulling content from existing live streams or videos and delivering them to the destination address.
  
## 4. FAQs
### 1. Can I try out CSS?
New users can get 20 GB free traffic valid for one year after activating CSS, and excessive traffic will be billed daily in pay-as-you-go mode. CSS value-added features are disabled by default, such as live watermarking, transcoding, recording, screencapturing, and porn detection. They can be enabled as needed and will be billed afterward. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/267/2822).

### 2. Is there an upper limit on the number of online viewers?
By default, CSS does not limit the number of online viewers for a live stream as long as the network and other conditions permit. However, if you have configured a bandwidth limit, new viewers cannot watch the live stream if there are so many existing viewers that the bandwidth limit is exceeded. In this case, the number of online viewers is limited.

### 3. What should I do to display the nickname and profile photo on the UI when the message sending status, `Message.nick`, and `Message.avatar` fields are empty during message sending?
Call the `getUserInfo` API to get the `Message.nick` and `Message.avatar` fields in the user's information and use them as the fields for message sending.

### 4. Why are messages lost?

Possible causes include the following:

- An audio-video group has the frequency limit of 40 messages per second. You can check whether the callback before sending a message and the callback after sending a message are received for a lost message. If the former is received but the latter is not, then the message has been blocked due to frequency restriction.
- You can check whether a group member quits on the Android, iOS, or PC client after quitting on the web client as instructed in [Message](https://intl.cloud.tencent.com/document/product/1047/34458).
- If a problem occurs on the web client, check whether your SDK version is earlier than v2.7.6; if yes, upgrade it to the latest version.

If the problem persists, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.



## 5. Contact Us

Contact us for more information.
