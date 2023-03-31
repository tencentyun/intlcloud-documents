## Feature Description

The methods to manipulate the group member profile are in the `TencentImSDKPlugin.v2TIMManager.getGroupManager()` core class.

[](id:getGroupMembersInfo)

## Getting the Profile of a Group Member

You can call `getGroupMembersInfo` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMGroupManager/getGroupMembersInfo.html)) to get the group member profile. This API supports passing in multiple `userID` values at a time to batch get group member profiles and therefore improve the network transfer efficiency.

Below is the sample code:

```javascript
// Get the group member profile
const memberInfos = await groupManager.getGroupMembersInfo("groupID", ["id1"]);
```

[](id:setGroupMemberInfo)

## Modifying the Profile of a Group Member

The group owner or admin can call the `setGroupMemberInfo` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMGroupManager/setGroupMemberInfo.html)) to modify the group name card (`nameCard`), custom field (`customInfo`), and other information of a group member.

Below is the sample code:

```javascript
// Set the group member profile
groupManager.setGroupMemberInfo("groupID", "userID", "nameCard");
```
