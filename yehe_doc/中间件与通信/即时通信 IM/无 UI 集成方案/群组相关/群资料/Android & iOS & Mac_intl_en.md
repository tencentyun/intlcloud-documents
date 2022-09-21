## Feature Description
The group profile refers to the information about the group, such as group ID, group type, custom group field, and the number of joined members. It is saved in the `V2TIMGroupInfo` object, which is created and returned by the IM SDK and cannot be customized.
The methods to get the group profile are in the `V2TIMGroupManager(Android)` / `V2TIMManager(Group)(iOS and macOS)` core class.

[](id:getGroupInfo)
## Getting the Group Profile
Call `getGroupsInfo` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ada614335043d548c11f121500e279154) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a9bca7e5318cfed44335566a783a6b568)) to get the group profile. This API supports passing in multiple `groupID` values at a time to batch get group profiles.

Sample code:

<dx-tabs>
::: Android
```java
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
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] getGroupsInfo:@[@"groupA"] succ:^(NSArray<V2TIMGroupInfoResult *> *groupResultList) {
    // Obtained the group profile successfully
} fail:^(int code, NSString *desc) {
    // Failed to obtain the group profile
}];
```
:::
</dx-tabs>

[](id:setGroupInfo)
## Modifying the Group Profile
Call `setGroupInfo` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad4ceef92975fa00c4a5dddc8f7e1edcf) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#aa9519a479493e56d7920e40aba796144)) to modify the group profile.

If you have called `addGroupListener` to add a group event listener, after the group profile is modified, all the group members will receive the `onGroupInfoChanged` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ac3a88ea430c6dc35845472ed98ad049b) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#abbe2208a234d77364bff697eea503d27)).

Member roles that can modify the group profile vary by group type as follows:

| Group Type | Member Roles Allowed to Modify the Group Profile |
| --- | --- |
| Work group (Work) | All group members |
| Public group (Public)| Group owner and admin |
| Meeting group (Meeting)| Group owner and admin |
| Community (Community)| Group owner and admin |
| Audio-video group (AVChatRoom)| Group owner |

> ! Not all the fields of the group profile `V2TIMGroupInfo` can be modified, but only those writable.

Sample code:
<dx-tabs>
::: Android
```java
// Sample code: Modify the group profile
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
```objectivec
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
</dx-tabs>

[](id:setGroupReceiveMessageOpt)
## Setting the Group Message Receiving Option
Any group member can call the `setGroupReceiveMessageOpt` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a2735427ac22485626aea278a9d465b3e) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a379eeef926e41ec5d48287e7fb55b80a)) to change the group message receiving option. This setting will take effect only for the group member and will not affect the setting of other group members.

`V2TIMReceiveMessageOpt` has the following options:

| Message Receiving Option | Description |
| --- | --- |
| V2TIM_RECEIVE_MESSAGE | Messages will be received when the user is online, and push notifications will be received when the user is offline. |
| V2TIM_NOT_RECEIVE_MESSAGE | No group messages will be received.|
| V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE | Messages will be received when the user is online, and no push notifications will be received when the user is offline.|

Different `V2TIMReceiveMessageOpt` options can be used to implement group message notification muting:

**No group messages will be received.**
With the group message receiving option set to `V2TIM_NOT_RECEIVE_MESSAGE`, no group message will be received, and the conversation list will not be updated.

**Group messages will be received but will not be notified to the user, and a badge without the unread count will be displayed on the conversation list UI.**
1. The group message receiving option is set to `V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE`.
2. When the receiver receives a new group message and needs to update the conversation list, it can get the unread count through `unreadCount` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#ab6a7667ac8a9f7a17a38ee8e7caec98e) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a816b83eb32d84ea5345f14ced92bb7f6)) in `V2TIMConversation`.
3. The receiver displays a badge rather than the unread count when identifying the group message receiving option as `V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE` based on the `recvOpt` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversation.html#a82f673186669d31f7acd38c52d412ba2) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMConversation.html#a851651878491c64d73aa83131134e6cc)) of `V2TIMConversation`.

> ? As this method requires the `unreadCount` feature, it applies only to work groups (Work), public groups (Public), and communities (Community), but not to audio-video groups (AVChatRoom) or meeting groups (Meeting). For more information on group types, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).

Sample code:

<dx-tabs>
::: Android
```java
V2TIMManager.getMessageManager().setGroupReceiveMessageOpt("groupA", V2TIMMessage.V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE, new V2TIMCallback() {
  @Override
  public void onSuccess() {
  	// Changed the group message receiving option successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to change the group message receiving option
  }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] setGroupReceiveMessageOpt:@"groupA" opt:V2TIM_RECEIVE_NOT_NOTIFY_MESSAGE succ:^{
    // Changed the group message receiving option successfully
} fail:^(int code, NSString *desc) {
    // Failed to change the group message receiving option
}];
```
:::
</dx-tabs>


