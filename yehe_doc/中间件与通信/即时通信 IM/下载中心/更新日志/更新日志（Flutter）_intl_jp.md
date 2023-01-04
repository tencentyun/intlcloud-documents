## プラットフォームの対応バージョン

FlutterのすべてのプラットフォームをサポートするIM SDKとTUIKitの構築に取り組み、1つのコードセットですべてのプラットフォームで実行することを支援します。

| プラットフォーム                                                         | UI SDK (tencent_im_sdk_plugin)なし | UIと基礎のビジネスロジックTUIKit (tim_ui_kit)を含む |
| ------------------------------------------------------------ | --------------------------------- | ---------------------------------------- |
| iOS                                                          | すべてのバージョンに対応                      | すべてのバージョンに対応                            |
| Android                                                      | すべてのバージョンに対応                      | すべてのバージョンに対応                             |
| [Web](https://intl.cloud.tencent.com/document/product/1047/45907) | 4.1.1+2とそれ以降のバージョンは対応可                 | 0.1.5とそれ以降のバージョンは対応可                          |
| [macOS](https://intl.cloud.tencent.com/document/product/1047/45907) | 4.1.8とそれ以降のバージョンは対応可                   | 間もなくリリースされます                                 |
| [Windows](https://intl.cloud.tencent.com/document/product/1047/45907) | 4.1.8とそれ以降のバージョンは対応可                   | 間もなくリリースされます                                 |

>? Web/macOS/Windowsプラットフォームでは、わずかなステップで簡単に導入できます。詳細については[Web互換性](https://intl.cloud.tencent.com/document/product/1047/45907)および[Desktop互換性(https://intl.cloud.tencent.com/document/product/1047/45907)]ガイドラインをご参照ください。

## ログの更新
>?
>
>- IM Flutter SDK（UIなし）は、[tencent_im_sdk_plugin](https://pub.dev/packages/tencent_im_sdk_plugin)パッケージを参照し、すべてのIMクライアントAPIとリスニングコールバックのみを含みます。
>- IM Flutter TUIKit（UIを含む）は[tim_ui_kit](https://pub.dev/packages/tim_ui_kit)パッケージを参照し、UI SDKがない場合は、完全なUIコンポーネントライブラリとビジネスロジックも含まれています。

## IM Flutter TUIKit 0.1.8 @2022.10.21

- 最適化：一度に複数のファイルメッセージをクリックできるファイル一括ダウンロードキュー。
- 最適化：グループリストウィジェットが自動的に更新されます。
- 最適化：カメラ撮影が性能の低いデバイスをサポートし、解像度を自動調整します。
- 最適化：特にTIMUIKitChatコンポーネントについて、アプリバーの色と文字スタイルのカスタマイズをサポートします。
- 修正：友達の備考またはニックネームがグループ紹介に表示されません。
- 修正：ビデオ再生のエラー。
- 修正：わずかのエラー。

## IM Flutter SDK 4.1.8 @2022.10.18
- 新規追加：macOSとWindowsを含むPCプラットフォームをサポートします。
- 新規追加：メッセージ拡張。
- 新規追加：シグナリングの編集。
- 最適化：下層SDKのアップグレード。
- 修正：高バージョンJDKの変換問題。
- 修正：わずかな問題。

## IM Flutter TUIKit 0.1.7 @2022.10.18
- 新規追加：大きな画像やRAW画像をサポートし、特に最新バージョンのiOSやiPhone 14 Proシリーズからキャプチャした画像について、自動送信前に圧縮・フォーマットを実行します。
- 最適化：特に履歴メッセージのリストと起動の性能と安定性。
- 最適化：' TIMUIKitChat 'の初期化を冪等処理とします。
- 最適化：一番下にスクロールしたときに最新のメッセージを読み込みます。
- 最適化：Flutter 2.xと3.xシリーズへのサポートを最適化しました。
- 修正：iOSアルバム、一部の画像だけの許可、権限へのサポート。
- 修正：わずかのbug。

## IM Flutter TUIKit 0.1.5 @2022.09.22
- 新規追加：Webへのサポート。現在、iOS/Android/WebプラットフォームでTUIKitを実装できます。
- 新規追加：ログイン後にディスクストレージをチェックし、`init`の`config`で制御します。
- 新規追加：`TIMUIKitChatConfig`に、`timeDividerConfig`、`notificationAndroidSound`HuaweiからGoogleへの音声設定のプッシュ、`isSupportMarkdown`テキストメッセージかMarkdownの解析をサポートするかどうか、`onTapLink`を追加しました。
- 削除：著作権の問題があるので、デフォルトのEmojiリスト。[tim_ui_kit_sticker_plugin](https://pub.dev/packages/tim_ui_kit_sticker_plugin)を使用して、TUIKitに自分の絵文字リストを提供できます。
- 最適化：ダイアログのリストに@メッセージを表示しないように選択できるようになりました。
- 最適化：`TIMUIKitChatConfig`と`MessageItemBuilder`から返された`notificationExt/notificationBody`は`null`であり、特定の条件では必要に応じてデフォルト値を使用することができます。つまり、コード内のTUIKitと同じロジックを再定義することなく、提供された条件に応じてカスタム設定を使用するかどうかを選択できます。
- 最適化：テキストメッセージの複数行をサポートします。
- 最適化：`TIMUIKitChat`に対する体験を改造および向上します。また、`TIMUIKitChatController`を使用するには、[チュートリアル](https://www.tencentcloud.com/document/product/1047/50054)で示したように、`controler`に渡す必要があります。

## IM Flutter SDK 4.1.3 @2022.09.21
- Web側の問題をいくつか解決しました。

## IM Flutter SDK 4.1.1+2 @2022.08.25
- 下層データベースのバージョンを6.6.xにアップグレードしました。
- Flutter Webへの完全対応になっています。

## IM Flutter SDK 4.1.0 @2022.08.09
- 下層データベースのバージョンをアップグレードしました。

## IM Flutter TUIKit 0.1.3 @2022.08.03
- ユーザーの入力中状態を追加しました。
- メッセージの絵文字応答能力を追加しました。
- ユーザーのオンライン状態表示を追加しました。

## IM Flutter SDK 4.0.8 @2022.07.25
- セッション・リストを取得するための拡張インタフェースを追加し、セッションの種類/ラベル、グループごとにセッションリストをプルできるようになりました。
- セッションのタグ付けをカスタマイズするインターフェースを追加しました。
- セッションのグループ化能力を追加しました。
- Dartバージョンの依存関係が2.0.0に減少させました。
- Flutterマルチエンジンをサポートします。
- Android側のオフラインでサウンド設定をプッシュことをサポートします。
- ユーザーのオンライン状態のカスタマイズをサポートします。
- 下層データベースのバージョンを6.5.xにアップグレードしました。

## IM Flutter TUIKit 0.1.2 @2022.07.08
- 元参照されていたサードパーティの下層レコーディングライブラリ`flutter_record_plugin_plus`が使用できない問題を修正しました。

## IM Flutter TUIKit 0.1.1 @2022.07.07
- 画像プレビューロジックを最適化しました。
- 各コンポーネントにライフサイクルフック関数LifeCycle hooksを追加しました。
- グループチャットページに発言禁止状態を追加しました。
- テキストメッセージ内のURLをクリックするとジャンプできるようになり、Webサイト情報のプレビューカードを追加しました。
- TUIKitレイヤーのグローバルイベントのコールバック（表示されるメッセージテキスト/Flutterレイヤーのエラー通知/IM APIレイヤーのエラー通知の返しを含む）を追加しました。またTUIKitではメッセージのポップアップ表示がなくなり、コールバックと通知メッセージに基づいてポップアップをカスタマイズできます。
- `TUIKitGroupProfile`グループ資料コンポーネントと`TUIKitProfile`ユーザ資料コンポーネントをリファクタリングし、使い方を簡素化し、超高速アクセスを実現できます。

## IM Flutter SDK 4.0.7 @2022.07.07
- iOSでカスタム添字をサポートします。
- グループ参加申請ロジックを最適化しました。

## IM Flutter SDK 4.0.6 @2022.07.04
- 下層データベースのバージョンを6.2.xにアップグレードしました。
- オフラインプッシュ情報フィールドを修正しました。

## IM Flutter SDK 4.0.5 @2022.07.01
- ユーザーのオンライン状態確認を追加しました。
- メッセージの種類による履歴メッセージリストのリクエストをサポートします。
- リッチテキストメッセージの送信をサポートします。

## IM Flutter TUIKit 0.1.0 @2022.06.10
- 各サブコンポーネントを用いてチャットページを独自に組み立てられるよう、`TIMUIKitChat`コンポーネントの原子化サービス開発能力を追加しました。
- メッセージ編集更新のUI能力をサポートします。
- グループ参加申請審査ページコンポーネントを追加しました。
- 国際化言語に繁体字中国語を追加しました。
- より多くのカスタムコンポーネントパラメータをオープンしました。

## IM Flutter TUIKit 0.0.9 @2022.05.30
- [tim_ui_kit_push_plugin](https://pub.dev/packages/tim_ui_kit_push_plugin)プッシュプラグインの新リリースに合わせるよう、オフラインプッシュをサポートします。
- Flutter 3.0をサポートします。
- メディアメッセージのローカルプレビューを最適化しました。

## IM Flutter SDK 4.0.2 @2022.05.27
- ローカルビデオパスを修正しました。

## IM Flutter SDK 4.0.1 @2022.05.23
- トピック作成能力を追加しました。
- メッセージ編集能力を追加しました。

## IM Flutter SDK 4.0.0 @2022.04.26
- 下層データベースのバージョンを6.2.xにアップグレードしました。
- オフラインプッシュ情報フィールドを修正しました。

## IM Flutter TUIKit 0.0.8 @2022.04.24
- グループメッセージの既読通知能力を追加しました。
- 新しいチャット領域の右下に小さな舌を追加し、一番下に戻る/新しいメッセージの数を表示する/@メッセージ通知をサポートします。

## IM Flutter SDK 3.9.3 @2022.4.20
- 発言禁止のグループのtips boolValueが失われたという問題を修正しました。
 - 現在、グループ情報変更のコールバックによって返されるデータは、key(string)-value(string)の形式であり、key(string)-boolValue(bool)の形式が新しく追加されています。
- セッションインスタンスでnameCardフィールドが解析されていないという問題を修正しました。
- グループ開封確認関連のインターフェースを追加しました。
 - [sendMessageReadReceptes](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/sendMessageReadReceipts.html)では、グループメッセージの開封確認を送信できるようになりました。
 - [getMessageReadReceptes](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/getMessageReadReceipts.html)では、自分から送信したメッセージの開封確認を取得できるようになりました。
 - [getgroupMessageReadMemeberList](https://comm.qq.com/en_doc_site/flutter/api/manager_v2_tim_message_manager/V2TIMMessageManager/getGroupMessageReadMemberList.html)では、自分から送信したグループメッセージの既読（未読）グループメンバーリストを取得できるようになりました。
- Flutter for Webを最適化しました。

## IM Flutter SDK 3.9.1 @2022.3.24
- 下層データベースのバージョンを6.1.2155にアップグレードします。

## IM Flutter SDK 3.9.0 @2022.3.22
- grouplistenerを修正します。

## IM Flutter SDK 3.8.9 @2022.3.18
- リッスンと登録の問題を修正します。

## IM Flutter SDK 3.8.4 @2022.3.14
- interfaceを更新します。

## IM Flutter SDK 3.8.3 @2022.3.1
- 環境に応じてtokenエンコーディングを切り替えます

## IM Flutter SDK 3.8.2 @2022.2.21
- グループメンバーパラメータの制約を更新します。

## IM Flutter SDK 3.8.0 @2022.2.17
- 下層interfaceの依存関係をアップグレードします。

## IM Flutter SDK 3.7.8 @2022.2.15
- 強制解凍により引き起こされる異常を修正します。

## IM Flutter SDK 3.7.7 @2022.2.10
- Swiftコードwarningを修正します。
- Swiftの強制解凍コードを書き直します。
- sendMessageインターフェースにより返されるmessageインスタンスにidフィールドを追加します。


## IM Flutter SDK 3.7.5 @2022.01.23
- 下層データベースを6.0.1975にアップグレードしました。
- オフラインプッシュの設定でTPNS TOKENをサポートしました。


## IM Flutter SDK 3.7.1 @2022.01.12
- メッセージ送信プログレスイベントで作成したメッセージのidを戻すようにしました。
- コールバック部分を最適化し、サービス側にコールバックのエラーがSDK中でcatchされ、サービス側に修正の必要があることを通知するようにしました。

## IM Flutter SDK 3.7.0 @2022.01.10
- CloudCustomDataアンパックを最適化しました。


## IM Flutter SDK 3.6.9 @2022.01.06
- 返信メッセージパラメータを最適化しました。


## IM Flutter SDK 3.6.8 @2022.01.06
- 返信メッセージインターフェースを最適化しました。


## IM Flutter SDK 3.6.7 @2022.01.05
- iOSコンパイル環境を8.0から9.0にアップデートしました。


## IM Flutter SDK 3.6.6 @2021.12.30
- メッセージに返信インターフェースを追加しました。
- Web端末のrelease modeでのエラー問題を修正しました。


## IM Flutter SDK 3.6.5 @2021.12.17
- java文法エラーを修正しました。

## IM Flutter SDK 3.6.4  @2021.12.17
- Androidの非同期登録イベントが何も返されないbugを修正しました。
- 基礎監視イベントが削除されるエラーを修正しました。
- メッセージプログレスイベントに送信中のメッセージのuuidを追加しました。

## IM Flutter SDK 3.6.3 @2021.12.9
- addFriendインターフェースの最適化：addTypeをintからFriendTypeEnumに変更しました。
- acceptFriendApplicationインターフェースの最適化：acceptTypeをintからFriendResponseTypeEnumに変更しました。
- checkFriendインターフェースの最適化：checkTypeをintからFriendTypeEnumに変更しました。
- createGroupインターフェースの最適化：addOptをintからGroupAddOptTypeEnumに変更しました。
- deleteFromFriendListインターフェースの最適化：deleteTypeをintからFriendTypeEnumに変更しました。
- getGroupMemberListインターフェースの最適化：filterをintからGroupMemberFilterTypeEnumに変更しました。
- getHistoryMessageListインターフェースの最適化：typeをintからHistoryMsgGetTypeEnumに変更しました。
- getHistoryMessageListWithoutFormatインターフェースの最適化：typeをintからHistoryMsgGetTypeEnumに変更しました。
- getGroupMemberListインターフェースの最適化：typeをintからGroupMemberFilterTypeEnumに変更しました。
- getGroupMemberListインターフェースの最適化：filterをintからGroupMemberFilterTypeEnumに変更しました。
- initSDKインターフェースの最適化：loglevelをintからLogLevelEnumに変更しました。
- refuseFriendApplicationインターフェースの最適化：acceptTypeをintからFriendApplicationTypeEnumに変更しました。
- sendCustomMessageインターフェースの最適化：priorityをintからMessagePriorityEnumに変更しました。
- sendFaceMessageインターフェースの最適化：priorityをintからMessagePriorityEnumに変更しました。
- sendFileMessageインターフェースの最適化：priorityをintからMessagePriorityEnumに変更しました。
- sendForwardMessageインターフェースの最適化：priorityをintからMessagePriorityEnumに変更しました。
- sendImageMessageインターフェースの最適化：priorityをintからMessagePriorityEnumに変更しました。
- sendLocationMessageインターフェースの最適化：priorityをintからMessagePriorityEnumに変更しました。
- sendMergerMessageインターフェースの最適化：priorityをintからMessagePriorityEnumに変更しました。
- sendSoundMessageインターフェースの最適化：priorityをintからMessagePriorityEnumに変更しました。
- sendTextAtMessageインターフェースの最適化：priorityをintからMessagePriorityEnumに変更しました。
- sendTextMessageインターフェースの最適化：priorityをintからMessagePriorityEnumに変更しました。
- setGroupMemberRoleインターフェースの最適化：roleをintからGroupMemberRoleTypeEnumに変更しました。
- イベントコールバック登録の戻り値を非同期に修正しました。

## IM Flutter SDK 3.6.2 @2021.12.9
- 高度なメッセージが削除されuuidが渡されないエラーを修正しました。


## IM Flutter SDK 3.6.1 @2021.12.8
- ファイルのプログレスイベントが消失する問題を修正しました。


## IM Flutter SDK 3.6.0 @2021.12.1
- 各モジュールでlistenerの複数登録、複数コールバックをサポートしました。
- すべてのセッションを既読に設定するapi markAllMessageAsReadを追加しました。
- 組み合わせメッセージ解析を追加しました。
- nativeのバージョンを5.8.1668にアップデートしました。


## IM Flutter SDK 3.5.6 @2021.11.25
- checkFriendが失敗する問題を修正しました。
- getC2CHistoryMessageListが後続のメッセージを獲得できない問題を修正しました。

## IM Flutter SDK 3.5.5 @2021.11.23
- アーキテクチャを調整しました。


## IM Flutter SDK 3.5.4 @2021.11.22
- downloadMergeMesasgeインターフェースを追加しました。


## IM Flutter SDK 3.5.3 @2021.11.15
- onTotalUnreadMessageCountChangedイベントを追加しました。
- セッションの並び替えのためにV2TimConversationにorderkeyフィールドを追加しました。


## IM Flutter SDK 3.5.2 @2021.11.12
add web support

## IM Flutter SDK 3.5.1 @2021.11.10
- 配列の許容外ロジックに対応しました。


## IM Flutter SDK 3.5.0 @2021.10.1
- いくつかの既知の問題を修正しました。
- 次のインターフェースを追加しました。
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
- iOSの履歴メッセージ獲得エラーを修正しました。

## IM Flutter SDK 1.0.33 @2021.03.22
- sdkのminSdkVersionを16に修正しました。

## IM Flutter SDK 1.0.32 @2021.03.22
- セッション情報のlastMessageが空のときcrashする問題を修正しました。

## IM Flutter SDK 1.0.30-1.0.31 @2021.03.18
- カスタムメッセージのdataフィールドがnullのときcrashする問題を修正しました。

## IM Flutter SDK 1.0.29 @2021.03.16
- 【重要】グループメンバーリスト獲得時のパラメータ渡しのエラーを修正しました。

## IM Flutter SDK 1.0.28 @2021.03.16
- 【重要】checkFriendsインターフェースの入力パラメータを変更しました。

## IM Flutter SDK 1.0.15-1.0.27 @2021.03.15
- グループメンバーカスタムフィールドを追加しました。
- iOSシグナリングを改善しました。
- iOSシグナリングbugを修正しました。
- カスタムフィールドを解析してStringにして戻すようにしました。
- パーソナルカスタムフィールドの設定を最適化しました。
- Android getHistoryMessageListを更新しました。
- Android端末のcheckFriendのパラメータ渡しエラーを修正しました。

## IM Flutter SDK 1.0.5-1.0.14 @2021.02.26
- deleteFriendApplicationのパラメータ渡しエラーを修正しました。
- native sdkを5.1.132に更新しました。
- native sdkを5.1.137に更新しました。
- シグナル招待インターフェースのパラメータ渡しのbugを修正しました。
- シグナルインターフェースがidを戻さない問題を修正しました。
- sdkの圧縮設定を修正しました。
- シグナリングのコールバックのbugを修正しました。
- カスタムメッセージの戻しデータを修正しました。
- 【重要】シグナリングメッセージの戻す内容のフォーマットを修正したため、シグナリングを使用する場合はこのバージョンおよびそれ以降のバージョンに更新してください


## IM Flutter SDK 1.0.4 @2021.01.14

- Android端末のSDKバージョンを5.1.129に更新しました。
- iOS端末のSDKバージョンを5.1.129に更新しました。

## IM Flutter SDK 1.0.3 @2021.01.13
- Android/iOSマルチプラットフォームに対応しました。
- シングルチャット、グループチャット（討論グループ、ライブストリーミンググループ）のセッションタイプに対応しました。
- テキスト、スタンプ、画像、音声、カスタムメッセージのメッセージタイプに対応しました。
- APNsオフラインプッシュ（Token、フロント/バックエンドの切替イベントの報告）に対応しました。
- メッセージのローカルストレージ

## IM Flutter SDK 0.0.1-1.0.2 @2020.12.01
- Flutter SDKをリリースしました。
- ユーザーをベータ版テストに招待しました。
