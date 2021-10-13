[](id:DemoUI)

## AppのUIの再利用

[](id:ui.step1)

### 手順1：アプリケーションの新規作成

1. TRTCコンソールにログインし、 **開発支援** > **[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)**を選択します。
2. アプリケーション名（例：`TestChatSalon`）を入力し、**作成**をクリックします。
3. **ダウンロードしました。次のステップ**をクリックすると、この手順をスキップします。

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>!本機能はTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。



[](id:ui.step2)

### 手順2：Appソースコードのダウンロード
クリックして[TUIChatSalon](https://github.com/tencentyun/TUIChatSalon)に進み、ソースコードをCloneまたはダウンロードします。

[](id:ui.step3)
### 手順3：Appプロジェクトファイルの設定

1. 設定変更ページに進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `TUIChatSalon/Debug/GenerateTestUserSig.swift`ファイルを見つけて開きます。
3. `GenerateTestUserSig.swift`ファイル内の関連パラメータを設定します。
<ul style="margin:0"><li/>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。
<li/>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</ul>
4. 貼り付け完了後、**貼り付けました。次のステップ**をクリックすれば、作成が完了します。
5. コンパイル完了後、 **コンソール概要に戻る** をクリックすれば終了です。

>!
>- ここで言及するUserSigの発行方法は、クライアントコードの中でのSECRETKEY設定となりますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者がお客様のTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのAppクイックスタートおよび機能デバッグにのみ適しています**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを送信し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:ui.step4)

### 手順4：Appの実行

Xcode（11.0およびそれ以降のバージョン）を使用してソースコードプロセス`TUIChatSalon/TUIChatSalonApp.xcworkspace`を開き、 **実行**をクリックすれば、このAppのデバッグが開始されます。

[](id:ui.step5)

### 手順5：Appソースコードの修正

ソースコードの`Source`フォルダは、uiとmodelの2つのサブフォルダを含んでいます。uiフォルダには、インターフェースコードとインターフェース関連のロジックが含まれています。以下の表にはそれぞれのswiftファイルまたはフォルダおよびそれらが対応するUIをリストアップして、二次調整を行いやすくしています。

| ファイルまたはフォルダ                      | 機能の説明                             |
| --------------------------------- | ------------------------------------ |
| TRTCChatSalonEnteryControl.swift  | このファイルには、すべてのViewController初期化メソッドが含まれています。このインスタンスを介してViewControllerオブジェクトをすばやく取得することができます。                 |
| TRTCCreateChatSalonViewController | ルーム作成ページのロジックを作成します。                   |
| TRTCChatSalonViewController | メインルームページ。管理者およびリスナーという2種類のインターフェースがあります。 |

## アプリケーション体験
>! 体験アプリケーションには、少なくとも2台のデバイスが必要です。

### ユーザーA

1. ユーザー名を入力し（**ユーザー名は一意のものとし、他のユーザーと重複しないようにしてください**）、ログインします。
2. **ルームの作成**をクリックします。
3. ルームトピックを入力し、**チャット開始**をクリックします。

### ユーザーB
1. ユーザー名を入力し（**ユーザー名は一意のものとし、他のユーザーと重複しないようにしてください**）、ログインします。
2. ユーザーAが作成したルーム番号を入力し、**入室する**をクリックします。

>! ルーム番号はユーザーAのルーム上部に表示されます。


[](id:model)
## カスタムUIの実装

[ソースコード](https://github.com/tencentyun/TUIChatSalon)の`Source`フォルダには、uiとmodelという2つのサブフォルダがあり、modelフォルダには再利用できるオープンソースコンポーネントTRTCChatSalonが含まれています。`TRTCChatSalon.h`ファイルでこのコンポーネントが提供するインターフェース関数を確認し、対応するインターフェースを使用してカスタマイズしたUIを実装することができます。
![](https://main.qcloudimg.com/raw/7613bd7ec5b4e665f32ee5df69e5de85.png)

[](id:model.step1)

### 手順1：SDKへの統合

ボイスサロンコンポーネントTRTCChatSalonは、TRTC SDKとIM SDKに依存し、次の手順で2つのSDKをプロジェクトに統合することができます。

- **方法1：cocoapodsリポジトリを介する依存**
<dx-codeblock>
::: swift
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
:::
</dx-codeblock>
>?2つのSDK製品の最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK)および[IM](https://github.com/tencentyun/TIMSDK)のGitHubトップページで取得することができます。
- **方法2：ローカルを介する依存**
開発環境でのcocoapodsリポジトリへのアクセスが遅い場合は、ZIPパッケージを直接ダウンロードし、統合ドキュメントに従って手動でプロジェクトに統合することができます。
<table>
<tr><th>SDK</th><th>ダウンロードページ</th><th>統合ガイド</th></tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35092">統合ドキュメント</a></td>
</tr><tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34307">統合ドキュメント</a></td>
</tr></table>

[](id:model.step2)
### 手順2：権限の設定
`info.plist`ファイルに`Privacy > Camera Usage Description`、`Privacy > Microphone Usage Description`を追加し、マイクの権限を申請する必要があります。

[](id:model.step3)
### 手順3：TUIChatSalonコンポーネントのインポート
**cocoapodsを介してコンポーネントをインポートします**。具体的な操作は次のとおりです。
1. プロジェクトディレクトリ下の`Source`、`Resources`、`TXAppBasic`フォルダ、`TUIChatSalon.podspec`ファイルをプロジェクトディレクトリ下へコピーします。
2. `Podfile`ファイル内に以下の依存関係を追加します。その後、`pod install`コマンドを実行すると、インポートが完了します。
<dx-codeblock>
::: swift
pod 'TXAppBasic', :path => "TXAppBasic/"
pod 'TXLiteAVSDK_TRTC'
pod 'TUIChatSalon', :path => "./", :subspecs => ["TRTC"] 
:::
</dx-codeblock>

[](id:model.step4)
### 手順4：コンポーネントの作成およびログイン
1. TRTCChatSalonの`sharedInstance`クラスメソッドを呼び出すと、TRTCChatSalonのインスタンスオブジェクトを作成できます。
2. `setDelegate`メソッドを呼び出して、コンポーネントのイベントコールバック通知を登録します。
3. `login`メソッドを呼び出して、コンポーネントのログインを完了します。下表を参考にキーパラメータを入力してください。
<table>    
<tr><th>パラメータ名</th><th>機能</th></tr><tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a> で SDKAppIDを表示できます。</td>
</tr><tr>
<td>userId</td>
<td>現在のユーザーID、文字列タイプでは、英語のアルファベット（a-z と A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。</td>
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

### 手順5：管理者側での配信開始

1. 管理者は、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. 管理者は、`createRoom`を呼び出して新しいボイスサロンを作成します。この時、ルームID、マイク・オンにすることの管理者の確認の要否、ルームタイプなどルームの属性情報を渡します。
3. 管理者は、メンバーが参加した`onAnchorEnterSeat`というイベント通知を受信します。この時、マイク集音は自動的に開始されます。

![](https://main.qcloudimg.com/raw/dfe6ed5d0c973e399e834eb233c96ec6.png)
<dx-codeblock>
::: Swift Swift
// 1.管理者は、ニックネームおよびプロフィール画像を設定します
self.chatSalon.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // 結果のコールバック           
}


// 2.管理者側でルームを作成します
let param = ChatSalonParam.init()
Param.roomName = 「ルーム名」
param.needRequest = true // リスナーのマイク・オンに対する管理者の同意の要否
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

### 手順6：リスナー側の視聴

1. リスナー側は、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. リスナー側は、業務バックエンドから最新のボイスサロンのルームリストを取得します。
>?Appのボイスサロンリストは、デモンストレーション用のためだけのものです。ボイスサロンリストのビジネスロジックは様々です。Tencent Cloudでは現在ボイスサロンリストの管理サービスを提供していません。ご自身でボイスサロンリストを管理してください。
3. リスナー側は`getRoomInfoList`を呼び出して、ルームの詳細情報を取得します。この情報は、管理者側が`createRoom`を呼び出してボイスサロンを作成するときに設定する簡単な説明情報です。
>!ボイスサロンリストに十分に包括的な情報がある場合は、`getRoomInfoList`の呼び出しに関する手順をスキップできます。
4. リスナーはボイスサロンの1つを選択し、`enterRoom`を呼び出してルームナンバーを渡すと、そのルームに参加できます。
5. 入室後、コンポーネントの`onRoomInfoChange` ルーム属性変更イベント通知を受信します。この時、ルーム属性を記録し、それに応じた修正を行うことができます。例：UIに表示するルーム名、発言者にする際の管理者への同意リクエストの要否の記録など。
6. 入室後にマイクリストにキャスターが参加した`onAnchorEnterSeat`というイベント通知も受信します。

![](https://main.qcloudimg.com/raw/6fbabfa4e217022cf3d05677e4a45538.png)
<dx-codeblock>
::: Swift Swift
// 1.リスナーは、ニックネームおよびプロフィール画像を設定します
self.chatSalon.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // 結果のコールバック           
}

// 2.業務バックエンドから取得したルームリストをroomListと仮定します
let roomList: [Int] = getRoomIDList() // ルームIDリストを取得する関数

// 3.getRoomInfoListを呼び出すことによって、ルームの詳細情報を取得します
self.chatSalon.getRoomInfoList(roomIdList: roomIdsInt) { (code, message, roomInfos: [ChatSalonInfo]) in
    //結果の取得。この時、UIの更新が可能
}

// 4.roomIdを渡してルームに参加します
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
::: 管理者側

1. `pickSeat`は、リスナーのuserIdを渡し、発言できるように視聴者を招待できます。ルーム内の全メンバーは`onAnchorEnterSeat`というイベント通知を受信します。
2. `kickSeat`で該当するユーザーのuserIdを渡すと、その人をキックアウトしてマイク・オフにできます。ルーム内の全メンバーが`onAnchorLeaveSeat`というイベント通知を受信します。

![](https://main.qcloudimg.com/raw/d968f479f51160f626d07ce8bf403f13.png)

マイク操作後のイベント通知の順番は次のとおりです。callback > onAnchorEnterSeatなど独立したイベント。

<dx-codeblock>
::: Swift Swift
// 1.管理者が、視聴者を発言できるように招待できます
self.chatSalon.pickSeat(userID: "123") { (code, message) in
    // 2. callbackコールバックを受信します
}

// 3.リスナーがキャスターとしてマイク通知に進むと、リスナーが実際にマイク・オンに成功したかどうかを判断できます
func onAnchorEnterSeat(user: ChatSalonUserInfo) {
    // マイク・オンイベントの処理
}
:::
</dx-codeblock>

:::
::: リスナー側

1. `enterSeat`でマイク・オンにすることができます。ルーム内の全メンバーが `onAnchorEnterSeat`というイベント通知を受信します。
2. `leaveSeat`でユーザーが視聴者になります。ルーム内の全メンバーが`onAnchorLeaveSeat`というイベント通知を受信します。

![](https://main.qcloudimg.com/raw/c9611b5017536604f63333ce7c19c309.png)
マイク操作後のイベント通知の順番は次のとおりです。callback > onAnchorEnterSeatなど独立したイベント。
<dx-codeblock>
::: Swift Swift
// 1.リスナーがユーザーを発言者にします
self.chatSalon.enterSeat { (code, message) in
    // 2. callbackコールバックを受信します
}

// 3.リスナーがキャスターとしてマイク通知に進むと、ここで自分が適切な処理を行っているかどうかを判断することができます
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
::: リスナーからの自主的なマイク・オン申請

1. リスナー側が`sendInvitation`を呼び出し、管理者のuserIdおよび業務のカスタムコマンドワードなどを渡します。この時、関数が1つのinviteIdを返しますので、このinviteIdを記録します。
2. 管理者側は、`onReceiveNewInvitation`というイベント通知を受信します。この時UIでウィンドウをポップアップさせ、管理者に同意の有無をたずねることができます。
3. 管理者が同意を選択後、`acceptInvitation`を呼び出してinviteIdを渡します。
4. リスナー側は、`onInviteeAccepted`というイベント通知を受信し、`enterSeat`を呼び出してマイク・オンにします。

![](https://main.qcloudimg.com/raw/71b657c495cb52317c4c32a919407b36.png)
<dx-codeblock>
::: Swift Swift
// リスナー側の視点
// 1.sendInvitationを呼び出し、マイク・オンをリクエストします
let inviteId = self.chatSalon.sendInvitation(cmd: "ENTER_SEAT", userID: ownerUserId, content: "1") { (code, message) in
    // 送信結果のコールバック
}
// 2.招待のリクエスト同意を受信し、正式にマイク・オンになります
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.chatSalon.enterSeat { (code, message) in
            // マイク・オン結果のコールバック
        }
    }
}

// 管理者側の視点
// 1.管理者がリクエストを受信します
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "ENTER_SEAT" {
        // 2.管理者がリスナーのリクエストに同意します
        self.chatSalon.acceptInvitation(identifier: identifier, callback: nil)
    }
}
:::
</dx-codeblock>
:::
::: 管理者からの招待によるリスナーのマイク・オン

1. 管理者側が`sendInvitation`を呼び出し、リスナーのuserIdおよび業務のカスタムコマンドワードなどを渡します。この時、関数が1つのinviteIdを返しますので、このinviteIdを記録します。
2. リスナー側は、`onReceiveNewInvitation`というイベント通知を受信します。この時UIでウィンドウをポップアップさせ、リスナーに同意の有無をたずねることができます。
3. リスナーが同意を選択後、`acceptInvitation`を呼び出してinviteIdを渡します。
4. 管理者側は、`onInviteeAccepted`というイベント通知を受信し、`pickSeat`を呼び出しリスナーをピックしてマイク・オンにします。

![](https://main.qcloudimg.com/raw/60025544abae69e22de22a4b81bf6951.png)

<dx-codeblock>
::: Swift Swift
// 管理者側の視点
// 1.管理者はsendInvitationを呼び出して、リスナー「123」をピックしてマイク・オンをリクエストします
let inviteId = self.chatSalon.sendInvitation(cmd: "PICK_SEAT", userID: ownerUserId, content: "2") { (code, message) in
    // 送信結果のコールバック
}

// 2.招待のリクエスト同意を受信し、正式にマイク・オンになります
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.chatSalon.pickSeat(userID: ) { (code, message) in
            // マイク・オン結果のコールバック
        }
    }
}

// リスナー側の視点
// 1.リスナーがリクエストを受信します
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "PICK_SEAT" {
        // 2.リスナーが管理者のリクエストに同意します
        self.chatSalon.acceptInvitation(identifier: identifier, callback: nil)
    }
}
:::
</dx-codeblock>
:::
</dx-tabs>


[](id:model.step9)

### 手順9：文字チャットおよび弾幕コメントの実装

- `sendRoomTextMsg`によって通常のテキストメッセージを送信できるようになり、このルーム内のすべてのキャスターおよびリスナーが`onRecvRoomTextMsg`のコールバックを受信することができます。
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

- `sendRoomCustomMsg`によって、カスタム（シグナリング）メッセージを送信できます。当該ルーム内のすべてのキャスターとリスナーが`onRecvRoomCustomMsg`コールバックを受信できます。
  カスタムメッセージは、カスタムシグナリングの送信によく用いられます。例えば、「いいね」情報の発信やブロードキャストに使用します。
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
