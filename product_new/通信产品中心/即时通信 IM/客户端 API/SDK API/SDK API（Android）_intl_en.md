## TIMManager

As a core module of the IM SDK, TIMManager works for initialization, login, conversation creation, and push management of the IM SDK.
- Initialization: the prerequisite for using the IM SDK. You need to call the init API first before calling other APIs.
- Login: you need to configure the SDKAppID, UserID, and UserSig before using IM.
- Conversation: each time you start a conversation, you open a conversation window. A conversation can be a C2C chat or a group chat.
- Push: you can configure and manage features related to offline push, including tokens and feature enabling/disabling.

### Initialization APIs
| API | Description |
| --- | --- |
| [getInstance](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#getinstance) | Obtains the instance of [TIMManager](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#timmanager). |
| [init](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#init) | Initializes the SDK and specifies the global configurations. |
| [unInit](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#uninit) | Deinitializes the SDK. |
| [getSdkConfig](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#getsdkconfig) | Obtains global configurations. |
| [setUserConfig](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#setuserconfig) | Specifies user configurations. |
| [getUserConfig](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#getuserconfig) | Obtains user configurations. |
| [addMessageListener](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#addmessagelistener) | Adds a message receiving listener. |
| [removeMessageListener](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#removemessagelistener) | Removes a message receiving listener. |
| [isInited](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#isinited) | Checks whether the SDK is initialized. |


### Login APIs
| API | Description |
| --- | --- |
| [login](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#login) | Logs in. |
| [autoLogin](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#autologin) | Enables auto-login. |
| [logout](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#logout) | Logs out. |
| [getLoginUser](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#getloginuser) | Obtains the login user. |


### Conversation management APIs
| API | Description |
| --- | --- |
| [getConversationList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#getconversationlist) | Obtains the list of conversations. |
| [getConversation](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#getconversation) | Obtains a conversation. |
| [deleteConversation](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#deleteconversation) | Deletes a conversation. |
| [deleteConversationAndLocalMsgs](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#deleteconversationandlocalmsgs) | Deletes a conversation and its messages. |


### APIs for configuring offline push
| API | Description |
| --- | --- |
| [setOfflinePushToken](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#setofflinepushtoken) | Configures the client token and the certificate business ID. |
| [setOfflinePushSettings](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#setofflinepushsettings) | Initializes the offline push configurations. Use this API on condition that you have logged in. |
| [getOfflinePushSettings](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#getofflinepushsettings) | Obtains the offline push configurations. Use this API on condition that you have logged in. |
| [setOfflinePushListener](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#setofflinepushlistener) | Configures the message notification listener which works while the app is running on the backend. (This API is deprecated.) |
| [doBackground](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#dobackground) | Reports that the app is running in the backend. |
| [doForeground](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#doforeground) | Reports that the app is running in the frontend. |


### APIs for querying local conversations and messages without login
| API | Description |
| --- | --- |
| [initStorage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#initstorage) | Loads the local storage without login. |


### Debugging APIs
| API | Description |
| --- | --- |
| [getVersion](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#getversion) | Obtains the version number. |
| [addMessageUpdateListener](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#addmessageupdatelistener) | Adds a message update listener to get message updates. |
| [removeMessageUpdateListener](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#removemessageupdatelistener) | Deletes a message update listener. |
| [getNetworkStatus](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#getnetworkstatus) | Obtains the network connection status. |
| [getServerTimeDiff](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#getservertimediff) | Obtains the time difference between the server and local device, expressed in seconds. `Time difference = svrTime – localTime`. |


## TIMConversation

Each time you start a conversation, you open a conversation window. A conversation can be a C2C chat or a group chat.
All API functions provided by [TIMConversation](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#timconversation) are related to message operations, including sending messages, obtaining message history, setting read receipt, recalling messages, and deleting messages. 

### APIs for sending messages
| API | Description |
| --- | --- |
| [sendMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#sendmessage) | Sends a message. |
| [sendOnlineMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#sendonlinemessage) | Sends an online message. (Incognito)  |


### APIs for obtaining messages
| API | Description |
| --- | --- |
| [getMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#getmessage) | Pulls message history from the cloud. |
| [getLocalMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#getlocalmessage) | Obtains message history from the local database. |
| [getLastMsg](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#getlastmsg) | Obtains the last message of the current conversion. |


### APIs for marking message as read
| API | Description |
| --- | --- |
| [setReadMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#setreadmessage) | Marks a message as read. |
| [getUnreadMessageNum](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#getunreadmessagenum) | Obtains the number of unread messages. |


### APIs for recalling and deleting messages
| API | Description |
| --- | --- |
| [revokeMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#revokemessage) | Recalls a message that has been sent. |
| [deleteLocalMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#deletelocalmessage) | Deletes local message history of the current conversation. |


### APIs for obtaining conversation information
| API | Description |
| --- | --- |
| [getType](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#gettype) | Obtains the conversation type. |
| [getPeer](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#getpeer) | Obtains the conversation ID. |
| [getGroupName](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#getgroupname) | Obtains the group name. |


### Drafts APIs
| API | Description |
| --- | --- |
| [setDraft](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#setdraft) | Adds an unfinished message as a draft. |
| [getDraft](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#getdraft) | Obtains a draft. |
| [hasDraft](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#hasdraft) | Checks whether the current conversation has a draft. |


### APIs for importing messages to a conversation
| API | Description |
| --- | --- |
| [saveMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#savemessage) | Adds a message to the list of local messages without sending it. |
| [importMsg](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#importmsg) | Imports a message to the local database. |
| [findMessages](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#findmessages) | Searches for a message using the given message locator. |


## TIMGroupManager

Group management module is used to create groups, delete groups, invite/delete group members, modify group/member profiles.

### API for obtaining a group instance
| API | Description |
| --- | --- |
| [getInstance](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#getinstance) | Obtains the instance of TIMGroupManager. |


### APIs for creating, disbanding, joining, and quitting groups
| API | Description |
| --- | --- |
| [createGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#creategroup) | Creates a group. |
| [deleteGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#deletegroup) | Disbands a group. |
| [applyJoinGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#applyjoingroup) | Applies for joining a group. |
| [quitGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#quitgroup) | Quits a group. |


### APIs for inviting and deleting group members
| API | Description |
| --- | --- |
| [inviteGroupMember](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#invitegroupmember) | Invites a friend to a group. |
| [deleteGroupMember](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#deletegroupmember) | Deletes a group member. |


### APIs for obtaining group information
| API | Description |
| --- | --- |
| [getGroupList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#getgrouplist) | Obtains the group lists. |
| [getGroupInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#getgroupinfo) | Obtains group information from the server. |
| [queryGroupInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#querygroupinfo) | Obtains group information from local storage. |
| [getGroupMembers](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#getgroupmembers) | Obtains the list of group members. |
| [getSelfInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#getselfinfo) | Obtains your profile in the group. |
| [getGroupMembersInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#getgroupmembersinfo) | Obtains the profiles of specific members. |
| [getGroupMembersByFilter](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#getgroupmembersbyfilter) | Obtains a list of a specific type of group members (filtered by field, displayed in pagination mode). |


### APIs for modifying group information
| API | Description |
| --- | --- |
| [modifyGroupInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#modifygroupinfo) | Modifies the group information. |
| [modifyGroupOwner](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#modifygroupowner) | Transfers the group ownership. |


### APIs for modifying group member profiles
| API | Description |
| --- | --- |
| [modifyMemberInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#modifymemberinfo) | Modifies a group member's profile. |


### APIs for handling pending group requests
| API | Description |
| --- | --- |
| [getGroupPendencyList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#getgrouppendencylist) | Obtains the list of pending group requests. |
| [reportGroupPendency](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#reportgrouppendency) | Reports that the pending group requests have been read. |


## TIMFriendshipManager

TIMFriendshipManager is the module for managing profile relationship chains. You can use it to add friends, delete friends, obtain friend information, modify friend profiles, etc.

| API | Description |
| --- | --- |
| [getInstance](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#getinstance) | Obtains the instance of TIMFriendshipManager. |
| [init](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#init) | Initializes TIMFriendshipManager. |
| [getUsersProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#getusersprofile) | Obtains profiles of specific users. |
| [getSelfProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#getselfprofile) | Obtains your personal profile. |
| [querySelfProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#queryselfprofile) | Obtains your personal local profile. If there is no available data, null is returned. |
| [queryUserProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#queryuserprofile) | Obtains a local user profile. If there is no available data, null is returned. |
| [modifySelfProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#modifyselfprofile) | Modifies your personal profile. |
| [getFriendList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#getfriendlist) | Obtains the friends list. |
| [queryFriendList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#queryfriendlist) | Obtains the relationship chain lists in the cache. The cached data source is the return result of the previous call of [getFriendList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#getfriendlist). Make sure that getFriendList has been called. |
| [queryFriend](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#queryfriend) | Queries the relationship chain of a friend in the cache. The cached data source is the return result of the previous call of [getFriendList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#getfriendlist). Make sure that getFriendList has been called. |
| [addFriend](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#addfriend) | Adds friend. |
| [deleteFriends](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#deletefriends) | Deletes friend. |
| [modifyFriend](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#modifyfriend) | Modifies a friend profile. |
| [doResponse](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#doresponse) | Processes a friend request. |
| [createFriendGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#createfriendgroup) | Creates a friend group. |
| [getFriendGroups](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#getfriendgroups) | Obtains specific friend group. If groupNames is set to null, all friend groups will be returned. |
| [deleteFriendGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#deletefriendgroup) | Deletes a friend group. |
| [renameFriendGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#renamefriendgroup) | Renames a friend group. |
| [addFriendsToFriendGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#addfriendstofriendgroup) | Adds friends to a friend group. |
| [deleteFriendsFromFriendGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#deletefriendsfromfriendgroup) | Deletes specific friends from a friend group. |
| [getPendencyList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#getpendencylist) | Deletes the list of pending requests. |
| [deletePendency](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#deletependency) | Deletes a pending request. |
| [pendencyReport](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#pendencyreport) | Reports that the pending requests have been read. |
| [getBlackList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#getblacklist) | Obtains the blacklist. |
| [addBlackList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#addblacklist) | Adds a user to the blacklist. |
| [deleteBlackList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#deleteblacklist) |Deletes a specific user from the blacklist. |
| [checkFriends](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#checkfriends) | Checks the friendship with a specific user. |


## TIMMessage

[TIMMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#timmessage) consists of multiple message elements (TIMElem). The TIMElem can be text or an image, and each message can contain multiple texts or images. For more information, see [Receiving and Sending Messages](https://cloud.tencent.com/document/product/269/9232).

| API | Description |
| --- | --- |
| [addElement](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#addelement) | Adds a message element. |
| [getElement](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getelement) | Obtains the message element of the corresponding index. |
| [getElementCount](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getelementcount) | Obtains the number of message elements. |
| [status](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#status) | Queries message status. |
| [isSelf](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#isself) | Checks whether you are the message sender. |
| [getSender](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getsender) | Queries who is the message sender. |
| [getMsgId](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getmsgid) | Obtains the message ID. |
| [getMsgUniqueId](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getmsguniqueid) | Obtains the uniqueId of the message. |
| [timestamp](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#timestamp) | Obtains the message timestamp. |
| [isRead](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#isread) | Checks whether you have read the message. |
| [isPeerReaded](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#ispeerreaded) | Checks whether the message receiver has read the message This API is applicable to C2C conversations only. |
| [getMessageLocator](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getmessagelocator) | Obtains the message locator. |
| [checkEquals](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#checkequals) | Checks whether the message is the one specified by the locator. |
| [remove](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#remove) | Deletes a message. |
| [getConversation](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getconversation) | Obtains a conversation. |
| [getSenderProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getsenderprofile) | Obtains the sender profile. |
| [getSenderGroupMemberProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getsendergroupmemberprofile) | Obtains the sender profile in the group. |
| [setPriority](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#setpriority) | Configures message priority (for group message only).|
| [getPriority](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getpriority) | Obtains message priority (for group message only). |
| [setOfflinePushSettings](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#setofflinepushsettings) | Configures parameters related to offline push. |
| [getOfflinePushSettings](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getofflinepushsettings) | Obtains the offline push configurations of messages. |
| [setCustomInt](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#setcustomint) | Configures the custom integer. The default value is 0. This attribute is for local use only. |
| [getCustomInt](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getcustomint) | Obtains the custom integer. |
| [setCustomStr](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#setcustomstr) | Configures the custom content. The default value is the empty string `""`. This attribute is for local use only. |
| [getCustomStr](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getcustomstr) | Obtains the value of the custom content. |
| [copyFrom](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#copyfrom) | Copies message content to the current message, including `Elem`, `priority`, `online`, and `offlinePushInfo`. |
| [convertToImportedMsg](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#converttoimportedmsg) | Imports the message to local storage. |
| [setTimestamp](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#settimestamp) | Configures the message timestamp. |
| [setSender](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#setsender) | Configures the sender ID. |
| [getRecvFlag](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getrecvflag) | Obtains the notification type of the message. |
| [getRand](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getrand) | Obtains the random code of the message. |
| [getSeq](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getseq) | Obtains the sequence number of the message. |


