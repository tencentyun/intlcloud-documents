## Feature Description
A community group is a large group of people brought together by common topics, and multiple topics can be created under the same community group based on different interests.
A community is used to manage members. All its topics are shared among members, who can send and receive messages independently.
[**Community mode**](https://cloud.tencent.com/document/product/269/75979).

- The community and topic management APIs are in the `TencentImSDKPlugin.v2TIMManager.getGroupManager()` core class.
- The topic message APIs are in the `TencentImSDKPlugin.v2TIMManager.getMessageManager()` core class.

>? This feature is supported by the SDK for Flutter on v4.0.0 or later. To use it, you need to [purchase the Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577#.E5.8D.87.E7.BA.A7.E5.BA.94.E7.94.A8), go to the [**console**](https://console.cloud.tencent.com/im/qun-setting), select **Group feature configuration**, and enable the **Community** feature.

## Community Management
### Creating a community

You need to perform two steps to create a community group that supports topics:

1. Create the `V2TIMGroupInfo` object ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Group/V2TimGroupInfo.html)) and set `groupType` to `Community` and `isSupportTopic` to `true`/`YES`.
2. Call the `createGroup` API ([dart](https://comm.qq.c om/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/createGroup.html)) to create a community.

Sample code:

```dart
// Create a topic-enabled community
groupManager.createGroup(groupType: "Community", groupName: "Community",isSupportTopic: true);
```


### Getting the list of joined communities
Call `getJoinedCommunityList` ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getJoinedCommunityList.html)) to get the list of joined topic-enabled communities.

Sample code:

```dart
// Get the list of joined communities
V2TimValueCallback<List<V2TimGroupInfo>> groupList = await groupManager.getJoinedCommunityList();
```

### Other management APIs
Other features can be used in the same way as an ordinary group feature and involve the following APIs:

<table>
<tr>
<th width="15%">Category</th>
<th width="25%">Feature</th>
<th width="60%">API</th>
</tr>
<tr>
<td rowspan="5">Community management</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48464#joinGroup">Joins a community</a></td>
<td>joinGroup (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/joinGroup.html">dart</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48464#quitGroup">Leaves a community</a></td>
<td>quitGroup (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/quitGroup.html">dart</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48464#dismissGroup">Disbands a community</a></td>
<td>dismissGroup (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/dismissGroup.html">dart</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48183#getGroupsInfo">Gets the community profile</a></td>
<td>getGroupsInfo (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getGroupsInfo.html">dart</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48183#setGroupInfo">Modifies the community profile</a></td>
<td>setGroupInfo (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/setGroupInfo.html">dart</a>)</td>
</tr>
<tr>
<td rowspan="4">Community group member management</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48179#getGroupMemberList">Gets the list of community members</a></td>
<td>getGroupMemberList (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getGroupMemberList.html">dart</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48176#getGroupMembersInfo">Gets the profiles of the community members</a></td>
<td>getGroupMembersInfo (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getGroupMembersInfo.html">dart</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48176#setGroupMemberInfo">Modifies the profile of a community member</a></td>
<td>setGroupMemberInfo (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/setGroupMemberInfo.html">dart</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48179#kickGroupMember">Removes a member from the community</a></td>
<td>kickGroupMember (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/kickGroupMember.html">dart</a>)</td>
</tr>
</table>


## Topic Management

### Creating a topic

You need to perform two steps to create a topic:
1. Create the `V2TIMTopicInfo` object ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Topic/V2TimTopicInfo.html)).
2. Call the `createTopicInCommunity` API ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/createTopicInCommunity.html)) to create a topic.

Sample code:


```java
// Create a topic
groupManager.createTopicInCommunity(groupID: "groupID", topicInfo: V2TimTopicInfo.fromJson({
    "topicName":"topic"
}));
```


### Deleting a topic
Call the `deleteTopicFromCommunity` API ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/deleteTopicFromCommunity.html)) to delete a topic.

Sample code:


```dart
// Delete a topic
groupManager.deleteTopicFromCommunity(groupID: "",topicIDList:["topicID"]);
```


### Modifying the information of a topic
You need to perform two steps to modify the information of a topic:

1. Create the `V2TIMTopicInfo` object ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Topic/V2TimTopicInfo.html)) and set the fields to be modified.
2. Call the `setTopicInfo` API ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/setTopicInfo.html)) to modify the information of a topic.

Sample code:


```dart
// Modify the information of a topic
groupManager.setTopicInfo(topicInfo:V2TimTopicInfo.fromJson({
    "topicName":"topicName"
}));
```


### Getting the topic list[](id:getTopicList)
Call the `getTopicInfoList` API ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getTopicInfoList.html)) to get the topic list.
- If `topicIDList` is an empty array, the list of all topics in the community will be obtained.
- If `topicIDList` contains the IDs of specified topics, the list of the specified topics will be obtained.

Sample code:


```dart
// Get the topic list
groupManager.getTopicInfoList(groupID: "",topicIDList: ['topicID']);
```


### Topic group
The community mode (a new powerful tool for entertainment collaboration) supports the community-**group**-topic hierarchy to isolate messages.



The [`customInfo`](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Group/V2TimGroupInfo.html#custominfo) of a community saves the topic group list of the community, while the [`customString`](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Topic/V2TimTopicInfo.html#customstring) field of each topic stores the topic group.

- When a community is loaded, the [`customInfo`](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Group/V2TimGroupInfo.html#custominfo) field for the topic group list of the community (group) is used to display the group list. We recommend you store the field in the `List<String>` format.
- To get the topics in each group, traverse the topic list and get the group of each topic through the [`customString`](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Topic/V2TimTopicInfo.html#customstring) of [`V2TimTopicInfo`](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Topic/V2TimTopicInfo.html#customstring).

>? 
>
> You can customize the `key` value of the [`customInfo`](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Group/V2TimGroupInfo.html#custominfo) field for the topic group list of the community (group).
> The following sample code names it `categoryList`.

#### Getting the list of groups in the community

Call the `getCommunityCategoryList(String groupID)` method. Sample code:

```dart
getCommunityCategoryList(String groupID) async {
    final Map<String, String>? customInfo = await getCommunityCustomInfo(groupID);
    if(customInfo != null){
      final String? categoryListString = customInfo["categoryList"];
      if(categoryListString != null && categoryListString.isNotEmpty){
        return jsonDecode(categoryListString);
      }
    }
  }

 Future<Map<String, String>?> getCommunityCustomInfo(String groupID) async {
    V2TimValueCallback<List<V2TimGroupInfoResult>> res =
        await TencentImSDKPlugin.v2TIMManager
            .getGroupManager().getGroupsInfo(groupIDList: [groupID]);
    if(res.code != 0){
      final V2TimGroupInfoResult? groupInfo = res.data?[0];
      if(groupInfo != null){
        Map<String, String>? customInfo = groupInfo.groupInfo?.customInfo;
        return customInfo;
      }
    }
    return null;
  }
```

#### Configuring the group list for the community

You just need to modify the `customInfo` in `groupInfo`. Here is a `Map`, and the `key` value is the name of the field for the topic group list you defined.

The `getCommunityCustomInfo` method is implemented in the above section. Sample code:

```dart
setCommunityCategoryList(String groupID, String groupType, List<String> newCategoryList) async {
    final Map<String, String>? customInfo = await getCommunityCustomInfo(groupID);
    customInfo?["categoryList"] = jsonEncode(newCategoryList);
    TencentImSDKPlugin.v2TIMManager
        .getGroupManager()
        .setGroupInfo(info: V2TimGroupInfo(
      customInfo: customInfo,
      groupID: groupID,
      groupType: groupType,
      // ...Other profiles
    ));
  }
```

#### Adding a topic to a group

Sample code:

```dart
addCategoryForTopic(String groupID, String categoryName) {
    TencentImSDKPlugin.v2TIMManager.getGroupManager().setTopicInfo(
      topicInfo: V2TimTopicInfo(
        customString: categoryName
      ),
      groupID: groupID, // Group ID of the topic
    );
  }
```

#### Getting the topic group

Use the `customString` after [getting the topic list](#getTopicList).

### Listening for a topic callback
In `V2TIMGroupListener` ([dart](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Listener/V2TimGroupListener.html)), topic callback methods such as `onTopicCreated`, `onTopicDeleted`, and `onTopicInfoChanged` are added to listen for topic events. 

Sample code:


```dart
V2TIMGroupListener v2TIMGroupListener = new V2TIMGroupListener() {
 onTopicCreated(String groupID, String topicID) {
  	// Listen for the topic creation notification
  }

  onTopicDeleted(String groupID, List<String> topicIDList) {
  	// Listen for the topic deletion notification
  }
	onTopicInfoChanged(String groupID, V2TIMTopicInfo topicInfo) {
  	// Listen for the topic information update notification
  }
};
V2TIMManager.getInstance().addGroupListener(v2TIMGroupListener);
```



## Topic Message
Topic messages can be used in the same way as ordinary messages and involve the following APIs:

<table>
<tr>
<th width="15%">Feature</th>
<th width="40%">API</th>
<th width="30%">Description</th>
</tr>
<tr>
<td>Sends a message</td>
<td>sendMessage (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessage.html">dart</a>)</td>
<td>Set `groupID` to the topic ID.</td>
</tr>
<tr>
<td>Receives a message</td>
<td>The `onRecvNewMessage` method in `V2TIMAdvancedMsgListener` (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Listener/V2TimAdvancedMsgListener.html">dart</a>)</td>
<td>Set `groupID` in the message to the topic ID.</td>
</tr>
<tr>
<td>Marks a message as read</td>
<td>markGroupMessageAsRead (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/markGroupMessageAsRead.html">dart</a></td>
<td>Set `groupID` to the topic ID.</td>
</tr>
<tr>
<td>Gets historical messages</td>
<td>getGroupHistoryMessageList (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/getGroupHistoryMessageList.html">dart</a></td>
<td>Set `groupID` to the topic ID.</td>
</tr>
<tr>
<td>Recalls a message</td>
<td>revokeMessage (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/revokeMessage.html">dart</a>)</td>
<td>Set `groupID` to the topic ID.</td>
</tr>
</table>


