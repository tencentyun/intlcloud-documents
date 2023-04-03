## TIMManager

As a core module of the IM SDK, TIMManager works for initialization, login, conversation creation, and push management of the IM SDK.
- Initialization: the prerequisite for using the IM SDK. You need to call the init API first before calling other APIs.
- Login: you need to configure the SDKAppID, UserID, and UserSig before using IM.
- Conversation: each time you start a conversation, you open a conversation window. A conversation can be a C2C chat or a group chat.
- Push: you can configure and manage features related to offline push, including tokens and feature enabling/disabling.

### Initialization APIs
| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [sharedInstance](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#sharedinstance) | Obtains the instance of [TIMManager](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#timmanager). |
| [initSdk](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#initsdk) | Initializes the SDK and specifies the global configurations. |
| [unInit](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#uninit) | Uninitialize the SDK.                                        |
| [getGlobalConfig](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#getglobalconfig) | Obtains global configurations.                               |
| [setUserConfig](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#setuserconfig) | Specifies user configurations.                               |
| [getUserConfig](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#getuserconfig) | Obtains user configurations.                                 |
| [addMessageListener](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#addmessagelistener) | Adds a message receiving listener.                           |
| [removeMessageListener](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#removemessagelistener) | Deletes a message receiving listener.                        |


### Login APIs
| API                                                          | Description                       |
| ------------------------------------------------------------ | --------------------------------- |
| [login](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#login) | Logs in.                          |
| [autoLogin](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#autologin) | Enables auto-login.               |
| [logout](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#logout) | Logs out.                         |
| [getLoginUser](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#getloginuser) | Obtains the login user.           |
| [getLoginStatus](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#getloginstatus) | Obtains the current login status. |


### Conversation management APIs
| API                                                          | Description                              |
| ------------------------------------------------------------ | ---------------------------------------- |
| [getConversationList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#getconversationlist) | Obtains the list of conversations.       |
| [getConversation](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#getconversation) | Obtains a conversation.                  |
| [deleteConversation](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#deleteconversation) | Deletes a conversation.                  |
| [deleteConversationAndMessages](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#deleteconversationandmessages) | Deletes a conversation and its messages. |


### Configures APNs push
| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setToken](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#settoken) | Configures the client token and the certificate business ID. |
| [setAPNS](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#setapns) | Configures APNs.                                             |
| [getAPNSConfig](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#getapnsconfig) | Obtains the APNs configurations.                             |
| [doBackground](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#dobackground) | Reports that the app is running in the backend.              |
| [doForeground](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#doforeground) | Reports that the app is running in the frontend.             |


### APIs for querying local conversations and messages without login
| API                                                          | Description                            |
| ------------------------------------------------------------ | -------------------------------------- |
| [initStorage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#initstorage) | Loads the local storage without login. |


### Debugging APIs
| API                                                          | Description                      |
| ------------------------------------------------------------ | -------------------------------- |
| [GetVersion](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#getversion) | Obtains the version number.      |
| [log](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#log) | Prints the log.                  |
| [getLogPath](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#getlogpath) | Obtains the log file path.       |
| [getIsLogPrintEnabled](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#getislogprintenabled) | Obtains the log printing status. |
| [getLogLevel](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMManager.html#getloglevel) | Obtains the log level.           |


## TIMConversation

Each time you start a conversation, you open a conversation window. A conversation can be a C2C chat or a group chat.
All API functions provided by TIMConversation are about message operations, including sending messages, obtaining message history, setting read receipt, recalling messages, and deleting messages.

### APIs for sending messages
| API                                                          | Description                          |
| ------------------------------------------------------------ | ------------------------------------ |
| [sendMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMConversation.html#sendmessage) | Sends a message.                     |
| [sendOnlineMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMConversation.html#sendonlinemessage) | Sends an online message. (Incognito) |


### APIs for obtaining messages
| API                                                          | Description                                           |
| ------------------------------------------------------------ | ----------------------------------------------------- |
| [getMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMConversation.html#getmessage) | Pulls message history from the cloud.                 |
| [getLocalMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMConversation.html#getlocalmessage) | Obtains message history from the local database.      |
| [getLastMsg](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMConversation.html#getlastmsg) | Obtains the last message of the current conversation. |


### APIs for setting read receipt
| API                                                          | Description                            |
| ------------------------------------------------------------ | -------------------------------------- |
| [setReadMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMConversation.html#setreadmessage) | Marks a message as read.               |
| [getUnReadMessageNum](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMConversation.html#getunreadmessagenum) | Obtains the number of unread messages. |


### APIs for recalling and deleting messages
| API                                                          | Description                                                |
| ------------------------------------------------------------ | ---------------------------------------------------------- |
| [revokeMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMConversation.html#revokemessage) | Recalls a sent message.                                    |
| [deleteLocalMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMConversation.html#deletelocalmessage) | Deletes local message history of the current conversation. |


### APIs for obtaining conversation information
| API                                                          | Description                    |
| ------------------------------------------------------------ | ------------------------------ |
| [getType](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMConversation.html#gettype) | Obtains the conversation type. |
| [getReceiver](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMConversation.html#getreceiver) | Obtains the conversation ID.   |
| [getGroupName](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMConversation.html#getgroupname) | Obtains the group name.        |


### Drafts APIs
| API                                                          | Description                            |
| ------------------------------------------------------------ | -------------------------------------- |
| [setDraft](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMConversation.html#setdraft) | Adds an unfinished message as a draft. |
| [getDraft](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMConversation.html#getdraft) | Obtains a draft.                       |


### APIs for importing messages to a conversation
| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [saveMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMConversation.html#savemessage) | Adds a message to the list of local messages without sending it. |
| [importMessages](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMConversation.html#importmessages) | Imports a message to the local database.                     |


## TIMGroupManager

Group management module is used to create groups, delete groups, invite/delete group members, modify group/member profiles.

### API for obtaining a group instance
| API                                                          | Description                              |
| ------------------------------------------------------------ | ---------------------------------------- |
| [sharedInstance](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#sharedinstance) | Obtains the instance of TIMGroupManager. |


### APIs for creating, disbanding, joining, and quitting groups
| API                                                          | Description                                |
| ------------------------------------------------------------ | ------------------------------------------ |
| [createPrivateGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#createprivategroup) | Creates a private group.                   |
| [createPublicGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#createpublicgroup) | Creates a public group.                    |
| [createChatRoomGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#createchatroomgroup) | Creates a chat room.                       |
| [createAVChatRoomGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#createavchatroomgroup) | Creates an audio & video chat room.        |
| [createGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#creategroup) | Creates a group with specific type and ID. |
| [createGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#creategroup2) | Creates a custom group.                    |
| [deleteGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#deletegroup) | Disbands a group.                          |
| [joinGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#joingroup) | Applies for joining a group.               |
| [quitGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#quitgroup) | Quits a group.                             |


### APIs for inviting and deleting group members
| API                                                          | Description                       |
| ------------------------------------------------------------ | --------------------------------- |
| [inviteGroupMember](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#invitegroupmember) | Invites a friend to join a group. |
| [deleteGroupMemberWithReason](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#deletegroupmemberwithreason) | Deletes a group member.           |


### APIs for obtaining group information
| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getGroupList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#getgrouplist) | Obtains the group lists.                                     |
| [getGroupInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#getgroupinfo) | Obtains group information from the server.                   |
| [queryGroupInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#querygroupinfo) | Obtains group information from local storage.                |
| [getGroupMembers](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#getgroupmembers) | Obtains the list of group members.                           |
| [getGroupSelfInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#getgroupselfinfo) | Obtains your profile in the group.                           |
| [getGroupMembersInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#getgroupmembersinfo) | Obtains the profiles of specific members.                    |
| [getGroupMembers](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#getgroupmembers2) | Obtains a list of a specific type of group members (filtered by field, displayed in pagination mode). |
| [getReciveMessageOpt](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#getrecivemessageopt) | Obtains the options for receiving messages.                  |


### APIs for modifying group information
| API                                                          | Description                                  |
| ------------------------------------------------------------ | -------------------------------------------- |
| [modifyGroupName](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#modifygroupname) | Modifies the group name.                     |
| [modifyGroupIntroduction](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#modifygroupintroduction) | Modifies the group introduction.             |
| [modifyGroupNotification](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#modifygroupnotification) | Modifies the group announcement.             |
| [modifyGroupFaceUrl](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#modifygroupfaceurl) | Modifies the group profile photo.            |
| [modifyGroupAddOpt](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#modifygroupaddopt) | Modifies the options for joining the group.  |
| [modifyGroupSearchable](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#modifygroupsearchable) | Modifies the search attributes.              |
| [modifyReceiveMessageOpt](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#modifyreceivemessageopt) | Modifies the options for receiving messages. |
| [modifyGroupAllShutup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#modifygroupallshutup) | Modifies the global mute attributes.         |
| [modifyGroupCustomInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#modifygroupcustominfo) | Modifies the custom fields.                  |
| [modifyGroupOwner](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#modifygroupowner) | Transfers the group ownership.               |


### APIs for modifying group member profiles
| API                                                          | Description                                          |
| ------------------------------------------------------------ | ---------------------------------------------------- |
| [modifyGroupMemberInfoSetNameCard](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#modifygroupmemberinfosetnamecard) | Modifies the name card of a group member.            |
| [modifyGroupMemberInfoSetRole](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#modifygroupmemberinfosetrole) | Modifies the role of a group member.                 |
| [modifyGroupMemberVisible](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#modifygroupmembervisible) | Modifies the visibility attribute of a group member. |
| [modifyGroupMemberInfoSetSilence](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#modifygroupmemberinfosetsilence) | Mutes users.                                         |
| [modifyGroupMemberInfoSetCustomInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#modifygroupmemberinfosetcustominfo) | Modifies the custom fields of a group member.        |


### APIs for handling pending group requests
| API                                                          | Description                                             |
| ------------------------------------------------------------ | ------------------------------------------------------- |
| [getPendencyFromServer](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#getpendencyfromserver) | Obtains the list of pending group requests.             |
| [pendencyReport](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMGroupManager.html#pendencyreport) | Reports that the pending group requests have been read. |


## TIMFriendshipManager

TIMFriendshipManager is the module for managing profile relationship chains. You can use it to add friends, delete friends, obtain friend information, modify friend profiles, etc.

| API                                                          | Description                                                 |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| [sharedInstance](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#sharedinstance) | Obtains the instance of TIMFriendshipManager.               |
| [modifySelfProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#modifyselfprofile) | Configures your personal profile.                           |
| [getSelfProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#getselfprofile) | Obtains your personal profile.                              |
| [querySelfProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#queryselfprofile) | Queries your personal profile in the cache.                 |
| [getUsersProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#getusersprofile) | Obtains profiles of specific users.                         |
| [queryUserProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#queryuserprofile) | Queries the profile of a specific user in the cache.        |
| [getFriendList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#getfriendlist) | Obtains the friends list.                                   |
| [queryFriend](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#queryfriend) | Queries the relationship chain data of a user in the cache. |
| [queryFriendList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#queryfriendlist) | Obtains the relationship chain lists in the cache.          |
| [checkFriends](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#checkfriends) | Checks the friendships of a specific user.                  |
| [addFriend](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#addfriend) | Adds friend.                                                |
| [doResponse](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#doresponse) | Responds to a friend request.                               |
| [deleteFriends](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#deletefriends) | Deletes friend.                                             |
| [modifyFriend](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#modifyfriend) | Modifies friend attributes.                                 |
| [getPendencyList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#getpendencylist) | Deletes the list of pending requests.                       |
| [deletePendency](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#deletependency) | Deletes pending requests.                                   |
| [pendencyReport](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#pendencyreport) | Reports that the pending requests have been read.           |
| [getBlackList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#getblacklist) | Obtains the blacklist.                                      |
| [addBlackList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#addblacklist) | Adds a user to the blacklist.                               |
| [deleteBlackList](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#deleteblacklist) | Deletes a specific user from the blacklist.                 |
| [createFriendGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#createfriendgroup) | Creates a friend group.                                     |
| [getFriendGroups](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#getfriendgroups) | Obtains specified friend group information.                 |
| [deleteFriendGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#deletefriendgroup) | Deletes a friend group.                                     |
| [renameFriendGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#renamefriendgroup) | Renames a friend group.                                     |
| [addFriendsToFriendGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#addfriendstofriendgroup) | Adds a friend to a specific friend group.                   |
| [deleteFriendsFromFriendGroup](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMFriendshipManager.html#deletefriendsfromfriendgroup) | Deletes specific friends from a friend group.               |


## TIMMessage

[TIMMessage](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#timmessage) consists of multiple message elements [TIMElem](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#timelem). The TIMElem can be text or an image, and each message can contain multiple texts or images. 

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [addElem](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#addelem) | Adds Elem.                                                   |
| [getElem](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#getelem) | Obtains the element of the corresponding index.              |
| [elemCount](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#elemcount) | Obtains the number of elements.                              |
| [setBusinessCmd](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#setbusinesscmd) | Configures the business command words.                       |
| [status](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#status) | Queries message status.                                      |
| [isSelf](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#isself) | Confirms whether you are the sender.                         |
| [sender](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#sender) | Obtains the message sender.                                  |
| [msgId](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#msgid) | Obtains the message ID.                                      |
| [uniqueId](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#uniqueid) | Obtains the the message uniqueId.                            |
| [timestamp](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#timestamp) | Obtains the message timestamp.                               |
| [isReaded](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#isreaded) | Checks whether you have read the message.                    |
| [isPeerReaded](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#ispeerreaded) | Checks whether the message has been read (Work for C2C message only.) |
| [locator](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#locator) | Obtains the message locator.                                 |
| [respondsToLocator](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#respondstolocator) | Checks whether the message is the one specified by the locator. |
| [remove](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#remove) | Deletes a message.                                           |
| [getConversation](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#getconversation) | Obtains a conversation.                                      |
| [getSenderProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#getsenderprofile) | Obtains the sender profile.                                  |
| [getSenderGroupMemberProfile](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#getsendergroupmemberprofile) | Obtains the sender profile in the group.                     |
| [setPriority](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#setpriority) | Configures message priority (for group message only).        |
| [getPriority](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#getpriority) | Obtains message priority (for group message only).           |
| [setOfflinePushInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#setofflinepushinfo) | Configures parameters related to offline push.               |
| [getOfflinePushInfo](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#getofflinepushinfo) | Obtains the offline push configurations of messages.         |
| [setCustomInt](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#setcustomint) | Configures the custom integer. The default value is 0.       |
| [customInt](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#customint) | Obtains the custom integer.                                  |
| [setCustomData](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#setcustomdata) | Configures the custom data. The default data is an empty string (`""`). |
| [customData](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#customdata) | Obtains the custom data.                                     |
| [copyFrom](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#copyfrom) | Copies the attributes of a message, including `Elem`, `priority`, `online`, and `offlinePushInfo`. |
| [convertToImportedMsg](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#converttoimportedmsg) | Imports the message to local storage.                        |
| [setTime](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#settime) | Configures the message timestamp.                            |
| [setSender](https://imsdk-1252463788.cos.ap-guangzhou.myqcloud.com/IM_DOC/iOS/ImSDK/Classes/TIMMessage.html#setsender) | Configures the message sender.                               |
