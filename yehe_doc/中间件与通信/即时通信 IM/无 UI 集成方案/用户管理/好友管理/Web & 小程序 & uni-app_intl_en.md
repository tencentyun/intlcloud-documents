## Feature Description

The IM SDK supports friend management, and users can add and delete friends and set to send messages only to friends.

### Getting contacts

Contacts cached in the SDK can be obtained. When the contacts are updated, the SDK will deliver the [TIM.EVENT.FRIEND_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.FRIEND_LIST_UPDATED) event.

>! This feature is supported by v2.13.0 or later. For more information, see [Tutorial: Relationship Chain Usage Guide (Web & Mini Program)](https://web.sdk.qcloud.com/im/doc/en/tutorial-03-sns.html).

**API**

<dx-codeblock>
:::  js

tim.getFriendList();

:::
</dx-codeblock>

**Parameter**

None

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.getFriendList();
promise.then(function(imResponse) {
  const friendList = imResponse.data; // Contacts
}).catch(function(imError) {
  console.warn('getFriendList error:', imError); // Failed to obtain contacts
});


:::
</dx-codeblock>


### Adding a friend

>! This feature is supported by v2.13.0 or later. For more information, see [Tutorial: Relationship Chain Usage Guide (Web & Mini Program)](https://web.sdk.qcloud.com/im/doc/en/tutorial-03-sns.html).

**API**

<dx-codeblock>
:::  js

tim.addFriend(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name      | Type                | Description                                                  |
| --------- | ------------------- | ------------------------------------------------------------ |
| to        | String              | User ID                                                      |
| source    | String              | Friend source.<br/><li>It consists of two parts: the prefix and the keyword. The former is `AddSource_Type_`, and the latter must be a string of up to eight bytes. We recommend you use an English word or its abbreviation as the keyword. For example, if the keyword is `Android`, this field will be `AddSource_Type_Android`.</li> |
| wording   | String \| undefined | Friending remarks, which can contain up to 256 bytes.        |
| type      | String \| undefined | Friending method (two-way friending by default). Valid values:<br/><li>TIM.TYPES.SNS_ADD_TYPE_SINGLE (one-way friending, where user B is in the friend list of user A but not vice versa)</li><li>TIM.TYPES.SNS_ADD_TYPE_BOTH (two-way friending, where user B is in the friend list of user A and vice versa)</li> |
| remark    | String \| undefined | Friend remarks, which can contain up to 96 bytes.            |
| groupName | String \| undefined | List name, which can contain up to 30 bytes.                 |

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

// Add a friend
let promise = tim.addFriend({
  to: 'user1',
  source: 'AddSource_Type_Web',
  remark: 'Jane',
  groupName: 'Friend',
  wording: 'I'm user0',
  type: TIM.TYPES.SNS_ADD_TYPE_BOTH,
});
promise.then(function(imResponse) {
  // Sent the friend request successfully
  const { code } = imResponse.data;
  if (code === 30539) {
    // 30539 indicates that user1 has set the friend request processing method to manually accept friend requests received. The SDK will trigger the TIM.EVENT.FRIEND_APPLICATION_LIST_UPDATED event.
  } else if (code === 0) {
    // 0 indicates that user1 has set the friend request processing method to automatically accept all friend requests received. The SDK will trigger the TIM.EVENT.FRIEND_LIST_UPDATED event.
  }
}).catch(function(imError) {
  console.warn('addFriend error:', imError); // Failed to add the friend
});

:::
</dx-codeblock>


### Deleting a friend

Delete friends. Both one-way deletion and two-way deletion are supported.

>!
>- This feature is supported by v2.13.0 or later. For more information, see [Tutorial: Relationship Chain Usage Guide (Web & Mini Program)](https://web.sdk.qcloud.com/im/doc/en/tutorial-03-sns.html).
>- We recommend you include up to 100 `userID` values in the `userIDList` at a time, as a large data packet may be rejected by the backend, which requires that a data packet not exceed 1 MB.

**API**

<dx-codeblock>
:::  js

tim.deleteFriend(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name       | Type                | Description                                                  |
| ---------- | ------------------- | ------------------------------------------------------------ |
| userIDList | Array               | List of `userID` values of the friends to be deleted. The number of `userID` values cannot exceed 100 per request. |
| type       | String \| undefined | Deletion mode (two-way deletion by default). Valid values:<br/><li>TIM.TYPES.SNS_DELETE_TYPE_SINGLE (one-way deletion, where user B is deleted from the friend list of user A but not vice versa)</li><li>TIM.TYPES.SNS_DELETE_TYPE_BOTH (two-way deletion, where user B is deleted from the friend list of user A and vice versa)</li> |

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.deleteFriend({
  userIDList: ['user1','user2'],
  type: TIM.TYPES.SNS_DELETE_TYPE_BOTH
});
promise.then(function(imResponse) {
  const { successUserIDList, failureUserIDList } = imResponse.data;
  // List of successfully deleted `userID` values
  successUserIDList.forEach((item) => {
    const { userID } = item;
  });
  // List of `userID` values failed to be deleted
  failureUserIDList.forEach((item) => {
    const { userID, code, message } = item;
  });
  // If the contacts are updated, the SDK will trigger the TIM.EVENT.FRIEND_LIST_UPDATED event.
}).catch(function(imError) {
  console.warn('removeFromFriendList error:', imError);
});

:::
</dx-codeblock>

### Checking the friend relationship

>! This feature is supported by v2.13.0 or later. For more information, see [Tutorial: Relationship Chain Usage Guide (Web & Mini Program)](https://web.sdk.qcloud.com/im/doc/en/tutorial-03-sns.html).

**API**

<dx-codeblock>
:::  js

tim.checkFriend(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name       | Type                | Description                                                  |
| ---------- | ------------------- | ------------------------------------------------------------ |
| userIDList | Array               | List of the `userID` values to be verified. The number of `userID` values cannot exceed 1,000 per request. |
| type       | String \| undefined | Verification mode (two-way verification by default). Valid values:<br/><li>TIM.TYPES.SNS_CHECK_TYPE_SINGLE (one-way verification, where the friend list of user A is checked for user B but not vice versa)</li><li>TIM.TYPES.SNS_CHECK_TYPE_BOTH (two-way verification, where the friend list of user A is checked for user B and vice versa)</li> |

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.checkFriend({
  userIDList: ['user0','user1'],
  type: TIM.TYPES.SNS_CHECK_TYPE_BOTH,
});
promise.then(function(imResponse) {
  const { successUserIDList, failureUserIDList } = imResponse.data;
  // List of the `userID` values that passed the verification
  successUserIDList.forEach((item) => {
    const { userID, code, relation } = item; // The value of code is always 0.
    // Possible results of one-way friend verification are:
    // - relation: TIM.TYPES.SNS_TYPE_NO_RELATION: B is not on A's friend list, but it cannot determine whether A is on B's friend list.
    // - relation: TIM.TYPES.SNS_TYPE_A_WITH_B: B is on A's friend list, but it cannot determine whether A is on B's friend list.
    // Possible results of two-way friend verification are:
    // - relation: TIM.TYPES.SNS_TYPE_NO_RELATION: A and B are not on each other's friend list
    // - relation: TIM.TYPES.SNS_TYPE_A_WITH_B: B is on A's friend list, but A is not on B's friend list
    // - relation: TIM.TYPES.SNS_TYPE_B_WITH_A: B is not on A's friend list, but A is on B's friend list
    // - relation: TIM.TYPES.SNS_TYPE_BOTH_WAY: A and B are on each other's friend list
  });
  // List of the `userID` values that failed the verification
  failureUserIDList.forEach((item) => {
    const { userID, code, message } = item;
  });
}).catch(function(imError) {
  console.warn('checkFriend error:', imError);
});

:::
</dx-codeblock>

### Setting to send messages to friends only

By default, IM SDK does not check the relationship when sending one-to-one messages. This default setting is generally applied in customer service scenarios, where having to friend a customer service agent before chatting is inefficient.
To implement "adding a friend before sending a message", you can log in to the [IM console](https://console.cloud.tencent.com/im), select **Feature Configuration** > **Login and Message** > **Relationship Check**, and enable **Check Relationship for One-to-One Messages**. After it is enabled, a user can send messages only to friends. If the user sends a message to a non-friend user, the SDK will report error code 20009.
