Tencent CloudのTRTCは、iOSプラットフォームで2つの異なる画面共有ソリューションをサポートしています。
- **アプリ内共有**
現在のアプリの画面のみを共有できます。この特性をサポートするには、iOSのバージョン13以降のOSが必要です。現在のアプリ以外の画面コンテンツを共有できないため、高度なプライバシー保護が必要なシーンに適しています。
- **アプリケーション間共有**
AppleのReplaykitソリューションをベースとして、システム全体の画面コンテンツを共有できます。ただし、現在のアプリはExtension拡張コンポーネントを追加で提供する必要があるため、結合手順はアプリ内共有よりもやや多くなります。

>! 注意すべき点としては、モバイル端末版のTRTC SDKは、デスクトップ版のように、「サブストリームの共有」をサポートしていません。これは、iOSとAndroidシステムは、どちらもバックグラウンドで実行されているアプリに対し、カメラの使用権を制限しているからです。従って、サブストリームの共有をサポートする意義はあまりありません。

## サポートするプラットフォーム

| iOS | Android | Mac OS | Windows |Electron| WeChat Mini Program | Chromeブラウザ|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003; |  &#10003; |  &#10003;  |&#10003;  |   &#10003;  |   ×   |  &#10003;  |

## アプリ内共有

アプリ内共有のソリューションは非常にシンプルです。TRTC SDKが提供するインターフェース[startScreenCaptureInApp](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a16d30ca3f89863da2581ff3872bf31f0)を呼び出し、エンコードパラメータ`TRTCVideoEncParam`を渡すだけでOKです。このパラメータはnilに設定することができます。この場合、SDKは画面共有が開始される前のエンコードパラメータを引き続き使用します。

iOS画面共有に推奨されるエンコードパラメータは次のとおりです。

| パラメータ項目 | パラメータ名 | 通常の推奨値 | テキスト教育シナリオ |
|---------|---------|---------|-----|
| 解像度 | videoResolution | 1280 × 720 | 1920 × 1080 |
| フレームレート | videoFps | 10 FPS | 8 FPS |
| 最高ビットレート | videoBitrate| 1600 kbps | 2000 kbps |
| 解像度アダプティブ | enableAdjustRes | NO | NO |

- 画面共有されるコンテンツには通常、大幅な変更がなく、FPSを高く設定するのは経済的ではないため、10FPSを推奨します。
- 共有したい画面コンテンツに大量のテキストが含まれている場合、解像度とビットレートを適宜引き上げることができます。
- 最高ビットレート(videoBitrate)とは、画面が大きく変化したときの最高出力ビットレートのことです。画面コンテンツの変化が少ない場合、実際のエンコードビットレートは低くなります。


## アプリケーション間共有

### サンプルコード
[Github](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTC-API-Example-OC)の**ScreenShare**ディレクトリに、アプリケーション間共有用のサンプルコードを設置しています。これには、次のようなテキストが含まれています。

```
├─ TRTC-API-Example-OC              // TRTC API Example 
|  ├─ Basic                   // アプリケーション間画面共有機能のデモンストレーション
|  |  ├─ ScreenShare                   // アプリケーション間画面共有機能のデモンストレーション
|  |  |  ├── ScreenAnchorViewController.h
|  |  |  ├── ScreenAnchorViewController.m       // キャスターのスクリーンキャプチャステータス表示インターフェース
|  |  |  ├── ScreenAnchorViewController.xib
|  |  |  ├── ScreenAudienceViewController.h
|  |  |  ├── ScreenAudienceViewController.m     // 視聴者が見るレコーディングインターフェース
|  |  |  ├── ScreenAudienceViewController.xib
|  |  |  ├── ScreenEntranceViewController.h
|  |  |  ├── ScreenEntranceViewController.m     // 機能エントリーインターフェース
|  |  |  ├── ScreenEntranceViewController.xib
|  |  |  ├── TRTCBroadcastExtensionLauncher.h
|  |  |  ├── TRTCBroadcastExtensionLauncher.m   // スクリーンキャプチャを呼び出すために用いられる補助コード
|  |  |  ├── TXReplayKit_Screen   // スクリーンキャプチャのプロセスBroadcast Upload Extensionコードの詳細は手順2をご参照ください。
|  |  |  │   ├── Info.plist
|  |  |  │   ├── SampleHandler.h
|  |  |  │   └── SampleHandler.m                // システムからのスクリーンキャプチャデータを受信するために使用されます
```

[README](https://github.com/tencentyun/TRTCSDK/blob/master/iOS/TRTC-API-Example-OC/README.md)のガイドによって、このサンプルDemoを実行することができます。


### 結合手順

iOSシステムでアプリケーション間画面共有を行うには、Extensionスクリーンキャプチャプロセスを追加し、メインアプリプロセスと連携してプッシュを行う必要があります。Extensionスクリーンキャプチャプロセスは、システムによってスクリーンキャプチャが必要なときに作成され、システムが収集した画面イメージの受信を担当します。従って、次の事項を行う必要があります。

1. App Groupを作成し、XCodeにおいて設定を行います（オプション）。このステップは、Extensionスクリーンキャプチャプロセスが、同じメインアプリプロセスとプロセス間通信できるようにすることを目的としています。
2. お客様のプロジェクトにおいて、Broadcast Upload ExtensionのTargetを新規作成し、拡張コモジュール用としてカスタマイズされた`TXLiteAVSDK_ReplayKitExt.framework`をSDK圧縮パッケージに統合します。
3. メインアプリ側の受信ロジックと結合し、メインアプリにBroadcast UploadExtensionからのスクリーンキャプチャデータを待機させます。
4. Demoにあらかじめ実装されたhelper class (`RPSystemBroadcastPickerView`)を使用して、TencentMeetingのiOS版のように、ボタンをクリックすれば画面共有を呼び出せる効果を実現します（オプション）。

>! 手順1をスキップした場合、すなわちApp Groupsを設定しない場合は（インターフェースはnilを渡します）、画面共有は実行できますが、安定性が若干損なわれます。手順はやや多いですが、できる限り正しいApp Groupsを設定して、画面共有機能の安定性を確保してください。

[](id:createGroup)
#### 手順1：App Groupsの作成
お客様のアカウントを使用して[**https://developer.apple.com/**](https://developer.apple.com/)にログインし、次の操作を実行します。**完了後は、対応するProvisioning Profileを再ダウンロードする必要がありますので、ご注意ください**。

1. 【Certificates, IDs & Profiles】をクリックします。
2. 右側のインターフェースでプラス記号をクリックします。
3. 【App Groups】を選択して、【Continue】をクリックします。
4. ポップアップされたフォームにDescriptionとIdentifierを入力します。そのうちIdentifierは、インターフェースにおいて対応するAppGroupパラメータに渡す必要があります。完了したら、【Continue】をクリックします。
 ![](https://main.qcloudimg.com/raw/43dd60f5053b21c167ee3a8dbe7d16f9/Create_AppGroup.jpg)
5. Identifierページに戻り、左上のメニューから【App IDs】を選択し、お客様のアプリIDをクリックします（メインアプリとExtensionのアプリIDにも同様の設定が必要です）。
6. 【App Groups】を選択し、【Edit】をクリックします。
7. ポップアップされたフォームからお客様が作成したApp Groupを選択し、【Continue】をクリックして編集ページに戻り、【Save】をクリックして保存します。
 ![](https://main.qcloudimg.com/raw/962c1b705433aa62c9617f90d28238c5/Apply_AppGroup.jpg)
8. Provisioning Profileを再度ダウンロードし、XCodeに設定します。

[](id:createExtension)
#### 手順2：Broadcast Upload Extensionの作成
1. Xcodeメニューの【File】、【New】 、【Target...】を順にクリックし、【Broadcast Upload Extension】を選択します。
2. ポップアップされたダイアログボックスに関連情報を入力し、**【Include UI Extension】にはチェックを入れずに**【Finish】をクリックして作成を完了します。
3. ダウンロードしたSDK圧縮パッケージのプロジェクトにTXLiteAVSDK_ReplayKitExt.frameworkをドラッグし、先ほど作成したTargetにチェックを入れます。
4. 新しく追加したTargetを選択し、【+ Capability】を順番にクリックして、【App Groups】をダブルクリックします。下図のとおりです。
 ![AddCapability](https://main.qcloudimg.com/raw/a2b38f1581a495f2a966f6eaf464e057.png)
 操作が完了すると、下図のようにファイルリストに`Target名.entitlements`という名前のファイルが生成されます。このファイルを選択し、+記号をクリックして上記の手順のApp Groupを入力すればOKです。
 ![AddGroup](https://main.qcloudimg.com/raw/b4904a8b425cf55e58497b35c0700966.png)
5. メインアプリのTargetを選択し、**上記の手順に従って、メインアプリのTargetに同様の処理を行います。**
6. 新規作成したTargetにおいて、Xcodeは「SampleHandler.h」という名前のファイルを自動的に作成し、それを次のコードに置き換えます。**コード内のAPPGROUPを先ほど作成したApp Group Identifierに変更する必要があります**。
<dx-codeblock>
::: iOS object-c
#import "SampleHandler.h"
@import TXLiteAVSDK_ReplayKitExt;

#define APPGROUP @"group.com.tencent.liteav.RPLiveStreamShare"

@interface SampleHandler() <TXReplayKitExtDelegate>
@end

@implementation SampleHandler
// 注意：ここでのAPPGROUPは、先ほど作成したApp Group Identifierに変更する必要があります。
- (void)broadcastStartedWithSetupInfo:(NSDictionary<NSString *,NSObject *> *)setupInfo {
    [[TXReplayKitExt sharedInstance] setupWithAppGroup:APPGROUP delegate:self];
}

- (void)broadcastPaused {
    // User has requested to pause the broadcast. Samples will stop being delivered.
}

- (void)broadcastResumed {
    // User has requested to resume the broadcast. Samples delivery will resume.
}

- (void)broadcastFinished {
    [[TXReplayKitExt sharedInstance] finishBroadcast];
    // User has requested to finish the broadcast.
}

#pragma mark - TXReplayKitExtDelegate
- (void)broadcastFinished:(TXReplayKitExt *)broadcast reason:(TXReplayKitExtReason)reason
{
    NSString *tip = @"";
    switch (reason) {
        case TXReplayKitExtReasonRequestedByMain:
            tip = @"画面共有は終了しました";
            break;
        case TXReplayKitExtReasonDisconnected:
            tip = @"アプリケーションは切断されました";
            break;
        case TXReplayKitExtReasonVersionMismatch:
            tip = @"統合エラー（SDKバージョン番号が一致しません）";
            break;
    }

    NSError *error = [NSError errorWithDomain:NSStringFromClass(self.class)
                                         code:0
                                     userInfo:@{
                                         NSLocalizedFailureReasonErrorKey:tip
                                     }];
    [self finishBroadcastWithError:error];
}

- (void)processSampleBuffer:(CMSampleBufferRef)sampleBuffer withType:(RPSampleBufferType)sampleBufferType {
    switch (sampleBufferType) {
        case RPSampleBufferTypeVideo:
            [[TXReplayKitExt sharedInstance] sendVideoSampleBuffer:sampleBuffer];
            break;
        case RPSampleBufferTypeAudioApp:
            // Handle audio sample buffer for app audio
            break;
        case RPSampleBufferTypeAudioMic:
            // Handle audio sample buffer for mic audio
            break;
            
        default:
            break;
    }
}
@end
:::
</dx-codeblock>

[](id:receive)
#### 手順3：メインアプリ側の受信ロジックとの結合
以下の手順に従って、メインアプリ側の受信ロジックと結合します。すなわち、ユーザーが画面共有をトリガーする前に、メインアプリを「待機」状態にして、Broadcast Upload Extensionプロセスからスクリーンキャプチャデータをいつでも受信できるようにします。
1. TRTCCloudがカメラのキャプチャをオフにしていることを確認します。オフになっていない場合は、[stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a01ee967e3180a5e2fc0e37e9e99e85b3)を呼び出して、カメラのキャプチャをオフにしてください。
2. [startScreenCaptureByReplaykit:appGroup:](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a78a8da8c2f235446d03cd2db26f97b60)メソッドを呼び出し、[手順1](#createGroup)で設定したAppGroupを渡して、SDKを「待機」状態にします。
3. ユーザーが画面共有をトリガーするまで待機します。[手順4](#launch)における「トリガーボタン」が実装されていない場合、ユーザーがiOSシステムのコントロールセンターにおいて、スクリーンキャプチャボタンを長押しして画面共有をトリガーする必要があります。
4. [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa8ea0235691fc9cde0a64833249230bb)インターフェースを呼び出すことにより、いつでも画面共有を停止できます。
<dx-codeblock>
::: iOS object-c
// 画面共有を開始するには、APPGROUPを上記の手順で作成したApp Group Identifierに置き換える必要があります。
- (void)startScreenCapture {
    TRTCVideoEncParam *videoEncConfig = [[TRTCVideoEncParam alloc] init];
    videoEncConfig.videoResolution = TRTCVideoResolution_1280_720;
    videoEncConfig.videoFps = 10;
    videoEncConfig.videoBitrate = 2000;
    //APPGROUPを上記の手順で作成したApp Group Identifierに置き換える必要があります。
    [[TRTCCloud sharedInstance] startScreenCaptureByReplaykit:videoEncConfig
                                                     appGroup:APPGROUP];
}

// 画面共有を停止します
- (void)stopScreenCapture {
    [[TRTCCloud sharedInstance] stopScreenCapture];
}

// 画面共有の開始イベントの通知は、TRTCCloudDelegateを介して受信できます
- (void)onScreenCaptureStarted {
    [self showTip:@"画面共有の開始"];
}
:::
</dx-codeblock>

[](id:launch)
#### 手順4：画面共有のトリガーボタンの追加（オプション）
[手順3](＃receive)までに、ユーザーがコントロールセンターからスクリーンキャプチャボタンを長押しして、画面共有を手動で開始する必要があります。以下の方法で、VooVMeetingのように、ボタンをクリックすることでトリガーする効果を実現できます。

1. [Demo](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTC-API-Example-OC/Basic/ScreenShare)において`TRTCBroadcastExtensionLauncher`というクラスを見つけて、お客様のプロジェクトに追加します。
2. インターフェースにボタンを設置し、ボタンの応答関数において`TRTCBroadcastExtensionLauncher`の`launch`関数を呼び出すと、画面共有機能を呼び出すことができます。
<dx-codeblock>
::: iOS object-c
// カスタムボタンによる応答メソッド
- (IBAction)onScreenButtonTapped:(id)sender {
    [TRTCBroadcastExtensionLauncher launch];
}
:::
</dx-codeblock>

>!
>- AppleはiOS12.0に`RPSystemBroadcastPickerView`を追加しました。これによって、ユーザーがアプリケーションからランチャーをポップアップして、画面共有の開始を確認することができます。現時点では、`RPSystemBroadcastPickerView`はインターフェースのカスタマイズをサポートしておらず、公式の呼び出しメソッドもありません。
>- TRTCBroadcastExtensionLauncherの原理とは、`RPSystemBroadcastPickerView` のサブViewをスキャンしてUIButtonを見つけ、そのクリックイベントをトリガーするというものです。
> -**ただし、このソリューションはAppleで公式に推奨されているものではなく、システムが新たにアップデートされた場合、無効になる可能性があります。従って、[手順4](#launch)はオプションのソリューションにすぎず、お客様の自己責任でこのソリューションをご利用ください。**

## 画面共有の確認
- **Mac/Windows画面共有の確認**
  ルームにいるMac/Windowsユーザーが画面共有を起動し、サブストリームを介して共有を実行します。ルームにいるその他のユーザーは、TRTCCloudDelegate内の[onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a52ad5b09959df6e940aec7fb9615de9c)イベントを介してこの通知を受け取ります。
  画面共有を確認したいユーザーは[startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae029514645970e7d32470cf1c7aca716)インターフェースを介して、リモートユーザーのサブストリーム画面のレンダリングを起動することができます。

- **Android / iOS画面共有の確認**
  ユーザーがAndroid / iOSを介して画面共有を実行する場合は、メインストリームを介して共有を実行します。ルームにいるその他ユーザーはTRTCCloudDelegateの中の[onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80)イベントを介してこの通知を受け取ります。
  画面共有を確認したいユーザーは[startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49)インターフェースを介して、リモートユーザーのメインストリーム画面のレンダリングを起動することができます。








