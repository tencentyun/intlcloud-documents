## Feature Description
To group friends into categories such as "Classmates at university" and "Coworkers", call the following APIs.

## Friend List

### Creating a friend list

>! This feature is supported by v2.13.0 or later. For more information, see [Tutorial: Relationship Chain Usage Guide (Web & Mini Program)](https://web.sdk.qcloud.com/im/doc/en/tutorial-03-sns.html).

**API**

<dx-codeblock>
:::  js

tim.createFriendGroup(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name       | Type   | Description                                                  |
| ---------- | ------ | ------------------------------------------------------------ |
| name       | String | List name                                                    |
| userIDList | Array  | List of `userID` values of the friends to be added to the list |

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.createFriendGroup({
  name: 'My friend list 1',
  userIDList: ['user0','user1']
});
promise.then(function(imResponse) {
  const { friendGroup,failureUserIDList } = imResponse;
  // friendGroup - Friend list instance
  // failureUserIDList - List of the `userID` values failed to be added
  // When the friend list is successfully created, the SDK triggers the TIM.EVENT.FRIEND_GROUP_LIST_UPDATED event.
}).catch(function(imError) {
  console.warn('getFriendGroupInfo error:', imError); // Failed to obtain the information
});

:::
</dx-codeblock>

### Deleting a friend list

>! This feature is supported by v2.13.0 or later. For more information, see [Tutorial: Relationship Chain Usage Guide (Web & Mini Program)](https://web.sdk.qcloud.com/im/doc/en/tutorial-03-sns.html).

**API**

<dx-codeblock>
:::  js

tim.deleteFriendGroup(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name | Type   | Description |
| ---- | ------ | ----------- |
| name | String | List name   |

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.deleteFriendGroup({
  name: 'My friend list 1',
});
promise.then(function(imResponse) {
  console.log(imResponse.data); // Friend list instance
  // When the friend list is successfully deleted, the SDK triggers the TIM.EVENT.FRIEND_GROUP_LIST_UPDATED event.
}).catch(function(imError) {
  console.warn('deleteFriendGroup error:', imError); // Failed to obtain the information
});
:::
</dx-codeblock>

### Renaming a friend list

>! This feature is supported by v2.13.0 or later. For more information, see [Tutorial: Relationship Chain Usage Guide (Web & Mini Program)](https://web.sdk.qcloud.com/im/doc/en/tutorial-03-sns.html).

**API**

<dx-codeblock>
:::  js

tim.renameFriendGroup(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name    | Type   | Description   |
| ------- | ------ | ------------- |
| oldName | String | Old list name |
| newName | String | New list name |

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.renameFriendGroup({
  oldName: 'Friends',
  newName: 'Besties'
});
promise.then(function(imResponse) {
  console.log(imResponse.data); // Friend list instance
  // When the name of a friend list is changed successfully, the SDK triggers the TIM.EVENT.FRIEND_GROUP_LIST_UPDATED event.
}).catch(function(imError) {
  console.warn('updateMyProfile error:', imError);
});

:::
</dx-codeblock>


### Getting a friend list

The friend lists cached in the SDK can be obtained. When a friend list is updated, the SDK will deliver the [TIM.EVENT.FRIEND_GROUP_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.FRIEND_GROUP_LIST_UPDATED) event.

>! This feature is supported by v2.13.0 or later. For more information, see [Tutorial: Relationship Chain Usage Guide (Web & Mini Program)](https://web.sdk.qcloud.com/im/doc/en/tutorial-03-sns.html).

**API**

<dx-codeblock>
:::  js

tim.getFriendGroupList();

:::
</dx-codeblock>

**Parameter**

None

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.getFriendGroupList();
promise.then(function(imResponse) {
  const friendGroupList = imResponse.data; // Friend list
}).catch(function(imError) {
  console.warn('getFriendGroupList error:', imError); // Failed to obtain the friend list
});

:::
</dx-codeblock>


### Adding a friend to a list

>! This feature is supported by v2.13.0 or later. For more information, see [Tutorial: Relationship Chain Usage Guide (Web & Mini Program)](https://web.sdk.qcloud.com/im/doc/en/tutorial-03-sns.html).

**API**

<dx-codeblock>
:::  js

tim.addToFriendGroup(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name       | Type   | Description                                        |
| ---------- | ------ | -------------------------------------------------- |
| name       | String | List name                                          |
| userIDList | Array  | List of `userID` values of the friends to be added |

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.addToFriendGroup({
  name: 'My friend list 1',
  userIDList: ['user1','user2'],
});
promise.then(function(imResponse) {
  const { friendGroup, failureUserIDList } = imResponse.data;
  // friendGroup - Friend list instance
  // failureUserIDList - List of the `userID` values failed to be added
  // When the friends are successfully added to the friend list, the SDK triggers the TIM.EVENT.FRIEND_GROUP_LIST_UPDATED event.
}).catch(function(imError) {
  console.warn('addToFriendGroup error:', imError); // Failed to obtain the information
});

:::
</dx-codeblock>

### Removing a friend from a list

>! This feature is supported by v2.13.0 or later. For more information, see [Tutorial: Relationship Chain Usage Guide (Web & Mini Program)](https://web.sdk.qcloud.com/im/doc/en/tutorial-03-sns.html).

**API**

<dx-codeblock>
:::  js

tim.removeFromFriendGroup(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name       | Type   | Description                                          |
| ---------- | ------ | ---------------------------------------------------- |
| name       | String | List name                                            |
| userIDList | Array  | List of `userID` values of the friends to be removed |

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.removeFromFriendGroup({
  name: 'My friend list 1',
  userIDList: ['user1','user2'],
});
promise.then(function(imResponse) {
  const { friendGroup, failureUserIDList } = imResponse.data;
  // friendGroup - Friend list instance
  // failureUserIDList - List of the `userID` values failed to be added
  // When the friends are successfully removed from the friend list, the SDK triggers the TIM.EVENT.FRIEND_GROUP_LIST_UPDATED event.
}).catch(function(imError) {
  console.warn('addToFriendGroup error:', imError); // Failed to obtain the information
});

:::
</dx-codeblock>