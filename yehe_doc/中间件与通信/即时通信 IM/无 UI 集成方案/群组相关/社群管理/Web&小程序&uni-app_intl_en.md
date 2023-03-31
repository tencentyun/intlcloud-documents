## Feature Description

A community is a large group of people brought together by common topics, and multiple topics can be created under the same community based on different interests. A community is used to manage members. All its topics are shared among members, who can send and receive messages independently.

## Community Group Management

### Creating a community group

**Sample**

<dx-codeblock>
:::  js

// Create a topic-enabled community
let promise = tim.createGroup({
  type: TIM.TYPES.GRP_COMMUNITY,
  name: 'WebSDK',
  isSupportTopic: true,
});
promise.then(function(imResponse) { // Created successfully
  console.log(imResponse.data.group); // Profile of the created group
}).catch(function(imError){
  console.warn('createGroup error:', imError); // Error information
});

:::
</dx-codeblock>


### Getting the list of topic-enabled communities

>! This API is supported only by v2.19.1 or later and applies only to topic-enabled communities. To use the feature, you need to [purchase the Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577), go to the [**console**](https://console.cloud.tencent.com/im/qun-setting), select **Feature Configuration** > **Group configuration** > **Group feature configuration** > **Community**, and enable the community feature.

**API**

<dx-codeblock>
:::  js

tim.getJoinedCommunityList();

:::
</dx-codeblock>

**Parameters**

Unlimited

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

// Get the list of topic-enabled communities
let promise = tim.getJoinedCommunityList();
promise.then(function(imResponse) { // Got successfully
  console.log(imResponse.data.groupList); // List of topic-enabled communities
}).catch(function(imError) { // Getting failed
  console.warn('getJoinedCommunityList error:', imError); // Failure message
});

:::
</dx-codeblock>

### Creating a topic

>!
>- This API is supported only by v2.19.1 or later and applies only to topic-enabled communities. To use the feature, you need to [purchase the Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577), go to the [**console**](https://console.cloud.tencent.com/im/qun-setting), select **Feature Configuration** > **Group configuration** > **Group feature configuration** > **Community**, enable the community feature, and enable the topic feature.
>- Before using this API, you must call [createGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createGroup) to create a topic-enabled community.

**API**

<dx-codeblock>
:::  js

tim.createTopicInCommunity(options);

:::
</dx-codeblock>

**Parameters**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name         | Type   | Description                                                  |
| ------------ | ------ | ------------------------------------------------------------ |
| groupID      | String | Community ID of the topic                                    |
| topicName    | String | Topic name                                                   |
| topicID      | String | A custom topic ID must be in the format of "community ID + custom topic ID", such as "@TGS#_xxx@TOPIC#_xxx". |
| avatar       | String | Topic profile photo                                          |
| notification | String | Topic notice                                                 |
| introduction | String | Topic introduction                                           |
| customData   | String | Custom topic information                                     |

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

// Create a topic
let promise = tim.createTopicInCommunity({
  groupID: 'group1',
  topicName: 'test',
  avatar: 'xxx'
  notification: 'xxx',
  introduction: 'xxx',
  customData: 'xxxx',
});
promise.then(function(imResponse) { // Created successfully
  console.log(imResponse.data.topicID); // Topic ID
}).catch(function(imError) { // Creation failed
  console.warn('createTopicInCommunity error:', imError); // Failed to create the topic
});

:::
</dx-codeblock>

### Deleting a topic

>! This API is supported only by v2.19.1 or later and applies only to topic-enabled communities. To use the feature, you need to [purchase the Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577) and [apply for enablement](https://intl.cloud.tencent.com/document/product/1047/44322).

**API**

<dx-codeblock>
:::  js

tim.deleteTopicFromCommunity(options);

:::
</dx-codeblock>

**Parameters**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name        | Type               | Description                                                  |
| ----------- | ------------------ | ------------------------------------------------------------ |
| groupID     | String             | Community ID of the topic                                    |
| topicIDList | Array \| undefined | List of topic IDs. If it is not passed in, all the topics are deleted. |

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

// Delete a specified topic under a community
let promise = tim.deleteTopicFromCommunity({
  groupID: 'group1',
  topicIDList: ['topicID'],
});
promise.then(function(imResponse) { // Deleted successfully
  const { successTopicList, failureTopicList } = imResponse.data;
  // List of topics deleted successfully
  successTopicList.forEach((item) => {
     const { topicID } = item;
  });
  // List of topics failed to be deleted
  failureTopicList.forEach((item) => {
     const { topicID, code, message } = item;
  })
}).catch(function(imError) { // Deletion failed
  console.warn('deleteTopicFromCommunity error:', imError); // Failed to delete the topic
});

:::
</dx-codeblock>


<dx-codeblock>
:::  js

// Delete all the topics under a community
let promise = tim.deleteTopicFromCommunity({
  groupID: 'group1',
});
promise.then(function(imResponse) { // Deleted successfully
  const { successTopicList, failureTopicList } = imResponse.data;
  // List of topics deleted successfully
  successTopicList.forEach((item) => {
     const { topicID } = item;
  });
  // List of topics failed to be deleted
  failureTopicList.forEach((item) => {
     const { topicID, code, message } = item;
  })
}).catch(function(imError) { // Deletion failed
  console.warn('deleteTopicFromCommunity error:', imError); // Failed to delete the topic
});

:::
</dx-codeblock>

### Modifying the topic profile

>! This API is supported only by v2.19.1 or later and applies only to topic-enabled communities. To use the feature, you need to [purchase the Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577) and [apply for enablement](https://intl.cloud.tencent.com/document/product/1047/44322).

**API**

<dx-codeblock>
:::  js

tim.updateTopicProfile(options);

:::
</dx-codeblock>

**Parameters**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name           | Type                 | Description                                                  |
| -------------- | -------------------- | ------------------------------------------------------------ |
| groupID        | String               | Community ID of the topic                                    |
| topicID        | String               | Topic ID, which is required                                  |
| topicName      | String \| undefined  | Topic name                                                   |
| avatar         | String \| undefined  | Topic profile photo                                          |
| notification   | String \| undefined  | Topic notice                                                 |
| introduction   | String \| undefined  | Topic introduction                                           |
| customData     | String \| undefined  | Custom topic information                                     |
| muteAllMembers | Boolean \| undefined | Muting all. Valid values: `true`: mute all; `false`: unmute all. |

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

// Update the topic profile
let promise = tim.updateTopicProfile({
  groupID: 'group1',
  topicID: 'topic1',
  topicName: 'test',
  avatar: 'xxx'
  notification: 'xxx',
  introduction: 'xxx',
  customData: 'xxxx',
  muteAllMembers: true
});
promise.then(function(imResponse) { // Topic profile set successfully
  console.log(imResponse.data.topic); // Modified topic profile
}).catch(function(imError) { // Failed to set the topic profile
  console.warn('updateTopicProfile error:', imError); // Information on the failure in setting the topic profile
});

:::
</dx-codeblock>

[](id:getTopicList)
### Getting the topic list

>! This API is supported only by v2.19.1 or later and applies only to topic-enabled communities. To use the feature, you need to [purchase the Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577) and [apply for enablement](https://intl.cloud.tencent.com/document/product/1047/44322).

**API**

<dx-codeblock>
:::  js

tim.getTopicList(options);

:::
</dx-codeblock>

**Parameters**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name        | Type               | Description                                                  |
| ----------- | ------------------ | ------------------------------------------------------------ |
| groupID     | String             | Community ID of the topic                                    |
| topicIDList | Array \| undefined | List of topic IDs. If it is not passed in, all the topics are obtained. |

**Return values**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

// Get a specified topic
let promise = tim.getTopicList({
  groupID: 'group1',
  topicIDList: ['topicID'],
});
promise.then(function(imResponse) { // Got successfully
  const { successTopicList, failureTopicList } = imResponse.data;
  // List of topics got successfully
  successTopicList.forEach((item) => {
     const { topicID } = item;
  });
  // List of topics failed to be got
  failureTopicList.forEach((item) => {
     const { topicID, code, message } = item;
  })
}).catch(function(imError) { // Getting failed
  console.warn('getTopicList error:', imError); // Information on the failure in getting the topic list
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Get all the topics
let promise = tim.getTopicList({
  groupID: 'group1',
});
promise.then(function(imResponse) { // Got successfully
  const { successTopicList, failureTopicList } = imResponse.data;
  // List of topics got successfully
  successTopicList.forEach((item) => {
     const { topicID } = item;
  });
  // List of topics failed to be got
  failureTopicList.forEach((item) => {
     const { topicID, code, message } = item;
  })
}).catch(function(imError) { // Getting failed
  console.warn('getTopicList error:', imError); // Information on the failure in getting the topic list
});

:::
</dx-codeblock>

### Topic group


The community-**group**-topic hierarchy is implemented as follows:
The [groupCustomField](https://web.sdk.qcloud.com/im/doc/en/Group.html) field in the community profile defines a field to store the topic group list of the community. The customData field in the topic profile stores the group to which each topic belongs.

- When a community is loaded, the `groupCustomField` field for the topic group list in the community (group) profile is used to display the group list.
- When the topic list of a community is loaded, the `customData` field in the topic profile is used to get the group name for assignment.

>? 
>
>You can customize the `key` value of the `groupCustomField` field for the topic group list of the community (group).
>The following sample code names it `topic_category`.

#### Configuring the group list for the community
You only need to modify the `groupCustomField` field in the group profile. The `key` value is the name of the field for the topic group list you defined.
Sample code:
<dx-codeblock>
:::  js
// Topic group list
const categoryList = ['Group 1', 'Group 2'];
// Update the topic group list of the community
let promise = tim.updateGroupProfile({
  groupID: 'group1',
  // You need to configure the custom group field `topic_category` in the console first.
  groupCustomField: [{ key: 'topic_category', value: JSON.stringify(categoryList) }]
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // Detailed group profile after modification
}).catch(function(imError){
  console.warn('updateGroupProfile error:', imError); // Error information
});
:::
</dx-codeblock>

#### Getting the list of groups in the community

Sample code:
<dx-codeblock>
:::  js
let promise = tim.getGroupProfile({ groupID: 'group1', groupCustomFieldFilter: ['topic_category'] });
promise.then(function(imResponse) {
  console.log(imResponse.data.group);
  const categoryList = []; // Topic group list
  const { groupCustomField } = imResponse.data.group;
  groupCustomField.forEach((item) => {
    if (item.key === 'topic_category') {
      // Parse the group list
      categoryList = JSON.parse(item.value);
    }
  });
}).catch(function(imError){
  console.warn('getGroupProfile error:', imError); // Error information
});
:::
</dx-codeblock>

#### Adding a topic to a group

You can save the topic group with the `customData` field of the topic.
Sample code:
<dx-codeblock>
:::  js
// Define a group for the topic
const customData = { category: 'Group 1' };
// Update the topic group
let promise = tim.updateTopicProfile({
  groupID: 'group1', // Community ID
  topicID: 'topic1', // Topic ID
  customData: JSON.stringify(customData),
});
promise.then(function(imResponse) { // Topic group updated successfully
  console.log(imResponse.data.topic); // Modified topic profile
}).catch(function(imError) { // Failed to update the topic group
  console.warn('updateTopicProfile error:', imError); // Information on the failure in updating the topic group
});
:::
</dx-codeblock>

#### Getting the topic group

Use the `customData` to parse the JSON content after [getting the topic list](#getTopicList).

### Listening for topic callbacks

<dx-codeblock>
:::  js

let onTopicCreated = function(event) {
   const groupID = event.data.groupID // ID of the community to which the topic belongs
   const topicID = event.data.topicID // Topic ID
   console.log(event.data);
};
tim.on(TIM.EVENT.TOPIC_CREATED, onTopicCreated);

:::
</dx-codeblock>

<dx-codeblock>
:::  js

let onTopicDeleted = function(event) {
   const groupID = event.data.groupID // ID of the community to which the topic belongs
   const topicIDList = event.data.topicIDList // List of deleted topic IDs
   console.log(event.data);
};
tim.on(TIM.EVENT.TOPIC_DELETED, onTopicDeleted);

:::
</dx-codeblock>

<dx-codeblock>
:::  js

let onTopicUpdated = function(event) {
   const groupID = event.data.groupID // ID of the community to which the topic belongs
   const topic = event.data.topic // Topic profile
   console.log(event.data);
};
tim.on(TIM.EVENT.TOPIC_UPDATED, onTopicUpdated);

:::
</dx-codeblock>
