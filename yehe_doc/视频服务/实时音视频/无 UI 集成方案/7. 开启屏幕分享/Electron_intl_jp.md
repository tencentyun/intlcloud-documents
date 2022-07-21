このドキュメントでは、主に画面共有の使用方法を紹介します。現在、TRTCオーディオビデオルームで使用できる画面共有は1つだけです。

Electronプラットフォームでの画面共有は、ビッグストリーム共有とサブストリーム共有の2つのスキームをサポートます：

- **サブストリーム共有**
TRTCでは、画面共有のための「サブストリーム（**substream**）」という1チャネルのアップリンクのビデオストリームを個別にスタートできます。サブストリーム共有は、キャスターがカメラ画面とスクリーン画面の両方を同時にアップロードします。これはTencentMeetingの使用スキームであり、`startScreenCapture`インターフェースを呼び出す場合に、`TRTCVideoStreamType`パラメータを`TRTCVideoStreamTypeSub `に指定して、このモードを有効にすることができます。

- **ビッグストリーム共有**
TRTCでは、通常、カメラが動くチャネルを「ビッグストリーム（**bigstream**）」といい、ビッグストリーム共有は、カメラチャネルを使用して画面を共有します。このモードでは、キャスターは、アップストリームのカメラ画面、もしくはアップストリームのスクリーン画面のいずれかのアップストリームのビデオストリームを1チャンネルのみ有し、両者は相互に排他的です。`startScreenCapture`インターフェースを呼び出す場合に、`TRTCVideoStreamType`パラメータを`TRTCVideoStreamTypeBig`に指定し、このモードをイネーブルできます。

[](id:step1)
## 手順1：共有ターゲットの取得
`getScreenCaptureSources`を介して 共有可能なウィンドウのリストをリストアップでき、リストは出力パラメータ sourceInfoList を介して戻されます。
>? Electronのデスクトップ画面もウィンドウの1つであり、デスクトップウィンドウ（Desktop）と呼ばれ、モニターが2台ある場合は、各モニターに対応するデスクトップウィンドウがあります。したがって、getScreenCaptureSourcesを介して返されるウィンドウリストにもDesktopウィンドウがあります。

取得したウィンドウ情報に基づき、ユーザーの選択のために共有できるターゲットを一覧表示するシンプルなリストページを実現できます：


```javascript
import TRTCCloud from 'trtc-electron-sdk';
const rtcCloud = new TRTCCloud();
// https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCloud.html#getScreenCaptureSources
const screenList = rtcCloud.getScreenCaptureSources();
```

[](id:step2)
## 手順2：画面共有の開始
 - [selectScreenCaptureTarget](https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCloud.html#selectScreenCaptureTarget)を呼び出すことにより、共有ターゲットを選択できます。
 - 共有ターゲットを選択すると、[startScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCloud.html#startScreenCapture)インターフェースを使用して画面共有を開始できます。
 - 共有プロセスにおいても、[selectScreenCaptureTarget](https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCloud.html#selectScreenCaptureTarget)を呼び出すことにより、共有ターゲットを変更できます。
 - [pauseScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCloud.html#pauseScreenCapture)と[stopScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCloud.html#stopScreenCapture)の区別は、pauseが画面コンテンツのキャプチャを停止し、その時点の画像スペーサーを一時停止するため、リモート側に表示される画像は、resumeまで常に最後のフレームになります。

```javascript
import TRTCCloud, { 
	Rect, TRTCScreenCaptureProperty, TRTCVideoStreamType, TRTCVideoEncParam,
	TRTCVideoResolution, TRTCVideoResolutionMode
} from 'trtc-electron-sdk';
const rtcCloud = new TRTCCloud();
// https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getScreenCaptureSources
const screenList = rtcCloud.getScreenCaptureSources();
// https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/Rect.html
const captureRect = new Rect(0, 0, 0, 0);
// https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCScreenCaptureProperty.html
const property = new TRTCScreenCaptureProperty(
	true, true, true, 0, 0, false
);
if (screenList.length > 0) {
	rtcCloud.selectScreenCaptureTarget(screenList[0], captureRect, property)
}

const screenshareDom = document.querySelector('screen-dom');
// https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCVideoEncParam.html
const encParam = new TRTCVideoEncParam(
	TRTCVideoResolution.TRTCVideoResolution_1920_1080,
	TRTCVideoResolutionMode.TRTCVideoResolutionModeLandscape,
	15,
	2000,
	0,
	false
); 
rtcCloud.startScreenCapture(screenshareDom, TRTCVideoStreamType.TRTCVideoStreamTypeSub, encParam);
```

[](id:step3)
## 手順3：画面品質の設定
`startScreenCapture`インターフェースの3番目のパラメータ`encParam`を介して、　　　　　　　解像度、ビットレート、フレームレートを含む画面共有の画質を設定できます（[手順2](#step2)を参照）。以下の推奨基準値を提供します：

| 解像度レベル | 解像度 | フレームレート | ビットレート |
|:-------------:|:---------:|:---------:| :---------: |
| 超高精細（HD+） | 1920 × 1080 | 10 | 2000kbps |
|  高精細（HD） | 1280 × 720 | 10 | 600kbps |
| 標準（SD） | 960 × 720 | 10 | 400kbps |

[](id:step4)
## 手順4：画面共有の確認
ルームにいるユーザーが画面共有を起動し、サブストリームを介して共有を実行します。ルームにいるその他のユーザーは、[onUserSubStreamAvailable](https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCallback.html#event:onUserSubStreamAvailable)イベントを介してこの通知を受け取ります。
画面共有を視聴したいユーザーは[startRemoteView](https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCloud.html#startRemoteView)インターフェースを介してリモートユーザーのサブストリーム画面のレンダリングを起動することができます。

```javascript
import TRTCCloud, { 
	TRTCVideoStreamType
} from 'trtc-electron-sdk';
const rtcCloud = new TRTCCloud();

const remoteDom = document.querySelector('.remote-user');
function onUserSubStreamAvailable(userId, available) {
	if (available === 1) {
		rtcCloud.startRemoteView(userId, remoteDom, TRTCVideoStreamType.TRTCVideoStreamTypeSub);
	}else{
		rtcCloud.stopRemoteView(userId, TRTCVideoStreamType.TRTCVideoStreamTypeSub);
	}
}

rtcCloud.on('onUserSubStreamAvailable', onUserSubStreamAvailable);
```

## よくある質問
#### 1. 1つのルームで同時に複数の画面を共有できますか？
現在、1つのTRTCオーディオ・ビデオルームで共有できる画面は1つだけです。

#### 2. ウィンドウの共有(SourceTypeWindow)を指定し、ウィンドウのサイズが変化した場合は、ビデオストリームの解像度も変化しますか？
デフォルトでは、SDK内で共有ウィンドウのサイズに従ってエンコーディングパラメータを自動的に調整します。
解像度を固定する必要がある場合は、setSubStreamEncoderParamインターフェースを呼び出し画面共有のエンコーディングパラメータを設定するか、またはstartScreenCaptureを呼び出すときに、対応するエンコーディングパラメータを指定してください。
