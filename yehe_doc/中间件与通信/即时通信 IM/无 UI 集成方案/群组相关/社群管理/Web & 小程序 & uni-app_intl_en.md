## Feature Description

A community is a large group of people brought together by common topics, and multiple topics can be created under the same community based on different interests. A community is used to manage members. All its topics are shared among members, who can send and receive messages independently.

## Community Management

### Creating a community

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
  console.warn('createGroup error:', imError); // Failed to create the group
});

:::
</dx-codeblock>


### Getting the list of topic-enabled communities

>! This API is supported only by v2.19.1 or later and applies only to topic-enabled communities. To use the feature, you need to [purchase the Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577#.E5.8D.87.E7.BA.A7.E5.BA.94.E7.94.A8), go to the [**console**](https://console.cloud.tencent.com/im/qun-setting), select **Group feature configuration**, and enable the **Community** feature.

**API**

<dx-codeblock>
:::  js

tim.getJoinedCommunityList();

:::
</dx-codeblock>

**Parameter**

None

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

// Get the list of topic-enabled communities
let promise = tim.getJoinedCommunityList();
promise.then(function(imResponse) { // Obtained successfully
  console.log(imResponse.data.groupList); // List of topic-enabled communities
}).catch(function(imError) { // Failed to obtain
  console.warn('getJoinedCommunityList error:', imError); // Failure message
});

:::
</dx-codeblock>

### Creating a topic

>!
>- This API is supported only by v2.19.1 or later and applies only to topic-enabled communities. To use the feature, you need to [purchase the Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577#.E5.8D.87.E7.BA.A7.E5.BA.94.E7.94.A8) and [apply for enablement](https://intl.cloud.tencent.com/document/product/1047/44322).
>- Before using this API, you must call [createGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createGroup) to create a topic-enabled community.

**API**

<dx-codeblock>
:::  js

tim.createTopicInCommunity(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID     | String | 		Community ID of the topic |
| topicName | String | Topic name |
| topicID | String | A custom topic ID must be in the format of "community ID + custom topic ID", such as "@TGS#_xxx@TOPIC#_xxx". |
| avatar | String | Topic profile photo |
| notification | String | Topic notice |
| introduction | String | Topic introduction |
| customData | String | Custom topic information |

**Returned value**

`Promise` object

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
}).catch(function(imError) { // Failed to create
  console.warn('createTopicInCommunity error:', imError); // Failed to create the topic
});

:::
</dx-codeblock>

### Deleting a topic

>! This API is supported only by v2.19.1 or later and applies only to topic-enabled communities. To use the feature, you need to [purchase the Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577#.E5.8D.87.E7.BA.A7.E5.BA.94.E7.94.A8) and [apply for enablement](https://intl.cloud.tencent.com/document/product/1047/44322).

**API**

<dx-codeblock>
:::  js

tim.deleteTopicFromCommunity(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID     | String | 		Community ID of the topic |
| topicIDList | Array \| undefined | List of topic IDs. If it is not passed in, all the topics are deleted. |

**Returned value**

`Promise` object

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

### Modifying the information of a topic

>! This API is supported only by v2.19.1 or later and applies only to topic-enabled communities. To use the feature, you need to [purchase the Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577#.E5.8D.87.E7.BA.A7.E5.BA.94.E7.94.A8) and [apply for enablement](https://intl.cloud.tencent.com/document/product/1047/44322).

**API**

<dx-codeblock>
:::  js

tim.updateTopicProfile(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name | Type | Description |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID     | String | 		Community ID of the topic |
| topicID | String | Topic ID, which is required |
| topicName | String \| undefined | Topic name |
| avatar | String \| undefined | Topic profile photo |
| notification | String \| undefined | Topic notice |
| introduction | String \| undefined | Topic introduction |
| customData | String \| undefined | Custom topic information |
| muteAllMembers | Boolean \| undefined | Muting all. Valid values: `true`: mute all; `false`: unmute all. |

**Returned value**

`Promise` object

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
promise.then(function(imResponse) { // Set the topic profile successfully
  console.log(imResponse.data.topic); // Return the modified topic profile
}).catch(function(imError) { // Failed to set the topic profile
  console.warn('updateTopicProfile error:', imError); // Failed to set the topic profile
});

:::
</dx-codeblock>

### Getting the topic list

>! This API is supported only by v2.19.1 or later and applies only to topic-enabled communities. To use the feature, you need to [purchase the Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577#.E5.8D.87.E7.BA.A7.E5.BA.94.E7.94.A8) and [apply for enablement](https://intl.cloud.tencent.com/document/product/1047/44322).

**API**

<dx-codeblock>
:::  js

tim.getTopicList(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID     | String | 		Community ID of the topic |
| topicIDList | Array \| undefined | List of topic IDs. If it is not passed in, all the topics are obtained. |

**Returned value**

`Promise` object

**Sample**

<dx-codeblock>
:::  js

// Get a specified topic
let promise = tim.getTopicList({
  groupID: 'group1',
  topicIDList: ['topicID'],
});
promise.then(function(imResponse) { // Obtained successfully
  const { successTopicList, failureTopicList } = imResponse.data;
  // List of topics obtained successfully
  successTopicList.forEach((item) => {
     const { topicID } = item;
  });
  // List of topics failed to be obtained
  failureTopicList.forEach((item) => {
     const { topicID, code, message } = item;
  })
}).catch(function(imError) { // Failed to obtain
  console.warn('getTopicList error:', imError); // Failed to obtain the topic list
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// Get all the topics
let promise = tim.getTopicList({
  groupID: 'group1',
});
promise.then(function(imResponse) { // Obtained successfully
  const { successTopicList, failureTopicList } = imResponse.data;
  // List of topics obtained successfully
  successTopicList.forEach((item) => {
     const { topicID } = item;
  });
  // List of topics failed to be obtained
  failureTopicList.forEach((item) => {
     const { topicID, code, message } = item;
  })
}).catch(function(imError) { // Failed to obtain
  console.warn('getTopicList error:', imError); // Failed to obtain the topic list
});

:::
</dx-codeblock>

### Listening for a topic callback

<dx-codeblock>
:::  js

let onTopicCreated = function(event) {
   const groupID = event.data.groupID // Group ID of the topic
   const topicID = event.data.topicID // Topic ID
   console.log(event.data);
};
tim.on(TIM.EVENT.TOPIC_CREATED, onTopicCreated);

:::
</dx-codeblock>

<dx-codeblock>
:::  js

let onTopicDeleted = function(event) {
   const groupID = event.data.groupID // Group ID of the topic
   const topicIDList = event.data.topicIDList // List of deleted topic IDs
   console.log(event.data);
};
tim.on(TIM.EVENT.TOPIC_DELETED, onTopicDeleted);

:::
</dx-codeblock>

<dx-codeblock>
:::  js

let onTopicUpdated = function(event) {
   const groupID = event.data.groupID // Group ID of the topic
   const topic = event.data.topic // Topic profile
   console.log(event.data);
};
tim.on(TIM.EVENT.TOPIC_UPDATED, onTopicUpdated);

:::
</dx-codeblock>

