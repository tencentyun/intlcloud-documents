## Feature Description
The methods to manipulate the group member profile are in the `TencentImSDKPlugin.v2TIMManager.getGroupManager()` core class.

[](id:getGroupMembersInfo)

## Getting the Profile of a Group Member

Call `getGroupMembersInfo` ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/getGroupMembersInfo.html)) to get the group member profile. This API supports passing in multiple `userID` values at a time to batch get group member profiles and therefore improve the network transfer efficiency.

Sample code:



```dart
// Get the group member profile
V2TimValueCallback<List<V2TimGroupMemberFullInfo>> memberInfos = await groupManager.getGroupMembersInfo(groupID: "groupID", memberList: ["id1"]);
```

[](id:setGroupMemberInfo)

## Modifying the Profile of a Group Member

The group owner or admin can call the `setGroupMemberInfo` API ([dart](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/setGroupMemberInfo.html)) to modify the group name card (`nameCard`), custom field (`customInfo`), and other information of a group member.

Sample code:



```java
// Set the group member profile
groupManager.setGroupMemberInfo(groupID: "",userID: "",nameCard: "",customInfo: {});
```



