## Getting the Profile of Group Members

>! The maximum number of users in each query is 50. If the length of the array passed in is greater than 50, only the first 50 users will be queried, and the rest will be discarded.

**API**

<dx-codeblock>
:::  js

tim.getGroupMemberProfile(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name                    | Type               | Description                                                  |
| ----------------------- | ------------------ | ------------------------------------------------------------ |
| groupID                 | String             | Group ID                                                     |
| userIDList              | Array              | List of IDs of the group members to be queried               |
| memberCustomFieldFilter | Array \| undefined | Filtering the custom group member field. This attribute is optional. If it is not specified, all the custom group member fields are queried by default. |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

let promise = tim.getGroupMemberProfile({
  groupID: 'group1',
  userIDList: ['user1', 'user2'], // Note: Even if you retrieve the profile of only one group member, the value must be of array type, for example, userIDList: ['user1'].
  memberCustomFieldFilter: ['group_member_custom'], // Group member custom field to query: group_member_custom
});
promise.then(function(imResponse) {
  console.log(imResponse.data.memberList); // Group member list
}).catch(function(imError){
  console.warn('getGroupMemberProfile error:', imError);
});

:::
</dx-codeblock>

## Setting the Name Card of a Group Member

>! As an audio-video group doesn't store group member information, this API is not applicable to the group.

**API**

<dx-codeblock>
:::  js

tim.setGroupMemberNameCard(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name     | Type                | Description                                                  |
| -------- | ------------------- | ------------------------------------------------------------ |
| groupID  | String              | Group ID or topic ID                                         |
| userID   | String \| undefined | It is optional. By default, the user's own name card is modified. |
| nameCard | String              | Name card of a group member                                  |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

let promise = tim.setGroupMemberNameCard({ groupID: 'group1', userID: 'user1', nameCard: 'Name card' });
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // New group profile
  console.log(imResponse.data.member); // New group member profile
}).catch(function(imError){
  console.warn('setGroupMemberNameCard error:', imError); // Failed to set the name card of the group member
});

:::
</dx-codeblock>

## Setting a Custom Group Member Field

>! Ordinary group members can only set their own custom fields.

**API**

<dx-codeblock>
:::  js

tim.setGroupMemberCustomField(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name              | Type                | Description                                                  |
| ----------------- | ------------------- | ------------------------------------------------------------ |
| groupID           | String              | Group ID or topic ID                                         |
| userID            | String \| undefined | Optional. If it is not specified, the user's own custom group member field is modified. |
| memberCustomField | Array               | Custom group member field. Its array elements are as structured below:<br/><li>key --- String --- `Key` of the custom field</li><li>value --- String --- `Value` of the custom field</li> |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

let promise = tim.setGroupMemberCustomField({ groupID: 'group1', memberCustomField: [{key: 'group_member_test', value: 'test'}]});
promise.then(function(imResponse) {
  console.log(imResponse.data.group); // New group profile
  console.log(imResponse.data.member); // New group member profile
}).catch(function(imError){
  console.warn('setGroupMemberCustomField error:', imError); // Failed to set the custom group member field
});

:::
</dx-codeblock>
