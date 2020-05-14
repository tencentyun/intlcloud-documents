You can mute a group member or all group members for a specified period of time. During the muting period, the muted member cannot send messages in the current group. This muting operation is effective only for the current group. During the muting period, even if the muted member quits the group and rejoins it, the muting will remain effective until the muting period is over or the member is unmuted.
This document mainly describes how to mute/unmute group members in web and Mini Program SDKs.

## Use limits

- Group type restrictions
 <table>
<tr>
<th width="25%">Private group</th>
<th width="25%">Public group</th>
<th width="25%">Chat room</th>
<th width="25%">Audio-video chat room</th>
</tr>
<tr>
<td><strong>Not supported</strong></td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
</table>
- Member role restrictions
<table>
<tr>
<th width="25%">Member role</th>
<th>Permissions</th>
</tr>
<tr>
<td>App admin</td>
<td>App admins are allowed to mute/unmute all members in all groups under the current SDKAppID.</td>
</tr>
<tr>
<td>Group owner</td>
<td>The group owner is allowed to mute/unmute admins and common members in the current group.</td>
</tr>
<tr>
<td>Group admin</td>
<td>Group admins are allowed to mute/unmute common members in the current group.</td>
</tr>
<tr>
<td>Common member</td>
<td>No muting permissions</td>
</tr>
</table>

## Directions

### Step 1: Confirm the operation permission
1. Call the [getGroupProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupProfile) API to query the type of the current group and confirm whether muting/unmuting is supported.
 > If the type is Private (private group), muting is not supported.
 >
2. Call the [getGroupMemberProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupMemberProfile) API to query the member role of the specified userID in the current group and confirm whether the user has the permission to perform muting/unmuting.

### Step 2: Mute/Unmute a group member
#### Muting/Unmuting a single user
App admins, the group owner, or group admins can call the [setGroupMemberMuteTime](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#setGroupMemberMuteTime) API to mute/unmute a specified member in the specified group. For each call, only one member can be muted/unmuted.
The following table lists the request parameters.

| Name | Type | Description |
| --------- | ------- | --------|
| groupID | String | Group ID |
| userID  | String | Group Member ID|
| muteTime | Number | The muting period, in seconds. 0: unmuting. |

Below is a sample request:
```javascript
let promise = tim.setGroupMemberMuteTime({
  groupID: 'group1',
  userID: 'user1',
  muteTime: 1000
});
```

#### Muting/Unmuting all members
> To use this feature, you need to upgrade the SDK to 2.6.2 or higher. At present, for muting and unmuting all members, no group tip message is delivered.
 
App admins or the group owner can call the [updateGroupProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#updateGroupProfile) API to mute/unmute all admins and common members in the specified group.
The following table lists the request parameters.

| Name | Type | Description |
| --------- | ------- | --------|
| groupID | String | Group ID |
| muteAllMembers | Boolean | Set muting. true: mute all members. false: unmute all members. |

Below is a sample request:
```javascript
let promise = tim.updateGroupProfile({
  groupID: 'group1',
  muteAllMembers：true, // true: mute all members. false: unmute all members.
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // The detailed group profile after modification.
}).catch(function(imError) {
  console.warn('updateGroupProfile error:', imError); // Information on the failure in modifying the group profile.
});
```



### Step 3: Monitor and process the event TIM.EVENT.MESSAGE_RECEIVED
After a group member is muted, the member will receive a [group tip](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupTipPayload) indicating that he/she has been muted. You can traverse event.data to get relevant data and render it to the interface.
> After relevant muting/unmuting notifications are received, we recommend that you implement the disable/enable input box or input area status.

<pre>
tim.on(TIM.EVENT.MESSAGE_RECEIVED, function(event) {
  // Received new one-to-one, group, group tips, and group system notification messages that are pushed. Traverse event.data to get message list data and render it to the interface.
  // event.name - TIM.EVENT.MESSAGE_RECEIVED
  // event.data - an array that stores Message objects - [Message]
  const length = event.data.length;
  let message;
  for (let i = 0; i < length; i++) {
    message = event.data[i];
    switch (message.type) {
      // Mute user A, user A will receive a group tip message indicating that he/she has been muted.
      case TIM.TYPES.MSG_GRP_TIP:
        this._handleGroupTip(message);
        break;
      case TIM.TYPES.MSG_TEXT: // Text message. For more message types, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html">Message</a>.
        break;
      default:
        break;
    }
  }
});

_handleGroupTip(message) {
  switch (message.payload.operationType) {
    case TIM.TYPES.GRP_TIP_MBR_PROFILE_UPDATED: // Group member profile is modified. For example, a member is muted.
      const memberList = message.payload.memberList;
      for (let member of memberList) {
        console.log(`${member.userID} muted for ${member.muteTime} seconds`);
      }
      break;
    case TIM.TYPES.GRP_TIP_MBR_JOIN: // A member joins the group.
      break;
    case TIM.TYPES.GRP_TIP_MBR_QUIT: // A member quits the group.
      break;
    case TIM.TYPES.GRP_TIP_MBR_KICKED_OUT: // A member is kicked out of the group.
      break;
    case TIM.TYPES.GRP_TIP_GRP_PROFILE_UPDATED: // Group profile is modified.
      break;
	default:
	  break;
  }
}
</pre>

### Step 4: Check the muting status

- For SDK 2.6.2 and higher, you can call the [getGroupMemberList](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupMemberList) API to pull the muting stop timestamp (muteUntil) of a group member. Based on its value, you can find out whether the member is muted and the remaining muting time. After the member is unmuted, the following calculation formula for the member is valid: GroupMember.muteUntil * 1000 <= Date.now().
```javascript
// Starting from v2.6.2, the getGroupMemberList API can be used to pull the muting stop timestamps of group members.
let promise = tim.getGroupMemberList({ groupID: 'group1', count: 30, offset:0 }); // Pull 30 group members starting from 0.
promise.then(function(imResponse) {
  console.log(imResponse.data.memberList); // Group member list
  for (let groupMember of imResponse.data.memberList) {
    if (groupMember.muteUntil * 1000  > Date.now()) {
      console.log(`${groupMember.userID} Muted`);
    } else {
      console.log(`${groupMember.userID} Not muted`);
    }
  }
}).catch(function(imError) {
  console.warn('getGroupMemberProfile error:', imError);
});
```
- For SDK versions earlier than 2.6.2, you can call the [getGroupMemberProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupMemberProfile) API to query the muting stop timestamps (muteUntil) and other profile information of group members.
