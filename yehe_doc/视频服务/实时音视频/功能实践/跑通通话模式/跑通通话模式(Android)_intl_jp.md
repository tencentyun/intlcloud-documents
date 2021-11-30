## 適用ケース
TRTC は、4種類の異なる入室モードをサポートしています。このうち、ビデオ通話（VideoCall）および音声通話（AudioCall）を総称して通話モードといい、ビデオ・インタラクティブストリーミング（Live）およびボイス・インタラクティブストリーミング（VoiceChatRoom）を総称して [ライブストリーミングモード](https://intl.cloud.tencent.com/document/product/647/35108)といいます。
通話モードでのTRTCは、1つのルームに最大で300人の同時オンラインをサポートし最大で50人の同時発言をサポートします。1対1のビデオ通話、300人のビデオミーティング、オンライン問診、リモート面接、ビデオカスタマーサービス、オンライン人狼ゲームなどのユースケースに適合しています。

## 原理解析
TRTC クラウドサービスは、2種類の異なるタイプのサーバーノードから構成されており、それぞれ“インターフェースモジュール”および“プロキシモジュール”からなっています：
- **インターフェースモジュール**
この種のノードは、最も良質の回線および高性能の機器を採用しており、エンドツーエンドの低遅延マイク接続通話の処理に優れますが、単位時間当たりの費用はやや高くなります
- **プロキシモジュール**
この種のノードは、通常の回線および性能も一般的な機器を採用しており、同時進行性の高いプルストリーミング再生のニーズの処理にすぐれ、単位当たりの費用はやや低くなります。

通話モードでは、TRTCルームのすべてのユーザーはインターフェースモジュールに分配されます。各ユーザーは“キャスター”に相当し、各ユーザーは随時発言でき（同時アップストリームの最大制限は50）、このためオンラインミーティングなどのユースケースに適していますが、1つのルームの人数制限は300人になります。


## サンプルコード
 [Github] にログインし、本ファイルに関連するサンプルコードを取得することができます。
![](https://main.qcloudimg.com/raw/3ef83a68399c22ba0c1fbb079e3dfaf3.png)

> Githubへのアクセスが遅い場合は、 [TXLiteAVSDK_TRTC_Android_latest.zip](http://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip)を直接ダウンロードすることもできます。

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
>現在 TRTC SDK は armeabi ， armeabi-v7a および arm64-v8aをサポートしています。
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
```
//  trtcCloud インスタンスを作成
mTRTCCloud = TRTCCloud.sharedInstance(getApplicationContext());
mTRTCCloud.setListener(new TRTCCloudListener());
```
2. `setListener`属性を設定しイベントのコールバックを登録し、関連 イベントおよびエラー通知をモニタします。
```
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
[enterRoom()] インターフェースをコールするとき、キーパラメータ [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a674b3c744a0522802d68dfd208763b59)を入力する必要があります。このパラメータに含まれる入力必須のフィールドは下表に示すとおりです。

| パラメータ名 | フィールドタイプ | 補足説明 |記入例 |
|---------|---------|---------|---------|
| sdkAppId | 数字 | アプリケーション ID， <a href="https://console.cloud.tencent.com/trtc/app">Tencent Real-Time Communicationコンソール</a> でSDKAppIDを表示できます。|1400000123 |
| userId | 文字列 | アルファベットの大文字、小文字（a-z、A-Z）、数字（0-9）、下線およびハイフンのみを許可。 | test_user_001 |
| userSig | 文字列 |  userId を基に userSigは計算されます。計算方法は [ UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166) をご参照ください。| eJyrVareCeYrSy1SslI... |
| roomId | 数字 | 数字タイプのルームナンバー。文字列形式のルームナンバーを使用したい場合は、TRTCParamsのstrRoomIdをご使用ください。 | 29834 |

>TRTC は同時に2つの同じ userIdで入室できません。そうしないと相互に干渉することになります。

<span id = "step5"></span>
### 手順5：新規作成および入室
1.  [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) をコールすると、すぐに TRTCParams パラメータの`roomId`が示すオーディオ・ビデオルームを追加できます。このルームが存在しない場合は、SDK はフィールド`roomId`の値をルームナンバーとする新しいルームを自動的に作成します。
2. ユースケースに基づき適切な**`appScene`**パラメータを設定してください。誤った選択をすると、ラグ率または画面の解像度が想定のレベルに到達しなくなります。
 - ビデオ通話は、`TRTC_APP_SCENE_VIDEOCALL`と設定してください。
 - 音声通話は、`TRTC_APP_SCENE_AUDIOCALL`に設定してください。
3. 入室に成功したら、SDK は`onEnterRoom(result)`イベントをコールバックします。そのうち、パラメータ`result`が0より大きいときは入室成功を示し、具体的な数値は入室してからの消費時間になります。単位はミリ秒（ms）です。`result`が0より小さいときは入室失敗を示し、具体的な数値は入室失敗のエラーコードになります。

```
public void enterRoom() {
    TRTCCloudDef.TRTCParams trtcParams = new TRTCCloudDef.TRTCParams();
    trtcParams.sdkAppId = sdkappid
    trtcParams.userId   = userid;
    trtcParams.roomId = usersig;
    trtcParams.userSig = 908;
    mTRTCCloud.enterRoom(trtcParams, TRTC_APP_SCENE_VIDEOCALL);
}

@Override
public void onEnterRoom(long result) {
    if result > 0 {
        toastTip("入室成功，総消費時間[╲(result)]ms")
    }else{
        toastTip("入室失敗，エラーコード[╲(result)]")
    }
}
```
> 
>- 入室に失敗した場合は、SDK は同時に`onError`イベントもコールバックし、パラメータ`errCode`（[エラーコード](https://intl.cloud.tencent.com/document/product/647/35130)）、`errMsg`（エラー原因）および`extraInfo`（予約済みパラメータ）に戻ります。
>- 既に特定のルームにいる場合は、まず`exitRoom()`をコールして現在のルームを退出すると、もう一つのルームに入ることができるようになります。

<span id = "step6"></span>
### 手順6：リモート側のオーディオ・ビデオストリーミングの閲覧
SDKは自動閲覧および手動閲覧をサポートします。

#### 自動閲覧モード（デフォルト）
自動閲覧モードでは、特定のルームに入った後、SDKはルームのその他のユーザーのオーディオストリーミングを自動で受信します。これによって最高の“インスタントブロードキャスティング”効果が得られます。
1. ルームのその他のユーザーが音声データをアップストリームするとき、 [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f) イベントの通知を受信します。SDK はリモート側ユーザーの音声を自動再生します。
2.  [muteRemoteAudio(userId, mute: true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8d8b8edf120036d4049cc3639a1ce81f)によって、特定の userId の音声データを遮断し、[muteAllRemoteAudio(true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a5b63c0796404b80323ae67aafe0384ba) によって、すべてのリモート側ユーザーの音声データを遮断することもできます。遮断後にSDK はリモート側ユーザーに対応する音声データをこれ以上継続してプルすることはありません。
3. ルームのその他のユーザーがビデオデータをアップストリームするとき、 [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) イベント通知を受信します。しかし、このとき SDKはビデオデータをどのように表示するか指令を受け取っていないため、ビデオデータを自動処理することはありません。 [startRemoteView(userId, view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) メソッドをコールしてリモート側ユーザーのビデオデータと`view`表示をバインドする必要があります。
4.  [setRemoteViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ab4197bc2efb62b471b49f926bab9352f) によってビデオ画面の表示モードを指定することができます。
 - Fill モード：塗りつぶしを意味し、画面は同じ比率で拡大およびトリミングできますが、黒い縁取りは付きません。
 - Fit モード：適応を意味し、画面は同じ比率で縮小してスクリーンにフィットしてそのコンテンツを完全に表示しますが、黒い縁取りが付くことがあります。
5. [stopRemoteView(userId)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8f3e86bc219090d0e8f2d5c2fab4467a) によって、特定の userId のビデオデータを遮断し、[stopAllRemoteView()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#addaac0786ac0bd6e73a5f35c038df127) によって、すべてのリモート側のユーザーのビデオデータを遮断することもできます。遮断後、SDK はリモート側ユーザーに対応するビデオデータを継続してプルすることはありません。

```
@Override
public void onUserVideoAvailable(String userId, boolean available) {
    TXCloudVideoView remoteView = remoteViewDic[userId];
    if (available) {
        mTRTCCloud.startRemoteView(userId, remoteView);
        mTRTCCloud.setRemoteViewFillMode(userId, TRTC_VIDEO_RENDER_Mode_FIT)：
    }else{
        mTRTCCloud.stopRemoteView(userId);
    }
}
```

> `onUserVideoAvailable()`イベントを受信しコールバック後、すぐに`startRemoteView()`をコールしてビデオストリーミングを閲覧しない場合は、SDK は5s以内にリモートからのビデオデータの受信を停止します。

#### 手動閲覧モード
 [setDefaultStreamRecvMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a0b8d004665d5003ce1d9a48a9ab551b3) インターフェースによって、 SDK を手動閲覧モードに指定できます。手動閲覧モードでは、SDK はルームのその他のユーザーの音声ビデオデータを自動受信しませんので、手動で API 関数を通じてトリガーさせる必要があります。

1. **入室前**に [setDefaultStreamRecvMode(false, false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a0b8d004665d5003ce1d9a48a9ab551b3) インターフェースをコールして、 SDK を手動閲覧モードに設定します。
2. ルームのその他のユーザーが音声データをアップストリームするとき、 [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f) イベントの通知を受信します。この時 [muteRemoteAudio(userId, false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8d8b8edf120036d4049cc3639a1ce81f) をコールすることで、そのユーザーの音声データを手動で閲覧する必要があります。SDK はそのユーザーの音声データを受信後、デコードして再生します。
3. ルームのその他のユーザーがビデオデータをアップストリームするとき、 [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) イベントの通知を受信します。この時[startRemoteView(userId, remoteView)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c)メソッドをコールしてそのユーザーのビデオデータを手動で閲覧する必要があります。SDKは、そのユーザーのビデオデータを受信後、デコードして再生します。


<span id = "step7"></span>
### 手順7：ローカルのオーディオ・ビデオストリーミングの公開
1. [startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a9428ef48d67e19ba91272c9cf967e35e) をコールして、ローカルのマイク集音を起動し、集音した音声をエンコードして送信します。
2. [startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116) をコールして、ローカルのカメラを起動し、収集したビデオをエンコードして送信します。
3.  [setLocalViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#af36ab721c670e5871e5b21a41518b51d)をコールすると、ローカルのビデオ画面の表示モードを設定することができます。
 - Fill モードは塗りつぶしを意味し、画面は同じ比率で拡大およびトリミングできますが、黒い縁取りは付きません。
 - Fit モードは適応を意味し、画面は同じ比率で縮小してスクリーンにフィットしてそのコンテンツを完全に表示しますが、黒い縁取りが付くことがあります。
4.  [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ae047d96922cb1c19135433fa7908e6ce) インターフェースをコールすると、ローカルビデオのエンコードパラメータを設定できますが、そのパラメータはルームのその他ユーザーが視聴する画面の [画質](https://intl.cloud.tencent.com/document/product/647/35153)を決定します。
```java
//サンプルコード：ローカルのオーディオ・ビデオストリーミングの公開
mTRTCCloud.setLocalViewFillMode(TRTC_VIDEO_RENDER_MODE_FIT);
mTRTCCloud.startLocalPreview(mIsFrontCamera, mLocalView);
mTRTCCloud.startLocalAudio();
```

<span id = "step8"></span>
### 手順8：現在のルームからの退出

[exitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a41d16a97a9cb8f16ef92f5ef5bfebee1) メソッドをコールしてルームを退出する場合、SDK は退室するとき、カメラ、マイクなどのハードデバイスを停止またはリリースする必要があります。このため、退室動作は決して瞬時に完了するものではなく、[onExitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ad5ac26478033ea9c0339462c69f9c89e)のコールバックを受信してから、実際に退室操作を完了したとみなす必要があります。

```java
// 退室のコール後は、onExitRoom イベントのコールバックをお待ちください
mTRTCCloud.exitRoom()

@Override
public void onExitRoom(int reason) {
    Log.i(TAG, "onExitRoom: reason = " + reason);
}
```

>  App の中で多くの音声ビデオの SDKを同時に統合した場合は、`onExitRoom`コールバックを受信してからその他の音声ビデオ SDKを起動してください。そうしない場合は、ハード上の占有問題が生じることがあります。


