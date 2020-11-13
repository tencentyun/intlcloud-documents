## Group Overview

Instant Messaging (IM) supports multiple group types. For more information on their characteristics and limits, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). A group is identified by a unique ID that enables different operations.

## Group Management

### Obtaining your group list
This API is used to obtain your group list when you need to render or refresh **My Groups**. For more information, see [Group](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Group.html).

>!The list of groups returned by this API does not include TIM.TYPES.GRP_AVCHATROOM (live streaming groups). 

**API**

```js
tim.getGroupList();
```

**Request Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Required | Description |
| :---------------------- | :------------- | :--- | :----------------------------------------------------------- |
| `groupProfileFilter` | `Array<String>` | `<optional>` | Group profile filter. The system specifies some profile fields to retrieve by default. You can specify additional group profile fields to retrieve. Valid values:<br/>TIM.TYPES.GRP_PROFILE_OWNER_ID: group owner ID<br/>TIM.TYPES.GRP_PROFILE_CREATE_TIME: group creation time<br/>TIM.TYPES.GRP_PROFILE_LAST_INFO_TIME: the last time the group profile was modified<br/>TIM.TYPES.GRP_PROFILE_MEMBER_NUM: the number of group members<br/>TIM.TYPES.GRP_PROFILE_MAX_MEMBER_NUM: the maximum number of group members<br/>TIM.TYPES.GRP_PROFILE_JOIN_OPTION: the options for joining the group<br/>TIM.TYPES.GRP_PROFILE_INTRODUCTION: group introduction<br/>TIM.TYPES.GRP_PROFILE_NOTIFICATION: group announcement<br/>TIM.TYPES.GRP_PROFILE_MUTE_ALL_MBRS: the Mute All setting, supported by v2.6.2 and later. |

**Response**

This API returns a `Promise` object.
- The callback parameter of `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.groupList` contains the list of groups.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**
- Group profile information that is retrieved by default:
```js
// This API retrieves the following information by default: group type, group name, group profile photo, and the time of the last message.
let promise = tim.getGroupList();
promise.then(function(imResponse) {
  console.log(imResponse.data.groupList); // Group list.
}).catch(function(imError) {
  console.warn('getGroupList error:', imError); // Information on the failure in obtaining the group list.
});
```
- Other group profile information to retrieve:
```js
// If the profile fields that are retrieved by default fail to meet your requirements, you can retrieve additional profile fields by referring to the following code.
let promise = tim.getGroupList({
   groupProfileFilter: [TIM.TYPES.GRP_PROFILE_OWNER_ID],
});
promise.then(function(imResponse) {
  console.log(imResponse.data.groupList); // Group list.
}).catch(function(imError) {
  console.warn('getGroupList error:', imError); // Information on the failure in obtaining the group list.
});
```

### Obtaining the detailed group profile

For more information, see [Group](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Group.html).

**API**

```js
tim.getGroupProfile(options);
```

**Request Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Required | Description |
| :---------------------- | :------------- | :--- | :----------------------------------------------------------- |
| `groupID` | `String` | - | Group ID. |
| `groupCustomFieldFilter` | `Array<String>` | `<optional>` | The filter for group custom fields. You can specify group custom fields to retrieve. For more information, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529). |

**Response**

This API returns a `Promise` object.
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
  console.warn('getGroupProfile error:', imError); // Information on the failure in obtaining the detailed group profile.
});
```



### Creating a group

For more information, see [Group](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Group.html).

>!After this API is used to create TIM.TYPES.GRP_AVCHATROOM (live streaming group), you must call [joinGroup](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#joinGroup) to join the group and enable the messaging process.

**API**

```js
tim.createGroup(options);
```

**Request Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Required | Default Value | Description |
| :--------------- | :------------- | :--------- | :----------------------------------- | :----------------------------------------------------------- |
| `name` | `String` | - | - | Required. Group name with a maximum length of 30 bytes. |
| `type` | `String` | `<optional>` | `TIM.TYPES.GRP_WORK` | Group types include: <li>TIM.TYPES.GRP_WORK: work group (default)</li><li>TIM.TYPES.GRP_PUBLIC: social networking group</li><li>TIM.TYPES.GRP_MEETING: temporary meeting group</li><li>TIM.TYPES.GRP_AVCHATROOM: livestreaming group</li> |
| `groupID` | `String` | `<optional>` | - | Group ID. If this field is not filled in, a unique group ID will be created automatically. |
| `introduction` | `String` | `<optional>` | - | Group introduction. The value can be up to 240 bytes in length. |
| `notification` | `String` | `<optional>` | - | Group notice. The value can be up to 300 bytes in length. |
| `avatar` | `String` | `<optional>` | - | The URL of the group’s profile photo. The value can be up to 100 bytes in length. |
| `maxMemberNum` | `Number` | `<optional>` | - | The maximum number of group members. The default values are as follows: work group: 6,000, social networking group: 6,000, temporary meeting group: 6,000, livestreaming group: no limit. |
| `joinOption` | `String` | `<optional>` | `TIM.TYPES.JOIN_OPTIONS_FREE_ACCESS` | The processing method for applications to join the group. **This field cannot be specified when creating work groups, temporary meeting groups, and livestreaming groups.** For work groups, this field is always set to **Applications disabled**. For temporary meeting groups and livestreaming groups, this field is always set to **Free access**. Valid values:<br><li>TIM.TYPES.JOIN_OPTIONS_FREE_ACCESS: users can join the group freely</li><li>TIM.TYPES.JOIN_OPTIONS_NEED_PERMISSION: approval is required</li><li>TIM.TYPES.JOIN_OPTIONS_DISABLE_APPLY: users cannot join this group</li><br/>This field cannot be specified when creating TIM.TYPES.GRP_WORK, TIM.TYPES.GRP_MEETING, and TIM.TYPES.GRP_AVCHATROOM groups. Users cannot apply to join work groups and can join temporary meeting groups and livestreaming groups at will. |
| `memberList` | `Array<Object>` | `<optional>`| - | Initial group members. The maximum number is 500. This field is unavailable for livestreaming groups. For more information, see [memberList parameter description](#memberList) below. |
| `groupCustomField` | `Array<Object>` | `<optional>` | - | Group-level custom fields. No custom field is specified by default. To create a group custom field, see [Group Member Profiles](https://intl.cloud.tencent.com/document/product/1047/33529). |

<span id="memberList"></span>
`memberList` parameter description

| Name | Type | Required | Description |
| :------------------ | :------------- | :--------- | :----------------------------------------------------------- |
| `userID` | `String` | - | Required. The UserID of the group member. |
| `role` | `String` | `<optional>` | The role of the group member. The only available value is Admin, which means to add the user and set the user as an admin. |
| `memberCustomField` | `Array<Object>` | `<optional>` | Group member custom fields. No custom field is specified by default. To create a group member custom field, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529). |

**Response**

This API returns a `Promise` object.
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). You can obtain group profiles from `IMResponse.data.group`.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
// Create a work group.
let promise = tim.createGroup({
  type: TIM.TYPES.GRP_WORK,
  name: 'WebSDK',
  memberList: [{userID: 'user1'}, {userID: 'user2'}] // If memberList is specified, userID must also be specified.
});
promise.then(function(imResponse) { // Created successfully.
  console.log(imResponse.data.group); // The profile of the created group.
}).catch(function(imError) {
  console.warn('createGroup error:', imError); // Information on the failure in creating the group.
});
```

### Disbanding a group

This API is used by a group owner to disband a group.
>!The group owner cannot disband work groups.

**API**

```js
tim.dismissGroup(groupID);
```

**Request Parameters**

| Name | Type | Description |
| :-------- | :----- | :------ |
| `groupID` | `String` | Group ID. |

**Response**

This API returns a `Promise` object.
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). You can obtain the ID of the disbanded group from `IMResponse.data.groupID`.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.dismissGroup('group1');
promise.then(function(imResponse) { // Disbanded successfully.
  console.log(imResponse.data.groupID); // The ID of the disbanded group.
}).catch(function(imError) {
  console.warn('dismissGroup error:', imError); // Information on the failure in disbanding the group.
});
```

### Updating a group profile

**API**

```js
tim.updateGroupProfile(options);
```

**Request Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Required | Default | Description |
| :----------------- | :------------- | :--------- | :----------------------------------- | :----------------------------------------------------------- |
| `groupID` | `Object` | - | - | Group ID. |
| `name` | `Object` | `<optional>` | - | Group name. The value can be up to 30 bytes in length. |
| `avatar` | `Object` | `<optional>` | - | The URL of the group’s profile photo. The value can be up to 100 bytes in length. |
| `introduction` | `Object` | `<optional>` | - | Group introduction. The value can be up to 240 bytes in length. |
| `notification` | `Object` | `<optional>` | - | Group notice. The value can be up to 300 bytes in length. |
| `maxMemberNum` | `Number` | `<optional>` | - | The maximum number of group members. The maximum value is 6000. |
| `muteAllMembers` | `Boolean` | - | - | The Mute All setting. Mutes all users when set to true and unmutes all users when set to false. Supported by v2.6.2 and later. |
| `joinOption` | `String` | `<optional>` | `TIM.TYPES.JOIN_OPTIONS_FREE_ACCESS` | The processing method for applications to join the group.<br><li>TIM.TYPES.JOIN_OPTIONS_FREE_ACCESS: users can join the group freely.</li><li>TIM.TYPES.JOIN_OPTIONS_NEED_PERMISSION: approval is required</li><li>TIM.TYPES.JOIN_OPTIONS_DISABLE_APPLY: users cannot join the group</li><br/>!This property of TIM.TYPES.GRP_WORK, TIM.TYPES.GRP_MEETING, and TIM.TYPES.GRP_AVCHATROOM cannot be modified. Users cannot apply to join work groups and can join temporary meeting groups and livestreaming groups freely. |
| `groupCustomField` | `Array<Object>` | `<optional>` | - | Group-level custom field. For more information, see [`groupCustomField` parameter description](#groupCustomField).<br>No custom field is specified by default. To create a group-level custom field, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529). |

<span id="groupCustomField"></span>
`groupCustomField` parameter description

| Name | Type | Description |
| :------ | :----- | :---------------- |
| `key` | `String` | The key of the custom field. |
| `value` | `String` | The value of the custom field. |

**Response**

This API returns a `Promise` object.
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). You can obtain the modified group profile from `IMResponse.data.group`.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.updateGroupProfile({
  groupID: 'group1',
  name: 'new name', // Modify the group name.
  introduction: 'this is introduction.', // Modify the group notice.
  // Starting from v2.6.0, group members can receive group prompts about custom group field modifications and obtain related content. For more information, see Message.payload.newGroupProfile.groupCustomField.
  groupCustomField: [{ key: 'group_level', value: 'high'}] // Modify the group-level custom field.
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // The detailed group profile after modification.
}).catch(function(imError) {
  console.warn('updateGroupProfile error:', imError); // Information on the failure in modifying the group profile.
});
```

### Applying to join a group

This API is called when a user applies to join a group.

>!
- Users cannot apply to join a work group and can only be added to the group through the [addGroupMember](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#addGroupMember) method.
- TIM.TYPES.GRP_AVCHATROOM (livestreaming groups) support two ways to join a group:
 - Users join the group in the normal manner after login. All APIs in the SDK can be called normally.
 - Users join the group anonymously without login. Messages will be received, but any APIs that require authentication cannot be called.
- Only TIM.TYPES.GRP_AVCHATROOM (livestreaming groups) support anonymous group joining.
- Users can join only one livestreaming group at a time. **For example**, when a user joins live streaming group B when already in live streaming group A, the SDK quits group A first and then joins group B.

**API**

```js
tim.joinGroup(options);
```

**Request Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Required | Description |
| :------------- | :----- | :--------- | :----------------------------------------------------------- |
| `groupID` | `String` | - | - |
| `applyMessage` | `String` | - | Remarks on the application. |
| `type` | `String` | `<optional>` | The type of the group the user wants to join. Valid values:<br/><li>TIM.TYPES.GRP_PUBLIC: social networking group</li><li>TIM.TYPES.GRP_MEETING: temporary meeting group</li><li>TIM.TYPES.GRP_AVCHATROOM: livestreaming group</li> |

**Response**

This API returns a `Promise` object.
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data` contains the following property values:
	<table>
     <tr>
         <th>Name</th>  
         <th>Description</th>
     </tr>
	 <tr>
	     <td>status</td>   
	     <td>The status of the group joining process. Valid values:<ul><li>TIM.TYPES.JOIN_STATUS_WAIT_APPROVAL: waiting for the admin’s approval</li><li>TIM.TYPES.JOIN_STATUS_SUCCESS: joined successfully</li><li>TIM.TYPES.JOIN_STATUS_ALREADY_IN_GROUP: already in the group</li></ul></td>
     </tr> 
	 <tr>
	     <td>group</td>   
	     <td>The group profile displayed when the user joins the group. </td>   
     </tr> 
</table>

- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.joinGroup({ groupID: 'group1', type: TIM.TYPES.GRP_AVCHATROOM });
promise.then(function(imResponse) {
  switch (imResponse.data.status) {
    case TIM.TYPES.JOIN_STATUS_WAIT_APPROVAL: break; // Waiting for the admin’s approval.
    case TIM.TYPES.JOIN_STATUS_SUCCESS: // Joined the group successfully.
      console.log(imResponse.data.group); // The profile of the group.
      break;
    case TIM.TYPES.JOIN_STATUS_ALREADY_IN_GROUP: //Already in the group
      break;
    default: break;
  }
}).catch(function(imError){
  console.warn('joinGroup error:', imError); // Information on the failure in joining the group.
});
```

### Quitting a group

A group owner can only quit work groups. After the group owner quits, the work group has no group owner.

**API**

```js
tim.quitGroup(groupID);
```

**Request Parameters**

| Name | Type | Description |
| :-------- | :----- | :------ |
| `groupID` | `String` | Group ID. |

**Response**

This API returns a `Promise` object.
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.groupID` is the ID of the group that the user quits.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.quitGroup('group1');
promise.then(function(imResponse) {
  console.log(imResponse.data.groupID); // The ID of the group that the user quits.
}).catch(function(imError){
  console.warn('quitGroup error:', imError); // Information on the failure in quitting the group.
});
```

### Searching for a group by group ID

This API is used to search for a group by group ID.

> Note: work groups (TIM.TYPES.GRP_WORK) can not be searched for.

**API**

```js
tim.searchGroupByID(groupID);
```

**Request Parameters**

| Name | Type | Description |
| :-------- | :----- | :------ |
| `groupID` | `String` | Group ID. |

**Response**

This API returns a `Promise` object.
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` is the group profile.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.searchGroupByID('group1');
promise.then(function(imResponse) {
  const group = imResponse.data.group; // Group profile.
}).catch(function(imError) {
  console.warn('searchGroupByID error:', imError); // Information on the failure in searching for the group.
});
```

### Transferring a group
This API is used to transfer a group. Only the group owner has the permission to perform this operation.

> Note: only the group owner can transfer the ownership of a group. Livestreaming groups (TIM.TYPES.GRP_AVCHATROOM) cannot be transferred.

**API**

```js
tim.changeGroupOwner(options);
```

**Request Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Description |
| :----------- | :----- | :-------------- |
| `groupID` | `String` | The ID of the group to be transferred. |
| `newOwnerID` | `String` | The ID of the new group owner. |

**Response**

This API returns a `Promise` object.
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` is the group profile.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.changeGroupOwner({
  groupID: 'group1',
  newOwnerID: 'user2'
});
promise.then(function(imResponse) { // Transferred successfully.
  console.log(imResponse.data.group); // Group profile.
}).catch(function(imError) { // Failed to transfer the group.
  console.warn('changeGroupOwner error:', imError); // Information on the failure in transferring the group.
});
```

### Processing an application to join a group

This API is used to approve or reject an application to join a group.

>!If a group has multiple administrators, all online administrators receive a group system notification when someone [applies to join the group](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupSystemNoticePayload). If one of the administrators has approved or rejected the application, other administrators cannot change the result.

**API**

```js
tim.handleGroupApplication(options);
```

**Request Parameters**

The `options` parameter is of the `Object` type. It contains the following property values:

| Name | Type | Required | Description |
| :-------------- | :--------------------- | :--------- | :----------------------------------------------- |
| `handleAction` | `String` | - | Processing result. Agree: the application is approved. Reject: the application is rejected. |
| `handleMessage` | `String` | `<optional>` | Remarks. |
| `message` | [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html) | - | The message instance of the **Group System Notification** for an application to join a group. This instance can be obtained in the following ways:<li>The callback function parameter of the <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.GROUP_SYSTEM_NOTICE_RECERIVED">event for new group system notifications</a></li><li>The messages for system sessions</li> |

**Response**

This API returns a `Promise` object.
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` is the group profile.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.handleGroupApplication({
  handleAction: 'Agree',
  handleMessage: 'Welcome',
  message: message // The message instance of the group system notification for an application to join a group.
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // Group profile.
}).catch(function(imError){
  console.warn('handleGroupApplication error:', imError); // Error information.
});
```

### Setting the notification type for group messages

**API**

```js
tim.setMessageRemindType(options);
```

**Request Parameters**

The `options` parameter is of the `Object` type. It contains the following property values:

| Name | Type | Description |
| :------------------ | :----- | :----------------------------------------------------------- |
| `groupID` | `String` | Group ID. |
| `messageRemindType` | `String` | The notification type of group messages. Valid values:<li>TIM.TYPES.MSG_REMIND_ACPT_AND_NOTE: the SDK receives a message and throws a <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED">message receiving event</a> to notify the access side, which then sends a notification.</li><li>TIM.TYPES.MSG_REMIND_ACPT_NOT_NOTE: the SDK receives a message and throws a <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED">message receiving event</a> to notify the access side, which then does not send any notifications.</li><li>TIM.TYPES.MSG_REMIND_DISCARD: the SDK rejects a message and does not throw any <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED">message receiving events</a>.</li> |

**Response**

This API returns a `Promise` object.
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` is the group profile.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.setMessageRemindType({ groupID: 'group1', messageRemindType: TIM.TYPES.MSG_REMIND_DISCARD }); // Reject the message.
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // The group profile that is displayed after modification.
}).catch(function(imError) {
  console.warn('setMessageRemindType error:', imError);
});
```

## Group Member Management

### Getting group member list

>!
>- Starting from v2.6.2, this API can be used to pull the muting stop timestamps of group members (muteUntil). Based on its value, the access side can find out whether the member is muted and the remaining muting time.
>- In versions earlier than v2.6.2, this API can be used to get profile information including profile photo and nickname, which is sufficient to meet the rendering requirements of the group member list. To get detailed information such as member muting stop timestamp (muteUntil), use [getGroupMemberProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupMemberProfile).
>- This API is used to pull a paginated list of group members and not the complete list. To get the complete list of group members (memberNum), use [getGroupProfile](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#getGroupProfile).

For more information, see [GroupMember](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/GroupMember.html).

**API**

```js
tim.getGroupMemberList(options);
```

**Request Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Required | Default Value | Description |
| :-------- | :------- | :------------ | :----- | :--------------------------- |
| `groupID` | `String` | - | - | Group ID. |
| `count` | `Number` | `<optional> ` | `15` | The number of members whose IDs are to be retrieved. The maximum value is 100, which avoids request failure caused by excessively large returned packets. If the IDs of more than 100 members are passed in, only the IDs of the first 100 members will be retrieved. |
| `offset` | `Number` | `<optional> ` | `0` | Offset. The IDs are retrieved from 0 by default. |

**Response**

This API returns a `Promise` object.

- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.memberList` is the list of group members. For more information, see [GroupMember](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/GroupMember.html).
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```javascript
let promise = tim.getGroupMemberList({ groupID: 'group1', count: 30, offset:0 }); // Pull 30 group members starting from 0.
promise.then(function(imResponse) {
  console.log(imResponse.data.memberList); // Group member list.
}).catch(function(imError) {
  console.warn('getGroupMemberList error:', imError);
});
// Starting from v2.6.2, this API can be used to pull the muting stop timestamps of group members.
let promise = tim.getGroupMemberList({ groupID: 'group1', count: 30, offset:0 }); // Pull 30 group members starting from 0.
promise.then(function(imResponse) {
  console.log(imResponse.data.memberList); // Group member list.
  for (let groupMember of imResponse.data.memberList) {
    if (groupMember.muteUntil * 1000  > Date.now()) {
      console.log(`${groupMember.userID} muted`);
    } else {
      console.log(`${groupMember.userID} not muted`);
    }
  }
}).catch(function(imError) {
    console.warn('getGroupMemberProfile error:', imError);
});
```

### Getting the profiles of group members

>!
>- This API requires SDK v2.2.0 or later.
>- The maximum number of users in each query is 50. If the length of the array passed in is greater than 50, only the first 50 users will be queried and the rest will be discarded. 

For more information, see [GroupMember](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/GroupMember.html).

**API**

```js
tim.getGroupMemberProfile(options);
```

**Request Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Required | Description |
| :------------------------ | :--------------- | :------------ | :----------------------------------------------------------- |
| `groupID` | `String` | - | Group ID. |
| `userIDList` | `Array.<String>` | - | IDs of group members whose profiles you want to query. |
| `memberCustomFieldFilter` | `Array.<String>` | `<optional>` | The filter for group member custom fields. If this field is not specified, all the group member custom fields are queried by default. |

**Response**

This API returns a `Promise` object.

- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.memberList` is the list of group members whose profiles are queried successfully. For more information, see [GroupMember](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/GroupMember.html).
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

### Adding group members

The rules for adding group members are as follows:
-  TIM.TYPES.GRP_PRIVATE (work group): any group member can invite users to the group and acceptance by the invitee is not required.
-  TIM.TYPES.GRP_PUBLIC (social networking group)/TIM.TYPES.GRP_CHATROOM (temporary meeting group): only the app admin can invite users to the group and acceptance by the invitee is not required.
-  TIM.TYPES.GRP_AVCHATROOM (livestreaming group): no member (including the app admin) is allowed to invite any user to the group.

For more information, see [Group](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Group.html)[GroupMember](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/GroupMember.html) and [Differences in joining a group](https://intl.cloud.tencent.com/document/product/1047/33529).

**API**

```js
tim.addGroupMember(options);
```

**Request Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Description |
| :----------- | :------------- | :-------------------------------------------- |
| `groupID` | `String` | Group ID. |
| `userIDList` | `Array<String>` | An array of IDs of the group members to be added. Up to 300 group members can be added at a time. |

**Response**

This API returns a `Promise` object.
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data` contains the following property values:
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
	     <td>Group profile that is displayed after the API is called</td>   
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
  console.log(imResponse.data.successUserIDList); // The userIDList of group members that were added successfully.
  console.log(imResponse.data.failureUserIDList); // The userIDList of group members that failed to be added.
  console.log(imResponse.data.existedUserIDList); // The userIDList of group members that were already in the group.
  console.log(imResponse.data.group); // The group profile that is displayed after the group members are added.
}).catch(function(imError) {
  console.warn('addGroupMember error:', imError); // Error information.
});
```



### Deleting group members

This API is used to delete group members. Only the group owner can delete group members.

**API**

```js
tim.deleteGroupMember(options)
```

**Request Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Description |
| :----------- | :------------- | :----------------------- |
| `groupID` | `String` | Group ID. |
| `userIDList` | `Array<String>` | List of IDs of the group members that are to be deleted. |
| `reason` | `String` | Reason for deleting the one or more group members. This field is optional. |

**Response**

This API returns a `Promise` object.
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` is the updated group profile.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.deleteGroupMember({groupID: 'group1', userIDList:['user1'], reason: 'You are deleted from the group because you have violated the group rules.'});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // Group profile that is displayed after one or more group members are deleted.
  console.log(imResponse.data.userIDList); // List of userIDs of the deleted group members.
}).catch(function(imError) {
  console.warn('deleteGroupMember error:', imError); // Error information.
});
```



### Muting or unmuting a group member

This API is used to set the muting duration for a group member. You can mute or unmute a group member. The muting and unmuting features are unavailable in work groups (TIM.TYPES.GRP_WORK).
>?Only the group owner and the group admin have the permissions for this operation.
>- The group owner can mute and unmute the admin and ordinary group members.
>- The admin can mute and unmute ordinary group members.

**API**

```js
tim.setGroupMemberMuteTime(options)
```

**Request Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Description |
| :--------- | :----- | :----------------------------------------------------------- |
| `groupID` | `String` | Group ID. |
| `userID` | `String` | Group member ID. |
| `muteTime` | `Number` | The muting duration in seconds.<br>For example, if the muting duration is set to 1,000, the user is muted for 1,000 seconds immediately. If the muting duration is set to 0, the user is unmuted. |

**Response**

This API returns a `Promise` object.
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` is the group profile displayed after modification.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.setGroupMemberMuteTime({
  groupID: 'group1',
  userID: 'user1',
  muteTime: 600 // The user is muted for 10 minutes. If the value is set to 0, the user is unmuted.
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // The group profile that is displayed after modification.
  console.log(imResponse.data.member); // The group member’s profile that is displayed after modification.
}).catch(function(imError) {
  console.warn('setGroupMemberMuteTime error:', imError); // Information on the failure in muting the group member.
});
```



### Setting or canceling the admin

This API is used to change the role of a group member. Only the group owner has the permission to perform this operation.

**API**

```js
tim.setGroupMemberRole(options)
```

**Request Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Description |
| :-------- | :----- | :----------------------------------------------------------- |
| `groupID` | `String` | Group ID. |
| `userID` | `String` | Group member ID |
| `role` | `String` | Valid values: `TIM.TYPES.GRP_MBR_ROLE_ADMIN`: group admin. `TIM.TYPES.GRP_MBR_ROLE_MEMBER`: ordinary group member. |

**Response**

This API returns a `Promise` object.
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` is the group profile displayed after modification.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.setGroupMemberRole({
  groupID: 'group1',
  userID: 'user1',
  role: TIM.TYPES.GRP_MBR_ROLE_ADMIN // Set user1 as the admin of group1.
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // The group profile that is displayed after modification.
  console.log(imResponse.data.member); // The group member’s profile that is displayed after modification.
}).catch(function(imError) {
  console.warn('setGroupMemberRole error:', imError); // Error information.
});
```



### Modifying a group member’s name card

This API is used to modify a group member’s name card.
- The group owner can set the name cards of all members.
- The group admin can set its own name card and the name cards of ordinary group members.
- Ordinary group members can only set their own name cards.

**API**

```js
tim.setGroupMemberNameCard(options)
```

**Request Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Description |
| :--------- | :--------------- | :------------------------- |
| `groupID` | `String` | Group ID. |
| `userID` | `String<optional>` | The userID of the user whose name card is to be modified. The value is the user’s own userID by default. |
| `nameCard` | `String` | - |

**Response**

This API returns a `Promise` object.
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` is the group profile displayed after modification.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.setGroupMemberNameCard({ groupID: 'group1', userID: 'user1', nameCard: 'Name card' });
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // The group profile that is displayed after modification.
  console.log(imResponse.data.member); // The group member’s profile that is displayed after modification.
}).catch(function(imError) {
  console.warn('setGroupMemberNameCard error:', imError); // Information on the failure in setting a group member’s name card.
});
```


### Modifying a group member custom field

This API is used to modify a group member custom field.
> Ordinary group members can only modify their own custom fields.

**API**

```js
tim.setGroupMemberCustomField(options)
```

**Request Parameters**

`options` is of the `Object` type. Its values are as follows:

| Name | Type | Description |
| :------------------ | :----------------- | :-------- |
| `groupID` | `String` | Group ID. |
| `userID`  | `String<optional>` | The ID of the group member. If this field is not specified, the user’s own group member custom field is modified by default. |
| `memberCustomField` | `Array<Object>` | The group member custom field to be modified. |

The `memberCustomField` parameter contains the following property values:

| Name | Type | Description |
| :------ | :----------------- | :------ |
| `key` | `String` | The key of the custom field. |
| `value` | `String<optional>`| The value of the custom field. |

**Response**

This API returns a `Promise` object.
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` is the group profile displayed after modification.
- The callback parameter of `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.setGroupMemberCustomField({ groupID: 'group1', memberCustomField: [{key: 'group_member_test', value: 'test'}]});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // The group profile that is displayed after modification.
  console.log(imResponse.data.member); // The group member’s profile that is displayed after modification.
}).catch(function(imError) {
  console.warn('setGroupMemberCustomField error:', imError); // Information on the failure in modifying the group member custom field.
});
```

## Group Notification

This API is used to send a group notification in a group when a user is invited to the group or deleted from the group. The access side can determine whether to display the message to group members as needed or ignore all the messages.
IM provides multiple types of group notifications. For more information, see [Message.GroupTipPayload](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupTipPayload).

| Name | Type | Description |
| :---------------- | :--------------- | :------------------------------------- |
| `operatorID` | `String` | The ID of the user who performs the operation. |
| `operationType` | `Number` | The type of the operation. |
| `userIDList` | `Array<String>` | List of relevant userIDs. |
| `newGroupProfile` | `Object` | The new group profile to which the group profile needs to be changed. |

The parameters of a group notification are described above. The system sends a group notification to all group members at the appropriate time. For example, when a user quits or joins a group, the system sends the corresponding group notification to all group members.

## Group System Notification

When a user applies to join a group, the group admin receives a system message about the application. The admin can accept or reject the application, and the IM SDK sends the result to the access side via a corresponding group system notification, which is then displayed to the user by the access side.
IM provides multiple types of system notifications. For more information, see [Types, Constants, and Meanings of Group System Notifications](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupSystemNoticePayload).

<pre>
let onGroupSystemNoticeReceived = function(event) {
  const type = event.data.type; // The type of the group system notification. For more information, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupSystemNoticePayload">Message.GroupSystemNoticePayload</a>. 
  const message = event.data.message; // The message instance of the group system notification. For more information, see <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html">Message</a>.
  console.log(message.payload); // The content of the message. This describes the payload of the group system notification.
};
tim.on(TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED, onGroupSystemNoticeReceived);
</pre>



| Name | Type | Description |
| :-------------- | :------- | :----------------------------------------------------------- |
| `operatorID` | `String` | The ID of the user who performs the operation. |
| `operationType` | `Number` | The type of the operation. |
| `groupProfile`  | `Object` | The profile of the relevant group. |
| `handleMessage` | `Object` | Remarks on the processing.<br>For example, if user1 enters remarks on an application to join group1 that requires approval, the admin of group1 will see this field in the group system notification. |

`operationType` description

| Name | Description | Recipient |
| :--- | :--------------------------------- | :---|
| 1 | A user applies to join the group. | The group admin and the group owner |
| 2 | Application to join the group is approved. | The applicant |
| 3 | Application to join group is rejected. | The applicant |
| 4 | A user is deleted from a group. | The user who is deleted |
| 5 | The group is deleted. | All group members |
| 6 | The group is created. | The creator |
| 7 | A user is invited to the group. | The invitee |
| 8 | A user quits the group. | The user who quits the group |
| 9 | The admin is modified. | The new admin |
| 10 | The admin is canceled. | The admin who is canceled |
| 255 | A custom notification is triggered. | All group members by default |

The parameters of a group system notification are described above. The system sends a group system notification to all group members at the appropriate time. For example, when user1 is deleted from a group, the system sends the corresponding group system notification to user1.
