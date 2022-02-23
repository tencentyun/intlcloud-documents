## 内容紹介

Tencent Real-Time Communication(TRTC)は、携帯電話のライブストリーミングのような縦画面による変化に乏しいユーザーエクスペリエンスとは異なり、横画面と縦画面という2つのユースケースを両立させることが必要です。このため、横画面と縦画面の処理ロジックを対応させる必要があります。ここでは主に、次の事項についてご説明します。
- 縦画面モードを実装する方法。例：WeChatのビデオ通話は典型的な縦画面体験モードです。
- 横画面モードを実装する方法。例えば、多人数インタラクティブオーディオビデオアプリ（XYLink（小魚易連）など）は多くの場合、横画面モードを採用しています。
- ローカル画面およびリモート画面の回転方向およびフィルモードをカスタマイズする方法。

![](https://main.qcloudimg.com/raw/1b4452db22edfe88646cd35888794d44.jpg)

## サポートプラットフォーム

| iOS | Android | Mac OS | Windows | Electron|web|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
| &#10003;  |  &#10003; |  &#10003; |  &#10003;  |&#10003;  |  × |


## 縦画面モード
WeChatのビデオ通話のような体験モードを実装したい場合は、2つの作業を行う必要があります。

[](id:step1)
### 1.  アプリのUIインターフェースを縦画面に設定する
<dx-tabs>
::: iOSプラットフォーム
XCodeの【General】>【Deployment Info】>【Device Orientation】で直接設定することができます。
![](https://main.qcloudimg.com/raw/f7d62ed0954fd44f80d3983a0e6fb52d.png)

Appdelegateの `supportedInterfaceOrientationsForWindow`メソッドを実装することにより、設定することもできます。

<dx-codeblock>
::: ObjectiveC ObjectiveC
- (UIInterfaceOrientationMask)application:(UIApplication *)application 
    supportedInterfaceOrientationsForWindow:(UIWindow *)window 
{

    return  UIInterfaceOrientationMaskPortrait ;

}
:::
</dx-codeblock>
>?CSDNに掲載されている、[iOSの縦横画面の回転およびその基本的な適用方法](https://blog.csdn.net/DreamcoffeeZS/article/details/79037207)という記事に、iOSプラットフォームで画面の向きに関する開発工程の一部を詳細に説明しています。
:::
::: Androidプラットフォーム
Androidプラットフォームでは、activityの`screenOrientation`属性をportraitに指定することで、そのインターフェースを縦画面モードに指定することができます。
<dx-codeblock>
::: xml 
<activity android:name=".trtc.TRTCMainActivity"  android:launchMode="singleTask" android:windowSoftInputMode="adjustPan"
          android:screenOrientation="portrait" />
:::
</dx-codeblock>
:::
</dx-tabs>

[](id:step2)
### 2. SDKで使用する縦画面解像度の設定
TRTCCloudを使用したsetVideoEncoderParamインターフェースにビデオコーデックパラメータを設定する場合は、resModeを`TRTCVideoResolutionModePortrait`に指定します。
サンプルコードは次のとおりです。[](id:example_code)
<dx-codeblock>
::: iOSプラットフォーム ObjectiveC
TRTCVideoEncParam* encParam = [TRTCVideoEncParam new];
encParam.videoResolution = TRTCVideoResolution_640_360;
encParam.videoBitrate = 600;
encParam.videoFps = 15;
encParam.resMode = TRTCVideoResolutionModePortrait; //解像度モードを縦画面モードに設定

[trtc setVideoEncoderParam: encParam];
:::
::: Androidプラットフォーム java
TRTCCloudDef.TRTCVideoEncParam encParam = new TRTCCloudDef.TRTCVideoEncParam();
encParam.videoResolution = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_640_360;
encParam.videoBitrate = 600;
encParam.videoFps = 15;
encParam.videoResolutionMode = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT; //解像度モードを縦画面モードに設定
trtc.setVideoEncoderParam(encParams);
:::
</dx-codeblock>

## 横画面モード
アプリに横画面のユーザーエクスペリエンスを提供する場合、縦画面モードと同様の作業を行う必要がありますが、手順1と2のパラメータに対応する調整を行うだけでOKです。
特に[手順2](#step2)では、TRTCVideoEncParamのresMode値は次のとおりとなります。
- iOSプラットフォームでは`TRTCVideoResolutionModeLandscape`と指定する必要があります。
- Androidプラットフォームでは`TRTC_VIDEO_RESOLUTION_MODE_LANDSCAPE`と指定する必要があります。

## カスタマイズ制御

TRTC SDKにより提供された多数のインターフェース関数は、ローカルおよびリモートの画面の回転方向およびフィルモードをコントロールできます。

| インターフェース関数 | 機能の役割 |  備考説明 |
|---------|---------| ----- |
| setLocalViewRotation | ローカルプレビュー画面での時計回りの回転角度| 時計回りの回転を90度、180度、270度という3方向でサポート  |
| setLocalViewFillMode | ローカルプレビュー画面のフィルモード | トリミングか黒枠を残すか|
| setRemoteViewRotation | リモートビデオ画面での時計回りの回転角度 | 時計回りの回転を90度、180度、270度という3方向でサポート  |
| setRemoteViewFillMode | リモートビデオ画面のフィルモード | トリミングか黒枠を残すか|
| setVideoEncoderRotation | エンコーダーを設定して出力した画面の時計回りの回転角度 | 時計回りの回転を90度、180度、270度という3方向でサポート|

![](https://main.qcloudimg.com/raw/f965d6d603f95862d73525469637b437.jpg)


## GSensorMode
画面の回転はレコーディングやCDN Relayed live streamingの調節に関するさまざまな項目に影響することを考慮すると、TRTC SDKはシンプルな重力センサーの自動調節機能を提供するだけであるので、TRTCCloudの`setGSensorMode`インターフェースを介してオンにすることができます。

この機能は、現在180度の上下回転の自動調節のみをサポートしています。つまり、ユーザー自身の携帯電話が上下180度逆さまになっている場合、相手が見る画面の向きが変わらないように維持します（90度または270度回転への適応はまだサポートしていません）。この自動調節はエンコーダーの方向調整に基づいて実装されているため、レコーディングしたビデオやH5端末に表示されるビデオ画面も、元の向きを維持することができます。

>!重力センサーの自動調節のもう一つの実装ソリューションでは、各フレームのビデオ情報ごとに現在のビデオの重力方向を対応させた上で、リモートユーザー側でレンダリング方向を自動調節します。ただしこのソリューションでは、レコーディングしたビデオの向きと求めるビデオの向きの一致を維持させるために、追加でトランスコードリソースを導入する必要があるためお勧めできません。
