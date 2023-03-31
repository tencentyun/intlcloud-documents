## Feature Description

The group profile refers to the information about the group, the attributes of which are in the [Group](https://web.sdk.qcloud.com/im/doc/en/Group.html) core class.

## Getting the Group Profile

**API**

<dx-codeblock>
:::  js

tim.getGroupProfile(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name                   | Type               | Description                                                  |
| ---------------------- | ------------------ | ------------------------------------------------------------ |
| groupID                | String             | Group ID                                                     |
| groupCustomFieldFilter | Array \| undefined | Custom group field filter. You can specify the custom group field to be obtained. For more information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

let promise = tim.getGroupProfile({ groupID: 'group1', groupCustomFieldFilter: ['key1','key2'] });
promise.then(function(imResponse) {
  console.log(imResponse.data.group);
}).catch(function(imError){
  console.warn('getGroupProfile error:', imError); // Failed to obtain the detailed group profile
});

:::
</dx-codeblock>

## Modifying the Group Profile

**API**

<dx-codeblock>
:::  js

tim.updateGroupProfile(options);

:::
</dx-codeblock>

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name             | Type                 | Description                                                  |
| ---------------- | -------------------- | ------------------------------------------------------------ |
| groupID          | String               | Group ID                                                     |
| name             | String \| undefined  | Group name, which can contain up to 30 bytes.                |
| avatar           | String \| undefined  | Group profile photo URL, which can contain up to 100 bytes.  |
| introduction     | String \| undefined  | Group introduction, which can contain up to 240 bytes.       |
| notification     | String \| undefined  | Group notice, which can contain up to 300 bytes.             |
| maxMemberNum     | Number \| undefined  | Maximum number of group members, which is 6,000.             |
| muteAllMembers   | Boolean \| undefined | Muting all. Valid values: `true`: mute all; `false`: unmute all. It is supported by v2.6.2 or later. |
| joinOption       | String               | Method to join a group. Valid values:<br/><li>TIM.TYPES.JOIN_OPTIONS_FREE_ACCESS (free to join)</li><li>TIM.TYPES.JOIN_OPTIONS_NEED_PERMISSION (approval required)</li><li>TIM.TYPES.JOIN_OPTIONS_DISABLE_APPLY (no group join)</li>Note: It cannot be modified for `TIM.TYPES.GRP_WORK`, `TIM.TYPES.GRP_MEETING`, and `TIM.TYPES.GRP_AVCHATROOM` groups. Work groups cannot be joined on request, and meeting groups and audio-video groups can be joined freely. |
| groupCustomField | Array \| undefined   | Custom group field, which is unavailable by default. For more information on how to enable a custom group field, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

let promise = tim.updateGroupProfile({
  groupID: 'group1',
  name: 'new name', // Modify the group name
  introduction: 'this is introduction.', // Modify the group introduction
  // Starting from v2.6.0, group members can receive group messages about group custom field modifications and obtain related content. For more information, see Message.payload.newGroupProfile.groupCustomField.
  groupCustomField: [{ key: 'group_level', value: 'high'}] // Modify the group custom field
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // Detailed group profile after modification
}).catch(function(imError){
  console.warn('updateGroupProfile error:', imError); // Failed to modify the group profile
});

:::
</dx-codeblock>

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
