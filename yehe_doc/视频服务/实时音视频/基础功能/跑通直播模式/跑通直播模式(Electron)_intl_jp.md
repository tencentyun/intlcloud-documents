## ユースケース

TRTCは、4種類の異なる入室モードをサポートしています。このうち、ビデオ通話（VideoCall）および音声通話（VoiceCall）を総称して[通話モード](https://intl.cloud.tencent.com/document/product/647/36069)といい、ビデオ・インタラクティブストリーミング（Live）およびボイス・インタラクティブストリーミング（VoiceChatRoom）を総称してライブストリーミングモードといいます。
ライブストリーミングモードでのTRTCは、1つのルームで最大10万人の同時接続をサポートし、300ms未満のマイク接続遅延、1000ms未満の視聴遅延およびマイクのオン・オフのスムーズな切り替え技術を備えています。低レイテンシーインタラクティブストリーム、10万人のインタラクティブ教室、ビデオ婚活、eラーニング、リモート研修、超大規模ミーティングなどのユースケースに適しています。

## 原理解析

TRTCクラウドサービスは、「インターフェースモジュール」および「プロキシモジュール」という2種類の異なるタイプのサーバーノードから構成されています。

-   **インターフェースモジュール**
    この種のノードは、最も良質の回線および高性能の機器を採用しており、エンドツーエンドの低遅延マイク接続通話の処理に優れています。
-   **プロキシモジュール**
    この種のノードは、通常の回線および性能も一般的な機器を採用しており、同時進行性の高いプルストリーミング再生ニーズの処理にすぐれています。

通話モードでは、TRTCルームのすべてのユーザーはインターフェースモジュールに割り当てられます。各ユーザーは「キャスター」に相当し、各ユーザーは随時発言でき（同時アップストリームの最大制限は50）、このためオンラインミーティングなどのユースケースに適していますが、1つのルームの人数制限は300人になります。

![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## サンプルコード

[Github](https://github.com/tencentyun/TRTCSDK/tree/master/Electron)にログインして、このドキュメントに関連したサンプルコードを取得することができます。

## 操作手順

[](id:step1)
### 手順1：公式ウェブサイトのSimpleDemoクイックスタートを試行する

初めにドキュメント[SimpleDemoクイックスタート(Electron)](https://intl.cloud.tencent.com/document/product/647/35089)を読み、ドキュメントのガイドに従って、提供されている公式SimpleDemoクイックスタートを実行してください。
SimpleDemoが順調に動作する場合は、プロジェクトにおいてElectronのインストール方法をお客様が把握していることを意味します。
- 反対に、 SimpleDemo の動作に問題がある場合は、Electronのダウンロード、インストールに問題があったことが考えられます。この場合はElectron の公式サイトの [インストールガイド](https://www.electronjs.org/docs/tutorial/installation) をご参照ください。

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

`trtc-electron-sdk`インスタンスの新規作成：

```javascript
import TRTCCloud from 'trtc-electron-sdk';
let trtcCloud = new TRTCCloud();
```

`onError`イベントの監視：

```javascript
// エラー通知は監視すべきもので、捕捉してユーザーに通知する必要があります
let onError = function(err) {
  console.error(err);
}
trtcCloud.on('onError',onError);
```

[](id:step4)
### 手順4：入室パラメータTRTCParamsを組み立てる

[enterRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enterRoom)インターフェースを呼び出すときはキーパラメータ[TRTCParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCParams.html)を入力する必要があります。このパラメータに含まれる入力必須フィールドは下表に示すとおりです。

| パラメータ     | タイプ   | 説明                                                         | サンプル                   |
| :------- | :----- | :----------------------------------------------------------- | :--------------------- |
| sdkAppId | 数字  | アプリケーションID。 [コンソール](https://console.cloud.tencent.com/trtc/app) >【アプリケーション管理】>【アプリケーション情報】にあります。 | 1400000123  |
| userId   | 文字列 | アルファベットの大文字、小文字（a-z、A-Z）、数字（0-9）、下線およびハイフンのみを許可。ビジネスの実際のアカウントシステムを組み合わせて設定することをお勧めします。 | test_user_001|
| userSig | 文字列 |  userIdを基にuserSigを計算できます。計算方法は[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。 | eJyrVareCeYrSy1SslI... |
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
param.role = TRTCRoleType.TRTCRoleAnchor; // ロールを「キャスター」に設定します
:::
</dx-codeblock>

>! 
>- TRTCは、2つの同じuserIdによる同時入室をサポートしていません。同時に入室した場合、相互に干渉します。
>- 各端末のユースケースappSceneについては、統一する必要があります。統一していない場合、想定外のトラブルが生じる恐れがあります。

[](id:step5)
### 手順5：キャスター端末でのカメラのプレビューとマイク集音を起動する
1.  キャスターは[startLocalPreview()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalPreview)を呼び出してローカルのカメラプレビューを起動することができます。SDKはカメラのアクセス許可をシステムにリクエストします。
2. キャスター側で`setLocalViewFillMode()`を呼び出して、ローカルビデオ画面の表示モードを設定することができます。
    -  `TRTCVideoFillMode.TRTCVideoFillMode_Fill`：塗りつぶしを意味し、画面は同じ比率で拡大およびトリミングできますが、黒い縁取りは付きません。
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fit`：適応を意味し、画面は同じ比率で縮小してスクリーンにフィットしてそのコンテンツを完全に表示しますが、黒い縁取りが付くことがあります。
3.  キャスターは[setVideoEncoderParam()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderParam)インターフェースを呼び出してローカルビデオのコーデックパラメータを設定することができます。このパラメータによりルームの他のユーザーが視聴する画面の[画質](https://intl.cloud.tencent.com/document/product/647/35153)が決定されます。
4.  キャスターは[startLocalAudio()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalAudio)を呼び出してマイクをオンにします。SDKはマイクの使用をシステムにリクエストします。


<dx-codeblock>
::: javascript javascript
//サンプルコード：ローカルのオーディオ・ビデオストリーミングの公開
trtcCloud.startLocalPreview(view);
trtcCloud.startLocalAudio();
trtcCloud.setLocalViewFillMode(TRTCVideoFillMode.TRTCVideoFillMode_Fill);

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

[](id:step6)
### 手順6：キャスター端末により美顔エフェクトを設定する

1.  キャスターは[setBeautyStyle(style, beauty, white, ruddiness)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBeautyStyle)を呼び出して、美顔エフェクトをオンにすることができます
2. パラメータの説明：
    -   style：美顔スタイルで、「スムース」または「ナチュラル」があります。スムースタイプは美肌補正がより強く、華やかなシーンに適しています。
        -   `TRTCBeautyStyle.TRTCBeautyStyleSmooth`: スムース。美女が登場するシーンに適しており、明らかな効果が感じられます。
        -   `TRTCBeautyStyle.TRTCBeautyStyleNature`: ナチュラル。美肌補正のアルゴリズムにより顔の細部の質感が保たれ、より自然な感じに仕上がります。
    -   beauty：美顔レベル。数値の範囲は0～9です。0はオフを表し、1～9まで数値が大きくなるほど効果が高くなります
    -   white：美白レベル。数値の範囲は0～9です。0はオフを表し、1～9まで数値が大きくなるほど効果が高くなります
    -   ruddiness：肌色補正レベル。数値の範囲は0～9です。0はオフを表し、1～9まで数値が大きくなるほど効果が高くなります。このパラメータは、Windowsプラットフォームではまだ有効ではありません

```javascript
// 美顔エフェクトをオン 
trtcCloud.setBeautyStyle(TRTCBeautyStyle.TRTCBeautyStyleNature, 5, 5, 5);
```


[](id:step7)
### 手順7：キャスター端末からルームを新規作成し、プッシュを開始する

1.  キャスターは[TRTCParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCParams.html)のフィールド`role`を**`TRTCRoleType.TRTCRoleAnchor`**に設定します。これは現在のユーザーのロールがキャスターであることを示します。
2.  キャスター側でenterRoom（）を呼び出すと、TRTCParamsパラメータフィールド`roomId`の値がルーム番号となるオーディオ・ビデオルームを作成し、`appScene`パラメータを指定することができます。
    -   `TRTCAppScene.TRTCAppSceneLIVE`：ビデオ・インタラクティブストリーミングは、スムーズなマイクのオン・オフをサポートしています。切り替え中に待機の必要がなく、キャスターの遅延は300ミリ秒未満です。10万人規模の視聴者の同時再生をサポートしつつ、再生遅延は1000ミリ秒に抑えます。ここでは、このモードを例として取り上げます。
    -   `TRTCAppScene.TRTCAppSceneVoiceChatRoom`：ボイス・インタラクティブストリーミングは、スムーズなマイクのオン・オフをサポートします。切り替え中に待機の必要がなく、キャスターの遅延は300ミリ秒未満です。10万人規模の視聴者の同時再生をサポートしつつ、再生遅延は1000ミリ秒に抑えます。 
    -   `TRTCAppScene`の詳細については、[TRTCAppScene ](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCAppScene)をご参照ください。
3.  ルームの作成が成功したら、キャスター側はオーディオ・ビデオデータのエンコードと伝送フローを開始します。それと同時に、SDKは[onEnterRoom(result)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onEnterRoom)イベントをコールバックします。パラメータ`result`が0より大きいときは入室成功を示し、具体的な数値は入室してからの消費時間になります。単位はミリ秒（ms）です。`result`が0より小さいときは入室失敗を示し、具体的な数値は入室失敗のエラーコードになります。

<dx-codeblock>
::: javascript javascript
let onEnterRoom = function (result) {
  if (result > 0) {
    console.log(`onEnterRoom、入室成功、${result}秒を使用`);
  }else{
    console.warn(`onEnterRoom: 入室失敗 ${result}`);
  }
};

trtcCloud.on('onEnterRoom', onEnterRoom);

let param = new TRTCParams();
param.sdkAppId = 1400000123;
param.roomId = 29834;
param.userId = 'test_user_001';
param.userSig = 'eJyrVareCeYrSy1SslI...';
param.role = TRTCRoleType.TRTCRoleAnchor;
trtcCloud.enterRoom(param, TRTCAppScene.TRTCAppSceneLIVE);
:::
</dx-codeblock>

[](id:step8)
### 手順8：視聴者が入室しライブストリーミングを視聴する

1.  視聴者側は[TRTCParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCParams.html)のフィールド`role`を**`TRTCRoleType.TRTCRoleAudience`**に設定します。これは現在のユーザーロールが視聴者であることを示します。
1.  視聴者側で`enterRoom()`を呼び出すと、`TRTCParams`パラメータの`roomId`が示すオーディオ・ビデオルームに入室し、`appScene`パラメータを指定することができます。
    -  `TRTCAppScene.TRTCAppSceneLIVE`：ビデオ・インタラクティブストリーミング。
    -  `TRTCAppScene.TRTCAppSceneVoiceChatRoom`：ボイス・インタラクティブストリーミング。
2. キャスター画面の視聴：
    -  視聴者側が事前にキャスターの`userId`を知っている場合、ルームに入室成功後に直ちにキャスターの`userId`を使用して[startRemoteView(userId, view)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView)を呼び出し、キャスターの画面を表示することができます。
    -  視聴者がキャスターの`userId`を知らない場合、視聴者は入室成功後に[onUserVideoAvailable()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserVideoAvailable)イベント通知を受け取り、コールバック中に取得するキャスターの`userId`を使用して[startRemoteView(userId, view)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView)を呼び出すと、キャスターの画面を表示することができます。

<dx-codeblock>
::: html html
<div id="video-container"></div>
<script>
  const videoContainer = document.querySelector('#video-container');
  const roomId = 29834;
  // 入室コールバック。このコールバックは、入室に成功したときにトリガーされます。
  let onEnterRoom = function(result) {
    if (result > 0) {
      console.log(`onEnterRoom、入室成功、${result}秒を使用`);
    }else{
      console.warn(`onEnterRoom: 入室失敗 ${result}`);
    }
  };
  // このコールバックは、キャスターがカメラプッシュのオン/オフを切り替えたときにトリガーされます
  let onUserVideoAvailable = function(userId, available) {
    if (available === 1) {
        let id = `${userId}-${roomId}-${TRTCVideoStreamType.TRTCVideoStreamTypeBig}`;
        let view = document.getElementById(id);
        if (!view) {
          view = document.createElement('div');
          view.id = id;
          videoContainer.appendChild(view);
        }
        trtcCloud.startRemoteView(userId, view);
        trtcCloud.setRemoteViewFillMode(userId, TRTCVideoFillMode.TRTCVideoFillMode_Fill);
    }else{
        let id = `${userId}-${roomId}-${TRTCVideoStreamType.TRTCVideoStreamTypeBig}`;
        let view = document.getElementById(id);
        if (view) {
          videoContainer.removeChild(view);
        }
    }
  };

  trtcCloud.on('onEnterRoom', onEnterRoom);
  trtcCloud.on('onUserVideoAvailable', onUserVideoAvailable);

  let param = new TRTCParams();
  param.sdkAppId = 1400000123;
  param.roomId = roomId;
  param.userId = 'test_user_001';
  param.userSig = 'eJyrVareCeYrSy1SslI...';
  param.role = TRTCRoleType.TRTCRoleAudience; // ロールを「視聴者」に設定します
  trtcCloud.enterRoom(param, TRTCAppScene.TRTCAppSceneLIVE);
</script>
:::
</dx-codeblock>

[](id:step9)
### 手順9：視聴者とキャスターとのマイク接続

1.  視聴者は[switchRole(TRTCRoleType.TRTCRoleAnchor)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#switchRole)を呼び出して、ロールをキャスター（`TRTCRoleType.TRTCRoleAnchor`）に切り替えます。
2.  視聴者は[startLocalPreview()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalPreview)を呼び出してローカル画面を起動することができます。
3.  視聴者は[startLocalAudio()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalAudio)を呼び出してマイクの集音をオンにします。

<dx-codeblock>
::: javascript javascript
//サンプルコード：視聴者マイク・オン
trtcCloud.switchRole(TRTCRoleType.TRTCRoleAnchor);
trtcCloud.startLocalAudio();
trtcCloud.startLocalPreview(frontCamera, view);

//サンプルコード：視聴者マイク・オフ
trtcCloud.switchRole(TRTCRoleType.TRTCRoleAudience);
trtcCloud.stopLocalAudio();
trtcCloud.stopLocalPreview();
:::
</dx-codeblock>


[](id:step10)
### 手順10：キャスター間でルーム間マイク接続PKを行う

TRTCでは、異なるオーディオ・ビデオルームにいる2人のキャスターが当初のライブストリーミングルームを退出しない場合にも、「ルーム間通話」機能によってマイク接続通話機能をプルし、「ルーム間マイク接続PK」を行うことができます。

1.  キャスターAは[connectOtherRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#connectOtherRoom)インターフェースを呼び出します。インターフェースのパラメータは現在JSONフォーマットを採用し、キャスターBの`roomId`と`userId`の形式に組み立てた`{"roomId": 978,"userId": "userB"}`のパラメータをインターフェース関数に渡す必要があります。
2.  ルームを跨ぐことに成功した後、キャスターAは[onConnectOtherRoom(userId, errCode, errMsg)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onConnectOtherRoom)イベントコールバックを受け取ります。同時に、2つのライブストリーミングルームのすべてのユーザーはいずれも[onUserVideoAvailable()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserVideoAvailable)および[onUserAudioAvailable()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserAudioAvailable)イベント通知を受け取ります。
    例えば、ルーム「001」のキャスターAがルーム「002」のキャスターBと`connectOtherRoom()`を介してルーム間通話をする場合、ルーム「001」のユーザーはキャスターBの`onUserVideoAvailable(B, true)`コールバックと`onUserAudioAvailable(B, true)`コールバックを受信します。ルーム「002」のユーザーはキャスターAの`onUserVideoAvailable(A, true)`コールバックと`onUserAudioAvailable(A, true)`コールバックを受信します。
3.  両方のルームのユーザーは[startRemoteView(userId, view)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView)を呼び出すと、もう一方のルームのキャスター画面を表示することができ、音声は自動再生されます。

![](https://main.qcloudimg.com/raw/bffa420102bb31dee6f76d7f08a16e4f.png)

<dx-codeblock>
::: javascript javascript
//サンプルコード：ルーム間マイク接続PK
let onConnectOtherRoom = function(userId, errCode, errMsg) {
  if(errCode === 0) {
    console.log(`キャスター${userId}のルームとの接続に成功しました`);
  }else{
    console.warn(`他のキャスターのルームとの接続に失敗しました：${errMsg}`);
  }
};

const paramJson = '{"roomId": "978","userId": "userB"}';
trtcCloud.connectOtherRoom(paramJson);
trtcCloud.on('onConnectOtherRoom', onConnectOtherRoom); 
:::
</dx-codeblock>

[](id:step11)
### 手順11：現在のルームから退出する  

[exitRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#exitRoom)メソッドを呼び出してルームを退出します。SDKは退出時にカメラやマイクなどのハードデバイスを停止またはリリースする必要があるため、退出動作は一瞬では完了しません。退出操作を完了するには[onExitRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onExitRoom)コールバックを受信する必要があります。

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

>! Electronプログラムで複数の音声ビデオSDKを同時に統合した場合は、`onExitRoom`コールバックを受信してから、その他の音声ビデオSDKを起動してください。そうしない場合、ハード上の占有問題が生じることがあります。
