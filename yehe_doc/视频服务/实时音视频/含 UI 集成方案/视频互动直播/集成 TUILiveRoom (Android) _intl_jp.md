## コンポーネントの説明

TUILiveRoomはオープンソースのビデオライブストリーミングUIコンポーネントであり、プロジェクトにTUILiveRoomコンポーネントを統合することにより、数行のコードを書くだけで、Appに「ビデオインタラクティブストリーミング」のシーンを組み込むことができます。TUILiveRoomにはAndroid、iOS、ミニプログラムなどのプラットフォーム用のソースコードが含まれます。基本機能は下図のとおりです：

>?TUIKitシリーズコンポーネントはTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047/35448)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMサービスの課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。TRTCをアクティブにすると、デフォルトでは、100DAUまでサポートするIM SDK体験版もアクティブになります。

<table>
<tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/a1b4b04662bb342de1e7b713cb3f59ce.png"></td>
</tr>
</table>

[](id:model)
## コンポーネントの統合
[](id:model.step1)
### ステップ1：TUILiveRoomコンポーネントのダウンロードとインポート
クリックして[Github](https://github.com/tencentyun/TUILiveRoom)に進み、コードのクローン/ダウンロードを選択した後、`Android/debug` 、`Android/tuiaudioeffect` 、 `Android/tuibarrage` 、 `Android/tuibeauty` 、 `Android/tuigift` と `Android/tuiliveroom`ディレクトリをプロジェクトにコピーし、次のようにインポート動作を完了します。

- `setting.gradle`へのインポートを完了します。以下をご参照ください：
```
include ':debug'
include ':tuibeauty'
include ':tuibarrage'
include ':tuiaudioeffect'
include ':tuigift'
include ':tuiliveroom'
```
- `app`の`build.gradle`ファイルに`tuiliveroom`に対する依存関係を追加します：
```
api project(":tuiliveroom")
```
- ルートディレクトリの`build.gradle`ファイルに`TRTC SDK`および`IM SDK`の依存関係を追加します：
```
ext {
    liteavSdk = "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    imSdk = "com.tencent.imsdk:imsdk-plus:latest.release"
}
```

[](id:model.step2)
### ステップ2：権限の設定および難読化ルール
1. AndroidManifest.xmlにAppの権限を設定します。SDKには次の権限が必要です（6.0以上のAndroidシステムではカメラ、ストレージ読み取りの権限を動的に申請してください）：
```java
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-feature android:name="android.hardware.camera"/>
<uses-feature android:name="android.hardware.camera.autofocus" />
```
2. proguard-rules.proファイルでは、SDK関連クラスを非難読化リストに追加します：
```java
-keep class com.tencent.** { *; }
```

[](id:model.step3)
### ステップ3：コンポーネントの初期化およびログイン
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

// 2.TUILiveRoomコンポーネントの初期化
TUILiveRoom mLiveRoom = TUILiveRoom.sharedInstance(mContext);
```

**パラメータの説明：**
- **SDKAppID**：**TRTCアプリケーションID**です。Tencent Cloud TRTCサービスをアクティブ化していない場合は、[Tencent Cloud TRTCコンソール](https://console.cloud.tencent.com/trtc/app)に進み、新しいTRTCアプリケーションを作成した後、**アプリケーション情報**をクリックすると、SDKAppID情報が次の図のように表示されます：
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**：**TRTC アプリケーションキー**であり、SDKAppIdに対応しています。[TRTCアプリケーション管理](https://console.cloud.tencent.com/trtc/app)に進むと、SecretKey情報が上の図のように表示されます。
- **userId**：現在のユーザーID。文字列タイプであり、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。業務の実際のアカウントシステムと組み合わせてご自身で設定することをお勧めします。
- **userSig**：SDKAppId、userId、Secretkeyなどの情報に基づく計算によって得られるセキュリティ保護署名です。[ここ](https://console.cloud.tencent.com/trtc/usersigtool)をクリックするとデバッグ用のuserSigがオンラインで直接生成されます。[UserSigの計算、使用方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。


[](id:model.step4)
### ステップ4：ビデオインタラクティブストリーミングルームの実装
1. **キャスター側の配信開始**
```java
mLiveRoom.createRoom(int roomId, String roomName, String coverUrl);
```
2. **視聴者側の視聴**
```java
mLiveRoom.enterRoom(roomId);
```
3. **視聴者とキャスターがマイク接続 [TRTCLiveRoom#requestJoinAnchor](https://intl.cloud.tencent.com/document/product/647/37333)**
```java
// 1.視聴者側がマイク接続のリクエストを送信します
// LINK_MIC_TIMEOUTはタイムアウト時間です
TRTCLiveRoom mTRTCLiveRoom=TRTCLiveRoom.sharedInstance(mContext);
mTRTCLiveRoom.requestJoinAnchor(mSelfUserId + "あなたとのマイク接続をリクエスト", LINK_MIC_TIMEOUT
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // キャスターが視聴者のリクエストを受け入れます
            TXCloudVideoView view = new TXCloudVideoView(context);
            parentView.add(view);
            // 視聴者がプレビューを起動し、プッシュを開始します
            mTRTCLiveRoom.startCameraPreview(true, view, null);
            mTRTCLiveRoom.startPublish(mSelfUserId + "_stream", null);
        }
    }
});

// 2.キャスター側がマイク接続のリクエストを受信します
mTRTCLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestJoinAnchor(final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, 
        String reason, final int timeout) {
        // 相手のマイク接続のリクエストに同意します
        mTRTCLiveRoom.responseJoinAnchor(userInfo.userId, true, "マイク接続に同意");
    }

    @Override
    public void onAnchorEnter(final String userId) {
        // キャスターがマイク接続の視聴者のマイク・オンの通知を受信します
        TXCloudVideoView view = new TXCloudVideoView(context);
        parentView.add(view);
        // キャスターが視聴者の画面を再生します
        mTRTCLiveRoom.startPlay(userId, view, null);
    }
});
```
4. **キャスター間のPK [TRTCLiveRoom#requestRoomPK](https://intl.cloud.tencent.com/document/product/647/37333#requestroompk)**
```java
// キャスターAがルーム12345を作成します
mLiveRoom.createRoom(12345, "roomA", "Your coverUrl");
// キャスターBがルーム54321を作成します
mLiveRoom.createRoom(54321, "roomB", "Your coverUrl");

// キャスターA:
TRTCLiveRoom mTRTCLiveRoom=TRTCLiveRoom.sharedInstance(mContext);

// 1.キャスターAがキャスターBにPKのリクエストを送信します
mTRTCLiveRoom.requestRoomPK(54321, "B", 
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {  
        // 5.同意の有無のコールバックを受信します
        if (code == 0) {
            // ユーザー受け入れ
        }else{
            // ユーザー拒否
        }
    }
});

mTRTCLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onAnchorEnter(final String userId) {
        // 6.Bのルーム参加の通知を受信します
        mTRTCLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});

// キャスターB：
// 2.キャスターBがキャスターAのメッセージを受信します
mTRTCLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestRoomPK(
       final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, final int timeout) {
        // 3.キャスターBがキャスターAに回答し、リクエストを受け入れます
        mTRTCLiveRoom.responseRoomPK(userInfo.userId, true, "");
    }
    @Override
    public void onAnchorEnter(final String userId) {
        // 4.キャスターBがキャスターAのルーム参加の通知を受信し、キャスターAの画面を再生します
        mTRTCLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});
```

## よくあるご質問
ご要望やフィードバックなどがございましたら、colleenyu@tencent.comまでご連絡ください。
