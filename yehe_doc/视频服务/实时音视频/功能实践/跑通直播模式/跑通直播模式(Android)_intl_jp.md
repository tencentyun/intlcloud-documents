## 適用ケース
TRTC は、4種類の異なる入室モードをサポートしています。このうち、ビデオ通話（VideoCall）および音声通話（VoiceCall）を総称して[通話モード](https://intl.cloud.tencent.com/document/product/647/35103)といい、ビデオ・インタラクティブストリーミング（Live）およびボイス・インタラクティブストリーミング（VoiceChatRoom）を総称してライブストリーミングモードモードといいます。
ライブストリーミングモードでの TRTCは、1つのルームで最大10万人が同時にオンラインでつながるのをサポートし、300ms未満のマイク接続の遅延、1000ms未満の視聴遅延、およびマイクのオン・オフのスムーズな切り替え技術を備えています。低遅延のILVB、10万人のインタラクティブな授業、ビデオ婚活、eラーニング、リモート研修、超大型会議などのユースケースに適用しています。

## 原理解析
TRTC クラウドサービスは、2種類の異なるタイプのサーバーノードから構成されており、それぞれ“インターフェースモジュール”および“プロキシモジュール”からなっています：
- **インターフェースモジュール**
この種のノードは、最も良質の回線および高性能の機器を採用しており、エンドツーエンドの低遅延マイク接続通話の処理に優れますが、単位時間当たりの費用はやや高くなります
- **プロキシモジュール**
この種のノードは、通常の回線および性能も一般的な機器を採用しており、同時進行性の高いプルストリーミング再生のニーズの処理にすぐれ、単位当たりの費用はやや低くなります。

ライブストリーミングモードでは、TRTC はロールのコンセプトを導入し、ユーザーは「キャスター」および「視聴者」の2種類のロールに分けられ、「キャスター」はインターフェースモジュールに配分され、「視聴者」はプロキシモジュールに分配されます。同一ルームの視聴者の上限は10万人です。
「視聴者」をマイク・オンにしたい場合、まずロール（switchRole）を「キャスター」に切り替えると発言できます。ロールを切り替えることで、ユーザーをプロキシモジュールからインターフェースモジュールに移動させ、TRTC 特有の低遅延視聴技術およびスムーズなマイクのオン/オフ切替技術は、すべての切り替え時間を非常に短くすることができます。


## サンプルコード
 [Github]にログインし、本ファイルに関連するサンプルコードを取得することができます。
![](https://main.qcloudimg.com/raw/eedbd4ef8a02bce63f071656faded01a.png)

>?Githubへのアクセスが遅い場合は、 [TXLiteAVSDK_TRTC_Android_latest.zip](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Android_latest.zip)を直接ダウンロードすることもできます。

##　操作手順
<span id="step1"></span>
### 手順1： SDKへの統合
以下の方式を選択して **TRTC SDK** を項目に統合することができます。
#### 方法一：自動ロード（aar）
TRTC SDK は、jcenterライブラリにリリースされています。更新を自動的にダウンロードするようにgradleを構成することで自動でダウンロード、更新できます。
Android Studio を使用して、SDKの統合待ちのプロジェクト（TRTCSimpleDemo は統合が完了済みのため、サンプルコードを参照用として提供できます）を開き、その後簡単な手続きで`app/build.gradle`ファイルを修正すれば、 SDK の統合を完了できます。

1. dependencies に TRTCSDK のリクエストを追加します。
```
dependencies {
      compile 'com.tencent.liteav:LiteAVSDK_TRTC:latest.release'
}
```
2.  defaultConfig で App が使用する CPU アーキテクチャを指定します。
>?現在 TRTC SDK は armeabi ， armeabi-v7a および arm64-v8aをサポートしています。
>
```
 defaultConfig {
      ndk {
          abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
      }
  }
```
3. 【Sync Now】をクリックし、 SDKを同期します。
 jcenterへのネットワーク接続に問題がない場合、SDKは自動的にダウンロードされ、プロジェクトに統合されます。

#### 方法二：ZIP パッケージをダウンロードして手動で統合
[ZIP 圧縮パッケージ](https://intl.cloud.tencent.com/document/product/647/34615)を直接ダウンロードして、 [クイックインテグレーション(Android)](https://intl.cloud.tencent.com/document/product/647/35093) を参照して SDK をプロジェクトに統合することができます。


<span id="step2"></span>
### 手順2： App 権限の設定
`AndroidManifest.xml`ファイルにカメラ、マイクおよびネットワークのアクセス許可のリクエストを追加します。

```
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/ >
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/ >
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH"/>

<uses-feature android:name="android.hardware.camera" />
<uses-feature android:name="android.hardware.camera.autofocus" />
```


<span id="step3"></span>
### 手順3： SDKのインスタンスを初期化してイベントのコールバックをモニタ

1.  [sharedInstance()](https://intl.cloud.tencent.com/document/product/647/35125) インターフェースを使用して`TRTCCloud`インスタンスを作成します。
 ```java
//  trtcCloud インスタンスを作成
mTRTCCloud = TRTCCloud.sharedInstance(getApplicationContext());
mTRTCCloud.setListener(new TRTCCloudListener());
 ```
2. `setListener`属性を設定しイベントのコールバックを登録し、関連 イベントおよびエラー通知をモニタします。
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

<span id="step4"></span>
### 手順4：入室パラメータ TRTCParamsの組み立て
[enterRoom()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) インターフェースをコールするとき、キーパラメータ [TRTCParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#a674b3c744a0522802d68dfd208763b59)を入力する必要があります。このパラメータに含まれる入力必須のフィールドは下表に示すとおりです。

| パラメータ名 | フィールドタイプ | 補足説明 |記入例 |
|---------|---------|---------|---------|
| sdkAppId | 数字 | アプリケーション ID， <a href="https://console.cloud.tencent.com/trtc/app">Tencent Real-Time Communicationコンソール</a> でSDKAppIDを表示できます。|1400000123 |
| userId | 文字列 | アルファベットの大文字、小文字（a-z、A-Z）、数字（0-9）、下線およびハイフンのみを許可。 | test_user_001 |
| userSig | 文字列 |  userId を基に userSigは計算されます。計算方法は [ UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166) をご参照ください。| eJyrVareCeYrSy1SslI... |
| roomId | 数字 | デフォルトでは文字列のタイプのルームナンバーをサポートしていません、文字列タイプのルームナンバーは入室速度に影響します。文字列タイプのルームナンバーをサポートする必要が確実にある場合は、 [チケットを提出](https://console.cloud.tencent.com/workorder/category) してご連絡ください。 | 29834 |

>!TRTC は同時に2つの同じ userIdで入室できません。そうしないと相互に干渉することになります。

<span id = "step5"></span>
### 手順5：キャスター端末でのカメラのプレビューおよびマイク集音の起動
1. キャスター端末が[startLocalPreview()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116) をコールすると、ローカルのカメラのプレビューを起動することができ、SDKはシステムにカメラのアクセス許可をリクエストします。
2. キャスター端末が [setLocalViewFillMode()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#af36ab721c670e5871e5b21a41518b51d) をコールすると、ローカルのビデオ画面の表示モードを設定することができます。
 - Fill モードは塗りつぶしを意味し、画面は同じ比率で拡大およびトリミングできますが、黒い縁取りは付きません。
 - Fit モードは適応を意味し、画面は同じ比率で縮小してスクリーンにフィットしてそのコンテンツを完全に表示しますが、黒い縁取りが付くことがあります。
3. キャスター端末が [setVideoEncoderParam()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ae047d96922cb1c19135433fa7908e6ce) インターフェースをコールすると、ローカルビデオのエンコードパラメータを設定できますが、そのパラメータはルームのその他ユーザーが視聴する画面の [画質](https://intl.cloud.tencent.com/document/product/647/35153)を決定します。
4. キャスター端末が[startLocalAudio()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a9428ef48d67e19ba91272c9cf967e35e) をコールすると、マイクを起動し、SDKはシステムにマイクの使用権限をリクエストします。

```java
//サンプルコード：ローカルのオーディオ・ビデオストリーミングの公開
mTRTCCloud.setLocalViewFillMode(TRTC_VIDEO_RENDER_MODE_FIT);
mTRTCCloud.startLocalPreview(mIsFrontCamera, mLocalView);
//ローカルビデオエンコードパラメータの設定
TRTCCloudDef.TRTCVideoEncParam encParam = new TRTCCloudDef.TRTCVideoEncParam();
encParam.videoResolution = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_960_540;
encParam.videoFps = 15;
encParam.videoBitrate = 1200;
encParam.videoResolutionMode = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT;
trtcCloud.setVideoEncoderParam(encParam);
mTRTCCloud.startLocalAudio();
```

<span id = "step6"></span>
### 手順6：キャスター端末による美顔効果の設定

1. キャスター端末が [getBeautyManager()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a3fdfeb3204581c27bbf1c8b5598714fb) をコールすると、美顔設定インターフェース [TXBeautyManager](http://doc.qcloudtrtc.com/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager)を取得できます。
2. キャスター端末が [setBeautyStyle()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a46ffe2b60f916a87345fb357110adf10) をコールすると、美顔スタイルを設定できます：
 - Smooth：スムース。明らかな効果が感じられます。インフルエンサーのスタイルに近づけます。
 - Nature：ナチュラル。美肌補正のアルゴリズムは顔の詳細な質感を維持し、より自然な感じになります。
 - Pitu ： [企業版](https://intl.cloud.tencent.com/document/product/647/34615#Enterprise) のみサポートしています。
3. キャスター端末が [setBeautyLevel()](http://doc.qcloudtrtc.com/group__TXBeautyManager__android.html#a7f388122cf319218b629fb8e192a2730) をコールすると、顔加工法のレベルを設定します。通常、5の設定でOKです。
4. キャスター端末が [setBeautyLevel()](http://doc.qcloudtrtc.com/group__TXBeautyManager__android.html#aa4e57d02a4605984f4dc6d3508987746) をコールすると、美白レベルを設定します。通常、5の設定でOKです。


<span id = "step7"></span>
### 手順7：キャスター端末によるルーム新規作成およびプッシュの開始
1. キャスター端末が [TRTCParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#a674b3c744a0522802d68dfd208763b59) のフィールド`role`を **`TRTCCloudDef.TRTCRoleAnchor`**に設定し、現在のユーザーのキャラクターをキャスターとして表示します。
2. キャスター端末が [enterRoom()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) をコールすると、 TRTCParams パラメータのフィールド`roomId`の値をルームナンバーとするオーディオ・ビデオルームを作成し、**`appScene`**パラメータを指定します。
 - TRTCCloudDef.TRTC_APP_SCENE_LIVE：ビデオILVBモード。ここではこのモードを例にします。
 - TRTCCloudDef.TRTC_APP_SCENE_VOICE_CHATROOM：音声ILVBモード。
3. ルームの新規作成が成功したら、キャスター端末は音声ビデオデータのデコードおよび伝送フローを開始します。同時にSDK は [onEnterRoom(result)](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#abf0525c3433cbd923fd1f13b42c416a2)  イベントをコールバックします。パラメータ`result`が0より大きいときは入室成功を意味し、具体的な数値は入室してからの消費時間であり、単位はミリ秒（ms）です；`result`が0より小さい時は入室失敗を意味し、具体的な数値は入室失敗のエラーコードになります。

```java
public void enterRoom() {
    TRTCCloudDef.TRTCParams trtcParams = new TRTCCloudDef.TRTCParams();
    trtcParams.sdkAppId = sdkappid;
    trtcParams.userId   = userid;
    trtcParams.roomId = usersig;
    trtcParams.userSig = 908;
    mTRTCCloud.enterRoom(trtcParams, TRTCCloudDef.TRTC_APP_SCENE_LIVE);
}

@Override
public void onEnterRoom(long result) {
    if (result > 0) {
        toastTip("入室成功，総消費時間[╲(result)]ms")
    }else{
        toastTip("入室失敗，エラーコード[╲(result)]")
    }
}
```

<span id = "step8"></span>
### 手順8：視聴者端末が入室しライブストリーミングを視聴
1. 視聴者端末が [TRTCParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#a674b3c744a0522802d68dfd208763b59) のフィールド`role`を **`TRTCCloudDef.TRTCRoleAudience`**に設定し、現在のユーザーのキャラクターを視聴者として表示します。
2. 視聴者端末が [enterRoom()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) をコールすると、 TRTCParams パラメータのフィールド`roomId`が示すオーディオ・ビデオルームに入室し、**`appScene`**パラメータを指定します。
 - TRTCCloudDef.TRTC_APP_SCENE_LIVE：ビデオILVBモード。ここではこのモードを例にします。
 - TRTCCloudDef.TRTC_APP_SCENE_VOICE_CHATROOM：音声ILVBモード。
3. キャスターの画面の視聴：
 - 視聴者端末が事前にキャスターの userIdを知っていて、入室に成功後、直接キャスターの`userId`を使用して [startRemoteView(userId, view)](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) をコールすると、キャスターの画面を表示することができます。
 - 視聴者端末がキャスターの userIdを知らず、視聴者端末が入室に成功後に [onUserVideoAvailable()](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) イベント通知を受信してから、コールバックにより受け取ったキャスター`userId`を使用して [startRemoteView(userId, view)](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) をコールすると、キャスターの画面を表示することができます。

<span id = "step9"></span>
### 手順9：視聴者とキャスターとのマイク接続
1.視聴者端末が[switchRole(TRTCCloudDef.TRTCRoleAnchor)](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a915a4b3abca0e41f057022a4587faf66) をコールしてロールをキャスター（TRTCCloudDef.TRTCRoleAnchor）に切り替えます。
2. 視聴者端末が[startLocalPreview()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116) をコールすると、ローカルの画面をアクティブにすることができます。
3. 視聴者端末が[startLocalAudio()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a9428ef48d67e19ba91272c9cf967e35e) をコールすると、マイクの集音を開始します。

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


<span id="step10"> </span>
### 手順10：キャスター間でのルームを跨いだマイク接続PKの実施

TRTC ではの異なるオーディオ・ビデオルームのキャスターが2人、当初のライブストリーミングを退出しないというユースケースにおいて、“ルームを跨いだ通話”機能によってマイク接続通話機能をプルして“ルームを跨いだマイク接続PK”を実施することができます。

1. キャスター A は、 [connectOtherRoom()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ac1ab7e4a017b99bb91d89ce1b0fac5fd) インターフェースをコールします。インターフェースパラメータは現在、JSON形式を採用しており、キャスターBの`{"roomId": 978,"userId": "userB"}`のフォーマットに組み立てられた`roomId`と`userId`のパラメータをインターフェース関数に渡す必要があります。
2．ルームを跨ぐことに成功した後は、キャスター A は [onConnectOtherRoom()](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#ac9fd524ab9de446f4aaf502f80859e95) イベントコールバックを受け取ります。同時に、2つのライブストリーミングルームのすべてのユーザーはいずれも [onUserVideoAvailable()](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05)  および [onUserAudioAvailable()](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f)  イベント通知を受け取ります。
 例えば、ルーム「001」のキャスターAがルーム「002」のキャスターBと`connectOtherRoom()`を介してルーム間通話する場合、ルーム「001」のユーザーはキャスターBの`onUserVideoAvailable(B, true)`コールバックと`onUserAudioAvailable(B, true)`コールバックを受信します。ルーム「002」のユーザーはキャスターAの`onUserVideoAvailable(A, true)`コールバックと`onUserAudioAvailable(A,true)`コールバックを受信します。
3. 2つのルームにいるユーザーは、 [startRemoteView(userId, view)](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) をコールすることで、もう一方のルームのキャスターの画面を表示することができ、音声は自動再生されます。

```java
//サンプルコード：ルームを跨いだマイク接続PK
mTRTCCloud.ConnectOtherRoom(String.format("{\"roomId\":%s,\"userId\":\"%s\"}", roomId, username));
```

<span id="step11"> </span>
### 手順11：現在のルームからの退出

[exitRoom()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a41d16a97a9cb8f16ef92f5ef5bfebee1) メソッドをコールしてルームを退出する場合、SDK は退室するとき、カメラ、マイクなどのハードデバイスを停止またはリリースする必要があります。このため、退室動作は決して瞬時に完了するものではなく、[onExitRoom()](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#ad5ac26478033ea9c0339462c69f9c89e)のコールバックを受信してから、実際に退室操作を完了したとみなす必要があります。

```java
// 退室のコール後は、onExitRoom イベントのコールバックをお待ちください
mTRTCCloud.exitRoom()

@Override
public void onExitRoom(int reason) {
    Log.i(TAG, "onExitRoom: reason = " + reason);
}
```

>!  App の中で多くの音声ビデオの SDKを同時に統合した場合は、`onExitRoom`コールバックを受信してからその他の音声ビデオ SDKを起動してください。そうしない場合は、ハード上の占有問題が生じることがあります。

