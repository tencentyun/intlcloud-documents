## 適用ケース

TRTCは、4種類の異なる入室モードをサポートしています。このうち、ビデオ通話（VideoCall）および音声通話（VoiceCall）を総称して通話モードといい、ビデオ・インタラクティブストリーミング（Live）およびボイス・インタラクティブストリーミング（VoiceChatRoom）を総称して [ライブストリーミングモード](https://intl.cloud.tencent.com/document/product/647/36070)といいます。
通話モードでのTRTCは、1つのルームに最大で300人の同時オンラインをサポートし最大で50人の同時発言をサポートします。1対1のビデオ通話、300人のビデオミーティング、オンライン問診、リモート面接、ビデオカスタマーサービス、オンライン人狼ゲームなどのユースケースに適合しています。

## 原理解析

TRTCクラウドサービスは、「インターフェースモジュール」および「プロキシモジュール」という2種類の異なるタイプのサーバーノードから構成されています。

-   **インターフェースモジュール**
    この種のノードは、最も良質の回線および高性能の機器を採用しており、エンドツーエンドの低遅延マイク接続通話の処理に優れますが、単位時間当たりの費用はやや高くなります
-   **プロキシモジュール**
    この種のノードは、通常の回線および性能も一般的な機器を採用しており、同時進行性の高いプルストリーミング再生のニーズの処理にすぐれ、単位当たりの費用はやや低くなります。

通話モードでは、TRTCルームのすべてのユーザーはインターフェースモジュールに割り当てられます。各ユーザーは「キャスター」に相当し、各ユーザーは随時発言でき（同時アップストリームの最大制限は50）、このためオンラインミーティングなどのユースケースに適していますが、1つのルームの人数制限は300人になります。

![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## サンプルコード

[Github](https://github.com/tencentyun/TRTCSDK/tree/master/Electron)にログインして、このドキュメントに関連したサンプルコードを取得することができます。

## 操作手順

[](id:step1)
### 手順1：公式ウェブサイトのSimpleDemoクイックスタートを試行する

初めにドキュメント[SimpleDemoクイックスタート(Electron)](https://intl.cloud.tencent.com/document/product/647/35089)を読み、ドキュメントのガイドに従って、提供されている公式SimpleDemoクイックスタートを実行してください。

SimpleDemoが順調に動作する場合は、プロジェクトにおいてElectronのインストール方法をお客様が把握していることを意味します。
- 反対に、SimpleDemoの動作に問題がある場合は、Electronのダウンロード、インストールに問題があったことが考えられます。この場合はElectronの公式サイトの[インストールガイド](https://www.electronjs.org/docs/tutorial/installation)をご参照ください。

[](id:step2)

### 手順2：お客様のプロジェクトにtrtc-electron-sdkを統合する

[手順1]](#step1) が正常に動作し、予想どおりの効果があった場合は、 Electron環境のインストール方法を把握していることを意味します。

- 弊社の公式Demoをベースとして二次開発を行うことができ、プロジェクトの初級段階がスムーズに進みます。
- 次のコマンドを実行して、既存のプロジェクトに`trtc-electron-sdk`をインストールすることもできます。
```bash
npm install trtc-electron-sdk --save
```

[](id:step3)
### 手順3：SDKインスタンスを初期化し、イベントコールバックを監視する

1. `trtc-electron-sdk`インスタンスの新規作成：
```javascript
import TRTCCloud from 'trtc-electron-sdk';
let trtcCloud = new TRTCCloud();
```
2. `onError`イベントの監視：
<dx-codeblock>
::: javascript javascript
// エラー通知は監視すべきもので、捕捉してユーザーに通知する必要があります
let onError = function(err) {
    console.error(err);
};
trtcCloud.on('onError',onError);
:::
</dx-codeblock>

[](id:step4)
### 手順4：入室パラメータTRTCParamsを組み立てる

[enterRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enterRoom)インターフェースを呼び出すときはキーパラメータ[TRTCParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCParams.html)を入力する必要があります。このパラメータに含まれる入力必須フィールドは下表に示すとおりです。

| パラメータ     | タイプ   | 説明                                                         | サンプル                   |
| :------- | :----- | :----------------------------------------------------------- | :--------------------- |
| sdkAppId | 数字  | アプリケーションID。 [コンソール](https://console.cloud.tencent.com/trtc/app) >【アプリケーション管理】>【アプリケーション情報】にあります。 | 1400000123  |
| userId  | 文字列 | アルファベットの大文字、小文字（a-z、A-Z）、数字（0-9）、下線およびハイフンのみを許可。 | test_user_001 |
| userSig | 文字列 |  userIdを基にuserSigを計算できます。計算方法は[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166) をご参照ください。| eJyrVareCeYrSy1SslI... |
| roomId   | 数字   | 数字タイプのルームナンバー。文字列形式のルームナンバーを使用したい場合は、TRTCParamsのstrRoomIdをご使用ください。 | 29834  |

<dx-codeblock>
::: javascript javascript
import {
  TRTCParams,
  TRTCRoleType 
} from "trtc-electron-sdk/liteav/trtc_define";

let param = new TRTCParams();
param.sdkAppId = 1400000123;
param.roomId = 29834;
param.userId = 'test_user_001';
param.userSig = 'eJyrVareCeYrSy1SslI...';
:::
</dx-codeblock>


>! 
>- TRTCは、2つの同じuserIdによる同時入室をサポートしていません。同時に入室した場合、相互に干渉します。
>- 各端末のユースケースappSceneについては、統一する必要があります。統一していない場合、想定外のトラブルが生じる恐れがあります。

[](id:step5)
### 手順5：ルームの新規作成および入室

1. [enterRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enterRoom)を呼び出せば、TRTCParamsパラメータの`roomId`が示すオーディオ・ビデオルームに参加できます。該当するルームが存在しない場合、SDKはフィールド`roomId`の値をルームナンバーとする新しいルームを自動的に作成します。
2. ユースケースに基づき適切な`appScene`パラメータを設定してください。誤った選択をすると、ラグ率または画面の解像度が想定のレベルに到達しなくなります。
   - ビデオ通話は、`TRTCAppScene.TRTCAppSceneVideoCall`に設定してください。
   - 音声通話は、`TRTCAppScene.TRTCAppSceneAudioCall`に設定してください。
>? `TRTCAppScene`の詳細な説明については、[TRTCAppScene ](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCAppScene)をご参照ください。
3. 入室に成功すると、SDKは[onEnterRoom(result)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onEnterRoom)イベントをコールバックします。このうち、パラメータ `result` が0より大きいときは、入室成功を意味し、具体的な数値は入室のために消費した時間となります。単位はミリ秒（ms）です。`result` が0より小さいときは、入室失敗を意味し、具体的な数値は入室失敗のエラーコードとなります。

<dx-codeblock>
::: javascript javascript
import TRTCCloud from 'trtc-electron-sdk';
import { TRTCParams, TRTCAppScene } from "trtc-electron-sdk/liteav/trtc_define";
import TRTCCloud from 'trtc-electron-sdk';
let trtcCloud = new TRTCCloud();

let onEnterRoom = function (result) {
  if (result > 0) {
    console.log(`onEnterRoom、入室成功、${result}秒を使用`);
  } else {
    console.warn(`onEnterRoom: 入室失敗 ${result}`);
  }
};

/ /入室成功イベントを閲覧
trtcCloud.on('onEnterRoom', onEnterRoom);

// 入室。ルームが存在しない場合は、TRTCバックエンドは新規ルームを自動作成
let param = new TRTCParams();
param.sdkAppId = 1400000123;
param.roomId = 29834;
param.userId = 'test_user_001';
param.userSig = 'eJyrVareCeYrSy1SslI...';
trtcCloud.enterRoom(param, TRTCAppScene.TRTCAppSceneVideoCall);
:::
</dx-codeblock>


[](id:step6)
### 手順6：リモート側のオーディオビデオストリーミングの閲覧

SDKは、自動閲覧モードおよび手動閲覧モードの2種類のモードをサポートします。自動閲覧はインスタントブロードキャスティング速度を追求するので、少人数で通話するユースケースに適しています；手動閲覧はトラフィックの節約を追求するので、人数が多いミーティングでのユースケースに適しています。

#### 自動閲覧（推奨）

特定のルームに入った後、SDKはルームのその他のユーザーのオーディオストリームを自動で受信します。これによって最高の「インスタントブロードキャスティング」効果に達します。

1. ルーム内の他のユーザーがオーディオデータをアップストリームすると、[onUserAudioAvailable()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserAudioAvailable)のイベント通知を受信し、SDKがそのリモートユーザーの音声を自動再生します。
2. [muteRemoteAudio(userId,  true)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteRemoteAudio)によって、特定のuserId のオーディオデータを遮断でき、[muteAllRemoteAudio(true)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteAllRemoteAudio)によって、すべてのリモートユーザーのオーディオデータを遮断することもできます。遮断した後、SDKは、当該リモートユーザーのオーディオデータをそれ以上プルしなくなります。
3. ルーム内の他のユーザーがビデオデータをアップストリームすると、[onUserVideoAvailable()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserVideoAvailable)のイベント通知を受信しますが、このときSDKはビデオデータをどのように表示するか指令を受け取っていないため、ビデオデータを自動処理することはありません。[startRemoteView(userId, view, streamType)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView)メソッドを呼び出して、リモートユーザーのビデオデータと`view`（表示）を関連付けする必要があります。
4. [setLocalViewFillMode()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewFillMode)によって、ビデオ画面の表示モードを指定することができます。
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fill` モード：塗りつぶしを意味し、画面は同じ比率で拡大およびトリミングできますが、黒い縁取りは付きません。
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fit` モード：適応を意味し、画面は同じ比率で縮小してスクリーンにフィットしてそのコンテンツを完全に表示しますが、黒い縁取りが付くことがあります。
5. [stopRemoteView(userId)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopRemoteView)によって、特定のuserIdのビデオデータを遮断でき、[stopAllRemoteView()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopAllRemoteView)によって、すべてのリモートユーザーのビデオデータを遮断することもできます。遮断した後、SDKは、該当するリモートユーザーのオーディオデータをそれ以上プルしなくなります。

<dx-codeblock>
::: html html
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
    if (available === 1) {
      let id = `${uid}-${roomId}-${TRTCVideoStreamType.TRTCVideoStreamTypeBig}`;
      let view = document.getElementById(id);
      if (!view) {
        view = document.createElement('div');
        view.id = id;
        videoContainer.appendChild(view);
      }
      trtcCloud.startRemoteView(uid, view);
      trtcCloud.setRemoteViewFillMode(uid, TRTCVideoFillMode.TRTCVideoFillMode_Fill);
    } else {
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
:::
</dx-codeblock>

>? `onUserVideoAvailable()`イベントのコールバックを受信した後、すぐに`startRemoteView()`を呼び出してビデオストリームを閲覧しない場合、SDKは5s以内にリモートからのビデオデータの受信を停止します。

#### 手動閲覧

[setDefaultStreamRecvMode(autoRecvAudio, autoRecvVideo)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setDefaultStreamRecvMode)インターフェースによって、SDKを手動閲覧モードに指定できます。手動閲覧モードでは、SDKはルーム内のその他ユーザーの音声ビデオデータを自動受信しませんので、API関数を介して、手動でトリガーする必要があります。

1. **入室前**に、[setDefaultStreamRecvMode(false, false)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setDefaultStreamRecvMode)インターフェースを呼び出して、SDKを手動閲覧モードに設定します。
2. ルーム内の他のユーザーがオーディオデータをアップストリームすると、[onUserAudioAvailable()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserAudioAvailable)のイベント通知を受信します。この時、[muteRemoteAudio(userId, false)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteRemoteAudio)を呼び出して、当該ユーザーのオーディオデータを手動で閲覧する必要があります。SDKは、そのユーザーのオーディオデータを受信した後、デコードして再生します。
3. ルーム内の他のユーザーがビデオデータをアップストリームすると、[onUserVideoAvailable(userId, available)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserVideoAvailable)のイベント通知を受信します。この時、[startRemoteView(userId,  view)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView)メソッドを呼び出して、当該ユーザーのビデオデータを手動で閲覧する必要があります。SDKは、そのユーザーのビデオデータを受信した後、デコードして再生します。


[](id:step7)
### 手順7：ローカルのオーディオビデオストリーミングの公開

1. [startLocalAudio()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalAudio)を呼び出すと、ローカルのマイク集音を起動し、採集した音声をエンコードして送信することができます。
2. [startLocalPreview()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalPreview)を呼び出すと、ローカルのカメラを起動し、キャプチャした画面をエンコードして送信することができます。
3. [setLocalViewFillMode()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewFillMode)を呼び出すと、ローカルのビデオ画面の表示モードを設定することができます。
   - `TRTCVideoFillMode.TRTCVideoFillMode_Fill` モードは塗りつぶしを意味し、画面は同じ比率で拡大およびトリミングできますが、黒い縁取りは付きません。
   - `TRTCVideoFillMode.TRTCVideoFillMode_Fit` は適応を意味し、画面は同じ比率で縮小してスクリーンにフィットしてそのコンテンツを完全に表示しますが、黒い縁取りが付くことがあります。
4. [setVideoEncoderParam()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderParam)インターフェースを呼び出すと、ローカルビデオのエンコードパラメータを設定できます。このパラメータにより、ルーム内の他のユーザーが視聴する際の画面の[画質](https://intl.cloud.tencent.com/document/product/647/35153)が決定されます。

<dx-codeblock>
::: javascript javascript
//サンプルコード：ローカルのオーディオ・ビデオストリーミングの公開
trtcCloud.startLocalPreview(view);
trtcCloud.setLocalViewFillMode(TRTCVideoFillMode.TRTCVideoFillMode_Fill);
trtcCloud.startLocalAudio();
//ローカルビデオコーデックパラメータの設定
let encParam = new TRTCVideoEncParam();
encParam.videoResolution = TRTCVideoResolution.TRTCVideoResolution_640_360;
encParam.resMode = TRTCVideoResolutionMode.TRTCVideoResolutionModeLandscape;
encParam.videoFps = 25;
encParam.videoBitrate = 600;
encParam.enableAdjustRes = true;
trtcCloud.setVideoEncoderParam(encParam);
:::
</dx-codeblock>


>! SDKはデフォルトでは、現在のシステムのデフォルトのカメラおよびマイクを使用します。[setCurrentCameraDevice()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentCameraDevice)および[setCurrentMicDevice()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentMicDevice)を呼び出して、その他のカメラおよびマイクを選択することができます。


[](id:step8)
### 手順8：現在のルームから退出する

[exitRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#exitRoom)メソッドを呼び出してルームを退出します。SDKは退室する時に、カメラ、マイクなどのハードウェアデバイスを停止してリリースする必要があるため、退室の動作は瞬時に完了するものではなく、[onExitRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onExitRoom)のコールバックを受信してはじめて、実際の退室操作が完了します。

<dx-codeblock>
::: javascript javascript
// 退室を呼び出した後は、onExitRoomイベントのコールバックをお待ちください
let onExitRoom = function (reason) {
  console.log(`onExitRoom, reason: ${reason}`);
};
trtcCloud.exitRoom();
trtcCloud.on('onExitRoom', onExitRoom);
:::
</dx-codeblock>

>! Electronプログラムで複数の音声ビデオSDKを同時に統合した場合は、`onExitRoom`を受信してコールバックしてから、その他の音声ビデオSDKを起動してください。そうしない場合は、ハード上の占有問題が生じることがあります。
