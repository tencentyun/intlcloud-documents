## コンポーネントの説明

TUIVoiceRoomはオープンソースのオーディオビデオUIコンポーネントであり、プロジェクトにTUIVoiceRoomコンポーネントを統合することにより、数行のコードを書くだけで、Appに「多人数ボイスチャット」などのシーンを組み込むことができます。TUIVoiceRoomは[Android](https://intl.cloud.tencent.com/document/product/647/37286)などのプラットフォームをサポートしています。基本機能は下図のとおりです。

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/a30e897eabbc6f9104bd41db246f33b1.png" width="250"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/857d3b1651cdf1126f1653e1541b3bba.png" width="250"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/6ddb805c442974d202ef610db643fa39.png" width="250"></td>
</tr>
</tbody></table>


## コンポーネントの統合
### ステップ1：TUIVoiceRoomコンポーネントのダウンロードとインポート

xcodeプロジェクトの`Podfile`ファイルと同一階層のディレクトリ下に`TUIVoiceRoom`フォルダを作成し、[Githubリポジトリ iOSディレクトリ](https://github.com/One-time/TUIVoiceRoom/tree/main/iOS)下の[TXAppBasic](https://github.com/One-time/TUIVoiceRoom/tree/main/iOS/TXAppBasic)、[Resources](https://github.com/One-time/TUIVoiceRoom/tree/main/iOS/Resources)、[Source](https://github.com/One-time/TUIVoiceRoom/tree/main/iOS/Source)、[TUIVoiceRoom.podspec](https://github.com/One-time/TUIVoiceRoom/blob/main/iOS/TUIVoiceRoom.podspec)などのファイルを、ご自身のプロジェクトで作成した`TUIVoiceRoom`ディレクトリ下にコピーします。さらに、次のようにインポート動作を完了します。
- プロジェクトのPodfileファイルを開き、TUIVocieRoom.podspecをインポートします。次をご参照ください。
```
# pathはTXAppBasic.podspecのPodfileファイルに対する相対パスです
pod 'TXAppBasic', :path => "TUIVoiceRoom/TXAppBasic/"
# pathはTUIVoiceRoom.podspecのPodfileファイルに対する相対パスです
pod 'TUIVoiceRoom', :path => "TUIVoiceRoom/", :subspecs => ["TRTC"]    
```
- 端末でPodfileのあるディレクトリ下に入り、`pod install`を実行します。次をご参照ください。
```
pod install
```

### ステップ2：権限の設定および難読化ルール
info.plistファイルにおいて、`Privacy > Microphone Usage Description`を追加して、マイクの権限を申請する必要があります。

```plist
<key>NSMicrophoneUsageDescription</key>
<string>VoiceRoomAppはマイクへのアクセス権限が必要です。有効にした後にレコーディングしたビデオでなければ音声は出ません</string>
```

### ステップ3：初期化およびログイン

```Swift
// 初期化
let mTRTCVoiceRoom = TRTCVoiceRoom.shared()
// ログイン
mTRTCVoiceRoom.login(sdkAppID: SDKAppID, userId: userId, userSig: userSig) { code, message in
    if code == 0 {
        //ログイン成功
    }
}
```
**パラメータの説明：**
- **SDKAppID**：**TRTCアプリケーションID**です。Tencent Cloud TRTCサービスをアクティブ化していない場合は、[Tencent Cloud TRTCコンソール](https://console.cloud.tencent.com/trtc/app)に進み、新しいTRTCアプリケーションを作成した後、**アプリケーション情報**をクリックすると、SDKAppID情報が次の図のように表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**：**TRTC アプリケーションキー**であり、SDKAppIdに対応しています。[TRTCアプリケーション管理](https://console.cloud.tencent.com/trtc/app)に進むと、SecretKey情報が上の図のように表示されます。
- **userId**：現在のユーザーID。文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。業務の実際のアカウントシステムと組み合わせてご自身で設定することをお勧めします。
- **userSig**：SDKAppId、userId，Secretkeyなどの情報に基づく計算によって得られるセキュリティ保護署名です。[ここ](https://console.cloud.tencent.com/trtc/usersigtool)をクリックするとデバッグ用のuserSigがオンラインで直接生成されます。また当社の[デモプロジェクト](https://github.com/tencentyun/TUIRoom/blob/main/Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java#L88)を参照してご自身で計算することもできます。その他の情報については、[UserSigの計算、使用方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。




### ステップ4：ボイスチャットルームの実装
1. **管理者によるボイスチャットルーム作成の実装[TRTCVoiceRoom#createRoom](https://intl.cloud.tencent.com/document/product/647/38171)**
```Swift
// ボイスチャットルームパラメータの初期化
let roomParam = VoiceRoomParam()
roomParam.roomName = "ルーム名"
roomParam.needRequest = false // リスナーのマイク・オンに対する管理者の同意の要否
roomParam.coverUrl = "ルームカバー図のURL"
roomParam.seatCount = 7 // ルームの座席数。ここでは計7席あり、管理者が1席を占め、残り6席がリスナーとなります
roomParam.seatInfoList = []
// マイク情報の初期化
for _ in 0..< param.seatCount {
    let seatInfo = VoiceRoomSeatInfo()
    param.seatInfoList.append(seatInfo)
}
// 管理者側でルームを作成
mTRTCVoiceRoom.createRoom(roomID: yourRoomID, roomParam: roomParam) { (code, message) in
    if code == 0 {
        // 作成に成功
    }
}
```
2. **リスナーのボイスチャットルーム入室の実装[TRTCVoiceRoom#enterRoom](https://intl.cloud.tencent.com/document/product/647/38171)**
```Swift
// 1.リスナーが呼び出して入室
mTRTCVoiceRoom.enterRoom(roomID: roomID) { (code, message) in
    // 入室結果コールバック
    if code == 0 {
       // 入室に成功
    }
}
```
3. **リスナーの自主的なマイク・オンの実装[TRTCVoiceRoom#enterRoom](https://intl.cloud.tencent.com/document/product/647/38171)**
```Swift
// 1: リスナーが呼び出してマイク・オン
let seatIndex = 2; //マイクのindex
mTRTCVoiceRoom.enterSeat(seatIndex: 2) { (code, message) in
    if code == 0 {
        // マイク・オン成功
    }
}

// 2. onSeatListChangeコールバックを受信し、マイクリストを更新します
@Override
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // 更新したマイクリスト
}
```
4. **管理者による視聴者発言招待の実装[TRTCVoiceRoom#enterRoom](https://intl.cloud.tencent.com/document/product/647/38171)**
```Swift
// 1: 管理者が呼び出して、視聴者が発言できるように招待
let seatIndex = 2; //マイクのindex
let userId = "123"; //マイク・オンが必要なユーザーid
mTRTCVoiceRoom.pickSeat(seatIndex: 1, userId: "123") { (code, message) in
    if code == 0 {
    }
}

// 2. onSeatListChangeコールバックを受信し、マイクリストを更新します
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // 更新したマイクリスト
}
```
5. **リスナーによるマイク・オン申請の実装  [TRTCVoiceRoom#sendInvitation](https://intl.cloud.tencent.com/document/product/647/38171)**
```Swift
// リスナー側の視点
// 1.リスナーが呼び出してマイク・オンを申請
let seatIndex = "1"; //マイクのindex
let userId = "123"; //ユーザーid
let inviteId = mTRTCVoiceRoom.sendInvitation(cmd: "takeSeat", userId: ownerUserId, content: "1") { (code, message) in
    // 発信結果のコールバック
}

// 2.招待のリクエスト同意を受信し、正式にマイク・オンになります
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.mTRTCVoiceRoom.enterSeat(seatIndex: ) { (code, message) in
            // マイク・オン結果のコールバック
        }
    }
}

// 管理者側の視点
// 1.管理者がリクエストを受信します
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "takeSeat" {
        // 2.管理者がリスナーのリクエストに同意します
        self.mTRTCVoiceRoom.acceptInvitation(identifier: identifier, callback: nil)
    }
}
```
6. **管理者によるマイク・オンへの招待の実装  [TRTCVoiceRoom#sendInvitation](https://intl.cloud.tencent.com/document/product/647/38171)**
```Swift
// 管理者側の視点
// 1.管理者はsendInvitationを呼び出して、リスナー「123」をピックして2号マイクのマイク・オンをリクエストします
let inviteId = self.mTRTCVoiceRoom.sendInvitation(cmd: "pickSeat", userId: ownerUserId, content: "2") { (code, message) in
    // 発信結果のコールバック
}

// 2.招待のリクエスト同意を受信し、正式にマイク・オンになります
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.mTRTCVoiceRoom.pickSeat(seatIndex: ) { (code, message) in
            // マイク・オン結果のコールバック
        }
    }
}

// リスナー側の視点
// 1.リスナーがリクエストを受信します
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "pickSeat" {
        // 2.リスナーが管理者のリクエストに同意します
        self.mTRTCVoiceRoom.acceptInvitation(identifier: identifier, callback: nil)
    }
}
```
7. **テキストチャットの実装  [TRTCVoiceRoom#sendRoomTextMsg](https://intl.cloud.tencent.com/document/product/647/38171)**
```Swift
// 発信側：テキストメッセージの発信
self.mTRTCVoiceRoom.sendRoomTextMsg(message: message) { (code, message) in
         
}

// 受信側：テキストメッセージのモニタリング
func onRecvRoomTextMsg(message: String, userInfo: VoiceRoomUserInfo) {
    // 受信したmessage情報の処理方法        
}
```
8. **弾幕コメントの実装 [TRTCVoiceRoom#sendRoomCustomMsg](https://intl.cloud.tencent.com/document/product/647/38171)**
```Swift
// 例：発信側：カスタマイズCmdによって、弾幕と「いいね」情報を区分することができます
// eg:「CMD_DANMU」は弾幕コメントを表し、「CMD_LIKE」は「いいね」情報を表します
self.mTRTCVoiceRoom.sendRoomCustomMsg(cmd: "CMD_DANMU", message: "hello world", callback: nil)
self.mTRTCVoiceRoom.sendRoomCustomMsg(cmd: "CMD_LIKE", message: "", callback: nil)

// 受信側：カスタムメッセージのモニタリング
func onRecvRoomCustomMsg(cmd: String, message: String, userInfo: VoiceRoomUserInfo) {
    if cmd == "CMD_DANMU" {
        // 弾幕コメントの受信
    }
    if cmd == "CMD_LIKE" {
        // 「いいね」情報の受信
    }
}
```


## よくあるご質問
ご要望やフィードバックなどがございましたら、colleenyu@tencent.comまでご連絡ください。
