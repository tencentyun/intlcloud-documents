ここでは主に、ルーム内の他のユーザーのオーディオビデオストリーミングをサブスクリプションする方法、すなわち他のユーザーのオーディオとビデオを再生する方法についてご説明します。便宜上、これ以降は「ルーム内にいる他のユーザー」を「リモートユーザー」と総称します。
![](https://qcloudimg.tencent-cloud.cn/raw/c8ae41656c97fe546b9c4b0b857b0746.png)

## 呼び出しガイド

[](id:step1)
### ステップ1：前のステップの完了
ドキュメント[SDKのプロジェクトへのインポート](https://intl.cloud.tencent.com/document/product/647/35097)を参照し、SDKのインポートを完了してください。

[](id:step2)
### ステップ2：サブスクリプションモードの設定（必須ではありません）
TRTCCloudの**setDefaultStreamRecvMode**インターフェースを呼び出すことでサブスクリプションモードを設定することができます。TRTCは、2つのサブスクリプションモードを提供しています。
- 自動サブスクリプション：SDKは、お客様側で追加の操作をしなくても、自動的にリモートユーザーの音声を再生します。これはSDKのデフォルトの動作です。
- 手動サブスクリプション：SDKは、自動的にリモートユーザーの音声をプルして再生しないため、手動で**muteRemoteAudio(userId, false)**を呼び出して音声を再生させる必要があります。
>! setDefaultStreamRecvModeを呼び出さなくても、SDKのデフォルトの動作は自動サブスクリプションである点にご注意ください。ただし、手動サブスクリプションに設定したい場合は、**setDefaultStreamRecvModeはenterRoomの前に呼び出した場合にのみ有効であることにご注意ください。**

[](id:step3)
### ステップ3：TRTCルームへの入室
ドキュメント[入室](https://intl.cloud.tencent.com/document/product/647/48049)をご参照のうえ、現在のユーザーをTRTCルームに入室させます。入室に成功した場合にのみ、他のユーザーのオーディオビデオストリーミングをサブスクリプションすることができます。

[](id:step4)
### ステップ4：オーディオストリームの再生
インターフェースmuteRemoteAudio("denny"，true)を呼び出すことでリモートユーザーdennyの音声をミュートでき、その後、インターフェースmuteRemoteAudio('denny'，false)を呼び出すことでミュートを解除できます。

```javascript
import TRTCCloud from 'trtc-electron-sdk';
const rtcCloud = new TRTCCloud();

// Reference https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteRemoteAudio
// Mute user with id denny
rtcCloud.muteRemoteAudio('denny', true);
// Unmute user with id denny
rtcCloud.muteRemoteAudio('denny', false);
```

[](id:step5)
### ステップ5：ビデオストリームの再生

#### 1. 再生の開始と停止(startRemoteView + stopRemoteView)
インターフェースstartRemoteViewを呼び出すことで、リモートユーザーのビデオ画面を再生することができます。ただし、ユーザーのビデオ画面のレンダリングウィジェットとして使用するviewオブジェクトをSDKに渡した場合に限ります。

startRemoteViewの最初のパラメータはリモートユーザーのuserId、2番目のパラメータはリモートユーザーのストリームタイプ、3番目のパラメータは渡す必要のあるviewオブジェクトです。そのうち2番目のパラメータstreamType（ストリームタイプ）には、次の3つのオプション値があります。
- **TRTCVideoStreamTypeBig**：ユーザーのメインチャネル画面です。通常、ユーザーのカメラ画面を送信するために使用します。
- **TRTCVideoStreamTypeSub**：ユーザーのサブチャネル画面です。通常、ユーザー画面と共有している画面を送信するために使用します。
- **TRTCVideoStreamTypeSmall**：ユーザーの低解像度小画面です。これは、メインチャネルと相対するもので、リモートユーザーが「デュアルチャネルエンコーディング(enableEncSmallVideoStream)」を有効にした場合にのみ、そのユーザーの低解像度画面を再生することができるようになります。また、メインチャネル画面と低解像度小画面のうち、どちらか一方しか選択できません。

stopRemoteViewインターフェースを呼び出すと、特定のリモートユーザーのビデオ再生を停止することができます。また、stopAllRemoteViewインターフェースを呼び出すと、すべてのリモートユーザーのビデオ再生を停止することもできます。

```javascript
// https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteViewをご参照ください

import TRTCCloud, { TRTCVideoStreamType } from 'trtc-electron-sdk';

const cameraView = document.querySelector('.user-dom');
const screenView = document.querySelector('.screen-dom');
const rtcCloud = new TRTCCloud();
// dennyのカメラ画面の再生（「メインチャネル画面」と呼びます）
rtcCloud.startRemoteView('denny', cameraView, TRTCVideoStreamType.TRTCVideoStreamTypeBig);
// dennyの画面共有画面の再生（「サブチャネル画面」と呼びます）
rtcCloud.startRemoteView('denny', screenView, TRTCVideoStreamType.TRTCVideoStreamTypeSub);
// dennyの低解像度画面の再生（メインチャネル画面と低解像度画面のうちどちらか一方のみ選択可能）
rtcCloud.startRemoteView('denny', cameraView, TRTCVideoStreamType.TRTCVideoStreamTypeSmall);
// dennyのカメラ画面の再生停止
rtcCloud.stopRemoteView('denny', TRTCVideoStreamType.TRTCVideoStreamTypeBig);
// すべてのビデオ画面の再生停止
rtcCloud.stopAllRemoteView();
```

#### 2. 再生パラメータの設定（setRemoteRenderParams）

setRemoteRenderParamsによって、画面のフィルモード、回転角度およびイメージモードを設定することができます。
- フィルモード：フィルとフィットがあり、どちらも画面の元のアスペクト比を維持できます。違いは黒い縁取りの有無です。
- 回転角度：0度、90度、180度および270度など、4つの回転角度が設定できます。
- イメージモード：画面の左右イメージモードのことです。

```javascript
// https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteRenderParamsをご参照ください
// リモートユーザーdennyのメインチャネル画面をフィルモードに設定し、左右のイメージモードを有効にします
import TRTCCloud, { 
  TRTCRenderParams, TRTCVideoStreamType, TRTCVideoRotation,
  TRTCVideoFillMode, TRTCVideoMirrorType
} from 'trtc-electron-sdk';

const param = new TTRTCRenderParams(
  TRTCVideoRotation.TRTCVideoRotation0,
  TRTCVideoFillMode.TRTCVideoFillMode_Fill,
  TRTCVideoMirrorType.TRTCVideoMirrorType_Enable
);
const rtcCloud = new TRTCCloud();
rtcCloud.setRemoteRenderParams('denny', TRTCVideoStreamType.TRTCVideoStreamTypeBig, param);
```

[](id:step6)
### ステップ6：ルーム内にいるリモートユーザーのオーディオビデオステータスの感知

[ステップ4](#step4)と[ステップ5](#step4)では、リモートユーザーに対して音声やビデオの再生を制御することができますが、十分な情報がないと以下の事項がわからなくなります。
- 現在、ルームにいるユーザーは誰か。
- ユーザーたちはカメラやマイクをオンにしているか。

この問題を解決するには、SDKからのイベントコールバックのいくつかを監視する必要があります。
- **オーディオステータス変更通知（onUserAudioAvailable）**
リモートユーザーがマイクをオンやオフした場合、onUserAudioAvailable(userId，boolean)を監視することで、このステータスの変化を感知することができます。

- **ビデオステータス変更通知（onUserVideoAvailable）**
リモートユーザーがカメラをオンやオフにした場合、onUserVideoAvailable(userId，boolean)を監視することで、このステータスの変化を感知することができます。
リモートユーザーが画面共有画面をオンやオフにした場合、onUserVideoAvailable(userId，boolean)を監視することで、このステータスの変化を感知することができます。

- **ユーザーの入退室通知（onRemoteUserEnter/LeaveRoom）**
リモートユーザーが現在のルームに入るとき、onRemoteUserEnterRoom(userId)によってそのユーザーのuserIdを感知することができます。リモートユーザーが現在のルームから退出するとき、onRemoteUserLeaveRoom(userId, reason)によってそのユーザーのuserIdとそのユーザーの退出した理由を感知することができます。
>! 正確に言うと、onRemoteUserEnter/LeaveRoomは、ロール(role)はキャスター(anchor)のユーザーの入退室通知のみを感知することができます。このような設計になっているのは、多数の視聴者(audience)がオンラインになっているルームでは人の出入りが頻繁であるため、ルームにいるすべてのユーザーが他のユーザーの入退出によって、「シグナリングストーム」攻撃を受けるのを避けるためです。

これらのイベントコールバックにより、どのユーザーがルームにいるか、彼らのカメラとマイクがオンになっているかどうかを把握することができます。次のサンプルコードをご参照ください。このサンプルコードでは、mCameraUserList、mMicrophoneUserListおよびmUserListを使用して次の事項を管理しています。
- ルーム内にいるユーザー（正確にはキャスター）は誰なのか
- そのうちカメラがオンになっているのはどのユーザーか
- そのうちマイクがオンになっているのはどのユーザーか

```javascript
import TRTCCloud from 'trtc-electron-sdk';
let openCameraUserList = [];
let openMicUserList = [];
let roomUserList = [];

function onUserVideoAvailable(userId, available) {
  if (available === 1) {
    openCameraUserList.push(userId);
  } else {
    openCameraUserList = openCameraUserList.filter((item) => item !== userId);
  }
}

function onUserAudioAvailable(userId, available) {
  if (available === 1) {
    openMicUserList.push(userId);
  } else {
    openMicUserList = openMicUserList.filter((item) => item !== userId);
  }
}

function onRemoteUserEnterRoom(userId) {
  roomUserList.push(userId);
}

function onRemoteUserLeaveRoom(userId, reason) {
  roomUserList = roomUserList.filter((item) => item !== userId);
}

const rtcCloud = new TRTCCloud();
rtcCloud.on('onUserVideoAvailable', onUserVideoAvailable);
rtcCloud.on('onUserAudioAvailable', onUserAudioAvailable);
rtcCloud.on('onRemoteUserEnterRoom', onRemoteUserEnterRoom);
rtcCloud.on('onRemoteUserLeaveRoom', onRemoteUserLeaveRoom);
```

## アドバンスガイドライン

### 同じ「ミュート」ですが、違いは何ですか。
ビジネスニーズを深掘りしていくに従い、「ミュート」には3つのタイプがあることがわかると思います。「ミュート」という名称は同じでも、技術的な原理はまったく異なります。
- **1つめ：再生側のオーディオストリームのサブスクリプションを停止する**
muteRemoteAudio("denny", true)関数を呼び出すと、リモートユーザーdennyの音声をもう再生したくないという意味になり、SDKはdennyのオーディオデータストリームのプルを停止します。このモードはトラフィックの節約になります。ただし、再度dennyの音声を再生したい場合は、SDKがオーディオデータをプルするプロセスを再起動する必要があるため、「ミュート」状態から「アンミュート」状態への復帰速度が遅くなります。

- **2つめ：再生音量をゼロに調整する**
ビジネスシナリオでミュートの切り替えに高速なレスポンス速度が求められる場合、setRemoteAudioVolume("denny", 0)によってリモートユーザーdennyの再生音量をゼロに設定することができます。このインターフェースはネットワーク操作を伴わないため、影響速度は非常に速くなります。

- **3つめ：リモートユーザーが自分でマイクをオフにする**
ここでご説明する操作はすべて再生側の操作で、これらの操作によって生じる効果は現在のユーザーにのみ有効です。例えば、muteRemoteAudio("denny", true)によってリモートユーザーdennyをミュートに設定しても、ルーム内の他のユーザーにはdennyの音声が聞こえます。
dennyを完全にミュートにするには、dennyのオーディオ公開の動作に影響を与える必要があります。これについては、次のドキュメント[オーディオビデオストリーミングの公開](https://intl.cloud.tencent.com/document/product/647/48050)で詳しくご説明しています。
