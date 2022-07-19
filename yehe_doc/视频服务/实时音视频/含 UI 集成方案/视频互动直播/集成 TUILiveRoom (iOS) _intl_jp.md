## コンポーネントの説明

TUILiveRoomはオープンソースのビデオライブストリーミングUIコンポーネントであり、プロジェクトにTUILiveRoomコンポーネントを統合することにより、数行のコードを書くだけで、Appに「ビデオインタラクティブストリーミング」のシーンを組み込むことができます。TUILiveRoomにはAndroid、iOSなどのプラットフォーム用のソースコードが含まれます。基本機能は下図のとおりです：

>?TUIKitシリーズコンポーネントはTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047/35448)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMサービスの課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。TRTCをアクティブにすると、デフォルトでは、100DAUまでサポートするIM SDK体験版もアクティブになります。

<table>
<tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/a1b4b04662bb342de1e7b713cb3f59ce.png"></td>
</tr>
</table>

[](id:model)
## コンポーネントの統合

[](id:model.step1)
### ステップ3：TUILiveRoomコンポーネントのインポート

**cocoapodsによってコンポーネントをインポートします**。具体的な手順については、以下のとおりです：
1. プロジェクトの`Podfile`ファイルと同じ階層のディレクトリ下に`TUILiveRoom`フォルダを作成します。
2. クリックして[**Github/TUILiveRoom**](https://github.com/tencentyun/TUILiveRoom)に進み、コードのクローン/ダウンロードを選択した後、[**TUILiveRoom/iOS/**](https://github.com/tencentyun/TUILiveRoom/tree/main/iOS)ディレクトリ下の`Source`、`Resources` 、`TUIBeauty`、`TUIAudioEffect`、`TUIBarrage`、`TUIGift`、`TXAppBasic`フォルダと`TUILiveRoom.podspec`ファイルを、`ステップ1`で作成したTUILiveRoomフォルダ下にコピーします。
3. Podfileファイル内に以下の依存関係を追加します。その後、`pod install`コマンドを実行すると、インポートが完了します。
```
# :path => "TUILiveRoom.podspecを指定する相対パス"
pod 'TUILiveRoom', :path => "./TUILiveRoom/TUILiveRoom.podspec", :subspecs => ["TRTC"]
# :path => "TXAppBasic.podspecを指定する相対パス"
pod 'TXAppBasic', :path => "./TUILiveRoom/TXAppBasic/"
# :path => "TUIBeauty.podspecを指定する相対パス"
pod 'TUIBeauty', :path => "./TUILiveRoom/TUIBeauty/"
# :path => "TUIBeauty.podspecを指定する相対パス"
pod 'TUIAudioEffect', :path => "./TUILiveRoom/TUIAudioEffect/"
# :path => "TUIBeauty.podspecを指定する相対パス"
pod 'TUIBarrage', :path => "./TUILiveRoom/TUIBarrage/"
# :path => "TUIBeauty.podspecを指定する相対パス"
pod 'TUIGift', :path => "./TUILiveRoom/TUIGift/"
```

>! 
>- `Source`、`Resources`フォルダと`TUILiveRoom.podspec`ファイルは同一のディレクトリ下にある必要があります。
>- TXAppBasic.podspecはTXAppBasicフォルダ下にあります。

[](id:model.step2)
### ステップ2：権限の設定

オーディオビデオ機能を使用するには、マイクおよびカメラの使用権限を付与する必要があります。AppのInfo.plistで以下の2項を追加します。これらはシステムが権限付与ダイアログボックスをポップアップする際に表示される、マイクとカメラのメッセージにそれぞれ対応します。

```
<key>NSCameraUsageDescription</key>
<string>RoomAppはカメラへのアクセス権限が必要です。有効にした後にレコーディングしたビデオでなければ画面は出ません</string>
<key>NSMicrophoneUsageDescription</key>
<string>RoomAppはマイクへのアクセス権限が必要です。有効にした後にレコーディングしたビデオでなければ音声は出ません</string>
```
![](https://qcloudimg.tencent-cloud.cn/raw/9395aca2af5433c9a63ffb4ba9ff9888.png)

[](id:model.step3)
### ステップ3：コンポーネントの初期化およびログイン

<dx-codeblock>
:::  Objective-C ObjectiveC
@import TUILiveRoom;
@import TUICore;

// 1.コンポーネントのログイン
[TUILogin login:@"あなたのSDKAppID" userID:@あなたのUserID" userSig:@"あなたのUserSig" succ:^{
        
} fail:^(int code, NSString *msg) {
        
}];
// 2.TUILiveRoomインスタンスの初期化
TUILiveRoom *mLiveRoom = [TUILiveRoom sharedInstance];
```
:::
::: Swift  Swift
import TUILiveRoom
import TUICore

// 1.コンポーネントのログイン
TUILogin.login("あなたのSDKAppID", userID: "あなたのUserID", userSig: "あなたのUserSig") {
        
} fail: { code, msg in
        
}
// 2.TUILiveRoomインスタンスの初期化
let mLiveRoom = TUILiveRoom.sharedInstance
```
:::
</dx-codeblock>

**パラメータの説明**：
- **SDKAppID**：**TRTCアプリケーションID**です。Tencent Cloud TRTCサービスをアクティブ化していない場合は、[Tencent Cloud TRTCコンソール](https://console.cloud.tencent.com/trtc/app)に進み、新しいTRTCアプリケーションを作成した後、**アプリケーション情報**をクリックすると、SDKAppID情報が次の図のように表示されます：
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **SecretKey**：**TRTC アプリケーションキー**であり、SDKAppIDに対応しています。[TRTCアプリケーション管理](https://console.cloud.tencent.com/trtc/app)に進むと、SecretKey情報が上の図のように表示されます。
- **UserID**：現在のユーザーのIDです。文字列形式で、長さは32バイト以内とし、特殊文字の使用はサポートしていません。英語または数字の使用をお勧めします。業務の実際のアカウントシステムと組み合わせてご自身で設定することができます。
- **UserSig**：SDKAppId、UserID、SecretKeyなどの情報に基づく計算によって得られるセキュリティ保護署名です。[ここ](https://console.cloud.tencent.com/trtc/usersigtool)をクリックするとデバッグ用のUserSigがオンラインで直接生成されます。また当社の[TUILiveRoomデモプロジェクト](https://github.com/tencentyun/TUIRoom/blob/main/iOS/Example/Debug/GenerateTestUserSig.swift#L42)を参照してご自身で計算することもできます。その他の情報については、[UserSigの計算、使用方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。


[](id:model.step4)
### ステップ4：ビデオインタラクティブストリーミングルームの実装
1. **キャスター側の配信開始**
<dx-codeblock>
:::  Objective-C Objc
[mLiveRoom createRoomWithRoomId:123 roomName:@"test room" coverUrl:@""];

:::
::: Swift  Swift
mLiveRoom.createRoom(roomId: 123, roomName: "test room", coverUrl:"")
:::
</dx-codeblock>
2. **視聴者側の視聴**
<dx-codeblock>
:::  Objective-C Objc
[mLiveRoom enterRoomWithRoomId:123];

:::
::: Swift  Swift
mLiveRoom.createRoom(roomId: 123）
:::
</dx-codeblock>

3. **視聴者とキャスターがマイク接続 [TRTCLiveRoom#requestJoinAnchor](https://intl.cloud.tencent.com/document/product/647/37332#requestjoinanchor)**
<dx-codeblock>
:::  Objective-C Objc
// 1.視聴者側がマイク接続のリクエストを送信します
[TRTCLiveRoom shareInstance].delegate = self;
// @param mSelfUserId String 現在のユーザーid
NSString *mSelfUserId = @"1314";
[[TRTCLiveRoom shareInstance] requestJoinAnchor:[NSString stringWithFormat:@"%@ マイク接続をリクエスト", mSelfUserId] timeout:30 responseCallback:^(BOOL agreed, NSString * _Nullable reason) {
    if (agreed) {
        // キャスターが視聴者のリクエストを受け入れます
      UIView *playView = [UIView new];
            [self.view addSubView:playView];
        // 視聴者がプレビューを起動し、プッシュを開始します
      [[TRTCLiveRoom shareInstance] startCameraPreviewWithFrontCamera:YES view:playView callback:nil];
      [[TRTCLiveRoom shareInstance] startPublishWithStreamID:[NSString stringWithFormat:@"%@_stream", mSelfUserId] callback:nil];
    }            
}];

// 2.キャスター側がマイク接続のリクエストを受信します
#pragma mark - TRTCLiveRoomDelegate
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom onRequestJoinAnchor:(TRTCLiveUserInfo *)user reason:(NSString *)reason {
    // 相手のマイク接続のリクエストに同意します
    [[TRTCLiveRoom shareInstance] responseJoinAnchor:user.userId agree:YES reason:@"マイク接続に同意"];
}

- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom onAnchorEnter:(NSString *)userID {
    // キャスターがマイク接続の視聴者のマイク・オンの通知を受信します
    UIView *playView = [UIView new];
    [self.view addSubview:playView];
    // キャスターが視聴者の画面を再生します
    [[TRTCLiveRoom shareInstance] startPlayWithUserID:userID view:playView callback:nil];
}

:::
::: Swift  Swift
// 1.視聴者側がマイク接続のリクエストを送信します
TRTCLiveRoom.shareInstance().delegate = self
let mSelfUserId = "1314"
TRTCLiveRoom.shareInstance().requestJoinAnchor(reason: mSelfUserId + "マイク接続をリクエスト", timeout: 30) {  [weak self] (agree, msg) in
    guard let self = self else { return }
  if agree {
        // キャスターが視聴者のリクエストを受け入れます
        let playView = UIView()
        self.view.addSubView(playView)
        // 視聴者がプレビューを起動し、プッシュを開始します
        TRTCLiveRoom.shareInstance().startCameraPreview(frontCamera: true, view: playView)
        TRTCLiveRoom.shareInstance().startPublish(streamID: mSelfUserId + "_stream")
  }
}

// 2.キャスター側がマイク接続のリクエストを受信します
extension ViewController: TRTCLiveRoomDelegate {
    
    func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRequestJoinAnchor user: TRTCLiveUserInfo, reason: String?) {
        // 相手のマイク接続のリクエストに同意します
        TRTCLiveRoom.shareInstance().responseRoomPK(userID: user.userId, agree: true, reason: "マイク接続に同意")
    }
    
    func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
        // キャスターがマイク接続の視聴者のマイク・オンの通知を受信します
        let playView = UIView()
        view.addSubview(playView)
        // キャスターが視聴者の画面を再生します
        TRTCLiveRoom.shareInstance().startPlay(userID: userID, view: playView);
    }
}
:::
</dx-codeblock>

4. **キャスター間のPK [TRTCLiveRoom#requestRoomPK](https://intl.cloud.tencent.com/document/product/647/37332#requestroompk)**
<dx-codeblock>
:::  Objective-C Objc
// キャスターAがルーム12345を作成します
[[TUILiveRoom sharedInstance] createRoomWithRoomId:12345 roomName:@"roomA" coverUrl:@"roomA coverUrl"];
// キャスターBがルーム54321を作成します
[[TUILiveRoom sharedInstance] createRoomWithRoomId:54321 roomName:@"roomB" coverUrl:@"roomB coverUrl"];

// キャスターA
// キャスターAがキャスターBにPKのリクエストを送信します
[[TRTCLiveRoom shareInstance] requestRoomPKWithRoomID:543321 userID:@"roomB userId" timeout:30 responseCallback:^(BOOL agreed, NSString * _Nullable reason) {
    if (agreed) {
        // ユーザーBが受け入れます
    }else{
        // ユーザーBが拒否します
    }
}];

// キャスターB：
// 2.キャスターBがキャスターAのメッセージを受信します
#pragma mark - TRTCLiveRoomDelegate
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom onRequestRoomPK:(TRTCLiveUserInfo *)user {
    // 3.キャスターBがキャスターAに回答し、リクエストを受け入れます
    [[TRTCLiveRoom shareInstance] responseRoomPKWithUserID:user.userId agree:YES reason:@""];
}

- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom onAnchorEnter:(NSString *)userID {
    // 4.キャスターBがキャスターAのルーム参加の通知を受信し、キャスターAの画面を再生します
    [[TRTCLiveRoom shareInstance] startPlayWithUserID:userID view:playAView callback:nil];
}

:::
::: Swift  Swift
// キャスターAがルーム12345を作成します
TUILiveRoom.sharedInstance.createRoom(roomId: 12345, roomName: "roomA")
// キャスターBがルーム54321を作成します
TUILiveRoom.sharedInstance.createRoom(roomId: 54321, roomName: "roomB")

// キャスターA
// キャスターAがキャスターBにPKのリクエストを送信します
TRTCLiveRoom.shareInstance().requestRoomPK(roomID: 543321, userID: "roomB userId", timeout: 30) { [weak self] (agreed, msg) in
     guard let self = self else { return }
    if agreed {
        // ユーザーBが受け入れます
    }else{
        // ユーザーBが拒否します
    }
}

// キャスターB：
// 2.キャスターBがキャスターAのメッセージを受信します
extension ViewController: TRTCLiveRoomDelegate {
    func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRequestRoomPK user: TRTCLiveUserInfo) {
        // 3.キャスターBがキャスターAに回答し、リクエストを受け入れます
        TRTCLiveRoom.shareInstance().responseRoomPK(userID: user.userId, agree: true, reason: "")
    }
    
    func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
        // 4.キャスターBがキャスターAのルーム参加の通知を受信し、キャスターAの画面を再生します
        TRTCLiveRoom.shareInstance().startPlay(userID: userID, view: playAView);
    }
}
:::
</dx-codeblock>

## よくあるご質問
ご要望やフィードバックなどがございましたら、colleenyu@tencent.comまでご連絡ください。
