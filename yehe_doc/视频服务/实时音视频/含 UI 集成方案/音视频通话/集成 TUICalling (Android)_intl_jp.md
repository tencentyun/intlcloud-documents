## コンポーネントの説明

TUICallingはオープンソースのオーディオビデオUIコンポーネントであり、プロジェクトにTUICallingコンポーネントを統合することにより、数行のコードを書くだけで、Appに「1対1オーディオビデオ通話」などのシナリオを組み込むことができ、さらにオフラインでのリマインダー機能もサポートしています。TUICallingはまたiOS、Web、Flutter、UniAppなどのプラットフォームでもサポートしています。基本機能は下図のとおりです：

>?TUIKitシリーズコンポーネントはTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047/35448)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMサービスの課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。TRTCをアクティブにすると、デフォルトでは、100DAUまでサポートするIM SDK体験版もアクティブになります。

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/af697557d2746585a0d9f4b894dc42d5.png" </td>
</tr>
</tbody></table>

>?TUICallingコンポーネントはTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/zh/document/product/1047)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMサービスの課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。TRTCをアクティブにすると、デフォルトでは、100DAUまでサポートするIM SDK体験版もアクティブにします。

## コンポーネントの統合

### ステップ1：TUICallingコンポーネントのダウンロードとインポート
クリックして[Github](https://github.com/tencentyun/TUICalling)に進み、コードのクローン/ダウンロードを選択した後、Androidディレクトリ下のtuicallingおよびdebugディレクトリをプロジェクトのappの同一階層のディレクトリにコピーし、次のようにインポート動作を完了します：
- `setting.gradle`へのインポートを完了します。以下をご参照ください：
```java
include ':tuicalling'
include ':debug'
```
- appのbuild.gradleファイルにtuicallingに対する依存関係を追加します：
```java
api project(':tuicalling')
```
- ルートディレクトリの`build.gradle`ファイルに`TRTC SDK`および`IM SDK`の依存関係を追加します：
```java
ext {
    liteavSdk = "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    imSdk = "com.tencent.imsdk:imsdk-plus:latest.release"
}
```

### ステップ2：権限の設定および難読化ルール

1. AndroidManifest.xmlにAppの権限を設定します。SDKには次の権限が必要です（6.0以上のAndroidシステムではカメラ、マイク、ストレージ読み取りの権限などを動的に申請してください）：
```java
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />        // ユースケース：フローティングウィンドウ、アプリケーションがバックエンドにあるときに通話画面をプルアップする場合はこの権限が必要です。
<uses-permission android:name="android.permission.INTERNET" />              
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />                  // ユースケース：Bluetoothイヤホンを使用する場合はこの権限が必要です。
<uses-permission android:name="android.permission.READ_PHONE_STATE" />           // ユースケース：システムが着信を中断したかどうかを判断する場合はこの権限が必要です。
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature android:name="android.hardware.camera"/>
<uses-feature android:name="android.hardware.camera.autofocus" />
```
2. proguard-rules.proファイルでは、SDK関連クラスを非難読化リストに追加します。
```
-keep class com.tencent.** { *; }
```

### ステップ3：コンポーネントの作成と初期化

```java
// 1.イベント監視およびログインを追加します
TUILogin.addLoginListener(new TUILoginListener() {
    @Override
    public void onConnecting() {      // 接続中
        super.onConnecting();
    }
    @Override
    public void onConnectSuccess() {  // 接続成功通知
        super.onConnectSuccess();
    }
    @Override
    public void onConnectFailed(int errorCode, String errorMsg) {  // 接続失敗通知
        super.onConnectFailed(errorCode, errorMsg);
    }
    @Override
    public void onKickedOffline() {  //  ログインがキックアウトされたオフライン通知（例：アカウントが他のデバイスでログインしている）
        super.onKickedOffline();
    }
    @Override
    public void onUserSigExpired() { // userSig期限切れ通知
        super.onUserSigExpired();
    }
});
TUILogin.login(mContext, "Your SDKAppID", "Your userId", "Your userSig", new TUICallback() {
    @Override
    public void onSuccess() {
    }
    @Override
    public void onError(int errorCode, String errorMsg) {
        Log.d(TAG, "errorCode: " + errorCode + " errorMsg:" + errorMsg);
    }
});
// 2.TUICallingインスタンスの初期化
TUICalling callingImpl = TUICallingImpl.sharedInstance(context);
```
**パラメータの説明**：
- **SDKAppID**：**TRTCアプリケーションID**です。Tencent Cloud TRTCサービスをアクティブ化していない場合は、[Tencent Cloud TRTCコンソール](https://console.cloud.tencent.com/trtc/app)に進み、新しいTRTCアプリケーションを作成した後、**アプリケーション情報**をクリックすると、SDKAppID情報が次の図のように表示されます：
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**：**TRTCアプリケーションキー**であり、SDKAppIdに対応しています。[TRTCアプリケーション管理](https://console.cloud.tencent.com/trtc/app)に進むと、SecretKey情報が上の図のように表示されます。
- **userId**：現在のユーザーのIDです。文字列タイプであり、長さは32バイト以内とし、特殊文字の使用はサポートしていません。英語または数字の使用をお勧めします。業務の実際のアカウントシステムと組み合わせてご自身で設定することができます。
- **userSig**：SDKAppId、userId，Secretkeyなどの情報に基づく計算によって得られるセキュリティ保護署名です。[ここ](https://console.cloud.tencent.com/trtc/usersigtool)をクリックするとデバッグ用のUserSigがオンラインで直接生成されます。[UserSigの計算、使用方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。


### ステップ4：オーディオビデオ通話の実装
**1対1ビデオ通話/オーディオ通話の実装[TUICalling#call](https://intl.cloud.tencent.com/document/product/647/43140)**
```java
// 1対1ビデオ通話を開始します。userIdは1111と仮定します。
callingImpl.call(["1111"], TUICalling.Type.VIDEO);
```


>? 
>- 受信側がステップ3を完了、すなわちログインに成功した後、再度通話リクエストを受信した場合、TUICallingコンポーネントは対応する応答画面を自動的に起動します。    
>- 音声通話を開始したい場合は、タイプを`TUICalling.Type.AUDIO`に変更します。

### ステップ5：オフラインプッシュ（オプション）

上記の4ステップが完了すると、オーディオビデオ通話の発信と接続が実現できますが、業務シーン上、`Appのプロセスが強制終了された後`または`APPがバックエンドに戻った後`も、オーディオビデオ通話リクエストを正常に受信できる必要がある場合は、TUICallingコンポーネントにオフラインプッシュ機能を追加してください。

### ステップ6：ステータスの監視（オプション）
業務上、通話の開始や終了などの[通話ステータスの監視](https://intl.cloud.tencent.com/document/product/647/43140)が必要な場合は、次のイベントを監視することができます。
```
callingImpl.setCallingListener(new TUICalling.TUICallingListener() {
    @Override
    public boolean shouldShowOnCallView() {
        return true;
    }

    @Override
    public void onCallStart(String[] userIDs, TUICalling.Type type, TUICalling.Role role, View tuiCallingView) {

    }

    @Override
    public void onCallEnd(String[] userIDs, TUICalling.Type type, TUICalling.Role role, long totalTime) {

    }

    @Override
    public void onCallEvent(TUICalling.Event event, TUICalling.Type type, TUICalling.Role role, String message) {
        Log.d(TAG, "onCallEvent: event = " + event + " ,message = " + message);
    }
});
```

### ステップ7：フローティングウィンドウ機能（オプション）
業務上、フローティングウィンドウ機能を有効にする必要がある場合は、TUICallingコンポーネントの初期化の際に`callingImpl.enableFloatWindow(true)`を呼び出してこの機能を有効化することができます。

現在、コンポーネントは次の2つの状況でのフローティングウィンドウをサポートしています。
- システムフローティングウィンドウ(homeキーをクリックしてバックエンドに戻る)：フローティングウィンドウの権限を有効にしてください。
- アプリケーション内のフローティングウィンドウ（最小化して前の画面に戻る）：フローティングウィンドウの権限を有効にし、戻る1つ前の画面を設定してください。
フローティングウィンドウの権限を有効にする方法：**スマートフォンの設定**を開き、**アプリケーション管理**からアプリケーションを見つけ、**権限**をクリックし、**フローティングウィンドウの許可**をクリックします（スマートフォンのメーカー、プラットフォームにより、これらの位置が異なる場合があります）。

戻る1つ前の画面を設定するには、`AndroidManifest.xml`でリダイレクト先の画面へのリダイレクト動作 `com.tencent.trtc.tuicalling`を設定する必要があります。例えば次のように行います：
```
<activity
    android:name="{packageName}.MainActivity"
    android:launchMode="singleTop">
    <intent-filter>
        <action android:name="com.tencent.trtc.tuicalling" /> 
        <category android:name="android.intent.category.DEFAULT" />
    </intent-filter>
</activity>
```

## よくあるご質問

### TUICallingコンポーネントはプロフィール画像とニックネームのカスタマイズをサポートしていますか？

サポートしています。`setUserNickname/setUserAvatar`を呼び出して行うことができます。

### TUICallingコンポーネントは着信音のカスタマイズをサポートしていますか？
サポートしています。[setCallingBell](https://intl.cloud.tencent.com/document/product/647/43140)を呼び出して行うことができます。

>? ご要望やフィードバックなどがございましたら、colleenyu@tencent.comまでご連絡ください。
