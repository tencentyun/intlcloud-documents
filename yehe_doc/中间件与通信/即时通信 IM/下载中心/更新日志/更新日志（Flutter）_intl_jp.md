## IM Flutter SDK 3.9.1 @2022.3.24
- 下層データベースのバージョンを6.1.2155にアップグレードします

## IM Flutter SDK 3.9.0 @2022.3.22
- grouplistenerを修正します

## IM Flutter SDK 3.8.9 @2022.3.18
- リッスンと登録の問題を修正します

## IM Flutter SDK 3.8.4 @2022.3.14
- interfaceを更新します

## IM Flutter SDK 3.8.3 @2022.3.1
- 環境に応じてtokenエンコーディングを切り替えます

## IM Flutter SDK 3.8.2 @2022.2.21
- グループメンバーパラメータの制約を更新します

## IM Flutter SDK 3.8.0 @2022.2.17
- 下層interfaceの依存関係をアップグレードします

## IM Flutter SDK 3.7.8 @2022.2.15
- 強制解凍により引き起こされる異常を修正します

## IM Flutter SDK 3.7.7 @2022.2.10
- Swiftコードwarningを修正します
- Swiftの強制解凍コードを書き直します
- sendMessageインターフェースにより返されるmessageインスタンスにidフィールドを追加します


## IM Flutter SDK 3.7.5 @2022.01.23
- 下層データベースを6.0.1975にアップグレードしました
- オフラインプッシュの設定でTPNS TOKENをサポートしました


## IM Flutter SDK 3.7.1 @2022.01.12
- メッセージ送信プログレスイベントで作成したメッセージのidを戻すようにしました
- コールバック部分を最適化し、サービス側にコールバックのエラーがSDK中でcatchされ、サービス側に修正の必要があることを通知するようにしました

## IM Flutter SDK 3.7.0 @2022.01.10
- CloudCustomDataアンパックを最適化しました


## IM Flutter SDK 3.6.9 @2022.01.06
- 返信メッセージパラメータを最適化しました


## IM Flutter SDK 3.6.8 @2022.01.06
- 返信メッセージインターフェースを最適化しました


## IM Flutter SDK 3.6.7 @2022.01.05
- iOSコンパイル環境を8.0から9.0にアップデートしました


## IM Flutter SDK 3.6.6 @2021.12.30
- メッセージに返信インターフェースを追加しました
- Web端末のrelease modeでのエラー問題を修正しました


## IM Flutter SDK 3.6.5 @2021.12.17
- java文法エラーを修正しました

## IM Flutter SDK 3.6.4  @2021.12.17
- Androidの非同期登録イベントで返されないbugを修正しました
- 基礎監視イベントが削除されるエラーを修正しました
- メッセージプログレスイベントに送信中のメッセージのuuidを追加しました

## IM Flutter SDK 3.6.3 @2021.12.9
- addFriendインターフェースの最適化：addTypeをintからFriendTypeEnumに変更しました
- acceptFriendApplicationインターフェースの最適化：acceptTypeをintからFriendResponseTypeEnumに変更しました
- checkFriendインターフェースの最適化：checkTypeをintからFriendTypeEnumに変更しました
- createGroupインターフェースの最適化：addOptをintからGroupAddOptTypeEnumに変更しました
- deleteFromFriendListインターフェースの最適化：deleteTypeをintからFriendTypeEnumに変更しました
- getGroupMemberListインターフェースの最適化：filterをintからGroupMemberFilterTypeEnumに変更しました
- getHistoryMessageListインターフェースの最適化：typeをintからHistoryMsgGetTypeEnumに変更しました
- getHistoryMessageListWithoutFormatインターフェースの最適化：typeをintからHistoryMsgGetTypeEnumに変更しました
- getGroupMemberListインターフェースの最適化：typeをintからGroupMemberFilterTypeEnumに変更しました
- getGroupMemberListインターフェースの最適化：filterをintからGroupMemberFilterTypeEnumに変更しました
- initSDKインターフェースの最適化：loglevelをintからLogLevelEnumに変更しました
- refuseFriendApplicationインターフェースの最適化：acceptTypeをintからFriendApplicationTypeEnumに変更しました
- sendCustomMessageインターフェースの最適化：priorityをintからMessagePriorityEnumに変更しました
- sendFaceMessageインターフェースの最適化：priorityをintからMessagePriorityEnumに変更しました
- sendFileMessageインターフェースの最適化：priorityをintからMessagePriorityEnumに変更しました
- sendForwardMessageインターフェースの最適化：priorityをintからMessagePriorityEnumに変更しました
- sendImageMessageインターフェースの最適化：priorityをintからMessagePriorityEnumに変更しました
- sendLocationMessageインターフェースの最適化：priorityをintからMessagePriorityEnumに変更しました
- sendMergerMessageインターフェースの最適化：priorityをintからMessagePriorityEnumに変更しました
- sendSoundMessageインターフェースの最適化：priorityをintからMessagePriorityEnumに変更しました
- sendTextAtMessageインターフェースの最適化：priorityをintからMessagePriorityEnumに変更しました
- sendTextMessageインターフェースの最適化：priorityをintからMessagePriorityEnumに変更しました
- setGroupMemberRoleインターフェースの最適化：roleをintからGroupMemberRoleTypeEnumに変更しました
- イベントコールバック登録の戻り値を非同期に修正しました

## IM Flutter SDK 3.6.2 @2021.12.9
- 高度なメッセージが削除されuuidが渡されないエラーを修正しました


## IM Flutter SDK 3.6.1 @2021.12.8
- ファイルのプログレスイベントが消失する問題を修正しました


## IM Flutter SDK 3.6.0 @2021.12.1
- 各モジュールでlistenerの複数登録、複数コールバックをサポートしました
- すべてのセッションを既読に設定するapi markAllMessageAsReadを追加しました
- 組み合わせメッセージ解析を追加しました
- nativeのバージョンを5.8.1668にアップデートしました


## IM Flutter SDK 3.5.6 @2021.11.25
- checkFriendが失敗する問題を修正しました
- getC2CHistoryMessageListが後続のメッセージを獲得できない問題を修正しました

## IM Flutter SDK 3.5.5 @2021.11.23
- アーキテクチャを調整しました


## IM Flutter SDK 3.5.4 @2021.11.22
- downloadMergeMesasgeインターフェースを追加しました


## IM Flutter SDK 3.5.3 @2021.11.15
- onTotalUnreadMessageCountChangedイベントを追加しました
- セッションの並び替えのためにV2TimConversationにorderkeyフィールドを追加しました


## IM Flutter SDK 3.5.2 @2021.11.12
add web support

## IM Flutter SDK 3.5.1 @2021.11.10
- 配列の許容外ロジックに対応しました


## IM Flutter SDK 3.5.0 @2021.10.1
- いくつかの既知の問題を修正しました
- 次のインターフェースを追加しました：
 - callExperimentalAPI
 - clearC2CHistoryMessage
 - clearGroupHistoryMessage
 - searchLocalMessages
 - findMessages
 - searchGroups
 - searchGroupMembers
 - getSignalingInfo
 - addInvitedSignaling
 - searchFriends

## IM Flutter SDK 1.0.34 @2021.03.22
- iOSの履歴メッセージ獲得エラーを修正しました

## IM Flutter SDK 1.0.33 @2021.03.22
- sdkのminSdkVersionを16に修正しました

## IM Flutter SDK 1.0.32 @2021.03.22
- セッション情報のlastMessageが空のときcrashする問題を修正しました

## IM Flutter SDK 1.0.30-1.0.31 @2021.03.18
- カスタムメッセージのdataフィールドがnullのときcrashする問題を修正しました

## IM Flutter SDK 1.0.29 @2021.03.16
- 【重要】グループメンバーリスト獲得時のパラメータ渡しのエラーを修正しました

## IM Flutter SDK 1.0.28 @2021.03.16
- 【重要】checkFriendsインターフェースの入力パラメータを変更しました

## IM Flutter SDK 1.0.15-1.0.27 @2021.03.15
- グループメンバーカスタムフィールドを追加しました
- iOSシグナリングを改善しました
- iOSシグナリングbugを修正しました
- カスタムフィールドを解析してStringにして戻すようにしました
- パーソナルカスタムフィールドの設定を最適化しました
- Android getHistoryMessageListを更新しました
- Android端末のcheckFriendのパラメータ渡しエラーを修正しました

## IM Flutter SDK 1.0.5-1.0.14 @2021.02.26
- deleteFriendApplicationのパラメータ渡しエラーを修正しました
- native sdkを5.1.132に更新しました
- native sdkを5.1.137に更新しました
- シグナル招待インターフェースのパラメータ渡しのbugを修正しました
- シグナルインターフェースがidを戻さない問題を修正しました
- sdkの圧縮設定を修正しました
- シグナリングのコールバックのbugを修正しました
- カスタムメッセージの戻しデータを修正しました
- 【重要】シグナリングメッセージの戻す内容のフォーマットを修正したため、シグナリングを使用する場合はこのバージョンおよびそれ以降のバージョンに更新してください


## IM Flutter SDK 1.0.4 @2021.01.14

- Android端末のSDKバージョンを5.1.129に更新しました
- iOS端末のSDKバージョンを5.1.129に更新しました

## IM Flutter SDK 1.0.3 @2021.01.13
- Android/iOSマルチプラットフォームに対応しました
- シングルチャット、グループチャット（討論グループ、ライブストリーミンググループ）のセッションタイプに対応しました
- テキスト、スタンプ、画像、音声、カスタムメッセージのメッセージタイプに対応しました
- APNsオフラインプッシュ（Token、フロント/バックエンドの切替イベントの報告）に対応しました
- メッセージのローカルストレージ

## IM Flutter SDK 0.0.1-1.0.2 @2020.12.01
- Flutter SDKをリリースしました
- ユーザーをベータ版テストに招待しました
