## コンポーネントの説明
TUIRoomはオープンソースのオーディオビデオUIコンポーネントであり、プロジェクトにTUIRoomコンポーネントを統合することにより、数行のコードを書くだけで、Appに画面共有、美顔、低遅延ビデオ通話などを組み込むことができます。TUIRoomはまた、[iOS](https://intl.cloud.tencent.com/document/product/647/37284)、[Windows](https://intl.cloud.tencent.com/document/product/647/44071)、[Mac](https://intl.cloud.tencent.com/document/product/647/44071)などのプラットフォームでもサポートしています。基本機能は下図のとおりです：

>?TUIKitシリーズコンポーネントはTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047/35448)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMサービスの課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。TRTCをアクティブにすると、デフォルトでは、100DAUまでサポートするIM SDK体験版もアクティブになります。

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/2944bac3c5d348b06d2a11c439783b48.png"></td>
</tr>
</tbody></table>

## コンポーネントの統合
### ステップ1：TUIRoomコンポーネントのダウンロードとインポート
クリックして[Github](https://github.com/tencentyun/TUIRoom)に進み、コードのクローン/ダウンロードを選択した後、Android下のtuiroom、debug、tuibeautyディレクトリをプロジェクトにコピーし、次のようにインポート動作を完了します：
1. `setting.gradle`へのインポートを完了します。以下をご参照ください：
```
include ':tuiroom'
include ':debug'
include ':tuibeauty'
```
2. appの`build.gradle`ファイルにtuiroom、debug、tuibeautyに対する依存関係を追加します：
```
api project(':tuiroom')
api project(':debug')
api project(':tuibeauty')
```
3. ルートディレクトリの`build.gradle`ファイルに`TRTC SDK`および`IM SDK`の依存関係を追加します：
```
ext {
    liteavSdk = "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    imSdk = "com.tencent.imsdk:imsdk-plus:latest.release"
}
```

### ステップ2：権限の設定および難読化ルール
1. AndroidManifest.xmlにAppの権限を設定します。SDKには次の権限が必要です（6.0以上のAndroidシステムではマイクの権限などを動的に申請してください）：
```
<uses-permission android:name="android.permission.INTERNET" />              
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature android:name="android.hardware.camera"/>
<uses-feature android:name="android.hardware.camera.autofocus" />
```
2. proguard-rules.proファイルでは、SDK関連クラスを非難読化リストに追加します：
```
-keep class com.tencent.** { *; }
```

### ステップ3：TUIコンポーネントリポジトリの作成と初期化
```java
// 1.コンポーネントのログイン
TUILogin.addLoginListener(new TUILoginListener() {
    @Override
    public void onKickedOffline() {  //  ログインがキックアウトされたオフライン通知（例：アカウントが他のデバイスでログインしている）
    }

    @Override
    public void onUserSigExpired() { // userSig期限切れ通知
    }
});

TUILogin.login(context, "あなたのSDKAppId", "あなたのuserId", "あなたのuserSig", null);


// 2.TUIRoomインスタンスの初期化
TUIRoom tuiRoom = TUIRoom.sharedInstance(this);
```

#### パラメータの説明
- **SDKAppID**：**TRTCアプリケーションID**です。Tencent Cloud TRTCサービスをアクティブ化していない場合は、[Tencent Cloud TRTCコンソール](https://console.cloud.tencent.com/trtc/app)に進み、新しいTRTCアプリケーションを作成した後、**アプリケーション情報**をクリックすると、SDKAppID情報が次の図のように表示されます：
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**：**TRTC アプリケーションキー**であり、SDKAppIdに対応しています。[TRTCアプリケーション管理](https://console.cloud.tencent.com/trtc/app)に進むと、SecretKey情報が上の図のように表示されます。
- **userId**：現在のユーザーID。文字列タイプであり、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。業務の実際のアカウントシステムと組み合わせてご自身で設定することをお勧めします。
- **userSig**：SDKAppId、userId，Secretkeyなどの情報に基づく計算によって得られるセキュリティ保護署名です。[ここ](https://console.cloud.tencent.com/trtc/usersigtool)をクリックするとデバッグ用のuserSigがオンラインで直接生成されます。また当社の[デモプロジェクト](https://github.com/tencentyun/TUIRoom/blob/main/Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java#L88)を参照してご自身で計算することもできます。その他の情報については、[UserSigの計算、使用方法](https://cloud.tencent.com/document/product/647/17275)をご参照ください。


### ステップ4：多人数オーディオビデオインタラクションの実装
1. **管理者が多人数オーディオビデオインタラクティブルームを作成できるようにします**。
```java
tuiRoom.createRoom(12345, TUIRoomCoreDef.SpeechMode.FREE_SPEECH, true, true);
```
2. **他のメンバーがオーディオビデオルームに参加できるようにします**。
```java
tuiRoom.enterRoom(12345, true, true);
```

### ステップ5：ルーム管理（オプション）
1. **管理者によるルーム解散 [TUIRoomCore#destroyRoom](https://intl.cloud.tencent.com/document/product/647/37281)**。
```java
// 1.管理者が呼び出してルームを解散
mTUIRoomCore.destroyRoom(new TUIRoomCoreCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
                    
    }
});

メンバー側は、ルームの解散を通知するonDestroyRoomコールバックメッセージを受信します
@Override
public void onDestroyRoom() {
    //管理者が解散し、ルームから退出
}
```
2. **メンバーの退室 [TUIRoomCore#leaveRoom](https://intl.cloud.tencent.com/document/product/647/37281)**。
```java
// 1.管理者以外による退室の呼び出し
mTUIRoomCore.leaveRoom(new TUIRoomCoreCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
                    
    }
});

//メンバー側は、退室者があったことを通知するonRemoteUserLeaveコールバックメッセージを受信します
@Override
public void onRemoteUserLeave(String userId) {
        Log.d(TAG, "onRemoteUserLeave userId: " + userId);
}
```

### ステップ6：画面共有（オプション）
画面共有[TUIRoomCore#startScreenCapture](intl.cloud.tencent.com/document/product/647/37281)を実装します。
```java
// 1.AndroidManifest.xmlのファイルの中にSDKのスクリーンレコーディング機能のactivityと権限を追加します
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<application>
    <activity
        android:name="com.tencent.rtmp.video.TXScreenCapture$TXScreenCaptureAssistantActivity"
        android:theme="@android:style/Theme.Translucent" />
</application>

// 2.自分のインターフェースの中でフローティングウィンドウの権限を申請します
if (Build.VERSION.SDK_INT >= 23) {
    if (!Settings.canDrawOverlays(getApplicationContext())) {
        Intent intent = new Intent(Settings.ACTION_MANAGE_OVERLAY_PERMISSION, Uri.parse("package:" + getPackageName()));
        startActivityForResult(intent, 100);
    }else{
        startScreenCapture();
    }
}else{
    startScreenCapture();
}

// 3.システムのコールバックの結果
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    if (requestCode == 100) {
        if (Build.VERSION.SDK_INT >= 23) {
            if (Settings.canDrawOverlays(this)) {
                // ユーザーの権限承認が成功
                startScreenCapture();
            }else{
            }
        }
    }
}

// 4.画面共有の起動
private void startScreenCapture() {
        TRTCCloudDef.TRTCVideoEncParam encParams = new TRTCCloudDef.TRTCVideoEncParam();
        encParams.videoResolution = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_1280_720;
        encParams.videoResolutionMode = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT;
        encParams.videoFps = 10;
        encParams.enableAdjustRes = false;
        encParams.videoBitrate = 1200;

        TRTCCloudDef.TRTCScreenShareParams params = new TRTCCloudDef.TRTCScreenShareParams();
        mTUIRoom.stopCameraPreview();
        mTUIRoom.startScreenCapture(encParams, params);
}
```

## よくあるご質問
ご要望やフィードバックなどがございましたら、colleenyu@tencent.comまでご連絡ください。
