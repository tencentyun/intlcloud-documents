このドキュメントでは、主に画面共有の使用方法を紹介します。現在、TRTCオーディオビデオルームで使用できる画面共有は1つだけです。

Windowsプラットフォームでの画面共有は、ビッグストリーム共有とサブストリーム共有の2つのスキームをサポートます。

- **サブストリーム共有**
TRTCでは、画面共有のための「サブストリーム(**substream**)」という1チャネルのアップリンクのビデオストリームを個別にスタートできます。サブストリーム共有は、キャスターがカメラ画面とスクリーン画面の両方を同時にアップロードします。これはTencentMeetingの使用スキームであり、`startScreenCapture`インターフェースを呼び出す場合に、`TRTCVideoStreamType`パラメータを`TRTCVideoStreamTypeSub `に指定して、このモードを有効にすることができます。

- **ビッグストリーム共有**
TRTCでは、通常、カメラが動くチャネルを「ビッグストリーム(**bigstream**)」といい、ビッグストリーム共有は、カメラチャネルを使用して画面を共有します。このモードでは、キャスターは、アップストリームのカメラ画面、もしくはアップストリームのスクリーン画面のいずれかのアップストリームのビデオストリームを1チャンネルのみ有し、両者は相互に排他的です。`startScreenCapture`インターフェースを呼び出す場合に、`TRTCVideoStreamType`パラメータを`TRTCVideoStreamTypeBig`に指定し、このモードをイネーブルできます。

## 依存するAPI

| API機能 | C++バージョン |  C#バージョン | Electronバージョン |
|---------|---------|---------|---------|
|共有ターゲットの選択| selectScreenCaptureTarget | [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a2aabe079ed38fb5122be988434a81a92) | [selectScreenCaptureTarget](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#selectScreenCaptureTarget) |
|画面共有を開始| startScreenCapture | [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#adde6382876b0afab78bab89e8be8e254) | [startScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startScreenCapture) |
|画面共有の一時停止| pauseScreenCapture | [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a448e432a91c092f80421d377425fb1bb) | [pauseScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pauseScreenCapture) |
|画面共有のリカバー| resumeScreenCapture | [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad1fc32927622168e9b3cbb3f70043450) | [resumeScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumeScreenCapture)|
|画面共有の終了| stopScreenCapture | [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad02093be5c603f66f356978169946a18) | [stopScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopScreenCapture) |


## 共有ターゲットの取得
`getScreenCaptureSources`を介して 共有可能なウィンドウのリストをリストアップでき、リストは出力パラメータ sourceInfoList を介して戻されます。
>? Windowsのデスクトップ画面もウィンドウの1つであり、デスクトップウィンドウ（Desktop）と呼ばれ、モニターが2台ある場合は、各モニターに対応するデスクトップウィンドウがあります。したがって、getScreenCaptureSourcesを介して返されるウィンドウリストにもDesktopウィンドウがあります。

取得したウィンドウ情報に基づき、ユーザーの選択のために共有できるターゲットを一覧表示するシンプルなリストページを実現できます：

## 画面共有の開始

 - 共有ターゲットを選択した後、`startScreenCapture`インターフェースを使用して画面共有を起動することができます。
 - 共有プロセスにおいても、`selectScreenCaptureTarget`を呼び出し、共有ターゲットを変更することができます。
 - `pauseScreenCapture` と `stopScreenCapture` の違いは、pauseはスクリーンコンテンツのキャプチャを停止し、その瞬間の画面を一時停止するため、resumeするまで最後の画面がリモート側に表示され続けます。


## 画質の設定
`setSubStreamEncoderParam`インターフェースを介して解像度、ビットレートとフレームレートを含む画面共有の画面品質を設定できます。推奨する参考値を以下に提示します：

| 解像度レベル | 解像度 | フレームレート | ビットレート |
|:-------------:|:---------:|:---------:| :---------: |
| 超高精細（HD+） | 1920 × 1080 | 10 | 800kbps |
|  高精細（HD） | 1280 × 720 | 10 | 600kbps |
| 標準（SD） | 960 × 720 | 10 | 400kbps |

## 画面共有の確認
  ルームにいるユーザーが画面共有を起動し、サブストリームを介して共有を実行します。ルームにいるその他のユーザーは、TRTCCloudDelegate内の[onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudCallback__cplusplus.html)イベントを介してこの通知を受け取ります。
  画面共有を視聴したいユーザーは[startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html)インターフェースを介してリモートユーザーのサブストリーム画面のレンダリングを起動することができます。

```C++
//サンプルコード：画面共有の画面を見る
void CTRTCCloudSDK::onUserSubStreamAvailable(const char * userId, bool available) {
    LINFO(L"onUserSubStreamAvailable userId[%s] available[%d]\n", UTF82Wide(userId).c_str(), available);
    liteav::ITRTCCloud* trtc_cloud_ = getTRTCShareInstance();
    if (available)  {
        trtc_cloud_->startRemoteView(userId, liteav::TRTCVideoStreamTypeSub, hWnd);
    }else{
        trtc_cloud_->stopRemoteView(userId, liteav::TRTCVideoStreamTypeSub);
    }
}
```

## よくあるご質問
#### 1つのルームで同時に複数の画面を共有できますか？
現在、1つのTRTCオーディオ・ビデオルームで共有できる画面は1つだけです。

#### ウィンドウの共有(SourceTypeWindow)を指定し、ウィンドウのサイズが変化した場合は、ビデオストリームの解像度も変化しますか？
デフォルトでは、SDK内で共有ウィンドウのサイズに従ってエンコーディングパラメータを自動的に調整します。
解像度を固定する必要がある場合は、setSubStreamEncoderParamインターフェースを呼び出し画面共有のエンコーディングパラメータを設定するか、またはstartScreenCaptureを呼び出すときに、対応するエンコーディングパラメータを指定してください。
