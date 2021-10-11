## デモンストレーション
当社のAppを[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)してインストールし、多人数ビデオミーティングの効果を体験いただけます。これには、画面共有、美顔、低遅延ミーティングなど、TRTCの多人数ビデオミーティングシナリオ関連の機能が含まれています。


多人数ビデオミーティングの機能にすばやくアクセスしたい場合は、当社が提供するAppをもとに直接アダプタを直接修正するか、当社が提供するTRTCMeetingのコンポーネントを使用してカスタマイズしたUIを実装することができます。

[](id:DemoUI)
## AppのUIの再利用
[](id:ui.step1)

### 手順1：アプリケーションの新規作成
1. TRTCコンソールにログインし、【開発支援】>【[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. アプリケーション名（例：`TestMeetingRoom`）を入力し、【作成】をクリックします。
3. 【ダウンロードしました。次のステップ】をクリックすると、この手順をスキップします。

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)
>!  本機能はTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://cloud.tencent.com/document/product/269)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。

[](id:ui.step2)
### 手順2：Appソースコードのダウンロード
[TUIMeeting](https://github.com/tencentyun/TUIMeeting)をクリックして当該ページに入り、ソースコードをCloneまたはダウンロードします。

[](id:ui.step3)
### 手順3：Appファイルの設定
1. 設定変更ページに進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java`のファイルを見つけて開きます。
3. `GenerateTestUserSig.java`ファイル内の関連パラメータを設定します。
<ul style="margin:0"><li/>SDKAPPID：デフォルトはプレースホルダー(PLACEHOLDER)。実際のSDKAppIDを設定してください。
<li/>SECRETKEY：デフォルトはプレースホルダー(PLACEHOLDER)。実際のキー情報を設定してください。</ul>
4. 貼り付け完了後、【貼り付けました。次のステップ】をクリックすれば、作成が完了します。
5. コンパイル完了後、【コンソール概要に戻る】をクリックすればOKです。


>!
>- ここで言及するUserSigの発行方法は、クライアントコードの中でのSECRETKEY設定となりますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者がお客様のTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのAppクイックスタートおよび機能デバッグにのみ適しています**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを送信し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:ui.step4)
### 手順4：Appの実行
Android Studio（バージョン3.5以降）を使用してソースコード`TUIMeeting`プロジェクトを開き、【実行】をクリックすれば、このAppのデバッグが開始されます。

[](id:ui.step5)
### 手順5：Appソースコードの修正
ソースコードの`Source`フォルダには、uiとmodelの2つのサブフォルダが含まれ、uiフォルダの中はいずれもインターフェースコードです。以下の表にはファイルまたはフォルダおよび対応するUIをリストアップし、二次調整に役立つようにしています。

| ファイルまたはフォルダ | 機能の説明 |
|:-------:|:--------|
| remote | リモートユーザーのリストのインターフェース |
| widget | 一般的なUIコンポーネント |
| CreateMeetingActivity.java | ミーティング作成のインターフェース |
| MeetingMainActivity.java | ビデオミーティングのメインインターフェース |
| MeetingVideoView.java | TRTCのTXCloudVideoViewをパッケージ化し、自分とリモートユーザーのビデオデータの表示に利用します。 |
| MemberEntity.java | UI層のユーザーデータ |
| MemberListAdapter.java | ビデオミーティングのメインインターフェースのAdapter |



## アプリケーション体験

> ! アプリケーション体験には、少なくとも2台のデバイスが必要です。

### ユーザーA
1. 図のように、ユーザー名を入力し（**ユーザー名は一意のものとし、他のユーザーと重複しないようにしてください**）、ログインします。
2. コードを入力し、【ミーティングに参加】をクリックします（下図のとおり）。
3. ルームトピックを入力し、【チャット開始】をクリックします。

### ユーザーB
1. 図のように、ユーザー名を入力し（**ユーザー名は一意のものとし、他のユーザーと重複しないようにしてください**）、ログインします。
2. ユーザーAが作成したコードを入力し、【ミーティングに参加】をクリックします。<br>

[](id:model)
## カスタムUIの実装

[ソースコード(https://github.com/tencentyun/TUIMeeting/tree/master/Android/Source/src/main/java/com/tencent/liteav/meeting)のSourceフォルダには、uiとmodelという2つのサブフォルダがあり、modelフォルダには再利用可能なオープンソースコンポーネントTRTCMeetingが含まれています。`TRTCMeeting.java`ファイルの中からこのコンポーネントが提供するインターフェース関数を見つけ、対応するインターフェースを使用してカスマイズUIを実装することが可能です。
![](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)

[](id:model.step1)
### 手順1：SDKへの統合
多人数ビデオミーティングのコンポーネントTRTCMeetingは、TRTC SDKとIM SDKに依存し、次の手順で2つのSDKをプロジェクトに統合することができます。

**方法1：Mavenリポジトリを介する依存**
1. dependenciesにTRTCSDKとIMSDKの依存を追加します。
<dx-codeblock>
::: java java
dependencies {
       compile "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
       compile 'com.tencent.imsdk:imsdk:latest.release'
}
:::
</dx-codeblock>
>?2つのSDKの最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK)および[IM](https://github.com/tencentyun/TIMSDK)のGithubトップページで取得することができます。
2. defaultConfigでAppが使用するCPUアーキテクチャを指定します。
<dx-codeblock>
::: java java
defaultConfig {
      ndk {
          abiFilters "armeabi-v7a"
      }
}
:::
</dx-codeblock>
3. 【Sync Now】をクリックし、自動でSDKをダウンロードし、プロジェクトに統合します。

**方法2：ローカルAARを介する依存**
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

[](id:model.step2)
### 手順2：権限の設定および難読化ルール
AndroidManifest.xmlにAppの権限を設定します。SDKには次の権限が必要です（6.0以上のAndroidシステムではカメラ、ストレージ読み取りの権限を動的に申請する必要があります）。
<dx-codeblock>
::: java java
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
:::
</dx-codeblock>

proguard-rules.proファイルでは、SDK関連を非難読化リストに追加します。
<dx-codeblock>
::: java java
-keep class com.tencent.** { *; }
:::
</dx-codeblock>

[](id:model.step3)
### 手順3：TRTCMeetingコンポーネントのインポート
次のディレクトリ内のすべてのファイルをプロジェクトにコピーします。
<dx-codeblock>
::: java java
src/main/java/com/tencent/liteav/meeting/model
:::
</dx-codeblock>

[](id:model.step4)
### 手順4：コンポーネントの作成およびログイン
1. sharedInstanceインターフェースを呼び出すと、TRTCMeetingコンポーネントのインスタンスオブジェクトを作成できます。
2. setDelegate関数を呼び出し、コンポーネントのイベント通知を登録します。
3. login関数を呼び出し、コンポーネントのログインを完了させます。下表を参照してキーパラメータを入力してください。
<table>
<tr><th>パラメータ名</th><th>機能</th></tr><tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a> で SDKAppIDを表示できます。</td>
</tr><tr>
<td>userId</td>
<td>現在のユーザーID、文字列タイプでは、英語のアルファベット（a-z と A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については、<a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSigの計算方法</a>をご参照ください。</td>
</tr><tr>
<td>callback</td>
<td>ログインのコールバック。成功時にcodeは0になります。</td>
</tr>
</table>
<dx-codeblock>
::: java java
TRTCMeeting trtcMeeting = TRTCMeeting.sharedInstance(this);
trtcMeeting.login(SDKAPPID, userId, userSig, new TRTCMeetingCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            //ログイン成功
        }
    }
});
:::
</dx-codeblock>

[](id:model.step5)
### 手順5：多人数ミーティングの新規作成
1. キャスターは、[手順4](#model.step4)でログインした後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. キャスターは、setDelegateの呼び出しで、createMeetingのイベントの呼び出しを実行し、新しいミーティングルームを作成することができます。
3. キャスターは、`startCameraPreview`を呼び出してビデオ画面をキャプチャすることができ、`startMicrophone`を呼び出して音声をキャプチャすることもできます。
4. キャスターに美顔のニーズがある場合は、インターフェース上に美顔調節ボタンを設定して呼び出すことができ、getBeautyManager を介して美顔設定を行います。
>?エンタープライズ版以外のSDKは美顔やスタンプの機能をサポートしていません。

![](https://main.qcloudimg.com/raw/7d55d4983e6fe8da04e63babe5ab3822.png)


<dx-codeblock>
::: java java
// 1.キャスターがニックネームとプロフィール画像を設定します
trtcMeeting.setSelfProfile("my_name", "my_avatar", null);

// 2.キャスターがルームを作成します
trtcMeeting.createMeeting(roomId, new TRTCMeetingCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 3.カメラと音声キャプチャを立ち上げます
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
:::
</dx-codeblock>

[](id:model.step6)
### 手順6：参加者の多人数ミーティングへの参加
1. 参加者は、[手順4](#model.step4)でログインした後、setSelfProfileを呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. 参加者は、enterMeeting呼び出してミーティングルーム番号を渡すと、ミーティングルームに参加できます。
3. 参加者は、startCameraPreviewを呼び出してビデオ画面をキャプチャでき、startMicrophoneを呼び出して音声をキャプチャできます。
4. 他の参加者がカメラを起動すると、onUserVideoAvailableのイベントを受け取ります。この時、startRemoteViewを呼び出してuserIdを渡すと再生を開始できます。

![](https://main.qcloudimg.com/raw/ce4bc9c134a94709c3f8e1768c65be88.png)

<dx-codeblock>
::: java java
// 1.参加者がニックネームとプロフィール画像を設定します
trtcMeeting.setSelfProfile("my_name", "my_avatar", null);

// 2.参加者がenterMeetingを呼び出し、ミーティングルームナンバーに参加します
trtcMeeting.enterMeeting(roomId, new TRTCMeetingCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 3.入室に成功したら、自分のカメラとマイクを起動させます。同時に美顔機能も起動することができます
            TXCloudVideoView txCloudVideoView = new TXCloudVideoView(TestMeetingActivity.this);
            parentView.add(view);
            trtcMeeting.startCameraPreview(true, txCloudVideoView);
            trtcMeeting.startMicrophone();
            trtcMeeting.getBeautyManager().setBeautyStyle(1);
            trtcMeeting.getBeautyManager().setBeautyLevel(6);
        }
    }
});

// 3.参加者が他のメンバーのカメラ起動の通知を受信し、再生が開始されます
trtcMeeting.setDelegate(new TRTCMeetingDelegate() {
    @Override
    public void onUserVideoAvailable(String userId, boolean available) {
        if (available) {
            TXCloudVideoView txCloudVideoView = new TXCloudVideoView(TestMeetingActivity.this);
            parentView.add(view);
            trtcMeeting.startRemoteView(userId, txCloudVideoView);
        } else {
            trtcMeeting.stopRemoteView(userId, null);
        }
    }
});
:::
</dx-codeblock>

[](id:model.step7)
### 手順7：画面共有

1. 画面共有機能は、システムにフローティングウィンドウの権限を申請する必要があり、自分でUIの中で特定のロジックを実装する必要があります。
2. startScreenCaptureを呼び出し、エンコードパラメータとスクリーンキャプチャのプロセスのフローティングウィンドウを渡すと、画面共有機能を実装できます。具体的な情報については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58)をご参照ください。
3. ミーティング中の他メンバーがonUserVideoAvailableのイベント通知を受け取ります。

>! 画面共有とカメラキャプチャは相互排他的な操作です。画面共有機能をアクティブにしたい場合は、先にstopCameraPreviewを呼び出してカメラキャプチャを停止してください。

<dx-codeblock>
::: java java
// 1.AndroidManifest.xmlのファイルの中にSDKのスクリーンキャプチャ機能のactivityと権限を追加します
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<application>
    <activity
        android:name="com.tencent.rtmp.video.TXScreenCapture$TXScreenCaptureAssistantActivity"
        android:theme="@android:style/Theme.Translucent" />
</application>
:::
</dx-codeblock>
<dx-codeblock>
::: java java
// 2.自分のインターフェースの中でフローティングウィンドウの権限を申請します
if (Build.VERSION.SDK_INT >= 23) {
    if (!Settings.canDrawOverlays(getApplicationContext())) {
        Intent intent = new Intent(Settings.ACTION_MANAGE_OVERLAY_PERMISSION, Uri.parse("package:" + getPackageName()));
        startActivityForResult(intent, 100);
    } else {
        startScreenCapture();
    }
} else {
    startScreenCapture();
}

// 3.システムのコールバックの結果
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    if (requestCode == 100) {
        if (Build.VERSION.SDK_INT >= 23) {
            if (Settings.canDrawOverlays(this)) {
                // ユーザーの権限承認が成功
                startScreenCapture();
            } else {
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
:::
</dx-codeblock>

[](id:model.step8)
### 手順8：文字チャットとミュートメッセージの実現
- sendRoomTextMsgにより、ノーマルなテキストメッセージを送信でき、そのルーム内のすべてのキャスターおよび視聴者がonRecvRoomTextMsgのコールバックを受信します。
 IMバックエンドは、デフォルトのセンシティブワードフィルタルールを備えており、センシティブワードと認識されたテキストメッセージはクラウドに転送されることはありません。
 <dx-codeblock>
 ::: java java
 // 送信側：テキストメッセージの送信
 trtcMeeting.sendRoomTextMsg("Hello Word!", null);
 // 受信側：テキストメッセージの監視
 trtcMeeting.setDelegate(new TRTCMeetingDelegate() {
    @Override
    public void onRecvRoomTextMsg(
		    String message, TRTCMeetingDef.UserInfo userInfo) {
        Log.d(TAG, userInfo.userName + "からのメッセージを受信:" + message);
    }
 });
 :::
 </dx-codeblock>
- `sendRoomCustomMsg`によって、カスタム（シグナリング）メッセージを送信できます。当該ルーム内のすべてのキャスターと視聴者が`onRecvRoomCustomMsg` コールバックを受信できます。
カスタムメッセージは、通常カスタマイズしたシグナリングの転送に使用します（例：ミュートの会場内制御など）。
<dx-codeblock>
::: java java
// 送信側：カスタマイズしたCmdでミュートの通知を区別できます
// eg:"CMD_MUTE_AUDIO"はミュートの通知を表します
trtcMeeting.sendRoomCustomMsg("CMD_MUTE_AUDIO", "1", null);
// 受信側：カスタムメッセージの監視
trtcMeeting.setDelegate(new TRTCMeetingDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, 
		    String message, TRTCMeetingDef.UserInfo userInfo) {
        if ("CMD_MUTE_AUDIO".equals(cmd)) {
            // ミュートの通知を受信します
            Log.d(TAG,"が" + userInfo.userName + "からミュート通知を受信しました:" + message );
            trtcMeeting.muteLocalAudio("1".equals(message));
        }
    }
});
:::
</dx-codeblock>
