## デモンストレーション
当社のAppを[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)してインストールし、多人数オーディオビデオ通話の効果をご体験いただけます。これには、画面共有、美顔、低遅延ビデオ通話など、TRTCの多人数オーディオビデオシーン関連の機能が含まれています。




## ソリューションの優位性
- 超低遅延のオーディオビデオ通話、画面共有、美顔などの機能を統合し、多人数オーディオビデオルームの一般的な機能をカバーします。
- 二次開発の需要に応じて、カスタムUIやレイアウトを迅速に実装し、ビジネスの迅速な立ち上げに役立ちます。
- TRTCとIMの基本SDKをカプセル化し、基本的なロジックコントロールを実装し、呼び出しを容易にするインターフェースを提供します。

## アクセスガイド
多人数オーディオビデオルームの機能に素早くアクセスしたい場合は、当社が提供するAppを直接修正して適応させるか、App内のModuleを使用してカスタマイズしたUIを実装することができます。

[](id:step1_1)
### 手順1：アプリケーションの新規作成
1. TRTCコンソールにログインし、**開発支援** > [**Demoクイックスタート**](https://console.cloud.tencent.com/trtc/quickstart)を選択します。
2. `TestTUIRoom`などのアプリケーション名を入力して、**作成**をクリックします。
3. **ダウンロードしました。次のステップ**をクリックすると、この手順をスキップします。

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>!本機能はTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/10479)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期してアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。

[](id:step1_2)
### 手順2：Appソースコードのダウンロード
クリックして[TUIRoom](https://github.com/tencentyun/TUIRoom)に進み、ソースコードをCloneまたはダウンロードします。

[](id:step1_3)
### 手順3：Appプロジェクトファイルの設定
1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java`のファイルを見つけて開きます。
3. `GenerateTestUserSig.java`ファイル内の関連パラメータを設定します。
<ul style="margin:0"><li/>SDKAPPID：デフォルトはプレースホルダー(PLACEHOLDER)。実際のSDKAppIDを設定してください。
<li/>SECRETKEY：デフォルトはプレースホルダー(PLACEHOLDER)。実際のキー情報を設定してください。</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. 貼り付け完了後、**貼り付けました。次のステップ**をクリックすれば、作成が完了します。
5. コンパイル完了後、 **コンソール概要に戻る** をクリックすれば終了です。

>? 
>- ここで言及するUserSigの発行方法は、クライアントコードの中でのSECRETKEY設定となりますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者がお客様のTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのAppクイックスタートおよび機能デバッグにのみ適しています**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[UserSigに関するご質問](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:step1_4)
### 手順4：Appの実行
Android Studio（バージョン3.5以上）を使用してソースコード`TUIRoom`プロジェクトを開き、**実行**をクリックすれば、このAppのデバッグが開始されます。

[](id:step1_5)
### 手順5：プロジェクトソースコードの修正
ソースコードの`Source`フォルダには、uiとmodelの2つのサブフォルダが含まれ、uiフォルダの中はいずれもインターフェースコードです。以下の表にはファイルまたはフォルダおよび対応するUIをリストアップし、二次調整に役立つようにしています。

| ファイルまたはフォルダ | 機能説明 |
|:-------:|:--------|
| remote | リモートユーザーのリストのインターフェース |
| widget | 一般的なUIコンポーネント |
| CreateRoomActivity.java | オーディオビデオルーム作成のインターフェース |
| RoomMainActivity.java | オーディオビデオルームのメインインターフェース |
| RoomVideoView.java | TRTCのTXCloudVideoViewをパッケージ化し、自分とリモートユーザーのビデオデータの表示に利用します |
| MemberEntity.java | UI層のユーザーデータ |
| MemberListAdapter.java | オーディオビデオルームのメインインターフェースのAdapter |

## 体験アプリケーション
>! 体験アプリケーションには、少なくとも2台のデバイスが必要です。
### エントリーインターフェース
図のように、「ルームの作成」または「ルームへの参加」を選択してください。


### ルーム作成ページ
ユーザーAが作成し、ルームナンバーはデフォルトで発行されます。**ルーム作成**をクリックすると、メインページに進むことができます。


### ルーム参加ページ
ユーザーBはユーザーAのルームナンバーを入力し、**ルームへの参加**をクリックすると、メインページに進むことができます。


### メインページ（ユーザーA）
<img src="https://qcloudimg.tencent-cloud.cn/raw/eebab2b82db719000f0dc376070a25e7.png" width=300px>

### 配信側リスト
配信側リストには現在のルームのメンバーを表示できます。相手がカメラとマイクを起動すると、相手の画面を見ること、相手の声を聞くことができます。

### 上部のコントロールバー
イヤホン/マイク切り替え、フロント/リアカメラ切り替え、ルーム情報、退出の機能を実装しました。

### 下部のツールバー
自身のマイク/カメラの制御、美顔、メンバーリスト、設定などの機能を実装しました。

### 美顔
ライブストリーミング中に画面に対し美顔およびエフェクト表示を行うことができます。


### 設定ウィンドウ
オーディオビデオ関連パラメータを設定でき、**画面共有**の開始をサポートします。


### 退室
- **キャスター**：ルームを解散し、全員を退室させます。
- **キャスター以外**：自ら退室します。

## UIカスタマイズの実装

[ソースコード](https://github.com/tencentyun/TUIRoom)の`Source`フォルダには、uiとmodelという2つのサブフォルダがあり、modelフォルダには再利用できるオープンソースコンポーネントTUIRoomCoreが含まれています。`TUIRoomCore.java`ファイルでこのコンポーネントが提供するインターフェース関数を確認し、対応するインターフェースを使用してカスタマイズしたUIを実装することができます。
![#600px](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)

[](id:step2_1)
### 手順1：SDKの統合 
多人数オーディオビデオルームのコンポーネントTUIRoomCoreは、TRTC SDKとIM SDKに依存しています。次の手順で2つのSDKをプロジェクトに統合することができます。

- **方法1：Mavenリポジトリを介する依存**
	1. dependenciesにTRTCSDKとIMSDKの依存を追加します。
```java
dependencies {
	 compile "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
	 compile 'com.tencent.imsdk:imsdk:latest.release'
}
```
>?2つのSDKの最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK) および[IM](https://github.com/tencentyun/TIMSDK) のGithubトップページで取得することができます。

	2. defaultConfigでAppが使用するCPUアーキテクチャを指定します。
```java
defaultConfig {
	ndk {
			abiFilters "armeabi-v7a"
	}
}
```
	3. **Sync Now**をクリックし、自動でSDKをダウンロードし、プロジェクトに統合します。
- **方法2：ローカルAARを介する依存**
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

[](id:step2_2)
### 手順2：権限の設定および難読化ルール
1. `AndroidManifest.xml`にAppの権限を設定します。SDKには次の権限が必要です（6.0以上のAndroidシステムではカメラ、ストレージ読み取りの権限を動的に申請する必要があります）。
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
2. proguard-rules.proファイルでは、SDK関連クラスを非難読化リストに追加します。
```java
-keep class com.tencent.** { *; }
```

[](id:step2_3)
### ステップ3：TUIRoomCoreコンポーネントのインポート
次のディレクトリ内のすべてのファイルをプロジェクトにコピーします。
```java
src/main/java/com/tencent/liteav/tuiroom/model
```

[](id:step2_4)
### 手順4：コンポーネントの作成およびログイン
TUICoreのTUILoginを呼び出してログインします。次の例をご参照ください。
```java
TUILogin.init(this, "sdkAppid", null, new V2TIMSDKListener() {

		@Override
		public void onKickedOffline() {

		}

		@Override
		public void onUserSigExpired() {

		}
	});
TUILogin.login("userId", "userSig", new V2TIMCallback() {
	@Override
	public void onError(int code, String msg) {

	}

	@Override
	public void onSuccess() {

	}
});
```

[](id:step2_5)
### ステップ5：ニックネームの設定
正常にログインした後、setSelfProfileを呼び出し、ユーザー情報を設定します。

[](id:step2_6)

### ステップ6：ルームの作成
1. メンバーがcreateRoomインターフェースを呼び出し、新たなルームを作成します。ルームの作成後、キャスターとしてチャットルームとTRTCルームを含むルームに入室します。
```java
TUIRoomCore tuiRoomCore = TUIRoomCore.getInstance(context);
tuiCore.setListener(listener);
tuiCore.createRoom("roomId", TUIRoomCoreDef.SpeechMode.FREE_SPEECH,
        new TUIRoomCoreCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
            // ルーム作成の成功
            }else{
		}
	}
});

```
2. startCameraPreviewインターフェースを呼び出し 、ローカルビデオのキャプチャと表示を開始します。
![](https://qcloudimg.tencent-cloud.cn/raw/8c3391905188089fecd17e23477d34ea.png)

[](id:step2_7)
### ステップ7：ルームの解散
- キャスターがdestoryRoomインターフェースを呼び出し 、ルームを解散します。IMグループチャットを解散して、TRTCルームを退室します。
- メンバー側は、グループを解散し、TRTCルームを退室するよう通知するonDestroyRoomコールバックメッセージを受信します。

[](id:step2_8)
### ステップ8：ルームへの参加
1. ルーム参加手順は、作成手順と基本的に同じです。メンバーはenterRoomインターフェースを呼び出して入室する必要があります。
2. その他のメンバーは、メンバーの入室があったことを通知するonRemoteUserEnterコールバックを受信します。
```java
TUIRoomCore tuiRoomCore = TUIRoomCore.getInstance(context);
tuiCore.setListener(listener);
tuiCore.enterRoom("roomId", new TUIRoomCoreCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
            // 入室に成功
            }else{
		}
	}
});
```
![](https://qcloudimg.tencent-cloud.cn/raw/ffbda4de381ea198bf808de7d823ab59.png)

[](id:step2_9)
### ステップ9：退室
1. メンバーがleaveRoomインターフェースを呼び出し、IMルームとTRTCルームを退室します。
2. その他メンバーグループ側は、メンバーが退室したことを通知するonRemoteUserLeaveコールバックを受信します。

[](id:step2_10)
### 手順10：画面共有

1. 画面共有機能は、システムにフローティングウィンドウの権限を申請する必要があり、自分でUIの中で特定のロジックを実装する必要があります。
2. TUIRoomCoreの`startScreenCapture`を呼び出して共有を行います。エンコードパラメータとスクリーンキャプチャのプロセスのフローティングウィンドウを渡すと、画面共有機能を実装できます。具体的な情報については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58)をご参照ください。
3. ルーム内のその他メンバーはonRemoteUserScreenVideoAvailableのイベント通知を受信します。

>! 画面共有とカメラキャプチャは相互排他的な操作です。画面共有機能をアクティブにしたい場合は、先にstopCameraPreviewを呼び出してカメラキャプチャを停止してください。

<dx-codeblock>
::: java java
// 1.AndroidManifest.xmlのファイルの中にSDKのスクリーンレコーディング機能のactivityと権限を追加します
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
:::
</dx-codeblock>
