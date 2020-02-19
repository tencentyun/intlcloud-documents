## 在线状态

| 回调类型         | 回调命令字                                    |
| ---------------- | --------------------------------------------- |
| 状态变更回调 | [State.StateChange](https://intl.cloud.tencent.com/document/product/1047/34357) |

## 资料关系链

| 回调类型           | 回调命令字                                                   |
| ------------------ | ------------------------------------------------------------ |
| 添加好友之后回调   | [Sns.CallbackFriendAdd](https://intl.cloud.tencent.com/document/product/1047/34359)        |
| 删除好友之后回调   | [Sns.CallbackFriendDelete](https://intl.cloud.tencent.com/document/product/1047/34360)  |
| 添加黑名单之后回调 | [Sns.CallbackBlackListAdd](https://intl.cloud.tencent.com/document/product/1047/34361)  |
| 删除黑名单之后回调 | [Sns.CallbackBlackListDelete](https://intl.cloud.tencent.com/document/product/1047/34362) |

## 单聊消息

| 回调类型           | 回调命令字                                                   |
| ------------------ | ------------------------------------------------------------ |
| 发单聊消息之前回调 | [C2C.CallbackBeforeSendMsg](https://intl.cloud.tencent.com/document/product/1047/34364) |
| 发单聊消息之后回调 | [C2C.CallbackAfterSendMsg](https://intl.cloud.tencent.com/document/product/1047/34365)  |

## 群组系统

| 回调类型           | 回调命令字                                                   |
| ------------------ | ------------------------------------------------------------ |
|创建群组之前回调|[Group.CallbackBeforeCreateGroup](https://intl.cloud.tencent.com/document/product/1047/34368)|
|创建群组之后回调|[Group.CallbackAfterCreateGroup](https://intl.cloud.tencent.com/document/product/1047/34369)|
|申请入群之前回调|[Group.CallbackBeforeApplyJoinGroup](https://intl.cloud.tencent.com/document/product/1047/34370)|
|拉人入群之前回调|[Group.CallbackBeforeInviteJoinGroup](https://intl.cloud.tencent.com/document/product/1047/34371)|
|新成员入群之后回调|[Group.CallbackAfterNewMemberJoin](https://intl.cloud.tencent.com/document/product/1047/34372)|
|群成员离开之后回调|[Group.CallbackAfterMemberExit](https://intl.cloud.tencent.com/document/product/1047/34373)|
|群内发言之前回调|[Group.CallbackBeforeSendMsg](https://intl.cloud.tencent.com/document/product/1047/34374)|
|群内发言之后回调|[Group.CallbackAfterSendMsg](https://intl.cloud.tencent.com/document/product/1047/34375)|
|群组满员之后回调|[Group.CallbackAfterGroupFull](https://intl.cloud.tencent.com/document/product/1047/34376)|
|群组解散之后回调|[Group.CallbackAfterGroupDestroyed](https://intl.cloud.tencent.com/document/product/1047/34377)|
|群组资料修改之后回调|[Group.CallbackAfterGroupInfoChanged](https://intl.cloud.tencent.com/document/product/1047/34378)|
