## ユースケース
TRTCは、4種類の異なる入室モードをサポートしています。このうち、ビデオ通話（VideoCall）および音声通話（VoiceCall）を総称して[通話モード](https://intl.cloud.tencent.com/document/product/647/35103)といい、ビデオ・インタラクティブストリーミング（Live）およびボイス・インタラクティブストリーミング（VoiceChatRoom）を総称してライブストリーミングモードといいます。
ライブストリーミングモードでのTRTCは、1つのルームで最大10万人の同時接続をサポートし、300ms未満のマイク接続遅延、1000ms未満の視聴遅延およびマイクのオン・オフのスムーズな切り替え技術を備えています。低レイテンシーインタラクティブストリーム、10万人のインタラクティブ教室、ビデオ婚活、eラーニング、リモート研修、超大規模ミーティングなどのユースケースに適しています。

## 原理解析
TRTCクラウドサービスは、「インターフェースモジュール」および「プロキシモジュール」という2種類の異なるタイプのサーバーノードから構成されています。
-   **インターフェースモジュール**
この種のノードは、最も良質の回線および高性能の機器を採用しており、エンドツーエンドの低遅延マイク接続通話の処理に優れています。
-   **プロキシモジュール**
この種のノードは、通常の回線および性能も一般的な機器を採用しており、同時進行性の高いプルストリーミング再生ニーズの処理にすぐれています。

ライブストリーミングモードでは、TRTCはロールのコンセプトを導入し、ユーザーは「キャスター」および「視聴者」の2種類のロールに分けられ、「キャスター」はインターフェースモジュールに配分され、「視聴者」はプロキシモジュールに分配されます。同一ルームの視聴者の上限は10万人です。
「視聴者」をマイク・オンにしたい場合、まずロール（switchRole）を「キャスター」に切り替えると発言できます。ロールを切り替えることで、ユーザーをプロキシモジュールからインターフェースモジュールに移動させ、TRTC特有の低遅延視聴技術およびスムーズなマイクのオン/オフ切替技術によって、すべての切り替え時間を非常に短くすることができます。
![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## サンプルコード
[Github](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTC-API-Example) にログインし、本ファイルに関連するサンプルコードを取得することができます。
![](https://main.qcloudimg.com/raw/959efe00790a0a2952f8837a48baec25.png)

>?Githubへのアクセスが遅い場合は、 [TXLiteAVSDK_TRTC_Android_latest.zip](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip)を直接ダウンロードすることもできます。

## 操作手順
[](id:step1)
### 手順1：SDKの統合 
以下の方式を選択して **TRTC SDK** をプロジェクトに統合することができます。
#### 方法1：自動ロード（aar）
TRTC SDKは、jcenterライブラリにリリースされています。更新を自動的にダウンロードするようにgradleを構成することで自動でダウンロード、更新できます。
Android Studioを使用して、SDKを統合予定のプロジェクト（TRTC-API-Exampleは統合が完了済み、サンプルコードは参照用として提供）を開き、その後簡単な手順で`app/build.gradle`ファイルを修正するだけで、SDKの統合を完了できます。

1. dependenciesの中にTRTCSDKの依存を追加します。
```
dependencies {
      compile 'com.tencent.liteav:LiteAVSDK_TRTC:latest.release'
}
```
2. defaultConfigでAppが使用するCPUアーキテクチャを指定します。
>?現在 TRTC SDKは、armeabi、armeabi-v7a、arm64-v8aをサポートしています。
>
```
 defaultConfig {
      ndk {
          abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
      }
  }
```
3. **Sync Now**をクリックし、SDKを同期します。
 jcenterへのネットワーク接続に問題がない場合、SDKは自動的にダウンロードされ、プロジェクトに統合されます。

#### 方法2：ZIPパッケージをダウンロードして手動で統合
[ZIP圧縮パッケージ](https://intl.cloud.tencent.com/document/product/647/34615)を直接ダウンロードして、 [クイックインテグレーション(Android)](https://intl.cloud.tencent.com/document/product/647/35093)を参照してSDKをプロジェクトに統合することができます。


[](id:step2)
### 手順2： App権限の設定
`AndroidManifest.xml`ファイルにカメラ、マイクおよびネットワークのアクセス許可のリクエストを追加します。

```
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />

<uses-feature android:name="android.hardware.camera" />
<uses-feature android:name="android.hardware.camera.autofocus" />
```


[](id:step3)
### 手順3：SDKインスタンスを初期化し、イベントコールバックを監視する

1. [sharedInstance()](https://intl.cloud.tencent.com/document/product/647/35125) インターフェースを使用して`TRTCCloud`インスタンスを作成します。
 ```java
// trtcCloudインスタンスを作成
mTRTCCloud = TRTCCloud.sharedInstance(getApplicationContext());
mTRTCCloud.setListener(new TRTCCloudListener());
 ```
2. `setListener`属性を設定しイベントのコールバックを登録し、関連イベントおよびエラー通知をモニタします。
```java
// エラー通知のモニタ。エラー通知は、 SDK が動作を継続できないことを示します
@Override
public void onError(int errCode, String errMsg, Bundle extraInfo) {
    Log.d(TAG, "sdk callback onError");
    if (activity != null) {
        Toast.makeText(activity, "onError: " + errMsg + "[" + errCode+ "]" , Toast.LENGTH_SHORT).show();
        if (errCode == TXLiteAVCode.ERR_ROOM_ENTER_FAIL) {
            activity.exitRoom();
        }
    }
}
```

[](id:step4)
### 手順4：入室パラメータTRTCParamsを組み立てる
[enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c)インターフェースを呼び出すとき、キーパラメータ[TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a674b3c744a0522802d68dfd208763b59)を入力する必要があります。このパラメータに含まれる入力必須のフィールドは下表に示すとおりです。

| パラメータ名 | フィールドタイプ | 補足説明 |記入例 |
|---------|---------|---------|---------|
| sdkAppId | 数字 | アプリケーションID。<a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a>でSDKAppIDを表示できます。|1400000123 |
| userId | 文字列 | アルファベットの大文字、小文字（a-z、A-Z）、数字（0-9）、下線およびハイフンのみを許可。ビジネスの実際のアカウントシステムを組み合わせて設定することをお勧めします。 |test_user_001 |
| userSig | 文字列 | userIdを基にuserSigは計算されます。計算方法は[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166) をご参照ください。| eJyrVareCeYrSy1SslI... |
| roomId   | 数字   | 数字タイプのルームナンバー。文字列形式のルームナンバーを使用したい場合は、TRTCParamsのstrRoomIdをご使用ください。 | 29834  |

>!
>- TRTCは、2つの同じuserIdによる同時入室をサポートしていません。同時に入室した場合、相互に干渉します。
>- 各端末のユースケースappSceneについては、統一する必要があります。統一していない場合、想定外のトラブルが生じる恐れがあります。

[](id:step5)
### 手順5：キャスター端末でのカメラのプレビューとマイク集音を起動する
1. キャスター側は、[startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116)を呼び出すと、ローカルのカメラのプレビューを起動することができ、SDKがシステムにカメラの使用許可をリクエストします。
2. キャスター側は、[setLocalViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#af36ab721c670e5871e5b21a41518b51d)を呼び出すと、ローカルのビデオ画面の表示モードを設定することができます。
 - Fillモードは塗りつぶしを意味し、画面は同じ比率で拡大およびトリミングできますが、黒い縁取りは付きません。
 - Fitモードは適応を意味し、画面は同じ比率で縮小してスクリーンにフィットしてそのコンテンツを完全に表示しますが、黒い縁取りが付くことがあります。
3. キャスター側は、[setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ae047d96922cb1c19135433fa7908e6ce)インターフェースを呼び出すと、ローカルビデオのエンコードパラメータを設定できます。このパラメータにより、ルーム内の他のユーザーが視聴する際の画面の[画質](https://intl.cloud.tencent.com/document/product/647/35153)が決定されます。
4. キャスター側は、[startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a9428ef48d67e19ba91272c9cf967e35e)を呼び出すと、マイクを起動でき、SDKがシステムにマイクの使用許可をリクエストします。

```java
//サンプルコード：ローカルのオーディオ・ビデオストリーミングの公開
mTRTCCloud.setLocalViewFillMode(TRTC_VIDEO_RENDER_MODE_FIT);
mTRTCCloud.startLocalPreview(mIsFrontCamera, localView);
//ローカルビデオコーデックパラメータの設定
TRTCCloudDef.TRTCVideoEncParam encParam = new TRTCCloudDef.TRTCVideoEncParam();
encParam.videoResolution = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_960_540;
encParam.videoFps = 15;
encParam.videoBitrate = 1200;
encParam.videoResolutionMode = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT;
mTRTCCloud.setVideoEncoderParam(encParam);
mTRTCCloud.startLocalAudio();
```

[](id:step6)
### 手順6：キャスター端末により美顔エフェクトを設定する

1. キャスター側は、[getBeautyManager()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3fdfeb3204581c27bbf1c8b5598714fb)を呼び出すと、美顔設定インターフェース[TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager)を取得できます。
2. キャスター側は、[setBeautyStyle()](https://liteav.sdk.qcloud.com/doc/api/zh-cngroup__TRTCCloud__android.html#a46ffe2b60f916a87345fb357110adf10)を呼び出すと、美顔スタイルを設定できます。
 - Smooth：スムース。明らかな効果が感じられます。インフルエンサーのスタイルに近づけます。
 - Nature：ナチュラル。美肌補正のアルゴリズムは顔の詳細な質感を維持し、より自然な感じになります。
 - Pitu ：[エンタープライズ版](https://intl.cloud.tencent.com/document/product/647/34615#Enterprise) のみサポートしています。
3. キャスター側は、[setBeautyLevel()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#a3931ccd8fa54bb846783ab4d6ca2874b)を呼び出すと、美肌補正レベルを設定できます。通常、5の設定でOKです。
4. キャスター側は、[setWhitenessLevel()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#ab08c07ce725dbb8769b61fe0c76b0e95)を呼び出すと、美白レベルを設定できます。通常、5の設定でOKです。


[](id:step7)
### 手順7：キャスター端末からルームを新規作成し、プッシュを開始する
1. キャスター側は、[TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a674b3c744a0522802d68dfd208763b59)のフィールド`role`を**`TRTCCloudDef.TRTCRoleAnchor`**に設定します。これは現在のユーザーのロールがキャスターであることを表します。
2. キャスター側は、[enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c)を呼び出すと、TRTCParamsパラメータのフィールド`roomId`の値をルームナンバーとするオーディオ・ビデオルームを作成し、**`appScene`**パラメータを指定することができます。
 - TRTCCloudDef.TRTC_APP_SCENE_LIVE：ビデオ・インタラクティブストリーミングモード。ここではこのモードを例にします。
 - TRTCCloudDef.TRTC_APP_SCENE_VOICE_CHATROOM：ボイス・インタラクティブストリーミングモード。
3. ルームの新規作成が成功すると、キャスター側は、音声ビデオデータのエンコードおよび伝送フローを開始します。同時にSDKが[onEnterRoom(result)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#abf0525c3433cbd923fd1f13b42c416a2)イベントをコールバックします。パラメータ`result`が0より大きいときは入室成功を表し、具体的な数値は入室のために消費した時間になります。単位はミリ秒（ms）です。`result`が0より小さい時は入室失敗を表し、具体的な数値は入室失敗のエラーコードになります。

```java
public void enterRoom() {
    TRTCCloudDef.TRTCParams trtcParams = new TRTCCloudDef.TRTCParams();
    trtcParams.sdkAppId = sdkappid;
    trtcParams.userId = userid;
    trtcParams.roomId = 908;
    trtcParams.userSig = usersig;
    mTRTCCloud.enterRoom(trtcParams, TRTCCloudDef.TRTC_APP_SCENE_LIVE);
}

@Override
public void onEnterRoom(long result) {
    if (result > 0) {
        toastTip("入室成功，総消費時間[∖(result)]ms")
    }else{
        toastTip("入室失敗，エラーコード[∖(result)]")
    }
}
```

[](id:step8)
### 手順8：視聴者が入室しライブストリーミングを視聴する
1. 視聴者側は、[TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a674b3c744a0522802d68dfd208763b59)のフィールド`role`を**`TRTCCloudDef.TRTCRoleAudience`**に設定します。これは現在のユーザーのロールが視聴者であることを表します。
2. 視聴者側は、[enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c)を呼び出すと、TRTCParamsパラメータの`roomId`が示すオーディオ・ビデオルームに入室し、**`appScene`**パラメータを指定することができます。
 - TRTCCloudDef.TRTC_APP_SCENE_LIVE：ビデオ・インタラクティブストリーミングモード。ここではこのモードを例にします。
 - TRTCCloudDef.TRTC_APP_SCENE_VOICE_CHATROOM：ボイス・インタラクティブストリーミングモード。
3. キャスター画面の視聴：
 - 視聴者側が事前にキャスターのuserIdを知っている場合は、入室に成功した後、直接キャスターの`userId`を使用して[startRemoteView(userId, view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c)を呼び出せば、キャスターの画面を表示することができます。
 - 視聴者側がキャスターのuserIdを知らない場合、視聴者側が、入室に成功すると、[onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05)イベント通知を受信しますので、コールバックにより受け取ったキャスター`userId`を使用して[startRemoteView(userId, view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c)を呼び出せば、キャスターの画面を表示することができます。

[](id:step9)
### 手順9：視聴者とキャスターとのマイク接続
1. 視聴者側が[switchRole(TRTCCloudDef.TRTCRoleAnchor)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a915a4b3abca0e41f057022a4587faf66)を呼び出し、ロールをキャスター（TRTCCloudDef.TRTCRoleAnchor）に切り替えます。
2. 視聴者側が[startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116)を呼び出すと、ローカルの画面をアクティブにすることができます。
3. 視聴者側が[startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a9428ef48d67e19ba91272c9cf967e35e)を呼び出すと、マイクの集音が開始されます。

```java
//サンプルコード：視聴者マイク・オン
mTrtcCloud.switchRole(TRTCCloudDef.TRTCRoleAnchor);
mTrtcCloud.startLocalAudio();
mTrtcCloud.startLocalPreview(mIsFrontCamera, localView);

//サンプルコード：視聴者マイク・オフ
mTrtcCloud.switchRole(TRTCCloudDef.TRTCRoleAudience);
mTrtcCloud.stopLocalAudio();
mTrtcCloud.stopLocalPreview();
```


[](id:step10)
### 手順10：キャスター間でルーム間マイク接続PKを行う

TRTCでは、異なるオーディオ・ビデオルームにいる2人のキャスターが当初のライブストリーミングルームを退出しない場合にも、「ルーム間通話」機能によってマイク接続通話機能をプルし、「ルーム間マイク接続PK」を行うことができます。

1. キャスターAが、[connectOtherRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ac1ab7e4a017b99bb91d89ce1b0fac5fd)インターフェースを呼び出します。インターフェースパラメータは現在JSON形式を採用しており、キャスターBの`roomId`と`userId`を接合して`{"roomId": "978","userId": "userB"}`の形式にしたパラメータをインターフェース関数に渡す必要があります。
2. クロスルームに成功すると、キャスターAは[onConnectOtherRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac9fd524ab9de446f4aaf502f80859e95)のイベントコールバックを受け取ります。同時に、2つのライブストリーミングルームのすべてのユーザーが[onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05)と[onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f)のイベント通知を受け取ります。
 例えば、ルーム「001」のキャスターAがルーム「002」のキャスターBと`connectOtherRoom()`を介してルーム間通話をする場合、ルーム「001」のユーザーはキャスターBの`onUserVideoAvailable(B, true)`コールバックと`onUserAudioAvailable(B, true)`コールバックを受信します。ルーム「002」のユーザーはキャスターAの`onUserVideoAvailable(A, true)`コールバックと`onUserAudioAvailable(A, true)`コールバックを受信します。
3. 2つのルームにいるユーザーは、[startRemoteView(userId, view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c)を呼び出すことで、もう一方のルームのキャスターの画面を表示することができ、音声が自動的に再生されます。

```java
//サンプルコード：ルーム間マイク接続PK
mTRTCCloud.ConnectOtherRoom(String.format("{\"roomId\":%s,\"userId\":\"%s\"}", roomId, username));
```

[](id:step11)
### 手順11：現在のルームから退出する

[exitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a41d16a97a9cb8f16ef92f5ef5bfebee1)メソッドを呼び出してルームを退出します。SDKは退室する時に、カメラ、マイクなどのハードウェアデバイスを停止してリリースする必要があるため、退室の動作は瞬時に完了するものではなく、[onExitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ad5ac26478033ea9c0339462c69f9c89e)のコールバックを受信してはじめて、実際に退室操作を完了したことになります。

```java
// 退室を呼び出した後は、onExitRoomイベントのコールバックをお待ちください
mTRTCCloud.exitRoom()

@Override
public void onExitRoom(int reason) {
    Log.i(TAG, "onExitRoom: reason = " + reason);
}
```

>! Appの中で多くの音声ビデオのSDKを同時に統合した場合は、`onExitRoom`コールバックを受信してからその他の音声ビデオSDKを起動してください。そうしない場合は、ハード上の占有問題が生じることがあります。

