腾讯云通信 IM 的跨平台 C 接口（API）。

**各个平台的下载链接**

- Windows 平台 [IM SDK](https://github.com/tencentyun/TIMSDK/tree/master/cross-platform/Windows)，Windows 快速开始 [集成 IM SDK](https://intl.cloud.tencent.com/document/product/1027/31235) 和 [跑通 demo](https://intl.cloud.tencent.com/document/product/1027/31228)。暂不支持64位编译。
- iOS 平台 [IM SDK](https://github.com/tencentyun/TIMSDK/tree/master/cross-platform/iOS)。
- Mac 平台 [IM SDK](https://github.com/tencentyun/TIMSDK/tree/master/cross-platform/Mac)。
- Android 平台 [IM SDK](https://github.com/tencentyun/TIMSDK/tree/master/cross-platform/Android)。


**关于回调的说明**

- 回调分两种，一种是指调用接口的异步返回，另外一种指后台推送的通知。回调在 IM SDK 内部的逻辑线程触发，跟调用接口的线程可能不是同一线程。
- 在 Windows 平台，如果调用 [TIMInit](https://intl.cloud.tencent.com/document/product/1027/31276#timinit) 接口进行初始化 IM SDK 之前，已创建了 UI 的消息循环，且调用 [TIMInit](https://intl.cloud.tencent.com/document/product/1027/31276#timinit) 接口的线程为主 UI 线程，则 IM SDK 内部会将回调抛到主 UI 线程调用。



### 事件回调接口

| API | 描述 |
|-----|-----|
| [TIMAddRecvNewMsgCallback](https://intl.cloud.tencent.com/document/product/1027/31281#timaddrecvnewmsgcallback) | 增加接收新消息回调 |
| [TIMRemoveRecvNewMsgCallback](https://intl.cloud.tencent.com/document/product/1027/31281#timremoverecvnewmsgcallback) | 删除接收新消息回调 |
| [TIMSetMsgReadedReceiptCallback](https://intl.cloud.tencent.com/document/product/1027/31281#timsetmsgreadedreceiptcallback) | 设置消息已读回执回调 |
| [TIMSetMsgRevokeCallback](https://intl.cloud.tencent.com/document/product/1027/31281#timsetmsgrevokecallback) | 设置接收的消息被撤回回调 |
| [TIMSetMsgElemUploadProgressCallback](https://intl.cloud.tencent.com/document/product/1027/31281#timsetmsgelemuploadprogresscallback) | 设置消息内元素相关文件上传进度回调 |
| [TIMSetGroupTipsEventCallback](https://intl.cloud.tencent.com/document/product/1027/31281#timsetgrouptipseventcallback) | 设置群组系统消息回调 |
| [TIMSetConvEventCallback](https://intl.cloud.tencent.com/document/product/1027/31281#timsetconveventcallback) | 设置会话事件回调 |
| [TIMSetNetworkStatusListenerCallback](https://intl.cloud.tencent.com/document/product/1027/31281#timsetnetworkstatuslistenercallback) | 设置网络连接状态监听回调 |
| [TIMSetKickedOfflineCallback](https://intl.cloud.tencent.com/document/product/1027/31281#timsetkickedofflinecallback) | 设置被踢下线通知回调 |
| [TIMSetUserSigExpiredCallback](https://intl.cloud.tencent.com/document/product/1027/31281#timsetusersigexpiredcallback) | 设置票据过期回调 |
| [TIMSetLogCallback](https://intl.cloud.tencent.com/document/product/1027/31281#timsetlogcallback) | 设置日志回调 |
| [TIMSetMsgUpdateCallback](https://intl.cloud.tencent.com/document/product/1027/31281#timsetmsgupdatecallback) | 设置消息在云端被修改后回传回来的消息更新通知回调 |


### IM SDK 初始化相关接口

| API | 描述 |
|-----|-----|
| [TIMInit](https://intl.cloud.tencent.com/document/product/1027/31276#timinit) | IM SDK 初始化 |
| [TIMUninit](https://intl.cloud.tencent.com/document/product/1027/31276#timuninit) | IM SDK 卸载 |
| [TIMGetSDKVersion](https://intl.cloud.tencent.com/document/product/1027/31276#timgetsdkversion) | 获取 IM SDK 版本号 |
| [TIMSetConfig](https://intl.cloud.tencent.com/document/product/1027/31276#timsetconfig) | 设置额外的用户配置 |


### 登录登出相关接口

| API | 描述 |
|-----|-----|
| [TIMLogin](https://intl.cloud.tencent.com/document/product/1027/31277#timlogin) | 登录 |
| [TIMLogout](https://intl.cloud.tencent.com/document/product/1027/31277#timlogout) | 登出 |


### 会话相关接口

| API | 描述 |
|-----|-----|
| [TIMConvCreate](https://intl.cloud.tencent.com/document/product/1027/31278#timconvcreate) | 创建会话 |
| [TIMConvDelete](https://intl.cloud.tencent.com/document/product/1027/31278#timconvdelete) | 删除会话 |
| [TIMConvGetConvList](https://intl.cloud.tencent.com/document/product/1027/31278#timconvgetconvlist) | 获取本地缓存的会话列表 |
| [TIMConvSetDraft](https://intl.cloud.tencent.com/document/product/1027/31278#timconvsetdraft) | 设置指定会话的草稿 |
| [TIMConvCancelDraft](https://intl.cloud.tencent.com/document/product/1027/31278#timconvcanceldraft) | 删除指定会话的草稿 |


### 消息相关接口

| API | 描述 |
|-----|-----|
| [TIMMsgSendNewMsg](https://intl.cloud.tencent.com/document/product/1027/31279#timmsgsendnewmsg) | 发送新消息 |
| [TIMMsgReportReaded](https://intl.cloud.tencent.com/document/product/1027/31279#timmsgreportreaded) | 消息上报已读 |
| [TIMMsgRevoke](https://intl.cloud.tencent.com/document/product/1027/31279#timmsgrevoke) | 消息撤回 |
| [TIMMsgFindByMsgLocatorList](https://intl.cloud.tencent.com/document/product/1027/31279#timmsgfindbymsglocatorlist) | 根据消息定位精准查找指定会话的消息 |
| [TIMMsgImportMsgList](https://intl.cloud.tencent.com/document/product/1027/31279#timmsgimportmsglist) | 导入消息列表到指定会话 |
| [TIMMsgSaveMsg](https://intl.cloud.tencent.com/document/product/1027/31279#timmsgsavemsg) | 保存自定义消息 |
| [TIMMsgGetMsgList](https://intl.cloud.tencent.com/document/product/1027/31279#timmsggetmsglist) | 获取指定会话的消息列表 |
| [TIMMsgDelete](https://intl.cloud.tencent.com/document/product/1027/31279#timmsgdelete) | 删除指定会话的消息 |
| [TIMMsgDownloadElemToPath](https://intl.cloud.tencent.com/document/product/1027/31279#timmsgdownloadelemtopath) | 下载消息内元素到指定文件路径（图片、视频、音频、文件） |
| [TIMMsgBatchSend](https://intl.cloud.tencent.com/document/product/1027/31279#timmsgbatchsend) | 群发消息 |


### 群组相关接口

| API | 描述 |
|-----|-----|
| [TIMGroupCreate](https://intl.cloud.tencent.com/document/product/1027/31280#timgroupcreate) | 创建群组 |
| [TIMGroupDelete](https://intl.cloud.tencent.com/document/product/1027/31280#timgroupdelete) | 删除（解散）群组 |
| [TIMGroupJoin](https://intl.cloud.tencent.com/document/product/1027/31280#timgroupjoin) | 申请加入群组 |
| [TIMGroupQuit](https://intl.cloud.tencent.com/document/product/1027/31280#timgroupquit) | 退出群组 |
| [TIMGroupInviteMember](https://intl.cloud.tencent.com/document/product/1027/31280#timgroupinvitemember) | 邀请加入群组 |
| [TIMGroupDeleteMember](https://intl.cloud.tencent.com/document/product/1027/31280#timgroupdeletemember) | 删除群组成员 |
| [TIMGroupGetJoinedGroupList](https://intl.cloud.tencent.com/document/product/1027/31280#timgroupgetjoinedgrouplist) | 获取已加入群组列表 |
| [TIMGroupGetGroupInfoList](https://intl.cloud.tencent.com/document/product/1027/31280#timgroupgetgroupinfolist) | 获取群组信息列表 |
| [TIMGroupModifyGroupInfo](https://intl.cloud.tencent.com/document/product/1027/31280#timgroupmodifygroupinfo) | 修改群信息 |
| [TIMGroupGetMemberInfoList](https://intl.cloud.tencent.com/document/product/1027/31280#timgroupgetmemberinfolist) | 获取群成员信息列表 |
| [TIMGroupModifyMemberInfo](https://intl.cloud.tencent.com/document/product/1027/31280#timgroupmodifymemberinfo) | 修改群成员信息 |
| [TIMGroupGetPendencyList](https://intl.cloud.tencent.com/document/product/1027/31280#timgroupgetpendencylist) | 获取群未决信息列表。<br/>群未决信息是指还没有处理的操作，例如，邀请加群或者请求加群操作还没有被处理，称之为群未决信息 |
| [TIMGroupReportPendencyReaded](https://intl.cloud.tencent.com/document/product/1027/31280#timgroupreportpendencyreaded) | 上报群未决信息已读 |
| [TIMGroupHandlePendency](https://intl.cloud.tencent.com/document/product/1027/31280#timgrouphandlependency) | 处理群未决信息 |


