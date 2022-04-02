## Online Status

| Callback Type | Callback Command Keyword |
| ---------------- | --------------------------------------------- |
| Status change callback | [State.StateChange](https://intl.cloud.tencent.com/document/product/1047/34357) |

## Profile Relationship Chain

| Callback Type | Callback Command Keyword |
| ------------------ | ------------------------------------------------------------ |
| Callback before adding a friend   | [Sns.CallbackPrevFriendAdd](https://intl.cloud.tencent.com/document/product/1047/43468)        |
| Callback before a friend request is responded   | [Sns.CallbackPrevFriendResponse](https://intl.cloud.tencent.com/document/product/1047/43467)  |
| Callback after adding a friend | [Sns.CallbackFriendAdd](https://intl.cloud.tencent.com/document/product/1047/34359) |
| Callback after deleting a friend | [Sns.CallbackFriendDelete](https://intl.cloud.tencent.com/document/product/1047/34360) |
| Callback after adding a blocklist | [Sns.CallbackBlackListAdd](https://intl.cloud.tencent.com/document/product/1047/34361) |
| Callback after deleting a blocklist | [Sns.CallbackBlackListDelete](https://intl.cloud.tencent.com/document/product/1047/34362) |

## One-to-One Chat Messages

| Callback Type | Callback Command Keyword |
| ------------------ | ------------------------------------------------------------ |
| Callback before sending one-to-one chat messages | [C2C.CallbackBeforeSendMsg](https://intl.cloud.tencent.com/document/product/1047/34364) |
| Callback after sending one-to-one chat messages | [C2C.CallbackAfterSendMsg](https://intl.cloud.tencent.com/document/product/1047/34365) |
| Callback after marking a one-to-one message as read| [C2C.CallbackAfterMsgReport](https://intl.cloud.tencent.com/document/product/1047/43465)  |
| Callback after recalling a one-to-one message | [C2C.CallbackAfterMsgWithDraw](https://intl.cloud.tencent.com/document/product/1047/43466)  |

## Group Systems

| Callback Type | Callback Command Keyword |
| ------------------ | ------------------------------------------------------------ |
| Callback before creating a group | [Group.CallbackBeforeCreateGroup](https://intl.cloud.tencent.com/document/product/1047/34368) |
| Callback after creating a group | [Group.CallbackAfterCreateGroup](https://intl.cloud.tencent.com/document/product/1047/34369) |
| Callback before applying to join a group | [Group.CallbackBeforeApplyJoinGroup](https://intl.cloud.tencent.com/document/product/1047/34370) |
| Callback before inviting users to a group | [Group.CallbackBeforeInviteJoinGroup](https://intl.cloud.tencent.com/document/product/1047/34371) |
| Callback after a new member joins a group | [Group.CallbackAfterNewMemberJoin](https://intl.cloud.tencent.com/document/product/1047/34372) |
| Callback after a group member quits | [Group.CallbackAfterMemberExit](https://intl.cloud.tencent.com/document/product/1047/34373) |
| Callback before delivering a group message | [Group.CallbackBeforeSendMsg](https://intl.cloud.tencent.com/document/product/1047/34374) |
| Callback after delivering a group message | [Group.CallbackAfterSendMsg](https://intl.cloud.tencent.com/document/product/1047/34375) |
| Callback after a group is full | [Group.CallbackAfterGroupFull](https://intl.cloud.tencent.com/document/product/1047/34376) |
| Callback after dismissing a group | [Group.CallbackAfterGroupDestroyed](https://intl.cloud.tencent.com/document/product/1047/34377) |
| Callback after modifying the profile of a group | [Group.CallbackAfterGroupInfoChanged](https://intl.cloud.tencent.com/document/product/1047/34378) |
