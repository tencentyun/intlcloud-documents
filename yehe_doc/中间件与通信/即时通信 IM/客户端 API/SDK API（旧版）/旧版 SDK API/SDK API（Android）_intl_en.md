## TIMManager

As a core component of the IM SDK, TIMManager works for the initialization, login, conversation creation, and push management of the IM SDK.
- Initialization: is the prerequisite for using the IM SDK. You need to call the init API before calling other APIs.
- Login: you need to configure SDKAppID, UserID, and UserSig before using IM.
- Conversation: each time you start a conversation, you open a conversation window. A conversation can be a C2C chat or a group chat.
- Push: you can configure and manage features related to offline push, including tokens and feature enabling and disabling.

### Initialization APIs
| API | Description |
| --- | --- |
| [getInstance](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#getinstance) | Obtains the instance of [TIMManager](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#timmanager). |
| [init](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#init) | Initializes the SDK and specifies the global configuration. |
| [unInit](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#uninit) | Uninitializes the SDK. |
| [getSdkConfig](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#getsdkconfig) | Obtains the global configuration. |
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
| [getLoginUser](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#getloginuser) | Obtains the logged-in user. |
| [getLoginStatus](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#getLoginStatus) | Obtains the current login status. |


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
| [setOfflinePushToken](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#setofflinepushtoken) | Configures the client token and the certificate busiID. |
| [setOfflinePushSettings](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#setofflinepushsettings) | Initializes the offline push configuration. Use this API after you have logged in to ensure that the configuration takes effect. |
| [getOfflinePushSettings](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#getofflinepushsettings) | Obtains the offline push configuration. Use this API after you have logged in. |
| [setOfflinePushListener](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#setofflinepushlistener) | Configures the message notification listener that works when the app is running at the backend. (This API has been deprecated.) |
| [doBackground](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#dobackground) | Reports that the app is running at the backend. |
| [doForeground](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#doforeground) | Reports that the app is running at the frontend. |


### APIs for querying local conversations and messages without login
| API | Description |
| --- | --- |
| [initStorage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#initstorage) | Loads the local storage without login. |


### Debugging APIs
| API | Description |
| --- | --- |
| [getVersion](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#getversion) | Obtains the version number. |
| [addMessageUpdateListener](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#addmessageupdatelistener) | Adds a message update listener to obtain message updates. |
| [removeMessageUpdateListener](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#removemessageupdatelistener) | Deletes a message update listener. |
| [getNetworkStatus](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#getnetworkstatus) | Obtains the network connection status. |
| [getServerTimeDiff](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMManager.html#getservertimediff) | Obtains the time difference in the unit of seconds between the server and local device. `Time difference = svrTime – localTime`. |


## TIMConversation

Each time you start a conversation, you open a conversation window. A conversation can be a C2C chat or a group chat.
All API functions provided by [TIMConversation](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#timconversation) are related to message operations, including sending messages, obtaining the message history, setting read receipts, recalling messages, and deleting messages.

### APIs for sending messages
| API | Description |
| --- | --- |
| [sendMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#sendmessage) | Sends a message. |
| [sendOnlineMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#sendonlinemessage) | Sends an online message. (Incognito) |


### APIs for obtaining messages
| API | Description |
| --- | --- |
| [getMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#getmessage) | Pulls the message history from the cloud. |
| [getLocalMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#getlocalmessage) | Obtains the message history from the local database. |
| [getLastMsg](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#getlastmsg) | Obtains the last message of the current conversion. |


### APIs for marking messages as read
| API | Description |
| --- | --- |
| [setReadMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#setreadmessage) | Marks a message as read. |
| [getUnreadMessageNum](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#getunreadmessagenum) | Obtains the number of unread messages. |


### APIs for recalling and deleting messages
| API | Description |
| --- | --- |
| [revokeMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#revokemessage) | Recalls a sent message. |
| [deleteLocalMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#deletelocalmessage) | Deletes the local message history of the current conversation. |


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
| [findMessages](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMConversation.html#findmessages) | Searches for a message by using the given message locator. |


## TIMGroupManager

The group management component is used to create groups, delete groups, invite or delete group members, and modify group or member profiles.

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
| [getGroupList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#getgrouplist) | Obtains the list of groups. |
| [getGroupInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#getgroupinfo) | Obtains group information from the server. |
| [queryGroupInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#querygroupinfo) | Obtains group information from the local storage. |
| [getGroupMembers](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#getgroupmembers) | Obtains the list of group members. |
| [getSelfInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#getselfinfo) | Obtains your profile in the group. |
| [getGroupMembersInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#getgroupmembersinfo) | Obtains the profiles of specific members. |
| [getGroupMembersByFilter](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#getgroupmembersbyfilter) | Obtains a list of group members of a specific type (which can be filtered by field and displayed in pagination mode). |


### APIs for modifying group information
| API | Description |
| --- | --- |
| [modifyGroupInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#modifygroupinfo) | Modifies group information. |
| [modifyGroupOwner](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#modifygroupowner) | Transfers the group ownership. |


### API for modifying group member profiles
| API | Description |
| --- | --- |
| [modifyMemberInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#modifymemberinfo) | Modifies a group member's profile. |


### APIs for handling pending group requests
| API | Description |
| --- | --- |
| [getGroupPendencyList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#getgrouppendencylist) | Obtains the list of pending group requests. |
| [reportGroupPendency](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMGroupManager.html#reportgrouppendency) | Reports that pending group requests have been read. |


## TIMFriendshipManager

TIMFriendshipManager is the component for managing profile relationship chains. You can use it to add friends, delete friends, obtain friend information, and modify friend profiles.

| API | Description |
| --- | --- |
| [getInstance](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#getinstance) | Obtains the instance of TIMFriendshipManager. |
| [init](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#init) | Initializes TIMFriendshipManager. |
| [getUsersProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#getusersprofile) | Obtains profiles of specific users. |
| [getSelfProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#getselfprofile) | Obtains your personal profile. |
| [querySelfProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#queryselfprofile) | Obtains your personal local profile. If there is no available data, null is returned. |
| [queryUserProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#queryuserprofile) | Obtains a local user profile. If there is no available data, null is returned. |
| [modifySelfProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#modifyselfprofile) | Modifies your personal profile. |
| [getFriendList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#getfriendlist) | Obtains the list of friends. |
| [queryFriendList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#queryfriendlist) | Obtains the relationship chain list in the cache. The cached data source is the return result of the previous call of [getFriendList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#getfriendlist). Ensure that getFriendList has been called. |
| [queryFriend](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#queryfriend) | Queries the relationship chain of a friend in the cache. The cached data source is the return result of the previous call of [getFriendList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#getfriendlist). Ensure that getFriendList has been called. |
| [addFriend](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#addfriend) | Adds a friend. |
| [deleteFriends](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#deletefriends) | Deletes a friend. |
| [modifyFriend](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#modifyfriend) | Modifies a friend profile. |
| [doResponse](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#doresponse) | Processes a friend request. |
| [createFriendGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#createfriendgroup) | Creates a friend group. |
| [getFriendGroups](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#getfriendgroups) | Obtains specific friend groups. If groupNames is set to null, all friend groups will be returned. |
| [deleteFriendGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#deletefriendgroup) | Deletes a friend group. |
| [renameFriendGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#renamefriendgroup) | Renames a friend group. |
| [addFriendsToFriendGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#addfriendstofriendgroup) | Adds friends to a friend group. |
| [deleteFriendsFromFriendGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#deletefriendsfromfriendgroup) | Deletes specific friends from a friend group. |
| [getPendencyList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#getpendencylist) | Obtains the list of pending requests. |
| [deletePendency](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#deletependency) | Deletes a pending request. |
| [pendencyReport](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#pendencyreport) | Reports that pending requests have been read. |
| [getBlackList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#getblacklist) | Obtains the blacklist. |
| [addBlackList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#addblacklist) | Adds a user to the blacklist. |
| [deleteBlackList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#deleteblacklist) | Deletes a specific user from the blacklist. |
| [checkFriends](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMFriendshipManager.html#checkfriends) | Checks the friendship with a specific user. |


## TIMMessage

[TIMMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#timmessage) consists of multiple message elements (TIMElem). The TIMElem can be text or an image, and each message can contain multiple texts or images. For more information, see [Receiving and Sending Messages](https://intl.cloud.tencent.com/document/product/1047/34320).

| API | Description |
| --- | --- |
| [addElement](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#addelement) | Adds a message element. |
| [getElement](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getelement) | Obtains the message element of the corresponding index. |
| [getElementCount](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getelementcount) | Obtains the number of message elements. |
| [status](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#status) | Queries the message status. |
| [isSelf](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#isself) | Checks whether you are the message sender. |
| [getSender](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getsender) | Queries the message sender. |
| [getSenderNickname](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getsender) | Queries the nickname of the message sender. |
| [getSenderFaceUrl](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getsender) | Queries the profile photo URL of the message sender. |
| [getMsgId](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getmsgid) | Obtains the message ID. |
| [getMsgUniqueId](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getmsguniqueid) | Obtains the uniqueId of the message. |
| [timestamp](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#timestamp) | Obtains the message timestamp. |
| [isRead](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#isread) | Checks whether you have read the message. |
| [isPeerReaded](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#ispeerreaded) | Checks whether the message receiver has read the message. This API is applicable to C2C conversations only. |
| [getMessageLocator](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getmessagelocator) | Obtains the message locator. |
| [checkEquals](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#checkequals) | Checks whether the message is the one specified by the locator. |
| [remove](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#remove) | Deletes a message. |
| [getConversation](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getconversation) | Obtains a conversation. |
| [getSenderProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getsenderprofile) | Obtains the sender profile. |
| [getSenderGroupMemberProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getsendergroupmemberprofile) | Obtains the sender profile in the group. |
| [setPriority](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#setpriority) | Configures message priority (for group messages only). |
| [getPriority](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getpriority) | Obtains message priority (for group messages only). |
| [setOfflinePushSettings](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#setofflinepushsettings) | Configures parameters related to offline push. |
| [getOfflinePushSettings](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getofflinepushsettings) | Obtains the offline push configuration of messages. |
| [setCustomInt](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#setcustomint) | Configures the custom integer. The default value is 0. This attribute is for local use only. |
| [getCustomInt](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getcustomint) | Obtains the custom integer. |
| [setCustomStr](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#setcustomstr) | Configures custom content. The default value is the empty string `""`. This attribute is for local use only. |
| [getCustomStr](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getcustomstr) | Obtains the value of the custom content. |
| [copyFrom](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#copyfrom) | Copies message content to the current message, including `Elem`, `priority`, `online`, and `offlinePushInfo`. |
| [convertToImportedMsg](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#converttoimportedmsg) | Imports the message to the local storage. |
| [setTimestamp](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#settimestamp) | Configures the message timestamp. |
| [setSender](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#setsender) | Configures the sender ID. |
| [getRecvFlag](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getrecvflag) | Obtains the notification type of the message. |
| [getRand](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getrand) | Obtains the random code of the message. |
| [getSeq](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/Android/ImSDK/com/tencent/imsdk/TIMMessage.html#getseq) | Obtains the sequence number of the message. |



