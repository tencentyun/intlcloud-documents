## TIMManager

As a core module of the IM SDK, TIMManager works for initialization, login, conversation creation, and push management of the IM SDK.
- Initialization: the prerequisite for using the IM SDK. You need to call the init API first before calling other APIs.
- Login: you need to configure the SDKAppID, UserID, and UserSig before using IM.
- Conversation: each time you start a conversation, you open a conversation window. A conversation can be a C2C chat or a group chat.
- Push: you can configure and manage features related to offline push, including tokens and feature enabling/disabling.

### Initialization APIs
| API | Description |
| --- | --- |
| **getInstance** | Obtains the instance of **TIMManager**. |
| **init** | Initializes the SDK and specifies the global configurations. |
| **unInit** | Deinitializes the SDK. |
| **getSdkConfig** | Obtains global configurations. |
| **setUserConfig** | Specifies user configurations. |
| **getUserConfig** | Obtains user configurations. |
| **addMessageListener** | Adds a message receiving listener. |
| **removeMessageListener** | Removes a message receiving listener. |
| **isInited** | Checks whether the SDK is initialized. |


### Login APIs
| API | Description |
| --- | --- |
| **login** | Logs in. |
| **autoLogin** | Enables auto-login. |
| **logout** | Logs out. |
| **getLoginUser** | Obtains the login user. |


### Conversation management APIs
| API | Description |
| --- | --- |
| **getConversationList** | Obtains the list of conversations. |
| **getConversation** | Obtains a conversation. |
| **deleteConversation** | Deletes a conversation. |
| **deleteConversationAndLocalMsgs** | Deletes a conversation and its messages. |


### APIs for configuring offline push
| API | Description |
| --- | --- |
| **setOfflinePushToken** | Configures the client token and the certificate business ID. |
| **setOfflinePushSettings** | Initializes the offline push configurations. Use this API on condition that you have logged in. |
| **getOfflinePushSettings** | Obtains the offline push configurations. Use this API on condition that you have logged in. |
| **setOfflinePushListener** | Configures the message notification listener which works while the app is running on the backend. (This API is deprecated.) |
| **doBackground** | Reports that the app is running in the backend. |
| **doForeground** | Reports that the app is running in the frontend. |


### APIs for querying local conversations and messages without login
| API | Description |
| --- | --- |
| **initStorage** | Loads the local storage without login. |


### Debugging APIs
| API | Description |
| --- | --- |
| **getVersion** | Obtains the version number. |
| **addMessageUpdateListener** | Adds a message update listener to get message updates. |
| **removeMessageUpdateListener** | Deletes a message update listener. |
| **getNetworkStatus** | Obtains the network connection status. |
| **getServerTimeDiff** | Obtains the time difference between the server and local device, expressed in seconds. `Time difference = svrTime – localTime`. |


## TIMConversation

Each time you start a conversation, you open a conversation window. A conversation can be a C2C chat or a group chat.
All API functions provided by **TIMConversation** are related to message operations, including sending messages, obtaining message history, setting read receipt, recalling messages, and deleting messages. 

### APIs for sending messages
| API | Description |
| --- | --- |
| **sendMessage** | Sends a message. |
| **sendOnlineMessage** | Sends an online message. (Incognito)  |


### APIs for obtaining messages
| API | Description |
| --- | --- |
| **getMessage** | Pulls message history from the cloud. |
| **getLocalMessage** | Obtains message history from the local database. |
| **getLastMsg** | Obtains the last message of the current conversion. |


### APIs for marking message as read
| API | Description |
| --- | --- |
| **setReadMessage** | Marks a message as read. |
| **getUnreadMessageNum** | Obtains the number of unread messages. |


### APIs for recalling and deleting messages
| API | Description |
| --- | --- |
| **revokeMessage** | Recalls a message that has been sent. |
| **deleteLocalMessage** | Deletes local message history of the current conversation. |


### APIs for obtaining conversation information
| API | Description |
| --- | --- |
| **getType** | Obtains the conversation type. |
| **getPeer** | Obtains the conversation ID. |
| **getGroupName** | Obtains the group name. |


### Drafts APIs
| API | Description |
| --- | --- |
| **setDraft** | Adds an unfinished message as a draft. |
| **getDraft** | Obtains a draft. |
| **hasDraft** | Checks whether the current conversation has a draft. |


### APIs for importing messages to a conversation
| API | Description |
| --- | --- |
| **saveMessage** | Adds a message to the list of local messages without sending it. |
| **importMsg** | Imports a message to the local database. |
| **findMessages** | Searches for a message using the given message locator. |


## TIMGroupManager

Group management module is used to create groups, delete groups, invite/delete group members, modify group/member profiles.

### API for obtaining a group instance
| API | Description |
| --- | --- |
| **getInstance** | Obtains the instance of TIMGroupManager. |


### APIs for creating, disbanding, joining, and quitting groups
| API | Description |
| --- | --- |
| **createGroup** | Creates a group. |
| **deleteGroup** | Disbands a group. |
| **applyJoinGroup** | Applies for joining a group. |
| **quitGroup** | Quits a group. |


### APIs for inviting and deleting group members
| API | Description |
| --- | --- |
| **inviteGroupMember** | Invites a friend to a group. |
| **deleteGroupMember** | Deletes a group member. |


### APIs for obtaining group information
| API | Description |
| --- | --- |
| **getGroupList** | Obtains the group lists. |
| **getGroupInfo** | Obtains group information from the server. |
| **queryGroupInfo** | Obtains group information from local storage. |
| **getGroupMembers** | Obtains the list of group members. |
| **getSelfInfo** | Obtains your profile in the group. |
| **getGroupMembersInfo** | Obtains the profiles of specific members. |
| **getGroupMembersByFilter** | Obtains a list of a specific type of group members (filtered by field, displayed in pagination mode). |


### APIs for modifying group information
| API | Description |
| --- | --- |
| **modifyGroupInfo** | Modifies the group information. |
| **modifyGroupOwner** | Transfers the group ownership. |


### APIs for modifying group member profiles
| API | Description |
| --- | --- |
| **modifyMemberInfo** | Modifies a group member's profile. |


### APIs for handling pending group requests
| API | Description |
| --- | --- |
| **getGroupPendencyList** | Obtains the list of pending group requests. |
| **reportGroupPendency** | Reports that the pending group requests have been read. |


## TIMFriendshipManager

TIMFriendshipManager is the module for managing profile relationship chains. You can use it to add friends, delete friends, obtain friend information, modify friend profiles, etc.

| API | Description |
| --- | --- |
| **getInstance** | Obtains the instance of TIMFriendshipManager. |
| **init** | Initializes TIMFriendshipManager. |
| **getUsersProfile** | Obtains profiles of specific users. |
| **getSelfProfile** | Obtains your personal profile. |
| **querySelfProfile** | Obtains your personal local profile. If there is no available data, null is returned. |
| **queryUserProfile** | Obtains a local user profile. If there is no available data, null is returned. |
| **modifySelfProfile** | Modifies your personal profile. |
| **getFriendList** | Obtains the friends list. |
| **queryFriendList** | Obtains the relationship chain lists in the cache. The cached data source is the return result of the previous call of **getFriendList**. Make sure that getFriendList has been called. |
| **queryFriend** | Queries the relationship chain of a friend in the cache. The cached data source is the return result of the previous call of **getFriendList**. Make sure that getFriendList has been called. |
| **addFriend** | Adds friend. |
| **deleteFriends** | Deletes friend. |
| **modifyFriend** | Modifies a friend profile. |
| **doResponse** | Processes a friend request. |
| **createFriendGroup** | Creates a friend group. |
| **getFriendGroups** | Obtains specific friend group. If groupNames is set to null, all friend groups will be returned. |
| **deleteFriendGroup** | Deletes a friend group. |
| **renameFriendGroup** | Renames a friend group. |
| **addFriendsToFriendGroup** | Adds friends to a friend group. |
| **deleteFriendsFromFriendGroup** | Deletes specific friends from a friend group. |
| **getPendencyList** | Deletes the list of pending requests. |
| **deletePendency** | Deletes a pending request. |
| **pendencyReport** | Reports that the pending requests have been read. |
| **getBlackList** | Obtains the blacklist. |
| **addBlackList** | Adds a user to the blacklist. |
| **deleteBlackList** |Deletes a specific user from the blacklist. |
| **checkFriends** | Checks the friendship with a specific user. |


## TIMMessage

**TIMMessage** consists of multiple message elements (TIMElem). The TIMElem can be text or an image, and each message can contain multiple texts or images. <!--For more information, see [Receiving and Sending Messages]().-->

| API | Description |
| --- | --- |
| **addElement** | Adds a message element. |
| **getElement** | Obtains the message element of the corresponding index. |
| **getElementCount** | Obtains the number of message elements. |
| **status** | Queries message status. |
| **isSelf**| Checks whether you are the message sender. |
| **getSender** | Queries who is the message sender. |
| **getMsgId** | Obtains the message ID. |
| **getMsgUniqueId** | Obtains the uniqueId of the message. |
| **timestamp** | Obtains the message timestamp. |
| **isRead** | Checks whether you have read the message. |
| **isPeerReaded** | Checks whether the message receiver has read the message This API is applicable to C2C conversations only. |
| **getMessageLocator** | Obtains the message locator. |
| **checkEquals** | Checks whether the message is the one specified by the locator. |
| **remove** | Deletes a message. |
| **getConversation** | Obtains a conversation. |
| **getSenderProfile** | Obtains the sender profile. |
| **getSenderGroupMemberProfile** | Obtains the sender profile in the group. |
| **setPriority** | Configures message priority (for group message only).|
| **getPriority** | Obtains message priority (for group message only). |
| **setOfflinePushSettings | Configures parameters related to offline push. |
| **getOfflinePushSettings** | Obtains the offline push configurations of messages. |
| **setCustomInt** | Configures the custom integer. The default value is 0. This attribute is for local use only. |
| **getCustomInt** | Obtains the custom integer. |
| **setCustomStr** | Configures the custom content. The default value is the empty string `""`. This attribute is for local use only. |
| **getCustomStr** | Obtains the value of the custom content. |
| **copyFrom** | Copies message content to the current message, including `Elem`, `priority`, `online`, and `offlinePushInfo`. |
| **convertToImportedMsg** | Imports the message to local storage. |
| **setTimestamp** | Configures the message timestamp. |
| **setSender** | Configures the sender ID. |
| **getRecvFlag** | Obtains the notification type of the message. |
| **getRand** | Obtains the random code of the message. |
| **getSeq** | Obtains the sequence number of the message. |


