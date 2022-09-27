## Feature Description

A community is a large group of people brought together by common topics, and multiple topics can be created under the same community based on different interests.
A community is used to manage members. All its topics are shared among members, who can send and receive messages independently.

- The community and topic management APIs are in the `TencentImSDKPlugin.v2TIMManager.getGroupManager()` core class.
- The topic message APIs are in the `TencentImSDKPlugin.v2TIMManager.getMessageManager()` core class.

> ? To use the community feature, you need to [purchase the Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577#.E5.8D.87.E7.BA.A7.E5.BA.94.E7.94.A8), go to the [**console**](https://console.cloud.tencent.com/im/qun-setting), select **Group feature configuration**, and enable the **Community** feature.

## Community Management

### Creating a community

You need to perform two steps to create a topic-enabled community:

1. Create the `V2TIMGroupInfo` object ([TS](https://comm.qq.com/im-react-native-doc/interfaces/interface.V2TimGroupInfo-1.html)) and set `groupType` to `Community` and `isSupportTopic` to `true`/`YES`.
2. Call the `createGroup` API ([TS](https://comm.qq.com/im-react-native-doc/classes/GroupManager________.V2TimGroupManager.html#createGroup)) to create a community.

Below is the sample code:

```javascript
// Create a topic-enabled community
groupManager.createGroup(groupType: "Community", groupName: "Community",isSupportTopic: true);
```

### Getting the list of joined communities

Call `getJoinedCommunityList` ([TS](https://comm.qq.com/im-react-native-doc/classes/GroupManager________.V2TimGroupManager.html#getJoinedCommunityList)) to get the list of joined topic-enabled communities.

Below is the sample code:

```javascript
// Get the list of joined communities
const groupList = await groupManager.getJoinedCommunityList();
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
<td>joinGroup (<a href="https://comm.qq.com/im-react-native-doc/classes/BaseManager______.V2TIMManager.html#joinGroup">TS</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48464#quitGroup">Leaves a community</a></td>
<td>quitGroup (<a href="https://comm.qq.com/im-react-native-doc/classes/BaseManager______.V2TIMManager.html#quitGroup">TS</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48464#dismissGroup">Disbands a community</a></td>
<td>dismissGroup (<a href="https://comm.qq.com/im-react-native-doc/classes/BaseManager______.V2TIMManager.html#dismissGroup">TS</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48183#getGroupsInfo">Gets the community profile</a></td>
<td>getGroupsInfo (<a href="https://comm.qq.com/im-react-native-doc/classes/GroupManager________.V2TimGroupManager.html#getGroupsInfo">TS</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48183#setGroupInfo">Modifies the community profile</a></td>
<td>setGroupInfo (<a href="https://comm.qq.com/im-react-native-doc/classes/GroupManager________.V2TimGroupManager.html#setGroupInfo">TS</a>)</td>
</tr>
<tr>
<td rowspan="4">Community member management</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48179#getGroupMemberList">Gets the list of community members</a></td>
<td>getGroupMemberList (<a href="https://comm.qq.com/im-react-native-doc/classes/GroupManager________.V2TimGroupManager.html#getGroupMemberList">TS</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48176#getGroupMembersInfo">Gets the profiles of the community members</a></td>
<td>getGroupMembersInfo (<a href="https://comm.qq.com/im-react-native-doc/classes/GroupManager________.V2TimGroupManager.html#getGroupMembersInfo">TS</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48176#setGroupMemberInfo">Modifies the profile of a community member</a></td>
<td>setGroupMemberInfo (<a href="https://comm.qq.com/im-react-native-doc/classes/GroupManager________.V2TimGroupManager.html#setGroupMemberInfo">TS</a>)</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/48179#kickGroupMember">Removes a member from the community</a></td>
<td>kickGroupMember (<a href="https://comm.qq.com/im-react-native-doc/classes/GroupManager________.V2TimGroupManager.html#kickGroupMember">TS</a>)</td>
</tr>
</table>

## Topic Management

### Creating a topic

You need to perform two steps to create a topic:

1. Create the `V2TIMTopicInfo` object ([TS](https://comm.qq.com/im-react-native-doc/interfaces/interface.V2TimTopicInfo-1.html)).
2. Call the `createTopicInCommunity` API ([TS](https://comm.qq.com/im-react-native-doc/classes/GroupManager________.V2TimGroupManager.html#createTopicInCommunity)) to create a topic.

Below is the sample code:

```javascript
// Create a topic
groupManager.createTopicInCommunity("groupID", {
  topicName: "topic",
});
```

### Deleting a topic

Call the `deleteTopicFromCommunity` API ([TS](https://comm.qq.com/im-react-native-doc/classes/GroupManager________.V2TimGroupManager.html#deleteTopicFromCommunity)) to delete a topic.

Below is the sample code:

```javascript
// Delete a topic
groupManager.deleteTopicFromCommunity("groupID", ["topicID"]);
```

### Modifying the information of a topic

You need to perform two steps to modify the information of a topic:

1. Create the `V2TIMTopicInfo` object ([TS](https://comm.qq.com/im-react-native-doc/interfaces/interface.V2TimTopicInfo-1.html)) and set the fields to be modified.
2. Call the `setTopicInfo` API ([TS](https://comm.qq.com/im-react-native-doc/classes/GroupManager________.V2TimGroupManager.html#setTopicInfo)) to modify the information of a topic.

Below is the sample code:

```javascript
// Modify the information of a topic
groupManager.setTopicInfo({
  topicName: "topicName",
});
```

### Getting the topic list

Call the `getTopicInfoList` API ([TS](https://comm.qq.com/im-react-native-doc/classes/GroupManager________.V2TimGroupManager.html#getTopicInfoList)) to get the topic list.

- If `topicIDList` is empty, the list of all topics of the community will be obtained.
- If `topicIDList` is the ID of specified topics, the list of the specified topics will be got.

Below is the sample code:

```javascript
// Get the topic list
groupManager.getTopicInfoList("groupID", ["topicID"]);
```

### Listening for a topic callback

In `V2TIMGroupListener` ([TS](https://comm.qq.com/im-react-native-doc/interfaces/interface.V2TimGroupListener-1.html)), topic callback methods such as `onTopicCreated`, `onTopicDeleted`, and `onTopicInfoChanged` are added to listen for topic events.

Below is the sample code:

```javascript
const v2TIMGroupListener = {
  onTopicCreated: (groupID, topicID) => {
    // Listening for topic creation notifications
  },
  onTopicDeleted: (groupID, topicIDList) => {
    // Listening for topic deletion notifications
  },
  onTopicInfoChanged: (groupID, topicInfo) => {
    // Listening for topic information update notifications
  },
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
<td>sendMessage (<a href="https://comm.qq.com/im-react-native-doc/classes/MessageManager__________.V2TIMMessageManager.html#sendMessage">TS</a>)</td>
<td>Set `groupID` to the topic ID.</td>
</tr>
<tr>
<td>Receives a message</td>
<td>The `onRecvNewMessage` method in `V2TIMAdvancedMsgListener` (<a href="https://comm.qq.com/im-react-native-doc/interfaces/interface.V2TimAdvancedMsgListener-1.html">TS</a>)</td>
<td>Set `groupID` in the message to the topic ID.</td>
</tr>
<tr>
<td>Marks a message as read</td>
<td>markGroupMessageAsRead (<a href="https://comm.qq.com/im-react-native-doc/classes/MessageManager__________.V2TIMMessageManager.html#markGroupMessageAsRead">TS</a></td>
<td>Set `groupID` to the topic ID.</td>
</tr>
<tr>
<td>Gets historical messages</td>
<td>getGroupHistoryMessageList (<a href="https://comm.qq.com/im-react-native-doc/classes/MessageManager__________.V2TIMMessageManager.html#getGroupHistoryMessageList">TS</a></td>
<td>Set `groupID` to the topic ID.</td>
</tr>
<tr>
<td>Recalls a message</td>
<td>revokeMessage (<a href="https://comm.qq.com/im-react-native-doc/classes/MessageManager__________.V2TIMMessageManager.html#revokeMessage">TS</a>)</td>
<td>Set `groupID` to the topic ID.</td>
</tr>
</table>


