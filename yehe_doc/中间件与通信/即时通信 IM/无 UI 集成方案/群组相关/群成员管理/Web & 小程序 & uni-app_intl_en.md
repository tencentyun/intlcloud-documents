## Feature Description

Group member management includes pulling the member list, muting group members, removing group members, granting permissions, and transferring the group ownership.

## Getting the Group Member List

>!
>- Starting from v2.6.2, this API supports pulling the muting stop timestamp (`muteUntil`). The receiver can determine whether a group member is muted and the remaining muting period based on the value. On versions earlier than v2.6.2, the profile in the group member list obtained through this API is incomplete, and it contains only the information which is sufficient to render the group member list, such as profile photo and nickname. To query the muting stop timestamp (`muteUntil`) and other details, use [getGroupMemberProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberProfile).
>- This API is used to pull group members by page but not the total number of group members. To get the total number of the group members (`memberNum`), use [getGroupProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupProfile).

**API**

<dx-codeblock>
:::  js

tim.getGroupMemberList(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID     | String | 		Group ID |
| count | Number | Number of group members to be pulled. Default value: `15`. Maximum value: `100`. Too large a response packet will cause a request failure. If more than 100 group members are passed in, only the first 100 group members are pulled. |
| offset | Number | Offset value. By default, the pull will start from `0`. |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

let promise = tim.getGroupMemberList({ groupID: 'group1', count: 30, offset:0 }); // Pull 30 group members starting from 0
promise.then(function(imResponse) {
  console.log(imResponse.data.memberList); // Group member list
}).catch(function(imError){
  console.warn('getGroupMemberList error:', imError);
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Starting from v2.6.2, this API can be used to pull the muting stop timestamps of group members.
let promise = tim.getGroupMemberList({ groupID: 'group1', count: 30, offset:0 }); // Pull 30 group members starting from 0
promise.then(function(imResponse) {
  console.log(imResponse.data.memberList); // Group member list
  for (let groupMember of imResponse.data.memberList) {
    if (groupMember.muteUntil * 1000  > Date.now()) {
      console.log(`${groupMember.userID} muted`);
    } else {
      console.log(`${groupMember.userID} not muted`);
    }
  }
}).catch(function(imError){
    console.warn('getGroupMemberProfile error:', imError);
});

:::
</dx-codeblock>

## Muting

### Muting a specified group member

>!
>- Only the group owner can mute/unmute the admin and ordinary group members. Only the admin can mute/unmute ordinary group members.
>- Starting from v2.19.1, the period for muting a community member in a topic can be set simply by passing in `topicID` for `groupID`.

**API**

<dx-codeblock>
:::  js

tim.setGroupMemberMuteTime(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID     | String | 		Group ID or topic ID |
| userID | String | User ID |
| muteTime | Number | Muting period in seconds. If it is set to `1000`, the user is muted for 1,000 seconds immediately; if it is set to `0`, the user is unmuted. |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

let promise = tim.setGroupMemberMuteTime({
  groupID: 'group1',
  userID: 'user1',
  muteTime: 600 // The user is muted for ten minutes. If the value is set to `0`, the user is unmuted.
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // New group profile
  console.log(imResponse.data.member); // New group member profile
}).catch(function(imError){
  console.warn('setGroupMemberMuteTime error:', imError); // Failed to mute the member
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

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
  console.warn('setGroupMemberMuteTime error:', imError); // Failed to mute the member
});

:::
</dx-codeblock>


### Muting the entire group

<dx-codeblock>
:::  js

// Starting from v2.6.2, the SDK supports muting and unmuting all. Currently, when all users are muted in a group, group notifications cannot be delivered.
let promise = tim.updateGroupProfile({
  groupID: 'group1',
  muteAllMembers: true, // true: mute all; false: unmute all
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // Detailed group profile after modification
}).catch(function(imError){
  console.warn('updateGroupProfile error:', imError); // Failed to modify the group profile
});

:::
</dx-codeblock>


## Removing a Group Member

**API**

<dx-codeblock>
:::  js

tim.deleteGroupMember(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID     | String | 		Group ID or topic ID |
| userIDList | Array | List of IDs of the group members to be removed |
| reason | String \| undefined | Reason for removing a member |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

let promise = tim.deleteGroupMember({groupID: 'group1', userIDList:['user1'], reason: 'You are kicked out because you have violated the group rules.'});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // Group profile displayed after group member deletion
  console.log(imResponse.data.userIDList); // List of userIDs of the deleted group members
}).catch(function(imError){
  console.warn('deleteGroupMember error:', imError); // Error message
});

:::
</dx-codeblock>

## Changing the Role of a Group Member

**API**

<dx-codeblock>
:::  js

tim.setGroupMemberRole(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID     | String | 		Group ID or topic ID |
| userIDList | Array | User ID |
| role | String | Valid values: TIM.TYPES.GRP_MBR_ROLE_ADMIN (group admin), TIM.TYPES.GRP_MBR_ROLE_MEMBER (ordinary group member), TIM.TYPES.GRP_MBR_ROLE_CUSTOM (custom group member role, which is supported only by the community) |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

let promise = tim.setGroupMemberRole({
  groupID: 'group1',
  userID: 'user1',
  role: TIM.TYPES.GRP_MBR_ROLE_ADMIN // Set user1 as the admin of group1.
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // New group profile
  console.log(imResponse.data.member); // New group member profile
}).catch(function(imError){
  console.warn('setGroupMemberRole error:', imError); // Error message
});

:::
</dx-codeblock>

## Getting the Number of Online Group Members

>! If this API is called to get the number of online members in a group other than an audio-video group (AVChatRoom), `memberCount` returned by the SDK is `0`. We recommend you call this API only once every 5-10 seconds.

**API**

<dx-codeblock>
:::  js

tim.getGroupOnlineMemberCount(groupID);

:::
</dx-codeblock>

**Parameter**

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID     | String | 		Group ID |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

// Get the number of online users in an audio-video group (supported from v2.8.0)
let promise = tim.getGroupOnlineMemberCount('group1');
promise.then(function(imResponse) {
  console.log(imResponse.data.memberCount);
}).catch(function(imError){
  console.warn('getGroupOnlineMemberCount error:', imError); // Failed to obtain the number of online members in the audio-video group (AVChatRoom)
});

:::
</dx-codeblock>
