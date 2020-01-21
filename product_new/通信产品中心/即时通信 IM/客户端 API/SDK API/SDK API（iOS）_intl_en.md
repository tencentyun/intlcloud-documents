
## TIMManager

As a core module of the IM SDK, TIMManager works for initialization, login, conversation creation, and push management of the IM SDK.
- Initialization: the prerequisite for using the IM SDK. You need to call the init API first before calling other APIs.
- Login: you need to configure the SDKAppID, UserID, and UserSig before using IM.
- Conversation: each time you start a conversation, you open a conversation window. A conversation can be a C2C chat or a group chat.
- Push: you can configure and manage features related to offline push, including tokens and feature enabling/disabling.

### Initialization APIs
| API | Description |
| --- | --- |
| **sharedInstance** | Obtains the instance of **TIMManager**. |
| **initSdk** | Initializes the SDK and specifies the global configurations. |
| **unInit** | Uninitialize the SDK. |
| **getGlobalConfig** | Obtains global configurations. |
| **setUserConfig** | Specifies user configurations. |
| **getUserConfig** | Obtains user configurations. |
| **addMessageListener** | Adds a message receiving listener. |
| **removeMessageListener** | Deletes a message receiving listener. |


### Login APIs
| API | Description |
| --- | --- |
| **login** | Logs in. |
| **autoLogin** | Enables auto-login. |
| **logout** | Logs out. |
| **getLoginUser** | Obtains the login user. |
| **getLoginStatus** | Obtains the current login status. |


### Conversation management APIs
| API | Description |
| --- | --- |
| **getConversationList** | Obtains the list of conversations. |
| **getConversation** | Obtains a conversation. |
| **deleteConversation** | Deletes a conversation. |
| **deleteConversationAndMessages** | Deletes a conversation and its messages. |


### Configures APNs push
| API | Description |
| --- | --- |
| **setToken** | Configures the client token and the certificate business ID. |
| **setAPNS** | Configures APNs. |
| **getAPNSConfig** | Obtains the APNs configurations. |
| **doBackground** | Reports that the app is running in the backend. |
| **doForeground** | Reports that the app is running in the frontend. |


### APIs for querying local conversations and messages without login
| API | Description |
| --- | --- |
| **initStorage** | Loads the local storage without login. |


### Debugging APIs
| API | Description |
| --- | --- |
| **GetVersion** | Obtains the version number. |
| **log** | Prints the log. |
| **getLogPath** | Obtains the log file path. |
| **getIsLogPrintEnabled** | Obtains the log printing status. |
| **getLogLevel** | Obtains the log level. |


## TIMConversation

Each time you start a conversation, you open a conversation window. A conversation can be a C2C chat or a group chat.
All API functions provided by TIMConversation are about message operations, including sending messages, obtaining message history, setting read receipt, recalling messages, and deleting messages.

### APIs for sending messages
| API | Description |
| --- | --- |
| **sendMessage** | Sends a message. |
| **sendOnlineMessage** | Sends an online message. (Incognito) |


### APIs for obtaining messages
| API | Description |
| --- | --- |
| **getMessage** | Pulls message history from the cloud. |
| **getLocalMessage** | Obtains message history from the local database. |
| **getLastMsg** | Obtains the last message of the current conversation. |


### APIs for setting read receipt
| API | Description |
| --- | --- |
| **setReadMessage** | Marks a message as read. |
| **getUnReadMessageNum** | Obtains the number of unread messages. |


### APIs for recalling and deleting messages
| API | Description |
| --- | --- |
| **revokeMessage** | Recalls a sent message. |
| **deleteLocalMessage** | Deletes local message history of the current conversation. |


### APIs for obtaining conversation information
| API | Description |
| --- | --- |
| **getType** | Obtains the conversation type. |
| **getReceiver** | Obtains the conversation ID. |
| **getGroupName** | Obtains the group name. |


### Drafts APIs
| API | Description |
| --- | --- |
| **setDraft** | Adds an unfinished message as a draft. |
| **getDraft** | Obtains a draft. |


### APIs for importing messages to a conversation
| API | Description |
| --- | --- |
| **saveMessage** | Adds a message to the list of local messages without sending it. |
| **importMessages** | Imports a message to the local database. |


## TIMGroupManager

Group management module is used to create groups, delete groups, invite/delete group members, modify group/member profiles.

### API for obtaining a group instance
| API | Description |
| --- | --- |
| **sharedInstance** | Obtains the instance of TIMGroupManager. |


### APIs for creating, disbanding, joining, and quitting groups
| API | Description |
| --- | --- |
| **createPrivateGroup** | Creates a private group. |
| **createPublicGroup** | Creates a public group. |
| **createChatRoomGroup** | Creates a chat room. |
| **createAVChatRoomGroup** | Creates an audio & video chat room. |
| **createGroup** | Creates a group with specific type and ID. |
| **createGroup** | Creates a custom group. |
| **deleteGroup** | Disbands a group. |
| **joinGroup** | Applies for joining a group. |
| **quitGroup** | Quits a group. |


### APIs for inviting and deleting group members
| API | Description |
| --- | --- |
| **inviteGroupMember** | Invites a friend to join a group. |
| **deleteGroupMemberWithReason** | Deletes a group member. |


### APIs for obtaining group information
| API | Description |
| --- | --- |
| **getGroupList** | Obtains the group lists. |
| **getGroupInfo** | Obtains group information from the server. |
| **queryGroupInfo** | Obtains group information from local storage. |
| **getGroupMembers** | Obtains the list of group members. |
| **getGroupSelfInfo** | Obtains your profile in the group. |
| **getGroupMembersInfo** | Obtains the profiles of specific members. |
| **getGroupMembers** | Obtains a list of a specific type of group members (filtered by field, displayed in pagination mode). |
| **getReciveMessageOpt** | Obtains the options for receiving messages. |


### APIs for modifying group information
| API | Description |
| --- | --- |
| **modifyGroupName** | Modifies the group name. |
| **modifyGroupIntroduction** | Modifies the group introduction. |
| **modifyGroupNotification** | Modifies the group announcement. |
| **modifyGroupFaceUrl** | Modifies the group profile photo. |
| **modifyGroupAddOpt** | Modifies the options for joining the group. |
| **modifyGroupSearchable** | Modifies the search attributes. |
| **modifyReceiveMessageOpt** | Modifies the options for receiving messages. |
| **modifyGroupAllShutup** | Modifies the global mute attributes. |
| **modifyGroupCustomInfo** | Modifies the custom fields. |
| **modifyGroupOwner** | Transfers the group ownership. |


### APIs for modifying group member profiles
| API | Description |
| --- | --- |
| **modifyGroupMemberInfoSetNameCard** | Modifies the name card of a group member. |
| **modifyGroupMemberInfoSetRole** | Modifies the role of a group member. |
| **modifyGroupMemberVisible** | Modifies the visibility attribute of a group member. |
| **modifyGroupMemberInfoSetSilence** | Mutes users. |
| **modifyGroupMemberInfoSetCustomInfo** | Modifies the custom fields of a group member. |


### APIs for handling pending group requests
| API | Description |
| --- | --- |
| **getPendencyFromServer** | Obtains the list of pending group requests. |
| **pendencyReport** | Reports that the pending group requests have been read. |


## TIMFriendshipManager

TIMFriendshipManager is the module for managing profile relationship chains. You can use it to add friends, delete friends, obtain friend information, modify friend profiles, etc.

| API | Description |
| --- | --- |
| **sharedInstance** | Obtains the instance of TIMFriendshipManager. |
| **modifySelfProfile** | Configures your personal profile. |
| **getSelfProfile** | Obtains your personal profile. |
| **querySelfProfile** | Queries your personal profile in the cache. |
| **getUsersProfile** | Obtains profiles of specific users. |
| **queryUserProfile** | Queries the profile of a specific user in the cache. |
| **getFriendList** | Obtains the friends list. |
| **queryFriend** | Queries the relationship chain data of a user in the cache. |
| **queryFriendList** | Obtains the relationship chain lists in the cache. |
| **checkFriends** | Checks the friendships of a specific user. |
| **addFriend** | Adds friend. |
| **doResponse** | Responds to a friend request. |
| **deleteFriends** | Deletes friend. |
| **modifyFriend** | Modifies friend attributes. |
| **getPendencyList** | Deletes the list of pending requests. |
| **deletePendency** | Deletes pending requests. |
| **pendencyReport** | Reports that the pending requests have been read. |
| **getBlackList** | Obtains the blacklist. |
| **addBlackList** | Adds a user to the blacklist. |
| **deleteBlackList** | Deletes a specific user from the blacklist. |
| **createFriendGroup** | Creates a friend group. |
| **getFriendGroups** | Obtains specified friend group information. |
| **deleteFriendGroup** | Deletes a friend group. |
| **renameFriendGroup** | Renames a friend group. |
| **addFriendsToFriendGroup** | Adds a friend to a specific friend group. |
| **deleteFriendsFromFriendGroup** | Deletes specific friends from a friend group. |


## TIMMessage

**TIMMessage** consists of multiple message elements **TIMElem**. The TIMElem can be text or an image, and each message can contain multiple texts or images. <!--For more information, see [Receiving and Sending Messages]().-->

| API | Description |
| --- | --- |
| **addElem** | Adds Elem. |
| **getElem** | Obtains the element of the corresponding index. |
| **elemCount** | Obtains the number of elements. |
| **setBusinessCmd** | Configures the business command words. |
| **status** | Queries message status. |
| **isSelf** | Confirms whether you are the sender. |
| **sender** | Obtains the message sender. |
| **msgId** | Obtains the message ID. |
| **uniqueId** | Obtains the the message uniqueId. |
| **timestamp** | Obtains the message timestamp. |
| **isReaded** | Checks whether you have read the message. |
| **isPeerReaded** | Checks whether the message has been read (Work for C2C message only.) |
| **locator** | Obtains the message locator. |
| **respondsToLocator** | Checks whether the message is the one specified by the locator. |
| **remove** | Deletes a message. |
| **getConversation** | Obtains a conversation. |
| **getSenderProfile** | Obtains the sender profile. |
| **getSenderGroupMemberProfile** | Obtains the sender profile in the group. |
| **setPriority** | Configures message priority (for group message only). |
| **getPriority** | Obtains message priority (for group message only).|
| **setOfflinePushInfo** | Configures parameters related to offline push. |
| **getOfflinePushInfo** | Obtains the offline push configurations of messages. |
| **setCustomInt** | Configures the custom integer. The default value is 0. |
| **customInt** | Obtains the custom integer. |
| **setCustomData** | Configures the custom data. The default data is an empty string (`""`). |
| **customData** | Obtains the custom data. |
| **copyFrom** | Copies the attributes of a message, including `Elem`, `priority`, `online`, and `offlinePushInfo`. |
| **convertToImportedMsg** | Imports the message to local storage. |
| **setTime** | Configures the message timestamp. |
| **setSender** | Configures the message sender. |


