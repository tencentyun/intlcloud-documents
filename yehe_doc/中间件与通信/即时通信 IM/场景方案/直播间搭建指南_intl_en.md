As live streaming has become ubiquitous, more and more enterprises and developers are building their own live streaming platforms. During the process, they need to handle complex requirements such as live stream push and pull, live chat room, live room interaction (like, gift, and co-anchoring), and live room status management. This document takes Tencent Cloud products ([IM](https://console.cloud.tencent.com/im), [TRTC](https://console.cloud.tencent.com/trtc), and [CSS](https://console.cloud.tencent.com/live/livestat)) as examples to describe how to implement a live room, along with possible problems and considerations, giving a glimpse of the live streaming business and requirements.

![](https://qcloudimg.tencent-cloud.cn/raw/91a6136c0b000f0c76b72a890f3e41ac.jpg)



## 1. Preparations

### Creating an application

To set up a live room in Tencent Cloud, you need to create an IM application in the [console](https://console.cloud.tencent.com/im) as shown below:
![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-081650.png)

### Creating a TRTC or CSS application

In addition to IM features, a live room also relies on the live streaming feature, which can be implemented with [TRTC](https://console.cloud.tencent.com/trtc) or [CSS](https://console.cloud.tencent.com/live/livestat). After creating an IM application, you can activate a TRTC application as shown below:
![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-081714.png)

To use [CSS](https://console.cloud.tencent.com/live/livestat), you can enable stream push and playback domain names as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/fb8a00c48c21bd8d8d74b5a83105893d.png)



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

![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-083718.png)


### Integrating the client SDK

After completing the preparations, you need to integrate the IM and TRTC client SDKs into your project. You can select different integration options as needed. For detailed directions, see [TUIKit Introduction](https://intl.cloud.tencent.com/document/product/1047/34547).

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
<th>Characteristic</td>
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
</tr><tr  ><td>You can store the live room status through a custom group field or group attribute and notify group users through the <a href="https://cloud.tencent.com/document/product/269/75406">callback for group attribute change</a> of the client SDK.</td>
<td>You don't need to provide an extra module for reading and writing the live room status.<br>Theoretically, the callback for group attribute change won't be lost.<br>Live room data is obtained from the group profile, which serves as a unified data source that reduces exceptions.</td>
<td>You need to get the group profile frequently in the high-exposure module, which increases the pressure on IM.<br>If the IM SDK module is not integrated, you need to call the IM server SDK on the business backend to get the group profile, and the number of calls is limited.</td>
</tr></tbody>
</table>


Based on the analysis above, we recommend you combine the two schemes to maintain the live room status:

1. In the live room, use scheme 1 to get the live room status.
2. Outside the live room, use scheme 2 to get the live room status.
3. After the live room status changes on the business backend, use the [IM server API](https://intl.cloud.tencent.com/document/product/1047/34621) to promptly sync the data to the IM group profile ([group attribute](https://intl.cloud.tencent.com/document/product/1047/34962) and [custom group field](https://intl.cloud.tencent.com/document/product/1047/34962)).

### Selecting a group type

The user chat section in live streaming scenarios has the following characteristics:

1. Users join and leave a group frequently, and group conversation information (unread count and `lastMessage`) doesn't need to be managed.
2. Users can join a group without approval.
3. Users send messages without caring about the chat history.
4. There are usually a large number of group members.
5. Group member information doesn't need to be stored.

Therefore, you can select **audio-video groups (AVChatRoom)** as the **Group type** for the live room based on the [group characteristics](https://intl.cloud.tencent.com/document/product/1047/33529) of IM.

IM audio-video groups (AVChatRoom) have the following characteristics:
- **They support interactive live streaming scenarios with an unlimited number of group members.**
- They support pushing messages (group system notifications) to all online members.
- Users can join a group directly with no admin approval required.

>? The IM SDK for web or mini programs allows users to join only one audio-video group (AVChatRoom) at a time. If a user logs in to an client and enters live room A, multi-client login is enabled in the [console](https://console.cloud.tencent.com/im/login-message), and the user logs in to another client and enters live room B, the user will be removed from live room A.

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
      // Group profile got successfully
  }

  @Override
  public void onError(int code, String desc) {
      // Failed to get the group profile
  }
});
// Modify the group profile on the client
V2TIMGroupInfo v2TIMGroupInfo = new V2TIMGroupInfo();
v2TIMGroupInfo.setGroupID("Group ID to be modified");
v2TIMGroupInfo.setFaceUrl("http://xxxx");
V2TIMManager.getGroupManager().setGroupInfo(v2TIMGroupInfo, new V2TIMCallback() {
  @Override
  public void onSuccess() {
      // Group profile modified successfully
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
    // Group profile got successfully
} fail:^(int code, NSString *desc) {
    // Failed to get the group profile
}];
V2TIMGroupInfo *info = [[V2TIMGroupInfo alloc] init];
info.groupID = @"Group ID to be modified";
info.faceURL = @"http://xxxx";
[[V2TIMManager sharedInstance] setGroupInfo:info succ:^{
    // Group profile modified successfully
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
    // Callback for the group information change
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
  console.warn('getGroupProfile error:', imError); // Information of the failure to get the detailed group profile
});
// Modify the group profile
let promise = tim.updateGroupProfile({
  groupID: 'group1',
  name: 'new name', // Modify the group name
  introduction: 'this is introduction.', // Modify the group introduction
  // Starting from v2.6.0, group members can receive group tips about group custom field changes and get the content. For more information, see `Message.payload.newGroupProfile.groupCustomField`.
  groupCustomField: [{ key: 'group_level', value: 'high'}] // Modify the group custom field
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // The successfully modified detailed group profile
}).catch(function(imError){
  console.warn('updateGroupProfile error:', imError); // Information of the failure to modify the group profile
});
// Starting from v2.6.2, the SDK supports muting and unmuting all. Currently, when all members in a group are muted, group tips cannot be delivered.
let promise = tim.updateGroupProfile({
  groupID: 'group1',
  muteAllMembers: true, // true: mute all; false: unmute all
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // The successfully modified detailed group profile
}).catch(function(imError){
  console.warn('updateGroupProfile error:', imError); // Information of the failure to modify the group profile
});
```

:::
</dx-tabs>

See the sample code for the group profile processing module in other SDKs [here](https://intl.cloud.tencent.com/document/product/1047/48185).

### Message priority

A live room features a large number of user messages. Each user may frequently send messages. When the number of messages sent reaches the IM frequency control threshold, the IM backend will discard some messages to ensure the system running stability. It's necessary to apply such a threshold, as messages are less readable when the client receives too many of them.

Group messages have three priorities, and the backend delivers high-priority messages first. Therefore, set different priorities for messages based on their importance.
The following lists the priorities from high to low:

| Priority | Description       |
| ------ | ---------- |
| High   | High priority   |
| Normal | Medium priority |
| Low    | Low priority   |

Messages are discarded according to the following policy:

Frequency control on the total number of messages limits the number of messages that can be sent per second in a group. By default, the value is 40. After the value is exceeded, the backend delivers high-priority messages first and those at the same priority randomly.

A message restricted by frequency control will not be delivered or stored in the message history, but a success response will be returned to the sender. The [callback before speaking in a group](https://intl.cloud.tencent.com/document/product/1047/34374) will be triggered, but the [callback after speaking in a group](https://intl.cloud.tencent.com/document/product/1047/34375) will not.

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
        // Custom group message sent successfully
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
/ Create a text message
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
    // Text message sent successfully
}
                                fail:^(int code, NSString *desc) {
    // Failed to send the text message
}];
```

:::

::: Flutter

```dart
/ Create a text message
V2TimValueCallback<V2TimMsgCreateInfoResult> createTextAtMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createTextAtMessage(
    text: "test",
    atUserList: [],
  );
 if(createTextAtMessageRes.code == 0){
    String id =  createTextAtMessageRes.data.id;

       // Send the text message
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(id: id, receiver: "", groupID: "groupID");
    if(sendMessageRes.code == 0){
      // Message sent successfully
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
  // Message priority, which applies to group chats (supported by v2.4.2 or later). If messages in a group exceed the frequency limit, the backend will deliver high-priority messages first. For more information, visit https://cloud.tencent.com/document/product/269/3663#.E6.B6.88.E6.81.AF.E4.BC.98.E5.85.88.E7.BA.A7.E4.B8.8E.E9.A2.91.E7.8E.87.E6.8E.A7.E5.88.B6.
  // Supported enumerated values: TIM.TYPES.MSG_PRIORITY_HIGH, TIM.TYPES.MSG_PRIORITY_NORMAL (default), TIM.TYPES.MSG_PRIORITY_LOW, TIM.TYPES.MSG_PRIORITY_LOWEST.
  // priority: TIM.TYPES.MSG_PRIORITY_NORMAL,
  payload: {
    text: 'Hello world!'
  },
  // The read receipt feature is supported for one-to-one messages by v2.20.0 or later. To use it, purchase the Ultimate edition package and set `needReadReceipt` to `true` when creating a message.
  needReadReceipt: true
  // Custom message data, which is saved in the cloud, will be sent to the receiver, and can still be pulled after the application is uninstalled and reinstalled. This attribute is supported by v2.10.2 or later.
  // cloudCustomData: 'your cloud custom data'
});
// 2. Send the message.
let promise = tim.sendMessage(message);
promise.then(function(imResponse) {
  // Message sent successfully
  console.log(imResponse);
}).catch(function(imError){
  // Failed to send the message
  console.warn('sendMessage error:', imError);
});
```

:::
</dx-tabs>

See the sample code for setting message priorities in other SDKs [here](https://intl.cloud.tencent.com/document/product/1047/47994).

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
    "OnlineOnlyFlag": 1, // The value is `1` if it is an online message or `0` (default) if it's not. For audio-video groups, the value is `0`.
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
/ Pull the message list for the first time when a conversation is opened
let promise = tim.getMessageList({conversationID: 'C2Ctest', count: 15});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // Message list
  const nextReqMessageID = imResponse.data.nextReqMessageID; // This parameter must be passed in for the next pull by page.
  const isCompleted = imResponse.data.isCompleted; // It indicates whether all messages have been pulled.
});
// Pull down the message list to view more messages
let promise = tim.getMessageList({conversationID: 'C2Ctest', nextReqMessageID, count: 15});
promise.then(function(imResponse) {
  const messageList = imResponse.data.messageList; // Message list
  const nextReqMessageID = imResponse.data.nextReqMessageID; // This parameter must be passed in for the next pull by page.
  const isCompleted = imResponse.data.isCompleted; // It indicates whether all messages have been pulled.
});
```

::: 
</dx-tabs>

See the sample code for pulling historical messages in other SDKs [here](https://intl.cloud.tencent.com/document/product/1047/47998).

### Number of online users in a live room

Displaying the number of online users in a live room is a common feature. There are two implementation schemes, each with pros and cons.

1. Pull the number of online users in a group in a scheduled polling way through the [getGroupOnlineMemberCount](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a56840105a4b3371eeab2046d8c300bce) API provided by the client SDK.
2. Deliver the data to all group members through the server API, such as [group system notification](https://intl.cloud.tencent.com/document/product/1047/34958) or [custom group message](https://intl.cloud.tencent.com/document/product/1047/34959), based on the callback for joining or leaving a group on the backend.

If there is only one live room, it's sufficient to pull the number of online users through the API of the client SDK. If there are multiple live rooms that require a large number of exposure positions to display the number of online users, the second scheme is recommended.

>? Your server can send the message of online user count statistics to the client in a scheduled manner, for example, once every five seconds. However, this will incur extra network overheads if the number of online users in the live room doesn't change sharply. We recommend you update the number by monitoring its change rate.
>
> You can determine the priority of the accuracy and real-timeness of the number of online users in the live room as needed.

### Muting a user in a live room

In a live room, you can mute all or a specified user in different scenarios.

In general, the server SDK is used for muting. To mute all, set the `MuteAllMember` field of the group attribute as instructed in [Modifying the Profile of a Group](https://intl.cloud.tencent.com/document/product/1047/34962). To mute a specified user, set the group member attribute as instructed in [Bulk Muting and Unmuting](https://intl.cloud.tencent.com/document/product/1047/34951).

When the live room admin sets group muting on the backend, the client should put the input box of the target user in the disabled status after receiving the callback event; otherwise, the user will receive the message sending failure prompt when sending a message. After the user is unmuted, the client should also put the input box in the enabled status.

Callback code on the client:

<dx-tabs>
::: Android

```java
V2TIMGroupListener groupListener = new V2TIMGroupListener() {
  // Group member notification, group lifecycle notification, group join request notification, topic event listening callback, etc.
  @Override
  public void onGroupInfoChanged(String groupID, List< V2TIMGroupChangeInfo > changeInfos) {
    // Group profile change
  }
  @Override
  public void onMemberInfoChanged (String groupID, List< V2TIMGroupMemberChangeInfo > v2TIMGroupMemberChangeInfoList) {
    // Group member profile change
  }
  
};
```

::: 

::: iOS and macOS

```swift
V2TIMManager.getInstance().addGroupListener(groupListener);
[[V2TIMManager sharedInstance] addGroupListener:self];

// Group member notification, group lifecycle notification, group join request notification, topic event listening callback, etc.
- (void)onGroupInfoChanged:(NSString *)groupID memberList:(NSArray<V2TIMGroupMemberInfo *>*)memberList {
    // Group profile change
}

- (void)onMemberInfoChanged:(NSString *)groupID member:(V2TIMGroupMemberInfo *)member {
    // Group member profile change
}

```

::: 

::: Flutter

```dart
// Listen for the group join event
 TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: V2TimGroupListener(onGroupInfoChanged: ((groupID, memberList) {
    // Group profile change
},onMemberInfoChanged: ((groupID, memberList) {
    // Group member profile change
})));
```

::: 

::: Web

```js
let onGroupListUpdated = function(event) {
   console.log(event.data);// Array that stores Group instances
};
tim.on(TIM.EVENT.GROUP_LIST_UPDATED, onGroupListUpdated);
```

::: 
</dx-tabs>

See the sample code for group listening in other SDKs [here](https://intl.cloud.tencent.com/document/product/1047/48466).

Note that the change of the group member muting status will not be delivered to the client by default and needs to be configured in the [console](https://console.cloud.tencent.com/im/qun-setting).
![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-090219.png)

>?Currently, audio-video groups (AVChatRoom) don't support delivering the notification of profile change, but you can send [custom messages](https://intl.cloud.tencent.com/document/product/1047/34959) for implementation.

### Removing a user from a live room

Similar to muting users in a live room, you can use a server [API](https://intl.cloud.tencent.com/document/product/1047/34949) to remove a user from a live room. As audio-video groups (AVChatRoom) don't support this API, you need another implementation scheme.

Below is the scheme:

1. The backend sends the custom group message containing the `userID` of the removed user. When many users are removed at a time, pay attention to the message body size and send the messages in batches.
2. The business backend maintains the group join blocklist.
3. The client receives the custom message and parses the `userID`. If its `userID` is identified, it will call the API to leave the group.
4. Configure the callback before group join and detect whether the user requesting to join the group is in the blocklist in step 2.

[Configuration items in the console](https://console.cloud.tencent.com/im/callback-setting) are as shown below:

![](https://markdown-1252238885.cos.ap-guangzhou.myqcloud.com/2022-08-09-090320.png)


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
    "OnlineOnlyFlag": 1, // The value is `1` if it is an online message or `0` (default) if it's not. For audio-video groups, the value is `0`.
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



| ErrorCode | Description                        |
| --------- | --------------------------- |
| 0         | Speaking is allowed, and messages can be delivered.    |
| 1         | Speaking is denied, and the client returns `10016`. |
| 2         | Silent discarding is enabled, and the client returns messages normally.  |

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

### Lucky draw based on on-screen comments in a live room

Similar to message statistics, lucky draws in live streaming also require the callback after sending a message. Specifically, the message content is detected, and users that hit the keywords of a lucky draw are added to the pool.

### Live on-screen comment
 Audio-video groups (AVChatRoom) support on-screen comments, gift, and like messages to build a friendly interaction experience.
![](https://qcloudimg.tencent-cloud.cn/raw/5c854b6e5754167b6fd394072d4bc42a.png)

### Broadcast in a live room

The broadcast feature is similar to a system notice feature in the live room, but it differs from the latter in that it belongs to messaging. When the system admin delivers a broadcast message, all the live rooms under the `SDKAppID` will receive it.

The broadcast feature is currently available only for the Ultimate edition and needs to be enabled in the console.

For detailed directions on how to send a broadcast message on the business backend, see [Broadcast Messaging of Audio-Video Group](https://intl.cloud.tencent.com/document/product/1047/49440).

>?If you are not an Ultimate edition user, you can implement the feature by sending a custom group message on the server.
>

## 3. Live Audio/Video Stream

- ### Anchor (stream push)

  Currently, CSS offers the following ways to push a stream:

  1. [Push via OBS](https://intl.cloud.tencent.com/document/product/267/31569) from the client
  2. [Web push](https://console.cloud.tencent.com/live/tools/webpush) from web
  3. [MLVB SDK](https://www.tencentcloud.com/document/product/1071/38158) from the application
  
>? You need to configure a push address for the anchor to push a stream, which can be generated as instructed in [Push Configuration](https://intl.cloud.tencent.com/document/product/267/31059) or through the [Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator).

- ### Client (stream pull)

  The client can get live streams in different ways:

  1. [VLC Player](https://intl.cloud.tencent.com/document/product/267/32483) from PC
  2. [TXLivePusher SDK](https://www.tencentcloud.com/document/product/1071/41881) from web
  3. [MLVB SDK](https://www.tencentcloud.com/document/product/1071/38158) for the application
  
>? You need to configure a playback address to pull a stream, which can be generated as instructed in [Playback Configuration](https://intl.cloud.tencent.com/document/product/267/31058) or through the [Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator).

- ### Live director

  To meet more requirements for live streaming, you can use the [live director](https://console.cloud.tencent.com/live/caster) to process live streams. Currently, the live director supports the following features:

  1. Watermark, text, and transition
  2. Video on demand to live streaming
  3. Definition, bitrate, and resolution settings for live streaming
  4. Layout adjustment for live streaming
  5. Live recording
  6. Live on-screen comment adding
  7. Live stream monitoring


- ### Live streaming in TRTC

  You can also use TRTC to implement live streaming. It provides more advanced features than CSS, such as:

  1. [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618)
  2. [On-cloud recording and playback](https://intl.cloud.tencent.com/document/product/647/35426)
  3. [CDN relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242)
  4. ...

## 4. FAQs
### 1. What should I do to display the nickname and profile photo on the UI when the message sending status, `Message.nick`, and `Message.avatar` fields are empty during message sending?
Call the `getUserInfo` API to get the `Message.nick` and `Message.avatar` fields in the user's information and use them as the fields for message sending.

### 2. How should I choose between TRTC and CSS?
Live streaming in TRTC features a low latency to facilitate interaction with the anchor, but it's expensive. CSS is cheap but has a high latency.

### 3. Why are messages lost?

Possible causes include the following:

- An audio-video group is subject to the frequency limit of 40 messages per second. You can check whether the callback before sending a message and the callback after sending a message are received for a lost message. If the former is received but the latter is not, then the message has been blocked due to the frequency limit.
- For more information, see [question 4](#p4). Check whether the Android/iOS/PC client exits due to the web client's exit.
- If a problem occurs on the web client, check whether your SDK version is earlier than v2.7.6; if yes, upgrade it to the latest version.

If the problem persists, submit a ticket for assistance.

### 4. Is there an open-source live streaming component that allows for video watching and chatting?

Yes, and its code is open source. For more information, see [TWebLive](https://github.com/tencentyun/TWebLive).


## 5. Contact Us

Join a Tencent Cloud IM group for:

- Reliable technical support
- Product details
- Constant exchange of ideas

Telegram group: [Join now](https://t.me/tencent_imsdk)



