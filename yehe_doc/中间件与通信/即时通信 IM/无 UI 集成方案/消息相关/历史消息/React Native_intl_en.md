## Feature Description

- The API for pulling historical messages is in the `TencentImSDKPlugin.v2TIMManager.getMessageManager()` class.
- In addition to the support for pulling historical one-to-one and group messages, an advanced API is provided to pull messages by sequence, start point, or time range.
- Both local and cloud historical messages can be pulled.

> ? When historical messages are pulled from the cloud and a network exception is noticed, the SDK will return the locally stored historical messages.

Locally stored historical messages are not subject to time limits, but those stored in the cloud are subject to the following time limits:

- Trial edition: The free storage period is 7 days and cannot be extended.
- Pro edition: The free storage period is 7 days and can be extended.
- Ultimate Edition: The free storage period is 30 days and can be extended.

> ?
>
> - Extending the storage period of historical messages is a value-added service. You can log in to the [IM console](https://console.cloud.tencent.com/im) to modify the relevant configuration. For billing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).
> - Rich media messages (such as images, files, and audios) have the same storage periods as historical messages.

[](id:c2c)

## Pulling Historical One-to-One Messages

Call the `getC2CHistoryMessageList` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/getC2CHistoryMessageList.html)) to get historical one-to-one messages.
When the network is normal, the latest cloud data will be pulled; when it is abnormal, the SDK will return the locally stored historical messages.
If you want to pull only local historical messages, see [Advanced API](#advance).

This API supports paged pull. For more information, see [Paged pull](#advance_page).

Below is the sample code:

```javascript
// Pull historical one-to-one messages
// Set `lastMsgID` to `null` for the first pull
// `lastMsgID` can be the ID of the last message in the returned message list for the second pull.
const userID = "userID";
const count = 10;
const lastMsgID = null;
TencentImSDKPlugin.v2TIMManager
  .getMessageManager()
  .getC2CHistoryMessageList(userID, count, lastMsgID);
```

[](id:group)

## Pulling Historical Group Messages

Call the `getGroupHistoryMessageList` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/getGroupHistoryMessageList.html)) to get historical group messages.
When the network is normal, the latest cloud data will be pulled; when it is abnormal, the SDK will return the locally stored historical messages.
If you want to pull only local historical messages, see [Advanced API](#advance).

This API supports paged pull. For more information, see [Paged pull](#advance_page).

> !
>
> - Only the historical messages of meeting groups (Meeting) can be pulled. For more information on group message limits, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).
> - This API does not apply to audio-video groups (AVChatRoom), as their messages are not stored on the cloud roaming server or in the local database.

Below is the sample code:

```javascript
// Pull historical group messages
// Set `lastMsgID` to `null` for the first pull
// `lastMsgID` can be the ID of the last message in the returned message list for the second pull.
const groupID = "userID";
const count = 10;
const lastMsgID = null;
TencentImSDKPlugin.v2TIMManager
  .getMessageManager()
  .getGroupHistoryMessageList(groupID, count, lastMsgID);
```

## Advanced Feature

[](id:advance)

### Advanced API

If the ordinary API mentioned above cannot meet your needs to pull historical messages, you can use the advanced API `getHistoryMessageList` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/getHistoryMessageList.html)).

In addition to pulling historical one-to-one and group messages, this API supports the following advanced features:

- Set the source for message pull: pull from the local database or the cloud
- Specify the sequence for message pull: pull in reverse chronological order or in chronological order
- Specify the message type for local pull: text, image, audio, video, file, emoji, group tip, merged, or custom message

API prototype:

```typescript
public getHistoryMessageList(
        count: number,
        getType = HistoryMsgGetTypeEnum.V2TIM_GET_LOCAL_OLDER_MSG,
        userID?: string,
        groupID?: string,
        lastMsgSeq = -1,
        lastMsgID?: string,
        messageTypeList?: number[]
    ): V2TimValueCallback<V2TimMessage[]>
```

Parameter description:

| Parameter  | Description                                                  | Valid for One-to-One Chat | Valid for Group Chat | Required | Remarks                                                      |
| ---------- | ------------------------------------------------------------ | ------------------------- | -------------------- | -------- | ------------------------------------------------------------ |
| getType    | Source and sequence of the message pull, which can be set to **local/cloud** and **reverse chronological order/chronological order** respectively. | YES                       | YES                  | YES      | When the pull source is set to the cloud, the local message list and cloud message list will be merged and returned. If there is no network connection, the local message list will be returned. |
| userID     | The specified user ID with which to pull historical one-to-one messages | YES                       | <b>NO</font>         | NO       | To pull one-to-one messages, you need to specify only the `userID`. |
| groupID    | The specified group ID with which to pull historical group messages | <b>NO</font>              | YES                  | NO       | To pull group messages, you need to specify only the `groupID`. |
| count      | Number of messages per pull                                  | YES                       | YES                  | YES      | We recommend you set it to `20`; otherwise, the pull speed may be affected. |
| lastMsgID  | ID of the last message, indicating the message starting from which to pull historical messages | YES                       | YES                  | NO       | 1. It can be used for both one-to-one and group chats.<br/>2. If it is set as the start point for the message pull, the message will **not be included** in the returned message list.<br/>3. If it is left empty, the latest message in the conversation will be used as the start point for pull. |
| lastMsgSeq | `seq` of the last message, indicating the message starting from which to pull historical messages | <b>NO</font>              | YES                  | NO       | 1. It can be used only for group chats.<br/>2. If it is set as the start point for the message pull, the message will be **included** in the returned message list.<br/>3. If both `lastMsg` and `lastMsgSeq` are specified, the SDK will use `lastMsg`.<br/>4. If neither `lastMsg` nor `lastMsgSeq` is specified, the start point for pull will be determined based on whether the `getTimeBegin` is set. If yes, the set range will be used as the start point; if no, the latest message will be used as the start point. |

[](id:advance_page)

### Paged pull

[Historical one-to-one message pull](#c2c), [historical group message pull](#group), and [pull via the advanced API](#advance) can all be paged by using `lastMsg` and `count`.

- Paged pull can be implemented by using `lastMsg` and `count`. For the first pull, `lastMsg` can be left empty, which indicates that the last message in the returned message list will be used as the `lastMsg` to pull data of the next page.
- When `lastMsg` is left empty, the SDK will return historical messages starting from the latest message by default.
- When `lastMsg` is set, it is not included in the returned message list.
- The returned message list displays messages in reverse chronological order.

> ?
>
> 1. To avoid affecting the speed of pulling historical messages, we recommend you set `count` to `20` for pagination.
> 2. We recommend you not use `lastMsgSeq` for the subsequent pull, as the corresponding message will be included in the returned message list.

### Pulling only local messages

Set `getType` to pull only local messages:

- When `getType` is set to `V2TIM_GET_LOCAL_OLDER_MSG`, locally stored messages will be pulled in reverse chronological order.
- When `getType` is set to `V2TIM_GET_LOCAL_NEWER_MSG`, locally stored messages will be pulled in chronological order.

The following sample code demonstrates the process of pulling 20 one-to-one messages from the local database in reverse chronological order, starting from the latest message:

```javascript
const count = 10;
const getType = HistoryMsgGetTypeEnum.V2TIM_GET_LOCAL_OLDER_MSG;
const userID = "userID";
TencentImSDKPlugin.v2TIMManager
  .getMessageManager()
  .getHistoryMessageList(count, getType, userID);
```

[](id:advance_group_at)

### Pulling messages after redirecting to the group @ message

After a user receives a group @ message in a group conversation, the user generally needs to click the @ bar to go to the message and pull the neighboring messages for display.
As the group @ message also needs to be displayed, you can set its `sequence` as the `lastMsgSeq` and use the [advanced API](#advance) to pull messages.

The following sample code demonstrates the process of clicking the @ bar, redirecting to the group @ message, and pulling the first 20 messages earlier and later than that message for display:

```javascript
// Get the `sequence` of the group @ message
const atSequence = 1081;

// Pull the group @ message and earlier messages

const count = 20;
const getType = HistoryMsgGetTypeEnum.V2TIM_GET_LOCAL_OLDER_MSG;
const lastMsgSeq = atSequence;
const userID = "";
const groupID = "groupID";
  TencentImSDKPlugin.v2TIMManager.getMessageManager().getHistoryMessageList(
        count, // Pull 20 messages
        getType, // Pull messages earlier than the group @ message
        userID,
        groupID // Pull group messages
        lastMsgSeq,// Start the pull from the group @ message, which is included in the pull list
      );



// Pull messages later than the group @ message
TencentImSDKPlugin.v2TIMManager.getMessageManager().getHistoryMessageList(
        count, // Pull 20 messages
        HistoryMsgGetTypeEnum.V2TIM_GET_CLOUD_NEWER_MSG, // Pull messages later than the group @ message
        userID,
        groupID // Pull group messages
        lastMsgSeq,// Start the pull from the group @ message, which is included in the pull list
      );
```

[](id:qa)

## FAQs

[](id:qa1)

### 1. What should I do if "total count of request cloud message exceed max limit" is displayed in the log when I am pulling historical messages?

Currently, the SDK policy is as described below:

1. When `getType` is set to pull cloud historical messages and the number of messages to be pulled is set to `x`, the SDK will pull `x` messages from the cloud.
2. The SDK will filter out invalid messages, such as deleted messages and those irrelevant to the current user.
3. If there are too many invalid historical messages in the cloud, the SDK will perform multiple paged pulls.
   To ensure the system stability and robustness, the SDK will perform up to three automatic paged pulls. After this limit is exceeded, the "total count of request cloud message exceed max limit" message will be displayed in the log.

To minimize the impact of such a limit mechanism on the business layer, you can take the following measures to reduce invalid messages:

- You can use online messages, that is, set `onlineUserOnly` to `YES/true` when sending messages.
- For group messages, you can use targeted group messages to specify the receiver.

[](id:qa2)

### 2. What should I do if messages are "lost" during cloud historical message pull?

When `getType` is set to pull cloud historical messages and the number of messages is `count`, the SDK will perform the following operations:

1. Pull `count` messages from the local database.
2. Pull `count` messages from the cloud and filter out invalid messages such as deleted messages. If the number is smaller than `count`, the paged pull will be triggered.
3. Merge local and cloud messages and update information such as the message status.
4. Return `count` messages from the merged message list.

Generally speaking, message loss indicates that too many invalid messages are pulled in step 2, which triggers the [limit mechanism in question 1](#qa1) and leads to an insufficient number of messages actually pulled from the cloud.
We recommend you fix this issue as instructed in [question 1](#qa1). If the issue persists, contact us for assistance.

[](id:qa3)

### 3. What should I do if group member information such as the group name card is not updated in real time when historical messages are pulled?

- When messages are generated, the SDK will update the current group member information such as the group name card and role and store it in the local database.
- When historical group messages are pulled, the SDK will directly return the group member information when the messages were generated and will not update it in real time.

If you want to get the latest group member information, you can use `getGroupMembersInfo` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMGroupManager/getGroupMembersInfo.html)).

[](id:qa4)

### 4. What should I do if I get a lag while pulling historical messages?

The SDK has been optimized for message pull. If a lag occurs, you can reduce the number of pulled messages (`count`). If the issue persists, contact us for assistance.
