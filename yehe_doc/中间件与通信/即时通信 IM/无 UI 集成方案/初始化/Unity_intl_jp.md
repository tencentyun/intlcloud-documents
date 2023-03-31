## 機能説明
IM SDKの各機能を使用する前に、初期化を実行する**必要**があります。
ほとんどの運用シーンでは、Appのライフサイクルにおいて、IM SDKの初期化を1回だけ実行すればよいです。


## 初期化
SDKを初期化するには、以下を実施してください：
1. SDKAppIDの用意
2. SdkConfigの設定
3. SDKイベントリスナーの設定
4. [`Init`](https://comm.qq.com/im/doc/unity/zh/api/IMSDKInit/Init.html)の呼出しによるSDKの初期化

以下では上記の各実施事項を詳しく説明します。

[](id:SDKAppID)
### SDKAppIDの用意
初期化するには、正しいSDKAppIDを持つ必要があります。
SDKAppIDはTencent Cloud IMサービスがお客様のアカウントを区別するための唯一の識別子です。独立したAppごとにSDKAppIDを申請することをお勧めします。異なるSDKAppIDでは、メッセージは隔離されており、お互い通信できません。
[IMコンソール](https://console.cloud.tencent.com/im)ですべてのSDKAppIDを確認できます。**Appを新規作成**ボタンをクリックすれば、新しいSDKAppIDを作成できます。


[](id:SDKConfig)
### SdkConfigの設定

SDKを初期化する前に、[SdkConfig](https://comm.qq.com/im/doc/unity/zh/types/SDKSetConfigAttributes/SdkConfig.html)オブジェクトを初期化する必要があります。このオブジェクトはローカルSDKキャッシュとログの保存先を設定することに使用されます。

IM動作時のログとデータの保存先を設定します。

### sdk_config_config_file_path

IMローカルデータの保存先。
>!Appにはこの保存先への読み取り、書込み権限が必要です。

### sdk_config_log_file_path

IMログの保存先。
>!アプリケーションにはこの保存先への読取り・書込み権限が必要です。

### 初期化インターフェースの呼出し
上記を実施した後、`Init`([詳細はこちら](https://comm.qq.com/im/doc/unity/zh/api/IMSDKInit/Init.html))を使用してSDKを初期化します。

サンプルコードは以下の通りです：

```c#
public static void Init() {
        int sdkappid = 0; // IMコンソールからAppのSDKAppIDを取得する。
        SdkConfig sdkConfig = new SdkConfig();

        sdkConfig.sdk_config_config_file_path = Application.persistentDataPath + "/TIM-Config";

        sdkConfig.sdk_config_log_file_path = Application.persistentDataPath + "/TIM-Log";

        TIMResult res = TencentIMSDK.Init(long.Parse(sdkappid), sdkConfig);
}
```

### SDKグローバルイベントリスナーの登録
SDKを初期化した後、[`NetworkStatusListenerCallback`](https://comm.qq.com/im/doc/unity/zh/callback/NetworkStatusListenerCallback.html)、[`UserSigExpiredCallback`](https://comm.qq.com/im/doc/unity/zh/callback/UserSigExpiredCallback.html)などのコールバックでイベントを出力します。例えば、接続状態、ログイン資格情報期限切れなど。
initSDKを呼出した直後にグローバルイベントリスナーを登録し、該当するコールバックでロジック処理を行うことをお勧めします。

関連のコールバックを下表に示します：

| イベントコールバック                                         | イベント説明                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [RecvNewMsgCallback](https://comm.qq.com/im/doc/unity/zh/callback/RecvNewMsgCallback.html) | 新しいメッセージを受信した時に実行するコールバック           |
| [MsgReadedReceiptCallback](https://comm.qq.com/im/doc/unity/zh/callback/MsgReadedReceiptCallback.html) | メッセージ既読確認を通知した時に実行するコールバック         |
| [MsgRevokeCallback](https://comm.qq.com/im/doc/unity/zh/callback/MsgRevokeCallback.html) | 受信したメッセージが取り消された時に実行するコールバック     |
| [MsgElemUploadProgressCallback](https://comm.qq.com/im/doc/unity/zh/callback/MsgElemUploadProgressCallback.html) | メッセージにおけるエレメント関連のファイルのアップロード進捗に関するコールバック |
| [GroupTipsEventCallback](https://comm.qq.com/im/doc/unity/zh/callback/GroupTipsEventCallback.html) | グループシステムメッセージに関するコールバック               |
| [GroupAttributeChangedCallback](https://comm.qq.com/im/doc/unity/zh/callback/GroupAttributeChangedCallback.html) | グループの属性が変更された時に実行するコールバック           |
| [ConvTotalUnreadMessageCountChangedCallback](https://comm.qq.com/im/doc/unity/zh/callback/ConvTotalUnreadMessageCountChangedCallback.html) | セッションの未読メッセージ数が変更された時に実行するコールバック |
| [NetworkStatusListenerCallback](https://comm.qq.com/im/doc/unity/zh/callback/NetworkStatusListenerCallback.html) | ネットワーク接続状態監視に関するコールバック                 |
| [KickedOfflineCallback](https://comm.qq.com/im/doc/unity/zh/callback/KickedOfflineCallback.html) | 強制退会によるオフラインを通知する時に実行するコールバック   |
| [UserSigExpiredCallback](https://comm.qq.com/im/doc/unity/zh/callback/UserSigExpiredCallback.html) | 資格情報が期限切れになった時に実行するコールバック           |
| [OnAddFriendCallback](https://comm.qq.com/im/doc/unity/zh/callback/OnAddFriendCallback.html) | 友達追加に関するコールバック                                 |
| [OnDeleteFriendCallback](https://comm.qq.com/im/doc/unity/zh/callback/OnDeleteFriendCallback.html) | 友達削除に関するコールバック                                 |
| [UpdateFriendProfileCallback](https://comm.qq.com/im/doc/unity/zh/callback/UpdateFriendProfileCallback.html) | 友達プロフィールが更新された時に実行するコールバック         |
| [FriendAddRequestCallback](https://comm.qq.com/im/doc/unity/zh/callback/FriendAddRequestCallback.html) | 友達追加申請に関するコールバック                             |
| [FriendApplicationListDeletedCallback](https://comm.qq.com/im/doc/unity/zh/callback/FriendApplicationListDeletedCallback.html) | 友達追加申請が削除された時に実行するコールバック             |
| [FriendApplicationListReadCallback](https://comm.qq.com/im/doc/unity/zh/callback/FriendApplicationListReadCallback.html) | 友達追加申請が既読になった時に実行するコールバック           |
| [FriendBlackListAddedCallback](https://comm.qq.com/im/doc/unity/zh/callback/FriendBlackListAddedCallback.html) | ブラックリストが追加された時に実行するコールバック           |
| [FriendBlackListDeletedCallback](https://comm.qq.com/im/doc/unity/zh/callback/FriendBlackListDeletedCallback.html) | ブラックリストが削除された時に実行するコールバック           |
| [LogCallback](https://comm.qq.com/im/doc/unity/zh/callback/LogCallback.html) | ログ関連のコールバック                                       |
| [MsgUpdateCallback](https://comm.qq.com/im/doc/unity/zh/callback/MsgUpdateCallback.html) | メッセージがクラウド側で変更されたことによってメッセージが更新されたことを通知した時に実行するコールバック |
| [MsgGroupMessageReadMemberListCallback](https://comm.qq.com/im/doc/unity/zh/callback/MsgGroupMessageReadMemberListCallback.html) | グループメッセージを既読したグループメンバーのリストを取得した時に実行するコールバック |

>! [`UserSigExpiredCallback`](https://comm.qq.com/im/doc/unity/zh/callback/UserSigExpiredCallback.html)コールバックを受信した場合、ログイン用のUserSig資格情報が期限切れになったため、新たに発行されたUserSigを使用して改めてログインしてください。期限切れのUserSigを引き続き使用すれば、IM SDKのログインが無限ループになります。

### 初期化解除
一般的には、ご利用のAppのライフサイクルはIM SDKのライフサイクルと同じで、Appを終了する前に、初期化を解除しなくてもかまいません。
ただし、運用シーンによって、IM SDKの初期化を解除する必要があります。例えば、特定のページに入ってからIM SDKを初期化し、そのページを終了してもう使用しなくなる場合。

初期化解除はワンステップだけで実施できます：それは、初期化解除インターフェース`unInit`の呼出しです([詳細はこちら](https://comm.qq.com/im/doc/unity/zh/api/IMSDKInit/Uninit.html))

サンプルコードは以下の通りです：

```c#
// SDKの初期化解除
TencentIMSDK.Uninit();
```
## その他
SDK呼出しの実行結果に、resがTIMResult.TIM_SUCC = 0の場合、インターフェースの呼出しに成功しました。

SDKの初期化に成功した直後に、必要なイベントリスナーを追加してください。これはメッセージ漏れを防ぐためです。

[](id:qa)

## よくある質問

[](id:qa1)

### 1. IM SDKのログイン、メッセージ、グループ、セッション、リレーショナルチェーン、プロフィール、シグナルなどの機能を使用する前に、初期化を実行する必要があります。
