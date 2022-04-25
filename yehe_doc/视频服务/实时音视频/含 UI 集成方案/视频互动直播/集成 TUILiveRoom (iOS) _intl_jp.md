## コンポーネントの説明

TUILiveRoomはオープンソースのオーディオビデオUIコンポーネントであり、プロジェクトにTUILiveRoomコンポーネントを統合することにより、数行のコードを書くだけで、Appに「ビデオインタラクティブストリーミング」などのシーンを組み込むことができます。TUILiveRoomはまた、[Android](https://intl.cloud.tencent.com/document/product/647/36061)、[Flutter](https://intl.cloud.tencent.com/document/product/647/41944)などのプラットフォームでもサポートしています。基本機能は下図のとおりです。

<table>
<tr>
<td><img width="260" height="561" src="https://qcloudimg.tencent-cloud.cn/raw/34337da1f6427b9a834f6562eba5c663.jpg"/></td>
<td><img width="260" height="561" src="https://qcloudimg.tencent-cloud.cn/raw/52eb1656b5a892e6da65f49a1d503735.jpg"/></td>
<td><img width="260" height="561" src="https://qcloudimg.tencent-cloud.cn/raw/70c9e1e7290592f8c7892b236fb1061e.jpg"/></td>
<td><img width="260" height="561" src="https://qcloudimg.tencent-cloud.cn/raw/ed8c3666aa03951c6d0d9cfe2dccc495.jpg"/></td>
</tr>
</table>


## コンポーネントの統合

### ステップ1：TUILiveRoomコンポーネントのダウンロードとインポート
xcodeプロジェクトの`Podfile`ファイルと同一階層のディレクトリ下に`TUILiveRoom`フォルダを作成し、[Githubリポジトリ iOSディレクトリ](https://github.com/One-time/TUILiveRoom/tree/main/iOS)下の[TXAppBasic](https://github.com/One-time/TUILiveRoom/tree/main/iOS/TXAppBasic)、[TCBeautyKit](https://github.com/One-time/TUILiveRoom/tree/main/iOS/TCBeautyKit)、[Resources](https://github.com/One-time/TUILiveRoom/tree/main/iOS/Resources)、[Source](https://github.com/One-time/TUILiveRoom/tree/main/iOS/Source)、[TUIVoiceRoom.podspec](https://github.com/One-time/TUILiveRoom/blob/main/iOS/TUILiveRoom.podspec)などのファイルを、ご自身のプロジェクトで作成した`TUILiveRoom`ディレクトリ下にコピーします。さらに、次のようにインポート動作を完了します。
- プロジェクトのPodfileファイルを開き、TUILiveRoom.podspecをインポートします。次をご参照ください。
```
# :path => "TXAppBasic.podspecのあるディレクトリを指定する相対パス"
pod 'TXAppBasic', :path => "TUILiveRoom/TXAppBasic/"

# :path => "TCBeautyKit.podspecのあるディレクトリを指定する相対パス"
pod 'TCBeautyKit', :path => "TUILiveRoom/TCBeautyKit/"

# :path => "TUILiveRoom.podspecのあるディレクトリを指定する相対パス"
pod 'TUILiveRoom', :path => "TUILiveRoom/", :subspecs => ["TRTC"]
```
- 端末でPodfileのあるディレクトリ下に入り、`pod install`を実行します。次をご参照ください。
```
pod install
```

### ステップ2：権限の設定および難読化ルール
順に、info.plistファイルに`Privacy > Microphone Usage Description`を追加してマイクの権限を申請し、`Privacy > Camera Usage Description`を追加してカメラの権限を申請します。

```plist
<key>NSMicrophoneUsageDescription</key>
<string>LiveRoomはマイクへのアクセス権限が必要です。有効にした後にレコーディングしたビデオでなければ音声は出ません</string>
<key>NSCameraUsageDescription</key>
<string>LiveRoomはカメラへのアクセス権限が必要です。有効にした後にレコーディングしたビデオでなければ画面は出ません</string>
```

### ステップ3：初期化およびログイン
```Swift
 let mTRTCLiveRoom = TRTCLiveRoom()
 //useCDNFirst：trueは一般視聴者のCDN経由の視聴、falseは一般視聴者の低レイテンシーによる視聴を表します
 //CDNPlayDomain：CDN視聴時に設定する再生ドメイン名を表します
 let config = TRTCLiveRoomConfig(useCDNFirst: useCDNFirst, cdnPlayDomain: yourCDNPlayDomain)
 mTRTCLiveRoom.login(SDKAPPID, userID, userSig, config) { (code, error) in
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

### ステップ4：ビデオインタラクティブストリーミングルームの実装
1. **キャスターが配信開始 [TRTCLiveRoom#createRoom](https://intl.cloud.tencent.com/document/product/647/37332)**
```Swift
// 1.キャスターは、ニックネームおよびプロフィール画像を設定します
 mTRTCLiveRoom.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

 // 2.キャスターが配信開始前にプレビューを立ち上げ、美顔パラメータを設定します
 let view = UIView()
 parentView.add(view)
 mTRTCLiveRoom.startCameraPreview(frontCamera: true, view: view, callback: nil)
 mTRTCLiveRoom.getBeautyManager().setBeautyStyle(.nature)
 mTRTCLiveRoom.getBeautyManager().setBeautyLevel(6)

 // 3.キャスターがルームを作成します
 let param = TRTCCreateRoomParam(roomName: "テストルーム", coverUrl: "")
 mTRTCLiveRoom.createRoom(roomID: 123456789, roomParam: param) { [weak self] (code, error) in
  if code == 0 {
    // 4.キャスターがプッシュを開始し、ストリームがCDNに配信されます。
    self?.mTRTCLiveRoom.startPublish(streamID: mSelfUserId + "_stream", callback: nil)
  }
}
```
2. **視聴者側が視聴 [TRTCLiveRoom#enterRoom](https://intl.cloud.tencent.com/document/product/647/37332)**
```Swift
// 1.業務バックエンドから取得したルームリストをroomListと仮定します
 var roomList: [UInt32] = GetRoomList()

 // 2. getRoomInfosを呼び出すことによって、ルームの詳細情報を取得します
 mTRTCLiveRoom.getRoomInfos(roomIDs: roomList, callback: { (code, msg, list) in
    if code == 0 {
      // ルーム詳細情報の取得後、キャスターリストページでキャスターのニックネーム、プロフィール画像等の関連情報を表示できます
    }
 })

 // 3.roomidを選択しルームに参加します
 mTRTCLiveRoom.enterRoom(roomID: roomID, callback: callback)

 // 4.視聴者がキャスターのルーム参加の通知を受信すると、再生が開始されます
 public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
   // 5.視聴者がキャスターの画面を再生します
   mTRTCLiveRoom.startPlay(userID: userID, view: renderView, callback: nil) 
 }
```
3. **視聴者とキャスターがマイク接続 [TRTCLiveRoom#requestJoinAnchor](https://intl.cloud.tencent.com/document/product/647/37332)**
```Swift
// 視聴者側：
  // 1.視聴者側がマイク接続のリクエストを送信します
  mTRTCLiveRoom.requestJoinAnchor(reason: mSelfUserId + "あなたとのマイク接続をリクエスト", responseCallback: { [weak self] (agreed, reason) in 
      // 4.キャスターが視聴者のリクエストを受け入れます
       if agreed {
        // 5.視聴者がプレビューを起動し、プッシュを開始します
        self?.mTRTCLiveRoom.startCameraPreview(frontCamera: true, view: localView, callback: nil)
        self?.mTRTCLiveRoom.startPublish(streamID: streamID, callback: nil)
       }        
  }, callback: callback)

  // キャスター側：
  // 2.キャスター側がマイク接続のリクエストを受信します
  public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRequestJoinAnchor user: TRTCLiveUserInfo, reason: String?, timeout: Double) {
    // 3.相手側のマイク接続のリクエストに同意します
    mTRTCLiveRoom.responseJoinAnchor(userID: userID, agree: true, reason: "マイク接続に同意")
  }

  // 6.キャスターがマイク接続の視聴者のマイク・オンの通知を受信します
  public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
    // 7.キャスターが視聴者の画面を再生します
    mTRTCLiveRoom.startPlay(userID: userID, view: view, callback: nil)
  }
```
4. **キャスター間のPK [TRTCLiveRoom#requestRoomPK](https://intl.cloud.tencent.com/document/product/647/37332)**
```Swift
// キャスターA:
// キャスターAがルーム12345を作成します
mTRTCLiveRoom.createRoom(roomID: 12345, roomParam: param, callback: nil)

// 1.キャスターAがキャスターBにPKのリクエストを送信します
mTRTCLiveRoom.requestRoomPK(roomID: 54321, userID: "B", responseCallback: { (agree, reason) in
  // 5.同意の有無のコールバックを受信します
  if agree {
  }       
}, callback: callback)

// キャスターAがキャスターBのルーム参加のコールバックを受信します
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
  // 6.Bのルーム参加の通知を受信し、Bの画面を再生します
  mTRTCLiveRoom.startPlay(userID: userID, view: view, callback: callback)
}

// キャスターB：
// キャスターBがルーム54321を作成します
mTRTCLiveRoom.createRoom(roomID: 54321, roomParam: param, callback: nil)

// 2.キャスターBがキャスターAのメッセージを受信します
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRequestRoomPK user: TRTCLiveUserInfo, timeout: Double) {
  // 3.キャスターBがキャスターAに回答し、リクエストを受け入れます
  mTRTCLiveRoom.responseRoomPK(userID: userID, agree: true, reason: reason)
}

public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
  // 4.キャスターBがキャスターAのルーム参加の通知を受信し、キャスターAの画面を再生します
  mTRTCLiveRoom.startPlay(userID: userID, view: view, callback: callback)
}
```
5. **テキストチャットの実装[TRTCLiveRoom#sendRoomTextMsg](https://intl.cloud.tencent.com/document/product/647/37332)**
```Swift
// 発信側：テキストメッセージの発信
mTRTCLiveRoom.sendRoomTextMsg(message: "Hello Word!", callback: callback)
// 受信側：テキストメッセージのモニタリング
mTRTCLiveRoom.delegate = self
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRecvRoomTextMsg message: String, fromUser user: TRTCLiveUserInfo) {
  debugPrint("\(user.userName)から受信したテキストメッセージ:\(message)")
}
```
6. **弾幕コメントの実装 [TRTCLiveRoom#sendRoomCustomMsg](https://intl.cloud.tencent.com/document/product/647/37332)**
```Swift
// 送信側：カスタマイズしたCmdで弾幕と「いいね！」のメッセージを区別することができます
// eg:「CMD_DANMU」は弾幕コメントを表し、「CMD_LIKE」は「いいね」情報を表します
mTRTCLiveRoom.sendRoomCustomMsg(command: "CMD_DANMU", message: "Hello world", callback: nil)
mTRTCLiveRoom.sendRoomCustomMsg(command: "CMD_LIKE", message: "", callback: nil)
// 受信側：カスタムメッセージのモニタリング
mTRTCLiveRoom.delegate = self
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRecvRoomCustomMsg command: String, message: String, fromUser user: TRTCLiveUserInfo) {
  if "CMD_DANMU" == command {
    // 弾幕コメントの受信
    debugPrint("\(user.userName)から受信した弾幕のメッセージ:\(message)")
  } else if "CMD_LIKE" == command {
    // 「いいね」情報の受信
    debugPrint("\(user.userName)がいいねを付けました")
  }
}
```


## よくあるご質問
ご要望やフィードバックなどがございましたら、colleenyu@tencent.comまでご連絡ください。
