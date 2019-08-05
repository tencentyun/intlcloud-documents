## 在线状态

| 回调类型         | 回调命令字                                    |
| ---------------- | --------------------------------------------- |
| 状态变更回调 | [State.StateChange](https://intl.cloud.tencent.com/document/product/1027/31380) |

## 资料关系链

| 回调类型           | 回调命令字                                                   |
| ------------------ | ------------------------------------------------------------ |
| 添加好友之后回调   | [Sns.CallbackFriendAdd](https://intl.cloud.tencent.com/document/product/1027/31382)        |
| 删除好友之后回调   | [Sns.CallbackFriendDelete](https://intl.cloud.tencent.com/document/product/1027/31383)  |
| 添加黑名单之后回调 | [Sns.CallbackBlackListAdd](https://intl.cloud.tencent.com/document/product/1027/31384)  |
| 删除黑名单之后回调 | [Sns.CallbackBlackListDelete](https://intl.cloud.tencent.com/document/product/1027/31385) |

## 单聊消息

| 回调类型           | 回调命令字                                                   |
| ------------------ | ------------------------------------------------------------ |
| 发单聊消息之前回调 | [C2C.CallbackBeforeSendMsg](https://intl.cloud.tencent.com/document/product/1027/31387) |
| 发单聊消息之后回调 | [C2C.CallbackAfterSendMsg](https://intl.cloud.tencent.com/document/product/1027/31388)  |

## 群组系统

| 回调类型           | 回调命令字                                                   |
| ------------------ | ------------------------------------------------------------ |
|创建群组之前回调|[Group.CallbackBeforeCreateGroup](https://intl.cloud.tencent.com/document/product/1027/31390)|
|创建群组之后回调|[Group.CallbackAfterCreateGroup](https://intl.cloud.tencent.com/document/product/1027/31391)|
|申请入群之前回调|[Group.CallbackBeforeApplyJoinGroup](https://intl.cloud.tencent.com/document/product/1027/31392)|
|拉人入群之前回调|[Group.CallbackBeforeInviteJoinGroup](https://intl.cloud.tencent.com/document/product/1027/31393)|
|新成员入群之后回调|[Group.CallbackAfterNewMemberJoin](https://intl.cloud.tencent.com/document/product/1027/31394)|
|群成员离开之后回调|[Group.CallbackAfterMemberExit](https://intl.cloud.tencent.com/document/product/1027/31395)|
|群内发言之前回调|[Group.CallbackBeforeSendMsg](https://intl.cloud.tencent.com/document/product/1027/31396)|
|群内发言之后回调|[Group.CallbackAfterSendMsg](https://intl.cloud.tencent.com/document/product/1027/31397)|
|群组满员之后回调|[Group.CallbackAfterGroupFull](https://intl.cloud.tencent.com/document/product/1027/31398)|
|群组解散之后回调|[Group.CallbackAfterGroupDestroyed](https://intl.cloud.tencent.com/document/product/1027/31399)|
|群组资料修改之后回调|[Group.CallbackAfterGroupInfoChanged](https://intl.cloud.tencent.com/document/product/1027/31400)|
