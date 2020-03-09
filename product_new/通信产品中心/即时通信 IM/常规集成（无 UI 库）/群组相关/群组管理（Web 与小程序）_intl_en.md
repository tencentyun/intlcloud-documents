## Group Overview

Instant Messaging (IM) supports multiple group types. For more information on their characteristics and limits, see the [Group System](https://intl.cloud.tencent.com/zh/document/product/1047/33529). A group is identified by a unique ID, which allows for different operations.

## Group Management

### Obtaining the list of groups you have joined
When you need to render or refresh **My group list**, call this API to obtain the group list. For more information, see [Group](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Group.html).

**API name**

```js
tim.getGroupList();
```

**Request parameters**

The `options` parameter is of the `Object` type. The property values that it contains are shown in the following table:

| Name | Type | Property | Description |
| :---------------------- | :------------- | :--- | :----------------------------------------------------------- |
| `groupProfileFilter` | `Array<String>` | `<optional>` | Group information filter. Specify additional group information fields to pull in addition to those that are pulled by default. The following values are supported:<br/>TIM.TYPES.GRP_PROFILE_OWNER_ID: group owner ID<br/>TIM.TYPES.GRP_PROFILE_CREATE_TIME: group creation time<br/>TIM.TYPES.GRP_PROFILE_LAST_INFO_TIME: last modification time of the group information<br/>TIM.TYPES.GRP_PROFILE_MEMBER_NUM: number of group members<br/>TIM.TYPES.GRP_PROFILE_MAX_MEMBER_NUM: maximum number of group members<br/>TIM.TYPES.GRP_PROFILE_JOIN_OPTION: option for joining groups<br/>TIM.TYPES.GRP_PROFILE_INTRODUCTION: group introduction<br/>TIM.TYPES.GRP_PROFILE_NOTIFICATION: group announcement. |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). The group list can be obtained from `IMResponse.data.groupList`.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**
- Pull default information:
```js
// This API pulls the following information by default: the group type, group name, group profile photo, and time of the last message.
let promise = tim.getGroupList();
promise.then(function(imResponse) {
  console.log(imResponse.data.groupList); // Group list
}).catch(function(imError) {
  console.warn('getGroupList error:', imError); // Information on failure to obtain the group list
});
```
- Pull other information:
```js
// You can pull additional information fields other than the default ones as needed by referring to the following code.
let promise = tim.getGroupList({
   groupProfileFilter: [TIM.TYPES.GRP_PROFILE_OWNER_ID],
});
promise.then(function(imResponse) {
  console.log(imResponse.data.groupList); // Group list
}).catch(function(imError) {
  console.warn('getGroupList error:', imError); // Information on failure to obtain the group list
});
```

### Obtaining detailed group information

For more information, see [Group](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Group.html).

**API name**

```js
tim.getGroupProfile(options);
```

**Request parameters**

The `options` parameter is of the `Object` type. The property values that it contains are shown in the following table:

| Name | Type | Property | Description |
| :---------------------- | :------------- | :--- | :----------------------------------------------------------- |
| `groupID` | `String` | - | Group ID |
| `groupCustomFieldFilter`  | `Array<String>` | `<optional>` | Group custom field filter for obtaining the group custom fields that you specify. For more information, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). Group information can be obtained from `IMResponse.data.group`.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.getGroupProfile({
  groupID: 'group1',
  groupCustomFieldFilter: ['key1','key2']
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group);
}).catch(function(imError) {
  console.warn('getGroupProfile error:', imError); // Information on failure to obtain detailed group information
});
```



### Creating a group

For more information, see [Group](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Group.html).

>After creating TIM.TYPES.GRP_AVCHATROOM (an AVChatRoom group) through this API, you need to call [joinGroup](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/SDK.html#joinGroup) to join the group before messaging becomes available.

**API name**

```js
tim.createGroup(options);
```

**Request parameters**

The `options` parameter is of the `Object` type. The property values that it contains are shown in the following table:

| Name | Type | Property | Default Value | Description |
| :--------------- | :------------- | :--------- | :----------------------------------- | :----------------------------------------------------------- |
| `name` | `String` | - | - | A required property, which indicates the group name with a maximum length of 30 bytes |
| `type` | `String` | `<optional>` | `TIM.TYPES.GRP_PRIVATE` | Group type, which can be: <li>TIM.TYPES.GRP_PRIVATE: Private (default)</li><li>TIM.TYPES.GRP_PUBLIC: Public<br/>TIM.TYPES.GRP_CHATROOM: ChatRoom</li><li>TIM.TYPES.GRP_AVCHATROOM: AVChatRoom</li> |
| `groupID` | `String` | `<optional>` | - | Group ID. If this field is not specified, a unique group ID is created automatically. |
| `introduction` | `String` | `<optional>` | - | Group introduction with a maximum length of 240 bytes |
| `notification` | `String` | `<optional>` | - | Group announcement with a maximum length of 300 bytes |
| `avatar` | `String` | `<optional>` | - | URL of the group profile photo with a maximum length of 100 bytes |
| `maxMemberNum` | `Number` | `<optional>` | - | Maximum number of group members. Default values for different group types are as follows: Private: 200, Public: 2,000, ChatRoom: 6,000, AVChatRoom: unlimited. |
| `joinOption` | `String` | `<optional>` | `TIM.TYPES.JOIN_OPTIONS_FREE_ACCESS` | Handling method of group joining applications. **This field cannot be set when you create a Private, ChatRoom, or AVChatRoom group.** For Private groups, the value of this field is fixed to "disallow to join". For ChatRoom and AVChatRoom groups, the value of this field is fixed to "free access".<br><li>TIM.TYPES.JOIN_OPTIONS_FREE_ACCESS: free access</li><li>TIM.TYPES.JOIN_OPTIONS_NEED_PERMISSION: approval required</li><li>TIM.TYPES.JOIN_OPTIONS_DISABLE_APPLY: disallow to join</li> |
| `memberList` | `Array<Object>` | `<optional>`| - | List of initial members. The maximum number of initial members is limited to 500. You cannot add members when creating AVChatRoom groups. For more information, see [memberList parameter description](#memberList) below. |
| `groupCustomField` | `Array<Object>` | `<optional>` | - | Group custom field. There are no custom fields by default. To enable custom fields, see [Group Member Information](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

<span id="memberList"></span>
`memberList` parameter description

| Name | Type | Property | Description |
| :------------------ | :------------- | :--------- | :----------------------------------------------------------- |
| `userID` | `String` | - | A required property, which indicates the UserID of the group member |
| `role` | `String` | `<optional>` | Group member role. The only available value is Admin, which means to add the user and set the user as an admin. |
| `memberCustomField` | `Array<Object>` | `<optional>` | Group member custom field. There are no custom fields by default. To enable custom fields, see [Custom Fields](https://cloud.tencent.com/document/product/269/1502#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). Group information can be obtained from `IMResponse.data.group`.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
// Create a private group
let promise = tim.createGroup({
  type: TIM.TYPES.GRP_PRIVATE,
  name: 'WebSDK',
  memberList: [{userID: 'user1'}, {userID: 'user2'}] // If memberList is specified, userID must be specified too.
});
promise.then(function(imResponse) { // Created successfully
  console.log(imResponse.data.group); // Information of the created group
}).catch(function(imError) {
  console.warn('createGroup error:', imError); // Information on failure to create the group
});
```

### Dismissing a group

The group owner can call this API to dismiss a group.
>Group owners cannot dismiss Private groups.

**API name**

```js
tim.dismissGroup(groupID);
```

**Request parameters**

| Name | Type | Description |
| :-------- | :----- | :------ |
| `groupID` | `String` | Group ID |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). The ID of the dismissed group can be obtained from `IMResponse.data.groupID`.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.dismissGroup('group1');
promise.then(function(imResponse) { // Dismissed successfully
  console.log(imResponse.data.groupID); // ID of the dismissed group
}).catch(function(imError) {
  console.warn('dismissGroup error:', imError); // Information on failure to dismiss the group
});
```

### Updating group information

**API name**

```js
tim.updateGroupProfile(options);
```

**Request parameters**

The `options` parameter is of the `Object` type. The property values that it contains are shown in the following table:

| Name | Type | Property | Default | Description |
| :----------------- | :------------- | :--------- | :----------------------------------- | :----------------------------------------------------------- |
| `groupID` | `Object` | - | - | Group ID |
| `name` | `Object` | `<optional>` | - | Group name with a maximum length of 30 bytes |
| `avatar` | `Object` | `<optional>` | - | Group profile photo URL with a maximum length of 100 bytes |
| `introduction` | `Object` | `<optional>` | - | Group introduction with a maximum length of 240 bytes |
| `notification` | `Object` | `<optional>` | - | Group announcement with a maximum length of 300 bytes |
| `maxMemberNum` | `Number` | `<optional>` | - | Maximum number of group members, which is limited to 6,000 |
| `joinOption` | `String` | `<optional>` | `TIM.TYPES.JOIN_OPTIONS_FREE_ACCESS` | Handling method of group joining applications.<br>**This field cannot be set when you modify the group information of Private, ChatRoom, and AVChatRoom groups**. For Private groups, the value of this field is fixed to "disallow to join". For ChatRoom and AVChatRoom groups, the value of this field is fixed to "free access".<li>TIM.TYPES.JOIN_OPTIONS_FREE_ACCESS: free access</li><li>TIM.TYPES.JOIN_OPTIONS_NEED_PERMISSION: approval required</li><li>TIM.TYPES.JOIN_OPTIONS_DISABLE_APPLY: disallow to join</li> |
| `groupCustomField` | `Array<Object>` | `<optional>` | - | Group custom field. For more information, see [`groupCustomField` parameter description](#groupCustomField) below.<br>There are no custom fields by default. To enable custom fields, see [Custom Fields](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |

<span id="groupCustomField"></span>
`groupCustomField` parameter description

| Name | Type | Description |
| :------ | :----- | :---------------- |
| `key` | `String` | Key of the custom field |
| `value` | `String` | Value of the custom field |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). The modified group information can be obtained from `IMResponse.data.group`.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.updateGroupProfile({
  groupID: 'group1',
  name: 'new name', // Modify the group name
  introduction: 'this is introduction.', // Modify the group introduction
  groupCustomField: [{ key: 'group_level', value: 'high'}] // Modify the group custom field
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // Detailed group information after modification
}).catch(function(imError) {
  console.warn('updateGroupProfile error:', imError); // Information on failure to modify group information
});
```

### Applying to join a group

Users can be added to Private groups only by invitation but not application.

**API name**

```js
tim.joinGroup(options);
```

**Request parameters**

The `options` parameter is of the `Object` type. The property values that it contains are shown in the following table:

| Name | Type | Property | Description |
| :------------- | :----- | :--------- | :----------------------------------------------------------- |
| `groupID` | `String` | - | - |
| `applyMessage` | `String` | - | Postscript |
| `type` | `String` | `<optional>` | Type of the group that the user will be added to. This field is required if the user is added to AVChatRoom groups. Valid values:<br/><li>TIM.TYPES.GRP_PUBLIC: Public</li><li>TIM.TYPES.GRP_CHATROOM: ChatRoom</li><li>TIM.TYPES.GRP_AVCHATROOM: AVChatRoom</li> |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data` contains the following property values:
	<table>
     <tr>
         <th>Name</th>  
         <th>Meaning</th>
     </tr>
	 <tr>
	     <td>status</td>   
	     <td>Group joining state, which can be: <ul><li>TIM.TYPES.JOIN_STATUS_WAIT_APPROVAL: waiting for admin’s approval</li><li>TIM.TYPES.JOIN_STATUS_SUCCESS: joined successfully</li><li>TIM.TYPES.JOIN_STATUS_ALREADY_IN_GROUP: already in group</li></ul></td>
     </tr> 
	 <tr>
	     <td>group</td>   
	     <td>Group information after joining the group</td>   
     </tr> 
</table>

- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.joinGroup({ groupID: 'group1', type: TIM.TYPES.GRP_AVCHATROOM });
promise.then(function(imResponse) {
  switch (imResponse.data.status) {
    case TIM.TYPES.JOIN_STATUS_WAIT_APPROVAL: break; // Waiting for the admin to approve
    case TIM.TYPES.JOIN_STATUS_SUCCESS: // Joined the group successfully
      console.log(imResponse.data.group); // Information of the joined group
      break;
    default: break;
  }
}).catch(function(imError){
  console.warn('joinGroup error:', imError); // Information on failure to join the group
});
```

### Quitting a group

Group owners can only quit Private groups. After the group owner quits, the Private group has no group owner.

**API name**

```js
tim.quitGroup(groupID);
```

**Request parameters**

| Name | Type | Description |
| :-------- | :----- | :------ |
| `groupID` | `String` | Group ID |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.groupID` indicates the ID of the quit group.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.quitGroup('group1');
promise.then(function(imResponse) {
  console.log(imResponse.data.groupID); // ID of the quit group
}).catch(function(imError){
  console.warn('quitGroup error:', imError); // Information on failure to quit the group
});
```

### Searching for a group by group ID

Private groups cannot be searched for.

**API name**

```js
tim.searchGroupByID(groupID);
```

**Request parameters**

| Name | Type | Description |
| :-------- | :----- | :------ |
| `groupID` | `String` | Group ID |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` indicates the group information.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.searchGroupByID('group1');
promise.then(function(imResponse) {
  const group = imResponse.data.group; // Group information
}).catch(function(imError) {
  console.warn('searchGroupByID error:', imError); // Information on failure to search for the group
});
```

### Transferring a group
Only the group owner can transfer the ownership of a group. AVChatRoom groups cannot be transferred.

**API name**

```js
tim.changeGroupOwner(options);
```

**Request parameters**

The `options` parameter is of the `Object` type. The property values that it contains are shown in the following table:

| Name | Type | Description |
| :----------- | :----- | :-------------- |
| `groupID` | `String` | ID of the group to be transferred |
| `newOwnerID` | `String` | ID of the new group owner |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` indicates the group information.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.changeGroupOwner({
  groupID: 'group1',
  newOwnerID: 'user2'
});
promise.then(function(imResponse) { // Transferred successfully
  console.log(imResponse.data.group); // Group information
}).catch(function(imError) { // Failed to transfer
  console.warn('changeGroupOwner error:', imError); // Information on failure to transfer the group
});
```

### Processing applications to join a group

When a user applies to join a group that requires admin approval, the admin or group owner receives a **group system notification message** about the application. For more information, see [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html).

**API name**

```js
tim.handleGroupApplication(options);
```

**Request parameters**

The `options` parameter is of the `Object` type. It contains the following property values:

| Name | Type | Property | Description |
| :-------------- | :--------------------- | :--------- | :----------------------------------------------- |
| `handleAction` | `String` | - | Processing result: Agree/Reject |
| `handleMessage` | `String` | `<optional>` | Postscript |
| `message` | [Message](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html) | - | Message instance of the **group system notification message** for an application to join a group. This instance can be obtained from: <li>the parameter of the <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.GROUP_SYSTEM_NOTICE_RECERIVED">new group system notification event</a> callback</li><li>the message list of a system conversation</li>. |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` indicates the group information.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.handleGroupApplication({
  handleAction: 'Agree',
  handleMessage: 'Welcome',
  message: message // Message instance of the group system notification message for an application to join a group
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // Group information
}).catch(function(imError){
  console.warn('handleGroupApplication error:', imError); // Error information
});
```

### Setting the notification type of group messages

**API name**

```js
tim.setMessageRemindType(options);
```

**Request parameters**

The `options` parameter is of the `Object` type. It contains the following property values:

| Name | Type | Description |
| :------------------ | :----- | :----------------------------------------------------------- |
| `groupID` | `String` | Group ID |
| `messageRemindType` | `String` | Group message notification type, which can be: <li>TIM.TYPES.MSG_REMIND_ACPT_AND_NOTE: the SDK receives a message and throws a <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED">message receiving event</a> to notify the access side, which then delivers a notification</li><li>TIM.TYPES.MSG_REMIND_ACPT_NOT_NOTE: the SDK receives a message and throws a <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED">message receiving event</a> to notify the access side, which does not subsequently deliver a notification</li><li>TIM.TYPES.MSG_REMIND_DISCARD: the SDK rejects a message and does not throw a <a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/module-EVENT.html#.MESSAGE_RECEIVED">message receiving event</a></li> |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` indicates the group information.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.setMessageRemindType({ groupID: 'group1', messageRemindType: TIM.TYPES.MSG_REMIND_DISCARD }); // Rejection message
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // Group information after configuration
}).catch(function(imError) {
  console.warn('setMessageRemindType error:', imError);
});
```

## Group Member Management

### Obtaining a list of group members

**API name**

```js
tim.getGroupMemberList(options);
```

**Request parameters**

The `options` parameter is of the `Object` type. The property values that it contains are shown in the following table:

| Name | Type | Property | Default Value | Description |
| :-------- | :------- | :------------ | :----- | :--------------------------- |
| `groupID` | `String` | - | - | Group ID |
| `count` | `Number` | `<optional> ` | `15` | Number of members to be pulled. The maximum number of pulled members is limited to 100 to avoid request failure due to large returned packets. If more than 100 members are passed in, only the first 100 will be pulled. |
| `offset` | `Number` | `<optional> ` | `0` | Offset. A pull starts from offset 0 by default. |

**Returned value**

This API returns `Promise` objects:

- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.memberList` indicates the group member list. For more information, see [GroupMember](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/GroupMember.html).
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

### Obtaining group member information

**API name**

```js
tim.getGroupMemberProfile(options);
```

**Request parameters**

The `options` parameter is of the `Object` type. The property values that it contains are shown in the following table:

| Name | Type | Property | Description |
| :------------------------ | :--------------- | :------------ | :----------------------------------------------------------- |
| `groupID` | `String` | - | Group ID |
| `userIDList` | `Array.<String>` | - | List of group member IDs to be queried |
| `memberCustomFieldFilter` | `Array.<String>` | `<optional>` | Filter for group member custom fields, which is optional. If not specified, all members’ custom fields are queried by default. |

**Returned value**

This API returns `Promise` objects:

- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.memberList` indicates the list of group members that are queried successfully. For more information, see [GroupMember](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/GroupMember.html).
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

### Adding group members

Detailed group member addition rules are as follows:

- For Private groups: any group member can invite and add users to the group without prior approval of the invitees.
- For Public and ChatRoom groups: only the app admin can invite and add users to the group without prior approval of the invitees.
- For AVChatRoom groups: none is allowed to invite users to the group, including the app admin.

**API name**

```js
tim.addGroupMember(options);
```

**Request parameters**

The `options` parameter is of the `Object` type. The property values that it contains are shown in the following table:

| Name | Type | Description |
| :----------- | :------------- | :-------------------------------------------- |
| `groupID` | `String` | Group ID |
| `userIDList` | `Array<String>` | Array of the IDs of the members to be added. Up to 500 members can be added at a time. |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data` contains the following property values:
	<table>
     <tr>
         <th nowrap="nowrap">Name</th>  
         <th>Type</th>  
         <th  nowrap="nowrap">Meaning</th>  
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
	     <td>List of userIDs that are already in the group</td>   
     </tr> 
	 <tr>      
         <td>group</td>   
	     <td><a href="https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Group.html">Group</a></td>   
	     <td>Group information after the API is called</td>   
     </tr> 
</table>

- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.addGroupMember({
  groupID: 'group1',
  userIDList: ['user1','user2','user3']
});
promise.then(function(imResponse) {
  console.log(imResponse.data.successUserIDList); // userIDList of members that were added successfully
  console.log(imResponse.data.failureUserIDList); // userIDList of members that failed to be added
  console.log(imResponse.data.existedUserIDList); // userIDList of members that are already in the group
  console.log(imResponse.data.group); // Group information after the members are added
}).catch(function(imError) {
  console.warn('addGroupMember error:', imError); // Error information
});
```



### Deleting group members

This API is used to delete group members. The group owner can remove group members.

**API name**

```js
tim.deleteGroupMember(options)
```

**Request parameters**

The `options` parameter is of the `Object` type. The property values that it contains are shown in the following table:

| Name | Type | Description |
| :----------- | :------------- | :----------------------- |
| `groupID` | `String` | Group ID |
| `userIDList` | `Array<String>` | List of the IDs of the group members to be deleted |
| `reason` | `String` | Reason for removing members (optional) |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` indicates the updated group information.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.deleteGroupMember({groupID: 'group1', userIDList:['user1'], reason: 'You are removed from the group due to violation!'});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // Group information after the deletion
  console.log(imResponse.data.userIDList); // List of the userIDs of the deleted members
}).catch(function(imError) {
  console.warn('deleteGroupMember error:', imError); // Error information
});
```



### Muting or unmuting members

This API is used to set a muting period for group members and mute or unmute group members. Members of TIM.TYPES.GRP_PRIVATE groups (Private groups) cannot be muted.
>Only the group owner and admin have the permission for this operation.
>- The group owner can mute or unmute admins and ordinary group members.
>- The admin can mute or unmute ordinary group members.

**API name**

```js
tim.setGroupMemberMuteTime(options)
```

**Request parameters**

The `options` parameter is of the `Object` type. The property values that it contains are shown in the following table:

| Name | Type | Description |
| :--------- | :----- | :----------------------------------------------------------- |
| `groupID` | `String` | Group ID |
| `userID` | `String` | Group member ID |
| `muteTime` | `Number` | Muting period in seconds.<br>For example, if the muting period is set to 1,000, the user is muted for 1,000 seconds immediately. If the muting period is set to 0, the user is unmuted. |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` indicates the modified group information.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.setGroupMemberMuteTime({
  groupID: 'group1',
  userID: 'user1',
  muteTime: 600 // Mute the user for 10 minutes. If the value is set to 0, the user is unmuted.
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // Group information after modification
  console.log(imResponse.data.member); // Group member information after modification
}).catch(function(imError) {
  console.warn('setGroupMemberMuteTime error:', imError); // Information on failure to mute members
});
```



### Setting or canceling an admin

This API is used to change a user’s role in a group. Only the group owner has the permission to perform this operation.

**API name**

```js
tim.setGroupMemberRole(options)
```

**Request parameters**

The `options` parameter is of the `Object` type. The property values that it contains are shown in the following table:

| Name | Type | Description |
| :-------- | :----- | :----------------------------------------------------------- |
| `groupID` | `String` | Group ID |
| `userID` | `String` | Group member ID |
| `role` | `String` | Valid values: `TIM.TYPES.GRP_MBR_ROLE_ADMIN` (group admin) and `TIM.TYPES.GRP_MBR_ROLE_MEMBER` (ordinary group member) |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` indicates the modified group information.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.setGroupMemberRole({
  groupID: 'group1',
  userID: 'user1',
  role: TIM.TYPES.GRP_MBR_ROLE_ADMIN // Set user1 as the admin of group1
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // Group information after modification
  console.log(imResponse.data.member); // Group member information after modification
}).catch(function(imError) {
  console.warn('setGroupMemberRole error:', imError); // Error information
});
```



### Modifying a member’s name card in a group

This API is used to set a member’s name card in a group.
- The group owner can set the name cards of all members.
- Group admins can set the name cards of themselves and ordinary group members.
- Ordinary group members can only set their own name cards.

**API name**

```js
tim.setGroupMemberNameCard(options)
```

**Request parameters**

The `options` parameter is of the `Object` type. The property values that it contains are shown in the following table:

| Name | Type | Description |
| :--------- | :--------------- | :------------------------- |
| `groupID` | `String` | Group ID |
| `userID` | `String<optional>` | An optional property, whose value is your own userID by default |
| `nameCard` | `String` | - |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` indicates the modified group information.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.setGroupMemberNameCard({ groupID: 'group1', userID: 'user1', nameCard: 'user’s name card' });
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // Group information after configuration
  console.log(imResponse.data.member); // Group member information after modification
}).catch(function(imError) {
  console.warn('setGroupMemberNameCard error:', imError); // Information on failure to set the member’s name card in the group
});
```


### Modifying custom fields

This API is used to set group member custom fields.
>Ordinary group members can only set their own custom fields.

**API name**

```js
tim.setGroupMemberCustomField(options)
```

**Request parameters**

The `options` parameter is of the `Object` type. The property values that it contains are shown in the following table:

| Name | Type | Description |
| :------------------ | :----------------- | :-------- |
| `groupID` | `String` | Group ID |
| `userID`  | `String<optional>` | Group member ID (optional). If not specified, your own userID is used by default. |
| `memberCustomField` | `Array<Object>` | Group member custom field |

`memberCustomField` contains the following property values:

| Name | Type | Description |
| :------ | :----------------- | :------ |
| `key` | `String` | Key of the custom field |
| `value` | `String<optional>`| Value of the custom field |

**Returned value**

This API returns `Promise` objects:
- The callback function parameter for `then` is [IMResponse](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMResponse). `IMResponse.data.group` indicates the modified group information.
- The callback function parameter for `catch` is [IMError](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/global.html#IMError).

**Example**

```js
let promise = tim.setGroupMemberCustomField({ groupID: 'group1', memberCustomField: [{key: 'group_member_test', value: 'test'}]});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // Group information after configuration
  console.log(imResponse.data.member); // Group member information after modification
}).catch(function(imError) {
  console.warn('setGroupMemberCustomField error:', imError); // Information on failure to set the group member custom field
});
```

## Group Prompt Messages

When a user is invited to a group or removed from a group, the system sends a prompt message in the group. The access side can display the message to group members as needed or ignore it.
There are multiple types of group prompt messages. For more information, see [Message.GroupTipPayload](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupTipPayload).

| Name | Type | Description |
| :---------------- | :--------------- | :------------------------------------- |
| `operatorID` | `String` | ID of the operator |
| `operationType` | `Number` | Operation type |
| `userIDList` | `Array<String>` | List of userIDs |
| `newGroupProfile` | `Object` | In the event of group information modifications, this field stores the modified group information. |

The content structure of group prompt messages. The system sends group prompt messages to all group members at appropriate times. For example, when a user quits or joins the group, the system sends the corresponding group prompt message to all group members.

## Group System Notifications

When a user applies to join a group, the group admin receives a system message about the application. The admin can accept or reject the application, and the IM SDK sends the corresponding group system message to the access side, which displays the message to users.
There are multiple types of group notification messages. For more information, see [Message.GroupSystemNoticePayload](https://imsdk-1252463788.file.myqcloud.com/IM_DOC/Web/Message.html#.GroupSystemNoticePayload).

```javascript
let onGroupSystemNoticeReceived = function(event) {
  const type = event.data.type; // Type of the group system notification. For details, see the constants and meanings of group system notification types. 
  const message = event.data.message; // Message instance of the group system notification. For details, see Message.
  console.log(message.payload); // Content of the message, which describes the payload of the group system notification message
};
tim.on(TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED, onGroupSystemNoticeReceived);
```



| Name | Type | Description |
| :-------------- | :------- | :----------------------------------------------------------- |
| `operatorID` | `String` | ID of the operator |
| `operationType` | `Number` | Operation type |
| `groupProfile`  | `Object` | Group information |
| `handleMessage` | `Object` | Postscript<br>For example, if user1 applies to join group1 that requires approval and user1 enters a postscript for the application, the admin of group1 will see this field in the group system notification. |

`operationType` description

| Name | Description | Recipient |
| :--- | :--------------------------------- | :---|
| 1 | User applies to join the group | Group admin or group owner |
| 2 | Application to join the group is approved | Applicant |
| 3 | Application to join the group is rejected | Applicant |
| 4 | User is removed from the group | Removed user |
| 5 | Group is dismissed | All group members |
| 6 | Group is created | Creator |
| 7 | User is invited to the group | Invitee |
| 8 | User quits the group | User who quits the group |
| 9 | Admin is set | Admin who is newly set |
| 10 | Admin is canceled | Admin who is canceled |
| 255 | Custom notification | All members by default |

The content structure of group system notifications. The system sends group system notifications to all group members at appropriate times. For example, when user1 is removed from a group, the system sends the corresponding group system message to user1.
