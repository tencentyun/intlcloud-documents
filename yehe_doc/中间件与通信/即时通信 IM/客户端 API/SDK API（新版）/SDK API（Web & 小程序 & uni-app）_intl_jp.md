## TIM

TIMは、IM Web SDKのネームスペースです。SDKインスタンスの静的メソッド[create()](https://web.sdk.qcloud.com/im/doc/en/TIM.html#.create)、イベント常数[EVENT](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html)、およびタイプ常数[TYPES](https://web.sdk.qcloud.com/im/doc/en/module-TYPES.html)を提供します。

**初期化**

| API        | 説明       |
| --- | --- |
| [create](https://web.sdk.qcloud.com/im/doc/en/TIM.html#.create) | SDKインスタンスを作成します。|

## SDKインスタンス

| 基本概念 | 説明 |
| :--- | :---- |
| Message（メッセージ） | IM SDKの[Message](https://web.sdk.qcloud.com/im/doc/en/Message.html)は相手に送信する内容を表します。メッセージには、送信者かどうか、送信者のアカウント番号、メッセージの生成時刻など、いくつかの属性が含まれています。|
| Conversation（セッション） | IM SDKの[Conversation](https://web.sdk.qcloud.com/im/doc/en/Conversation.html)は2種類に分けられます<li>C2C（Client to Client）セッションは、シングルチャットの場合、自分と相手の間で確立されたセッションを意味します。</li><li>GROUP（グループ）セッションは、グループチャットの場合、グループメンバーが形成するセッションを意味します。</li>|
| Profile（プロファイル） | IM SDKの[Profile](https://web.sdk.qcloud.com/im/doc/en/Profile.html)は、ニックネーム、性別、個人署名、およびプロファイルフォトアドレスなど、よく使用する個人の基本情報を記述します。|
| Friend（友達） | IM SDKの[Friend](https://web.sdk.qcloud.com/im/doc/en/Friend.html)は、メモやグループなど、よく使用する友達の基本情報を記述します。|
| FriendApplication（友達申請）	| IM SDKの[FriendApplication](https://web.sdk.qcloud.com/im/doc/en/FriendApplication.html)は、友達追加のソースやメモなど、友達の申請でよく使用する基本情報を記述します。|
| FriendGroup（友達グループ）| IM SDKの[FriendGroup](https://web.sdk.qcloud.com/im/doc/en/FriendGroup.html)は、グループ名やグループメンバーなど、友達グループによく使用する基本情報を記述します。
| Group（グループ） | IMの[Group](https://web.sdk.qcloud.com/im/doc/en/Group.html)は、複数人でのチャットをサポートする通信システムです。友人のワークグループ、知らない人とのソーシャルグループ、臨時ミーティンググループ、ライブブロードキャストグループをサポートします。|
| GroupMember（グループメンバー） | IM SDKの[GroupMember](https://web.sdk.qcloud.com/im/doc/en/GroupMember.html)は、ID、ニックネーム、グループ内でのアイデンティティ、およびグループへの加入時間など、よく使用するグループメンバーの基本情報を記述します。|
| グループプロンプトメッセージ | ユーザーがグループに招待されたり、グループから削除されたりするなどのイベントが発生するとき、グループ内でプロンプトメッセージが生成され、アクセス側は実際のニーズに応じてグループユーザーに表示したり無視したりできます。<br/>グループプロンプトメッセージにはさまざまなタイプがあります。詳細の説明については、[Message.GroupTipPayload](https://web.sdk.qcloud.com/im/doc/en/Message.html#.GroupTipPayload)をご参照ください。|
| グループシステム通知メッセージ | ユーザーがグループへの参加を申請するなどのイベントが発生するとき、管理者はグループへの参加申請などのシステムメッセージを受け取ります。管理者がグループへの参加申請に同意または拒否した場合、IM SDKはグループへの参加申請などの対応するメッセージをグループシステム通知メッセージを通じてアクセス側に送信し、アクセス側はそれをユーザーに表示します。<br/>グループシステム通知メッセージにはさまざまなタイプがあります。詳細の説明については、[Message.GroupSystemNoticePayload](https://web.sdk.qcloud.com/im/doc/en/Message.html#.GroupSystemNoticePayload)をご参照ください。  |
| メッセージの画面表示 | ユーザーが送信をクリックすると、事前に入力されたテキストや選択された画像などの情報が、ユーザーのコンピューターまたは携帯電話の画面に表示される過程です。|

### イベント関連
| API        | 説明       |
| --- | --- |
| [on](https://web.sdk.qcloud.com/im/doc/en/SDK.html#on) | イベントをリッスンします。 |
| [off](https://web.sdk.qcloud.com/im/doc/en/SDK.html#off) | イベントのリッスンをキャンセルします。 |

### プラグインの登録
| API        | 説明       |
| --- | --- |
| [registerPlugin](https://web.sdk.qcloud.com/im/doc/en/SDK.html#registerPlugin) | プラグインを登録します。 |

### ログレベルの設定
| API        | 説明       |
| --- | --- |
| [setLogLevel](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setLogLevel) | ログレベルを設定します。|

### SDKインスタンスの廃棄
| API        | 説明       |
| --- | --- |
| [destroy](https://web.sdk.qcloud.com/im/doc/en/SDK.html#destroy)  | SDKインスタンスを廃棄します。|

### ログイン関連
| API        | 説明       |
| --- | --- |
| [login](https://web.sdk.qcloud.com/im/doc/en/SDK.html#login) | ログインします。 |
| [logout](https://web.sdk.qcloud.com/im/doc/en/SDK.html#logout) | ログアウトします。 |

### メッセージ
| API        | 説明       |
| --- | --- |
| [createTextMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTextMessage) | テキストメッセージを作成します。 |
| [createTextAtMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTextAtMessage) |@リマインダ通知機能があるテキストメッセージを作成します。 |
| [createImageMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createImageMessage) | 画像メッセージを作成します。 |
| [createAudioMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createAudioMessage) | オーディオメッセージを作成します。 |
| [createVideoMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createVideoMessage) | ビデオメッセージを作成します。 |
| [createCustomMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createCustomMessage) | カスタムメッセージを作成します。 |
| [createFaceMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFaceMessage) | 絵文字メッセージを作成します。 |
| [createFileMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFileMessage) | ファイルメッセージを作成します。 |
| [createLocationMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createLocationMessage) | 地理位置メッセージを作成します。 |
| [createMergerMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createMergerMessage) | マージメッセージを作成します。 |
| [downloadMergerMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#downloadMergerMessage) | マージメッセージをダウンロードします。 |
| [createForwardMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createForwardMessage) | 転送メッセージを作成します。 |
| [sendMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#sendMessage) | メッセージを送信します。 |
| [revokeMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#revokeMessage) | メッセージを撤回します。 |
| [resendMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#resendMessage) | メッセージを再送します。 |
| [deleteMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessage) | メッセージを削除します。 |
| [setMessageExtensions](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setMessageExtensions) | メッセージ拡張子を設定します。|
| [getMessageExtensions](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageExtensions) | メッセージ拡張子を取得します。|
| [deleteMessageExtensions](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteMessageExtensions) | メッセージ拡張子を削除します。 |

### セッション
| API        | 説明       |
| --- | --- |
| [modifyMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#modifyMessage) | メッセージを変更します。
| [getMessageList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageList) | メッセージリストを取得します。  |
| [getMessageListHopping](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageListHopping) | 指定されたメッセージsequenceまたはメッセージ時間によってセッションのメッセージリストを取得します。|
| [sendMessageReadReceipt](https://web.sdk.qcloud.com/im/doc/en/SDK.html#sendMessageReadReceipt) | メッセージの開封確認を送信します。|
| [getMessageReadReceiptList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMessageReadReceiptList) | 開封確認リストを取得します。|
| [getGroupMessageReadMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMessageReadMemberList) | グループメッセージの既読（または未読）メンバーリストを取得します。|
| [findMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#findMessage) | messageIDに基づいてセッションのローカルメッセージをクエリーします。|
| [setMessageRead](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setMessageRead) | メッセージの開封確認を設定します。  |
| [getConversationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationList) | セッションリストを取得します。 |
| [getConversationProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationProfile) | セッションのプロファイルを取得します。 |
| [deleteConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversation) | セッションを削除します。 |
| [clearHistoryMessage](https://web.sdk.qcloud.com/im/doc/en/SDK.html#clearHistoryMessage) | シングルチャットまたはグループチャットのローカルメッセージとクラウドメッセージをクリアします（セッションを削除しません）。|
| [pinConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#pinConversation) | セッションをトップにしたりトップにすることをキャンセルしたりします。 |
| [setAllMessageRead](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setAllMessageRead) | すべてのセッションの未読メッセージを既読に設定します。 |
| [setMessageRemindType](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setMessageRemindType) | セッションメッセージのリマインダ通知タイプを設定します。このインターフェースを使用して、「メッセージ通知オフ」および「メッセージの拒否」機能を実現できます。 |
| [getTotalUnreadMessageCount](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getTotalUnreadMessageCount) | セッション未読総数を取得します。|

### セッションのサブグループ
| API        | 説明       |
| --- | --- |
| [setConversationCustomData](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setConversationCustomData) | セッションのカスタムデータを設定します。|
| [markConversation](https://web.sdk.qcloud.com/im/doc/en/SDK.html#markConversation) | セッションをタグつけます。 |
| [getConversationGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationGroupList) | セッションのサブグループリストを取得します。|
| [createConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createConversationGroup) | セッションのサブグループを作成します。|
| [deleteConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversationGroup) | セッションのサブグループを削除します。|
| [renameConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#renameConversationGroup) | セッションのサブグループをリネームします。|
| [addConversationsToGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addConversationsToGroup) | セッションをセッションのサブグループに追加します。|
| [deleteConversationsFromGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversationsFromGroup) | セッションのサブグループからセッションを削除します。|

### プロファイル
| API        | 説明       |
| --- | --- |
| [getMyProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getMyProfile) | 個人情報を取得します。|
| [getUserProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getUserProfile) | その他のユーザー個人情報を取得します。|
| [updateMyProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateMyProfile) | 個人情報を更新します。 |
| [getBlacklist](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getBlacklist) | 自分のブラックリストを取得します。 |
| [addToBlacklist](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addToBlacklist) | ユーザーをブラックリストに追加します。|
| [removeFromBlacklist](https://web.sdk.qcloud.com/im/doc/en/SDK.html#removeFromBlacklist) | ブラックリストからユーザーを削除します。|

### ユーザー状態
| API        | 説明       |
| --- | --- |
| [setSelfStatus](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setSelfStatus) | 自分のカスタム状態を設定します。 |
| [getUserStatus](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getUserStatus) | ユーザー状態をクエリーします。 |
| [subscribeUserStatus](https://web.sdk.qcloud.com/im/doc/en/SDK.html#subscribeUserStatus) | ユーザー状態をサブスクリプションします。 |
| [subscribeUserStatus](https://web.sdk.qcloud.com/im/doc/en/SDK.html#unsubscribeUserStatus) | ユーザー状態のサブスクリプションをキャンセルします。 |

### リレーショナルチェーン
| API        | 説明       |
| --- | --- |
| [getFriendList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendList) | SDKによってキャッシュされた友達リストを取得します。|
| [addFriend](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addFriend) | 友達を追加します。|
| [deleteFriend](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteFriend) | 友達を削除します。|
| [checkFriend](https://web.sdk.qcloud.com/im/doc/en/SDK.html#checkFriend) | 友好度を確認します。|
| [getFriendProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendProfile) | 指定した友達のフレンドデータとプロフィールデータを取得します。 |
| [updateFriend](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateFriend) | 友達のリレーショナルチェーンデータを更新します。|
| [getFriendApplicationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendApplicationList) | SDKによってキャッシュされた友達申請リストを取得します。 |
| [acceptFriendApplication](https://web.sdk.qcloud.com/im/doc/en/SDK.html#acceptFriendApplication) | 友達申請に同意します。|
| [refuseFriendApplication](https://web.sdk.qcloud.com/im/doc/en/SDK.html#refuseFriendApplication) | 友達申請を拒否します。|
| [deleteFriendApplication](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteFriendApplication) | 友達申請を削除します。|
| [setFriendApplicationRead](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setFriendApplicationRead) | 友達申請を既読として報告します。|
| [getFriendGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getFriendGroupList) | SDKによってキャッシュされた友達のサブグループリストを取得します。|
| [createFriendGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createFriendGroup) | 友達のサブグループを作成します。|
| [deleteFriendGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteFriendGroup) | 友達のサブグループを削除します。|
| [addToFriendGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addToFriendGroup) | 友達のサブグループリストに追加します。|
| [removeFromFriendGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#removeFromFriendGroup) | 友達のサブグループから友達を削除します。|
| [renameFriendGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#renameFriendGroup) | 友達のサブグループをリネームします。|

### グループ
| API        | 説明       |
| --- | --- |
| [getGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupList) | グループリストを取得します。 |
| [getGroupProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupProfile) | グループの詳細データを取得します。|
| [createGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createGroup) | グループを作成します。 |
| [dismissGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#dismissGroup) | グループを解散します。|
| [updateGroupProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateGroupProfile) | グループデータを変更します。 |
| [joinGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#joinGroup) | グループへの参加を申請します。|
| [quitGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#quitGroup) | グループから退出します。 |
| [searchGroupByID](https://web.sdk.qcloud.com/im/doc/en/SDK.html#searchGroupByID) | グループを検索します。 |
| [getGroupOnlineMemberCount](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupOnlineMemberCount) | ライブブロードキャストグループのオンライン人数を取得します。 |
| [changeGroupOwner](https://web.sdk.qcloud.com/im/doc/en/SDK.html#changeGroupOwner) | グループを転送します。|
| [getGroupApplicationList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupApplicationList) | グループへの参加リストを取得します。|
| [handleGroupApplication](https://web.sdk.qcloud.com/im/doc/en/SDK.html#handleGroupApplication) | グループへの参加を処理します。|
| [initGroupAttributes](https://web.sdk.qcloud.com/im/doc/en/SDK.html#initGroupAttributes) | グループ属性を初期化します。 |
| [setGroupAttributes](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupAttributes) | グループ属性を設定します。 |
| [deleteGroupAttributes](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteGroupAttributes) | グループ属性を削除します。 |
| [getGroupAttributes](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupAttributes) | グループ属性を取得します。 |

### グループメンバー
| API        | 説明       |
| --- | --- |
| [getGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberList) | グループメンバーリストを取得します。 |
| [getGroupMemberProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getGroupMemberProfile) | グループメンバーの個人情報を取得します。 |
| [addGroupMember](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addGroupMember) | グループメンバーを追加します。|
| [deleteGroupMember](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteGroupMember) | グループメンバーを削除します。 |
| [setGroupMemberMuteTime](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupMemberMuteTime) |グループメンバーの発言禁止時間を設定します。|
| [setGroupMemberRole](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupMemberRole) | グループメンバーのロールを変更します。|
| [setGroupMemberNameCard](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupMemberNameCard) | グループメンバーのプロファイルを設定します。 |
| [setGroupMemberCustomField](https://web.sdk.qcloud.com/im/doc/en/SDK.html#setGroupMemberCustomField) | グループメンバーのカスタムフィールドを設定します。|
| [markGroupMemberList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#markGroupMemberList) | グループメンバをタグつけます。|

### トピック
| API        | 説明       |
| --- | --- |
| [getJoinedCommunityList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getJoinedCommunityList) | 現在のユーザーが参加しているトピックをサポートするコミュニティリストを取得します。 |
| [createTopicInCommunity](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createTopicInCommunity) | トピックを作成します。 |
| [deleteTopicFromCommunity](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteTopicFromCommunity) | トピックを削除します。 |
| [updateTopicProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#updateTopicProfile) | トピックデータを更新します。 |
| [getTopicList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getTopicList) |トピックリストを取得します。|
