ここでは主に、キャスターが自分のオーディオビデオストリーミングを公開する方法についてご説明します。いわゆる「公開」とは、マイクとカメラをオンにして、自分の音声やビデオをルーム内にいる他のユーザーに聞かせたり、見せたりすることです。

![](https://qcloudimg.tencent-cloud.cn/raw/3f49218df6a0cc1a106f9a61c23fdb98.png)
## 呼び出しガイド

[](id:step1)
### ステップ1：前のステップの完了
ドキュメント[SDKのプロジェクトへのインポート](https://intl.cloud.tencent.com/document/product/647/35097)を参照し、SDKのインポートと設定を完了してください。

[](id:step2)
### ステップ2：カメラのプレビューを開く
**startLocalPreview**インターフェースを呼び出すと、カメラのプレビューを開くことができます。このとき、SDKはシステムにカメラの使用権限を申請し、ユーザーは承認を受けることでカメラのキャプチャ処理を開始することができます。

ローカル画面のレンダリングパラメータを設定したい場合は、**setLocalRenderParams**インターフェースを呼び出して、ローカルプレビューのレンダリングパラメータを設定することで行えます。プレビューを有効にしてからプレビューのパラメータを設定すると画面が飛んでしまうことを防ぐため、プレビューのパラメータを設定する必要がある場合は、プレビューを有効にする前にこのコマンドを呼び出すことをお勧めします。

```javascript
// ローカル画面のプレビューモードの設定：左右のイメージを有効にし、画面をフィルモードに設定します
import TRTCCloud, { 
	TRTCRenderParams, TRTCVideoRotation,
	TRTCVideoFillMode, TRTCVideoMirrorType
} from 'trtc-electron-sdk';

const param = new TRTCRenderParams(
	TRTCVideoRotation.TRTCVideoRotation0,
	TRTCVideoFillMode.TRTCVideoFillMode_Fill,
	TRTCVideoMirrorType.TRTCVideoMirrorType_Auto
);
const rtcCloud = new TRTCCloud();
rtcCloud.setLocalRenderParams(param);
const cameraVideoDom = document.querySelector('.camera-dom');
rtcCloud.startLocalPreview(cameraVideoDom);
```

[](id:step3)
### ステップ3：マイクキャプチャを有効にする
**startLocalAudio**を呼び出すことによって、マイクのキャプチャを有効にすることができます。このインターフェースでは、`quality`パラメータを介してキャプチャモードを決定する必要があります。このパラメータの名前はqualityですが、品質が高いほど良いというわけではなく、ビジネスシナリオによって選択すべき最適なパラメータがあります（このパラメータのより正確な意味はsceneです）。

- **SPEECH**
このモードのSDKオーディオモジュールは、音声信号をブラッシュアップし、周囲のノイズを可能な限り除去することに重点を置いています。また、このモードのオーディオデータは、質の悪いネットワークに対しても最高の耐性が得られるため、「ビデオ通話」や「オンラインミーティング」といった音声通信に焦点を当てたシナリオに特に適しています。
- **MUSIC**
このモードのSDKは、高い音声処理帯域幅とステレオモードを使用してキャプチャの品質を最大限に高めながら、オーディオのDSP処理モジュールを可能な限り弱いレベルに調整して音質を最大限に高めています。そのためこのモードは、「音楽ライブストリーミング」のシナリオ、特にキャスターがプロ用サウンドカードを使用して音楽ライブを行っているシナリオに適しています。
- **DEFAULT**
このモードのSDKは、インテリジェントな認識アルゴリズムが現在の環境を識別し、最適な処理モードを選択することができます。ただし、どんなに優れた認識アルゴリズムでも不正確な場合はあります。自社製品のポジショニングがはっきりしている場合は、音声通信に特化したSPEECHと音楽の音質に特化したMUSICのうちどちらかを選択することをお勧めします。

```javascript
import { TRTCAudioQuality } from 'trtc-electron-sdk';
// マイクキャプチャをオンにして、現在のシナリオを音声モード（高いノイズ抑制能力と脆弱なネットワーク耐性）に設定します
rtcCloud.startLocalAudio(TRTCAudioQuality.TRTCAudioQualitySpeech);

// マイクキャプチャをオンにして、現在のシナリオを音楽モード（高忠実度のキャプチャ、低音質損失、プロ用サウンドカードとの使用を推奨）に設定します
rtcCloud.startLocalAudio(TRTCAudioQuality.TRTCAudioQualityMusic);
```

[](id:step4)
### ステップ4：TRTCルームへの入室
ドキュメント[入室](https://intl.cloud.tencent.com/document/product/647/48049)をご参照のうえ、現在のユーザーをTRTCルームに入室させます。SDKはルームにいる他のユーザーに対し自分のオーディオストリームの公開を開始します。

>! もちろん、入室(enterRoom)後にカメラプレビューやマイクキャプチャを開始することもできますが、ライブストリーミングシナリオでは、まずキャスターにマイクテストや美顔のエフェクト調整の時間を与える必要があるので、入室前にカメラとマイクを先に開始することがより一般的な方法です。

```javascript
import { TRTCParams, TRTCRoleType, TRTCAppScene } from 'trtc-electron-sdk';

// TRTC入室パラメータを組み立てる場合、TRTCParamsの各フィールドをご自分のパラメータに置き換えてください
// Please replace each field in TRTCParams with your own parameters
const param = new TRTCParams();
params.sdkAppId = 1400000123;  // Please replace with your own SDKAppID
params.userId = "denny";       // Please replace with your own userid  
params.roomId = 123321;        // Please replace with your own room number
params.userSig = "xxx";        // Please replace with your own userSig
params.role = TRTCRoleType.TRTCRoleAnchor;

// シナリオが「オンラインライブストリーミング」の場合、ユースケースをTRTC_APP_SCENE_LIVEに設定してください
// If your application scenario is a video call between several people, please use "TRTC_APP_SCENE_LIVE"
rtcCloud.enterRoom(param, TRTCAppScene.TRTCAppSceneLIVE);
```

