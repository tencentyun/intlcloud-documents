## 内容紹介

携帯電話のライブストリーミングの一本調子の縦スクリーン体験とは異なります。Tencent Real-Time Communication（TRTC）は横型スクリーンおよび縦型スクリーンの2つのユースケースを両立させる必要があります。このため、多くの横型と縦型のスクリーンの処理ロジックを対応させる必要があります。ここでは主に以下のことを紹介します。
- 縦型スクリーンモードを実装する方法。例：WeChatのビデオ通話は典型的な縦型スクリーン体験モードです。
- 横型スクリーンモードを実装する方法。例：多人数ビデオミーティングApp（XYLink（小魚易連）など）は横型スクリーンモードを多く採用しています。
- ローカル画面及びリモート画面の回転方向およびフィルモードの制御をどのようにカスタマイズしますか？

![](https://main.qcloudimg.com/raw/1b4452db22edfe88646cd35888794d44.jpg)

## プラットフォームのサポート

| iOS | Android | Mac OS | Windows | Electron|WeChat Mini Program | Chrome ブラウザ|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| &#10003;  |  &#10003; |  &#10003; |  &#10003;  |&#10003;  |  ×  |  × |


## 縦型スクリーンモード
WeChatのビデオ通話に類似した体験モードを実現したい場合は、2つの作業が必要です。

**1.   App の UI インターフェースを縦型スクリーンに設定**
iOS プラットフォームは、 XCode の 【General】>【Deployment Info】>【Device Orientation】で直接設定することができます：
![](https://main.qcloudimg.com/raw/f7d62ed0954fd44f80d3983a0e6fb52d.png)

 Appdelegate の  `supportedInterfaceOrientationsForWindow` 方法を実現することで、同じ目的に到達することもできます：
``` ObjectiveC
- (UIInterfaceOrientationMask)application:(UIApplication *)application 
    supportedInterfaceOrientationsForWindow:(UIWindow *)window 
{

    return  UIInterfaceOrientationMaskPortrait ;

}
```

 Android プラットフォームでは、 activity の`screenOrientation` 属性を portraitに指定することで、そのインターフェースを縦型スクリーンモードに指定できます。
```xml
<activity android:name=".trtc.TRTCMainActivity"  android:launchMode="singleTask" android:windowSoftInputMode="adjustPan"
          android:screenOrientation="portrait" />
```

**2.  SDK で使用する縦型スクリーン解像度の設定**
 TRTCCloud を使用した setVideoEncoderParam インターフェースにビデオエンコードパラメータを設定する場合は、 resMode を `TRTCVideoResolutionModePortrait` に指定すればOKです。

iOSを例にとれば、サンプルコードは次のとおりです。
``` ObjectiveC
TRTCVideoEncParam* encParam = [TRTCVideoEncParam new];
encParam.videoResolution = TRTCVideoResolution_640_360;
encParam.videoBitrate = 600;
encParam.videoFps = 15;
encParam.resMode = TRTCVideoResolutionModePortrait; //解像度モードを縦型スクリーンモードに設定

[trtc setVideoEncoderParam: encParam];
```

## 横型スクリーンモード

Appに横型スクリーン体験を希望する場合は、実施する必要がある作業は縦型スクリーンモードのものと類似していますが、第一手順及び第二手順のパラメータに該当する調整だけでOKです。
特に第二手順では、 TRTCVideoEncParam の resModeを `TRTCVideoResolutionModeLandscape` （Android プラットフォームは：TRTC_VIDEO_RESOLUTION_MODE_LANDSCAPE）に指定する必要があります。

## カスタマイズ制御

TRTC SDK自身が大量に提供したインターフェース関数は、ローカルおよびリモートの画面の回転方向およびフィルモードをコントロールできます。

| インターフェース関数 | 機能作用 |  備考説明 |  
|---------|---------| ----- |
| setLocalViewRotation | ローカルのプレビュー画面の時計回りの回転角度| 時計回りの90度、180度、270度の三方向の回転のサポート  | 
| setLocalViewFillMode | ローカルプレビュー画面のフィルモード | トリミングか黒枠を残すか|
| setRemoteViewRotation | リモートビデオ画面の時計回りの回転角度 | 時計回りの90度、180度、270度の三方向への回転のサポート  |
| setRemoteViewFillMode | リモートビデオ画面のフィルモード | トリミングか黒枠を残すか|
| setVideoEncoderRotation | エンコーダーを設定して出力した画面の時計回りの回転角度 | 時計回りの角度90度、180度、270度の三方向の回転のサポート|

![](https://main.qcloudimg.com/raw/f965d6d603f95862d73525469637b437.jpg)


## GSensorMode
画面の回転が録画および CDN Relayed live streamingの各種附属問題に影響することを考慮すると、TRTC SDK は簡単な重力センサーの自己適応機能のみを提供しているだけなので、 TRTCCloud の `setGSensorMode`  インターフェースによって起動することができます。

この機能は、現在180度の上下回転の自己適応をサポートしているだけです。すなわち、ユーザー自身の携帯電話が上下180度逆さまになる場合は、相手が見る画面の向きが変わらない（90度回転または270度回転にはまだ適応していません）ように維持します。この自己適応はエンコーダーの方向調整を基に調整して実現したものであり、そのため録画したビデオ、およびミニプログラムやH5のWebサイトに表示されるビデオ画面も当初の方向を変えないまま維持します。

>!重力センサーの自己適応のもう一つの実現案は、各フレームのビデオ情報ごとに現在のビデオの重力方向を対応させることです。その後、リモートユーザーの元でレンダリングの方向を自己適応して調整します。しかしこの方法は追加でトランスコードリソースを導入しないと、録画したビデオの向きを希望するビデオの向きに一致させるという課題を克服できないことから、推奨していません。





