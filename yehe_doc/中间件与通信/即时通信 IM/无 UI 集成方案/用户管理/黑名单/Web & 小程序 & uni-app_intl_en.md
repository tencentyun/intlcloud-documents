## Feature Description

To block a user's messages, add the user to the blocklist.

## Blocklist
### Blocking a user

Add a user to the blocklist. By adding a user to the blocklist, you can block all the messages sent by the user. Therefore, this API can be used to block the messages of a specified user.

- If user A and user B are friends, the two-way friend relationship is terminated when either A or B is blocked by the other user.
- If either user A or user B is blocked by the other user, neither user A nor user B can start a conversation with the other user.
- If either user A or user B is blocked by the other user, neither user A nor user B can send a friend request to the other user.

**API**

<dx-codeblock>
:::  js

tim.addToBlacklist(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name       | Type  | Description                                                  |
| ---------- | ----- | ------------------------------------------------------------ |
| userIDList | Array | List of `userID` values of the users to be added to the blocklist. The number of `userID` values cannot exceed 1,000 per request. |

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.addToBlacklist({userIDList: ['user1', 'user2']}); // Note: Even if only one `userID` value is added to the blocklist, the value must be of the array type, for example, userIDList: ['user1'].
promise.then(function(imResponse) {
  console.log(imResponse.data); // `userID` values added to the blocklist successfully. The value is an array that stores `userID` values - [userID].
}).catch(function(imError) {
  console.warn('addToBlacklist error:', imError); // Failed to add the user to the blocklist
});

:::
</dx-codeblock>

### Unblocking a user

After a user is removed from the blocklist, messages from the user can be received.

**API**

<dx-codeblock>
:::  js

tim.removeFromBlacklist(options);

:::
</dx-codeblock>

**Parameter**

The `options` parameter is of the `Object` type. It contains the following attribute values:

| Name       | Type  | Description                                                  |
| ---------- | ----- | ------------------------------------------------------------ |
| userIDList | Array | List of `userID` values of the users to be removed from the blocklist. The number of `userID` values cannot exceed 1,000 per request. |

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.removeFromBlacklist({userIDList: ['user1', 'user2']}); // Note: Even if only one `userID` value is removed from the blocklist, the value must be of the array type, for example, userIDList: ['user1'].
promise.then(function(imResponse) {
  console.log(imResponse.data); // All `userID` values removed from the blocklist successfully. The value is an array that stores `userID` values - [userID].
}).catch(function(imError) {
  console.warn('removeFromBlacklist error:', imError); // Failed to remove the user from the blocklist
});

:::
</dx-codeblock>

### Getting the blocklist

**API**

<dx-codeblock>
:::  js

tim.getBlacklist();

:::
</dx-codeblock>

**Parameter**

None

**Returned value**

`Promise` object.

**Sample**

<dx-codeblock>
:::  js

let promise = tim.getBlacklist();
promise.then(function(imResponse) {
  console.log(imResponse.data); // Your blocklist. The value is an array that stores `userID` values - [userID].
}).catch(function(imError) {
  console.warn('getBlacklist error:', imError); // Failed to obtain the blocklist
});

:::
</dx-codeblock>
