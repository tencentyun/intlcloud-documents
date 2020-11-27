Tencent Cloud TRTC は画面共有機能をサポートし、Windowsプラットフォームにおける画面共有はビッグストリーム共有とサブストリーム共有の2つのスキームをサポートします。
- **サブストリーム共有**
TRTC では、画面共有のための“サブストリーム（**substream**）”というビデオストリームを個別にスタートできます。サブストリーム共有は、ホストがカメラ画面とスクリーン画面の両方を同時にアップロードします。これはTencentMeetingの使用スキームであり、`startScreenCapture` インターフェースを呼び出す場合に、 `TRTCVideoStreamType` パラメータを`TRTCVideoStreamTypeSub `に指定して、このスキーマをイネーブルできます。このストリーム画面を閲覧するには専用の `startRemoteSubStreamView` インターフェースを使用する必要があります。

- **ビッグストリーム共有**
TRTC では、通常、カメラが動くチャネルを“ビッグストリーム（**bigstream**）”といい、ビッグストリーム共有は、カメラチャネルと画面を共有します。このスキーマでは、ホストがアップストリームのカメラ画面か、もしくはアップストリームのスクリーン画面という、アップストリームのビデオストリーム1つのみを有し、両者は相互に排他的です。`startScreenCapture` インターフェースを呼び出す場合に、`TRTCVideoStreamType` パラメータを `TRTCVideoStreamTypeBig`に指定し、このスキーマをイネーブルできます。

## サポートするプラットフォーム

| iOS | Android | Mac OS | Windows | Electron|WeChat Mini Program | Chrome ブラウザ|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003;  |  &#10003;  |   &#10003; |   &#10003; | &#10003;  | ×    |  &#10003; |

## 依存する API

| API 機能 | C++ バージョン |  C# バージョン | Electron バージョン | 
|---------|---------|---------|---------|
|共有ターゲットの選択| [selectScreenCaptureTarget](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa5c3c7ed12993c155de77fb43ba0cf3b) | [selectScreenCaptureTarget](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#a2aabe079ed38fb5122be988434a81a92) | [selectScreenCaptureTarget](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#selectScreenCaptureTarget) |
|画面共有の開始| [startScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af83efff2a1020580bcb0bb89a8ffe4b0) | [startScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#adde6382876b0afab78bab89e8be8e254) | [startScreenCapture](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startScreenCapture) |
|画面共有の一時停止| [pauseScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0dcd89ed2e23706239db98b55dd806d4) | [pauseScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#a448e432a91c092f80421d377425fb1bb) | [pauseScreenCapture](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#pauseScreenCapture) |
|画面共有のリカバー| [resumeScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a9dc10db068b9d8c6a0fcb8b085359f33) | [resumeScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#ad1fc32927622168e9b3cbb3f70043450) | [resumeScreenCapture](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#resumeScreenCapture)|
|画面共有の終了| [stopScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0e09090fe4281c0e78d8eb38496a8ed0) | [stopScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#ad02093be5c603f66f356978169946a18) | [stopScreenCapture](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopScreenCapture) |


## 共有ターゲットの取得
 `getScreenCaptureSources`を介して 共有可能なウィンドウのリストをリストアップでき、リストは出力パラメータ sourceInfoList を介して戻されます。
>? Windows のデスクトップスクリーンもウィンドウの1つであり、デスクトップウィンドウ（Desktop）と呼ばれ、モニターが2台ある場合は、各モニターに対応するデスクトップウィンドウがあります。したがって、getScreenCaptureSources を介して戻されるウィンドウリストにもDesktop ウィンドウがあります。

sourceInfoList の各 sourceInfo が共有可能なターゲットは、次のフィールドのように記述されます。

| フィールド | タイプ | 意味|
|-------|--------| ---------------|
| type |TRTCScreenCaptureSourceType| キャプチャソースタイプ、指定タイプはウィンドウまたはスクリーン|
| sourceId | HWND| キャプチャソース ID<li>ウィンドウの場合、このフィールドはウィンドウハンドルを示します</li><li>スクリーンの場合、このフィールドはスクリーン IDを示します</li> |
| sourceName| string | ウィンドウ名、画面である場合は Screen0 Screen1...に戻ります |
| thumbWidth| int32 | ウィンドウサムネイル幅 | 
| thumbHeight| int32 | ウィンドウサムネイル高さ |
| thumbBGRA| buffer | ウィンドウサムネイルのバイナリー buffer |
| iconWidth | int32 | ウィンドウアイコンの幅 |
| iconHeight| int32 | ウィンドウアイコンの高さ |
| iconBGRA | buffer | ウィンドウアイコンのバイナリー buffer |

上述の情報に基づき、ユーザーの選択のために共有できるターゲットを一覧表示するシンプルなリストページを実現できます。

## 共有ターゲットの選択
TRTC SDK は3種の共有スキーマをサポートしており、 `selectScreenCaptureTarget`を介して指定できます：

- **全画面の共有**：
全スクリーンウィンドウの共有であり、マルチモニター分割画面をサポートします。1つのsourceInfoList 中の type が `TRTCScreenCaptureSourceTypeScreen` の source パラメータを指定し、 captureRect を { 0, 0, 0, 0 }に設定する必要があります。

- **指定領域の共有**：
スクリーンの特定領域の共有であり、ユーザーが領域の位置座標を決定する必要があります。1つの sourceInfoList 中の type が `TRTCScreenCaptureSourceTypeScreen` の source パラメータを指定し、 captureRect を{100、100、300、300}などの非 NULLに設定する必要があります。

- **指定ウィンドウの共有**：
ターゲットウィンドウのコンテンツの共有であり、ユーザーが共有したいウィンドウを指定する必要があります。1つの sourceInfoList 中の type が `TRTCScreenCaptureSourceTypeWindow`の source パラメータを指定し、 captureRectを { 0, 0, 0, 0 }に設定する必要があります。


>? 2つの追加パラメータ：
> - パラメータ captureMouse はマウスポインタをキャプチャするかどうかを指定するために使用されます。
> - パラメータ highlightWindow は共有するウィンドウを強調表示するかどうかを指定し、キャプチャされた画像がブロックされた場合にオクルージョンを移動するようユーザーに促すために使用されます。この部分のUI特殊効果は、SDK内で実現されます。


## 開始画面の共有

 - 共有ターゲットを選択した後、 `startScreenCapture` インターフェースを使用して画面共有を起動することができます。
 - 共有プロセスにおいても、 `selectScreenCaptureTarget` を呼び出し、共有ターゲットを変更することができます。
 - `pauseScreenCapture` と  `stopScreenCapture` の違いは、pauseはスクリーンコンテンツのキャプチャを停止し、その瞬間のスクリーンパッドを一時停止するため、resumeするまで最後の画面がリモート側に表示され続けます。
 
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
`setSubStreamEncoderParam` インターフェースを介して解像度、ビットレートとフレームレートを含む画面共有の画面品質を設定できます。推奨する参考値を以下に提示します：

| シャープネスレベル | 解像度 | フレームレート | ビットレート | 
|:-------------:|:---------:|:---------:| :---------: | 
| 超高精細（HD+） | 1920 × 1080 | 10 | 800kbps |
|  高精細（HD） | 1280 × 720 | 10 | 600kbps |
| 標準（SD） | 960 × 720 | 10 | 400kbps |

## 画面共有を見る
- ** Mac / Windows 画面共有を見る**
  ルームにいる Mac / Windows ユーザーが画面共有を起動し、サブストリームを介して共有を実行します。ルームにいるその他ユーザーはTRTCCloudDelegate 中の [onUserSubStreamAvailable](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__csharp.html#a15be39bb902bf917321b26701e961286) イベントを介してこの通知を受け取ります。
  画面共有を見たいユーザーは[startRemoteSubStreamView](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#ae029514645970e7d32470cf1c7aca716) インターフェースを介してリモートユーザーのサブストリーム画面のレンダリングを起動することができます。

- ** Android / iOS 画面共有を見る**
  ユーザーが Android / iOS を介して画面共有を実行する場合は、メインストリームを介して共有を実行することができます。ルームにいるその他ユーザーは TRTCCloudDelegate 中の [onUserVideoAvailable](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) イベントを介してこの通知を受け取ります。
  画面共有を見たいユーザーは[startRemoteView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) インターフェースを介してリモートユーザーのメインストリーム画面のレンダリングを起動することができます。



```C++
//サンプルコード：画面共有を見る、の画面
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
 **1つのルームで同時にいくつの画面を共有できますか？**
現在、1つの TRTC オーディオ・ビデオルームで共有できる画面は1つだけです。

 **ウィンドウの共有（SourceTypeWindow）を指定し、ウィンドウのサイズが変化した場合は、ビデオストリームの解像度も変化しますか？**
デフォルトでは、SDK内で共有ウィンドウのサイズに従ってエンコーディングパラメータを自動的に調整します。
解像度を固定する必要がある場合は、setSubStreamEncoderParam インターフェースを呼び出し画面共有のエンコーディングパラメータを設定するか、または startScreenCaptureを呼び出すときに、対応するエンコーディングパラメータを指定する必要があります。
