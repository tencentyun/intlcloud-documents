## Online Status

| Webhook Type              | Webhook Command Word                                         |
| ------------------------- | ------------------------------------------------------------ |
| Webhook for status change | [State.StateChange](https://intl.cloud.tencent.com/document/product/1047/34357) |


## Profile Relationship Chain

| Webhook Type                           | Webhook Command Word                                         |
| -------------------------------------- | ------------------------------------------------------------ |
| After a Profile Is Updated             | [Profile.CallbackPortraitSet](https://intl.cloud.tencent.com/document/product/1047/48733) |
| Before a Friend Is Added               | [Sns.CallbackPrevFriendAdd](https://intl.cloud.tencent.com/document/product/1047/43468) |
| Before a Friend Request Is Responded   | [Sns.CallbackPrevFriendResponse](https://intl.cloud.tencent.com/document/product/1047/43467) |
| After a Friend Is Added                | [Sns.CallbackFriendAdd](https://intl.cloud.tencent.com/document/product/1047/34359) |
| After a Friend Is Deleted              | [Sns.CallbackFriendDelete](https://intl.cloud.tencent.com/document/product/1047/34360) |
| After a User Is Added to Blocklist     | [Sns.CallbackBlackListAdd](https://intl.cloud.tencent.com/document/product/1047/34361) |
| After a User Is Removed from Blocklist | [Sns.CallbackBlackListDelete](https://intl.cloud.tencent.com/document/product/1047/34362) |


## One-to-One Message

| Webhook Type                                 | Webhook Command Word                                         |
| -------------------------------------------- | ------------------------------------------------------------ |
| Before a One-to-One Message Is Sent          | [C2C.CallbackBeforeSendMsg](https://intl.cloud.tencent.com/document/product/1047/34364) |
| After a One-to-One Message Is Sent           | [C2C.CallbackAfterSendMsg](https://intl.cloud.tencent.com/document/product/1047/34365) |
| After a One-to-One message Is Marked as Read | [C2C.CallbackAfterMsgReport](https://intl.cloud.tencent.com/document/product/1047/43465) |
| After A One-to-One Message Is Recalled       | [C2C.CallbackAfterMsgWithDraw](https://intl.cloud.tencent.com/document/product/1047/43466) |

## Groups

| Webhook Type                                                 | Webhook Command Word                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Before a Group Is Created                                    | [Group.CallbackBeforeCreateGroup](https://intl.cloud.tencent.com/document/product/1047/34368) |
| After a Group Is Created                                     | [Group.CallbackAfterCreateGroup](https://intl.cloud.tencent.com/document/product/1047/34369) |
| Before Applying to Join a Group                              | [Group.CallbackBeforeApplyJoinGroup](https://intl.cloud.tencent.com/document/product/1047/34370) |
| Before Inviting a User to a Group                            | [Group.CallbackBeforeInviteJoinGroup](https://intl.cloud.tencent.com/document/product/1047/34371) |
| After a User Joins a Group                                   | [Group.CallbackAfterNewMemberJoin](https://intl.cloud.tencent.com/document/product/1047/34372) |
| After a User Leaves a Group                                  | [Group.CallbackAfterMemberExit](https://intl.cloud.tencent.com/document/product/1047/34373) |
| Before Group Message Is Sent                                 | [Group.CallbackBeforeSendMsg](https://intl.cloud.tencent.com/document/product/1047/34374) |
| After a Group Message Is Sent                                | [Group.CallbackAfterSendMsg](https://intl.cloud.tencent.com/document/product/1047/34375) |
| After a Group Is Full                                        | [Group.CallbackAfterGroupFull](https://intl.cloud.tencent.com/document/product/1047/34376) |
| After a Group Is Disbanded                                   | [Group.CallbackAfterGroupDestroyed](https://intl.cloud.tencent.com/document/product/1047/34377) |
| After Group Profile Is Modified                              | [Group.CallbackAfterGroupInfoChanged](https://intl.cloud.tencent.com/document/product/1047/34378) |
| Webhook for Online and Offline Status of Audio-Video Group Members | [Group.CallbackOnMemberStateChange](https://intl.cloud.tencent.com/document/product/1047/48734) |
| Webhook for Exceptions When Group Messages Are Sent          | [Group.CallbackSendMsgException](https://intl.cloud.tencent.com/document/product/1047/49462) |
| Before a Topic Is Created                                    | [Group.CallbackBeforeCreateTopic](https://intl.cloud.tencent.com/document/product/1047/49463) |
| After a Topic Is Created                                     | [Group.CallbackAfterCreateTopic](https://intl.cloud.tencent.com/document/product/1047/49464) |
| After a Topic Is Deleted                                     | [Group.CallbackAfterTopicDestroyed](https://intl.cloud.tencent.com/document/product/1047/49465) |
| Topic Profile Change Webhook                                 | [Group.CallbackAfterTopicInfoChanged](https://intl.cloud.tencent.com/document/product/1047/49466) |
