## Group Overview

Instant Messaging (IM) supports multiple group types. For more information on their characteristics and limits, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). A group is identified by a unique ID that enables different operations.

## Group Management

### Obtaining your group list
This API is used to obtain your group list when you need to render or refresh **My Groups**. For more information, see [Group](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Group.html).

**API name**

```js
tim.getGroupList();
```

**Request parameters**

`options` is of `Object` type and has the following properties:

| Name | Type | Required | Description |
| :---------------------- | :------------- | :--- | :----------------------------------------------------------- |
| `groupProfileFilter` | `Array<String>` | `<optional>` | Group profile filter. The system specifies some profile fields to retrieve by default. You can specify additional group profile fields to retrieve. Valid values:<br/>TIM.TYPES.GRP_PROFILE_OWNER_ID: group owner ID<br/>TIM.TYPES.GRP_PROFILE_CREATE_TIME: group creation time<br/>TIM.TYPES.GRP_PROFILE_LAST_INFO_TIME: last modified time of the group profile<br/>TIM.TYPES.GRP_PROFILE_MEMBER_NUM: number of group members<br/>TIM.TYPES.GRP_PROFILE_MAX_MEMBER_NUM: maximum number of group members<br/>TIM.TYPES.GRP_PROFILE_JOIN_OPTION: option for joining the group<br/>TIM.TYPES.GRP_PROFILE_INTRODUCTION: group introduction<br/>TIM.TYPES.GRP_PROFILE_NOTIFICATION: group announcement |

**Response**

This API returns a `Promise` object. The callback functions are as follows:
- The callback parameter of `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.groupList` contains the list of groups.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**
- Group profile information that is retrieved by default:
```js
// This API retrieves the following information by default: group type, group name, group profile photo, and the time of the last message.
let promise = tim.getGroupList();
promise.then(function(imResponse) {
  console.log(imResponse.data.groupList); // Group list
}).catch(function(imError) {
  console.warn('getGroupList error:', imError); // Information on the failure in obtaining the group list
});
```
- Other group profile information to retrieve:
```js
// If the profile fields that are retrieved by default fail to meet your requirements, you can retrieve additional profile fields by referring to the following code.
let promise = tim.getGroupList({
   groupProfileFilter: [TIM.TYPES.GRP_PROFILE_OWNER_ID],
});
promise.then(function(imResponse) {
  console.log(imResponse.data.groupList); // Group list
}).catch(function(imError) {
  console.warn('getGroupList error:', imError); // Information on the failure in obtaining the group list
});
```

### Obtaining the detailed group profile

For more information, see [Group](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Group.html).

**API name**

```js
tim.getGroupProfile(options);
```

**Request parameters**

`options` is of `Object` type and has the following properties:

| Name | Type | Required | Description |
| :---------------------- | :------------- | :--- | :----------------------------------------------------------- |
| `groupID` | `String` | - | Group ID |
| `groupCustomFieldFilter` | `Array<String>` | `<optional>` | Filter for group custom fields. You can specify group custom fields to retrieve. For more information, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529). |

**Response**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). You can obtain group profiles from `IMResponse.data.group`.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.getGroupProfile({
  groupID: 'group1',
  groupCustomFieldFilter: ['key1','key2']
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group);
}).catch(function(imError) {
  console.warn('getGroupProfile error:', imError); // Information on the failure in obtaining the detailed group profile
});
```



### Creating a group

For more information, see [Group](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Group.html).

>After this API is used to create TIM.TYPES.GRP_AVCHATROOM (an audio-video chat room), you must call [joinGroup](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#joinGroup) to join the group before messaging becomes available.

**API name**

```js
tim.createGroup(options);
```

**Request parameters**

`options` is of `Object` type and has the following properties:

| Name | Type | Required | Default Value | Description |
| :--------------- | :------------- | :--------- | :----------------------------------- | :----------------------------------------------------------- |
| `name` | `String` | - | - | Required. It indicates the group name with a maximum length of 30 bytes. |
| `type` | `String` | `<optional>` | `TIM.TYPES.GRP_PRIVATE` | Group type. Valid values:<li>TIM.TYPES.GRP_PRIVATE: private group (default)</li><li>TIM.TYPES.GRP_PUBLIC: public group</li><li>TIM.TYPES.GRP_CHATROOM: chat room</li><li>TIM.TYPES.GRP_AVCHATROOM: ILVB chat room</li> |
| `groupID` | `String` | `<optional>` | - | Group ID If this field is not specified, a unique group ID will be created automatically. |
| `introduction` | `String` | `<optional>` | - | Group introduction. The value can be up to 240 bytes in length. |
| `notification` | `String` | `<optional>` | - | Group announcement. The value can be up to 300 bytes in length. |
| `avatar` | `String` | `<optional>` | - | URL of the group’s profile photo. The value can be up to 100 bytes in length. |
| `maxMemberNum` | `Number` | `<optional>` | - | Maximum number of group members. The default value varies with the group type, which is 200 for private groups, 2,000 for public groups, 6,000 for chat rooms, and no limit for audio-video chat rooms. |
| `joinOption` | `String` | `<optional>` | `TIM.TYPES.JOIN_OPTIONS_FREE_ACCESS` | Processing method of applications to join the group. **This field cannot be specified for private groups, chat rooms, and audio-video chat rooms.** For private groups, the value of this field is fixed to **Applications disabled**. For chat rooms and audio-video chat rooms, the value of this field is fixed to **Free access**. Valid values:<br><li>TIM.TYPES.JOIN_OPTIONS_FREE_ACCESS: the group can be joined freely.</li><li>TIM.TYPES.JOIN_OPTIONS_NEED_PERMISSION: approval is required.</li><li>TIM.TYPES.JOIN_OPTIONS_DISABLE_APPLY: the group cannot be joined.</li> |
| `memberList` | `Array<Object>` | `<optional>`| - | List of initial group members with a maximum number of 500 members. This field is unavailable for audio-video chat rooms. For more information, see the following [memberList parameter description](#memberList). |
| `groupCustomField` | `Array<Object>` | `<optional>` | - | Group custom fields. No custom fields are specified by default. To create a group custom field, see [Group Member Profiles](https://intl.cloud.tencent.com/document/product/1047/33529). |

<span id="memberList"></span>
`memberList` parameter description

| Name | Type | Required | Description |
| :------------------ | :------------- | :--------- | :----------------------------------------------------------- |
| `userID` | `String` | - | Required. It indicates the UserID of the group member. |
| `role` | `String` | `<optional>` | Role of the group member. The only valid value is Admin, which indicates to add the user and set the user as an admin. |
| `memberCustomField` | `Array<Object>` | `<optional>` | Group member custom fields. No custom fields are specified by default. To create a group member custom field, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529). |

**Response**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). You can obtain group profiles from `IMResponse.data.group`.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
// Create a private group.
let promise = tim.createGroup({
  type: TIM.TYPES.GRP_PRIVATE,
  name: 'WebSDK',
  memberList: [{userID: 'user1'}, {userID: 'user2'}] // If memberList is specified, userID must also be specified.
});
promise.then(function(imResponse) { // Created successfully
  console.log(imResponse.data.group); // Profile of the created group
}).catch(function(imError) {
  console.warn('createGroup error:', imError); // Information on the failure in creating the group
});
```

### Disbanding a group

This API is used by a group owner to disband a group.
>A group owner cannot disband private groups.

**API name**

```js
tim.dismissGroup(groupID);
```

**Request parameters**

| Name | Type | Description |
| :-------- | :----- | :------ |
| `groupID` | `String` | Group ID |

**Response**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). You can obtain the ID of the disbanded group from `IMResponse.data.groupID`.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.dismissGroup('group1');
promise.then(function(imResponse) { // Disbanded successfully
  console.log(imResponse.data.groupID); // ID of the disbanded group
}).catch(function(imError) {
  console.warn('dismissGroup error:', imError); // Information on the failure in disbanding the group
});
```

### Updating a group profile

**API name**

```js
tim.updateGroupProfile(options);
```

**Request parameters**

`options` is of `Object` type and has the following properties:

| Name | Type | Required | Default | Description |
| :----------------- | :------------- | :--------- | :----------------------------------- | :----------------------------------------------------------- |
| `groupID` | `Object` | - | - | Group ID |
| `name` | `Object` | `<optional>` | - | Group name. The value can be up to 30 bytes in length. |
| `avatar` | `Object` | `<optional>` | - | URL of the group’s profile photo. The value can be up to 100 bytes in length. |
| `introduction` | `Object` | `<optional>` | - | Group introduction. The value can be up to 240 bytes in length. |
| `notification` | `Object` | `<optional>` | - | Group announcement. The value can be up to 300 bytes in length. |
| `maxMemberNum` | `Number` | `<optional>` | - | Maximum number of group members. The maximum value is 6000. |
| `joinOption` | `String` | `<optional>` | `TIM.TYPES.JOIN_OPTIONS_FREE_ACCESS` | Processing method of applications to join the group.<br>**This field cannot be specified for private groups, chat rooms, and audio-video chat rooms.** For private groups, the value of this field is fixed to **Applications disabled**. For chat rooms and audio-video chat rooms, the value of this field is fixed to **Free access**. Valid values:<li>TIM.TYPES.JOIN_OPTIONS_FREE_ACCESS: the group can be joined freely.</li><li>TIM.TYPES.JOIN_OPTIONS_NEED_PERMISSION: approval is required.</li><li>TIM.TYPES.JOIN_OPTIONS_DISABLE_APPLY: the group cannot be joined.</li> |
| `groupCustomField` | `Array<Object>` | `<optional>` | - | Group custom field. For more information, see the following [`groupCustomField` parameter description](#groupCustomField).<br>No custom fields are specified by default. To create a group custom field, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529). |

<span id="groupCustomField"></span>
`groupCustomField` parameter description

| Name | Type | Description |
| :------ | :----- | :---------------- |
| `key` | `String` | Key of the custom field |
| `value` | `String` | Value of the custom field |

**Response**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). You can obtain the modified group profile from `IMResponse.data.group`.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.updateGroupProfile({
  groupID: 'group1',
  name: 'new name', // Modify the group name.
  introduction: 'this is introduction.', // Modify the group announcement.
  // Starting from v2.6.0, group members can receive group notifications about custom group field modifications and obtain related content. For more information, see Message.payload.newGroupProfile.groupCustomField.
  groupCustomField: [{ key: 'group_level', value: 'high'}] // Modify the group custom field.
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // Detailed group profile after the modification
}).catch(function(imError) {
  console.warn('updateGroupProfile error:', imError); // Information on the failure in modifying the group profile
});
```

### Applying to join a group

Users can join private groups only via invitation, but not application.

**API name**

```js
tim.joinGroup(options);
```

**Request parameters**

`options` is of `Object` type and has the following properties:

| Name | Type | Required | Description |
| :------------- | :----- | :--------- | :----------------------------------------------------------- |
| `groupID` | `String` | - | - |
| `applyMessage` | `String` | - | Postscript |
| `type` | `String` | `<optional>` | Type of the group that the user wants to join. This field is required when the user wants to join an audio-video chat room. Valid values:<br/><li>TIM.TYPES.GRP_PUBLIC: public group</li><li>TIM.TYPES.GRP_CHATROOM: chat room</li><li>TIM.TYPES.GRP_AVCHATROOM: audio-video chat room</li> |

**Response**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data` contains the following properties:
	<table>
     <tr>
         <th>Name</th>  
         <th>Meaning</th>
     </tr>
	 <tr>
	     <td>status</td>   
	     <td>Status of the group joining process. Valid values:<ul><li>TIM.TYPES.JOIN_STATUS_WAIT_APPROVAL: waiting for the admin’s approval</li><li>TIM.TYPES.JOIN_STATUS_SUCCESS: joined successfully</li><li>TIM.TYPES.JOIN_STATUS_ALREADY_IN_GROUP: already in the group</li></ul></td>
     </tr> 
	 <tr>
	     <td>group</td>   
	     <td>Group profile displayed when the user joins the group</td>   
     </tr> 
</table>

- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.joinGroup({ groupID: 'group1', type: TIM.TYPES.GRP_AVCHATROOM });
promise.then(function(imResponse) {
  switch (imResponse.data.status) {
    case TIM.TYPES.JOIN_STATUS_WAIT_APPROVAL: break; // Waiting for the admin’s approval
    case TIM.TYPES.JOIN_STATUS_SUCCESS: // Joined the group successfully
      console.log(imResponse.data.group); // Profile of the group
      break;
    default: break;
  }
}).catch(function(imError){
  console.warn('joinGroup error:', imError); // Information on the failure in joining the group
});
```

### Exiting a group

A group owner can only exit private groups. After the group owner exits, the private group has no group owner.

**API name**

```js
tim.quitGroup(groupID);
```

**Request parameters**

| Name | Type | Description |
| :-------- | :----- | :------ |
| `groupID` | `String` | Group ID |

**Response**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.groupID` is the ID of the exited group.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.quitGroup('group1');
promise.then(function(imResponse) {
  console.log(imResponse.data.groupID); // ID of the exited group
}).catch(function(imError){
  console.warn('quitGroup error:', imError); // Information on the failure in exiting the group
});
```

### Searching for a group by group ID

Private groups do not support searching.

**API name**

```js
tim.searchGroupByID(groupID);
```

**Request parameters**

| Name | Type | Description |
| :-------- | :----- | :------ |
| `groupID` | `String` | Group ID |

**Response**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` indicates the group profile.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.searchGroupByID('group1');
promise.then(function(imResponse) {
  const group = imResponse.data.group; // Group profile
}).catch(function(imError) {
  console.warn('searchGroupByID error:', imError); // Information on the failure in searching for the group
});
```

### Transferring a group
Only the group owner can transfer the ownership of a group. Audio-video chat rooms cannot be transferred.

**API name**

```js
tim.changeGroupOwner(options);
```

**Request parameters**

`options` is of `Object` type and has the following properties:

| Name | Type | Description |
| :----------- | :----- | :-------------- |
| `groupID` | `String` | ID of the group to be transferred |
| `newOwnerID` | `String` | ID of the new group owner |

**Response**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` indicates the group profile.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.changeGroupOwner({
  groupID: 'group1',
  newOwnerID: 'user2'
});
promise.then(function(imResponse) { // Transferred successfully
  console.log(imResponse.data.group); // Group profile
}).catch(function(imError) { // Failed to transfer the group
  console.warn('changeGroupOwner error:', imError); // Information on the failure in transferring the group
});
```

### Processing an application to join a group

When a user applies to join a group that requires an admin’s approval, the admins and the group owner will receive a **group system notification** concerning the application. For more information, see [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html).

**API name**

```js
tim.handleGroupApplication(options);
```

**Request parameters**

`options` parameter is of `Object` type and has the following properties:

| Name | Type | Required | Description |
| :-------------- | :--------------------- | :--------- | :----------------------------------------------- |
| `handleAction` | `String` | - | Processing result. Agree: the application is approved. Reject: the application is rejected. |
| `handleMessage` | `String` | `<optional>` | Postscript |
| `message` | [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html) | - | Message instance of the **group system notification** for an application to join a group. This instance can be obtained in the following ways:<li>The callback function parameter of the <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.GROUP_SYSTEM_NOTICE_RECERIVED">event for new group system notifications</a></li><li>Messages for system sessions</li> |

**Response**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` indicates the group profile.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.handleGroupApplication({
  handleAction: 'Agree',
  handleMessage: 'Welcome',
  message: message // Message instance of the group system notification for an application to join a group
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // Group profile
}).catch(function(imError){
  console.warn('handleGroupApplication error:', imError); // Error information
});
```

### Setting the notification type for group messages

**API name**

```js
tim.setMessageRemindType(options);
```

**Request parameters**

`options` is of `Object` type and has the following properties:

| Name | Type | Description |
| :------------------ | :----- | :----------------------------------------------------------- |
| `groupID` | `String` | Group ID |
| `messageRemindType` | `String` | Notification type of group messages. Valid values:<li>TIM.TYPES.MSG_REMIND_ACPT_AND_NOTE: the SDK receives a message and throws a <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED">message receiving event</a> to notify the access side, which then sends a notification.</li><li>TIM.TYPES.MSG_REMIND_ACPT_NOT_NOTE: the SDK receives a message and throws a <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED">message receiving event</a> to notify the access side, which then does not send any notifications.</li><li>TIM.TYPES.MSG_REMIND_DISCARD: the SDK rejects a message and does not throw any <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED">message receiving events</a>.</li> |

**Response**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` indicates the group profile.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.setMessageRemindType({ groupID: 'group1', messageRemindType: TIM.TYPES.MSG_REMIND_DISCARD }); // Reject the message.
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // Group profile after being set
}).catch(function(imError) {
  console.warn('setMessageRemindType error:', imError);
});
```

## Group Member Management

### Obtaining the group member list

>
>- Starting from v2.6.2, this API can be used to pull the muting stop timestamps of group members (muteUntil). Based on the value of muteUntil, the access side can find out whether the member is muted and the remaining muting time.
>- In versions earlier than v2.6.2, this API can be used to obtain profile information including profile photos and nicknames, which is sufficient to meet the rendering requirements of the group member list. To obtain detailed information such as member muting stop timestamps (muteUntil), use [getGroupMemberProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupMemberProfile).
>- This API is used to pull paginated lists of group members and not the full list. To obtain the full list of group members (memberNum), use [getGroupProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupProfile).

For more information, see [GroupMember](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/GroupMember.html).

**API name**

```js
tim.getGroupMemberList(options);
```

**Request parameters**

`options` is of `Object` type and has the following properties:

| Name | Type | Required | Default Value | Description |
| :-------- | :------- | :------------ | :----- | :--------------------------- |
| `groupID` | `String` | - | - | Group ID |
| `count` | `Number` | `<optional> ` | `15` | Number of members whose IDs are to be retrieved. The maximum value is 100, which avoids request failure caused by excessively large returned packets. If the IDs of more than 100 members are passed in, only the IDs of the first 100 members will be retrieved. |
| `offset` | `Number` | `<optional>` | `0` | Offset. IDs are retrieved starting from 0 by default. |

**Response**

This API returns a `Promise` object. The callback functions are as follows:

- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.memberList` indicates the list of group members. For more information, see [GroupMember](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/GroupMember.html).
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```javascript
let promise = tim.getGroupMemberList({ groupID: 'group1', count: 30, offset:0 }); // Pull 30 group members starting from 0.
promise.then(function(imResponse) {
  console.log(imResponse.data.memberList); // Group member list
}).catch(function(imError) {
  console.warn('getGroupMemberList error:', imError);
});
// Starting from v2.6.2, this API can be used to pull the muting stop timestamps of group members.
let promise = tim.getGroupMemberList({ groupID: 'group1', count: 30, offset:0 }); // Pull 30 group members starting from 0.
promise.then(function(imResponse) {
  console.log(imResponse.data.memberList); // Group member list
  for (let groupMember of imResponse.data.memberList) {
    if (groupMember.muteUntil * 1000  > Date.now()) {
      console.log(`${groupMember.userID} is muted`);
    } else {
      console.log(`${groupMember.userID} is not muted`);
    }
  }
}).catch(function(imError) {
    console.warn('getGroupMemberProfile error:', imError);
});
```

### Obtaining the profiles of group members

>
>- This API requires SDK v2.2.0 or later.
>- The maximum number of users queried each time is 50. If the length of the array passed in is greater than 50, only the first 50 users will be queried and the rest will be discarded. 

For more information, see [GroupMember](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/GroupMember.html).

**API name**

```js
tim.getGroupMemberProfile(options);
```

**Request parameters**

`options` is of `Object` type and has the following properties:

| Name | Type | Required | Description |
| :------------------------ | :--------------- | :------------ | :----------------------------------------------------------- |
| `groupID` | `String` | - | Group ID |
| `userIDList` | `Array.<String>` | - | IDs of group members whose profiles to be queried |
| `memberCustomFieldFilter` | `Array.<String>` | `<optional>` | Filter for group member custom fields. If this field is not specified, all group member custom fields are queried by default. |

**Response**

This API returns a `Promise` object. The callback functions are as follows:

- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.memberList` indicates the list of group members whose profiles are queried successfully. For more information, see [GroupMember](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/GroupMember.html).
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

### Adding a group member

The rules for adding a group member are as follows:
-  TIM.TYPES.GRP_PRIVATE (private group): any group member can invite users to the group, and acceptance by the invitee is not required.
-  TIM.TYPES.GRP_PUBLIC (public group)/TIM.TYPES.GRP_CHATROOM (chat room): only the app admin can invite users to the group, and acceptance by the invitee is not required.
-  TIM.TYPES.GRP_AVCHATROOM (audio-video chat room): no member (including the app admin) is allowed to invite any user to the group.

For more information, see [Group](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Group.html)[GroupMember](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/GroupMember.html) and [Differences in Group Member Operations](https://intl.cloud.tencent.com/document/product/1047/33529).

**API name**

```js
tim.addGroupMember(options);
```

**Request parameters**

`options` is of `Object` type and has the following properties:

| Name | Type | Description |
| :----------- | :------------- | :-------------------------------------------- |
| `groupID` | `String` | Group ID |
| `userIDList` | `Array<String>` | An array of IDs of the group members to be added. Up to 500 group members can be added at a time. |

**Response**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data` contains the following properties:
	<table>
     <tr>
         <th nowrap="nowrap">Name</th>  
         <th>Type</th>  
         <th nowrap="nowrap">Description</th>  
     </tr>
	 <tr>      
         <td>successUserIDList</td>   
	     <td>Array&#60;String&#62;</td>   
	     <td>List of userIDs that were added successfully</td>   
     </tr> 
	 <tr>      
         <td>failureUserIDList</td>   
	     <td>Array&#60;String&#62;</td>   
	     <td>List of userIDs that failed to be added</td>   
     </tr> 
	 <tr>      
         <td>existedUserIDList</td>   
	     <td>Array&#60;String&#62;</td>   
	     <td>List of userIDs that were already in the group</td>   
     </tr> 
	 <tr>      
         <td>group</td>   
	     <td><a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Group.html">Group</a></td>   
	     <td>Group profile after the API is called</td>   
     </tr> 
</table>

- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.addGroupMember({
  groupID: 'group1',
  userIDList: ['user1','user2','user3']
});
promise.then(function(imResponse) {
  console.log(imResponse.data.successUserIDList); // userIDList of group members that were added successfully
  console.log(imResponse.data.failureUserIDList); // userIDList of group members that failed to be added
  console.log(imResponse.data.existedUserIDList); // userIDList of group members that were already in the group
  console.log(imResponse.data.group); // Group profile that is displayed after the group members are added
}).catch(function(imError) {
  console.warn('addGroupMember error:', imError); // Error information
});
```



### Deleting a group member

This API is used to delete a group member. Only the group owner can delete a group member.

**API name**

```js
tim.deleteGroupMember(options)
```

**Request parameters**

`options` is of `Object` type and has the following properties:

| Name | Type | Description |
| :----------- | :------------- | :----------------------- |
| `groupID` | `String` | Group ID |
| `userIDList` | `Array<String>` | List of IDs of the group members that are to be deleted |
| `reason` | `String` | Reason for deleting the one or more group members. This field is optional. |

**Response**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` indicates the updated group profile.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.deleteGroupMember({groupID: 'group1', userIDList:['user1'], reason: 'You were deleted from the group because you violated the group rules.'});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // Group profile that is displayed after the one or more group members are deleted
  console.log(imResponse.data.userIDList); // List of userIDs of the deleted group members
}).catch(function(imError) {
  console.warn('deleteGroupMember error:', imError); // Error information
});
```



### Muting or unmuting a group member

This API is used to set the muting duration for a group member. You can mute or unmute a group member. The muting and unmuting features are unavailable to TIM.TYPES.GRP_PRIVATE groups (private groups).
>Only the group owner and the group admin have permissions for this operation.
>- The group owner can mute and unmute the group admin and ordinary group members.
>- The group admin can mute and unmute ordinary group members.

**API name**

```js
tim.setGroupMemberMuteTime(options)
```

**Request parameters**

`options` is of `Object` type and has the following properties:

| Name | Type | Description |
| :--------- | :----- | :----------------------------------------------------------- |
| `groupID` | `String` | Group ID |
| `userID` | `String` | Group member ID |
| `muteTime` | `Number` | Muting duration in seconds.<br>For example, if the muting duration is set to 1,000, the user is muted for 1,000 seconds immediately. If the muting duration is set to 0, the user is unmuted. |

**Response**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` indicates the group profile displayed after modification.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.setGroupMemberMuteTime({
  groupID: 'group1',
  userID: 'user1',
  muteTime: 600 // The user is muted for 10 minutes. If the value of this parameter is set to 0, the user is unmuted.
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // Group profile that is displayed after modification
  console.log(imResponse.data.member); // Group member’s profile that is displayed after modification
}).catch(function(imError) {
  console.warn('setGroupMemberMuteTime error:', imError); // Information on the failure in muting the group member
});
```



### Setting or canceling a group admin

This API is used to change the role of a group member. Only the group owner has the permission for this operation.

**API name**

```js
tim.setGroupMemberRole(options)
```

**Request parameters**

`options` is of `Object` type and has the following properties:

| Name | Type | Description |
| :-------- | :----- | :----------------------------------------------------------- |
| `groupID` | `String` | Group ID |
| `userID` | `String` | Group member ID |
| `role` | `String` | Valid values: `TIM.TYPES.GRP_MBR_ROLE_ADMIN`: group admin. `TIM.TYPES.GRP_MBR_ROLE_MEMBER`: ordinary group member. |

**Response**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` indicates the group profile displayed after modification.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.setGroupMemberRole({
  groupID: 'group1',
  userID: 'user1',
  role: TIM.TYPES.GRP_MBR_ROLE_ADMIN // Set user1 as the admin of group1.
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // Group profile that is displayed after modification
  console.log(imResponse.data.member); // Group member’s profile that is displayed after modification
}).catch(function(imError) {
  console.warn('setGroupMemberRole error:', imError); // Error information
});
```



### Modifying a group member’s name card

This API is used to modify a group member’s name card.
- The group owner can set the name cards of all members.
- The group admins can set their own name cards and the name cards of ordinary group members.
- Ordinary group members can only set their own name cards.

**API name**

```js
tim.setGroupMemberNameCard(options)
```

**Request parameters**

`options` is of `Object` type and has the following properties:

| Name | Type | Description |
| :--------- | :--------------- | :------------------------- |
| `groupID` | `String` | Group ID |
| `userID` | `String<optional>` | userID of the user whose name card is to be modified. The value is the user’s own userID by default. |
| `nameCard` | `String` | - |

**Response**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` indicates the group profile displayed after modification.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.setGroupMemberNameCard({ groupID: 'group1', userID: 'user1', nameCard: 'Name card' });
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // Group profile that is displayed after being set
  console.log(imResponse.data.member); // Group member’s profile that is displayed after modification
}).catch(function(imError) {
  console.warn('setGroupMemberNameCard error:', imError); // Information on the failure in setting the group member’s name card
});
```


### Modifying a group member custom field

This API is used to modify a group member custom field.
> Ordinary group members can only modify their own custom fields.

**API name**

```js
tim.setGroupMemberCustomField(options)
```

**Request parameters**

`options` is of `Object` type and has the following properties:

| Name | Type | Description |
| :------------------ | :----------------- | :-------- |
| `groupID` | `String` | Group ID |
| `userID`  | `String<optional>` | ID of the group member. If this field is not specified, the user’s own group member custom field is modified by default. |
| `memberCustomField` | `Array<Object>` | Group member custom field to be modified |

The `memberCustomField` parameter contains the following properties:

| Name | Type | Description |
| :------ | :----------------- | :------ |
| `key` | `String` | Key of the custom field |
| `value` | `String<optional>`| Value of the custom field |

**Response**

This API returns a `Promise` object. The callback functions are as follows:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` indicates the group profile displayed after modification.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.setGroupMemberCustomField({ groupID: 'group1', memberCustomField: [{key: 'group_member_test', value: 'test'}]});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // Group profile that is displayed after being set
  console.log(imResponse.data.member); // Group member’s profile that is displayed after modification
}).catch(function(imError) {
  console.warn('setGroupMemberCustomField error:', imError); // Information on the failure in modifying the group member custom field
});
```

## Group Notifications

This API is used to send a group notification in a group when a user is invited to the group or deleted from the group. The access side can determine whether to display the message to group members or ignore all such messages.
IM provides multiple types of group notifications. For more information, see [Message.GroupTipPayload](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupTipPayload).

| Name | Type | Description |
| :---------------- | :--------------- | :------------------------------------- |
| `operatorID` | `String` | ID of the user who performs the operation |
| `operationType` | `Number` | Type of the operation |
| `userIDList` | `Array<String>` | List of relevant userIDs |
| `newGroupProfile` | `Object` | New group profile to which the group profile needs to be changed |

The parameters of a group notification are described above. The system sends a group notification to all group members at the appropriate time. For example, when a user exits or joins a group, the system sends the corresponding group notification to all group members.

## Group System Notifications

When a user applies to join a group, the group admin receives a system message about the application. The admin can then accept or reject the application, and the IM SDK sends the application result to the access side via a corresponding group system notification, which is then displayed to the user by the access side.
IM provides multiple types of system notifications. For more information, see [Types, Constants, and Meanings of Group System Notifications](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupSystemNoticePayload).

<pre>
let onGroupSystemNoticeReceived = function(event) {
  const type = event.data.type; // Type of the group system notification. For more information, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupSystemNoticePayload">Message.GroupSystemNoticePayload</a>. 
  const message = event.data.message; // Message instance of the group system notification. For more information, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html">Message</a>.
  console.log(message.payload); // Content of the message, which describes the payload of the group system notification
};
tim.on(TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED, onGroupSystemNoticeReceived);
</pre>



| Name | Type | Description |
| :-------------- | :------- | :----------------------------------------------------------- |
| `operatorID` | `String` | ID of the user who performs the operation |
| `operationType` | `Number` | Type of the operation |
| `groupProfile`  | `Object` | Profile of the relevant group |
| `handleMessage` | `Object` | Postscripts for the handling process.<br>For example, if user1 enters postscripts for an application to join group1 that requires approval, the admin of group1 will see this field in the group system notification. |

`operationType` description

| Name | Description | Recipient |
| :--- | :--------------------------------- | :---|
| 1 | A user applies to join the group. | Group admin and group owner |
| 2 | Application to join the group is approved. | Applicant |
| 3 | Application to join the group is rejected. | Applicant |
| 4 | A user is deleted from a group. | Deleted user |
| 5 | The group is disbanded. | All group members |
| 6 | The group is created. | Creator |
| 7 | A user is invited to the group. | Invitee |
| 8 | A user exits the group. | User who exits the group |
| 9 | The group admin is set. | New admin |
| 10 | The group admin is canceled. | Group admin who is canceled |
| 255 | A custom notification is triggered. | All group members by default |

The parameters of a group system notification are described above. The system sends a group system notification to all group members at appropriate times. For example, when user1 is deleted from a group, the system sends the corresponding group system notification to user1.
