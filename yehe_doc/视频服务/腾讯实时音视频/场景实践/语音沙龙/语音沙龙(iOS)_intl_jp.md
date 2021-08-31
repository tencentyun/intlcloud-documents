## デモンストレーション

[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)してDemoをインストールし、ボイスチャット、マイクのオン・オフ、低遅延音声インタラクションなどのボイスチャットのユースケースにおけるTRTCの関連機能を含む、ボイスサロンの機能を体験できます。

ボイスサロン機能をすばやく実装する必要がある場合、当社が提供するDemoをもとにアダプタを直接修正するか、または当社が提供するTRTCChatSalonコンポーネントでUIのカスタマイズを実装することができます。

[](id:DemoUI)

## DemoのUIの再利用

[](id:ui.step1)

### 手順1：アプリケーションの新規作成

1．TRTCコンソールにログインし、【開発支援】>【[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. アプリケーション名（例：`TestChatSalon`）を入力し、【作成】をクリックします。

>!本機能はTencent Cloud[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。



[](id:ui.step2)

### 手順2：SDKおよびDemoソースコードをダウンロード
1. 実際の業務ニーズに基づき、SDKおよび付属のDemoソースコードをダウンロードします。
2. ダウンロード完了後、【ダウンロードしました。次のステップ】をクリックします。


[](id:ui.step3)
### 手順3：Demoプロジェクトファイルの設定

1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h`のファイルを見つけて開きます。
3. `GenerateTestUserSig.h`のファイルの関連するパラメータを設定します。
<ul style="margin:0"><li/>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。
<li/>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</ul>

4. 貼り付け完了後、【貼り付けました。次のステップ】をクリックすれば、作成が完了します。
5. コンパイル完了後、【コンソール概要に戻る】をクリックすればOKです。

>!
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**のこの手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:ui.step4)

### 手順4：Demoの実行

Xcode（11.0およびそれ以降のバージョン）を使用してソースコードプロセス`iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace`を開き、【実行】をクリックすれば本Demoのデバッグを開始することができます。

[](id:ui.step5)

### 手順5：Demoソースコードの修正

ソースコードのTRTCChatSalonDemoフォルダは、uiとmodelの2つのサブフォルダを含んでいます。uiフォルダには、インターフェースコードとインターフェース関連のロジックが含まれています。以下の表にはそれぞれのswiftファイルまたはフォルダおよびそれらが対応するUIをリストアップして、二次調整を行いやすくしています。

| ファイルまたはフォルダ                      | 機能の説明                             |
| --------------------------------- | ------------------------------------ |
| NetworkRoomManager                | 業務バックエンドインタラクション関連。                   |
| TRTCCreateChatSalonViewController |ボイスチャットルームページのロジックを作成します。                   |
| TRTCChatSalonListViewController | リストページのロジック。 |
| TRTCChatSalonViewController | メインルームページ。キャスターおよび視聴者という2種類のインターフェースがあります。 |

[](id:model)

## カスタマイズUIの実装

[ソースコード](https://github.com/tencentyun/TUIChatSalon)のtrtcchatsalondemoフォルダには、uiとmodelという2つのサブフォルダがあり、modelフォルダには再利用できるオープンソースコンポーネントTRTCChatSalonが含まれています。`TRTCChatSalon.h`ファイルでこのコンポーネントが提供するインターフェース関数を確認し、対応するインターフェースを使用してカスタマイズしたUIを実装することができます。
![](https://main.qcloudimg.com/raw/7613bd7ec5b4e665f32ee5df69e5de85.png)

[](id:model.step1)

### 手順1：SDKへの統合

ボイスチャットコンポーネントTRTCChatSalonは、TRTC SDKとIM SDKに依存し、次の手順で2つのSDKをプロジェクトに統合することができます。

**方法1：cocoapodsリポジトリを介する依存**

```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```

>?2つのSDK製品の最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK)および[IM](https://github.com/tencentyun/TIMSDK)のGithubトップページで取得することができます。

**方法2：ローカルを介する依存**
開発環境でのcocoapodsリポジトリへのアクセスが遅い場合は、ZIPパッケージを直接ダウンロードし、統合ドキュメントに従って手動でプロジェクトに統合することができます。

| SDK      | ダウンロードページ                                                     | 統合ガイド                                                     |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| TRTC SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/647/34615) | [統合ドキュメント](https://intl.cloud.tencent.com/document/product/647/35092) |
| IM SDK   | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/1047/33996) | [統合ドキュメント](https://intl.cloud.tencent.com/document/product/1047/34307) |

[](id:model.step2)

### 手順2：権限の設定

`info.plist`ファイルに`Privacy > Camera Usage Description`、`Privacy > Microphone Usage Description`を追加し、マイクの権限を申請する必要があります。

[](id:model.step3)

### 手順3：TRTCChatSalonコンポーネントのインポート

`iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCChatSalonDemo/model`ディレクトリのすべてのファイルをプロジェクトにコピーします。


[](id:model.step4)

### 手順4：コンポーネントの作成およびログイン

1. TRTCChatSalonの`sharedInstance`クラスメソッドを呼び出すと、TRTCChatSalonのインスタンスを作成できます。
2. `setDelegate`メソッドを呼び出して、コンポーネントのイベントコールバック通知を登録します。
3. `login`メソッドを呼び出して、コンポーネントのログインを完了します。下表を参考にキーパラメータを入力してください。
<table>    
<tr><th>パラメータ名</th><th>機能</th></tr><tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a>でSDKAppIDを表示できます。</td>
</tr><tr>
<td>userId</td>
<td>現在のユーザーID。文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については、<a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSigの計算方法</a>をご参照ください。</td>
</tr></tr>
<tr>
<td>callback</td>
<td>ログインのコールバック。成功時にcodeは0になります。</td>
</tr></table>
<dx-codeblock>
::: Swift Swift
// Swift例
// コード内でビジネスロジックを担当するクラス
class YourController {
    // 属性を計算してシングルトンオブジェクトを取得
    var chatSalon: TRTCChatSalon {
        return TRTCChatSalon.shared()
    }
    

    // その他のコードロジック
    ......

}
// chatSalonプロキシの設定
self.chatSalon.setDelegate(delegate: self)

// 呼び出し方法は以下のとおりです。循環参照を防ぐために、クロージャでweak selfを使用することをお勧めします（以下のサンプルコードでは、weak self例を省略）
self.chatSalon.login(sdkAppID: sdkAppID, userID: userId, userSig: userSig) { [weak self] (code, message) in
    guard let `self` = self else { return }
    // コールバックビジネスロジック        
}
:::
</dx-codeblock>

[](id:model.step5)

### 手順5：キャスター側での配信開始

1. キャスターは、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. キャスターは、`createRoom`を呼び出して新しいボイスサロンを作成します。このとき、ルームID、マイク・オンに管理者の確認の要否、ルームタイプなどルームの属性情報を渡します。
3. キャスターは、メンバーが参加した`onAnchorEnterSeat`のイベント通知を受信します。このとき、マイク集音は自動的に開始されます。

![](https://main.qcloudimg.com/raw/dfe6ed5d0c973e399e834eb233c96ec6.png)

<dx-codeblock>
::: Swift Swift
// 1.キャスターは、ニックネームおよびプロフィール画像を設定します
self.chatSalon.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // 結果のコールバック           
}


// 2.キャスター側でルームを作成します
let param = ChatSalonParam.init()
Param.roomName = 「ルーム名」
param.needRequest = true // 視聴者のマイク・オンに対するキャスターの同意の要否
param.coverUrl = 「カバーURL」
param.seatInfoList = []
self.chatSalon.createRoom(roomID: yourRoomID, roomParam: param) { (code, message) in
    guard code == 0 else { reutrn }
    // 3.ルーム作成成功後、席の占有を開始
    self.chatSalon.enterSeat { [weak self] (code, message) in
        guard let `self` = self else { return }
        if code == 0 {
            // 管理者による席の占有成功
        } else {
            // 管理者による席の占有失敗
        }
    }
}

// 4. 席の占有の成功後、onAnchorEnterSeatイベント通知を受信します
func onAnchorEnterSeat(user: ChatSalonUserInfo) {
}
:::
</dx-codeblock>


[](id:model.step6)

### 手順6：視聴者側の視聴

1. 視聴者側は、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. 視聴者側は、業務バックエンドから最新のボイスサロンのルームリストを取得します。
 >?Demoのボイスサロンリストは、デモンストレーションでの使用のみです。ボイスサロンリストのビジネスロジックは様々です。Tencent Cloudでは現在、ボイスサロンリストの管理サービスを提供していませんので、ご自身でボイスサロンリストを管理してください。
3. 視聴者側は、`getRoomInfoList`を呼び出してルームの詳細情報を取得します。この情報は、キャスター側が`createRoom`を呼び出してボイスサロンを作成するときに設定する簡単な説明情報です。
 >!ボイスサロンリストに十分に包括的な情報がある場合は、`getRoomInfoList`の呼び出しに関する手順をスキップできます。
4．視聴者は一つのボイスサロンを選択し、`enterRoom`を呼び出してルームナンバーを渡すと、そのルームに参加できます。
5. 入室後、コンポーネントの`onRoomInfoChange`というルーム属性の変更イベント通知を受信します。このとき、ルーム属性を記録し、UIに表示されるルーム名、マイク・オンにキャスターへの同意のリクエストの要否の記録など、対応する変更を行うことができます。
6. 入室後にマイクリストにキャスターが参加した`onAnchorEnterSeat`のイベント通知も受信します。

![](https://main.qcloudimg.com/raw/dfe6ed5d0c973e399e834eb233c96ec6.png)

<dx-codeblock>
::: Swift Swift
// 1.視聴者は、ニックネームおよびプロフィール画像を設定します
self.chatSalon.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // 結果のコールバック           
}

// 2.業務バックエンドから取得したルームリストをroomListと仮定します
let roomList: [Int] = getRoomIDList() // ルームIDリストを取得する関数

// 3.getRoomInfoListを呼び出すことによって、ルームの詳細情報を取得します
self.chatSalon.getRoomInfoList(roomIdList: roomIdsInt) { (code, message, roomInfos: [ChatSalonInfo]) in
    //結果の取得。この時、UIの更新が可能
}

// 4.roomidを渡してルームに参加します
self.chatSalon.enterRoom(roomID: roomInfo.roomID) { (code, message) in
    // 入室結果コールバック
    if code == 0 {
       // 入室に成功
    }
}

// 5.入室に成功後、onRoomInfoChangeイベント通知を受信します
func onRoomInfoChange(roomInfo: ChatSalonInfo) {
    // ルーム名などの情報の更新可
}

// 6. onAnchorEnterSeatイベント通知を受信します
func onAnchorEnterSeat(user: ChatSalonUserInfo) {
    // マイク・オンイベントの処理
}
:::
</dx-codeblock>

[](id:model.step7)

### 手順7：マイクのオン・オフ

<dx-tabs>
::: キャスター側

1. `pickSeat`は、視聴者のuserIdを渡し、ピックしてマイク・オンにできます。ルーム内の全メンバーは`onAnchorEnterSeat`のイベント通知を受信します。
2. `kickSeat`は、対応するユーザーのuserIdを渡し、キックアウトしてマイク・オフできます。ルーム内の全メンバーは`onAnchorEnterSeat`のイベント通知を受信します。

![](https://main.qcloudimg.com/raw/d968f479f51160f626d07ce8bf403f13.png)


マイク操作後のイベント通知の順番は次のとおりです。callback > onAnchorEnterSeatなど独立したイベント。

<dx-codeblock>
::: Swift Swift
// 1.キャスターがピックしてマイク・オンにします
self.chatSalon.pickSeat(userID: "123") { (code, message) in
    // 2. callbackコールバックを受信します
}

// 3.キャスターはマイク通知に進むと、ここで視聴者が適切な処理を行っているかどうかを判断することができます
func onAnchorEnterSeat(user: ChatSalonUserInfo) {
    // マイク・オンイベントの処理
}
:::
</dx-codeblock>

:::
::: 視聴者側

1. `enterSeat`はマイク・オンにし、ルーム内の全メンバーは`onAnchorEnterSeat`のイベント通知を受信します。
2. `leaveSeat`は自主的にマイク・オフにし、ルーム内の全メンバーは`onAnchorLeaveSeat`のイベント通知を受信します。

![](https://main.qcloudimg.com/raw/c9611b5017536604f63333ce7c19c309.png)

マイク操作後のイベント通知の順番は次のとおりです。callback > onAnchorEnterSeatなど独立したイベント。
<dx-codeblock>
::: Swift Swift
// 1.視聴者が自主的にマイク・オンにします
self.chatSalon.enterSeat { (code, message) in
    // 2. callbackコールバックを受信します
}

// 3.キャスターはマイク通知に進むと、ここで自分が適切な処理を行っているかどうかを判断することができます
func onAnchorEnterSeat(user: ChatSalonUserInfo) {
    // マイク・オンイベントの処理
}
:::
</dx-codeblock>
:::
</dx-tabs>


[](id:model.step8)

### 手順8：招待シグナリングの使用

Appが次の操作の業務フローを実施するために、相手の同意を必要とする場合、招待シグナリングによって対応するサポートを提供することができます。

<dx-tabs>
::: 視聴者からの自主的なマイク申請

1. 視聴者側は、`sendInvitation`を呼び出してキャスターのuserIdおよび業務のカスタムコマンドワードなどを渡します。この時、関数は1個のinviteIdを返しこのinviteIdを記録します。
2. キャスター側は、`onReceiveNewInvitation`のイベント通知を受信します。この時、UIはウィンドウをポップアップして、キャスターに同意するかどうか照会することができます。
3. キャスターが同意を選択後、`acceptInvitation`を呼び出してinviteIdを渡します。
4. 視聴者側は、`onInviteeAccepted`のイベント通知を受信し、`enterSeat`を呼び出してマイク・オンにします。

![](https://main.qcloudimg.com/raw/3543bf768896cfd78b0163dc9378e659.png)

<dx-codeblock>
::: Swift Swift
// 視聴者側の視点
// 1. sendInvitationを呼び出し、マイク・オンをリクエストします
let inviteId = self.chatSalon.sendInvitation(cmd: "ENTER_SEAT", userID: ownerUserId, content: "1") { (code, message) in
    // 送信結果のコールバック
}
// 2.招待の同意リクエストを受信して、正式にマイク・オンにします
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.chatSalon.enterSeat { (code, message) in
            // マイク・オン結果のコールバック
        }
    }
}

// キャスター側の視点
// 1.キャスターがリクエストを受信します
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "ENTER_SEAT" {
        // 2.キャスターが視聴者のリクエストに同意します
        self.chatSalon.acceptInvitation(identifier: identifier, callback: nil)
    }
}
:::
</dx-codeblock>
:::
::: キャスターから視聴者を招待してマイク・オン

1. キャスター側は、`sendInvitation`を呼び出して視聴者のuserIdおよび業務のカスタマイズコマンドワードなどを渡します。この時、関数は1個のinviteIdを返しこのinviteIdを記録します。
2. 視聴者側は、`onReceiveNewInvitation`のイベント通知を受信します。この時、UIはウィンドウをポップアップして、視聴者がマイク・オンに同意するかどうかを照会することができます。
3. 視聴者が同意を選択後、`acceptInvitation`を呼び出してinviteIdを渡します。
4. キャスター側は、`onInviteeAccepted`のイベント通知を受信し、`pickSeat`を呼び出し、視聴者をピックしてマイク・オンにします。

![](https://main.qcloudimg.com/raw/60025544abae69e22de22a4b81bf6951.png)


<dx-codeblock>
::: Swift Swift
// キャスター側の視点
// 1.キャスターはsendInvitationを呼び出して、視聴者123をピックしてマイク・オンをリクエストします
let inviteId = self.chatSalon.sendInvitation(cmd: "PICK_SEAT", userID: ownerUserId, content: "2") { (code, message) in
    // 送信結果のコールバック
}

// 2.招待の同意リクエストを受信して、正式にマイク・オンにします
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.chatSalon.pickSeat(userID: ) { (code, message) in
            // マイク・オン結果のコールバック
        }
    }
}

// 視聴者側の視点
// 1.視聴者がリクエストを受信します
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "PICK_SEAT" {
        // 2.視聴者がキャスターのリクエストに同意します
        self.chatSalon.acceptInvitation(identifier: identifier, callback: nil)
    }
}
:::
</dx-codeblock>
:::
</dx-tabs>


[](id:model.step9)

### 手順9：文字チャットおよび弾幕コメントの実装

- `sendRoomTextMsg`によって通常のテキストメッセージを送信できるようになり、該当するルーム内の全てのキャスターおよび視聴者が`onRecvRoomTextMsg`のコールバックを受信することができます。
  IMバックエンドは、デフォルトのセンシティブワードフィルタルールを備えており、センシティブワードと認識されたテキストメッセージはクラウドに転送されることはありません。
  <dx-codeblock>
  ::: Swift Swift
  // 送信側：テキストメッセージの送信
  self.chatSalon.sendRoomTextMsg(message: message) { (code, message) in
        

}
// 受信側：テキストメッセージの監視
func onRecvRoomTextMsg(message: String, userInfo: ChatSalonUserInfo) {
    // 受信したmessage情報の処理方法        
}
:::
</dx-codeblock>

- `sendRoomCustomMsg`によってカスタマイズ（シグナリング）情報を送信することができます。そのルーム内のすべてのキャスターおよび視聴者は`onRecvRoomCustomMsg`のコールバックを受信することができます。
  カスタムメッセージは、カスタマイズ信号の送信によく用いられます。例えば、「いいね」情報の発信やブロードキャストに使用します。
  <dx-codeblock>
  ::: Swift Swift
  // 例：送信側：カスタマイズCmdによって、弾幕と「いいね」情報を区分することができます
  // eg:「CMD_DANMU」は弾幕コメントを表し、「CMD_LIKE」は「いいね」情報を表します
  self.chatSalon.sendRoomCustomMsg(cmd: "CMD_DANMU", message: "hello world", callback: nil)
  self.chatSalon.sendRoomCustomMsg(cmd: "CMD_LIKE", message: "", callback: nil)
  // 受信側：カスタムメッセージの監視
  func onRecvRoomCustomMsg(cmd: String, message: String, userInfo: ChatSalonUserInfo) {
    if cmd == "CMD_DANMU" {
        // 弾幕コメントの受信
    }
    if cmd == "CMD_LIKE" {
        // 「いいね」情報の受信
    }
  }
  :::
  </dx-codeblock>
