## コンポーネントの説明
TUIRoomはオープンソースのオーディオビデオUIコンポーネントであり、プロジェクトにTUIRoomコンポーネントを統合することにより、数行のコードを書くだけで、Appに画面共有、美顔、低遅延ビデオ通話などを組み込むことができます。TUIRoomはまた、[Android](https://intl.cloud.tencent.com/document/product/647/37283)、[Windows](https://intl.cloud.tencent.com/document/product/647/44071)、[Mac](https://intl.cloud.tencent.com/document/product/647/44071)などのプラットフォームでもサポートしています。基本機能は下図のとおりです。

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/0f07b6d570174f6fdc999eb67864f1f3.png" width="250"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/9bdc61aa798c2c3926949d00a97302dc.png" width="250"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/37ef82ac97172967c037a523c5d09af3.png" width="250"></td>
</tr>
</tbody></table>


## コンポーネントの統合

### ステップ1：TUIRoomコンポーネントのダウンロードとインポート
**cocoapodsを使用してコンポーネントをインポート**することができます。具体的な手順は、以下のとおりです。
>? 画面共有機能が必要な場合は、[**公式サイトリンク**](https://intl.cloud.tencent.com/document/product/647/34615)からTXLiteAVSDK_ReplayKitExt.frameworkをダウンロードしてご自身のプロジェクトに追加し、targetに「Broadcast Upload Extension」を新規作成することができます。実装に関しては、[デモプロジェクト](https://github.com/tencentyun/TUIRoom/tree/main/iOS/Example/TXReplayKit_Screen)をご参照ください。

1. クリックして[Github](https://github.com/tencentyun/TUIKaraoke)に進み、コードのクローン/ダウンロードを選択した後、iOS下の`Resources`、`SDK`、`Source`フォルダ、`TUIRoom.podspec`ファイルをプロジェクトにコピーします。
2. `Podfile`ファイル内に以下の依存関係を追加します。その後、`pod install`コマンドを実行すると、インポートが完了します。
```swift
# TXLiteAVSDK
pod 'TXLiteAVSDK_TRTC'

# :path => "TXAppBasic.podspecのあるディレクトリを指定する相対パス"
pod 'TXAppBasic', :path => "../SDK/TXAppBasic/"

# :path => "TCBeautyKit.podspecのあるディレクトリを指定する相対パス"
pod 'TCBeautyKit', :path => "../SDK/TCBeautyKit/"

# :path => "TUIRoom.podspecのあるディレクトリを指定する相対パス"
pod 'TUIRoom', :path => "../", :subspecs => ["TRTC"]
```

>! `Source`、`Resources`フォルダと`TUIRoom.podspec`ファイルは同一のディレクトリ下にある必要があります。
>-  TXAppBasic.podspecはTXAppBasicフォルダ下にあります。
>-  TCBeautyKit.podspecはTCBeautyKitフォルダ下にあります。

### ステップ2：権限の設定

オーディオビデオ機能を使用するには、マイクおよびカメラの使用権限を付与する必要があります。AppのInfo.plistで以下の2項を追加します。これらはシステムが権限付与ダイアログボックスをポップアップする際に表示される、マイクとカメラのメッセージにそれぞれ対応します。
- **Privacy - Microphone Usage Description**、さらにマイク使用目的のプロンプトを記入します。
- **Privacy - Camera Usage Description**、さらにカメラ使用目的のプロンプトを記入します。

![](https://qcloudimg.tencent-cloud.cn/raw/224ae568f11d50124ea663ac0ef1c6e9.png)

### ステップ3：コンポーネントの作成およびログイン
1.  TUICoreのTUILoginを呼び出してログインします。次の例をご参照ください。
```swift
TUILogin.initWithSdkAppID(Int32("あなたのsdkAppID"))
TUILogin.login("あなたのuserId", userSig: "あなたのuserSig", succ: {
     debugPrint("login success")
}, fail: { code, errorDes in
     debugPrint("login failed, code:\(code), error: \(errorDes ?? "nil")")
})
```

**パラメータの説明**
- **SDKAppID**：**TRTCアプリケーションID**です。Tencent Cloud TRTCサービスをアクティブ化していない場合は、[Tencent Cloud TRTCコンソール](https://console.cloud.tencent.com/trtc/app)に進み、新しいTRTCアプリケーションを作成した後、**アプリケーション情報**をクリックすると、SDKAppID情報が次の図のように表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**：**TRTC アプリケーションキー**であり、SDKAppIdに対応しています。[TRTCアプリケーション管理](https://console.cloud.tencent.com/trtc/app)に進むと、SecretKey情報が上の図のように表示されます。
- **userId**：現在のユーザーID。文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。業務の実際のアカウントシステムと組み合わせてご自身で設定することをお勧めします。
- **userSig**：SDKAppId、userId，Secretkeyなどの情報に基づく計算によって得られるセキュリティ保護署名です。[ここ](https://console.cloud.tencent.com/trtc/usersigtool)をクリックするとデバッグ用のUserSigがオンラインで直接生成されます。また当社の[デモプロジェクト](https://github.com/tencentyun/TUIRoom/blob/main/iOS/Example/Debug/GenerateTestUserSig.swift#L42) を参照してご自身で計算することもできます。その他の情報については、[UserSigの計算、使用方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

### ステップ4：多人数オーディオビデオインタラクションの実装

1. **管理者による多人数オーディオビデオインタラクションルーム作成の実装[TUIRoomCore#createRoom](https://intl.cloud.tencent.com/document/product/647/37282)**。
```swift
let roomId = 123
TUIRoomCore.shareInstance().createRoom("\(roomId)",speechMode: .freeSpeech,callback: { [weak self] code, message in
    if code == 0 {
       debugPrint("create room success") 
    }else{
    }
})
```
2. **他メンバーのオーディオビデオルーム入室の実装  [TUIRoomCore#enterRoom](https://intl.cloud.tencent.com/document/product/647/37282)**。
```swift
let roomId = 123
TUIRoomCore.shareInstance().enterRoom("\(roomId)", callback: { [weak self] code, message in
    if code == 0 {
       debugPrint("enter room success") 
   }else{
   }
})
```
3. **退室の実装** 
	- **キャスター**は[TUIRoomCore#destroyRoom](https://intl.cloud.tencent.com/document/product/647/37282)インターフェースを呼び出してルームを解散し、IMグループチャットを解散し、TRTCルームから退出します。 メンバー側は、グループの解散を通知するonDestroyRoomコールバックメッセージを受信し、TRTCルームから退出します。
	- **メンバー**は[TUIRoomCore#leaveRoom](https://intl.cloud.tencent.com/document/product/647/37282)インターフェースを呼び出してルームを解散し、IMグループチャットから退出し、TRTCルームから退出します。 その他のメンバー側は、メンバーが退室したことを通知するonRemoteUserLeaveコールバックメッセージを受信します。
```swift
if isHomeowner {
    TUIRoomCore.shareInstance().destroyRoom { [weak self] _, _ in
        guard let self = self else { return }
        self.navigationController?.popViewController(animated: true)
    }
}else{
    TUIRoomCore.shareInstance().leaveRoom { [weak self] _, _ in
        guard let self = self else { return }
        self.navigationController?.popViewController(animated: true)
    }
 }
```
4. **画面共有の実装 [TUIRoomCore#startScreenCapture](https://intl.cloud.tencent.com/document/product/647/37282)**。
	- TUIRoomCoreの`startScreenCapture`を呼び出して共有します。
	- ルーム内の他のメンバーは`onRemoteUserScreenVideoAvailable`のイベント通知を受信します。
```swift
// ボタンのクリックで画面共有を実現します
if #available(iOS 12.0, *) {
    // 画面共有
    let params = TRTCVideoEncParam()
    params.videoResolution = TRTCVideoResolution._1280_720
    params.resMode = TRTCVideoResolutionMode.portrait
    params.videoFps = 10
    params.enableAdjustRes = false
    params.videoBitrate = 1500
    TUIRoomCore.shareInstance().startScreenCapture(params)
    TUIRoomBroadcastExtensionLauncher.launch()
}else{
    view.window?.makeToast(.versionLowToastText)
}    
```

## よくあるご質問
### CocoaPodsをインストールするにはどうすればよいですか。

端末のウィンドウに次のコマンドを入力します（事前にMac にRuby環境をインストールしておく必要があります ）。
```
sudo gem install cocoapods
```

>? ご要望やフィードバックなどがございましたら、colleenyu@tencent.comまでご連絡ください。

