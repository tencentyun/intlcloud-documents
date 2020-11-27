Tencent Cloud TRTC は画面共有機能をサポートし、Macプラットフォームにおける画面共有はビッグストリーム共有とサブストリーム共有の2つのスキームをサポートします。
- **サブストリーム共有**
TRTC では、画面共有のための“サブストリーム（**substream**）”というビデオストリームを個別にスタートできます。サブストリーム共有は、ホストがカメラ画面とスクリーン画面の両方を同時にアップロードします。これはTencentMeetingの使用スキームであり、`startScreenCapture` インターフェースを呼び出す場合に、 `TRTCVideoStreamType` パラメータを`TRTCVideoStreamTypeSub `に指定して、このスキーマをイネーブルできます。このストリーム画面を閲覧するには専用の `startRemoteSubStreamView` インターフェースを使用する必要があります。

- **ビッグストリーム共有**
TRTC では、通常、カメラが動くチャネルを“ビッグストリーム（**bigstream**）”といい、ビッグストリーム共有は、カメラチャネルと画面を共有します。このスキーマでは、ホストがアップストリームのカメラ画面か、もしくはアップストリームのスクリーン画面という、アップストリームのビデオストリーム1つのみを有し、両者は相互に排他的です。`startScreenCapture` インターフェースを呼び出す場合に、`TRTCVideoStreamType` パラメータを `TRTCVideoStreamTypeBig`に指定し、このスキーマをイネーブルできます。

## サポートするプラットフォーム

| iOS | Android | Mac OS | Windows |Electron| WeChat Mini Program | Chrome ブラウザ|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003; |  &#10003; |  &#10003;  |&#10003;  |   &#10003;  |   ×   |  &#10003;  |

## 共有ターゲットの取得
[getScreenCaptureSourcesWithThumbnailSize](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa8e5286e1035b64b7d2bf8fadd721123)を介して 共有可能なウィンドウのリストをリストアップでき、共有可能な各ターゲットはいずれも`TRTCScreenCaptureSourceInfo`オブジェクトです。

Mac OS内 のデスクトップスクリーンも共有可能なターゲットであり、通常の Mac ウィンドウのtype は `TRTCScreenCaptureSourceTypeWindow`であり、デスクトップスクリーンの type は `TRTCScreenCaptureSourceTypeScreen`です。

typeに加え、各 `TRTCScreenCaptureSourceInfo` には次のフィールド情報があります。

| フィールド | タイプ | 意味|
|:-------:|:--------:| :---------------:|
| type |TRTCScreenCaptureSourceType| キャプチャソースタイプ:指定タイプはウィンドウまたはスクリーン|
| sourceId | NSString| キャプチャソース ID：ウィンドウの場合、このフィールドはウィンドウハンドルを示します；<br>スクリーンの場合、このフィールドはスクリーン IDを示します |
| sourceName| NSString | ウィンドウ名、画面である場合は、Screen0 Screen1...に戻ります |
| extInfo| NSDictionary | 共有ウィンドウの追加情報 | 
| thumbnail| NSImage | ウィンドウサムネイル |
| icon | NSImage | ウィンドウアイコン |

上述のこれらの情報があれば、ユーザーの選択のために共有できるターゲットを一覧表示するシンプルなリストページを実現できます。

## 共有ターゲットの選択
TRTC SDK は3種の共有スキーマをサポートしており、 [selectScreenCaptureTarget](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a01ead6fb3106ea266caa922f5901bf18) を介して指定できます。

- **全画面の共有**：
全スクリーンウィンドウの共有であり、マルチモニター分割画面をサポートします。1つのtype が `TRTCScreenCaptureSourceTypeScreen` の screenSource パラメータを指定し、rectを{ 0, 0, 0, 0 }に設定する必要があります。

- **指定領域の共有**：
スクリーンの特定領域の共有であり、ユーザーが領域の位置座標を決定する必要があります。1つのtype が `TRTCScreenCaptureSourceTypeScreen` の screenSource パラメータを指定し、captureRect を{100、100、300、300}などの非 NULLに設定する必要があります。

- **指定ウィンドウの共有**：
ターゲットウィンドウのコンテンツを共有するには、ユーザーが共有したいウィンドウを指定する必要があります。1つの type が `TRTCScreenCaptureSourceTypeWindow`の screenSource パラメータを指定し、 captureRectを { 0, 0, 0, 0 }に設定する必要があります。


>? 2つの追加パラメータ：
> - パラメータ capturesCursor はマウスポインタをキャプチャするかどうかを指定するために使用されます。
> - パラメータ highlight は共有するウィンドウを強調表示するかどうかを指定し、キャプチャされた画像がブロックされた場合にオクルージョンを移動するようユーザーに促すために使用されます。この部分のUI特殊効果は、SDK内で実現されます


## 開始画面の共有

 - 共有ターゲットを選定した後、 [startScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97)インターフェースを使用して画面共有を起動することができます。
 - 2つの関数 [pauseScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a6f536bcc3df21b38885809d840698280) と  [stopScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa8ea0235691fc9cde0a64833249230bb) の違いは、pauseはスクリーンコンテンツのキャプチャを停止し、その瞬間のスクリーンパッドを一時停止するため、 [resumeScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af257a8fb6969fe908ca68a039e6dba15)まで最後の画面がリモート側に表示され続けます。
 
```Objective-C
 /**
 *  7.6 【画面共有】画面共有の起動
 *  @param view レンダリングウィジェットが配置される親ウィジェット
 */
- (void)startScreenCapture:(NSView *)view;

/**
 *  7.7 【画面共有】画面キャプチャの停止
 *  @return 0：成功 <0:失敗
 */
- (int)stopScreenCapture;

/**
 *  7.8 【画面共有】画面共有の一時停止
 *  @return 0：成功 <0:失敗
 */
- (int)pauseScreenCapture;

/**
 *  7.9 【画面共有】画面共有のリカバー
 *
 *  @return 0：成功 <0:失敗
 */
- (int)resumeScreenCapture;
```

## 画質の設定
[setSubStreamEncoderParam](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#abc0f3cd5c320d0e65163bd07c3c0a735)インターフェースを介して解像度、コードレートとフレームレートを含む画面共有の画面品質を設定できます。推奨する参考値を以下に提示します：

| シャープネスレベル | 解像度 | フレームレート | ビットレート | 
|:-------------:|:---------:|:---------:| :---------: | 
| 超高精細（HD+） | 1920 × 1080 | 10 | 800kbps |
|  高精細（HD） | 1280 × 720 | 10 | 600kbps |
| 標準（SD） | 960 × 720 | 10 | 400kbps |

## 画面共有を見る
- ** Mac / Windows 画面共有を見る**
  ルームにいる Mac / Windows ユーザーが画面共有を起動し、サブストリームを介して共有を実行します。ルームにいるその他ユーザーはTRTCCloudDelegate 中の [onUserSubStreamAvailable](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#ac45fb0751f7dbd2466a35c8828c9911b) イベントを介してこの通知を受け取ります。
  画面共有を見たいユーザーは[startRemoteSubStreamView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a68d048ccd0d018995e33e9e714e14474) インターフェースを介してリモートユーザーのサブストリーム画面のレンダリングを起動することができます。

- **鑑賞 Android / iOS 画面の共有**
  ユーザーが Android / iOS を介して画面共有を実行する場合は、メインストリームを介して共有を実行することができます。ルームにいるその他ユーザーは TRTCCloudDelegate 中の [onUserVideoAvailable](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) イベントを介してこの通知を受け取ります。
  画面共有を見たいユーザーは [startRemoteView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) インターフェースを介してリモートユーザーのメインストリーム画面のレンダリングを起動することができます。



```Objective-C
//サンプルコード：画面共有を見る、の画面

- (void)onUserSubStreamAvailable:(NSString *)userId available:(BOOL)available {
    if (available) {
        [self.trtcCloud startRemoteSubStreamView:userId view:self.capturePreviewWindow.contentView];
    } else {
        [self.trtcCloud stopRemoteSubStreamView:userId];
    }
}
```

## よくあるご質問
**1つのルームで同時にいくつの画面を共有できますか？**
現在、1つの TRTC オーディオ・ビデオルームで共有できる画面は1つだけです。

**ウィンドウの共有（SourceTypeWindow）を指定し、ウィンドウのサイズが変化した場合は、ビデオストリームの解像度も変化しますか？**
デフォルトでは、SDK内で共有ウィンドウのサイズに従ってエンコーディングパラメータを自動的に調整します。
解像度を固定する必要がある場合は、setSubStreamEncoderParam インターフェースを呼び出し画面共有のエンコーディングパラメータを設定するか、または startScreenCaptureを呼び出すときに、対応するエンコーディングパラメータを指定する必要があります。
