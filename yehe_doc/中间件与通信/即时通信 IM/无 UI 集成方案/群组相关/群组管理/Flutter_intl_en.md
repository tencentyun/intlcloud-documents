## Feature Description
The group management feature allows creating a group, joining a group, getting the joined groups, leaving a group, or disbanding a group through methods in the `TencentImSDKPlugin.v2TIMManager.getGroupManager()` core class.

[](id:listener)

## Group Event Listener
In the group management feature as described below, the IM SDK will automatically trigger the group event notification callback, for example, when someone joins or leaves a group.

Call `addGroupListener` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/addGroupListener.html)) to add a group event listener.

To stop receiving group events, call `removeGroupListener` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/removeGroupListener.html)) to remove the group event listener.

> ! You need to set the group event listener in advance to receive group event notifications.

Sample code:


```java
TencentImSDKPlugin.v2TIMManager.setGroupListener(listener: V2TimGroupListener());
```


## Creating a Group
To initialize the group information such as group introduction, group profile photo, and existing group members when creating a group, call the `createGroup` advanced API ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/createGroup.html)), and the `groupID` will be returned in the callback for successful creation.

Sample code:



```dart
// Create a public group and specify group attributes
groupManager.createGroup(
    groupType: "Publich",
    groupName: "groupName",
    notification: "",
    introduction: "",
    faceUrl: "",
    isAllMuted: false,
    isSupportTopic: false,
    addOpt: GroupAddOptTypeEnum.V2TIM_GROUP_ADD_AUTH,
    memberList: [],
);
```

[](id:joinGroup)

## Joining a Group
The method for joining a group may vary by group type as follows:

| Type                           | Method for Joining a Group                                   |
| ------------------------------ | ------------------------------------------------------------ |
| Work group (Work)              | By invitation                                                |
| Public group (Public)          | On request from the user and on approval from the group owner or admin |
| Meeting group (Meeting)        | Free to join                                                 |
| Community (Community)          | Free to join                                                 |
| Audio-video group (AVChatRoom) | Free to join                                                 |

The following describes how to join the groups in an easy-to-hard sequence.

> ! You need to call `addGroupListener` to add a group event listener in advance as instructed in [Group Event Listener](#advance_page) to receive the following group events.

#### Free to join a group
Meeting groups (Meeting), audio-video groups (AVChatRoom), and communities are mainly used for free interaction scenarios, such as online meeting and live show. The process of joining such groups is the simplest:
1. The user calls `joinGroup` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/joinGroup.html)) to join the group.
2. After the user has successfully joined the group, all the group members (including the user) will receive the `onMemberEnter` callback ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnMemberEnterCallback.html)).

Sample code:


```dart
// Join a group
TencentImSDKPlugin.v2TIMManager.joinGroup(groupID: "groupID",message: "hello",groupType: "Public");

// Listen for the group join event
 TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: V2TimGroupListener(onMemberEnter: ((groupID, memberList) {
    // Get the information of the user who joined the group
})));

```


#### Joining a group by invitation
Work groups (Work) are suitable for communication in work environments. The interaction pattern is designed to disable proactive group joining and only allow users to be invited to join the group by group members.
The steps to join a group are as follows:

1. A group member calls `inviteUserToGroup` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/inviteUserToGroup.html)) to invite a user to the group.
2. All the group members (including the inviter) receive the `onMemberInvited` callback ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnMemberInvitedCallback.html)), which can contain some UI tips.

Sample code:


```dart
// Invite the `userA` user to join the `groupA` group
groupManager.inviteUserToGroup(groupID: "groupID",userList:[]);

// Listen for the group invitation event
TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: V2TimGroupListener(onMemberInvited: ((groupID, opUser, memberList) {
    // Get the information of the inviter and the invitee
  })));
```


#### Joining a group on request and on approval
A public group (Public) is similar to the interest group and clan group of QQ. Anyone can join it on request and on approval from the group owner or admin.

The steps to join a group on request and on approval are as follows:
![](https://main.qcloudimg.com/raw/9164de02268e14b178937bbd85465f4f.png)

Description of process:
1. The user calls `joinGroup` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/joinGroup.html)) to request to join the group.

2. The group owner or admin receives the `onReceiveJoinApplication` group join request notification ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnReceiveJoinApplicationCallback.html)) and calls `getGroupApplicationList` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getGroupApplicationList.html)) to get the group join request list.

3. The group owner or admin traverses the group join request list and calls `acceptGroupApplication` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/acceptGroupApplication.html)) to approve a request or `refuseGroupApplication` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/refuseGroupApplication.html)) to reject it.

4. After the request to join the group is approved or rejected, the user will receive the `onApplicationProcessed` callback ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnApplicationProcessedCallback.html)). Here, if `isAgreeJoin` is `true`, the request is approved; otherwise, it is rejected.
   
5. On approval, all the group members (including the user) will receive the `onMemberEnter` callback ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnMemberEnterCallback.html)), notifying the group members that someone joined the group.

Sample code:



```dart
// ******Group owner******//
// 1. The group owner changes the group join option to approval required.
groupManager.setGroupInfo(info: V2TimGroupInfo.fromJson({
    "groupAddOpt":GroupAddOptTypeEnum.V2TIM_GROUP_ADD_AUTH
}));

// 2. The group owner listens for and processes requests to join the group.
TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: V2TimGroupListener(onReceiveJoinApplication: (groupID, member, opReason) async {
    // Get all the requests
    V2TimValueCallback<V2TimGroupApplicationResult> appls  = await groupManager.getGroupApplicationList();
    appls.data.groupApplicationList.forEach((application) {
        // Approve
        groupManager.acceptGroupApplication(groupID: application.groupID, fromUser: application.fromUser, toUser: application.toUser,type: GroupApplicationTypeEnum.values[application.type]);
        // Reject
        groupManager.refuseGroupApplication(groupID: application.groupID, fromUser: application.fromUser, toUser: application.toUser, addTime: application.addTime, type: GroupApplicationTypeEnum.values[application.type]);
    });
  },));
// ******User******//
// 1. The user requests to join the group.
 TencentImSDKPlugin.v2TIMManager.joinGroup(groupID: "groupID",message: "hello",groupType: "Public");

// 2. The user listens for the request review result.
 TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: V2TimGroupListener(
    onApplicationProcessed: ((groupID, opUser, isAgreeJoin, opReason) {
      // The request to join the group is processed.
    }),
    onMemberEnter:(groupID,memberlist){
      // The user joins the group.
    }
  ));
```


The group owner or admin can also call the `setGroupInfo` API ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/setGroupInfo.html)) to change the group join option (`V2TIMGroupAddOpt`) to "no group join" or "no approval required".

`V2TIMGroupAddOpt` has the following options:

| Group Join Option                          | Description                                                  |
| ------------------------------------------ | ------------------------------------------------------------ |
| GroupAddOptTypeEnum.V2TIM_GROUP_ADD_FORBID | No users can join the group.                                 |
| GroupAddOptTypeEnum.V2TIM_GROUP_ADD_AUTH   | Approval from the group owner or admin is required to join the group (default value). |
| GroupAddOptTypeEnum.V2TIM_GROUP_ADD_ANY    | Any user can join the group without approval.                |


## Getting the Joined Groups
Call `getJoinedGroupList` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getJoinedGroupList.html)) to get the list of joined work groups (Work), public groups (Public), meeting groups (Meeting), and communities (Community, which **don't support** the topic feature). Audio-video groups (AVChatRoom) and communities (Community, which **support** the topic feature) are not included in this list.

Sample code:



```dart
// Get the joined groups
V2TimValueCallback<List<V2TimGroupInfo>> groupRes  =await groupManager.getJoinedGroupList();
```

[](id:quitGroup)

## Leaving a Group

Call `quitGroup` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/quitGroup.html)) to leave a group.
The member who left the group will receive the `onQuitFromGroup` callback ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnQuitFromGroupCallback.html)).
Other group members will receive the `onMemberLeave` callback ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnMemberLeaveCallback.html)).

> ! The group owner **cannot** leave a public group (Public), meeting group (Meeting), community, or audio-video group (AVChatRoom) and can only [disband it](#dismiss).

Sample code:



```dart
// Leave a group
TencentImSDKPlugin.v2TIMManager.quitGroup(groupID: "groupID");

 TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: V2TimGroupListener(onMemberLeave: (groupID, member) {
    // Information of the member who left the group
  },));
```


[](id:dismissGroup)

## Disbanding a Group

Call `dismissGroup` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/dismissGroup.html)) to disband a group, and all the group members will receive the `onGroupDismissed` callback ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnGroupDismissedCallback.html)).

If you have allowed automatically disbanding an inactive group on the server, when the group is automatically disbanded by the server, the SDK will receive the `onGroupRecycled` callback ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Callback/OnGroupRecycledCallback.html)).

Sample code:



```dart
// Disband a group
TencentImSDKPlugin.v2TIMManager.dismissGroup(groupID: "groupID");
// Listen for the event
TencentImSDKPlugin.v2TIMManager.addGroupListener(listener: V2TimGroupListener(onGroupDismissed: (groupID, opUser) {
    // The group is disbanded.
  },onGroupRecycled: (groupID, opUser){
    // The group is reclaimed.
  }));
```


## Receiving a Custom Group System Notification
If you call the RESTful API on the server [to send a custom system messages to the group](https://intl.cloud.tencent.com/document/product/1047/34958), the SDK will call back `onReceiveRESTCustomData`.
