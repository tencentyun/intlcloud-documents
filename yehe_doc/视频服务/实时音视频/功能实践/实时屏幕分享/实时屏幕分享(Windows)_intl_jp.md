Tencent Cloud TRTCは画面共有機能をサポートし、Windowsプラットフォームにおける画面共有はビッグストリーム共有とサブストリーム共有の2つのスキームをサポートします。
- **サブストリーム共有**
TRTCでは、画面共有のための「サブストリーム（**substream**）」という1チャネルのアップストリームのビデオストリームを個別にスタートできます。サブストリーム共有は、キャスターがカメラ画面とスクリーン画面の両方を同時にアップロードします。これはTencentMeetingの使用スキームであり、`startScreenCapture` インターフェースを呼び出す場合に、`TRTCVideoStreamType`パラメータを`TRTCVideoStreamTypeSub `に指定して、このモードをイネーブルできます。このストリーム画面を閲覧するには専用の`startRemoteSubStreamView`インターフェースを使用する必要があります。

- **ビッグストリーム共有**
TRTCでは、通常、カメラが動くチャネルを「ビッグストリーム（**bigstream**）」といい、ビッグストリーム共有は、カメラチャネルを使用して画面を共有します。このモードでは、キャスターは、アップストリームのカメラ画面、もしくはアップストリームのスクリーン画面のいずれかのアップストリームのビデオストリームを1チャンネルのみ有し、両者は相互に排他的です。`startScreenCapture`インターフェースを呼び出す場合に、`TRTCVideoStreamType`パラメータを`TRTCVideoStreamTypeBig`に指定し、このモードをイネーブルできます。

## サポートするプラットフォーム

| iOS | Android | Mac OS | Windows | Electron|WeChat Mini Program | Chromeブラウザ|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003;  |  &#10003;  |   &#10003; |   &#10003; | &#10003;  | ×    |  &#10003; |

## 依存するAPI

| API機能 | C++バージョン |  C#バージョン | Electronバージョン |
|---------|---------|---------|---------|
|共有ターゲットの選択| [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a9d16af81b2ea2db7b91a8346add13393) | [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a2aabe079ed38fb5122be988434a81a92) | [selectScreenCaptureTarget](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#selectScreenCaptureTarget) |
|画面共有を開始| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a984f461eebe77819f40c4129fc5a71bb) | [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#adde6382876b0afab78bab89e8be8e254) | [startScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startScreenCapture) |
|画面共有の一時停止| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a0dcd89ed2e23706239db98b55dd806d4) | [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a448e432a91c092f80421d377425fb1bb) | [pauseScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pauseScreenCapture) |
|画面共有のリカバー| [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a9dc10db068b9d8c6a0fcb8b085359f33) | [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad1fc32927622168e9b3cbb3f70043450) | [resumeScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumeScreenCapture)|
|画面共有の終了| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a0e09090fe4281c0e78d8eb38496a8ed0) | [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad02093be5c603f66f356978169946a18) | [stopScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopScreenCapture) |


## 共有ターゲットの取得
`getScreenCaptureSources`を介して 共有可能なウィンドウのリストをリストアップでき、リストは出力パラメータ sourceInfoList を介して戻されます。
>? Windowsのデスクトップ画面もウィンドウの1つであり、デスクトップウィンドウ（Desktop）と呼ばれ、モニターが2台ある場合は、各モニターに対応するデスクトップウィンドウがあります。したがって、getScreenCaptureSourcesを介して返されるウィンドウリストにもDesktopウィンドウがあります。

sourceInfoListの各sourceInfoが共有可能なターゲットは、次のフィールドのように説明されます。

| フィールド | タイプ | 意味|
|-------|--------| ---------------|
| type |TRTCScreenCaptureSourceType| キャプチャソースタイプ。指定タイプはウィンドウまたはスクリーン|
| sourceId | HWND| ソースIDの収集<li>ウィンドウについては、当該フィールドにウィンドウのハンドル</li><li>を表示します。画面については、当該フィールドに画面ID</li>を表示します |
| sourceName| string | ウィンドウ名。画面である場合は Screen0 Screen1...を返します |
| thumbWidth| int32 | ウィンドウサムネイル幅 |
| thumbHeight| int32 | ウィンドウサムネイル高さ |
| thumbBGRA| buffer | ウィンドウサムネイルのバイナリーbuffer |
| iconWidth | int32 | ウィンドウアイコンの幅 |
| iconHeight| int32 | ウィンドウアイコンの高さ |
| iconBGRA | buffer | ウィンドウアイコンのバイナリーbuffer |

上述の情報に基づき、ユーザーの選択のために共有できるターゲットを一覧表示するシンプルなリストページを実現できます。

## 共有ターゲットの選択
TRTC SDK は3種の共有モードをサポートしており、`selectScreenCaptureTarget`を介して指定できます：

- **全画面の共有**：
全スクリーンウィンドウの共有であり、マルチモニター分割画面をサポートします。1つのsourceInfoList中のtypeに`TRTCScreenCaptureSourceTypeScreen`のsourceパラメータを指定し、captureRectを{ 0, 0, 0, 0 }に設定する必要があります。

- **指定領域の共有**：
スクリーンの特定領域の共有であり、ユーザーが領域の位置座標を決定する必要があります。1つのsourceInfoList中のtypeに`TRTCScreenCaptureSourceTypeScreen`のsourceパラメータを指定し、captureRectを{ 100, 100, 300, 300 }などの非NULLに設定する必要があります。

- **指定ウィンドウの共有**：
ターゲットウィンドウのコンテンツの共有であり、ユーザーが共有したいウィンドウを指定する必要があります。1つのsourceInfoList中のtypeに`TRTCScreenCaptureSourceTypeWindow`のsourceパラメータを指定し、captureRectを{ 0, 0, 0, 0 }に設定する必要があります。


>? 2つの追加パラメータ：
> - パラメータ captureMouse はマウスポインタをキャプチャするかどうかを指定するために使用されます。
> - パラメータhighlightWindow は共有するウィンドウを強調表示するかどうかを指定し、キャプチャされた画像に隠れた箇所がある場合、それを取り除くようユーザーに促します。この部分のUI特殊効果は、SDK内で実現されます。


## 画面共有の開始

 - 共有ターゲットを選択した後、`startScreenCapture`インターフェースを使用して画面共有を起動することができます。
 - 共有プロセスにおいても、`selectScreenCaptureTarget`を呼び出し、共有ターゲットを変更することができます。
 - `pauseScreenCapture` と `stopScreenCapture` の違いは、pauseはスクリーンコンテンツのキャプチャを停止し、その瞬間の画面を一時停止するため、resumeするまで最後の画面がリモート側に表示され続けます。

```C++
    /**
    * \brief 7.5 【画面共有】画面共有の起動
    * \param：rendHwnd - プレビュー画面をロードするHWND
    */
    void startScreenCapture(HWND rendHwnd);

    /**
    * \brief 7.6 【画面共有】画面共有の一時停止
    */
    void pauseScreenCapture();

    /**
    * \brief 7.7 【画面共有】画面共有のリカバー
    */
    void resumeScreenCapture();

    /**
    * \brief 7.8 【画面共有】画面共有の終了
    */
    void stopScreenCapture();
```

## 画質の設定
`setSubStreamEncoderParam`インターフェースを介して解像度、ビットレートとフレームレートを含む画面共有の画面品質を設定できます。推奨する参考値を以下に提示します。

| 解像度レベル | 解像度 | フレームレート | ビットレート |
|:-------------:|:---------:|:---------:| :---------: |
| 超高精細（HD+） | 1920 × 1080 | 10 | 800kbps |
|  高精細（HD） | 1280 × 720 | 10 | 600kbps |
| 標準（SD） | 960 × 720 | 10 | 400kbps |

## 画面共有の確認
- **Mac / Windows画面共有の確認**
  ルームにいるMac / Windowsユーザーが画面共有を起動し、サブストリームを介して共有を実行します。ルームにいるその他ユーザーはTRTCCloudDelegate中の[onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a15be39bb902bf917321b26701e961286)イベントを介してこの通知を受け取ります。
  画面共有を確認したいユーザーは[startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae029514645970e7d32470cf1c7aca716)インターフェースを介してリモートユーザーのサブストリーム画面のレンダリングを起動することができます。

- **Android / iOS画面共有の確認**
  ユーザーがAndroid / iOSを介して画面共有を実行する場合は、メインストリームを介して共有を実行します。ルームにいるその他ユーザーはTRTCCloudDelegateの中の[onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80)イベントを介してこの通知を受け取ります。
  画面共有を確認したいユーザーは[startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49)インターフェースを介してリモートユーザーのメインストリーム画面のレンダリングを起動することができます。

```C++
//サンプルコード：画面共有の画面を見る
void CTRTCCloudSDK::onUserSubStreamAvailable(const char * userId, bool available)
{
	    LINFO(L"onUserSubStreamAvailable userId[%s] available[%d]\n", UTF82Wide(userId).c_str(), available);
	   if (available)  {
	         startRemoteSubStreamView(userId, hWnd);
	   } else {
	         stopRemoteSubStreamView(userId);
	   }
}
```

## よくあるご質問
 **1つのルームで同時にいくつの画面を共有できますか。**
現在、1つのTRTCオーディオ・ビデオルームで共有できる画面は1つだけです。

 **ウィンドウの共有（SourceTypeWindow）を指定し、ウィンドウのサイズが変化した場合は、ビデオストリームの解像度も変化しますか。**
デフォルトでは、SDK内で共有ウィンドウのサイズに従ってエンコーディングパラメータを自動的に調整します。
解像度を固定する必要がある場合は、setSubStreamEncoderParamインターフェースを呼び出し画面共有のエンコーディングパラメータを設定するか、またはstartScreenCaptureを呼び出すときに、対応するエンコーディングパラメータを指定する必要があります。
