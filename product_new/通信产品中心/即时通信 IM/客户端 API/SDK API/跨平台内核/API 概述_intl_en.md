Here, APIs refer to the cross-platform C APIs of IM.

**Download URLs for different platforms:**
- [IM SDK](https://github.com/tencentyun/TIMSDK/tree/master/cross-platform/Windows) for Windows, quickstart guide for [integrating the IM SDK](https://intl.cloud.tencent.com/document/product/1047/34310) in Windows, and [Quick Demo Operation](https://intl.cloud.tencent.com/document/product/1047/34553). The 32-bit and 64-bit Windows systems are supported.
- [IM SDK](https://github.com/tencentyun/TIMSDK/tree/master/cross-platform/iOS) for iOS.
- [IM SDK](https://github.com/tencentyun/TIMSDK/tree/master/cross-platform/Mac) for Mac.
- [IM SDK](https://github.com/tencentyun/TIMSDK/tree/master/cross-platform/Android) for Android.

Callbacks are classified into two types. One is async callbacks that call an API, and the other is notifications pushed by the backend. A callback is triggered by the internal logic thread of the IM SDK, which may be different from the thread that calls the API.
In Windows, if a UI message loop has been created before the API [TIMInit](https://intl.cloud.tencent.com/document/product/1047/34388#timinit) is called to initialize the IM SDK and the thread that calls the API [TIMInit](https://intl.cloud.tencent.com/document/product/1047/34388#timinit) is a main UI thread, the IM SDK throws callbacks to the main UI thread for calling.

> If the parameter string of an API contains Chinese characters, it must be encoded in UTF-8.



### Event callback APIs

| API | Description |
|-----|-----|
| [TIMAddRecvNewMsgCallback](https://intl.cloud.tencent.com/document/product/1047/34389#timaddrecvnewmsgcallback) | Adds the callback for receiving a new message. |
| [TIMRemoveRecvNewMsgCallback](https://intl.cloud.tencent.com/document/product/1047/34389#timremoverecvnewmsgcallback) | Sets the callback for deleting a newly received message. |
| [TIMSetMsgReadedReceiptCallback](https://intl.cloud.tencent.com/document/product/1047/34389#timsetmsgreadedreceiptcallback) | Sets the callback for setting the message read receipt. |
| [TIMSetMsgRevokeCallback](https://intl.cloud.tencent.com/document/product/1047/34389#timsetmsgrevokecallback) | Sets the callback for recalling a received message. |
| [TIMSetMsgElemUploadProgressCallback](https://intl.cloud.tencent.com/document/product/1047/34389#timsetmsgelemuploadprogresscallback) | Sets the callback for checking the progress of uploading files pertaining to message elements. |
| [TIMSetGroupTipsEventCallback](https://intl.cloud.tencent.com/document/product/1047/34389#timsetgrouptipseventcallback) | Sets the callback for delivering a group system message. |
| [TIMSetConvEventCallback](https://intl.cloud.tencent.com/document/product/1047/34389#timsetconveventcallback) | Sets the callback for triggering a conversation event. |
| [TIMSetNetworkStatusListenerCallback](https://intl.cloud.tencent.com/document/product/1047/34389#timsetnetworkstatuslistenercallback) | Sets the callback for monitoring the network connection status. |
| [TIMSetKickedOfflineCallback](https://intl.cloud.tencent.com/document/product/1047/34389#timsetkickedofflinecallback) | Sets the callback for receiving a forcible logout notification. |
| [TIMSetUserSigExpiredCallback](https://intl.cloud.tencent.com/document/product/1047/34389#timsetusersigexpiredcallback) | Sets the callback for ticket expiration. |
| [TIMSetOnAddFriendCallback](https://intl.cloud.tencent.com/document/product/1047/34389#timsetonaddfriendcallback) | Sets the callback for adding a friend. |
| [TIMSetOnDeleteFriendCallback](https://intl.cloud.tencent.com/document/product/1047/34389#timsetondeletefriendcallback) | Sets the callback for deleting a friend. |
| [TIMSetUpdateFriendProfileCallback](https://intl.cloud.tencent.com/document/product/1047/34389#timsetupdatefriendprofilecallback) | Sets the callback for updating a friend’s profile. |
| [TIMSetFriendAddRequestCallback](https://intl.cloud.tencent.com/document/product/1047/34389#timsetfriendaddrequestcallback) | Sets the callback for friend requests. |
| [TIMSetLogCallback](https://intl.cloud.tencent.com/document/product/1047/34389#timsetlogcallback) | Sets the callback for logs. |
| [TIMSetMsgUpdateCallback](https://intl.cloud.tencent.com/document/product/1047/34389#timsetmsgupdatecallback) | Sets the callback for the message update notification that is returned after a message is modified in the cloud. |


### Initialization APIs of the IM SDK

| API | Description |
|-----|-----|
| [TIMInit](https://intl.cloud.tencent.com/document/product/1047/34388#timinit) | Initializes the IM SDK. |
| [TIMUninit](https://intl.cloud.tencent.com/document/product/1047/34388#timuninit) | Uninstalls the IM SDK. |
| [TIMGetSDKVersion](https://intl.cloud.tencent.com/document/product/1047/34388#timgetsdkversion) | Obtains the IM SDK version number. |
| [TIMSetConfig](https://intl.cloud.tencent.com/document/product/1047/34388#timsetconfig) | Sets extra user configurations. |


### Login and logout APIs

| API | Description |
|-----|-----|
| [TIMLogin](https://intl.cloud.tencent.com/document/product/1047/34390#timlogin) | Logs in to the IM backend server. |
| [TIMLogout](https://intl.cloud.tencent.com/document/product/1047/34390#timlogout) | Logs out from the IM backend server. |


### Conversation APIs

| API | Description |
|-----|-----|
| [TIMConvCreate](https://intl.cloud.tencent.com/document/product/1047/34557#timconvcreate) | Creates a conversation. |
| [TIMConvDelete](https://intl.cloud.tencent.com/document/product/1047/34557#timconvdelete) | Deletes a conversation. |
| [TIMConvGetConvList](https://intl.cloud.tencent.com/document/product/1047/34557#timconvgetconvlist) | Obtains the locally cached conversation list. |
| [TIMConvSetDraft](https://intl.cloud.tencent.com/document/product/1047/34557#timconvsetdraft) | Sets the draft for a specified conversation. |
| [TIMConvCancelDraft](https://intl.cloud.tencent.com/document/product/1047/34557#timconvcanceldraft) | Deletes the draft for a specified conversation. |


### Message APIs

| API | Description |
|-----|-----|
| [TIMMsgSendNewMsg](https://intl.cloud.tencent.com/document/product/1047/34391#timmsgsendnewmsg) | Sends a new message. |
| [TIMMsgReportReaded](https://intl.cloud.tencent.com/document/product/1047/34391#timmsgreportreaded) | Reports the read state of messages. |
| [TIMMsgRevoke](https://intl.cloud.tencent.com/document/product/1047/34391#timmsgrevoke) | Recalls a message. |
| [TIMMsgFindByMsgLocatorList](https://intl.cloud.tencent.com/document/product/1047/34391#timmsgfindbymsglocatorlist) | Accurately locates a message of the specified conversation by using the message locator. |
| [TIMMsgImportMsgList](https://intl.cloud.tencent.com/document/product/1047/34391#timmsgimportmsglist) | Imports the message list to a specified conversation. |
| [TIMMsgSaveMsg](https://intl.cloud.tencent.com/document/product/1047/34391#timmsgsavemsg) | Saves custom messages. |
| [TIMMsgGetMsgList](https://intl.cloud.tencent.com/document/product/1047/34391#timmsggetmsglist) | Obtains the message list of a specified conversation. |
| [TIMMsgDelete](https://intl.cloud.tencent.com/document/product/1047/34391#timmsgdelete) | Deletes the messages of a specified conversation. |
| [TIMMsgDownloadElemToPath](https://intl.cloud.tencent.com/document/product/1047/34391#timmsgdownloadelemtopath) | Downloads the internal elements (including image, video, audio, and file elements) of a message to a specified path. |
| [TIMMsgBatchSend](https://intl.cloud.tencent.com/document/product/1047/34391#timmsgbatchsend) | Sends messages in batches. |


### Group APIs

| API | Description |
|-----|-----|
| [TIMGroupCreate](https://intl.cloud.tencent.com/document/product/1047/34393#timgroupcreate) | Creates a group. |
| [TIMGroupDelete](https://intl.cloud.tencent.com/document/product/1047/34393#timgroupdelete) | Deletes (dismisses) a group. |
| [TIMGroupJoin](https://intl.cloud.tencent.com/document/product/1047/34393#timgroupjoin) | Submits an application for joining a group. |
| [TIMGroupQuit](https://intl.cloud.tencent.com/document/product/1047/34393#timgroupquit) | Quits a group. |
| [TIMGroupInviteMember](https://intl.cloud.tencent.com/document/product/1047/34393#timgroupinvitemember) | Invites a user to a group. |
| [TIMGroupDeleteMember](https://intl.cloud.tencent.com/document/product/1047/34393#timgroupdeletemember) | Deletes a member from a group. |
| [TIMGroupGetJoinedGroupList](https://intl.cloud.tencent.com/document/product/1047/34393#timgroupgetjoinedgrouplist) | Obtains the list of groups that a user has joined. |
| [TIMGroupGetGroupInfoList](https://intl.cloud.tencent.com/document/product/1047/34393#timgroupgetgroupinfolist) | Obtains the group information list. |
| [TIMGroupModifyGroupInfo](https://intl.cloud.tencent.com/document/product/1047/34393#timgroupmodifygroupinfo) | Modifies group information. |
| [TIMGroupGetMemberInfoList](https://intl.cloud.tencent.com/document/product/1047/34393#timgroupgetmemberinfolist) | Obtains the group member information list. |
| [TIMGroupModifyMemberInfo](https://intl.cloud.tencent.com/document/product/1047/34393#timgroupmodifymemberinfo) | Modifies group member information. |
| [TIMGroupGetPendencyList](https://intl.cloud.tencent.com/document/product/1047/34393#timgroupgetpendencylist) | Obtains the pending request list of a group. <br/>A pending request refers to an operation that has not yet been processed. For example, if an invitation to a user to join a group or a request from a user to join a group has not been accepted or rejected, the invitation is a pending request for the group. |
| [TIMGroupReportPendencyReaded](https://intl.cloud.tencent.com/document/product/1047/34393#timgroupreportpendencyreaded) | Reports the read state of pending requests of a group. |
| [TIMGroupHandlePendency](https://intl.cloud.tencent.com/document/product/1047/34393#timgrouphandlependency) | Handles the pending requests of a group. |


### User profile APIs

| API | Description |
|-----|-----|
| [TIMProfileGetUserProfileList](https://intl.cloud.tencent.com/document/product/1047/34558#timprofilegetuserprofilelist) | Obtains a specified user profile list. |
| [TIMProfileModifySelfUserProfile](https://intl.cloud.tencent.com/document/product/1047/34558#timprofilemodifyselfuserprofile) | Modifies your own profile. |


### Relationship chain APIs

| API | Description |
|-----|-----|
| [TIMFriendshipGetFriendProfileList](https://intl.cloud.tencent.com/document/product/1047/34559#timfriendshipgetfriendprofilelist) | Obtains the friend list. |
| [TIMFriendshipAddFriend](https://intl.cloud.tencent.com/document/product/1047/34559#timfriendshipaddfriend) | Adds a friend. |
| [TIMFriendshipHandleFriendAddRequest](https://intl.cloud.tencent.com/document/product/1047/34559#timfriendshiphandlefriendaddrequest) | Handles friend requests. |
| [TIMFriendshipModifyFriendProfile](https://intl.cloud.tencent.com/document/product/1047/34559#timfriendshipmodifyfriendprofile) | Updates a friend’s profile (such as remarks). |
| [TIMFriendshipDeleteFriend](https://intl.cloud.tencent.com/document/product/1047/34559#timfriendshipdeletefriend) | Deletes a friend. |
| [TIMFriendshipCheckFriendType](https://intl.cloud.tencent.com/document/product/1047/34559#timfriendshipcheckfriendtype) | Checks the friend type (one-way or two-way). |
| [TIMFriendshipCreateFriendGroup](https://intl.cloud.tencent.com/document/product/1047/34559#timfriendshipcreatefriendgroup) | Creates a friend group. |
| [TIMFriendshipGetFriendGroupList](https://intl.cloud.tencent.com/document/product/1047/34559#timfriendshipgetfriendgrouplist) | Obtains the group information of a specified friend group. |
| [TIMFriendshipModifyFriendGroup](https://intl.cloud.tencent.com/document/product/1047/34559#timfriendshipmodifyfriendgroup) | Modifies a friend group. |
| [TIMFriendshipDeleteFriendGroup](https://intl.cloud.tencent.com/document/product/1047/34559#timfriendshipdeletefriendgroup) | Deletes a friend group. |
| [TIMFriendshipAddToBlackList](https://intl.cloud.tencent.com/document/product/1047/34559#timfriendshipaddtoblacklist) | Adds a specified user to the blacklist. |
| [TIMFriendshipGetBlackList](https://intl.cloud.tencent.com/document/product/1047/34559#timfriendshipgetblacklist) | Obtains the blacklist. |
| [TIMFriendshipDeleteFromBlackList](https://intl.cloud.tencent.com/document/product/1047/34559#timfriendshipdeletefromblacklist) | Deletes a specified user from the blacklist. |
| [TIMFriendshipGetPendencyList](https://intl.cloud.tencent.com/document/product/1047/34559#timfriendshipgetpendencylist) | Obtains the information list of pending friend requests. |
| [TIMFriendshipDeletePendency](https://intl.cloud.tencent.com/document/product/1047/34559#timfriendshipdeletependency) | Deletes the specified pending friend request information. |
| [TIMFriendshipReportPendencyReaded](https://intl.cloud.tencent.com/document/product/1047/34559#timfriendshipreportpendencyreaded) | Reports the read state of the pending friend request information. |


