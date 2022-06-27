## コンポーネントの説明
TUIRoomはオープンソースのオーディオビデオUIコンポーネントであり、プロジェクトにTUIRoomコンポーネントを統合することにより、数行のコードを書くだけで、Appに画面共有、美顔、低遅延ビデオ通話などを組み込むことができます。TUIRoomはまた、[Android](https://intl.cloud.tencent.com/document/product/647/37283)、[Windows](https://intl.cloud.tencent.com/document/product/647/44071)、[Mac](https://intl.cloud.tencent.com/document/product/647/44071)などのプラットフォームでもサポートしています。基本機能は下図のとおりです。

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/2944bac3c5d348b06d2a11c439783b48.png"></td>
</tr>
</tbody></table>

## コンポーネントの統合

### ステップ1：TUIRoomコンポーネントのインポート

**cocoapodsによってコンポーネントをインポートします**。具体的な手順については、以下のとおりです。
1. プロジェクトの`Podfile`ファイルと同じ階層のディレクトリ下に`TUIRoom`フォルダを作成します。
2. クリックして[**Github/TUIRoom**](https://github.com/tencentyun/TUIRoom)に進み、コードのクローン/ダウンロードを選択した後、[**TUIRoom/iOS/**](https://github.com/tencentyun/TUIRoom/tree/main/iOS)ディレクトリ下の`Source`、`Resources` 、`TUIBeauty`、`TXAppBasicフォルダ、`TUIRoom.podspec`ファイルを、`ステップ1`で作成したTUIRoomフォルダ下にコピーします。
3. Podfileファイル内に以下の依存関係を追加します。その後、`pod install`コマンドを実行すると、インポートが完了します。

```
# :path => "TUIRoom.podspecを指定する相対パス"
pod 'TUIRoom', :path => "./TUIRoom/TUIRoom.podspec", :subspecs => ["TRTC"]
# :path => "TXAppBasic.podspecを指定する相対パス"
pod 'TXAppBasic', :path => "./TUIRoom/TXAppBasic/"
# :path => "TUIBeauty.podspecを指定する相対パス"
pod 'TUIBeauty', :path => "./TUIRoom/TUIBeauty/"
```

>! `Source`、`Resources`フォルダと`TUIRoom.podspec`ファイルは同一のディレクトリ下にある必要があります。
>-  TXAppBasic.podspecはTXAppBasicフォルダ下にあります。
>-  TUIBeauty.podspecはTCBeautyKitフォルダ下にあります。

### ステップ2：権限の設定

オーディオビデオ機能を使用するには、マイクおよびカメラの使用権限を付与する必要があります。AppのInfo.plistで以下の2項を追加します。これらはシステムが権限付与ダイアログボックスをポップアップする際に表示される、マイクとカメラのメッセージにそれぞれ対応します。

```
<key>NSCameraUsageDescription</key>
<string>RoomAppはカメラへのアクセス権限が必要です。有効にした後にレコーディングしたビデオでなければ画面は出ません</string>
<key>NSMicrophoneUsageDescription</key>
<string>RoomAppはマイクへのアクセス権限が必要です。有効にした後にレコーディングしたビデオでなければ音声は出ません</string>
```
![](https://qcloudimg.tencent-cloud.cn/raw/224ae568f11d50124ea663ac0ef1c6e9.png)

### ステップ3：TUIコンポーネントリポジトリの作成と初期化

<dx-codeblock>
:::  Objective-C ObjectiveC
@import TUIRoom;
@import TUICore;

// 1.コンポーネントのログイン
[TUILogin login:@"あなたのSDKAppID" userID:@あなたのUserID" userSig:@"あなたのUserSig" succ:^{
        
} fail:^(int code, NSString *msg) {
        
}];
// 2.TUIRoomインスタンスの初期化
TUIRoom *tuiRoom = [TUIRoom sharedInstance];
```
:::
::: Swift Swift
import TUIRoom
import TUICore

// 1.コンポーネントのログイン
TUILogin.login("あなたのSDKAppID", userID: "あなたのUserID", userSig: "あなたのUserSig") {
        
} fail: { code, msg in
        
}

// 2.TUIRoomインスタンスの初期化
let tuiRoom = TUIRoom.sharedInstance
```
:::
</dx-codeblock>

**パラメータの説明**
- **SDKAppID**：**TRTCアプリケーションID**です。Tencent Cloud TRTCサービスをアクティブ化していない場合は、[Tencent Cloud TRTCコンソール](https://console.cloud.tencent.com/trtc/app)に進み、新しいTRTCアプリケーションを作成した後、**アプリケーション情報**をクリックすると、SDKAppID情報が次の図のように表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **SecretKey**：**TRTC アプリケーションキー**であり、SDKAppIDに対応しています。[TRTCアプリケーション管理](https://console.cloud.tencent.com/trtc/app)に進むと、SecretKey情報が上の図のように表示されます。
- **UserID**：現在のユーザーのIDです。文字列形式で、長さは32バイト以内とし、特殊文字の使用はサポートしていません。英語または数字の使用をお勧めします。業務の実際のアカウントシステムと組み合わせてご自身で設定することができます。
- **UserSig**：SDKAppId、UserID，SecretKeyなどの情報に基づく計算によって得られるセキュリティ保護署名です。[ここ](https://console.cloud.tencent.com/trtc/usersigtool)をクリックするとデバッグ用のUserSigがオンラインで直接生成されます。また当社の[TUIRoomデモプロジェクト](https://github.com/tencentyun/TUIRoom/blob/main/iOS/Example/Debug/GenerateTestUserSig.swift#L42)を参照してご自身で計算することもできます。その他の情報については、[UserSigの計算、使用方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。


### ステップ4：多人数オーディオビデオインタラクションの実装
1. **管理者が多人数オーディオビデオインタラクティブルームを作成できるようにします**。
<dx-codeblock>
:::  Objective-C ObjectiveC
@import TUIRoom;

[tuiRoom createRoomWithRoomId:@"あなたのRoomId" speechMode:TUIRoomFreeSpeech isOpenCamera:YES isOpenMicrophone:YES];
:::
::: Swift Swift
import TUIRoom

tuiRoom.createRoom(roomId: "あなたのRoomId", speechMode: .freeSpeech, isOpenCamera: true, isOpenMicrophone: true)
```
:::
</dx-codeblock>
2. **他のメンバーがオーディオビデオルームに参加できるようにします**。
<dx-codeblock>
:::  Objective-C ObjectiveC
@import TUIRoom;

[tuiRoom enterRoomWithRoomId:@"相手のRoomId" isOpenCamera:YES isOpenMicrophone:YES]
:::
::: Swift Swift
import TUIRoom

tuiRoom.enterRoom(roomId: "相手のRoomId", isOpenCamera: true, isOpenMicrophone: true)
```
:::
</dx-codeblock>

### ステップ5：ルーム管理（オプション）
1. **管理者によるルーム解散 [TUIRoomCore#destroyRoom](https://intl.cloud.tencent.com/document/product/647/37282)**。
<dx-codeblock>
:::  Objective-C ObjectiveC
@import TUIRoom;

[[TUIRoomCore shareInstance] destroyRoom:^(NSInteger code, NSString * _Nonnull message) {
            
}];
```
:::
::: Swift Swift
import TUIRoom

TUIRoomCore.shareInstance().destroyRoom { [weak self] _, _ in
    guard let self = self else { return }
    self.navigationController?.popViewController(animated: true)
}
```
:::
</dx-codeblock>
2. **メンバーの退室 [TUIRoomCore#leaveRoom](https://intl.cloud.tencent.com/document/product/647/37282)**。
<dx-codeblock>
:::  Objective-C ObjectiveC
@import TUIRoom;

[[TUIRoomCore shareInstance] leaveRoom:^(NSInteger code, NSString * _Nonnull message) {
            
}];
```
:::
::: Swift Swift
import TUIRoom

TUIRoomCore.shareInstance().leaveRoom { [weak self] _, _ in
    guard let self = self else { return }
    self.navigationController?.popViewController(animated: true)
}
```
:::
</dx-codeblock>

### ステップ6：画面共有（オプション）
画面共有を実装します [TUIRoomCore#startScreenCapture](https://intl.cloud.tencent.com/document/product/647/37282)。画面共有プロジェクトの設定については、[リアルタイム画面共有(iOS)](https://intl.cloud.tencent.com/document/product/647/37338)をご参照ください。
<dx-codeblock>
:::  Objective-C ObjectiveC
@import TUIRoom;
@import TXLiteAVSDK_Professional;

TRTCVideoEncParam *params = [[TRTCVideoEncParam alloc] init];
params.videoResolution = TRTCVideoResolution_1280_720;
params.resMode = TRTCVideoResolutionModePortrait;
params.videoFps = 10;
params.enableAdjustRes = NO;
params.videoBitrate = 1500;

[[TUIRoomCore shareInstance] startScreenCapture:param];
```
:::
::: Swift  Swift
import TUIRoom

 // 画面共有
let params = TRTCVideoEncParam()
params.videoResolution = TRTCVideoResolution._1280_720
params.resMode = TRTCVideoResolutionMode.portrait
params.videoFps = 10
params.enableAdjustRes = false
params.videoBitrate = 1500
TUIRoomCore.shareInstance().startScreenCapture(params)

```
:::
</dx-codeblock>


## よくあるご質問

### CocoaPodsをインストールするにはどうすればよいですか。

ターミナルポートに以下のコマンド（事前にMacにRuby環境をインストールする必要があります）を入力します。
```
sudo gem install cocoapods
```

>? ご要望やフィードバックなどがございましたら、colleenyu@tencent.comまでご連絡ください。

