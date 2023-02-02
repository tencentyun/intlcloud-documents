## ログインインターフェースの初期化

正常に初期化してログインすることが、Tencent Cloud IMサービスを正常に使用するための前提です。


| API                                                          | 説明                                                  |
| --------------------------------------------------------------------------------------- | ------------------------- |
| [initSDK](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/initSDK.html)               | SDKを初期化                |
| [unInitSDK](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/unInitSDK.html)           | SDKを初期化解除              |
| [login](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/login.html)                   | ログイン                      |
| [logout](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/logout.html)                 | ログアウト                      |
| [getLoginUser](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/getLoginUser.html)     | ログインしているユーザのUserIDを取得 |
| [getLoginStatus](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/getLoginStatus.html) | ログイン状態を取得              |
| [getServerTime](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/getServerTime.html)   | サーバーの現在の時間を取得        |
| [getVersion](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/getVersion.html)         | バージョン番号を取得                |

## シグナルインターフェース

| API                                 | 説明                                         |
| ------------------------------------------------------------------------------------------------------------------ | ---------------- |
| [accept](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMSignalingManager/accept.html)                                   | 受信側が招待を受け入れる   |
| [addInvitedSignaling](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMSignalingManager/addInvitedSignaling.html)         |  シグナリングリクエストを作成  |
| [addSignalingListener](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMSignalingManager/addSignalingListener.html)       | シグナリングリスナーを追加     |
| [cancel](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMSignalingManager/cancel.html)                                   | 招待側が招待をキャンセル   |
| [getSignalingInfo](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMSignalingManager/getSignalingInfo.html)               | シグナリング情報を取得     |
| [invite](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMSignalingManager/invite.html)                                   | ある人を招待       |
| [inviteInGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMSignalingManager/inviteInGroup.html)                     | グループ内の一部の人を招待 |
| [reject](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMSignalingManager/reject.html)                                   | 受信側が招待を拒否   |
| [removeSignalingListener](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMSignalingManager/removeSignalingListener.html) | シグナリングリスナーをリムーブ   |

## メッセージ関連のインターフェース

| API                                 | 説明                                         |
| ---------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| [addAdvancedMsgListener](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/addAdvancedMsgListener.html)                     | 高度なメッセージのイベントリスナーを追加                            |
| [appendMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/appendMessage.html)                                       | 1通のメッセージに1通のメッセージを付けてリンクリストを追加。            |
| [clearC2CHistoryMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/clearC2CHistoryMessage.html)                     | 1対1チャットのローカルとクラウド側のメッセージをクリア（会話を削除しない）              |
| [clearGroupHistoryMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/clearGroupHistoryMessage.html)                 | グループチャットのローカルとクラウド側のメッセージをクリア（会話を削除しない）              |
| [createCustomMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createCustomMessage.html)                           | カスタムメッセージを作成                                      |
| [createFaceMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createFaceMessage.html)                               | スタンプメッセージを作成                                        |
| [createFileMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createFileMessage.html)                               | ファイルメッセージを作成                                        |
| [createForwardMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createForwardMessage.html)                         | 転送メッセージを作成                                        |
| [createImageMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createImageMessage.html)                             | 画像メッセージを作成                                         |
| [createLocationMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createLocationMessage.html)                       | 位置メッセージを作成                           |
| [createMergerMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createMergerMessage.html)                           | マージメッセージを作成                                         |
| [createSoundMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createSoundMessage.html)                             | 音声メッセージを作成                                         |
| [createTargetedGroupMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createTargetedGroupMessage.html)             | 指定グループメンバーのみ受信可能メッセージを作成                                  |
| [createTextAtMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createTextAtMessage.html)                           | テキストメッセージを作成。@を付けてリマインドする機能を利用可能(ライブストリーミンググループではサポートされない) |
| [createTextMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createTextMessage.html)                               | テキストメッセージを作成                                        |
| [createVideoMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/createVideoMessage.html)                             | ビデオメッセージを作成                                        |
| [deleteMessageExtensions](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/deleteMessageExtensions.html)                   | メッセージ拡張を削除                                        |
| [deleteMessageFromLocalStorage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/deleteMessageFromLocalStorage.html)       | ローカルメッセージを削除                                        |
| [deleteMessages](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/deleteMessages.html)                                     | ローカルとローミングメッセージを削除                                  |
| [downloadMergerMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/downloadMergerMessage.html)                       | マージ対象となるサブメッセージのリストを取得                            |
| [downloadMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/downloadMessage.html)                                   | マルチメッセージをダウンロード                                      |
| [getC2CHistoryMessageList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getC2CHistoryMessageList.html)                 | 1対1チャットのメッセージ履歴を取得                                    |
| [getC2CReceiveMessageOpt](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getC2CReceiveMessageOpt.html)                   | あるユーザのC2Cメッセージ受信おプションを確認                     |
| [getGroupHistoryMessageList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getGroupHistoryMessageList.html)             | グループのメッセージ履歴を取得                                    |
| [getGroupMessageReadMemberList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getGroupMessageReadMemberList.html)       | グループメッセージを既読/未読したグループメンバーのリストを取得                      |
| [getHistoryMessageList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getHistoryMessageList.html)                       | メッセージ履歴の高度なインターフェースを取得                                |
| [getMessageExtensions](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getMessageExtensions.html)                         | メッセージ拡張を取得                                        |
| [getMessageOnlineUrl](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getMessageOnlineUrl.html)                           | マルチメディアメッセージのURLを取得                                   |
| [getMessageReadReceipts](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/getMessageReadReceipts.html)                     | メッセージ既読確認を取得                                  |
| [insertC2CMessageToLocalStorage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/insertC2CMessageToLocalStorage.html)     | C2Cメッセージリストにメッセージを追加                         |
| [insertGroupMessageToLocalStorage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/insertGroupMessageToLocalStorage.html) | グループメッセージリストにメッセージを追加                        |
| [markAllMessageAsRead](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/markAllMessageAsRead.html)                         | すべてのメッセージを既読でマーク                                  |
| [markC2CMessageAsRead](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/markC2CMessageAsRead.html)                         | 1対1チャットのメッセージを既読でマーク                                    |
| [markGroupMessageAsRead](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/markGroupMessageAsRead.html)                     | グループチャットのメッセージを既読でマーク                                    |
| [modifyMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/modifyMessage.html)                                       | メッセージを編集                 |
| [removeAdvancedMsgListener](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/removeAdvancedMsgListener.html)               | 高度なメッセージリスナーをリムーブ                                  |
| [reSendMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/reSendMessage.html)                                       | メッセージを再送                                            |
| [revokeMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/revokeMessage.html)                                       | メッセージを取り消す                                            |
| [searchLocalMessages](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/searchLocalMessages.html)                           | ローカルメッセージを検索                                        |
| [sendMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/sendMessage.html)                                           | メッセージを送信                                            |
| [sendMessageReadReceipts](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/sendMessageReadReceipts.html)                   | メッセージ既読確認を送信                                    |
| [sendReplyMessage](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/sendReplyMessage.html)                                 | 返事メッセージを送信                                        |
| [setC2CReceiveMessageOpt](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/setC2CReceiveMessageOpt.html)                   | ユーザメッセージ受信オプションを設定                                |
| [setGroupReceiveMessageOpt](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/setGroupReceiveMessageOpt.html)               | グループメッセージ受信オプションを設定                                |
| [setLocalCustomData](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/setLocalCustomData.html)                             | メッセージのカスタムデータを設定                                  |
| [setLocalCustomInt](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/setLocalCustomInt.html)                               | メッセージのカスタムデータを設定                                  |
| [setMessageExtensions](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMMessageManager/setMessageExtensions.html)                         | メッセージ拡張を設定                                        |




## 会話関連のインターフェース

| API                                 | 説明                                         |
| --------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| [addConversationListener](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/addConversationListener.html)                         | 会話リスナーを設定             |
| [deleteConversation](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/deleteConversation.html)                                   | 会話を削除                   |
| [getConversation](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/getConversation.html)                                         | 会話情報を取得               |
| [getConversationList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/getConversationList.html)                                 | 会話リストを取得               |
| [getConversationListByConversaionIds](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/getConversationListByConversaionIds.html) | 会話IDで指定した会話リストを取得 |
| [getTotalUnreadMessageCount](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/getTotalUnreadMessageCount.html)                   | 未読会話数を取得           |
| [pinConversation](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/pinConversation.html)                                         | 会話を先頭固定表示                   |
| [removeConversationListener](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/removeConversationListener.html)                   | 会話リスナーをリムーブ             |
| [setConversationDraft](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMConversationManager/setConversationDraft.html)                               | 会話の下書きを設定               |


## リレーショナルチェーン関連のインターフェース

| API                    | 説明                                         |
| ----------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| [acceptFriendApplication](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/acceptFriendApplication.html)           | 友達追加申請を許可           |
| [addFriend](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/addFriend.html)                                       | 友達を追加               |
| [addFriendListener](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/addFriendListener.html)                       | リレーショナルチェーンリスナーを追加       |
| [addFriendsToFriendGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/addFriendsToFriendGroup.html)           | 友達をある友達グループに追加 |
| [addToBlackList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/addToBlackList.html)                             | ユーザをブラックリストに追加       |
| [checkFriend](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/checkFriend.html)                                   | 指定したユーザの友達関係を確認 |
| [createFriendGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/createFriendGroup.html)                       | 友達グループを新規作成           |
| [deleteFriendApplication](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/deleteFriendApplication.html)           | 友達追加申請を削除           |
| [deleteFriendGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/deleteFriendGroup.html)                       | 友達グループを削除           |
| [deleteFriendsFromFriendGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/deleteFriendsFromFriendGroup.html) | 友達追加申請を削除           |
| [deleteFromBlackList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/deleteFromBlackList.html)                   | ブラックリストからユーザを削除   |
| [deleteFromFriendList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/deleteFromFriendList.html)                 | 友達を削除               |
| [getBlackList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/getBlackList.html)                                 | ブラックリストを取得         |
| [getFriendApplicationList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/getFriendApplicationList.html)         | 友達追加申請リストを取得       |
| [getFriendGroups](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/getFriendGroups.html)                           | 友達グループリストを取得       |
| [getFriendList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/getFriendList.html)                               | 友達リストを取得           |
| [getFriendsInfo](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/getFriendsInfo.html)                             | 指定した友達の情報を取得       |
| [refuseFriendApplication](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/refuseFriendApplication.html)           | 友達追加申請を拒否           |
| [removeFriendListener](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/removeFriendListener.html)                 | リレーショナルチェーンリスナーをリムーブ        |
| [renameFriendGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/renameFriendGroup.html)                       | 友達グループ名を変更     |
| [searchFriends](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/searchFriends.html)                               | 友達を検索               |
| [setFriendApplicationRead](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/setFriendApplicationRead.html)         | 友達追加申請既読を設定       |
| [setFriendInfo](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMFriendshipManager/setFriendInfo.html)                               | 指定した友達の情報を設定       |

## グループ関連のインターフェース

| API                                 | 説明                                         |
| ----------------------------------- | ---------------------------------------- |
| [addGroupListener](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/addGroupListener.html)                       | グループリスナーを追加                           |
| [dismissGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/dismissGroup.html)                               | グループを解散                                 |
| [joinGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/joinGroup.html)                                     | グループに参加                                 |
| [quitGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/quitGroup.html)                                     | グループを退出                                 |
| [removeGroupListener](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMManager/removeGroupListener.html)                 | グループリスナーをリムーブ                           |
| [acceptGroupApplication](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/acceptGroupApplication.html)       | グループ参加申請を許可                       |
| [createGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/createGroup.html)                             | カスタムグループを作成                           |
| [createTopicInCommunity](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/createTopicInCommunity.html)       | トピックを作成                                 |
| [deleteGroupAttributes](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/deleteGroupAttributes.html)         | 指定したグループの属性を削除                           |
| [deleteTopicFromCommunity](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/deleteTopicFromCommunity.html)   | トピックを削除                                 |
| [getGroupApplicationList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/getGroupApplicationList.html)     | グループ参加申請リストを取得                       |
| [getGroupAttributes](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/getGroupAttributes.html)               | 指定したグループの属性を取得                           |
| [getGroupMemberList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/getGroupMemberList.html)               | グループメンバーリストを取得                           |
| [getGroupMembersInfo](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/getGroupMembersInfo.html)             | 指定したグループメンバーの情報を取得                     |
| [getGroupOnlineMemberCount](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/getGroupOnlineMemberCount.html) | 指定したグループのオンライングループメンバー数を取得                       |
| [getGroupsInfo](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/getGroupsInfo.html)                         | グループ情報を取得                               |
| [getJoinedCommunityList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/getJoinedCommunityList.html)       | 現在のユーザが参加している、トピックをサポートするコミュニティのリストを取得 |
| [getJoinedGroupList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/getJoinedGroupList.html)               | 現在のユーザが参加しているグループを取得               |
| [getTopicInfoList](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/getTopicInfoList.html)                   | トピック属性リストを取得                       |
| [initGroupAttributes](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/initGroupAttributes.html)             | グループ属性を初期化                             |
| [inviteUserToGroup](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/inviteUserToGroup.html)                 | 他人をグループに招待                             |
| [kickGroupMember](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/kickGroupMember.html)                     | 強制退会                                     |
| [muteGroupMember](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/muteGroupMember.html)                     | 発言禁止                                     |
| [refuseGroupApplication](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/refuseGroupApplication.html)       | グループ参加申請を拒否                       |
| [searchGroupMembers](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/searchGroupMembers.html)               | グループメンバーを検索                               |
| [searchGroups](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/searchGroups.html)                           | グループを検索                               |
| [setGroupApplicationRead](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/setGroupApplicationRead.html)     | すべてのグループ申請リストを既読でマーク               |
| [setGroupAttributes](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/setGroupAttributes.html)               | グループ属性を設定                               |
| [setGroupInfo](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/setGroupInfo.html)                           | グループ情報を変更                               |
| [setGroupMemberInfo](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/setGroupMemberInfo.html)               | 指定したグループメンバーの情報を変更                     |
| [setGroupMemberRole](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/setGroupMemberRole.html)               | グループメンバーのロールを設定                         |
| [setTopicInfo](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/setTopicInfo.html)                           | トピック属性を設定                             |
| [transferGroupOwner](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMGroupManager/transferGroupOwner.html)               | グループオーナーの権限を譲渡                                 |

## オフラインプッシュ関連のインターフェース

| API                                 | 説明                                         |
| -------------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| [doBackground](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMOfflinePushManager/doBackground.html)                 | APPがバックグランドで動作するようになったことを検出した場合、このインターフェースを呼び出すことが可能     |
| [doForeground](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMOfflinePushManager/doForeground.html)                 | APPがフォアグラウンドで動作するようになったことを検出した場合、このインターフェースを呼び出すことが可能     |
| [setOfflinePushConfig](https://comm.qq.com/im/doc/RN/zh/Api/V2TIMOfflinePushManager/setOfflinePushConfig.html) | オフラインプッシュの設定情報を設定                     |
