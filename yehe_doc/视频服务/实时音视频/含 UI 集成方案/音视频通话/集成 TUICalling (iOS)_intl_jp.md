## コンポーネントの説明

TUICallingはオープンソースのオーディオビデオUIコンポーネントであり、プロジェクトにTUICallingコンポーネントを統合することにより、数行のコードを書くだけで、Appに「1対1オーディオビデオ通話」、「多人数オーディオビデオ通話」などのシーンを組み込むことができ、さらにオフラインでのリマインダー機能もサポートしています。TUICallingはまたAndroid、Web、ミニプログラム、Flutter、UniAppなどのプラットフォームでもサポートしています。基本機能は下図のとおりです。

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/94bbec9961b0d569cc7068389dc41412.jpg" width="400"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/534089ed0be5c78fb63c65cde79ad866.jpg" width="400"></td>
</tr>
</tbody></table>


## コンポーネントの統合

### ステップ1：TUICallingコンポーネントのインポート

**cocoapodsによってコンポーネントをインポートします**。具体的な手順については、以下のとおりです。
1. プロジェクトの`Podfile`ファイルと同じ階層のディレクトリ下に`TUICalling`フォルダを作成します。
2. クリックして[**Github/TUICalling**](https://github.com/tencentyun/TUICalling)に進み、コードのクローン/ダウンロードを選択した後、[**TUICalling/iOS/**](https://github.com/tencentyun/TUICalling/tree/main/iOS)ディレクトリ下の`Source`、`Resources`フォルダ、`TUICalling.podspec`ファイルを、`ステップ1`で作成したTUICallingフォルダ下にコピーします。
3. Podfileファイル内に以下の依存関係を追加します。その後、`pod install`コマンドを実行すると、インポートが完了します。
```
# :path => "TUICalling.podspecを指定する相対パス"
pod 'TUICalling', :path => "TUICalling/TUICalling.podspec", :subspecs => ["TRTC"]
```

>! `Source`、`Resources`フォルダと`TUICalling.podspec`ファイルは同一のディレクトリ下にある必要があります。

### ステップ2：権限の設定

オーディオビデオ機能を使用するには、マイクおよびカメラの使用権限を付与する必要があります。AppのInfo.plistで以下の2項を追加します。これらはシステムが権限付与ダイアログボックスをポップアップする際に表示される、マイクとカメラのメッセージにそれぞれ対応します。

```
<key>NSCameraUsageDescription</key>
<string>CallingAppはカメラへのアクセス権限が必要です。有効にした後にレコーディングしたビデオでなければ画面は出ません</string>
<key>NSMicrophoneUsageDescription</key>
<string>CallingAppはマイクへのアクセス権限が必要です。有効にした後にレコーディングしたビデオでなければ音声は出ません</string>
```
![](https://qcloudimg.tencent-cloud.cn/raw/224ae568f11d50124ea663ac0ef1c6e9.png)

### ステップ3：コンポーネントの作成と初期化

<dx-tabs>
:::  Objective-C
```
// 1.コンポーネントのログイン
[TUILogin initWithSdkAppID:@"あなたのSDKAppID"];
[TUILogin login:@"あなたのUserID" userSig:@"あなたのUserSig" succ:^{
    NSLog(@"login success");
} fail:^(int code, NSString *msg) {
    NSLog(@"login failed, code: %d, error: %@", code, msg);
}];

// 2.TUICallingインスタンスの初期化
[TUICalling shareInstance];
```
:::
::: Swift
```
// 1.コンポーネントのログイン
TUILogin.initWithSdkAppID("あなたのSDKAppID")
TUILogin.login("あなたのUserID", userSig: "あなたのUserSig") {
    print("login success")
} fail: { code, message in
    print("login failed, code: \(code), error: \(message ?? "nil")")
}

// 2.TUICallingインスタンスの初期化
TUICalling.shareInstance()
```
:::
</dx-tabs>

**パラメータの説明**：
- **SDKAppID**：**TRTCアプリケーションID**です。Tencent Cloud TRTCサービスをアクティブ化していない場合は、[Tencent Cloud TRTCコンソール](https://console.cloud.tencent.com/trtc/app)に進み、新しいTRTCアプリケーションを作成した後、**アプリケーション情報**をクリックすると、SDKAppID情報が次の図のように表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **SecretKey**：**TRTC アプリケーションキー**であり、SDKAppIDに対応しています。[TRTCアプリケーション管理](https://console.cloud.tencent.com/trtc/app)に進むと、SecretKey情報が上の図のように表示されます。
- **UserID**：現在のユーザーのIDです。文字列形式で、長さは32バイト以内とし、特殊文字の使用はサポートしていません。英語または数字の使用をお勧めします。業務の実際のアカウントシステムと組み合わせてご自身で設定することができます。
- **UserSig**：SDKAppId、UserID、SecretKeyなどの情報に基づく計算によって得られるセキュリティ保護署名です。[ここ](https://console.cloud.tencent.com/trtc/usersigtool)をクリックするとデバッグ用のUserSigがオンラインで直接生成されます。また当社の[TUICallingデモプロジェクト](https://github.com/tencentyun/TUICalling/blob/main/iOS/Example/Debug/GenerateTestUserSig.swift#L39)を参照してご自身で計算することもできます。その他の情報については、[UserSigの計算、使用方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

### ステップ4：オーディオビデオ通話の実装

- 1対1ビデオ通話の実装[TUICalling#call](https://intl.cloud.tencent.com/document/product/647/43139)
<dx-codeblock>
:::  Objective-C Objectivec
// 1対1ビデオ通話を開始します。userIdは1111と仮定します
[[TUICalling shareInstance] call:@[@"1111"] type:TUICallingTypeVideo];
:::
::: Swift Swift
// 1対1ビデオ通話を開始します。userIdは1111と仮定します
TUICalling.shareInstance().call(userIDs: ["1111"], type: .video)
:::
</dx-codeblock>
- 多人数ビデオ通話の実装[TUICalling#call](https://intl.cloud.tencent.com/document/product/647/43139)
<dx-codeblock>
:::  Objective-C Objectivec
// 多人数ビデオ通話を開始します。userIdはそれぞれ1111、2222、3333と仮定します
[[TUICalling shareInstance] call:@[@"1111", @"2222", @"3333"] type:TUICallingTypeVideo];
:::
::: Swift Swift
// 多人数ビデオ通話を開始します。userIdはそれぞれ1111、2222、3333と仮定します
TUICalling.shareInstance().call(userIDs: ["1111", "2222", "3333"], type: .video)
:::
</dx-codeblock>

>? 受信側がステップ3を完了、すなわちログインに成功した後、再度通話リクエストを受信した場合、TUICallingコンポーネントは対応する応答画面を自動的に起動します。

### ステップ5：オフラインプッシュ（オプション）
上記の4ステップが完了すると、ビデオ通話の発信と接続が実現できますが、業務シーン上、`Appのプロセスが強制終了された後`または`Appがバックエンドに戻った後`も、オーディオビデオ通話リクエストを正常に受信できる必要がある場合は、TUICallingコンポーネントにオフラインプッシュ機能を追加する必要があります。詳細については、[**オフラインプッシュ（iOS）**](https://intl.cloud.tencent.com/document/product/1047/39157)をご参照ください。

### ステップ6：ステータスの監視（オプション）

業務上、通話の開始や終了などの[通話ステータスの監視](https://intl.cloud.tencent.com/document/product/647/43139)が必要な場合は、次のイベントを監視することができます。
<dx-codeblock>
:::  Objective-C Objectivec
[[TUICalling shareInstance] setCallingListener:self];

- (BOOL)shouldShowOnCallView {
    return YES;
}

- (void)callStart:(nonnull NSArray<NSString *> *)userIDs type:(TUICallingType)type role:(TUICallingRole)role viewController:(UIViewController * _Nullable)viewController {

}

- (void)callEnd:(nonnull NSArray<NSString *> *)userIDs type:(TUICallingType)type role:(TUICallingRole)role totalTime:(float)totalTime {

}

- (void)onCallEvent:(TUICallingEvent)event type:(TUICallingType)type role:(TUICallingRole)role message:(nonnull NSString *)message {

}
:::
::: Swift Swift
TUICalling.shareInstance().setCallingListener(listener: self)

public func shouldShowOnCallView() -> Bool {
    return true
}
    
public func callStart(userIDs: [String], type: TUICallingType, role: TUICallingRole, viewController: UIViewController?) {

}
    
public func callEnd(userIDs: [String], type: TUICallingType, role: TUICallingRole, totalTime: Float) {

}
    
public func onCallEvent(event: TUICallingEvent, type: TUICallingType, role: TUICallingRole, message: String) {

}
:::
</dx-codeblock>

### ステップ7：フローティングウィンドウ機能（オプション）

業務上、[フローティングウィンドウ機能](https://intl.cloud.tencent.com/document/product/647/43139)を有効にする必要がある場合は、TUICallingコンポーネントの初期化の際に`TUICalling.shareInstance().enableFloatWindow(enable: true)`を呼び出してこの機能を有効化することができます。

>? 現在、コンポーネントではアプリケーション内のフローティングウィンドウのみサポートしています（最小化して前の画面に戻る）。

## よくあるご質問

### TUICallingコンポーネントは着信音のカスタマイズをサポートしていますか。

サポートしています。[TUICalling#setCallingBell](https://intl.cloud.tencent.com/document/product/647/43139)を呼び出して行うことができます。

### CocoaPodsをインストールするにはどうすればよいですか。

端末のウィンドウに次のコマンドを入力します（事前にMac にRuby環境をインストールしておく必要があります ）。
```
sudo gem install cocoapods
```

### TUICallingはバックエンドでの実行をサポートしていますか。

サポートしています。バックグラウンドに入っても、依然として関連機能が動作するようにしたい場合は、現在のプログラムのプロジェクトを選択し、**Capabilities** の下の**Background Modes**の設定を **ON**にして、**Audio、AirPlay and Picture in Picture**にチェックを入れます。次の図のとおりです。
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)

>? ご要望やフィードバックなどがございましたら、colleenyu@tencent.comまでご連絡ください。
