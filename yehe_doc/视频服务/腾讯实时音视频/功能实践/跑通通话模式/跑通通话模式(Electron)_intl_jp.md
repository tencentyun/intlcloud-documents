## 適用ケース

TRTC は、4種類の異なる入室モードをサポートしています。このうち、ビデオ通話（VideoCall）および音声通話（VoiceCall）を総称して通話モードといい、ビデオ・インタラクティブストリーミング（Live）およびボイス・インタラクティブストリーミング（VoiceChatRoom）を総称して [ライブストリーミングモード](https://intl.cloud.tencent.com/document/product/647/36070)といいます。
通話モードでのTRTCは、1つのルームに最大で300人の同時オンラインをサポートし最大で50人の同時発言をサポートします。1対1のビデオ通話、300人のビデオミーティング、オンライン問診、リモート面接、ビデオカスタマーサービス、オンライン人狼ゲームなどのユースケースに適合しています。

## 原理解析

TRTC クラウドサービスは、2種類の異なるタイプのサーバーノードから構成されており、それぞれ“インターフェースモジュール”および“プロキシモジュール”からなっています：

- **インターフェースモジュール**
    この種のノードは、最も良質の回線および高性能の機器を採用しており、エンドツーエンドの低遅延マイク接続通話の処理に優れますが、単位時間当たりの費用はやや高くなります
- **プロキシモジュール**
    この種のノードは、通常の回線および性能も一般的な機器を採用しており、同時進行性の高いプルストリーミング再生のニーズの処理にすぐれ、単位当たりの費用はやや低くなります。

通話モードでは、TRTCルームのすべてのユーザーはインターフェースモジュールに分配されます。各ユーザーは“キャスター”に相当し、各ユーザーは随時発言でき（同時アップストリームの最大制限は50）、このためオンラインミーティングなどのユースケースに適していますが、1つのルームの人数制限は300人になります。

![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## サンプルコード

 [Github](https://github.com/tencentyun/TRTCSDK/tree/master/Electron) にログインし、本ファイルに関連するサンプルコードを取得することができます。

##　操作手順

<span id="step1"></span>
### 手順1：跑通正式サイト SimpleDemoのテスト

まずファイル [ SimpleDemoクイックスタート(Electron)](https://intl.cloud.tencent.com/document/product/647/35089)を読んで、ドキュメントのガイド、提供されている公式 SimpleDemoに従ってください。

SimpleDemo が順調に動作できる場合は、項目の中で Electron をインストールする方法を把握していることを意味します。

逆に、 SimpleDemo の動作に問題がある場合は、おそらく Electronのダウンロード、インストールに問題があったことが考えられます。この場合はElectron の公式サイトの [インストールガイド](https://www.electronjs.org/docs/tutorial/installation) を参照することができます。

<span id="step2"></span>
### 手順2：項目のための trtc-electron-sdkの統合

[手順1](#step1) が正常に動作し、予想通りの効果があった場合は、 Electron 環境のインストール方法を把握していることを意味します。

私どもの正式Demoにおいて二次開発を行うことができます。項目の初級段階は比較的順調です。

以下のコマンドを実行することもできます。 `trtc-electron-sdk` を既存のプロジェクトにインストールすることもできます。

```bash
npm install trtc-electron-sdk --save
```

<span id="step3"></span>
### 手順3： SDKのインスタンスを初期化してイベントのコールバックをモニタ

 `trtc-electron-sdk` インスタンスの新規作成：

```javascript
import TRTCCloud from 'trtc-electron-sdk';
let trtcCloud = new TRTCCloud();
```

 `onError` イベントのモニタ：

```javascript
// エラー通知はモニタされるべきもので、入手してユーザーに通知する必要があります
let onError = function(err) {
  console.error(err);
};
trtcCloud.on('onError',onError);
```

<span id="step4"></span>
### 手順4：入室パラメータ TRTCParamsの組み立て

[enterRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#enterRoom) インターフェースをコールするとき、一つのキーパラメータ [TRTCParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html)を入力する必要があります。このパラメータに含まれる入力必須のフィールドは下表のとおりです。

| パラメータ     | タイプ  | 説明                                                         | サンプル                  |
| :------- | :----- | :----------------------------------------------------------- | :--------------------- |
| sdkAppId | 数字  | アプリケーション ID， [コンソール](https://console.cloud.tencent.com/trtc/app) >【アプリケーション管理】>【アプリケーション情報】から見つかります。 | 1400000123  |
| userId  | 文字列 | アルファベットの大文字、小文字（a-z、A-Z）、数字（0-9）、下線およびハイフンのみを許可。 | test_user_001 |
| userSig | 文字列 |  userId を基に userSigを計算できます。計算方法は [ UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166) をご参照ください。| eJyrVareCeYrSy1SslI... |
| roomId | 数字 | デフォルトでは文字列のタイプのルームナンバーをサポートしていません、文字列タイプのルームナンバーは入室速度に影響します。文字列タイプのルームナンバーをサポートする必要が確実にある場合は、 [チケットを提出](https://console.cloud.tencent.com/workorder/category) してご連絡ください。 | 29834 |

```javascript
import {
  TRTCParams,
  TRTCRoleType 
} from "trtc-electron-sdk/liteav/trtc_define";

let param = new TRTCParams();
param.sdkAppId = 1400000123;
param.roomId = 29834;
param.userId = 'test_user_001';
param.userSig = 'eJyrVareCeYrSy1SslI...';
```

>! TRTC は同時に2つの同じ userIdで入室できません。そうしないと相互に干渉することになります。

<span id="step5"></span>
### 手順5：新規作成および入室

1.   [enterRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#enterRoom) をコールすると、すぐに TRTCParams パラメータの`roomId`が示すオーディオ・ビデオルームを追加できます。このルームが存在しない場合は、SDK はフィールド`roomId`の値をルームナンバーとする新しいルームを自動的に作成します。

2. ユースケースに基づき適切な　`appScene`　パラメータを設定してください。誤った選択をすると、ラグ率または画面の解像度が想定のレベルに到達しなくなります。

   - ビデオ通話は、`TRTCAppScene.TRTCAppSceneVideoCall`に設定してください。
   - 音声通話は、`TRTCAppScene.TRTCAppSceneAudioCall`に設定してください。

    `TRTCAppScene` の詳細説明は、次をクリックして表示してください：[TRTCAppScene ](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCAppScene)。

3. 入室に成功したら、SDK は [onEnterRoom(result)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onEnterRoom) イベントにコールバックします。このうち、パラメータ `result` が0より大きいときは、入室成功を意味し、具体的な数値は入室してからの消費時間を示します。単位はミリ秒（ms）です。 `result` が0より小さいときは、入室失敗を意味し、具体的な数値は入室失敗のエラーコードを示します。

```javascript
import TRTCCloud from 'trtc-electron-sdk';
import { TRTCParams, TRTCAppScene } from "trtc-electron-sdk/liteav/trtc_define";
import TRTCCloud from 'trtc-electron-sdk';
let trtcCloud = new TRTCCloud();

let onEnterRoom = function (result) {
  if (result > 0) {
    console.log(`onEnterRoom，入室成功、 ${result} 秒`を使用);
  }else{
    console.warn(`onEnterRoom: 入室失敗 ${result}`);
  }
};

/ /入室成功イベントを閲覧
trtcCloud.on('onEnterRoom', onEnterRoom);

// 入室。ルームが存在しない場合は、TRTC バックエンドは新規ルームを自動作成
let param = new TRTCParams();
param.sdkAppId = 1400000123;
param.roomId = 29834;
param.userId = 'test_user_001';
param.userSig = 'eJyrVareCeYrSy1SslI...';
trtcCloud.enterRoom(param, TRTCAppScene.TRTCAppSceneVideoCall);
```

<span id="step6"></span>
### 手順6：リモート側のオーディオ・ビデオストリーミングの閲覧

SDK は、自動閲覧モードおよび手動閲覧モードの2種類のモードをサポートします。自動閲覧はインスタントブロードキャスティング速度を追求するので、少人数で通話するユースケースに適しています；手動閲覧はトラフィックの節約を追求するので、人数が多いミーティングでのユースケースに適しています。

#### 自動閲覧（推奨）

特定のルームに入った後、SDKはルームのその他のユーザーのオーディオストリーミングを自動で受信します。これによって最高の“インスタントブロードキャスティング”効果に達します：

1.  ルームのその他のユーザーが音声データをアップストリームするとき、 [onUserAudioAvailable()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserAudioAvailable) イベントの通知を受け取り、SDK はこれらのリモート側ユーザーの音声を自動再生します。

2.   [muteRemoteAudio(userId,  true)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteRemoteAudio) によって、 userId の音声データを遮断し、[muteAllRemoteAudio(true)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteAllRemoteAudio) によって、すべてのリモート側ユーザーの音声データを遮断することもできます。遮断後にSDK はリモート側ユーザーに対応する音声データをこれ以上継続してプルすることはありません。

3. . ルームのその他のユーザーがビデオデータをアップストリームするとき、 [onUserVideoAvailable()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserVideoAvailable) イベント通知を受信します。しかし、このとき SDKはビデオデータをどのように表示するか指令を受け取っていないため、ビデオデータを自動処理することはありません。 [startRemoteView(userId, view)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView) メソッドをコールしてリモート側ユーザーのビデオデータと`view`表示を関連付けする必要があります。

4.    [setLocalViewFillMode()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLocalViewFillMode) によってビデオ画面の表示モードを指定することができます。
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fill` モード：塗りつぶしを意味し、画面は同じ比率で拡大およびトリミングできますが、黒い縁取りは付きません。
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fit` モード：適応を意味し、画面は同じ比率で縮小してスクリーンにフィットしてそのコンテンツを完全に表示しますが、黒い縁取りが付くことがあります。
  
5.   [muteRemoteAudio(userId,  true)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopRemoteView) によって、特定のuserId のビデオデータを遮断し、[stopAllRemoteView()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopAllRemoteView) によって、すべてのリモート側のユーザーのビデオデータを遮断することもできます。遮断後、SDK はリモート側ユーザーに対応するビデオデータを継続してプルすることはありません。

```html
<div id="video-container"></div>

<script>
  import TRTCCloud from 'trtc-electron-sdk';
  const trtcCloud = new TRTCCloud();
  const videoContainer = document.querySelector('#video-container');
  const roomId = 29834;

  /**
   * ビデオのカメラ起動の有無
   * @param {number} uid - ユーザーID
   * @param {boolean} available - 画面の起動の有無
   **/
  let onUserVideoAvailable = function (uid, available) {
    console.log(`onUserVideoAvailable: uid: ${uid}, available: ${available}`);
    if (available===1) {
      let id = `${uid}-${roomId}-${TRTCVideoStreamType.TRTCVideoStreamTypeBig}`;
      let view = document.getElementById(id);
      if (!view) {
        view = document.createElement('div');
        view.id = id;
        videoContainer.appendChild(view);
      }
      trtcCloud.startRemoteView(uid, view);
      trtcCloud.setRemoteViewFillMode(uid, TRTCVideoFillMode.TRTCVideoFillMode_Fill);
    }else{
      let id = `${uid}-${roomId}-${TRTCVideoStreamType.TRTCVideoStreamTypeBig}`;
      let view = document.getElementById(id);
      if (view) {
        videoContainer.removeChild(view);
      }
    }
  };

  // インスタンスコード：通知に基づきリモート側ユーザーのビデオ画面を閲覧（または閲覧の取り消し）します。
  trtcCloud.on('onUserVideoAvailable', onUserVideoAvailable);

</script>
```

>? `onUserVideoAvailable()`インシデントを受信しコールバック後、すぐに`startRemoteView()`をコールしてビデオストリーミングを閲覧しない場合は、SDK は5s以内にリモートからのビデオデータの受信を停止します。

#### 手動閲覧

 [setDefaultStreamRecvMode(autoRecvAudio, autoRecvVideo)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setDefaultStreamRecvMode) インターフェースによって、 SDK を手動閲覧モードに指定できます。手動閲覧モードでは、SDK はルームのその他のユーザーの音声ビデオデータを自動受信しませんので、手動で API 関数を通じてトリガーさせる必要があります。

1.  **入室前**に [setDefaultStreamRecvMode(false, false)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setDefaultStreamRecvMode) インターフェースをコールして、 SDK を手動閲覧モードに設定します。
2.  ルームのその他のユーザーが音声データをアップストリームするとき、 [onUserAudioAvailable()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserAudioAvailable)イベントの通知を受信します。この時[muteRemoteAudio(userId, false)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteRemoteAudio) をコールすることで、そのユーザーの音声データを手動で閲覧する必要があります。SDK はそのユーザーの音声データを受信後、デコードして再生します。
3. ルームのその他のユーザーがビデオデータをアップストリームするとき、 [onUserVideoAvailable(userId, available)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserVideoAvailable) イベントの通知を受信します。この時[startRemoteView(userId, view)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView) メソッドをコールしてそのユーザーのビデオデータを手動で閲覧する必要があります。SDKは、そのユーザーのビデオデータを受信後、デコードして再生します。


<span id="step7"></span>
### 手順7：ローカルのオーディオ・ビデオストリーミングの公開

1.  [startLocalAudio()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalAudio) をコールして、ローカルのマイク集音を起動し、集音した音声をエンコードして送信します。
2. [startLocalPreview()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalPreview) をコールして、ローカルのカメラを起動し、収集したビデオをエンコードして送信します。
3.    [setLocalViewFillMode()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLocalViewFillMode)  をコールすると、ローカルのビデオ画面の表示モードを設定することができます。
   -   `TRTCVideoFillMode.TRTCVideoFillMode_Fill` モードは塗りつぶしを意味し、画面は同じ比率で拡大およびトリミングできますが、黒い縁取りは付きません。
   -   `TRTCVideoFillMode.TRTCVideoFillMode_Fit` は適応を意味し、画面は同じ比率で縮小してスクリーンにフィットしてそのコンテンツを完全に表示しますが、黒い縁取りが付くことがあります。
4.  [setVideoEncoderParam()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setVideoEncoderParam) インターフェースをコールすると、ローカルビデオのエンコードパラメータを設定できますが、そのパラメータはルームのその他ユーザーが視聴する画面の [画質](https://intl.cloud.tencent.com/document/product/647/35153)を決定します。

```javascript
//サンプルコード：ローカルのオーディオ・ビデオストリーミングの公開
trtcCloud.startLocalPreview(view);
trtcCloud.setLocalViewFillMode(TRTCVideoFillMode.TRTCVideoFillMode_Fill);
trtcCloud.startLocalAudio();
//ローカルビデオエンコードパラメータの設定
let encParam = new TRTCVideoEncParam();
encParam.videoResolution = TRTCVideoResolution.TRTCVideoResolution_640_360;
encParam.resMode = TRTCVideoResolutionMode.TRTCVideoResolutionModeLandscape;
encParam.videoFps = 25;
encParam.videoBitrate = 600;
encParam.enableAdjustRes = true;
trtcCloud.setVideoEncoderParam(encParam);
```

>! SDK のデフォルトは、現在のシステムのデフォルトのカメラおよびマイクを使用します。[setCurrentCameraDevice()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentCameraDevice) および[setCurrentMicDevice()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentMicDevice) をコールして、その他のカメラおよびマイクを選択することができます。


<span id="step8"></span>
### 手順8：現在のルームからの退出

 [exitRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#exitRoom) メソッドをコールしてルームを退出する場合、SDK は退室するとき、カメラ、マイクなどのハードデバイスを停止またはリリースする必要があります。このため、退室動作は決して瞬時に完了するものではなく、 [onExitRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onExitRoom) のコールバックを受信してから、実際に退室操作を完了したとみなす必要があります。

```javascript
// 退室のコール後は、onExitRoom イベントのコールバックをお待ちください
let onExitRoom = function (reason) {
  console.log(`onExitRoom, reason: ${reason}`);
};
trtcCloud.exitRoom()
trtcCloud.on('onExitRoom', onExitRoom);
```

>!  Electron プログラムで複数の音声ビデオ SDKを同時に統合した場合は、`onExitRoom`を受信してコールバックしてから、その他の音声ビデオ SDKを起動してください。そうしない場合は、ハード上の占有問題が生じることがあります。
