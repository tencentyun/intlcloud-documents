## デモンストレーション
[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)からDemoをインストールして、マイク管理、低レイテンシー音声インタラクション、文字チャットなどのボイスチャットのユースケースにおけるTRTCの関連機能を含む、ボイスチャットルームの機能を体験できます。

ボイスチャットルーム機能をすばやく実装する必要がある場合は、当社が提供するDemoをもとに直接適応に変更を加えることも、当社が提供するTRTCVoiceRoomコンポーネントでUIのカスタマイズを実装することも可能です。

[](id:DemoUI)
## DemoのUIの再利用

[](id:ui.step1)
### 手順1：アプリケーションの新規作成
1．TRTCコンソールにログインし、【開発支援】>【[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. 例えば、`TestLiveRoom`などアプリケーション名を入力して、【作成】をクリックします。

>?本機能はTencent Cloud[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047)という2つの基本的なPAASサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの価格説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。



[](id:ui.step2)
### 手順2：SDKおよびDemoソースコードをダウンロード
1. 実際の業務ニーズに基づき、SDKおよび付属のDemoソースコードをダウンロードします。
2. ダウンロード完了後、【ダウンロードしました。次のステップ】をクリックします。

[](id:ui.step3)
### 手順3：Demoプロジェクトファイルの設定
1. 設定変更画面に入り、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h`のファイルを見つけて開きます。
3. `GenerateTestUserSig.h`のファイルの関連するパラメータを設定します。
-SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。
-SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。
![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
4. 貼り付け完了後、【貼り付けました。次のステップ】をクリックすれば、作成が完了します。
5. コンパイル完了後、【コンソール概要に戻る】をクリックすればOKです。

>!ここで言及した新規UserSigの作成法は、クライアントコードでSECRETKEYを設定し、この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適しています**。
≻ UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:ui.step4)
### 手順4：Demoの実行
Xcode（11.0以上のバージョン）を使用してソースコードプロセス`iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace`を開き、【実行】をクリックすれば、このDemoのデバッグが開始されます。

[](id:ui.step5)
### 手順5：Demoソースコードの修正
ソースコードのTRTCVoiceRoomDemoフォルダは、uiとmodelの2つのサブフォルダを含んでいます。uiフォルダには、インターフェースコードとインターフェース関連のロジックが含まれています。以下の表にはそれぞれのswiftファイルまたはフォルダ及びそれらが対応するUIをリストアップして、二次調整を行いやすくしています。

| ファイルまたはフォルダ | 機能説明 |
|:-------:|:--------|
|TRTCVoiceRoomEnteryController|このフォルダはすべてのViewControllerの初期化取得方法を含んでおり、このインスタンスによってすばやくViewControllerオブジェクトを取得できます。|
| NetworkRoomManager | 業務バックエンドインタラクション関連。 |
| TRTCCreateVoiceRoomViewController | ボイスチャットルームページのロジックを作成します。 |
| TRTCVoiceRoomListViewController | リストページのロジック。 |
| TRTCVoiceRoomViewController | メインルームページ。キャスターおよび視聴者という2種類のインターフェースがあります。 |

各`TRTC'XXXX'ViewController`フォルダには、`ViewController`、`RootView`および`ViewModel`が含まれ、各ファイルの役割は下表に示すとおりです。

| ファイル | 機能説明 |
|:-------:|:--------|
| ViewController | ページコントローラ。画面のルーティング作業、RootViewおよびViweModelのバインディング作業を担当します。 |
| RootView | ビュー。すべてのビューのレイアウト。 |
| ViewModel | ビューコントローラ。ビューのインタラクションに応答し、ビューの応答ステータスを返す作業を担当します。 |

[](id:model)
## UIカスタマイズの実現
[ソースコード](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCVoiceRoomDemo)のtrtcvoiceroomdemoフォルダには、uiとmodelの2つのサブフォルダがあり、modelフォルダには再利用できるオープンソースコンポーネントTRTCVoiceRoomがあります。`TRTCVoiceRoom.swift`ファイルでこのコンポーネントが提供するインターフェース関数を見て、対応するインターフェースを使用してUIのカスタマイズ を実装することができます。
![](https://main.qcloudimg.com/raw/319beb14d72a43120e102380278aa1da.png)


[](id:model.step1)
### 手順1：SDKへの統合
ボイスチャットコンポーネントTRTCVoiceRoomは、TRTC SDKとIM SDKに依存し、次の手順で2つのSDKをプロジェクトに統合することができます。

**方法1：cocoapodsリポジトリを介する依存**
```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```
>?2つのSDK製品の最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK)および[IM](https://github.com/tencentyun/TIMSDK)のGithubトップページで取得することができます。

**方法2：ローカルを介する依存**
開発環境でのcocoapodsリポジトリへのアクセスが遅い場合は、ZIPパッケージを直接ダウンロードし、統合ドキュメントに従って手動でプロジェクトに統合することができます。

| SDK | ダウンロードページ | ガイドの統合 |
|---------|---------|---------|
| TRTC SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/647/34615) | [統合ドキュメント](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/1047/33996) | [統合ドキュメント](https://intl.cloud.tencent.com/document/product/1047/34306) |

[](id:model.step2)
### 手順2：権限の設定
info.plistファイルにPrivacy > Camera Usage Description、Privacy > Microphone Usage Descriptionを追加し、カメラとマイクの権限をリクエストする必要があります。

[](id:model.step3)
### 手順3：TRTCVoiceRoomコンポーネントをインポート
`iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCVoiceRoomDemo/model`ディレクトリのすべてのファイルをプロジェクトにコピーします。

<span id="model.step4"></span>
### 手順4：コンポーネントの作成およびログイン
1. TRTCVoiceRoomImpの`sharedInstance`クラスメソッドを呼び出せば、TRTCVoiceRoomプロトコルを遵守するインスタンスオブジェクトを作成できます。`shared`クラスメソッドを呼び出しTRTCVoiceRoomImpインスタンスオブジェクトを取得して直接使用することもできます。両者は、TRTCVoiceRoomのインターフェースの使用において何の違いもありません。
2. `setDelegate`関数を呼び出してコンポーネントのイベントコールバック通知を登録します。
3. `login`関数を呼び出してコンポーネントのログインを完了します。下表を参考にキーパラメータを入力してください。
<table>    
<tr><th>パラメータ名</th><th>機能</th></tr><tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a> でSDKAppIDを表示できます。</td>
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

```
// Swift例
// コード内でビジネスロジックを担当するクラス
class YourController {
    // 属性を計算してシングルトンオブジェクトを取得
    var voiceRoom: TRTCVoiceRoomImp {
        return TRTCVoiceRoomImp.shared()
    }
    
    // その他のコードロジック
    ......
}
// voiceroomプロキシの設定
self.vocieRoom. setDelegate(delegate: voiceRoomDelegate)

// 呼び出し方法は以下のとおりです。循環参照を防ぐために、クロージャでweak selfを使用することをお勧めします（以下のサンプルコードでは、weak self例を省略）
self.vocieRoom.login(sdkAppId: sdkAppID, userId: userId, userSig: userSig) { [weak self] (code, message) in
    guard let `self` = self else { return }
    // コールバックビジネスロジック        
}
```

[](id:model.step5)
### 手順5：キャスター側での配信開始
1. キャスターは、[手順4](#model.step4) でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. キャスターは、`createRoom`を呼び出して新しいボイスチャットルームを作成します。この時にルームID、マイク・オンに管理者の確認の要否、マイク数などルームの属性情報を伝達します。
3. キャスターは、ルームの作成成功後、`enterSeat`を呼び出して参加します。
4. キャスターは、コンポーネントの`onSeatListChange`マイクリスト変更イベント通知を受信します。この時、マイクリストの変更をUI上に更新することができます。
5. キャスターは、マイクリストのメンバーが参加した`onAnchorEnterSeat`のイベント通知も受信します。この時はマイク集音は自動的に開始されます。

![](https://main.qcloudimg.com/raw/256ebe5ce1426b3f175c8c8b68095d5b.png)

サンプルコード：

```swift
// 1.キャスターは、ニックネームおよびプロフィール画像を設定します。
self.voiceRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // 結果のコールバック           
}



// 2.キャスター側でルームを作成します
let param = VoiceRoomParam.init()
param.roomName = "ルーム名"
param.needRequest = true // 視聴者のマイク・オンに対するキャスターの同意の要否
param.coverUrl = "カバーURL"
param.seatCount = 7; // ルームの座席数。ここは計7席あり、管理者が1席を占有した後、残り6席は視聴者が占有します
param.seatInfoList = []
for _ in 0..<param.seatCount {
    let seatInfo = VoiceRoomSeatInfo.init()
    param.seatInfoList.append(seatInfo)
}
self.voiceRoom.createRoom(roomID: yourRoomID, roomParam: param) { (code, message) in
    guard code == 0 else { reutrn }
    // ルーム作成成功後、席の占有を開始
    self.voiceRoom.enterSeat(seatIndex: 0) { [weak self] (code, message) in
        guard let `self` = self else { return }
        if code == 0 {
            // 管理者による席の占有成功
        } else {
            // 管理者による席の占有失敗
        }
    }
}



// 3.席の占有に成功した後、onSeatListChangeイベント通知を受信します
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // マイクリストの更新
}



// 4. onAnchorEnterSeatイベント通知を受信します
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // キャスターのマイク・オンイベントの処理
}
```

[](id:model.step6)
### 手順6：視聴者側の視聴
1. 視聴者側は、[手順4](#model.step4)でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. 視聴者側は、業務バックエンドに最新のボイスチャットルームのルームリストを取得します。
 >?Demoのボイスチャットルームリストは、デモンストレーションでの使用のみです。ボイスチャットルームリストのビジネスロジックは様々です。Tencent Cloudは、ボイスチャットのルームリスト管理サービスを一時的に提供しませんので、自身でボイスチャットのルームリストを管理してください。
3. 視聴者側は、`getRoomInfoList`を呼び出してルームの詳細情報を取得します。この情報は、キャスター側が`createRoom`を呼び出してボイスチャットルームを作成するときに設定する簡単な説明情報です。
 >!ボイスチャットルームのリストに十分で全体的な情報がある場合は、`getRoomInfoList`の呼び出しに関する手順をスキップできます。
4．視聴者は一つのボイスチャットルームを選択し、`enterRoom`を呼び出してルームナンバーを渡すと、そのルームに入室できます。
5. 入室後、コンポーネントの`onRoomInfoChange`ルーム属性の変更イベント通知を受信します。この時、ルーム属性を記録し、それに応じた修正を行うことができます。例：UIに表示されるルーム名、マイク・オンにキャスターへの同意をリクエストする要否の記録などを表示します。
6. 入室後は、コンポーネントの`onSeatListChange`マイクリスト変更イベント通知を受信します。この時、マイクリストの変更をUI上に更新することができます。
7. 入室後に、マイクリストにキャスターが参加した`onAnchorEnterSeat`というイベント通知も受信することがあります。


![](https://main.qcloudimg.com/raw/33432f97eb632fbb9710a59cba9e4469.png)


```
// 1.視聴者は、ニックネームおよびプロフィール画像を設定します。
self.voiceRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // 結果のコールバック           
}

// 2.業務バックエンドから取得したルームリストをroomListと仮定します
let roomList: [Int] = getRoomIDList() // ルームIDリストを取得する関数

// 3. getRoomInfoListを呼び出すことによって、ルームの詳細情報を取得します
self.voiceRoom.getRoomInfoList(roomIdList: roomIdsInt) { (code, message, roomInfos: [VoiceRoomInfo]) in
    //結果の取得。この時、UIの更新が可能
}

// 4.ボイスチャットルームを選択後、roomidを渡して入室します
self.voiceRoom.enterRoom(roomID: roomInfo.roomID) { (code, message) in
    // 入室結果コールバック
    if code == 0 {
       // 入室に成功
    }
}

// 5.入室に成功後、onRoomInfoChangeイベント通知を受信します
func onRoomInfoChange(roomInfo: VoiceRoomInfo) {
    // ルーム名などの情報の更新可
}

// 6.入室に成功後、onSeatListChangeイベント通知を受信します
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // マイクリストを更新
}

// 7. onAnchorEnterSeatイベント通知を受信します
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // マイク・オンイベントの処理
}
```

<span id="model.step7"></span>
### 手順7：マイク管理

#### キャスター側
1. `pickSeat`は、対応するマイクおよび視聴者のuserIdを渡し、発言権を付与してマイク・オンできます。ルーム内の全参加者は`onSeatListChange`および`onAnchorEnterSeat`のイベント通知を受信します。
2. `kickSeat`は、対応するマイクを渡した後、キックアウトしてマイク・オフにすることができます。ルーム内の全参加者は`onSeatListChange`および`onAnchorLeaveSeat`のイベント通知を受信します。
3. `muteSeat`は、対応するマイクを渡した後、ミュート/ミュート解除をすることができます。ルーム内の全参加者は`onSeatListChange`および`onSeatMute`のイベント通知を受信します。
4．`closeSeat`は、対応するマイクを送信後、任意のマイクのクローズ/解除をすることができます。クローズ後は、視聴者側はこれ以上マイクを使用することはできません。ルーム内の全参加者は`onSeatListChange`および`onSeatClose`のイベント通知を受信します。
![](https://main.qcloudimg.com/raw/367a0c670d2f9899d0b311ed1f322ea3.png)
#### 視聴者側：
1. `enterSeat`は、対応するマイクを渡した後、マイク・オンにすることができます。ルーム内の全参加者は`onSeatListChange`および`onAnchorEnterSeat`のイベント通知を受信します。
2. `leaveSeat`は、自主的にマイク・オフにします。ルーム内の全参加者は`onSeatListChange`および`onAnchorLeaveSeat`のイベント通知を受信します。

![](https://main.qcloudimg.com/raw/8d385dd387b6255b8512dbff5829e88a.png)

マイク操作後のイベント通知の順番は次のとおりです。callback > onSeatListChange > onAnchorEnterSeatなど独立したイベント。

```Swift
// case1: キャスターによる1号マイクの発言権の付与
self.voiceRoom.pickSeat(seatIndex: 1, userId: "123") { (code, message) in
    // 結果のコールバック
}

// 3. onSeatListChangeコールバックを受信し、マイクリストを更新します
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // 更新したマイクリスト
}

// 4.単一のマイク変更の通知によって、ここで視聴者が適切な処理を行っているか判断することができます
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // マイク・オンイベントの処理
}
```

```Swift
// case2: 視聴者による自主的な2号マイクのマイク・オン
voiceRoom.enterSeat(seatIndex: 2) { (code, message) in
    // マイク・オン結果のコールバック
}

// 3. onSeatListChangeコールバックを受信し、マイクリストを更新します
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // 更新したマイクリスト
}

// 4.単一のマイク変更の通知によって、ここでご自身が適切な処理を行っているか判断することができます
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // マイク・オンイベントの処理
}
```
:::
</dx-tabs>

[](id:model.step8)
### 手順8：招待シグナリングの使用
[マイク管理](#model.step7)では、視聴者がマイク・オン/オフにする場合やキャスターが発言権を付与してマイク・オンにする場合は、相手の同意を必要とせずに直接操作することができます。
Appにおいて相手の同意がなければ、次の操作の業務フローを実施できない場合は、招待シグナリングによって相応のサポートを行うことができます。
#### 視聴者からの自主的なマイク申請：
1. 視聴者側は、`sendInvitation`を呼び出してキャスターのuserIdおよび業務のカスタムコマンドワードなどを渡します。この時、関数は1個のinviteIdを返しこのinviteIdを記録します。
2. キャスター側は、`onReceiveNewInvitation`のイベント通知を受信します。この時、UIはウィンドウをポップアップして、キャスターに同意するかどうか照会することができます。
3. キャスターが同意を選択後、`acceptInvitation`を呼び出してinviteIdを渡します。
4. 視聴者側は、`onInviteeAccepted`のイベント通知を受信し、`enterSeat`を呼び出してマイク・オンにします。

![](https://main.qcloudimg.com/raw/5ccdb15f63efa127aa883ca6a7bcd80d.png)

```
// 視聴者側の視点
// 1. sendInvitationを呼び出し、1号マイクの使用をリクエストします
let inviteId = self.voiceRoom.sendInvitation(cmd: "ENTER_SEAT", userId: ownerUserId, content: "1") { (code, message) in
    // 発信結果のコールバック
}
// 4.招待の同意リクエストを受信して、正式にマイク・オンにします
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.voiceRoom.enterSeat(seatIndex: ) { (code, message) in
            // マイク・オン結果のコールバック
        }
    }
}

// キャスター側の視点
// 2.キャスターがリクエストを受信します
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "ENTER_SEAT" {
        // 3.キャスターが視聴者のリクエストに同意します
        self.voiceRoom.acceptInvitation(identifier: identifier, callback: nil)
    }
}
```
#### キャスターから視聴者を招待してマイク・オン
1. キャスター側は、`sendInvitation`を呼び出して視聴者のuserIdおよび業務のカスタマイズコマンドワードなどを渡します。この時、関数は1個のinviteIdを返しこのinviteIdを記録します。
2. 視聴者側は、`onReceiveNewInvitation`のイベント通知を受信します。この時、UIはウィンドウをポップアップして、視聴者がマイク・オンに同意するかどうかを照会することができます。
3. 視聴者が同意を選択後、`acceptInvitation`を呼び出してinviteIdを渡します。
4. キャスター側は、`onInviteeAccepted`のイベント通知を受信し、`pickSeat`を呼び出し、視聴者に発言権を付与してマイク・オンにします。

![](https://main.qcloudimg.com/raw/5515f49d6e30410e12cd828b75a8db0b.png)


```
// キャスター側の視点
// 1.キャスターはsendInvitationを呼び出し、視聴者123に発言権を付与して2号マイクのマイク・オンをリクエストします
let inviteId = self.voiceRoom.sendInvitation(cmd: "PICK_SEAT", userId: ownerUserId, content: "2") { (code, message) in
    // 発信結果のコールバック
}

// 4.招待の同意リクエストを受信して、正式にマイク・オンにします
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.voiceRoom.pickSeat(seatIndex: ) { (code, message) in
            // マイク・オン結果のコールバック
        }
    }
}

// 視聴者側の視点
// 2.視聴者がリクエストを受信します
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "PICK_SEAT" {
        // 3.視聴者がキャスターのリクエストに同意します
        self.voiceRoom.acceptInvitation(identifier: identifier, callback: nil)
    }
}
```

[](id:model.step9)
### 手順9：文字チャットおよび弾幕コメントの実装
- `sendRoomTextMsg`によって通常のテキストメッセージを発信できるようになり、該当するルーム内の全てのキャスターおよび視聴者が`onRecvRoomTextMsg`のコールバックを受信することができます。
IMバックエンドは、デフォルトのセンシティブワードフィルタルールを備えており、センシティブワードと認識されたテキストメッセージはクラウドに転送されることはありません。

```Swift
// 発信側：テキストメッセージの発信
self.voiceRoom.sendRoomTextMsg(message: message) { (code, message) in
         
}
// 受信側：テキストメッセージの監視
func onRecvRoomTextMsg(message: String, userInfo: VoiceRoomUserInfo) {
    // 受信したmessage情報の処理方法        
}
```
- `sendRoomCustomMsg`によってカスタマイズ（シグナリング）情報を発信することができます。そのルーム内のすべてのキャスターおよび視聴者は`onRecvRoomCustomMsg`のコールバックを受信することができます。
 カスタムメッセージは、カスタマイズ信号の送信によく用いられます。例えば、「いいね」情報の発信やブロードキャストに使用します。
```swift
// 例：発信側：カスタマイズCmdによって、弾幕と「いいね」情報を区分することができます
// eg:「CMD_DANMU」は弾幕コメントを表し、「CMD_LIKE」は「いいね」情報を表します
self.vocieRoom.sendRoomCustomMsg(cmd: "CMD_DANMU", message: "hello world", callback: nil)
self.voiceRoom.sendRoomCustomMsg(cmd: "CMD_LIKE", message: "", callback: nil)
// 受信側：カスタムメッセージの監視
func onRecvRoomCustomMsg(cmd: String, message: String, userInfo: VoiceRoomUserInfo) {
    if cmd == "CMD_DANMU" {
        // 弾幕コメントの受信
    }
    if cmd == "CMD_LIKE" {
        // 「いいね」情報の受信
    }
}
```


