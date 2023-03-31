## Feature Description

To block a user's messages, add the user to the blocklist.

## Blocklist

### Blocking a user

Call the `addToBlackList` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMFriendshipManager/addToBlackList.html)) to add a user to the blocklist, that is, block the user.

By default, a blocked user does not know that he/she is "blocked". After the user sends a message, the error code indicating that he/she has been blocked will not be returned.
To have the "You have been blocked by the user" error message returned after a blocked user sends a message, you can log in to the [IM console](https://console.cloud.tencent.com/im), select **Feature Configuration** > **Login and Message** > **Blocklist Check**, and disable **Show "Sent successfully" After Sending Messages**. Then the SDK will report error code 20007 after a blocked user sends a message.

```javascript
// Add a user to the blocklist
const addBlackList = await friendshipManager.addToBlackList(["user1"]);
```

### Unblocking a user

Call `deleteFromBlackList` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMFriendshipManager/deleteFromBlackList.html)) to remove a user from the blocklist, after which messages from the user can be received.

```javascript
// Remove a user from the blocklist
const deleteBlackList = await friendshipManager.deleteFromBlackList(["user1"]);
```

### Getting the blocklist

Call `getBlackList` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMFriendshipManager/getBlackList.html)) to view how many users have been blocked and manage them.

```javascript
// Get the blocklist
const blacklist = await friendshipManager.getBlackList();
```
