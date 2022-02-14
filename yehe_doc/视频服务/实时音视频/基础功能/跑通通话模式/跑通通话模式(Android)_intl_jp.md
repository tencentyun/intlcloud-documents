## ユースケース
TRTCは、4種類の異なる入室モードをサポートしています。このうち、ビデオ通話（VideoCall）および音声通話（AudioCall）を総称して通話モードといい、ビデオインタラクティブストリーミング（Live）およびボイスインタラクティブストリーミング（VoiceChatRoom）を総称して [ライブストリーミングモード](https://intl.cloud.tencent.com/document/product/647/35108)といいます。
通話モードでのTRTCは、1つのルームに最大で300人の同時オンラインをサポートし最大で50人の同時発言をサポートします。1対1のビデオ通話、300人のビデオミーティング、オンライン問診、リモート面接、ビデオカスタマーサービス、オンライン人狼ゲームなどのユースケースに適合しています。

## 原理解析
TRTCクラウドサービスは、「インターフェースモジュール」および「プロキシモジュール」という2種類の異なるタイプのサーバーノードから構成されています。
-   **インターフェースモジュール**
この種のノードは、最も良質の回線および高性能の機器を採用しており、エンドツーエンドの低遅延マイク接続通話の処理に優れますが、単位時間当たりの費用はやや高くなります。
-   **プロキシモジュール**
この種のノードは、通常の回線および性能も一般的な機器を採用しており、同時進行性の高いプルストリーミング再生のニーズの処理にすぐれ、単位当たりの費用はやや低くなります。

通話モードでは、TRTCルームのすべてのユーザーはインターフェースモジュールに割り当てられます。各ユーザーは「キャスター」に相当し、各ユーザーは随時発言でき（同時アップストリームの最大制限は50）、このためオンラインミーティングなどのユースケースに適していますが、1つのルームの人数制限は300人になります。
![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## サンプルコード
[Github](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTC-API-Example) にログインし、本ファイルに関連するサンプルコードを取得することができます。
![](https://main.qcloudimg.com/raw/cdef573133900a8dce22dcca5242fcfc.png)

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
3. 【Sync Now】をクリックし、SDKを同期します。
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
```
// trtcCloudインスタンスを作成
mTRTCCloud = TRTCCloud.sharedInstance(getApplicationContext());
mTRTCCloud.setListener(new TRTCCloudListener(){
    // コールバック処理
    ...
});
```
2. `setListener`属性を設定しイベントのコールバックを登録し、関連イベントおよびエラー通知をモニタします。
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

[](id:step4)
### 手順4：入室パラメータTRTCParamsを組み立てる
[enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c)インターフェースを呼び出すとき、キーパラメータ[TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a674b3c744a0522802d68dfd208763b59)を入力する必要があります。このパラメータに含まれる入力必須のフィールドは下表に示すとおりです。

| パラメータ名 | フィールドタイプ | 補足説明 |記入例 |
|---------|---------|---------|---------|
| sdkAppId | 数字 | アプリケーションID。<a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a>でSDKAppIDを表示できます。|1400000123 |
| userId | 文字列 | アルファベットの大文字、小文字（a-z、A-Z）、数字（0-9）、下線およびハイフンのみを許可。ビジネスの実際のアカウントシステムを組み合わせて設定することをお勧めします。 |test_user_001 |
| userSig | 文字列 | userIdを基にuserSigは計算されます。計算方法は[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166) をご参照ください。| eJyrVareCeYrSy1SslI... |
| roomId | 数字 | 数字タイプのルームナンバー。文字列形式のルームナンバーを使用したい場合は、TRTCParamsのstrRoomIdをご使用ください。 | 29834 |

>!TRTCは、2つの同じuserIdによる同時入室をサポートしていません。同時に入室した場合は相互に干渉します。

[](id:step5)
### 手順5：ルームの新規作成および入室
1. [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) を呼び出せば、TRTCParamsパラメータの`roomId`が示すオーディオビデオルームに入室できます。該当するルームが存在しない場合は、SDKがフィールド`roomId`の値をルームナンバーとする新しいルームを自動的に作成します。
2. ユースケースに基づき適切な**`appScene`**パラメータを設定してください。誤った選択をすると、ラグ率または画面の解像度が想定レベルに到達しなくなります。
 - ビデオ通話は、`TRTC_APP_SCENE_VIDEOCALL`と設定してください。
 - 音声通話は、`TRTC_APP_SCENE_AUDIOCALL`に設定してください。
3. 入室に成功したら、SDKは`onEnterRoom(result)`イベントをコールバックします。そのうち、パラメータ`result`が0より大きいときは入室成功を示し、具体的な数値は入室のために消費した時間になります。単位はミリ秒（ms）です。`result`が0より小さいときは入室失敗を示し、具体的な数値は入室失敗のエラーコードになります。

```
public void enterRoom() {
    TRTCCloudDef.TRTCParams trtcParams = new TRTCCloudDef.TRTCParams();
    trtcParams.sdkAppId = sdkappid;
    trtcParams.userId = userid;
    trtcParams.roomId = 908;
    trtcParams.userSig = usersig;
    mTRTCCloud.enterRoom(trtcParams, TRTC_APP_SCENE_VIDEOCALL);
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
>! 
>- 入室に失敗した場合は、SDKは同時に`onError`イベントもコールバックし、パラメータ`errCode`（[エラーコード](https://intl.cloud.tencent.com/document/product/647/35130)）、`errMsg`（エラー原因）および`extraInfo`（保留パラメータ）を返します。
>- すでに特定のルームにいる場合は、まず`exitRoom()`を呼び出して現在のルームを退出すると、もう一つのルームに入ることができるようになります。
>- 各端末のユースケースappSceneについては、統一する必要があります。統一していない場合、想定外のトラブルが生じる恐れがあります。

[](id:step6)
### 手順6：リモート側のオーディオビデオストリーミングの閲覧
SDKは自動閲覧および手動閲覧をサポートします。

#### 自動閲覧モード（デフォルト）
自動閲覧モードでは、特定のルームに入った後、SDKはルームのその他のユーザーのオーディオストリームを自動で受信します。これによって最適な「秒速開始」効果が得られます。
1. ルームのその他のユーザーがオーディオデータをアップストリームするとき、[onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f)イベントの通知を受信します。SDK はリモート側ユーザーの音声を自動再生します。
2. [muteRemoteAudio(userId, true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8d8b8edf120036d4049cc3639a1ce81f) によって、特定のuserIdのオーディオデータを遮断することができ、[muteAllRemoteAudio(true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a5b63c0796404b80323ae67aafe0384ba)によって、すべてのリモートユーザーのオーディオデータを遮断することもできます。遮断後、SDKは、当該リモートユーザーのオーディオデータをそれ以降プルしなくなります。
3. ルームのその他のユーザーがビデオデータを上りにするとき、 [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) インシデント通知を受信します。しかし、このとき SDKはビデオデータをどのように表示するか指令を受け取っていないため、ビデオデータを自動処理することはありません。 [startRemoteView(userId, view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) 方法をコールしてリモート側ユーザーのビデオデータおよび`view`表示をバインドする必要があります。
4. [setRemoteViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ab4197bc2efb62b471b49f926bab9352f) を介してビデオ画面の表示モードを指定できます。
 - Fillモード：塗りつぶしを意味し、画面は同じ比率で拡大およびトリミングできますが、黒い縁取りは付きません。
 - Fitモード：適応を意味し、画面は同じ比率で縮小してスクリーンにフィットしてそのコンテンツを完全に表示しますが、黒い縁取りが付くことがあります。
5. [stopRemoteView(userId)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8f3e86bc219090d0e8f2d5c2fab4467a)を介して、特定のuserIdのビデオデータを遮断することができ、また[stopAllRemoteView()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#addaac0786ac0bd6e73a5f35c038df127) を介して、すべてのリモートユーザーのビデオデータを遮断することもできます。遮断後、SDKは当該リモートユーザーのビデオデータをプルしなくなります。

```
@Override
public void onUserVideoAvailable(String userId, boolean available) {
    TXCloudVideoView remoteView = remoteViewDic[userId];
    if (available)  {
        mTRTCCloud.startRemoteView(userId, remoteView);
        mTRTCCloud.setRemoteViewFillMode(userId, TRTC_VIDEO_RENDER_MODE_FIT);
    }else{
        mTRTCCloud.stopRemoteView(userId);
    }
}
```

>? `onUserVideoAvailable()`イベントのコールバックを受信した後、すぐに`startRemoteView()`を呼び出してビデオストリームを閲覧しない場合、SDKは5s以内にリモートからのビデオデータの受信を停止します。

#### 手動閲覧モード
[setDefaultStreamRecvMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a0b8d004665d5003ce1d9a48a9ab551b3)インターフェースを介して、SDKを手動閲覧モードに指定できます。手動閲覧モードでは、SDKはルーム内の他のユーザーの音声・ビデオデータを自動受信しません。手動で、API関数を介してトリガーする必要があります。

1. **入室前**に[setDefaultStreamRecvMode(false, false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a0b8d004665d5003ce1d9a48a9ab551b3)インターフェースを呼び出し、SDKを手動閲覧モードに設定します。
2. ルーム内の他のユーザーがオーディオデータをアップストリームすると、[onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f) のイベント通知を受信します。この時に[muteRemoteAudio(userId, false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8d8b8edf120036d4049cc3639a1ce81f)を呼び出し、そのユーザーのオーディオデータを手動で閲覧する必要があります。SDKはそのユーザーのオーディオデータを受信した後、デコードして再生します。
3. ルーム内の他のユーザーがビデオデータをアップストリームすると、[onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05)のイベント通知を受信します。この時に、[startRemoteView(userId, remoteView)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) メソッドを呼び出し、そのユーザーのビデオデータを手動で閲覧する必要があります。SDKが、そのユーザーのビデオデータを受信後、デコードして再生します。


[](id:step7)
### 手順7：ローカルのオーディオビデオストリーミングの公開
1. [startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a9428ef48d67e19ba91272c9cf967e35e)を呼び出すと、ローカルのマイク集音を起動させ、採集した音声をエンコードして送信することができます。
2. [startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116)を呼び出すと、ローカルのカメラを起動させ、キャプチャした画面をエンコードして送信することができます。
3. [setLocalViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#af36ab721c670e5871e5b21a41518b51d)を呼び出し、ローカルのビデオ画面の表示モードを設定することができます。
 - Fillモードは塗りつぶしを意味し、画面は同じ比率で拡大およびトリミングできますが、黒い縁取りは付きません。
 - Fitモードは適応を意味し、画面は同じ比率で縮小してスクリーンにフィットしてそのコンテンツを完全に表示しますが、黒い縁取りが付くことがあります。
4. [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ae047d96922cb1c19135433fa7908e6ce)インターフェースを呼び出し、ローカルビデオのエンコードパラメータを設定できます。このパラメータにより、ルーム内の他のユーザーが視聴する際の画面の[画質](https://intl.cloud.tencent.com/document/product/647/35153)が決定されます。
```java
//サンプルコード：ローカルのオーディオ・ビデオストリーミングの公開
mTRTCCloud.setLocalViewFillMode(TRTC_VIDEO_RENDER_MODE_FIT);
mTRTCCloud.startLocalPreview(mIsFrontCamera, mLocalView);
mTRTCCloud.startLocalAudio();
```

[](id:step8)
### 手順8：現在のルームから退出する

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


