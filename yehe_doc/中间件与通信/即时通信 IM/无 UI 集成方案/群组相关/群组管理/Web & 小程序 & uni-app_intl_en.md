## Feature Description

The group management feature allows creating a group, joining a group, getting the joined groups, leaving a group, or disbanding a group.

[](id:listener)
## Group Event Listener

**Sample**

<dx-codeblock>
:::  js

let onGroupListUpdated = function(event) {
   console.log(event.data);// Array that stores Group instances
};
tim.on(TIM.EVENT.GROUP_LIST_UPDATED, onGroupListUpdated);

:::
</dx-codeblock>



## Creating a Group

>!
>- After this API is used to create `TIM.TYPES.GRP_AVCHATROOM` (an audio-video group), the [joinGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#joinGroup) API needs to be called to join the group to enable the messaging process.
>- Starting from v2.19.1, this API can be used to create topic-enabled communities.

**API**

<dx-codeblock>
:::  js

tim.createGroup(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name             | Type                | Description                                                  |
| ---------------- | ------------------- | ------------------------------------------------------------ |
| name             | String              | Group name, which can contain up to 30 bytes.                |
| type             | String              | Group type. Valid values:<br/><li>TIM.TYPES.GRP_WORK (work group, which is the default value)</li><li>TIM.TYPES.GRP_PUBLIC (public group)</li><li>TIM.TYPES.GRP_MEETING (meeting group)</li><li>TIM.TYPES.GRP_AVCHATROOM (audio-video group)</li><li>TIM.TYPES.GRP_COMMUNITY (community, which is supported by v2.17.0 or later)</li> |
| groupID          | String \| undefined | Group ID. If it is not specified, a unique ID will be automatically created for the group. |
| introduction     | String \| undefined | Group introduction, which can contain up to 240 bytes.       |
| notification     | String \| undefined | Group notice, which can contain up to 300 bytes.             |
| avatar           | String \| undefined | Group profile photo URL, which can contain up to 100 bytes.  |
| maxMemberNum     | Number \| undefined | Maximum number of group members. Default value: 200 for a work group, 2,000 for a public group, 10,000 for a meeting group, or unlimited for an audio-video group. |
| joinOption       | String              | Method to join a group. Valid values:<br/><li>TIM.TYPES.JOIN_OPTIONS_FREE_ACCESS (free to join)</li><li>TIM.TYPES.JOIN_OPTIONS_NEED_PERMISSION (approval required)</li><li>TIM.TYPES.JOIN_OPTIONS_DISABLE_APPLY (no group join allowed)</li>Note: It cannot be modified for `TIM.TYPES.GRP_WORK`, `TIM.TYPES.GRP_MEETING`, and `TIM.TYPES.GRP_AVCHATROOM` groups. Work groups cannot be joined on request, and meeting groups and audio-video groups can be joined freely. |
| memberList       | Array \| undefined  | List of up to 500 existing group members. No group members can be added when an audio-video group is created. The array elements are as structured below:<br/><li>userID --- String --- `userID` of the group member, which is required</li><li>role --- String --- member role, which can only be `Admin`, indicating to add and set the group member as the admin</li><li>memberCustomField --- Array |
| groupCustomField | Array \| undefined  | Custom group field, which is unavailable by default. For more information on how to enable a custom group field, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). |
| isSupportTopic   | Boolean             | It is required for creating a topic-enabled community. Valid values: `true`: create a topic-enabled community; `false`: create an ordinary community. It is supported by v2.19.1 or later. |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

// Create a work group
let promise = tim.createGroup({
  type: TIM.TYPES.GRP_WORK,
  name: 'WebSDK',
  memberList: [{
    userID: 'user1',
    // Group member custom field. By default, this parameter is not available and needs to be enabled. For details, see Custom Fields.
    memberCustomField: [{key: 'group_member_test', value: 'test'}]
  }, {
    userID: 'user2'
  }] // If `memberList` is specified, `userID` must also be specified.
});
promise.then(function(imResponse) { // Created successfully
  console.log(imResponse.data.group); // Profile of the created group
  // A member list is specified during group creation, but a certain user has exceeded the limit on the number of groups a single user can join.
  // If you specify userX, who has joined N groups (maximum number of groups userX can join), as a member of the group during group creation, userX cannot join the group properly.
  // The SDK places the information of userX in overLimitUserIDList for the access side to process.
  console.log(imResponse.data.overLimitUserIDList); // List of users who have exceeded the limit on the number of groups a single user can join. (Supported from v2.10.2)
}).catch(function(imError){
  console.warn('createGroup error:', imError); // Failed to create the group
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Create a topic-enabled community
let promise = tim.createGroup({
  type: TIM.TYPES.GRP_COMMUNITY,
  name: 'WebSDK',
  isSupportTopic: true,
});
promise.then(function(imResponse) { // Created successfully
  console.log(imResponse.data.group); // Profile of the created group
}).catch(function(imError){
  console.warn('createGroup error:', imError); // Failed to create the group
});

:::
</dx-codeblock>


## Joining a Group

The method for joining a group may vary by group type as follows:

| Type                           | Method for Joining a Group                                   |
| ------------------------------ | ------------------------------------------------------------ |
| Work group (Work)              | By invitation                                                |
| Public group (Public)          | On request from the user and on approval from the group owner or admin |
| Meeting group (Meeting)        | Free to join                                                 |
| Community (Community)          | Free to join                                                 |
| Audio-video group (AVChatRoom) | Free to join                                                 |

>!
>- Work groups cannot be joined on request, but only through [addGroupMember](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addGroupMember).
>- A user can join one audio-video group at a time. For example, if a user is already in audio-video group A and attempts to join audio-video group B, the SDK will remove the user from audio-video group A first and then add the user to audio-video group B.

**API**

<dx-codeblock>
:::  js

tim.joinGroup(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name         | Type                | Description |
| ------------ | ------------------- | ----------- |
| groupID      | String              | Group ID    |
| applyMessage | String \| undefined | Remarks     |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

let promise = tim.joinGroup({ groupID: 'group1', type: TIM.TYPES.GRP_AVCHATROOM });
promise.then(function(imResponse) {
  switch (imResponse.data.status) {
    case TIM.TYPES.JOIN_STATUS_WAIT_APPROVAL: // Waiting to be approved by the admin
      break;
    case TIM.TYPES.JOIN_STATUS_SUCCESS: // Joined the group successfully
      console.log(imResponse.data.group); // Profile of the group
      break;
    case TIM.TYPES.JOIN_STATUS_ALREADY_IN_GROUP: // The user is already in the group.
      break;
    default:
      break;
  }
}).catch(function(imError){
  console.warn('joinGroup error:', imError); // Failed to join the group
});

:::
</dx-codeblock>


## Getting the Joined Groups

**API**

<dx-codeblock>
:::  js

tim.getGroupList(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name               | Type               | Description                                                  |
| ------------------ | ------------------ | ------------------------------------------------------------ |
| groupProfileFilter | Array \| undefined | Group profile filter. You can specify extra group profiles to be pulled in addition to those pulled by default. Valid values:<br/><li>TIM.TYPES.GRP_PROFILE_OWNER_ID (group owner ID)</li><li>TIM.TYPES.GRP_PROFILE_CREATE_TIME (group creation time)</li><li>TIM.TYPES.GRP_PROFILE_LAST_INFO_TIME (time the group profile was last changed)</li><li>TIM.TYPES.GRP_PROFILE_MEMBER_NUM (number of group members)</li><li>TIM.TYPES.GRP_PROFILE_MAX_MEMBER_NUM (maximum number of group members)</li><li>TIM.TYPES.GRP_PROFILE_JOIN_OPTION (group join option)></li><li>TIM.TYPES.GRP_PROFILE_INTRODUCTION (group introduction)</li><li>TIM.TYPES.GRP_PROFILE_NOTIFICATION (group notice)</li><li>TIM.TYPES.GRP_PROFILE_MUTE_ALL_MBRS (muting all). It is supported by v2.6.2 or later.</li> |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

// This API pulls only the following information by default: group type, group name, group profile photo, and the time of the last message.
let promise = tim.getGroupList();
promise.then(function(imResponse) {
  console.log(imResponse.data.groupList); // Group list
}).catch(function(imError){
  console.warn('getGroupList error:', imError); // Failed to obtain the group list
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// If the profile fields that are pulled by default fail to meet your requirements, you can pull additional profile fields by referring to the following code.
let promise = tim.getGroupList({
   groupProfileFilter: [TIM.TYPES.GRP_PROFILE_OWNER_ID],
});
promise.then(function(imResponse) {
  console.log(imResponse.data.groupList); // Group list
}).catch(function(imError){
  console.warn('getGroupList error:', imError); // Failed to obtain the group list
});

:::
</dx-codeblock>

## Leaving a Group

>! A group owner can only leave a work group, after which the work group will have no group owner.

**API**

<dx-codeblock>
:::  js

tim.quitGroup(groupID);

:::
</dx-codeblock>

**Parameter**

| Name    | Type   | Description |
| ------- | ------ | ----------- |
| groupID | String | Group ID    |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

let promise = tim.quitGroup('group1');
promise.then(function(imResponse) {
  console.log(imResponse.data.groupID); // ID of the group that the user leaves
}).catch(function(imError){
  console.warn('quitGroup error:', imError); // Failed to leave the group
});

:::
</dx-codeblock>

## Disbanding a Group

>! A work group cannot be disbanded.

**API**

<dx-codeblock>
:::  js

tim.dismissGroup(groupID);

:::
</dx-codeblock>

**Parameter**

| Name    | Type   | Description |
| ------- | ------ | ----------- |
| groupID | String | Group ID    |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

let promise = tim.dismissGroup('group1');
promise.then(function(imResponse) { // Disbanded successfully
  console.log(imResponse.data.groupID); // ID of the disbanded group
}).catch(function(imError){
  console.warn('dismissGroup error:', imError); // Failed to disband the group
});

:::
</dx-codeblock>

## Transferring a Group

>! Only group owners have the permission to transfer groups. Audio-video groups (`TIM.TYPES.GRP_AVCHATROOM`) cannot be transferred.

**API**

<dx-codeblock>
:::  js

tim.changeGroupOwner(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name       | Type   | Description                       |
| ---------- | ------ | --------------------------------- |
| groupID    | String | ID of the group to be transferred |
| newOwnerID | String | ID of the new group owner         |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

let promise = tim.changeGroupOwner({
  groupID: 'group1',
  newOwnerID: 'user2'
});
promise.then(function(imResponse) { // Transferred successfully
  console.log(imResponse.data.group); // Group profile
}).catch(function(imError) { // Failed to transfer the group
  console.warn('changeGroupOwner error:', imError); // Failed to transfer the group
});

:::
</dx-codeblock>

## Processing (Approving or Rejecting) a Group Join Request

>! If there are multiple admins in a group, when a user requests to join the group, all the online admins will receive the [system notification of the group join request](https://web.sdk.qcloud.com/im/doc/en/Message.html#.GroupSystemNoticePayload). If one of the admins processes (approves or rejects) the request, other admins cannot process it again, that is, they cannot modify the processing result.

**API**

<dx-codeblock>
:::  js

tim.handleGroupApplication(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name          | Type                | Description                                         |
| ------------- | ------------------- | --------------------------------------------------- |
| handleAction  | String              | Processing result. Valid values: `Agree`, `Reject`. |
| handleMessage | String \| undefined | Remarks                                             |
| message       | Message             | Message instance of the group system notification   |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

let promise = tim.handleGroupApplication({
  handleAction: 'Agree',
  handleMessage: 'Welcome',
  message: message // The message instance of the group system notification for an application to join a group.
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // Group profile
}).catch(function(imError){
  console.warn('handleGroupApplication error:', imError); // Error message
});

:::
</dx-codeblock>
