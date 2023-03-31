## Feature Description
A community is a large group of people brought together by common topics, and multiple topics can be created under the same community based on different interests.
Community groups are used to manage group members. All topics under the same community group are shared among members, who can send and receive messages within each topic independently.
[**See use cases of community groups here.**](https://intl.cloud.tencent.com/document/product/1047/49713)

- Community and topic management APIs are in the `TencentImSDKPlugin.v2TIMManager.getGroupManager()` core class.
- Topic message APIs are in the `TencentImSDKPlugin.v2TIMManager.getMessageManager()` core class.

>? This feature is supported by Flutter SDK v4.0.0 or later. To use it, you need to [purchase the Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577), go to the [**console**](https://console.cloud.tencent.com/im/qun-setting), choose **Feature Configuration** > **Group configuration** > **Group feature configuration** > **Community**, and enable the community feature.

## Community Group Management
### Creating a community group

You need to perform two steps to create a community group that supports topics:

1. Create the `V2TIMGroupInfo` object ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Group/V2TimGroupInfo.html?h=V2TIMGroupInfo)) and set `groupType` to `Community` and `isSupportTopic` to `true`/`YES`.
2. Call the `createGroup` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/createGroup.html?h=createGroup)) API to create the community group.

Sample code:

```dart
// Create a topic-enabled community
groupManager.createGroup(groupType: "Community", groupName: "Community",isSupportTopic: true);
```


### Getting the list of community groups joined
You can call `getJoinedCommunityList`([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getJoinedCommunityList.html?h=getJoinedCommunityList)) to get the list of community groups joined.

Sample code:

```dart
// Getting the list of community groups joined
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
<td rowspan="5">Community group management</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48464">Joining a group</a></td>
<td>joinGroup (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/joinGroup.html">dart</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48464">Leaving a group</a></td>
<td>quitGroup (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/quitGroup.html">dart</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48464">Disbanding a group</a></td>
<td>dismissGroup (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMManager/dismissGroup.html">dart</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48183">Getting the group profile</a></td>
<td>getGroupsInfo (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getGroupsInfo.html">dart</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48183">Modifying the group profile</a></td>
<td>setGroupInfo (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/setGroupInfo.html">dart</a>)</td>
</tr>
<tr>
<td rowspan="4">Community group member management</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48179">Getting the group member list</a></td>
<td>getGroupMemberList (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getGroupMemberList.html">dart</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48176">Getting the profile of a group member</a></td>
<td>getGroupMembersInfo (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getGroupMembersInfo.html">dart</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48176">Modifying the profile of a group member</a></td>
<td>setGroupMemberInfo (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/setGroupMemberInfo.html">dart</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48179">Removing a group member</a></td>
<td>kickGroupMember (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/kickGroupMember.html">dart</a>)</td>
</tr>
</table>


## Topic Management
Multiple topics can be created under the same community group. All the topics are shared among group members, who can send and receive messages within each topic independently.
>?To use the feature, you need to go to the [**console**](https://console.cloud.tencent.com/im/qun-setting), choose **Feature Configuration** > **Group configuration** > **Group feature configuration** > **Community**, enable the community feature and then enable the topic feature.


### Creating a topic

You need to perform two steps to create a topic:
1. Create a `V2TIMTopicInfo` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Topic/V2TimTopicInfo.html)) object.
2. Call the `createTopicInCommunity` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/createTopicInCommunity.html)) API to create a topic.

Sample code:


```java
// Create a topic
groupManager.createTopicInCommunity(groupID: "groupID", topicInfo: V2TimTopicInfo.fromJson({
    "topicName":"topic"
}));
```


### Deleting a topic
You can call the `deleteTopicFromCommunity`([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/deleteTopicFromCommunity.html)) API to delete a topic.

Sample code:


```dart
// Delete a topic
groupManager.deleteTopicFromCommunity(groupID: "",topicIDList:["topicID"]);
```


### Modifying topic information
You need to perform two steps to modify the information of a topic:

1. Create a `V2TIMTopicInfo` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Topic/V2TimTopicInfo.html)) object and modify fields as needed.
2. Call the `setTopicInfo` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/setTopicInfo.html)) API to modify topic information.

Sample code:


```dart
// Modify topic information
groupManager.setTopicInfo(topicInfo:V2TimTopicInfo.fromJson({
    "topicName":"topicName"
}));
```


### Getting the topic list[](id:getTopicList)
You can call the `getTopicInfoList` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMGroupManager/getTopicInfoList.html)) API to get the topic list.
- If `topicIDList` is an empty array, the list of all topics of the community group will be got.
- If `topicIDList` is the ID of specified topics, the list of the specified topics will be got.

Sample code:


```dart
// Get the topic list
groupManager.getTopicInfoList(groupID: "",topicIDList: ['topicID']);
```


### Topic groups
The community is a new powerful tool for entertainment collaboration and supports the community-**group**-topic hierarchy to isolate messages.

<img style="width:50%;" src="https://qcloudimg.tencent-cloud.cn/raw/728b38c71f25a70bcb717c3fefe29aac.png" />

The [`customInfo`](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Group/V2TimGroupInfo.html#custominfo) of a community saves the topic group list of the community, while the [`customString`](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Topic/V2TimTopicInfo.html#customstring) field of each topic stores the topic group.

- When a community is loaded, the [`customInfo`](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Topic/V2TimTopicInfo.html#customstring) field for the topic group list of the community (group) is used to display the group list. We recommend you store the field in the `List<String>` format.
- To get the topics in each group, traverse the topic list and get the group of each topic through the [`customString`](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Topic/V2TimTopicInfo.html#customstring) of [`V2TimTopicInfo`](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Topic/V2TimTopicInfo.html).

>? 
>
>You can customize the `key` value of the [`customInfo`](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Group/V2TimGroupInfo.html#custominfo) field for the topic group list of the community (group).
>The following sample code names it `topic_category`.

#### Getting the list of groups in the community

Call the `getCommunityCategoryList(String groupID)` method. Sample code:

```dart
getCommunityCategoryList(String groupID) async {
    final Map<String, String>? customInfo = await getCommunityCustomInfo(groupID);
    if(customInfo != null){
      final String? categoryListString = customInfo["topic_category"];
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
    customInfo?["topic_category"] = jsonEncode(newCategoryList);
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

It is recommended that you pass in JSON strings into `V2TimTopicInfo customString`.
For example, the recommended format for `categoryName` in the code below is `{"category":"Group 1"}`.

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

### Listening for topic callbacks
In `V2TIMGroupListener` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Listener/V2TimGroupListener.html)), topic related callback methods `onTopicCreated`, `onTopicDeleted`, and `onTopicInfoChanged` are added for topic event listening. 

Sample code:


```dart
V2TIMGroupListener v2TIMGroupListener = new V2TIMGroupListener() {
 onTopicCreated(String groupID, String topicID) {
  	// Listen for topic creation notifications
  }

  onTopicDeleted(String groupID, List<String> topicIDList) {
  	// Listen for topic deletion notifications
  }
	onTopicInfoChanged(String groupID, V2TIMTopicInfo topicInfo) {
  	// Listen for topic information update notifications
  }
};
V2TIMManager.getInstance().addGroupListener(v2TIMGroupListener);
```



## Topic Messages
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
<td>`onRecvNewMessage` method in `V2TIMAdvancedMsgListener` (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Class/Listener/V2TimAdvancedMsgListener.html">dart</a>)</td>
<td>Set `groupID` in the message to the topic ID.</td>
</tr>
<tr>
<td>Marks a message as read</td>
<td>markGroupMessageAsRead (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/markGroupMessageAsRead.html">dart</a>)</td>
<td>Set `groupID` to the topic ID.</td>
</tr>
<tr>
<td>Gets historical messages</td>
<td>getGroupHistoryMessageList (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/getGroupHistoryMessageList.html">dart</a>)</td>
<td>Set `groupID` to the topic ID.</td>
</tr>
<tr>
<td>Recalls a message</td>
<td>revokeMessage (<a href="https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/revokeMessage.html">dart</a>)</td>
<td>Set `groupID` to the topic ID.</td>
</tr>
</table>
