## デモンストレーション
当社のDemoを[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)して、インストールし、複数人ビデオ会議の効果を体験いただけます。これには、画面共有、美顔、低レイテンシーのミーティングなどのTRTCの複数人ビデオミーティングのシーンにおける関連機能が含まれています。











迅速に複数人ビデオ会議の機能にアクセスしたい場合は、当社が提供するDemoをもとに直接修正を加えてフィットさせることも、当社が提供するTRTCMeetingの コンポーネントを使用してカスタマイズしたUIを実現することも可能です。

<span id="DemoUI"> </span>
## Demo の UI の再利用
<span id="ui.step1"></span>
### 手順1：アプリケーションの新規作成
1．Tencent Real-Time Communicationコンソールにログインし、【開発支援】>【[Demoのクイック実行](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. 【今すぐスタート】をクリックし、例えば、`TestMeetingRoom`などアプリケーション名を入力して、【アプリケーション作成】をクリックします。

>?本機能はTencent Cloud [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) と [IM](https://intl.cloud.tencent.com/document/product/1047) という2つの基本的な PaaS サービスを同時に使用し、TRTCをアクティブにした後、IM サービスを同期的にアクティブにすることができます。 IM は付加価値サービスであり、請求ルールの詳細については [Instant Messagingの価格説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。



<span id="ui.step2"></span>
### 手順2：SDKおよびDemoのソースコードをダウンロード
１．マウスを該当するカードまで移動し、【[Github](https://github.com/tencentyun/TRTCSDK/tree/master/Android)】をクリックしてGithub（または【[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Android_latest.zip）】をクリック) にジャンプして、関連するSDK および付属のDemoのソースコードをダウンロードします。
 ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. ダウンロード完了後、Tencent Real-Time Communicationコンソールに戻り、【ダウンロードしました。次のステップ】をクリックすれば、SDKAppIDおよびキー情報をクエリできます。

<span id="ui.step3"></span>
### 手順3：Demoプロジェクトファイルの設定
1．[手順2](#ui.step2) でダウンロードしたソースコードパッケージを解凍します。
2. `Android/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java`のファイルを探して開きます。
3.  `GenerateTestUserSig.java`のファイルの関連するパラメータを設定します。
  <ul><li>SDKAPPID：デフォルトは0、実際のSDKAppIDを設定してください。</li>
  <li>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</li></ul> 
    <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4．Tencent Real-Time Communicationコンソールに戻り、【貼り付け完了。次のステップ】をクリックします。
5.【ガイドを閉じてコンソールへ進む】をクリックします。

>!本書で言及した新規UserSigの作成法は、クライアントコードでSECRETKEYを設定し、この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになり、そのため**のこの手法はローカルDemo実行および機能デバッグにのみ適合します**。
≻ UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

<span id="ui.step4"></span>
### 手順4：Demoの動作
Android Studio（バージョン3.5以上）を使用してソースコードの`TRTCScenesDemo`プロジェクトを開き、【実行】をクリックすれば、本Demoのデバックが開始されます。

<span id="ui.step5"></span>
### 手順5：Demo ソースコードの修正
ソースコードの`trtcmeetingdemo` フォルダは、 ui と modelの2つのサブフォルダを含んでいます。ui フォルダにはインターフェースコードが含まれています。以下の表にはファイルまたはフォルダ及び対応する UIをリストアップして、二次調整を行いやすくしています。

| ファイルまたはフォルダ | 機能説明 |
|:-------:|:--------|
| remote | リモートユーザーのリストのインターフェース |
| widget | 一般的なUIコンポーネント |
| CreateMeetingActivity.java | ミーティング作成のインターフェース |
| MeetingMainActivity.java | ビデオミーティングのメインインターフェース |
| MeetingVideoView.java | TRTC の TXCloudVideoViewをパッケージ化、自分とリモートユーザーのビデオデータの表示に利用します。 |
| MemberEntity.java | UI層のユーザーデータ |
| MemberListAdapter.java | ビデオ会議のメインインターフェースのAdapter |

<span id="model"> </span>
## UIカスタマイズの実装

[ソースコード]のtrtcmeetingdemoフォルダには、 ui と modelの2つのサブフォルダがあり、model フォルダには再利用できるオープンソースコンポーネントTRTCMeetingがあります。`TRTCMeeting.java`ファイルでこのコンポーネントが提供するインターフェース関数を見て、対応するインターフェースを使用して UI のカスタマイズを実現することができます。
![](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)

<span id="model.step1"> </span>
### 手順1： SDKへの統合
多人数ビデオミーティングのコンポーネント TRTCMeetingは、TRTC SDKとIM SDKに依存し、次の手順で2つの SDKをプロジェクトに統合することができます。

**方法一：Mavenリポジトリを介した依存**
1. dependencies に TRTCSDKと IMSDK の依存を追加します。
```
dependencies {
       compile "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
       compile 'com.tencent.imsdk:imsdk:latest.release'
}
```
>?2つの SDK の最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK) および [IM](https://github.com/tencentyun/TIMSDK) の Github トップページで取得することができます。
>
2.  defaultConfig で App が使用する CPU アーキテクチャを指定します。
```
defaultConfig {
      ndk {
          abiFilters "armeabi-v7a"
      }
}
```
3．【Sync Now】をクリックし、自動でSDKをダウンロードし、プロジェクトに統合します。

**方法二：ローカル AARを介した依存**
開発環境でのMavenリポジトリへのアクセスが遅い場合は、ZIPパッケージを直接ダウンロードし、統合ドキュメントに従って手動でプロジェクトに統合することができます。
<table>
<tr>
<th>SDK</th>
<th>ダウンロードページ</th>
<th>統合ガイド</th>
</tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35093">統合ドキュメント</a></td>
</tr>
<tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">統合ドキュメント</a></td>
</tr>
</table>

<span id="model.step2"> </span>
### 手順2：権限の設定および難読化ルール
AndroidManifest.xml にAppの権限を設定します。SDKには次の権限が必要です（6.0以上の Android システムではカメラ、読み取りストレージの権限を動的に申請する必要があります）。
```
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

 proguard-rules.pro ファイルでは、 SDK 関連を非難読化リストに追加します。
```
-keep class com.tencent.** { *;}
```

<span id="model.step3"> </span>
### 手順3：TRTCMeetingコンポーネントのインポート
次のディレクトリ内のすべてのファイルをプロジェクトにコピーします。
```
src/main/java/com/tencent/liteav/meeting/model
```

<span id="model.step4"> </span>
### 手順4：コンポーネントの作成およびログイン
1. `sharedInstance`インターフェースをコールすると、 TRTCMeeting コンポーネントのインスタンスオブジェクトを作成できます。
2. `setDelegate`関数をコールしてコンポーネントのイベント通知を登録します。
3. `login`関数をコールしてコンポーネントのログインを完了します。下表を参考にキーパラメータを入力してください。
 <table>
<tr>
<th>パラメータ名</th>
<th>作用</th>
</tr>
<tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">Tencent Real-Time Communicationコンソール</a> で SDKAppIDを表示できます。</td>
</tr>
<tr>
<td>userId</td>
<td>現在のユーザーID、文字列タイプでは、英語のアルファベット（a-z と A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については、<a href="https://intl.cloud.tencent.com/document/product/647/35166"> UserSigの計算方法</a>をご参照ください。</td>
</tr>
<tr>
<td>callback</td>
<td>ログインのコールバック。成功時に code は0になります。</td>
</tr>
</table>
<pre>
TRTCMeeting trtcMeeting = TRTCMeeting.sharedInstance(this);
trtcMeeting.login(SDKAPPID, userId, userSig, new TRTCMeetingCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            //ログイン成功
        }
    }
});
</pre>

<span id="model.step5"> </span>
### 手順5：多人数ミーティングの新規作成
1. キャスターは、[手順4](#model.step4) でログイン後、`setSelfProfile`をコールして自身のニックネームおよびプロファイル写真を設定することができます。
2. キャスターは、`setDelegate`を呼び出すことで、`createMeeting`のイベントの呼び出しを行い、新しいミーティングルームを作成できます。
3. キャスターは、`startCameraPreview`を呼び出してビデオ画面をキャプチャすることができ、`startMicrophone`を呼び出して音声をキャプチャすることができます。
4. キャスターに美顔のニーズがある場合、画面上に美顔調節ボタンを設置して呼び出し、`getBeautyManager`で美顔設定を行うことができます。
>?エンタープライズ版以外のSDKは変顔やスタンプの機能をサポートしていません。
>

![](https://main.qcloudimg.com/raw/416a1afd87b196a6ef791bf63eeaa5e0.png)

```java
// 1.キャスターがニックネームとプロファイル写真を設定します。
trtcMeeting.setSelfProfile("my_name", "my_avatar", null);

// 2.キャスターがルームを作成します。
trtcMeeting.createMeeting(roomId, new TRTCMeetingCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 3.カメラと音声キャプチャを立ち上げます。
            TXCloudVideoView txCloudVideoView = new TXCloudVideoView(TestMeetingActivity.this);
            parentView.add(view);
            trtcMeeting.startCameraPreview(true, txCloudVideoView);
            trtcMeeting.startMicrophone();
            // 4.美顔を設定します。
            trtcMeeting.getBeautyManager().setBeautyStyle(1);
            trtcMeeting.getBeautyManager().setBeautyLevel(6);
        }
    }
});
```

<span id="model.step6"> </span>
### 手順6：参加者の多人数ミーティングへの参加
1. 参加者は、[手順4](#model.step4) でログイン後、`setSelfProfile`をコールして自身のニックネームおよびプロファイル写真を設定することができます。
2. 参加者は、`enterMeeting`を呼び出し、ミーティングルーム番号を渡すと、ミーティングルームに入ることができます。
3. 参加者は、`startCameraPreview`を呼び出してビデオ画面をキャプチャすることができ、`startMicrophone`を呼び出して音声をキャプチャすることができます。
4. 他の参加者がカメラを立ち上げると、`onUserVideoAvailable`のイベントを受信します。この時`startRemoteView`を呼び出してuserIdを渡すと再生が開始されます。

![](https://main.qcloudimg.com/raw/f33213dea7a32ca9904c066952fcc535.png)

```java
// 1.参加者がニックネームとプロファイル写真を設定します。
trtcMeeting.setSelfProfile("my_name", "my_avatar", null);

// 2.参加者が enterMeetingを呼び出し、ミーティングルームナンバーに参加します
trtcMeeting.enterMeeting(roomId, new TRTCMeetingCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 3.入室に成功したら、自分のカメラとマイクを立ち上げます。同時に美顔機能も立ち上げることができます。
            TXCloudVideoView txCloudVideoView = new TXCloudVideoView(TestMeetingActivity.this);
            parentView.add(view);
            trtcMeeting.startCameraPreview(true, txCloudVideoView);
            trtcMeeting.startMicrophone();
            trtcMeeting.getBeautyManager().setBeautyStyle(1);
            trtcMeeting.getBeautyManager().setBeautyLevel(6);
        }
    }
});

// 4.参加者が他のメンバーのカメラ起動の通知を受信し、再生が開始されます。
trtcMeeting.setDelegate(new TRTCMeetingDelegate() {
    @Override
    public void onUserVideoAvailable(String userId, boolean available) {
        if (available) {
            TXCloudVideoView txCloudVideoView = new TXCloudVideoView(TestMeetingActivity.this);
            parentView.add(view);
            trtcMeeting.startRemoteView(userId, txCloudVideoView);
        }else{
            trtcMeeting.stopRemoteView(userId, null);
        }
    }
});
```

<span id="model.step7"> </span>
### 手順7：画面共有

1. 画面共有機能は、システムにフローティングウィンドウの権限を申請する必要があり、自分で UIの中で特定のロジックを実装する必要があります。
2. `startScreenCapture`を呼び出し、エンコードパラメータとスクリーンキャプチャのプロセスのフローティングウィンドウを渡すと、画面共有機能を実装できます。具体的な情報は、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58)をご参照ください。
3. ミーティング中の他の参加者が、`onUserVideoAvailable`のイベントの通知を受信します。
>!画面共有とカメラのキャプチャの2つは相互排他的な操作です。画面共有機能を立ち上げたい時は、先に`stopCameraPreview`を呼び出し、カメラのキャプチャをオフにしてください。

```java
// 1.AndroidManifest.xmlのファイルの中にSDKのスクリーンキャプチャ機能のactivityと権限を追加します。
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<application>
    <activity
        android:name="com.tencent.rtmp.video.TXScreenCapture$TXScreenCaptureAssistantActivity"
        android:theme="@android:style/Theme.Translucent" />
</application>
// 2.自分のインターフェースの中でフローティングウィンドウの権限を申請します。
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
        mTRTCMeeting.stopCameraPreview();
        mTRTCMeeting.startScreenCapture(encParams, params);
}
```

<span id="model.step8"> </span>
### 手順8：文字チャットと禁止ワードメッセージの実現
- `sendRoomTextMsg`によって通常のテキストメッセージを発信できるようになり、該当するルーム内の全てのキャスターおよび視聴者が`onRecvRoomTextMsg`のコールバックを受信することができます。
 IMバックエンドは、デフォルトのNGワードフィルター規則を有し、NGワードと認識されたテキストメッセージはクラウドに転送されることはありません。
```java
// 発信側：テキストメッセージの発信
trtcMeeting.sendRoomTextMsg("Hello Word!", null);
// 受信側：テキストメッセージのモニタ
trtcMeeting.setDelegate(new TRTCMeetingDelegate() {
    @Override
    public void onRecvRoomTextMsg(
		    String message, TRTCMeetingDef.UserInfo userInfo) {
        Log.d(TAG,"が" + userInfo.userName + "から受信した情報:" + message);
    }
});
```
- `sendRoomCustomMsg`によってカスタマイズ（シグナリング）情報を発信することができます。そのルーム内の全てのキャスターおよび視聴者は`onRecvRoomCustomMsg`のコールバックを受信することができます。
カスタマイズメッセージは、通常カスタマイズしたシグナリングの転送に使用します（例：禁止ワードの会場内規制など）。
```java
// 送信側：カスタマイズした Cmdで禁止ワードの通知を区別できます。
// eg:"CMD_MUTE_AUDIO"は禁止ワードの通知を表します。
trtcMeeting.sendRoomCustomMsg("CMD_MUTE_AUDIO", "1", null);
// 受信側：カスタマイズメッセージのモニタ
trtcMeeting.setDelegate(new TRTCMeetingDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, 
		    String message, TRTCMeetingDef.UserInfo userInfo) {
        if ("CMD_MUTE_AUDIO".equals(cmd)) {
            // 禁止ワードの通知を受信します。
            Log.d(TAG,"が" + userInfo.userName + "から受信した禁止ワードの通知:" + message );
            trtcMeeting.muteLocalAudio("1".equals(message));
        }
    }
});
```
