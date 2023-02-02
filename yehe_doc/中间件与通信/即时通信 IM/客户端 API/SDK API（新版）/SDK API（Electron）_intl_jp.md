## イベントコールバックインターフェース


| API                                 | 説明                                         |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------ |
| [TIMAddRecvNewMsgCallback](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMAddRecvNewMsgCallback.html?h=TIMAddRecvNewMsgCallback)                                  | 新しいメッセージを受信するコールバックを追加                               |
| [TIMRemoveRecvNewMsgCallback](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMRemoveRecvNewMsgCallback.html?h=TIMRemoveRecvNewMsgCallback)                         | 新しいメッセージを受信するコールバックを削除                               |
| [TIMSetMsgReadedReceiptCallback](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMSetMsgReadedReceiptCallback.html?h=TIMSetMsgReadedReceiptCallback)                | メッセージ既読確認コールバックを設定                         |
| [TIMSetMsgRevokeCallback](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMSetMsgRevokeCallback.html?h=TIMSetMsgRevokeCallback)                                     | 受信したメッセージが取り消されたコールバックを設定                         |
| [TIMSetMsgElemUploadProgressCallback](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMSetMsgElemUploadProgressCallback.html?h=TIMSetMsgElemUploadProgressCallback) | メッセージにおけるエレメントに関するファイルのアップロード進捗コールバックを設定               |
| [TIMSetGroupTipsEventCallback](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMSetGroupTipsEventCallback.html?h=TIMSetGroupTipsEventCallback)                               | グループシステムメッセージコールバックを設定                             |
| [TIMSetConvEventCallback](https://comm.qq.com/im/doc/electron/zh/Api/conversationManager/TIMSetConvEventCallback.html?h=TIMSetConvEventCallback)                                       | 会話イベントコールバックを設定                                 |
| [TIMSetNetworkStatusListenerCallback](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMSetNetworkStatusListenerCallback.html?h=TIMSetNetworkStatusListenerCallback)        | ネットワーク接続状態リスナーコールバックを設定                         |
| [TIMSetKickedOfflineCallback](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMSetKickedOfflineCallback.html?h=TIMSetKickedOfflineCallback)                                | 強制退会によるオフライン通知コールバックを設定                             |
| [TIMSetUserSigExpiredCallback](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMSetUserSigExpiredCallback.html?h=TIMSetUserSigExpiredCallback)                             | 資格情報期限切れコールバックを設定                                 |
| [TIMSetOnAddFriendCallback](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMSetOnAddFriendCallback.html?h=TIMSetOnAddFriendCallback)                                   | 友達追加コールバックを設定                               |
| [TIMSetOnDeleteFriendCallback](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMSetOnDeleteFriendCallback.html?h=TIMSetOnDeleteFriendCallback)                          | 友達削除コールバックを設定                               |
| [TIMSetUpdateFriendProfileCallback](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMSetUpdateFriendProfileCallback.html?h=TIMSetUpdateFriendProfileCallback)           | 友達プロファイル更新コールバックを設定                           |
| [TIMSetFriendAddRequestCallback](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMSetFriendAddRequestCallback.html?h=TIMSetFriendAddRequestCallback)                    | 友達追加申請コールバックを設定                           |
| [TIMSetLogCallback](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMSetLogCallback.html?h=TIMSetLogCallback)                                                              | ログコールバックを設定                                     |
| [TIMSetMsgUpdateCallback](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMSetMsgUpdateCallback.html?h=TIMSetMsgUpdateCallback)                                     | メッセージがクラウド側で変更されたことによって返されたメッセージ更新通知コールバックを設定 |


## IM SDK初期化関連のインターフェース

| API                                                          | 説明                                                   |
| --------------------------------------------------------------------------------------------------- | ------------------ |
| [TIMInit](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMInit.html?h=TIMInit)         | IM SDKを初期化      |
| [TIMUninit](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMUninit.html)               | IM SDKをアンインストール        |
| [TIMGetSDKVersion](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMGetSDKVersion.html) | IM SDKのバージョン番号を取得 |
| [TIMSetConfig](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMSetConfig.html)         | 追加ユーザ設定を設定 |


## ログイン/ログアウト関連のインターフェース

| API                                                          | 説明                                           |
| ------------------------------------------------------------------------------------- | ---- |
| [TIMLogin](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMLogin.html)   | ログイン |
| [TIMLogout](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMLogout.html) | ログアウト |


## 会話関連のインターフェース

| API                                 | 説明                                         |
| ------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------- |
| [TIMConvCreate](https://comm.qq.com/im/doc/electron/zh/Api/conversationManager/TIMConvCreate.html)                                         | 会話を作成                   |
| [TIMConvDelete](https://comm.qq.com/im/doc/electron/zh/Api/conversationManager/TIMConvDelete.html)                                         | 会話を削除                   |
| [TIMConvGetConvList](https://comm.qq.com/im/doc/electron/zh/Api/conversationManager/TIMConvGetConvList.html)                               | 最近の連絡先との会話リストを取得   |
| [TIMConvSetDraft](https://comm.qq.com/im/doc/electron/zh/Api/conversationManager/TIMConvSetDraft.html)                                     | 指定した会話の下書きを設定         |
| [TIMConvCancelDraft](https://comm.qq.com/im/doc/electron/zh/Api/conversationManager/TIMConvCancelDraft.html)                               | 指定した会話の下書きを削除         |
| [TIMConvGetConvInfo](https://comm.qq.com/im/doc/electron/zh/Api/conversationManager/TIMConvGetConvInfo.html)                               | 指定した会話リストを取得           |
| [TIMConvGetTotalUnreadMessageCount](https://comm.qq.com/im/doc/electron/zh/Api/conversationManager/TIMConvGetTotalUnreadMessageCount.html) | すべての会話の累計未読メッセージ数を取得 |
| [TIMConvPinConversation](https://comm.qq.com/im/doc/electron/zh/Api/conversationManager/TIMConvPinConversation.html)                       | 会話の先頭固定表示を設定               |


## メッセージ関連のインターフェース

| API                                 | 説明                                         |
| ---------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------- |
| [TIMMsgBatchSend](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgBatchSend.html)                                 | メッセージを一括送信。このインターフェースはグループにメッセージを送信できない|
| [TIMMsgCancelSend](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgCancelSend.html)                               | messageIDで送信中のメッセージをキャンセル    |
| [TIMMsgClearHistoryMessage](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgClearHistoryMessage.html)             | 指定した会話のメッセージをクリア                     |
| [TIMMsgDelete](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgDelete.html)                                       | 指定した会話のローカルメッセージを削除                 |
| [TIMMsgDeleteMessageExtensions](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgDeleteMessageExtensions.html)     | メッセージ拡張を削除                           |
| [TIMMsgDownloadElemToPath](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgDownloadElemToPath.html)               | メッセージ内のエレメントを指定したファイルパスにダウンロード           |
| [TIMMsgDownloadMergerMessage](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgDownloadMergerMessage.html)         | メージメッセージをダウンロード                           |
| [TIMMsgFindByMsgLocatorList](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgFindByMsgLocatorList.html)           | メッセージ特定で指定した会話のメッセージを探す     |
| [TIMMsgFindMessages](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgFindMessages.html)                           | messageIDでローカルのメッセージリストを検索  |
| [TIMMsgGetC2CReceiveMessageOpt](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgGetC2CReceiveMessageOpt.html)     | あるユーザに対するC2Cメッセージ受信オプションを検索    |
| [TIMMsgGetMessageExtensions](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgGetMessageExtensions.html)           | メッセージ拡張を取得                           |
| [TIMMsgGetMsgList](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgGetMsgList.html)                               | 指定した会話のメッセージリストを取得                 |
| [TIMMsgImportMsgList](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgImportMsgList.html)                         | メッセージリストを指定した会話にインポート                 |
| [TIMMsgListDelete](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgListDelete.html)                               | 指定した会話のローカルとローミングメッセージを削除           |
| [TIMMsgModifyMessage](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgModifyMessage.html)                         | メッセージを変更                               |
| [TIMMsgReportReaded](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgReportReaded.html)                           | メッセージの報告を既読                           |
| [TIMMsgRevoke](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgRevoke.html)                                       | メッセージを取り消す                               |
| [TIMMsgSaveMsg](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgSaveMsg.html)                                     | カスタムメッセージを保存                         |
| [TIMMsgSearchLocalMessages](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgSearchLocalMessages.html)             | ローカルメッセージを検索                           |
| [TIMMsgSendNewMsg](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgSendMessage.html)                              | 新しいメッセージを送信                             |
| [TIMMsgSendMessageV2](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgSendMessageV2.html)                         | 新しいメッセージを送信V2                           |
| [TIMMsgSetC2CReceiveMessageOpt](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgSetC2CReceiveMessageOpt.html)     | あるユーザに対するC2Cメッセージ受信オプションを設定    |
| [TIMMsgSetGroupReceiveMessageOpt](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgSetGroupReceiveMessageOpt.html) | グループメッセージの受信オプションを設定                |
| [TIMMsgSetMessageExtensions](https://comm.qq.com/im/doc/electron/zh/Api/advanceMessageManager/TIMMsgSetMessageExtensions.html)           | メッセージ拡張を設定                           |


## グループ関連のインターフェース

| API                                 | 説明                                         |
| --------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------ |
| [TIMGroupCreate](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupCreate.html)                                           | グループを作成                       |
| [TIMGroupDelete](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupDelete.html)                                           | グループを削除（解散）               |
| [TIMGroupDeleteGroupAttributes](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupDeleteGroupAttributes.html)             | グルプ属性を削除                     |
| [TIMGroupDeleteMember](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupDeleteMember.html)                               | グループメンバーを削除                   |
| [TIMGroupGetGroupAttributes](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupGetGroupAttributes.html)                   | 指定したグループ属性を取得                 |
| [TIMGroupGetGroupInfoList](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupGetGroupInfoList.html)                       | グループ情報リストを取得               |
| [TIMGroupGetJoinedGroupList](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupGetJoinedGroupList.html)                   | 参加しているグループのリストを取得             |
| [TIMGroupGetMemberInfoList](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupGetMemberInfoList.html)                     | グループメンバー情報リストを取得             |
| [TIMGroupGetOnlineMemberCount](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupGetOnlineMemberCount.html)               | 指定したグループのオンライングループメンバー数を取得             |
| [TIMGroupGetPendencyList](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupGetPendencyList.html)                         | 未処理グループ操作のリストを取得             |
| [TIMGroupHandlePendency](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupHandlePendency.html)                           | 未処理グループ操作を処理                 |
| [TIMGroupInitGroupAttributes](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupInitGroupAttributes.html)                 | グループ属性を初期化                   |
| [TIMGroupInviteMember](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupInviteMember.html)                               | グループに招待                   |
| [TIMGroupJoin](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupJoin.html)                                               | グループ参加申請                   |
| [TIMGroupModifyGroupInfo](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupModifyGroupInfo.html)                         | グループ情報を変更                     |
| [TIMGroupModifyMemberInfo](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupModifyMemberInfo.html)                       | グループメンバー情報を変更                 |
| [TIMGroupQuit](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupQuit.html)                                               | グループを退出                       |
| [TIMGroupReportPendencyReaded](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupReportPendencyReaded.html)               | 未処理グループ操作の報告を既読             |
| [TIMGroupSearchGroupMembers](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupSearchGroupMembers.html)                   | グループメンバーリストを検索                 |
| [TIMGroupSearchGroups](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupSearchGroups.html)                               | グループリストを検索                     |
| [TIMGroupSetGroupAttributes](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMGroupSetGroupAttributes.html)                   | グループ属性を設定                     |
| [TIMMsgGetGroupMessageReadMemberList](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMMsgGetGroupMessageReadMemberList.html) | グループメッセージを既読または未読したグループメンバーのリストを取得 |
| [TIMMsgGetMessageReadReceipts](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMMsgGetMessageReadReceipts.html)               | メッセージ既読確認を取得               |
| [TIMMsgSendMessageReadReceipts](https://comm.qq.com/im/doc/electron/zh/Api/groupManager/TIMMsgSendMessageReadReceipts.html)             | メッセージ既読確認を送信               |

 



## ユーザプロフィール関連のインターフェース

| API                                 | 説明                                         |
| --------------------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| [TIMProfileGetUserProfileList](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMProfileGetUserProfileList.html)       | 指定したユーザリストの個人プロフィールを取得 |
| [TIMProfileModifySelfUserProfile](https://comm.qq.com/im/doc/electron/zh/Api/timbaseManager/TIMProfileModifySelfUserProfile.html) | 自分の個人プロフィールを変更         |


## リレーショナルチェーン関連のインターフェース

| API                                 | 説明                                         |
| -------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------- |
| [TIMFriendshipAddFriend](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipAddFriend.html)                           | 友達を追加                     |
| [TIMFriendshipAddToBlackList](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipAddToBlackList.html)                 | 指定したユーザをブラックリストに追加         |
| [TIMFriendshipCheckFriendType](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipCheckFriendType.html)               | 友達タイプを確認(単一方向または双方向)     |
| [TIMFriendshipCreateFriendGroup](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipCreateFriendGroup.html)           | 友達グループを作成                 |
| [TIMFriendshipDeleteFriend](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipDeleteFriend.html)                     | 友達を削除                     |
| [TIMFriendshipDeleteFriendGroup](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipDeleteFriendGroup.html)           | 友達グループを削除                 |
| [TIMFriendshipDeleteFromBlackList](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipDeleteFromBlackList.html)       | ブラックリストから指定したユーザリストを削除   |
| [TIMFriendshipDeletePendency](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipDeletePendency.html)                 | 未処理の友達追加申請リストを削除 |
| [TIMFriendshipGetBlackList](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipGetBlackList.html)                     | ブラックリストを取得               |
| [TIMFriendshipGetFriendGroupList](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipGetFriendGroupList.html)         | 指定した友達グループのグループ情報を取得   |
| [TIMFriendshipGetFriendProfileList](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipGetFriendProfileList.html)     | 友達プロフィールリストを取得             |
| [TIMFriendshipGetFriendsInfo](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipGetFriendsInfo.html)                 | 友達の情報を取得                 |
| [TIMFriendshipGetPendencyList](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipGetPendencyList.html)               | 未処理の友達追加申請リストを取得 |
| [TIMFriendshipHandleFriendAddRequest](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipHandleFriendAddRequest.html) | 友達追加申請を処理                 |
| [TIMFriendshipModifyFriendGroup](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipModifyFriendGroup.html)           | 友達グループを変更                 |
| [TIMFriendshipModifyFriendProfile](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipModifyFriendProfile.html)       | 友達プロフィールを更新(備考など)         |
| [TIMFriendshipReportPendencyReaded](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipReportPendencyReaded.html)     | 未処理の友達追加申請の報告を既読 |
| [TIMFriendshipSearchFriends](https://comm.qq.com/im/doc/electron/zh/Api/friendshipManager/TIMFriendshipSearchFriends.html)                   | 友達を検索                     |

