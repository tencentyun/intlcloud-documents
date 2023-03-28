### 2.26.1 @2023.2.10

**修正**

- グループ履歴メッセージの最新のメッセージがグループメッセージ通知のシナリオで表示されます。グループセッションのlastMessage.lastTimeが正しくありません。
- [markConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#markConversation)インターフェースを呼び出してセッションタグを設定しましたが、再ログイン後にタグの内容が失われました。
- [createGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createGroup)インターフェースを呼び出してグループを作成したときに、たまにグループ情報を確認できませんでした。
- [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList)インターフェースを呼び出して履歴メッセージをプルしますが、一部のシナリオで履歴メッセージが表示されません。

### 2.26.0 @2023.1.13

**追加**

- [translateText](https://web.sdk.qcloud.com/im/doc/en/SDK.html#translateText)インターフェースで、テキストの翻訳をサポートします。
- [setGroupCounters](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupCounters)インターフェースで、グループカウンタの設定をサポートします。アクセス側はこのインターフェースにより、「いいね」カウント、ライブ配信グループプレゼントカウント、視聴者数カウントなど、よく使われるカウント機能を実現できます。
- [increaseGroupCounter](https://web.sdk.qcloud.com/im/doc/en/SDK.html#increaseGroupCounter)インターフェースで、グループカウンタをインクリメントします。
- [decreaseGroupCounter](https://web.sdk.qcloud.com/im/doc/en/SDK.html#decreaseGroupCounter)インターフェースで、グループカウンタをデクリメントします。
- [getGroupCounters](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupCounters)インターフェースで、グループカウンタを取得します。
- グループメッセージのプルを取り消すシグナリングをサポートし、弱いネットワークの下でグループメッセージが取り消された状態の正確性を向上させます。
- [Message](https://web.sdk.qcloud.com/im/doc/en/Message.html)に`revoker`のフィールドを追加しました。このフィールドはメッセージを取り消した者の`userID`を示します。

**修正**

- サイトをまたがって購入されたセグメントは国際サイトとして認識されません。
- ログインログに表示されるuserIDエラーが繰り返します。


### 2.25.0 @2022.12.8

**追加**

- [clearHistoryMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#clearHistoryMessage)インターフェースは、ローカルメッセージおよびクラウドメッセージのクリアをサポートします。
- メッセージの拡張をサポートします（Ultimate Edition機能）。
- 共通グループおよびコミュニティグループの属性をサポートします。
- [wx.chooseMedia](https://developers.weixin.qq.com/miniprogram/dev/api/media/video/wx.chooseMedia.html)と互換性があります。
- [Message.readReceiptInfo](https://web.sdk.qcloud.com/im/doc/en/Message.html)は、C2Cの開封確認（NativeIMに合わせたデータ構造）をサポートします。
- エラーコード2101：ライブブロードキャストグループに参加していない場合は、ライブブロードキャストグループにメッセージを送信することはできません。

**変更**

- ログが報告したバックアップチャネルは、独立したクラスタードメイン名`https://events.im.qcloud.com`を使用します（信頼できるドメイン名構成を追加する必要があります）。

**修正**

- cookies blockedによる実行エラー（Failed to read the 'localStorage' property from 'Window': Access is denied for this document）。


### 2.24.1 @2022.11.11

**追加**

- 英語版のts宣言ファイル。
- RESTAPIで変更された友達のカスタムデータフィールドはSDKへのプッシュをサポートします。

**修正**

- [getMessageListHopping](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageListHopping)、一部のシナリオで異常な結果が返される問題。

### 2.24.0 @2022.11.3

**追加**

- ミニゲーム環境の統合をサポートします。
- ローカルの検証プラグイン[tim-profanity-filter-plugin](https://www.npmjs.com/package/tim-profanity-filter-plugin)でローカルの検証機能をサポートします。
- [getFriendProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendProfile)はデフォルトで、友達のカスタムフィールドと資料のカスタムフィールドをプルし、製品のエクスペリエンスを向上させます。
- [getGroupApplicationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupApplicationList)はグループ参加リストをすべてプルすることをサポートします。
- RESTAPIで変更された友達のカスタムフィールドはSDKへのプッシュをサポートします。
- 未読としてカウントされないトピックメッセージの送信をサポートします。
- 未読としてカウントされない通常のコミュニティメッセージの送信をサポートします。
- メッセージ送信がvoip pushをサポートします。

**修正**

- 友達データに関する問題。


### 2.23.1 @2022.9.29

**追加**

- [createTextMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTextMessage)などのインターフェースはグループ指向メッセージの作成をサポートします（メッセージは指定されたグループメンバーに送信される）。
- mov形式のビデオの送信をサポートします。
- REST APIの[友達の更新](https://intl.cloud.tencent.com/document/product/1047/34904)はSDKへのプッシュをサポートします。
- [getFriendProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendProfile)はカスタム友達フィールドとカスタム資料フィールドのプルをサポートします。
- [getConversationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationList)インターフェースから返されたデータに新しいフィールドisSyncCompletedを追加しました。クラウドからのセッションリストの同期が完了したかどうかを示すために使用されます。
- トピックが属するコミュニティメッセージが[MESSAGE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_RECEIVED)イベントを用いて導入側に通知することをサポートします。

**修正**

- グループリストが上限5000を超えた後、一部のグループセッションがローミングメッセージをプルことができない問題。
- setConversationCustomDataを呼び出してセッションのカスタムフィールドを設定した後に再ログインするとセッションのcustomDataが''になる問題。

### 2.23.0 @2022.9.16

**追加**

- SDKは、中国本土以外の環境をサポートします。
- [getTotalUnreadMessageCount](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getTotalUnreadMessageCount)はセッション未読総数の取得をサポートします。
- [TOTAL_UNREAD_MESSAGE_COUNT_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.TOTAL_UNREAD_MESSAGE_COUNT_UPDATED)、導入側がこのイベントをリスニングするとセッション未読合計数の変更の通知を取得できます。
- ライブストリーミンググループのグループメンバをタグつける[markGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#markGroupMemberList)。
- グループメンバーがグループから追放されるか、グループが解散されると、SDKがこのグループセッションが存在するセッションのサブグループを同期的に更新しました。
- 独立したパッケージングをサポートします。
- Webマルチインスタンスのサインオンシーンで、ネットワークが切断されて再接続された後、SDKが最近使用した連絡先のメッセージ履歴を自動で回復し、メッセージの信頼性を保証します。

**修正**

- Webマルチインスタンスのサインオンシーンで発生する可能性のあるセッションlastMessageの撤回状態の非同期問題。
- 最近使用した連絡先を同期するときのセッションのトップ表示問題。

### 2.22.0 @2022.8.18

**追加**

- uni-appでnative appへのパッケージ化時にオフライン配信を使用することをサポートします。[registerPlugin](https://web.sdk.qcloud.com/im/doc/en/SDK.html#registerPlugin)をご参照ください。
- ライブストリーミンググループのオンラインメンバーリストを取得することをサポートします。[getGroupMemberList ](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberList)（Ultimate Editionが必要）をご参照ください。
- ライブストリーミンググループのメンバーブロックをサポートします。[deleteGroupMember](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteGroupMember)（Ultimate Editionが必要）をご参照ください。
- セッションのカスタムデータを設定する[setConversationCustomData](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setConversationCustomData)。
- セッションをタグつける[markConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#markConversation)（Ultimate Editionが必要）。
- セッションのサブグループリストを取得する[getConversationGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationGroupList)（Ultimate Editionが必要）。
- セッションのサブグループを作成する[createConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createConversationGroup)（Ultimate Editionが必要）。
- セッショングループを削除する[createConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversationGroup)（Ultimate Editionが必要）。
- セッションのサブグループをリネームするする[renameConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#renameConversationGroup)（Ultimate Editionが必要）。
- セッションをセッションのサブグループに追加する[addConversationsToGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addConversationsToGroup)（Ultimate Editionが必要）。
- セッションのサブグループからセッションを削除する[deleteConversationsFromGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversationsFromGroup)（Ultimate Editionが必要）。

**修正**

- トピックメッセージが撤回されたとの通知を受けてもトピックの未読数が更新されない問題。

### 2.21.2 @2022.8.8

**追加**

- Web側での音声メッセージの作成と送信をサポートします。
- IDフィールドを追加したマージメッセージを作成する[createMergerMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createMergerMessage)。

### 2.21.1 @2022.8.3

**修正**

[resendMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#resendMessage)によるメッセージ重複問題。

### 2.21.0 @2022.7.28

**追加**

- 自分のカスタマイズ状態を設定する[setSelfStatus](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setSelfStatus)。
- ユーザー状態を取得する[getUserStatus](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getUserStatus)。
- ユーザーの状態をサブスクリプションする[subscribeUserStatus](https://web.sdk.qcloud.com/im/doc/en/SDK.html#subscribeUserStatus)。
- ユーザーの状態のサブスクリプションを解除する[unsubscribeUserStatus](https://web.sdk.qcloud.com/im/doc/en/SDK.html#unsubscribeUserStatus)。
- グループメッセージやトピックメッセージの通知オフ設定を多端末と多インスタンスで同期する[setMessageRemindType](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setMessageRemindType)。
- すべてのタイプのメッセージのcloudCustomDataの変更をサポートする[modifyMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#modifyMessage)。
- ライブストリーミンググループでメッセージをブロードキャストするため、[Message](https://web.sdk.qcloud.com/im/doc/en/Message.html)の新しいフィールドisBroadcastMessageを追加しました。
- グループ参加オプションのマルチ端末とマルチインスタンス同期をサポートします。
- 一般コミュニティとトピックの@全員およびトピックlastMessageをサポートします。

**変更**

- webworker対応のブラウザの国際サイトとプライベート環境でwebworkerがデフォルトでが有効になります。

**修正**

- セッションlastMessageを更新しないメッセージを受信した後、lastMessage.payloadがundefinedに設定される問題。
- オンラインメッセージが原因でグループメッセージの補償が開始されない問題。
- 頻繁にグループ脱退・グループ参加後にグループのローミングメッセージをプルすると異常が発生する問題。
- ページごとにグループリストのプルが遅れて、プルしたグループセッションのローミングメッセージが空の配列になるという問題。
- トピックが既知である問題。

### 2.20.1 @2022.6.27

**変更**

- 非ライブ配信グループを終了するか非ライブ配信グループから削除される、または非ライブ配信グループが解散されると、グループ履歴のみが削除され、対応するグループセッションは削除されません。nativeに合わせて同じような体験が提供されます。
- [deleteMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage)は、グループシステム通知の削除をサポートしていません。また、具体的なエラーメッセージが返されます。
- プライベートにデプロイされたリッチメディアメッセージはHTTPプロトコルをサポートするようになりました。

**修正**

- フォアグラウンドとバックグラウンドを切り替えるなどのシナリオで、グループセッションが失われるという偶発的な問題。
- C2CセッションのlastMessageが異常に更新されるという問題。

### 2.20.0 @2022.6.9

**追加**

- [modifyMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#modifyMessage)は、メッセージの変更をサポートするようになりました。
- [getMessageListHopping](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageListHopping)は、指定されたメッセージsequenceまたはメッセージ時間によってセッションのメッセージリストをプルすることをサポートするようになりました。
- 単一または複数のC2Cメッセージの開封確認の送信をサポートするようになりました（Ultimate Editionを有効化する必要があります）。
- C2CセッションlastMessageで、対向側がメッセージを開封したかどうかを識別するために使用されるフィールドisPeerReadを追加しました。
- グループの通知メッセージを未読セッションとしてカウントされないことをサポートするようになりました。
- [TIM.TYPES.KICKED_OUT_REST_API](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.KICKED_OUT_REST_API)タイプを追加し、REST API [kick](https://intl.cloud.tencent.com/document/product/1047/34957)をサポートします。

**変更**

- [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList)によるローミングメッセージのプル体験を改善、最適化しました。

**修正**

- パラメータを渡すときに発生する問題により、[deleteMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage)完了後にセッションリストが更新されないというエラー。
- 一部のモデルで、実際のデバイスでデバッグするときに発生する`Cannot add property markTimeline, Object is not extensible`という問題。

### 2.19.1 @2022.5.7

**追加**

- [コミュニティ(Community)](https://intl.cloud.tencent.com/document/product/1047/33529)の下でのトピックの作成をサポートし、よりインタラクティブなシナリオをサポートするようになりました。
- [getJoinedCommunityList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getJoinedCommunityList)では、トピックをサポートするコミュニティのリストを取得できるようになりました。
- [createTopicInCommunity](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTopicInCommunity)では、トピックを作成できるようになりました。
- [deleteTopicFromCommunity](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteTopicFromCommunity)では、トピックを削除できるようになりました。
[updateTopicProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateTopicProfile)では、トピックデータを設定できるようになりました。
- [getTopicList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getTopicList)では、トピックリストを取得できるようになりました。
- [Topic](https://web.sdk.qcloud.com/im/doc/en/Topic.html)：コミュニティのトピック対象であり、名称、お知らせ、概要、未読数などの情報を含むトピックのプロパティを説明するためのものです。
- イベント[TIM.EVENT.TOPIC_CREATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.TOPIC_CREATED)は、トピックの作成時にトリガーされます。
- イベント[TIM.EVENT.TOPIC_DELETED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.TOPIC_DELETED)は、トピックの削除時にトリガーされます。
- イベント[TIM.EVENT.TOPIC_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.TOPIC_UPDATED)は、トピックデータの更新時にトリガーされます。

### 2.18.2 @2022.4.22

**変更**

ライブ配信グループのユーザー体験を最適化しました。

**修正**

- 一部のシナリオにおいて統計が正確ではないという問題。
- インターフェース[getGroupMessageReadMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMessageReadMemberList)を呼び出した後、戻った結果が正しくないという問題。

### 2.18.0 @2022.4.8

**追加**

- [sendMessageReadReceipt](https://web.sdk.qcloud.com/im/doc/en/SDK.html#sendMessageReadReceipt)で、グループメッセージの開封確認を送信します。
- [getMessageReadReceiptList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageReadReceiptList)で、グループメッセージの開封確認リストをプルします。
- [getGroupMessageReadMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMessageReadMemberList)で、グループメンバーのグループメッセージの既読（または未読）リストをプルします。
- [findMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#findMessage)で、messageIDに基づいてセッションのローカルメッセージを照会します。
- メッセージが取り消された後、セッションの未読数の変更エクスペリエンスはNativeIMと調整されます。

**変更**

- [Message.ID](https://web.sdk.qcloud.com/im/doc/en/Message.html)スプライシングルールは`${senderTinyID}-${clientTime}-${random}`であり、NativeIMメッセージIDのスプライシングルールと一致します。
- SDK not readyのとき、アクセス側が使用しやすくするために、具体的な原因を表示します。

**修正**

グループメンバーがキックアウトされた後、他のグループメンバーが[CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED)イベントコールバックから取得した`Conversation.groupProfile.memberCount`値は更新されていない問題。

### 2.17.0 @2022.3.2

**追加**

- [Community](https://intl.cloud.tencent.com/document/product/1047/33529)をサポートしました。
- 最近の連絡先`Conversation.lastMessage`は、グループプロンプトメッセージをサポートしました。
- `Message.payload.memberList`は、グループ参加またはグループ退出のグループメンバーのニックネーム、プロファイルフォトなどの情報の取得をサポートしました。
- 画像メッセージの送信は、webp形式の画像をサポートしました。
- ビデオメッセージの送信は、ビデオカバー[snapshotUrl](https://web.sdk.qcloud.com/im/doc/en/Message.html#.VideoPayload)をサポートしました。
- メッセージの転送効率、スロットリング[CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED)などのイベントを最適化しました。

**修正**

- カスタムデータ（cloudCustomData）を含むメッセージが送信された後、再ログインすると、cloudCustomDataが空になるという問題。
- [login](https://web.sdk.qcloud.com/im/doc/en/SDK.html#login)に失敗した後、再ログインすると、「再ログインしないでください」という問題。
- [getGroupProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupProfile)後、`Conversation.groupProfile`は最新のグループプロファイルと一致しないという問題。

### 2.16.3 @2022.2.11

**修正**

Android app（一部のデバイス）をパッケージ化するuni-appをWindowsでアクセスする場合、ログインできないという問題。

### 2.16.2 @2022.2.10

**追加**

- uni-appがnative appをパッケージ化した後にファイルメッセージを送信することをサポートしました。
- インドのグローバルサイトをサポートしました。

**修正**

- 一部のemojiレンダリングの問題。

### 2.16.1 @2022.1.14

**追加**

- Alipayが.imageサフィックスが付いた画像を送信することをサポートしました。
- セッション[deleteConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversation)を削除すると同時に、履歴メッセージを削除します。

**修正**

- ダウンリンクのファイルメッセージ`fileName`が空の文字列であることによるエラー。
- グループ属性インターフェース呼び出しのタイミングによって引き起こされる問題。
- uni-appがBaiduなどのプラットフォームにパッケージ化されるときに発生する`__wxConfig is not defined`という問題。

### 2.16.0 @2022.1.5

**追加**

- [setMessageRemindType](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setMessageRemindType)で、C2Cセッションメッセージの設定をサポートしました。
- [setAllMessageRead](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setAllMessageRead)で、ワンクリックですべての未読セッションをクリアすることをサポートしました。
- [sendMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#sendMessage)で、未読セッションとしてカウントされず、セッションを更新しない`lastMessage`のメッセージの送信をサポートしました。
- ライブブロードキャストグループの新しいメンバーがグループに参加する前の履歴メッセージを確認することをサポートしました（フラッグシップ版を有効にしてください）。

**変更**

- SDKが[厳格モード](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Strict_mode)を使用します。
- セッションリストは、削除されたアカウントとのセッションをフィルタリングします。
- ローミングメッセージの`nick`と`avatar`の更新タイミングを最適化しました。
- 相手側（フレンド）のプロファイル更新を受け取った後、対応して`conversation.userProfile`を更新しました。

**修正**

- UTF-8以外の文字によるロングコネクションの異常な切断の問題。
- [deleteMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage)のときにコピーのメッセージの着信によって発生する実行エラー：`e.getOnlineOnlyFlag is not a function`。
- [deleteMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage)の後、セッション`lastMessage`が正しく更新されない問題。
- C2Cセッションの未読カウントの問題。
- `nick`と`avatar`のないC2Cセッションのリアルタイムメッセージによって引き起こされたメッセージレンダリング異常。
- セッション`lastMessage.payload`が`null`であることがある問題。
- 事前に署名されたアップロード画像のサムネイルURLが機能しない問題。
- @グループメンバー、再ログインした後にローミングメッセージをプルすると、対応するmessage.atUserListは空の配列である問題。
- グループプロンプトメッセージ（グループマスターの転送）の処理中にエラーが発生する問題。
- いくつかの統計エラー。

### 2.15.0 @2021.10.29

**追加**

- グローバルサイトをサポートしました。
- [createLocationMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createLocationMessage)で、地理的位置のメッセージ送信をサポートしました。
- 画像、ビデオ、ファイルなどをファイルタイプでアップロードし、ダウンロードとプレビューが簡単で、uniappと互換性があります。
- [Conversation](https://web.sdk.qcloud.com/im/doc/en/Conversation.html) `lastMessage`データ構造に、グループチャットセッション`lastMessage`の送信者の情報を表示するための`nick` `nameCard`フィールドを追加しました。

**変更**

- [getConversationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationList)で、指定されたセッションの一括取得をサポートしました。
- ロングコネクションの安定性を向上させました。

**修正**

- セッションリストのキャッシュ、最近の連絡先のページネーションがない場合、ログインすると、イベント[CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED)が配信されない問題。
- 一部のシーンでは、[getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList)が`isCompleted`を常に`false`に返す問題。
- [createFaceMessage](createFaceMessage)が`index`を0に設定すると、受信側は`index`フィールドを失う問題。

### 2.14.0 @2021.9.24

**追加**

- [pinConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#pinConversation)で、セッションをトップにすることをサポートしました。
- [initGroupAttributes](https://web.sdk.qcloud.com/im/doc/en/SDK.html#initGroupAttributes)などのグループ属性関連インターフェース。TRTCチャットルームでのマイク位置管理をサポートしました。

**変更**

- アクセス側で表示するために、グループチャットメッセージを送信する場合、メッセージ本文の`nameCard`属性を自動的に補完します。
- マルチ端末へのログインまたはマルチインスタンスへのログインのためにキックアウトされた場合、サーバー側のlogoutコールバックはトリガーされなくなりました。

**修正**

- C2Cセッションがローミングメッセージをプルするとき、メッセージを失うことがある問題。
- グループ参加の追記（applyMessage）がない問題。

### 2.13.1 @2021.8.27

**変更**

- ログインしていないときに、[login](https://web.sdk.qcloud.com/im/doc/en/SDK.html#login)を連続的に呼び出すと、【繰り返しログイン】を示すエラーコード`2025`が返されます。
- WebSocket再接続後、SDKは再ログインして未読メッセージを同期し、メッセージの信頼性を確保します。

**修正**

- ログインしていないときに、[login](https://web.sdk.qcloud.com/im/doc/en/SDK.html#login)を連続的に呼び出すときの未読数のエラー。
- [setGroupMemberNameCard](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupMemberNameCard)インターフェースを呼び出すときに、`nameCard`に空の文字列が渡された後に報告されるエラー。
- [getGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberList)インターフェースを呼び出したときに、返されたデータ`muteUntil`の値のエラー。

### 2.13.0 @2021.8.23

**追加**

フレンドシップチェーンをサポートします。[利用ガイド](https://web.sdk.qcloud.com/im/doc/en/tutorial-03-sns.html)をご参照ください。

**修正**

WebSocketロングコネクション切断時の偶発的なエラー。

### 2.12.2 @2021.8.6

**追加**

ビデオのアップロードは進行状況のコールバックをサポートしました。

**変更**

ローミングに存在しないグループカスタムフィールドなどのグループプロンプトメッセージを変更するとき、SDKはセッションの未読をカウントしなくなります。

**修正**

- ライブブロードキャストグループに参加しましたが、グループに参加したというプロンプトメッセージを受信できないことがある問題。
- restapiでc2cメッセージを送信し、randomを0に設定するとき、受信側が[MESSAGE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_RECEIVED)イベントを2回トリガーする問題。

### 2.12.1 @2021.7.20

**追加**

- Meetingグループの未読数をサポートしました。
- [TIM.EVENT.MESSAGE_MODIFIED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_MODIFIED)イベント、サードパーティが変更されたメッセージをコールバックし、SDKはこのイベントを通じてメッセージ送信側に通知します。

**修正**

- グループローミングメッセージをプルするとき、メッセージを失うことがある問題。
- uni-app統合中に発生する可能性のある`xx.toFixed is not a function`。

### 2.12.0 @2021.7.5

**追加**

- [deleteMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage)で、メッセージの削除をサポートしました。
- セッションリストを同期するときに、`lastMessage`が取り消されたメッセージであるケースをサポートしました。
- [getGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberList)で、`joinTime`（グループへの参加時間）のプルをサポートしました。

**修正**
adminの設定およびadminのキャンセル後、グループプロンプトメッセージの`nick`エラー。

### 2.11.2 @2021.6.16

**追加**

- WebSocket、[アップグレードガイド](https://web.sdk.qcloud.com/im/doc/en/tutorial-02-upgradeguideline.html)をサポートしました。
- uni-appが画像、ビデオなどのファイルメッセージを送信することをサポートしました。

### 2.10.2 @2021.4.27

**追加**

- メッセージの作成は、より様々なサービスニーズを満たすための`cloudCustomData`（カスタムフィールド）の設定をサポートしました。
- [createGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createGroup)または[addGroupMember](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addGroupMember)のときに、「1人のユーザーのグループ参加可能な最大数」を超えたユーザーがが存在する場合、`overLimitUserIDList`を介してアクセス側に通知します。

**修正**

- [コンソール](https://console.cloud.tencent.com/im)でAVチャットルーム（AVChatRoom）を作成し、グループマスターを指定します。グループマスターがグループに参加した後、[SendSystemNotification](https://intl.cloud.tencent.com/document/product/1047/34958)のREST APIを呼び出して、グループマスターがグループシステム通知を繰り返し受信する問題。
- [createForwardMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createForwardMessage)で、ニックネームを失う問題。
- [downloadMergerMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#downloadMergerMessage)で、偶発的なエラー。

### 2.10.1 @2021.3.19

**追加**

- [createMergerMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createMergerMessage)インターフェース。統合メッセージを作成します。
- [createForwardMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createForwardMessage)インターフェース。転送メッセージを作成します。
- マルチインスタンスまたはマルチ端末でログインした場合、1つの端末が既読を報告すると、同一セッションのWeb端末の未読数が同期され、0になります。

**変更**

MTA統計を廃棄しました。

**修正**

- Web・マルチインスタンスログインで、C2Cセッションの相手側のプロフィール画像とニックネームにエラーが発生する問題。
- メッセージ送信後のコールバックを登録し、かつREST APIを呼び出して頻繁にメッセージを取り消すシーンにおいて、一部メッセージが正しく取り消されない問題。

### 2.9.3 @2021.2.3

**変更**

ユーザーがグループ（ライブブロードキャストグループ以外）に参加していません。[quitGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#quitGroup)のときは、エラーコード2623（ユーザーが当該グループ内に存在しません）が返されます。

**修正**

C2Cセッションメッセージリストの`avatar`（プロフィール画像）または`nick`（ニックネーム）が一致しない問題。

### 2.9.2 @2021.1.26

**追加**

- C2Cメッセージの送受信に`avatar`（プロフィール画像）と`nick`（ニックネーム）が添付されます。
- Tencent Cloud IMのアップロードプラグイン[tim-upload-plugin](https://www.npmjs.com/package/tim-upload-plugin)をサポートするようになりました。ファイルのアップロードがより速く、より安全になります。Web版、Baidu（百度）、Toutiao（頭条）に対応し、容量はわずか26KBです。利用方法の詳細については、[registerPlugin](https://web.sdk.qcloud.com/im/doc/en/SDK.html#registerPlugin)をご参照ください。

**修正**

- ログアウトした後に匿名でライブストリーミンググループに参加すると、ロングポーリングのレスポンスにエラーコード70402が発生する問題。
- Taro 3.0+統合時にブラウザ環境でエラーと判断される問題。
- 画像のタイプとサイズの検証失敗時、返されるデータ構造が不正。

### 2.9.1 @2020.12.23

**修正**

開発者ツールベーシックエディションライブラリ2.14.1で[tim-wx-sdk.js](https://www.npmjs.com/package/tim-wx-sdk)をインポートしてコンパイルエラーが発生するという問題。

### 2.9.0 @2020.12.15

**追加**

- [createTextAtMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTextMessage)インターフェース。グループチャット時の@特定の人または@全員をサポートしました。
- [Message](https://web.sdk.qcloud.com/im/doc/en/Message.html)に`namecard`の属性を追加しました。グループメンバーのグループ名刺（グループニックネームと略称）の表示に使用されます。

### 2.8.5 @2020.11.23

**変更**

[logout](https://web.sdk.qcloud.com/im/doc/en/SDK.html#logout)インターフェースが、SDKがready状態でない時に呼び出せます。

**修正**

- 開封確認と既読通知が同時に存在するとき、SDKにランタイムエラーが起きる問題。
- ライブストリーミンググループをログアウトした後に、匿名で再び参加すると失敗する問題。
- グループリストが異常により消去される問題。

### 2.8.4 @2020.11.4

**追加**

- Baidu（百度）、Toutiao（頭条）、Alipay（支付宝）プラットフォームをサポートするようになりました（Baidu、Toutiao、Alipayプラットフォームでは、現在COSにアップロードする必要がある画像、ビデオ、ファイルなどのメッセージの送信がサポートされていません）。
- MPX、uni-appサードパーティフレームワークをサポートしました。

### 2.8.1 @2020.10.29

**追加**

bmp形式の画像の送信をサポートしました。

**変更**

送信側のオンラインメッセージ送信および受信側のオンラインメッセージ受信では、[セッションオブジェクト](https://web.sdk.qcloud.com/im/doc/en/Conversation.html)の`unreadCount`ならびに`lastMessage`を更新しません。

**修正**

最近の連絡先リストの同期異常により、SDKがready状態にならない問題。

### 2.8.0 @2020.10.20

**追加**

- [getGroupOnlineMemberCount](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupOnlineMemberCount)は、ライブブロードキャストグループのオンライン人数のクエリーをサポートします。
- 画像圧縮にアクセスするために画像メッセージを送信します。アクセス側は業務のニーズに応じてオリジナル画像またはサムネイルを表示できます。[ImagePayload](https://web.sdk.qcloud.com/im/doc/en/Message.html#.ImagePayload)をご参照ください。

**修正**

Taro 3.xをWebIMに統合するときの互換性の問題。

**変更**

SDKの容量を縮小しました。[tim-js-sdk](https://www.npmjs.com/package/tim-js-sdk)の容量を8.5%削減し、[tim-wx-sdk](https://www.npmjs.com/package/tim-wx-sdk)の容量を15%削減しました。

### 2.7.8 @2020.9.24

**追加**

[TIM.create](https://web.sdk.qcloud.com/im/doc/en/TIM.html#.create)インターフェースに`oversea`パラメータを追加しました。`true`に設定するとき、SDKが中国本土以外のドメイン名を使用し、干渉を回避します。

**修正**

- SDKがnot ready状態のときに、関連APIを呼び出すと戻り値が`undefined`となる問題。
- 統計に関する問題。

### 2.7.7 @2020.8.12

**追加**

[TIM.EVENT.SDK_RELOAD](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.SDK_RELOAD)イベント。

**修正**

- ネットワークが長時間切断した後に再接続したとき、またはバックエンドに長時間切り替えた後にフロントエンドに戻したときに、ライブストリーミンググループのメッセージが時々プルできなくなる問題。
- 画像メッセージimageFormatのタイプおよび値が、実際の画像形式と一致しない問題。
- Work・Publicのグループニックネームがおかしくなる問題。

### 2.7.6 @2020.7.9

**修正**

ライブストリーミンググループ（AVChatRoom）を長時間使用するとメッセージがプルできなくなることがある問題。

### 2.7.5 @2020.7.2

**修正**

REST APIを使用して[友だちワークグループの作成](https://intl.cloud.tencent.com/document/product/1047/34895)を行い、グループメンバーを指定すると、作成成功後にグループメンバーのメッセージ送信が失敗する問題。

### 2.7.2 @2020.6.30

**修正**

- [joinGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#joinGroup)の際に、実際にはグループ内にいないのに、SDKが「グループ内にすでに存在しています」と表示し、これによりメッセージが正常に受信できなくなることがある問題。
- 臨時ミーティンググループの送信メッセージ数の統計エラー。

### 2.7.0 @2020.6.8

**追加**

C2Cメッセージの開封報告（相手側が送信メッセージを読んだかどうか）をサポートしました。詳細については、イベント [TIM.EVENT.MESSAGE_READ_BY_PEER](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_READ_BY_PEER)をご参照ください。相手側が既読の[メッセージ](https://web.sdk.qcloud.com/im/doc/en/Message.html)は、`isPeerRead`属性値が`true`になります。

**修正**

- チャットルーム(ChatRoom)参加後に作成したセッションのうち最新のメッセージが表示されない問題。
- ログイン後、オーディオビデオチャットルーム（AVChatRoom）に参加していないのにオーディオビデオチャットルーム（AVChatRoom）にメッセージが送信可能である問題。

### 2.6.6 @2020.5.27

**修正**

- オーディオビデオチャットルーム（AVChatRoom）で、メッセージが画面に重複して表示されることがある問題。
- [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList)で空メッセージが検出されると、エラーが発生する問題。
- [logout](https://web.sdk.qcloud.com/im/doc/en/SDK.html#logout)後に、再度[login](https://web.sdk.qcloud.com/im/doc/en/SDK.html#login)すると、[joinGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#joinGroup)時に、70001のエラーが起きることがある問題。

### 2.6.4 @2020.5.8

**追加**

[sendMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#sendMessage)インターフェースに送信オプションを追加し、オンラインメッセージの送信（オフラインおよびローミングは無し。AVChatRoomならびにBChatRoomでは使用できません）、および[オフラインプッシュ](https://intl.cloud.tencent.com/document/product/1047/33525)の設定をサポートしました。

### 2.6.3 @2020.4.26

**修正**

- [createCustomMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createCustomMessage)のpayload.data payload.extensionタイプのインプットが不正だと、メッセージの内容が消失する問題。
- 1回のリクエストのレスポンスが複数のメッセージとなるときに起きる可能性がある、順序の乱れの問題。
- C2Cセッションの未読数オーバーフローにより、既読報告後の未読数カウントがクリアされないことがある問題。
- [TIM.EVENT.ERROR](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.ERROR)のevent.data.codeおよびevent.data.undefinedがundefinedになることがある問題。

### 2.6.2 @2020.4.16

**追加**

- [updateGroupProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateGroupProfile)で、全体ミュートおよび全体ミュートの取り消しをサポートしました。
- [getGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberList)で、グループメンバーのミュート期限タイムスタンプ（[muteUntil](https://web.sdk.qcloud.com/im/doc/en/GroupMember.html)）のプルをサポートしました。

**修正**

グループの最新のメッセージがグループプロンプトメッセージのときに、未読カウントがクリアされない問題。

### 2.6.1 @2020.4.8

**修正**

COSアップロードのサイン失効後にすみやかに更新しないとファイルをアップロードできなくなることがある問題。

### 2.6.0 @2020.3.30

**追加**

- Web端末で、ビデオメッセージ送信の作成[createVideoMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createVideoMessage)をサポートしました。最大100MBのビデオファイルを送信できます。
- [Message](https://web.sdk.qcloud.com/im/doc/en/Message.html)に`nick`および`avatar`の属性を追加しました。オーディオビデオチャットルーム(AVChatRoom)でメッセージ送信者のニックネームおよびプロフィール画像アドレスの表示に使用します（事前に[updateMyProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateMyProfile)を呼び出して設定してください）。
- Web端末で、マルチインスタンスでログインした時、C2Cメッセージの取り消し通知が各インスタンスにおいて同期できるようになりました。
- [updateGroupProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateGroupProfile)を呼び出してグループカスタムフィールドの修正に成功した後、グループメンバーがグループプロンプトメッセージを受信し、関連する内容[Message.payload.newGroupProfile.groupCustomField](https://web.sdk.qcloud.com/im/doc/en/Message.html#.GroupTipPayload)を取得できます。

**変更**

[TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.GROUP_SYSTEM_NOTICE_RECEIVED)は廃棄されました。[MESSAGE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_RECEIVED)を代替としてご利用ください。

**修正**

[getGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupList)インターフェースを呼び出すと時々エラーが報告される問題。

### 2.5.2 @2020.3.13

**変更**

[searchGroupByID](https://web.sdk.qcloud.com/im/doc/en/SDK.html#searchGroupByID)の失敗時のログレベルをWarningに引き下げ、プロンプトの文面を修正しました。

**修正**

- 匿名ユーザー（またはゲスト）が[TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM)タイプのグループへの参加に失敗する問題、および統計の問題。
- その他の既知の問題。

### 2.5.1 @2020.3.5

**変更**

[login](https://web.sdk.qcloud.com/im/doc/en/SDK.html#login)成功時のコールバックオブジェクト`imResponse.data`に`repeatLogin: true`のキーバリューペアを追加しました。すでにログインしているアカウントが再ログインした状況を表示するために使用します。

**修正**

オーディオビデオチャットルーム（AVChatRoom）の受信側が受信するメッセージの優先度と送信側で設定するメッセージ優先度が一致しない問題。

### 2.5.0 @2020.2.28

**追加**

- ネットワーク状態変更イベント [TIM.EVENT.NET_STATE_CHANGE](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.NET_STATE_CHANGE)。このイベントに基づき、アクセス側で関連するプロンプトとガイダンスを行うことができます。

**変更**
[エラーコード](https://web.sdk.qcloud.com/im/doc/en/global.html)を減らし、最適化しました。

**修正**

- [コンソール](https://console.cloud.tencent.com/im)でオーディオビデオチャットルーム（AVChatRoom）を作成してグループマスターを指定したときに、グループマスターがこのグループに参加した後、グループ内の他のメンバーが送信した情報がグループマスター側で重複する問題。
- [コンソール](https://console.cloud.tencent.com/im)またはREST APIを使用してグループを頻繁に作成、廃棄すると、SDKが[TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.GROUP_SYSTEM_NOTICE_RECEIVED) イベントを配信しなくなる問題。
- [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList)で、グループメッセージリストがプルできなくなることがある問題。

### 2.4.2 @2020.2.7

**追加**
グループメッセージで[メッセージの優先度](https://intl.cloud.tencent.com/document/product/1047/33526)、[列挙値](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.MSG_PRIORITY_HIGH)、[使用例](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTextMessage)の設定をサポートするようになりました。

### 2.4.1 @2020.1.14

**変更**
匿名ユーザー（またはゲスト）は、[TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM)タイプのグループのみ参加できます。

**修正**

- オンラインメッセージをプルするとロストが生じることがある問題。
- AVChatRoomのグループシステム通知を受信しても[TIM.EVENT.MESSAGE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_RECEIVED) イベントが配信されない問題。
- 一部のシーンにおいて、グループチャットメッセージ取り消しの結果が正しくない問題。
- その他の既知の問題。

### 2.4.0 @2020.1.3

**追加**

- メッセージの取り消し[revokeMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#revokeMessage)。
- [Message](https://web.sdk.qcloud.com/im/doc/en/Message.html)に`isRevoked`の属性を追加しました。値が`true`のとき、取り消されたメッセージを表示します。
- メッセージ取り消しのイベント通知[TIM.EVENT.MESSAGE_REVOKED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_REVOKED)。
- キックアウトによるオフラインのイベント通知[TIM.EVENT.KICKED_OUT](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.KICKED_OUT)に、キックアウトによるオフラインのタイプとして、[複数端末ログインによるキックアウト](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.KICKED_OUT_MULT_ACCOUNT)と[UserSig失効によるキックアウト](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.KICKED_OUT_USERSIG_EXPIRED)を追加しました。

**変更**

- [createFileMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFileMessage)で、アップロードするファイルサイズを20Mから100Mに変更しました。
- [グループプロンプトメッセージ](https://web.sdk.qcloud.com/im/doc/en/Message.html#.GroupTipPayload)の`msgMemberInfo`および`shutupTime`はまもなく廃棄されます。代替として`memberList`および`muteTime`を使用してください。
- コンソールで[IM AIBotエントリー](https://cloud.tencent.com/act/event/smarty-service?from=im-doc)を追加しました。

**修正**

- [off](https://web.sdk.qcloud.com/im/doc/en/SDK.html#off)インターフェースを呼び出してモニタリングイベントを取り消しできない問題。
- [Message](https://web.sdk.qcloud.com/im/doc/en/Message.html)の`isRead`の属性値およびタイプが正しくない問題。
- ビデオメッセージ送信時に、ビデオファイルが最大制限値を超えた後のエラーコードおよびエラー情報に誤りがある問題。
- カスタムフィールドの更新後に、フィールドの内容が正しくないことがある問題。
- ログイン後にAVチャットルームタイプのグループに参加すると、[JOIN_STATUS_ALREADY_IN_GROUP](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.JOIN_STATUS_ALREADY_IN_GROUP)が出現することがある問題。
- core-jsによる潜在的な性能の問題。

### 2.3.2 @2019.12.18

**変更**
[getUserProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getUserProfile)および[updateMyProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateMyProfile)で、[カスタムプロファイルフィールド](https://intl.cloud.tencent.com/document/product/1047/33520)をサポートしました。

**修正**
[getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList)で取得した複合メッセージのメッセージが消失する問題。

### 2.3.1 @2019.12.13

**追加**

- [createImageMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createImageMessage)および[createFileMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFileMessage)インターフェースで、[File](https://developer.mozilla.org/en/docs/Web/API/File)オブジェクトを渡せるようになりました。
- 顔絵文字メッセージ作成インターフェース[createFaceMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFaceMessage)。
- [TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM)タイプのグループのメッセージ通知効率を最適化し、ユーザーエクスペリエンスを大幅に向上させました。

**変更**

- メッセージ送信失敗時、SDKが実際のエラーコードおよびエラー情報を返します。
- [logout](https://web.sdk.qcloud.com/im/doc/en/SDK.html#logout)を呼び出したときに、現在のインスタンスのメッセージチャネルのみログアウトします。
- アクセス側がインプットするコールバック関数に対して安全にカプセル化し、コールバック関数のロジックにエラーがあったときに、異常をキャッチし迅速に問題を特定できるようにしました。
- [IMサーバーのエラーコード](https://intl.cloud.tencent.com/document/product/1047/34348)に遭遇したときに、SDKが中国語エラー情報を出力します。

**修正**

- 1回のメッセージ送信で[TIM.EVENT.CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED)が複数回トリガーされる問題。
- [registerPlugin](https://web.sdk.qcloud.com/im/doc/en/SDK.html#registerPlugin)またはインターフェースを呼び出さずに渡したパラメータが間違っていると、画像などのファイルをアップロードしたときにSDKがエラーを報告する問題。
- [TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM)タイプのグループを解散した後、ロングポーリングが停止しない問題。
- 「マルチインスタンス」または「マルチ端末」ログインを有効にし、1つのWebインスタンスをログアウトすると、その他のインスタンスまたは端末がメッセージを受信できなくなる問題。
- 偶発的に起きる、プルしたセッションリストの構造上の問題によりSDKがエラーを報告する問題。

### 2.2.1 @2019.11.28

**変更**
グループローミングメッセージをプルするロジックを改善しました。

**修正**

- グループマスターがオーディオビデオチャットルームのグループプロファイルを修正した後、SDKが[2901エラーコード](https://web.sdk.qcloud.com/im/doc/en/global.html)を表示する問題。
- グループ管理者がグループ参加申請の処理を完了し、更新した後も、依然として処理済みの申請を受信している問題。

### 2.2.0 @2019.11.21

**追加**

- ビデオメッセージ送信の作成[createVideoMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createVideoMessage)をサポートしました。全プラットフォームでビデオメッセージの相互通信が可能です（最新版の[TUIKitおよびSDK](https://intl.cloud.tencent.com/document/product/1047/33996)にアップグレードする必要があります）。
- グループメンバープロファイルのクエリーのインターフェース[getGroupMemberProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberProfile)。
Native IM v3.xから送信された音声、ファイルメッセージとの互換性をサポートしました。
- 位置情報メッセージ[GeoPayload](https://web.sdk.qcloud.com/im/doc/en/Message.html#.GeoPayload)の受信をサポートしました。

**変更**
ローカルストレージに書き込みできるグループ数は最大100件です。100件を超えるグループリストは全数を書き込みできません。

**修正**

- ログアウト後、[TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM)タイプのグループのロングポーリングが停止しない問題。
- [TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM)タイプのグループのメッセージインスタンスで、グループ名刺に値がない問題。
- IE10ブラウザでエラーが報告される問題。
- 匿名でグループに参加できない問題。

### 2.1.4 @2019.11.7

**変更**

- SDK APIが返した`Promise`状態が`rejected`のとき、SDKが[TIM.EVENT.ERROR](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.ERROR)イベントを配信しないようにしました。
- 自分のProfile（プロファイル）が更新されると、ローカルキャッシュにすみやかに書き込まれます。

**修正**

- Angularアーキテクチャのzone.jsでプロトタイプチェーンを修正するとSDKの統合でエラーが発生する問題。
- グループマスターが[TIM.TYPES.GRP_AVCHATROOM](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.GRP_AVCHATROOM)タイプのグループを作成して参加すると、メッセージを受信できない問題。
- グループリストが大きすぎると初期化にエラーが発生する問題。

### 2.1.3 @2019.10.31

**変更**
REST APIまたは旧版 IMで送信した複合メッセージ（1件のメッセージの中に複数のメッセージエレメントが含まれているもの）との互換性をサポートしました。詳細については、[互換性ガイド](https://web.sdk.qcloud.com/im/doc/en/tutorial-01-faq.html)をご参照ください。

**修正**

- 未読数カウントの不正。
- メッセージ既読の未報告により、メッセージの順番が乱れる問題。
- 空画像メッセージの送信に成功したがレンダリングできない問題。SDKは空画像メッセージの送信をサポートしていません。
- 空ファイルメッセージを送信したときのメッセージ状態の不正。SDKは空ファイルメッセージの送信をサポートしていません。
- [getGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberList)インターフェースを呼び出したときに、SDKコードでエラーが報告されることがある問題。

### 2.1.2 @2019.10.25

**追加**
 [getGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupList)インターフェースで、グループマスターID、グループメンバー数などのグループ関連プロファイルのプルをサポートしました。

**修正**

- REST APIを使用してオーディオビデオチャットルームのグループカスタム通知を送信すると、SDKコードでエラーが報告される問題。
- グループを退出して再度参加すると、getMessageListインターフェースを呼び出してもSDKがメッセージ履歴プルのリクエストを送信しない問題。
- アップロード失敗時、SDKコードでエラーが報告される問題。

### 2.1.1 @2019.10.18

**追加**
[オーディオメッセージの送信](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createAudioMessage)をサポートしました。全プラットフォームでオーディオメッセージの相互通信が可能です（最新版の[TUIKitおよびSDK](https://intl.cloud.tencent.com/document/product/1047/33996)にアップグレードする必要があります）。

**修正**
グループを退出して再度参加したとき、依然として、[getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList)でグループ退出前のメッセージ履歴をプルできる問題。

### 2.1.0 @2019.10.16

**追加**

- Webで、[オーディオメッセージ](https://web.sdk.qcloud.com/im/doc/en/Message.html#.AudioPayload)の受信をサポートしました。
- Webで、[ビデオメッセージ](https://web.sdk.qcloud.com/im/doc/en/Message.html#.VideoPayload)の受信をサポートしました。

**変更**

- [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList)インターフェースで、1回に最大15件のメッセージをプルできるようにしました。
- [TIM.TYPES.MSG_SOUND](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.MSG_SOUND)を廃棄し、[TIM.TYPES.MSG_AUDIO](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html#.MSG_AUDIO)で代替しました。

**修正**

- [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList)インターフェースで削除済みのグループチャットセッションのメッセージのプルができない問題。
- グループシステム通知にグループ名がない問題。
- メッセージを受信した新規作成セッションにプロファイルがない問題。

### 2.0.11 @2019.10.12

**修正**
Reactフレームワークにおける画像メッセージの送信失敗。

### 2.0.9 @2019.9.19

**追加**
画像メッセージ送信前に、画像の実際の幅・高さを検出します。

**変更**

- デフォルトでHTTPSプロトコルを使用します。
- 新規グループシステム通知イベントの受信について、タイプを [TIM.EVENT.GROUP_SYSTEM_NOTICE_RECEIVED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.GROUP_SYSTEM_NOTICE_RECEIVED)にしました。

**修正**

- 画像メッセージスプラッシュスクリーンの送信。
- 拡張子がJPGなどのタイプの画像の送信失敗。
