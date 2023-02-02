>?インターフェースの詳細については、[Unityのすべてのインターフェース](https://comm.qq.com/im/doc/unity/zh/)をご参照ください。

## 会話関連のインターフェース


| API                                 | 説明                                         |
| --------------------------------------------------------------------------------------------------------------------- | ------------------ |
| [ConvCancelDraft](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvCancelDraft.html)                               | 会話の下書きをキャンセル       |
| [ConvDelete](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvDelete.html)                                         | 会話を削除           |
| [ConvGetConvInfo](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvGetConvInfo.html)                               | 会話の情報を取得       |
| [ConvGetConvList](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvGetConvList.html)                               | 会話リストを取得       |
| [ConvGetTotalUnreadMessageCount](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvGetTotalUnreadMessageCount.html) | 累計未読会話数を取得 |
| [ConvPinConversation](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvPinConversation.html)                       | 会話を先頭固定表示           |
| [ConvSetDraft](https://comm.qq.com/im/doc/unity/zh/api/ConvApi/ConvSetDraft.html)                                     | 会話の下書きを設定       |

## リレーショナルチェーン関連のインターフェース

| API                                 | 説明                                         |
| ------------------------------------------------------------------------------------------------------------------------------- | -------------------- |
| [FriendshipAddFriend](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipAddFriend.html)                           | 友達を追加             |
| [FriendshipAddToBlackList](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipAddToBlackList.html)                 | ブラックリストに追加           |
| [FriendshipCheckFriendType](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipCheckFriendType.html)               | 友達関係を確認         |
| [FriendshipCreateFriendGroup](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipCreateFriendGroup.html)           | 友達グループを作成        |
| [FriendshipDeleteFriend](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipDeleteFriend.html)                     | 友達を削除             |
| [FriendshipDeleteFriendGroup](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipDeleteFriendGroup.html)           | 友達グループを削除     |
| [FriendshipDeleteFromBlackList](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipDeleteFromBlackList.html)       | ブラックリストから削除         |
| [FriendshipDeletePendency](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipDeletePendency.html)                 | 未処理の友達追加申請を削除     |
| [FriendshipGetBlackList](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipGetBlackList.html)                     | ブラックリストを取得       |
| [FriendshipGetFriendGroupList](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipGetFriendGroupList.html)         | 友達グループリストを取得     |
| [FriendshipGetFriendProfileList](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipGetFriendProfileList.html)     | 友達プロフィールリストを取得     |
| [FriendshipGetFriendsInfo](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipGetFriendsInfo.html)                 | 友達の情報を取得         |
| [FriendshipGetPendencyList](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipGetPendencyList.html)               | 未処理の友達追加申請を取得     |
| [FriendshipHandleFriendAddRequest](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipHandleFriendAddRequest.html) | 友達追加申請を処理         |
| [FriendshipModifyFriendGroup](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipModifyFriendGroup.html)           | 友達グループを変更     |
| [FriendshipModifyFriendProfile](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipModifyFriendProfile.html)       | 友達プロフィールを変更         |
| [FriendshipReportPendencyReaded](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipReportPendencyReaded.html)     | 未処理の友達追加申請が既読になったことを報告 |
| [FriendshipSearchFriends](https://comm.qq.com/im/doc/unity/zh/api/FriendshipApi/FriendshipSearchFriends.html)                   | 友達を検索             |

## グループ関連のインターフェース

| API                                 | 説明                                         |
| -------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| [GroupCreate](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupCreate.html)                                     | グループを作成                                   |
| [GroupCreateTopicInCommunity](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupCreateTopicInCommunity.html)     | トピックを作成                                 |
| [GroupDelete](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupDelete.html)                                     | グループを削除                                   |
| [GroupDeleteGroupAttributes](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupDeleteGroupAttributes.html)       | グループのカスタム属性を削除                         |
| [GroupDeleteMember](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupDeleteMember.html)                         | グループメンバーを強制退会                               |
| [GroupDeleteTopicFromCommunity](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupDeleteTopicFromCommunity.html) | トピックを削除                                 |
| [GroupGetGroupAttributes](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupGetGroupAttributes.html)             | 指定したグループ属性を取得                           |
| [GroupGetGroupInfoList](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupGetGroupInfoList.html)                 | グループの情報を取得                               |
| [GroupGetJoinedCommunityList](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupGetJoinedCommunityList.html)     | 現在のユーザが参加している、トピックをサポートするコミュニティのリストを取得 |
| [GroupGetJoinedGroupList](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupGetJoinedGroupList.html)             | 参加しているグループのリストを取得                     |
| [GroupGetMemberInfoList](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupGetMemberInfoList.html)               | グループメンバーの情報を取得                           |
| [GroupGetOnlineMemberCount](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupGetOnlineMemberCount.html)         | グループのオンラインメンバー数を取得                         |
| [GroupGetPendencyList](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupGetPendencyList.html)                   | 未処理のグループメッセージリストを取得                       |
| [GroupGetTopicInfoList](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupGetTopicInfoList.html)                 | トピックリストを取得                             |
| [GroupHandlePendency](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupHandlePendency.html)                     | 未処理のグループメッセージリストを処理                          |
| [GroupInitGroupAttributes](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupInitGroupAttributes.html)           | グループのカスタム属性を初期化                       |
| [GroupInviteMember](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupInviteMember.html)                         | ユーザをグループに招待                             |
| [GroupJoin](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupJoin.html)                                         | グループに参加                                   |
| [GroupModifyGroupInfo](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupModifyGroupInfo.html)                   | グループの情報を変更                              |
| [GroupModifyMemberInfo](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupModifyMemberInfo.html)                 | グループメンバーの情報を変更                           |
| [GroupQuit](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupQuit.html)                                         | グループを退出                                   |
| [GroupReportPendencyReaded](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupReportPendencyReaded.html)         | 未処理のグループメッセージが既読になったことを報告                       |
| [GroupSearchGroupMembers](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupSearchGroupMembers.html)             | グループメンバーを検索                               |
| [GroupSearchGroups](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupSearchGroups.html)                         | グループ資料を検索                               |
| [GroupSetGroupAttributes](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupSetGroupAttributes.html)             | グループ属性を設定                               |
| [GroupSetTopicInfo](https://comm.qq.com/im/doc/unity/zh/api/GroupApi/GroupSetTopicInfo.html)                         | トピックの情報を変更                             |

## IM SDK初期化関連のインターフェース

| API                                                          | 説明                                           |
| ------------------------------------------------------------------------------------- | -------------------- |
| [GetSDKVersion](https://comm.qq.com/im/doc/unity/zh/api/IMSDKInit/GetSDKVersion.html) | SDK下位層ライブラリのバージョンを取得    |
| [GetServerTime](https://comm.qq.com/im/doc/unity/zh/api/IMSDKInit/GetServerTime.html) | サーバー側の時間（秒）を取得 |
| [Init](https://comm.qq.com/im/doc/unity/zh/api/IMSDKInit/Init.html)                   | IM SDKを初期化         |
| [SetConfig](https://comm.qq.com/im/doc/unity/zh/api/IMSDKInit/SetConfig.html)         | グループ設定を設定         |
| [Uninit](https://comm.qq.com/im/doc/unity/zh/api/IMSDKInit/Uninit.html)               | IM SDKを初期化解除       |


## ログイン関連のインターフェース

| API                                                          | 説明                                           |
| ------------------------------------------------------------------------------------------- | ------------------ |
| [GetLoginStatus](https://comm.qq.com/im/doc/unity/zh/api/loginOrlogout/GetLoginStatus.html) | 現在のログイン状態を取得   |
| [GetLoginUserID](https://comm.qq.com/im/doc/unity/zh/api/loginOrlogout/GetLoginUserID.html) | ログインしているユーザのIDを取得 |
| [Login](https://comm.qq.com/im/doc/unity/zh/api/loginOrlogout/Login.html)                   | ログイン               |
| [Logout](https://comm.qq.com/im/doc/unity/zh/api/loginOrlogout/Logout.html)                 | ログアウト               |

## メッセージ関連のインターフェース

| API                                 | 説明                                         |
| ---------------------------------------------------------------------------------------------------------------------------- | -------------------------------------- |
| [GetMsgGroupMessageReadMemberList](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/GetMsgGroupMessageReadMemberList.html) | グループメッセージを既読したグループメンバーのリストを取得               |
| [MsgBatchSend](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgBatchSend.html)                                         | メッセージを一括送信                           |
| [MsgCancelSend](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgCancelSend.html)                                       | メッセージ送信をキャンセル                           |
| [MsgClearHistoryMessage](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgClearHistoryMessage.html)                     | メッセージ履歴をクリア                           |
| [MsgDelete](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgDelete.html)                                               | メッセージを削除                               |
| [MsgDoBackground](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgDoBackground.html)                                   | APPがバックグランドで動作するようになったことを検出した場合、このインターフェースを呼び出すことが可能|
| [MsgDoForeground](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgDoForeground.html)                                   | APPがフォアグラウンドで動作するようになったことを検出した場合、このインターフェースを呼び出すことが可能   |
| [MsgDownloadElemToPath](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgDownloadElemToPath.html)                       | マルチメッセージをダウンロード                         |
| [MsgDownloadMergerMessage](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgDownloadMergerMessage.html)                 | マージメッセージをダウンロード                           |
| [MsgFindByMsgLocatorList](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgFindByMsgLocatorList.html)                   | メッセージロケーターでメッセージを検索                 |
| [MsgFindMessages](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgFindMessages.html)                                   | ローカルでメッセージを検索                         |
| [MsgGetC2CReceiveMessageOpt](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgGetC2CReceiveMessageOpt.html)             | C2Cのメッセージ受信オプションを取得                      |
| [MsgGetMessageReadReceipts](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgGetMessageReadReceipts.html)               | メッセージ既読確認を取得                       |
| [MsgGetMsgList](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgGetMsgList.html)                                       | メッセージ履歴リストを取得                       |
| [MsgImportMsgList](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgImportMsgList.html)                                 | メッセージをインポート                               |
| [MsgListDelete](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgListDelete.html)                                       | メッセージを削除                               |
| [MsgMarkAllMessageAsRead](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgMarkAllMessageAsRead.html)                   | すべてのメッセージを既読でマーク                     |
| [MsgModifyMessage](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgModifyMessage.html)                                 | メッセージを変更                               |
| [MsgReportReaded](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgReportReaded.html)                                   | メッセージが既読になったことをC2Cに報告                       |
| [MsgRevoke](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgRevoke.html)                                               | メッセージを取り消す                               |
| [MsgSaveMsg](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgSaveMsg.html)                                             | メッセージを保存                               |
| [MsgSearchLocalMessages](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgSearchLocalMessages.html)                     | ローカルメッセージを検索                           |
| [MsgSendMessage](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgSendMessage.html)                                     | メッセージを送信                               |
| [MsgSendMessageReadReceipts](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgSendMessageReadReceipts.html)             | メッセージ既読確認を送信                       |
| [MsgSetC2CReceiveMessageOpt](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgSetC2CReceiveMessageOpt.html)             | メッセージ受信オプションを設定                         |
| [MsgSetGroupReceiveMessageOpt](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgSetGroupReceiveMessageOpt.html)         | グループメッセージ受信オプションを設定                       |
| [MsgSetLocalCustomData](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgSetLocalCustomData.html)                       | メッセージのローカルデータを設定                       |
| [MsgSetOfflinePushToken](https://comm.qq.com/im/doc/unity/zh/api/MessageApi/MsgSetOfflinePushToken.html)                     | オフラインプッシュの設定情報を設定                   |

## ユーザプロフィール関連のインターフェース

| API                                 | 説明                                         |
| ----------------------------------------------------------------------------------------------------------------- | ---------------- |
| [GetUserStatus](https://comm.qq.com/im/doc/unity/zh/api/UserApi/GetUserStatus.html)                               | ユーザ状態を取得     |
| [ProfileGetUserProfileList](https://comm.qq.com/im/doc/unity/zh/api/UserApi/ProfileGetUserProfileList.html)       | ユーザプロフィールリストを取得 |
| [ProfileModifySelfUserProfile](https://comm.qq.com/im/doc/unity/zh/api/UserApi/ProfileModifySelfUserProfile.html) | 自分のプロフィールを変更   |
| [SetSelfStatus](https://comm.qq.com/im/doc/unity/zh/api/UserApi/SetSelfStatus.html)                               | 自分の状態を設定   |
| [SubscribeUserStatus](https://comm.qq.com/im/doc/unity/zh/api/UserApi/SubscribeUserStatus.html)                   | ユーザ状態をサブスクライブ     |
| [UnsubscribeUserStatus](https://comm.qq.com/im/doc/unity/zh/api/UserApi/UnsubscribeUserStatus.html)               | ユーザ状態のサブスクリプションをキャンセル |

## SDKコールバックの登録

| API                                 | 説明                                         |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------- |
| [AddRecvNewMsgCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/AddRecvNewMsgCallback.html)                                                 | 新しいメッセージを受信するコールバックを登録                           |
| [RemoveRecvNewMsgCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/RemoveRecvNewMsgCallback.html)                                           | 新しいメッセージを受信するコールバックをリムーブ                           |
| [SetConvEventCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetConvEventCallback.html)                                                   | 会話イベントコールバックを設定                             |
| [SetConvTotalUnreadMessageCountChangedCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetConvTotalUnreadMessageCountChangedCallback.html) | 会話の累計未読メッセージ数が変更されたコールバックを設定               |
| [SetFriendAddRequestCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetFriendAddRequestCallback.html)                                     | 友達追加申請コールバックを設定                       |
| [SetFriendApplicationListDeletedCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetFriendApplicationListDeletedCallback.html)             | 友達追加申請が削除されたコールバックを設定                     |
| [SetFriendApplicationListReadCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetFriendApplicationListReadCallback.html)                   | 友達追加申請が既読になったコールバックを設定                       |
| [SetFriendBlackListAddedCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetFriendBlackListAddedCallback.html)                             | ブラックリストへの追加コールバックを設定                         |
| [SetFriendBlackListDeletedCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetFriendBlackListDeletedCallback.html)                         | ブラックリストからの削除コールバックを設定                         |
| [SetGroupAttributeChangedCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetGroupAttributeChangedCallback.html)                           | グループ属性変更コールバックを設定                         |
| [SetGroupTipsEventCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetGroupTipsEventCallback.html)                                         | グループシステムメッセージコールバックを設定                         |
| [SetGroupTopicChangedCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetGroupTopicChangedCallback.html)                                   | トピック更新コールバックを設定                             |
| [SetGroupTopicCreatedCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetGroupTopicCreatedCallback.html)                                   | トピックを作成するコールバックを設定                             |
| [SetGroupTopicDeletedCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetGroupTopicDeletedCallback.html)                                   | トピックを削除するコールバックを設定                           |
| [SetKickedOfflineCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetKickedOfflineCallback.html)                                           | 強制退会によるオフライン通知コールバックを設定                         |
| [SetLogCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetLogCallback.html)                                                               | ログコールバックを設定                                 |
| [SetMsgElemUploadProgressCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetMsgElemUploadProgressCallback.html)| メッセージにおけるエレメントに関するファイルのアップロード進捗コールバックを設定               |
| [SetMsgReadedReceiptCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetMsgReadedReceiptCallback.html)                | メッセージ既読確認コールバックを設定                         |
| [SetMsgRevokeCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetMsgRevokeCallback.html)                                     | 受信したメッセージが取り消されたコールバックを設定                         |
| [SetMsgUpdateCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetMsgUpdateCallback.html)                                     | メッセージがクラウド側で変更されたことによって返された更新通知コールバックを設定 |
| [SetNetworkStatusListenerCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetNetworkStatusListenerCallback.html)        | ネットワーク接続状態リスナーコールバックを設定                         |
| [SetOnAddFriendCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetOnAddFriendCallback.html)                                   | 友達追加コールバックを設定                               |
| [SetOnDeleteFriendCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetOnDeleteFriendCallback.html)                         | 友達削除コールバックを設定                               |
| [SetOnDeleteFriendCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetOnDeleteFriendCallback.html)                         | 友達削除コールバックを設定                               |
| [SetSelfInfoUpdatedCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetSelfInfoUpdatedCallback.html)                                       | 現在のユーザの情報が更新されたコールバックを設定           |
| [SetUpdateFriendProfileCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetUpdateFriendProfileCallback.html)           | 友達プロファイル更新コールバックを設定                           |
| [SetUserSigExpiredCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetUserSigExpiredCallback.html)                                         | 資格情報期限切れコールバックを設定                             |
| [SetUserStatusChangedCallback](https://comm.qq.com/im/doc/unity/zh/api/SDKRegisteringCallback/SetUserStatusChangedCallback.html)                                   | ユーザ状態変更通知コールバックを設定                     |





