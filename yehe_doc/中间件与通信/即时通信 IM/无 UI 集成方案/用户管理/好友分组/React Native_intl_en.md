## Feature Description

To group friends into categories such as "Classmates at university" and "Coworkers", call the following APIs.

## Friend List

### Creating a friend list

Call the `createFriendGroup` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMFriendshipManager/createFriendGroup.html)) to create a friend list.

Sample code:

```javascript
// Create a friend list and add a friend to the list
const groupName = "Friend list 1";
const userIDList = ["user1"];
const friendgroups = await friendshipManager.createFriendGroup(
  groupName,
  userIDList
);
```

### Deleting a friend list

Call the `deleteFriendGroup` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMFriendshipManager/deleteFriendGroup.html)) to delete a friend list.

Sample code:

```javascript
// Delete a friend list
const deleteFriendsgroup = await friendshipManager.deleteFriendGroup(["Friend list 1"]);
```

### Renaming a friend list

Call the `renameFriendGroup` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMFriendshipManager/renameFriendGroup.html)) to rename a friend list.

Sample code:

```javascript
// Rename a friend list
const rename = await friendshipManager.renameFriendGroup("New friend list 1", "Friend list 1");
```

### Getting a friend list

Call the `getFriendGroups` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMFriendshipManager/getFriendGroups.html)) to get a friend list.

Sample code:

```javascript
// Get the information of a friend list by list name
const friendGrous = await friendshipManager.getFriendGroups(["Friend list 1"]);
```

### Adding a friend to a list

Call the `addFriendsToFriendGroup` API ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMFriendshipManager/addFriendsToFriendGroup.html)) to add a friend to a list.

Sample code:

```javascript
// Add a friend to a friend list
const groupName = ["Friend list 1"];
const userIDList = ["user1"];
const addToFrindgroups = await friendshipManager.addFriendsToFriendGroup(
  groupName,
  userIDList
);
```

### Removing a friend from a list

Call `deleteFriendsFromFriendGroup` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMFriendshipManager/deleteFriendsFromFriendGroup.html)) to remove a friend from a list.

Sample code:

```javascript
// Remove a friend from a list
const groupName = ["Friend list 1"];
const userIDList = ["user1"];
const deletefromFriendsGrousps =
  await friendshipManager.deleteFriendsFromFriendGroup(groupName, userIDList);
```
