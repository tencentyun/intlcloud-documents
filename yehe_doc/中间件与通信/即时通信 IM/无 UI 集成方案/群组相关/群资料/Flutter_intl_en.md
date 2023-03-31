## Feature Description
The group profile refers to the information about the group, which can be obtained through the method in the `TencentImSDKPlugin.v2TIMManager.getGroupManager()` core class.

[](id:getGroupsInfo)

## Getting the Group Profile
Call `getGroupsInfo` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getGroupsInfo.html)) to get the group profile. This API supports passing in multiple `groupID` values at a time to batch get group profiles.

Sample code:



```dart
// Get the group profile
V2TimValueCallback<List<V2TimGroupInfoResult>> groupinfos = await groupManager.getGroupsInfo(groupIDList: ['groupid1']);
```

[](id:setGroupInfo)

## Modifying the Group Profile

Call `setGroupInfo` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/setGroupInfo.html)) to modify the group profile.

If you have called `addGroupListener` to add a group event listener in advance, after the group profile is modified, all the group members will receive the `onGroupInfoChanged` callback ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnGroupInfoChangedCallback.html)).

Member roles that can modify the group profile vary by group type as follows:

| Group Type                     | Member Roles Allowed to Modify the **Basic Group Profile** |
| ------------------------------ | ---------------------------------------------------------- |
| Work group (Work)              | All group members                                          |
| Public group (Public)          | Group owner and admin                                      |
| Meeting group (Meeting)        | Group owner and admin                                      |
| Community (Community)          | Group owner and admin                                      |
| Audio-video group (AVChatRoom) | Group owner                                                |

Sample code:


```dart
groupManager.setGroupInfo(info: V2TimGroupInfo.fromJson({
    "groupAddOpt":GroupAddOptTypeEnum.V2TIM_GROUP_ADD_AUTH
    // ...Other profiles
  }));
// Callback
TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: V2TimGroupListener(onGroupInfoChanged: ((groupID, changeInfos) {
    // The group information was changed.
  })));
```



## Setting the Group Message Receiving Option
Any group member can call the `setGroupReceiveMessageOpt` API ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/setGroupReceiveMessageOpt.html)) to change the group message receiving option.

`V2TIMReceiveMessageOpt` has the following options:

| Message Receiving Option                           | Description                                                  |
| -------------------------------------------------- | ------------------------------------------------------------ |
| ReceiveMsgOptEnum.V2TIM_RECEIVE_MESSAGE            | Messages will be received when the user is online, and push notifications will be received when the user is offline. |
| ReceiveMsgOptEnum.V2TIM_NOT_RECEIVE_MESSAGE        | No group messages will be received.                          |
| ReceiveMsgOptEnum.V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE | Messages will be received when the user is online, and no push notifications will be received when the user is offline. |

Different `V2TIMReceiveMessageOpt` options can be used to implement group message notification muting:

**No group messages will be received.**
With the group message receiving option set to `V2TIM_NOT_RECEIVE_MESSAGE`, no group message will be received, and the conversation list will not be updated.

**Group messages will be received but will not be notified to the user, and a badge without the unread count will be displayed on the conversation list UI.**
1. The group message receiving option is set to `V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE`.
2. When the receiver receives a new group message and needs to update the conversation list, it can get the unread count through `unreadCount` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html#unreadcount)) in `V2TIMConversation`.
3. The receiver displays a badge rather than the unread count when identifying the group message receiving option as `V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE` based on the `recvOpt` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Message/V2TimConversation.html#recvopt)) of `V2TIMConversation`.

> ? As this method requires the unread count feature, it applies only to work groups (Work) and public groups (Public).

Sample code:



```dart
// Set the group message receiving option
groupManager.setGroupInfo(info: V2TimGroupInfo.fromJson({
    "groupAddOpt":GroupAddOptTypeEnum.V2TIM_GROUP_ADD_AUTH
    // ...Other profiles
  }));
```
