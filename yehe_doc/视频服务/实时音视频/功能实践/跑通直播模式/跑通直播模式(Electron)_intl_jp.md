## 適用ケース

TRTCは、4種類の異なる入室モードをサポートしています。このうち、ビデオ通話（VideoCall）および音声通話（VoiceCall）を総称して[通話モード](https://intl.cloud.tencent.com/document/product/647/36069)といい、ビデオ・インタラクティブストリーミング（Live）およびボイス・インタラクティブストリーミング（VoiceChatRoom）を総称してライブストリーミングモードといいます。
ライブストリーミングモードでのTRTCは、1つのルームで最大10万人の同時接続をサポートし、300ms未満のマイク接続遅延、1000ms未満の視聴遅延およびマイクのオン・オフのスムーズな切り替え技術を備えています。低レイテンシーILVB、10万人のインタラクティブ教室、ビデオ婚活、eラーニング、リモート研修、超大規模ミーティングなどのユースケースに適しています。

## 原理解析

TRTCクラウドサービスは、「インターフェースモジュール」および「プロキシモジュール」という2種類の異なるタイプのサーバーノードから構成されています。

-   **インターフェースモジュール**
    この種のノードは、最も良質の回線および高性能の機器を採用しており、エンドツーエンドの低遅延マイク接続通話の処理に優れますが、単位時間当たりの費用はやや高くなります
-   **プロキシモジュール**
    この種のノードは、通常の回線および性能も一般的な機器を採用しており、同時進行性の高いプルストリーミング再生のニーズの処理にすぐれ、単位当たりの費用はやや低くなります。

通話モードでは、TRTCルームのすべてのユーザーはインターフェースモジュールに分配されます。各ユーザーは「キャスター」に相当し、各ユーザーは随時発言でき（同時アップストリームの最大制限は30）、このためオンラインミーティングなどのユースケースに適していますが、1つのルームの人数制限は300人になります。

![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## サンプルコード

[Github](https://github.com/tencentyun/TRTCSDK/tree/master/Electron) にログインし、本ファイルに関連するサンプルコードを取得することができます。

## 操作手順

<span id="step1"></span>

### 手順1：公式ウェブサイトのSimpleDemoクイックスタートを試行する

まずドキュメント[ SimpleDemoクイックスタート(Electron)](https://intl.cloud.tencent.com/document/product/647/35089)をご覧いただき、ドキュメントのガイドに従って、提供されている公式SimpleDemoクイックスタートを実行してください。
SimpleDemoが順調に動作する場合は、プロジェクトにおいてElectronのインストール方法をお客様が把握していることを意味します。
- 反対に、 SimpleDemo の動作に問題がある場合は、Electronのダウンロード、インストールに問題があったことが考えられます。この場合はElectron の公式サイトの [インストールガイド](https://www.electronjs.org/docs/tutorial/installation) をご参照ください。

<span id="step2"></span>

### 手順2：お客様のプロジェクトにtrtc-electron-sdkを統合する

[手順1]](#step1) が正常に動作し、予想どおりの効果があった場合は、 Electron環境のインストール方法を把握していることを意味します。

- 弊社の公式Demoをベースとして二次開発を行うことができ、プロジェクトの初級段階がスムーズに進みます。
- 次のコマンドを実行して、既存のプロジェクトに`trtc-electron-sdk`をインストールすることもできます。
```bash
npm install trtc-electron-sdk --save
```

<span id="step3"></span>
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

<span id="step4"></span>
### 手順4：入室パラメータTRTCParamsを組み立てる

[enterRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#enterRoom) インターフェースを呼び出すとき、1つのキーパラメータ [TRTCParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html)を入力する必要があります。このパラメータに含まれる必須のフィールドは下表のとおりです。

| パラメータ     | タイプ   | 説明                                                         | サンプル                   |
| :------- | :----- | :----------------------------------------------------------- | :--------------------- |
| sdkAppId | 数字  | アプリケーションID。 [コンソール](https://console.cloud.tencent.com/trtc/app) >【アプリケーション管理】>【アプリケーション情報】にあります。 | 1400000123  |
| userId  | 文字列 | アルファベットの大文字、小文字（a-z、A-Z）、数字（0-9）、下線およびハイフンのみを許可。 | test_user_001 |
| userSig | 文字列 |  userId を基に userSigを計算できます。計算方法は[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166) をご参照ください。| eJyrVareCeYrSy1SslI... |
| roomId | 数字 | デフォルトでは文字列のタイプのルームナンバーをサポートしていません、文字列タイプのルームナンバーは入室速度に影響します。文字列タイプのルームナンバーをサポートする必要が確実にある場合は、 [チケットを提出](https://console.cloud.tencent.com/workorder/category) してご連絡ください。 | 29834 |

```
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
```

>! TRTCは、相互に干渉しないよう、2つの同じuserIdによる同時入室をサポートしていません。

<span id="step5"></span>

### 手順5：キャスター端末でのカメラのプレビューとマイク集音を起動する
1.  キャスター側で[startLocalPreview()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalPreview) を呼び出して、ローカルのカメラプレビューを起動します。SDKは、システムにカメラの使用権限をリクエストします。
2. キャスター側で`setLocalViewFillMode()`を呼び出して、ローカルビデオ画面の表示モードを設定することができます。
    -  `TRTCVideoFillMode.TRTCVideoFillMode_Fill`：塗りつぶしを意味し、画面は同じ比率で拡大およびトリミングできますが、黒い縁取りは付きません。
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fit`：適応を意味し、画面は同じ比率で縮小してスクリーンにフィットしてそのコンテンツを完全に表示しますが、黒い縁取りが付くことがあります。
3. キャスター側で[setVideoEncoderParam()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setVideoEncoderParam) インターフェースを呼び出すと、ローカルビデオのエンコードパラメータを設定できますが、そのパラメータはルームのその他ユーザーが視聴する画面の [画質](https://intl.cloud.tencent.com/document/product/647/35153)を決定します。
4.  キャスター側で[startLocalAudio()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalAudio) を呼び出して、マイクを起動すると、SDKはシステムにマイクの使用権限をリクエストします。


```
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
```

<span id="step6"></span>

### 手順6：キャスター端末により美顔エフェクトを設定する

1. キャスター側で[setBeautyStyle(style, beauty, white, ruddiness)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setBeautyStyle)を呼び出して、美顔効果をオンにすることができます
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


<span id="step7"></span>
### 手順7：キャスター端末からルームを新規作成し、プッシュを開始する

1.  キャスター側で[TRTCParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html)のフィールド`role`を **`TRTCRoleType.TRTCRoleAnchor`**に設定し、現在のユーザーのロールがキャスターであることを示します。
2.  キャスター側でenterRoom（）を呼び出すと、TRTCParamsパラメータフィールド`roomId`の値がルーム番号となるオーディオ・ビデオルームを作成し、`appScene`パラメータを指定することができます。
    -   `TRTCAppScene.TRTCAppSceneLIVE`：ビデオ・インタラクティブストリーミングは、スムーズなマイクのオン・オフをサポートしています。切り替え中に待機の必要がなく、キャスターの遅延は300ミリ秒未満です。10万人規模の視聴者の同時再生をサポートしつつ、再生遅延は1000ミリ秒に抑えます。ここでは、このモードを例として取り上げます。
    -   `TRTCAppScene.TRTCAppSceneVoiceChatRoom`：ボイス・インタラクティブストリーミングは、スムーズなマイクのオン・オフをサポートします。切り替え中に待機の必要がなく、キャスターの遅延は300ミリ秒未満です。10万人規模の視聴者の同時再生をサポートしつつ、再生遅延は1000ミリ秒に抑えます。 
    -   `TRTCAppScene`の詳細な説明については、[TRTCAppScene ](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCAppScene)をご参照ください。
3.  ルームの作成に成功すると、キャスター側はオーディオ・ビデオデータのエンコードと伝送プロセスを開始します。これと同時にSDKは、[onEnterRoom(result)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onEnterRoom)イベントにコールバックします。このうち、パラメータ `result` が0より大きいときは、入室成功を意味し、具体的な数値は入室してからの消費時間を示します。単位はミリ秒（ms）です； `result` が0より小さいときは、入室失敗を意味し、具体的な数値は入室失敗のエラーコードを示します。

```
let onEnterRoom = function (result) {
  if (result > 0) {
    console.log(`onEnterRoom、入室成功、 ${result} 秒`を使用);
  } else {
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
```

<span id="step8"></span>
### 手順8：視聴者が入室しライブストリーミングを視聴する

1.  視聴者側で[TRTCParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html)のフィールド`role`を**`TRTCRoleType.TRTCRoleAudience`**に設定し、現在のユーザーのロールが視聴者であることを示します。
1.  視聴者側で`enterRoom()`を呼び出すと、`TRTCParams`パラメータの`roomId`が示すオーディオ・ビデオルームに入室し、`appScene`パラメータを指定することができます。
    -  `TRTCAppScene.TRTCAppSceneLIVE`：ビデオ・インタラクティブストリーミング。
    -  `TRTCAppScene.TRTCAppSceneVoiceChatRoom`：ボイス・インタラクティブストリーミング。
2. キャスター画面の視聴：
    -  視聴者側がキャスターの`userId`をあらかじめ知っている場合、入室に成功した後、キャスターの`userId`をそのまま使用して[startRemoteView(userId, view)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView)を呼び出すと、キャスター画面が表示されます。
    -  視聴者側がキャスターの`userId`を知らない場合、入室に成功した後、[onUserVideoAvailable()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserVideoAvailable)イベント通知を受信します。コールバックで取得したキャスターの`userId`を使用して[startRemoteView(userId, view)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView)を呼び出すと、キャスター画面が表示されます。

```
<div id="video-container"></div>
<script>
  const videoContainer = document.querySelector('#video-container');
  const roomId = 29834;
  // 入室コールバック。このコールバックは、入室に成功したときにトリガーされます。
  let onEnterRoom = function(result) {
    if (result > 0) {
      console.log(`onEnterRoom、入室成功、 ${result} 秒`を使用);
    } else {
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
    } else {
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
```

<span id="step9"></span>
### 手順9：視聴者とキャスターとをマイク接続する

1.  視聴者側で[switchRole(TRTCRoleType.TRTCRoleAnchor)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#switchRole)を呼び出して、ロールをキャスター(`TRTCRoleType.TRTCRoleAnchor`)に切り替えます。
2.  視聴者側で[startLocalPreview()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalPreview)を呼び出すと、ローカル画面を開くことができます。
3. 視聴者側で[startLocalAudio()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalAudio)を呼び出して、マイクの集音を起動します。

```
trtcCloud.switchRole(TRTCRoleType.TRTCRoleAnchor);
trtcCloud.startLocalAudio();
trtcCloud.startLocalPreview(frontCamera, view);

//サンプルコード：視聴者マイク・オフ
trtcCloud.switchRole(TRTCRoleType.TRTCRoleAudience);
trtcCloud.stopLocalAudio();
trtcCloud.stopLocalPreview();
```


<span id="step10"></span>
### 手順10：キャスター間でルーム間マイク接続PKを行う

TRTCでは、異なるオーディオ・ビデオルームにいる2人のキャスターが当初のライブストリーミングルームを退出しない場合にも、「ルーム間通話」機能によってマイク接続通話機能をプルし、「ルーム間マイク接続PK」を行うことができます。

1.  キャスターAが[connectOtherRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#connectOtherRoom)インターフェースを呼び出します。インターフェースパラメータは現在、JSON形式を採用しており、キャスターBの`roomId`と` userId`を `{" roomId "：978、" userId "：" userB "}`という形式のパラメータに組み立て、それらをインターフェース関数に渡す必要があります。
2. ルームを跨ぐことに成功すると、キャスターAは[onConnectOtherRoom(userId, errCode, errMsg)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onConnectOtherRoom)イベントのコールバックを受信します。これと同時に、2つのライブストリーミングルームにいるすべてのユーザーが、[onUserVideoAvailable()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserVideoAvailable) と[onUserAudioAvailable()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserAudioAvailable)のイベント通知を受信します。
    例えば、ルーム「001」のキャスターAがルーム「002」のキャスターBと`connectOtherRoom()`を介してルーム間通話をする場合、ルーム「001」のユーザーはキャスターBの`onUserVideoAvailable(B, true)`コールバックと`onUserAudioAvailable(B, true)`コールバックを受信します。ルーム「002」のユーザーはキャスターAの`onUserVideoAvailable(A, true)`コールバックと`onUserAudioAvailable(A, true)`コールバックを受信します。
3.  2つのルームのユーザーは、[startRemoteView(userId, view)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView)を呼び出すことにより、もう一方のルームにいるキャスターの画面を表示することができ、音声は自動的に再生されます。
![](https://main.qcloudimg.com/raw/bffa420102bb31dee6f76d7f08a16e4f.png)
```
//サンプルコード：ルーム間マイク接続PK
let onConnectOtherRoom = function(userId, errCode, errMsg) {
  if(errCode === 0) {
    console.log(`キャスターの${userId}ルームとの接続に成功しました`);
  } else {
    console.warn(`他のキャスターのルームとの接続に失敗しました：${errMsg}`);
  }
};

const paramJson = '{"roomId": "978","userId": "userB"}';
trtcCloud.connectOtherRoom(paramJson);
trtcCloud.on('onConnectOtherRoom', onConnectOtherRoom); 
```

<span id="step11"></span>
### 手順11：現在のルームから退出する  

[exitRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#exitRoom)メソッドを呼び出してルームを退出する場合、SDKは退室するとき、カメラ、マイクなどのハードデバイスを停止またはリリースする必要があります。このため、退室動作は直ちに完了するものではなく、[onExitRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onExitRoom)のコールバックを受信した後に、実際の退室操作が完了します。

```
// 退室を呼び出した後は、onExitRoomイベントのコールバックをお待ちください
let onExitRoom = function (reason) {
  console.log(`onExitRoom, reason: ${reason}`);
};
trtcCloud.exitRoom();
trtcCloud.on('onExitRoom', onExitRoom);
```

>! Electronプログラムで複数の音声ビデオSDKを同時に統合した場合は、`onExitRoom`を受信してコールバックしてから、その他の音声ビデオSDKを起動してください。そうしない場合、ハード上の占有問題が生じることがあります。
