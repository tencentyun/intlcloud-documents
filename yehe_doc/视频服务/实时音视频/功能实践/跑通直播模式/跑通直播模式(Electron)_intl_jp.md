## 適用ケース

TRTC は、4種類の異なる入室モードをサポートしています。このうち、ビデオ通話（VideoCall）および音声通話（VoiceCall）を総称して[通話モード](https://intl.cloud.tencent.com/document/product/647/36069)といい、ビデオ・インタラクティブストリーミング（Live）およびボイス・インタラクティブストリーミング（VoiceChatRoom）を総称してライブストリーミングモードモードといいます。
ライブストリーミングモードでの TRTCは、1つのルームで最大10万人が同時にオンラインでつながるのをサポートし、300ms未満のマイク接続の遅延、1000ms未満の視聴遅延、およびマイクのオン・オフのスムーズな切り替え技術を備えています。低遅延のILVB、10万人のインタラクティブな授業、ビデオ婚活、eラーニング、リモート研修、超大型会議などのユースケースに適用しています。

## 原理解析

TRTC クラウドサービスは、2種類の異なるタイプのサーバーノードから構成されており、それぞれ“インターフェースモジュール”および“プロキシモジュール”からなっています。

-   **インターフェースモジュール**
    この種のノードは、最も良質の回線および高性能の機器を採用しており、エンドツーエンドの低遅延マイク接続通話の処理に優れますが、単位時間当たりの費用はやや高くなります
-   **プロキシモジュール**
    この種のノードは、通常の回線および性能も一般的な機器を採用しており、同時進行性の高いプルストリーミング再生のニーズの処理にすぐれ、単位当たりの費用はやや低くなります。

通話モードでは、TRTCルームのすべてのユーザーはインターフェースモジュールに分配されます。各ユーザーは“キャスター”に相当し、各ユーザーは随時発言でき（同時アップストリームの最大制限は50）、このためオンラインミーティングなどのユースケースに適していますが、1つのルームの人数制限は300人になります。

![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## サンプルコード

 [Github](https://github.com/tencentyun/TRTCSDK/tree/master/Electron) にログインし、本ファイルに関連するサンプルコードを取得することができます。

##　操作手順

<span id="step1"> </span>
### 手順1：跑通正式サイト SimpleDemoのテスト

まずファイル [ SimpleDemoクイックスタート(Electron)](https://intl.cloud.tencent.com/document/product/647/35089)を読んで、ドキュメントのガイド、提供されている公式 SimpleDemoに従ってください。

SimpleDemo が順調に動作できる場合は、項目の中で Electron をインストールする方法を把握していることを意味します。

逆に、 SimpleDemo の動作に問題がある場合は、おそらく Electronのダウンロード、インストールに問題があったことが考えられます。この場合はElectron の公式サイトの [インストールガイド](https://www.electronjs.org/docs/tutorial/installation) を参照することができます。

<span id="step2"> </span>
### 手順2：項目のための trtc-electron-sdkの統合

[手順1](#step1) が正常に動作し、予想通りの効果があった場合は、 Electron 環境のインストール方法を把握していることを意味します。

私どもの正式Demoにおいて二次開発を行うことができます。項目の初級段階は比較的順調です。

以下のコマンドを実行することもできます。 `trtc-electron-sdk` を既存のプロジェクトにインストールすることもできます。

```bash
npm install trtc-electron-sdk --save
```

<span id="step3"> </span>
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
}
trtcCloud.on('onError',onError);
```

<span id="step4"></span>
### 手順4：入室パラメータ TRTCParamsの組み立て

[enterRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#enterRoom) インターフェースをコールするとき、一つのキーパラメータ [TRTCParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html)を入力する必要があります。このパラメータに含まれる必須のフィールドは下表のとおりです。

| パラメータ     | タイプ   | 説明                                                         | サンプル                   |
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
param.role = TRTCRoleType.TRTCRoleAnchor; // ロールを「キャスター」に設定します
```

> TRTC は同時に2つの同じ userIdで入室できません。そうしないと相互に干渉することになります。

### 手順5：キャスター端末でのカメラのプレビューおよびマイク集音の起動

1.キャスター側で[startLocalPreview()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalPreview) をコールして、ローカルのカメラプレビューを起動します。SDKは、システムにカメラの使用権限をリクエストします。
2.キャスター側で`setLocalViewFillMode()`をコールして、ローカルビデオ画面の表示モードを設定することができます。
    -  `TRTCVideoFillMode.TRTCVideoFillMode_Fill`：塗りつぶしを意味し、画面は同じ比率で拡大およびトリミングできますが、黒い縁取りは付きません。
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fit`：適応を意味し、画面は同じ比率で縮小してスクリーンにフィットしてそのコンテンツを完全に表示しますが、黒い縁取りが付くことがあります。
3.キャスター側で[setVideoEncoderParam()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setVideoEncoderParam) インターフェースをコールすると、ローカルビデオのエンコードパラメータを設定できますが、そのパラメータはルームのその他ユーザーが視聴する画面の [画質](https://intl.cloud.tencent.com/document/product/647/35153)を決定します。
4.キャスター側で[startLocalAudio()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalAudio) をコールして、マイクを起動すると、SDKはシステムにマイクの使用権限をリクエストします。

```javascript
//サンプルコード：ローカルのオーディオ・ビデオストリーミングの公開
trtcCloud.startLocalPreview(view);
trtcCloud.startLocalAudio();
trtcCloud.setLocalViewFillMode(TRTCVideoFillMode.TRTCVideoFillMode_Fill);

//ローカルビデオエンコードパラメータの設定
let encParam = new TRTCVideoEncParam();
encParam.videoResolution = TRTCVideoResolution.TRTCVideoResolution_640_360;
encParam.resMode = TRTCVideoResolutionMode.TRTCVideoResolutionModeLandscape;
encParam.videoFps = 25;
encParam.videoBitrate = 600;
encParam.enableAdjustRes = true;
trtcCloud.setVideoEncoderParam(encParam);
```

### 手順6：キャスター端末による美顔効果の設定

1.キャスター側で[setBeautyStyle(style, beauty, white, ruddiness)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setBeautyStyle)をコールして、美顔効果をオンにすることができます
2.パラメータの説明：
    -   style：美顔スタイルで、「スムース」または「ナチュラル」があります。スムースタイプは美肌補正がより強く、華やかなシーンに適しています。
        -   `TRTCBeautyStyle.TRTCBeautyStyleSmooth`: スムース。美女が登場するシーンに適しており、明らかな効果が感じられます。
        -   `TRTCBeautyStyle.TRTCBeautyStyleNature`: ナチュラル。美肌補正のアルゴリズムは顔の詳細な質感を維持し、より自然な感じになります。
    -   beauty：美顔レベル。数値の範囲は0～9です。0はオフを意味し、1～9まで数値が大きくなるほど効果が高くなります
    -   white：美白レベル。数値の範囲は0～9です。0はオフを意味し、1～9まで数値が大きくなるほど効果が高くなります
    -   ruddiness：肌色補正レベル。数値の範囲は0～9です。0はオフを意味し、1～9まで数値が大きくなるほど効果が高くなります。このパラメータは、Windowsプラットフォームではまだ有効ではありません

```javascript
// 美顔オン 
trtcCloud.setBeautyStyle(TRTCBeautyStyle.TRTCBeautyStyleNature, 5, 5, 5);
```



### 手順7：キャスター端末によるルーム新規作成およびプッシュの開始

1.キャスター側で[TRTCParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html)のフィールド`role`を **`TRTCRoleType.TRTCRoleAnchor`**に設定し、現在のユーザーのロールがキャスターであることを示します。
2.キャスター側でenterRoom（）をコールすると、TRTCParamsパラメータフィールド`roomId`の値がルーム番号となるオーディオ・ビデオルームを作成し、`appScene`パラメータを指定することができます。

    -   `TRTCAppScene.TRTCAppSceneLIVE`：ビデオ・インタラクティブストリーミングは、スムーズなマイクのオン・オフをサポートしています。切り替え中に待機の必要がなく、キャスターの遅延は300ミリ秒未満です。10万人規模の視聴者の同時再生をサポートしつつ、再生遅延は1000ミリ秒に抑えます。ここでは、このモードを例として取り上げます。
    -   `TRTCAppScene.TRTCAppSceneVoiceChatRoom`：ボイス・インタラクティブストリーミングは、スムーズなマイクのオン・オフをサポートします。切り替え中に待機の必要がなく、キャスターの遅延は300ミリ秒未満です。10万人規模の視聴者の同時再生をサポートしつつ、再生遅延は1000ミリ秒に抑えます。
    
     `TRTCAppScene` の詳細説明は、次をクリックして表示してください：[TRTCAppScene ](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCAppScene)。
3.ルームの作成に成功すると、キャスター側はオーディオ・ビデオデータのエンコードと伝送プロセスを開始します。これと同時にSDKは、[onEnterRoom(result)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onEnterRoom)イベントにコールバックします。このうち、パラメータ `result` が0より大きいときは、入室成功を意味し、具体的な数値は入室してからの消費時間を示します。単位はミリ秒（ms）です； `result` が0より小さいときは、入室失敗を意味し、具体的な数値は入室失敗のエラーコードを示します。


```javascript
let onEnterRoom = function (result) {
  if (result > 0) {
    console.log(`onEnterRoom，入室成功、 ${result} 秒`を使用);
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
```



### 手順8：視聴者端末が入室しライブストリーミングを視聴

1.視聴者側で[TRTCParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html)のフィールド`role`を**`TRTCRoleType.TRTCRoleAudience`**に設定し、現在のユーザーのロールが視聴者であることを示します。

1.視聴者側で`enterRoom()`をコールすると、`TRTCParams`パラメータの`roomId`が示すオーディオ・ビデオルームに入室し、`appScene`パラメータを指定することができます。

    -   `TRTCAppScene.TRTCAppSceneLIVE`：ビデオ・インタラクティブストリーミング。
    -   `TRTCAppScene.TRTCAppSceneVoiceChatRoom`：ボイス・インタラクティブストリーミング。

2. キャスターの画面の視聴：

    -   視聴者側がキャスターの`userId`をあらかじめ知っている場合、入室に成功した後、キャスターの`userId`をそのまま使用して[startRemoteView(userId, view)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView)をコールすると、キャスター画面が表示されます。
    -   視聴者側がキャスターの`userId`を知らない場合、入室に成功した後、[onUserVideoAvailable()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserVideoAvailable)イベント通知を受信します。コールバックで取得したキャスターの`userId`を使用して[startRemoteView(userId, view)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView)をコールすると、キャスター画面が表示されます。


```html
<div id="video-container"></div>
<script>
  const videoContainer = document.querySelector('#video-container');
  const roomId = 29834;
  // 入室コールバック。このコールバックは、入室に成功したときにトリガーされます。
  let onEnterRoom = function(result) {
    if (result > 0) {
      console.log(`onEnterRoom，入室成功、 ${result} 秒`を使用);
    }else{
      console.warn(`onEnterRoom: 入室失敗 ${result}`);
    }
  };
  // このコールバックは、キャスターがカメラのオン／オフを切り替えてプッシュしたときにトリガーされます
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
```

### 手順9：視聴者とキャスターとのマイク接続

1.視聴者側で[switchRole(TRTCRoleType.TRTCRoleAnchor)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#switchRole)をコールして、ロールをキャスター(`TRTCRoleType.TRTCRoleAnchor`)に切り替えます。
2.視聴者側で[startLocalPreview()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalPreview)をコールすると、ローカル画面を開くことができます。
3.視聴者側で[startLocalAudio()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalAudio)をコールして、マイクの集音を起動します。


```javascript
//サンプルコード：視聴者マイク・オン
trtcCloud.switchRole(TRTCRoleType.TRTCRoleAnchor);
trtcCloud.startLocalAudio();
trtcCloud.startLocalPreview(frontCamera, view);

//サンプルコード：視聴者マイク・オフ
trtcCloud.switchRole(TRTCRoleType.TRTCRoleAudience);
trtcCloud.stopLocalAudio();
trtcCloud.stopLocalPreview();
```



### 手順10：キャスター間でのルームを跨いだマイク接続PKの実施

TRTC ではの異なるオーディオ・ビデオルームのキャスターが2人、当初のライブストリーミングを退出しないというユースケースにおいて、“ルームを跨いだ通話”機能によってマイク接続通話機能をプルして“ルームを跨いだマイク接続PK”を実施することができます。

1.キャスターAが[connectOtherRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#connectOtherRoom)インターフェースを呼び出します。インターフェースパラメータは現在、JSON形式を採用しており、キャスターBの`{"roomId": 978,"userId": "userB"}`の形式に組み立てられた`roomId`と`userId`のパラメータをインターフェース関数に渡す必要があります。
2.ルームを跨ぐことに成功すると、キャスターAは[onConnectOtherRoom(userId, errCode, errMsg)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onConnectOtherRoom)イベントのコールバックを受信します。これと同時に、2つのライブストリーミングルームにいるすべてのユーザーが、[onUserVideoAvailable()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserVideoAvailable) と[onUserAudioAvailable()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserAudioAvailable)のイベント通知を受信します。
    例えば、ルーム「001」のキャスターAがルーム「002」のキャスターBと`connectOtherRoom()`を介してルーム間通話する場合、ルーム「001」のユーザーはキャスターBの`onUserVideoAvailable(B, true)`コールバックと`onUserAudioAvailable(B, true)`コールバックを受信します。ルーム「002」のユーザーはキャスターAの`onUserVideoAvailable(A, true)`コールバックと`onUserAudioAvailable(A, true)`コールバックを受信します。
3.2つのルームのユーザーは、[startRemoteView(userId, view)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView)をコールすることにより、もう一方のルームにいるキャスターの画面を表示することができ、音声は自動的に再生されます。

![キャスターのマイク接続シーケンス図](http://main.qcloudimg.com/raw/ac5b230340ebdab69998f95844fa61c1/%E4%B8%BB%E6%92%AD%E8%BF%9E%E9%BA%A6%E6%97%B6%E5%BA%8F%E5%9B%BE.png)

```javascript
//サンプルコード：ルームを跨いだマイク接続PK

let onConnectOtherRoom = function(userId, errCode, errMsg) {
  if(errCode === 0) {
    console.log(`キャスターの${userId}ルームとの接続に成功しました`);
  }else{
    console.warn(`他のキャスターのルームとの接続に失敗しました：${errMsg}`);
  }
};

const paramJson = '{"roomId": "978","userId": "userB"}';
trtcCloud.connectOtherRoom(paramJson);
trtcCloud.on('onConnectOtherRoom', onConnectOtherRoom); 
```

### ステップ11：現在のルームからの退出  

 [exitRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#exitRoom) メソッドをコールしてルームを退出する場合、SDK は退室するとき、カメラ、マイクなどのハードデバイスを停止またはリリースする必要があります。このため、退室動作は決して瞬時に完了するものではなく、 [onExitRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onExitRoom) のコールバックを受信してから、実際に退室操作を完了したとみなす必要があります。

```javascript
// 退室のコール後は、onExitRoom イベントのコールバックをお待ちください
let onExitRoom = function (reason) {
  console.log(`onExitRoom, reason: ${reason}`);
};
trtcCloud.exitRoom();
trtcCloud.on('onExitRoom', onExitRoom);

```

> Electron プログラムで複数の音声ビデオ SDKを同時に統合した場合は、`onExitRoom`を受信してコールバックしてから、その他の音声ビデオ SDKを起動してください。そうしない場合は、ハード上の占有問題が生じることがあります。
