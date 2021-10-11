## Androidプラットフォームの場合
Tencent CloudのTRTCは、Androidシステムでの画面共有をサポートしており、現在のシステムの画面コンテンツは、TRTC SDKを介してルーム内の他のユーザーと共有されます。この機能については、次のような2つの注意点があります。

- TRTC Android版の画面共有は、デスクトップ版のように「サブチャネルの共有」をサポートしていません。従って、画面共有を開始するときは、あらかじめカメラのキャプチャを停止する必要があります。停止しない場合、衝突が生じます。
- Androidシステムのバックグラウンドアプリが引き続きCPUを使用すると、システムによって強制終了されやすくなり、画面共有自体が必然的にCPUを消費してしまいます。この矛盾するような衝突を解消するには、アプリで画面共有を開始するとともに、Androidシステムにフローティングウィンドウをポップアップする必要があります。AndroidはフォアグラウンドUIを含むアプリプロセスを強制終了しないため、このソリューションによって、お客様のアプリはシステムに自動回収されることなく画面を共有し続けることができます。


### 画面共有を開始
Androidデバイスでの画面共有は、`TRTCCloud`の[startScreenCapture()](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startScreenCapture.html)インターフェースを呼び出すだけで開始することができます。ただし、明瞭で安定した共有効果を実現するには、次の3つの点に注意する必要があります。

#### Activityの追加
次のactivityをmanifestファイルに貼り付けます（項目コードに存在する場合は追加する必要はありません）。
```xml
<activity 
    android:name="com.tencent.rtmp.video.TXScreenCapture$TXScreenCaptureAssistantActivity" 
    android:theme="@android:style/Theme.Translucent"/>
```

#### ビデオコーデックパラメータの設定
[startScreenCapture()](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startScreenCapture.html)で最初のパラメータ`encParams`を設定することにより、画面共有のエンコード品質を指定することができます。`encParams`をnullに指定した場合、SDKは以前に設定されたエンコードパラメータを自動的に使用します。推奨されるパラメータの設定は、次のとおりです。

| パラメータ項目 | パラメータ名 | 通常の推奨値 | テキスト教育シナリオ |
|---------|---------|---------|-----|
| 解像度 | videoResolution | 1280 × 720 | 1920 × 1080 |
| フレームレート | videoFps | 10 FPS | 8 FPS |
| 最高ビットレート | videoBitrate| 1600 kbps | 2000 kbps |
| 解像度アダプティブ | enableAdjustRes | NO | NO |
>?
>- 画面共有されるコンテンツには通常、大幅な変更がなく、FPSを高く設定するのは経済的ではないため、10FPSを推奨します。
>- 共有したい画面コンテンツに大量のテキストが含まれている場合、解像度とビットレートを適宜引き上げることができます。
>- 最高ビットレート(videoBitrate)とは、画面が大きく変化したときの最高出力ビットレートのことです。画面コンテンツの変化が少ない場合、実際のエンコードビットレートは低くなります。

#### フローティングウィンドウのポップアップで強制終了を回避
Android 7.0以降のシステムから、バックグラウンドで実行されている通常のアプリプロセスに切り替わりますが、CPUのアクティビティがある場合、常にシステムによって強制終了されやすくなります。従って、アプリをバックグラウンドに切り替えてサイレントで画面共有すると、フローティングウィンドウのポップアップというソリューションによって強制終了を回避することができます。また、携帯電話の画面にフローティングウィンドウを表示することは、ユーザーが今、画面共有を行っていることをユーザーに知らせ、プライバシー情報の漏えい防止につながります。

##### 方法：通常のフローティングウィンドウをポップアップする
「TencentMeeting」に似たミニフローティングウィンドウのポップアップは、サンプルコード [tool.dart](https://github.com/c1avie/trtc_demo/blob/master/lib/page/trtcmeetingdemo/tool.dart) 中の実装を参考とすることができます。
```
//画面共有でミニフローティングウィンドウをポップアップした時、バックエンドに切り替えられたアプリケーションが強制終了されることを防止します。
  static void showOverlayWindow() {
    SystemWindowHeader header = SystemWindowHeader(
      title: SystemWindowText(
          text: 「画面共有中」, fontSize: 14, textColor: Colors.black45),
      decoration: SystemWindowDecoration(startColor: Colors.grey[100]),
    );
    SystemAlertWindow.showSystemWindow(
      width: 18,
      height: 95,
      header: header,
      margin: SystemWindowMargin(top: 200),
      gravity: SystemWindowGravity.TOP,
    );
  }
```

## iOSプラットフォームの場合
- **[アプリケーション内の共有](#Internal)**
現在のアプリの画面のみを共有できます。この特性をサポートするには、iOSのバージョン13以降のOSが必要です。現在のアプリ以外の画面コンテンツを共有できないため、高度なプライバシー保護が必要なシーンに適しています。
- **[アプリケーション間共有](#Cross)**
AppleのReplaykitソリューションをベースとして、システム全体の画面コンテンツを共有できます。ただし、現在のアプリはExtension拡張コンポーネントを追加で提供する必要があるため、結合手順はアプリ内共有よりもやや多くなります。

>! 注意すべき点としては、モバイル版のTRTC SDKは、デスクトップ版のように、「サブストリームの共有」をサポートしていません。これは、iOSとAndroidシステムは、どちらもバックグラウンドで実行されているアプリに対し、カメラの使用権を制限しているからです。従って、サブストリームの共有をサポートする意義はあまりありません。

[](id:Internal)
### 方法1：iOSプラットフォームアプリケーション内の共有

アプリ内共有のソリューションは非常にシンプルです。TRTC SDKが提供するインターフェース[startScreenCapture](https://pub.flutter-io.cn/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startScreenCapture.html)を呼び出し、エンコードパラメータ`TRTCVideoEncParam`と`appGroup`を渡して`''`にセットするだけです。`TRTCVideoEncParam`パラメータはnullに設定することができます。この場合、SDKは画面共有が開始される前のエンコードパラメータを引き続き使用します。

iOS画面共有に推奨されるエンコードパラメータは次のとおりです。

| パラメータ項目 | パラメータ名 | 通常の推奨値 | テキスト教育シナリオ |
|---------|---------|---------|-----|
| 解像度 | videoResolution | 1280 × 720 | 1920 × 1080 |
| フレームレート | videoFps | 10 FPS | 8 FPS |
| 最高ビットレート | videoBitrate| 1600 kbps | 2000 kbps |
| 解像度アダプティブ | enableAdjustRes | NO | NO |

>?
>- 画面共有されるコンテンツには通常、大幅な変更がなく、FPSを高く設定するのは経済的ではないため、10FPSを推奨します。
>- 共有したい画面コンテンツに大量のテキストが含まれている場合、解像度とビットレートを適宜引き上げることができます。
>- 最高ビットレート(videoBitrate)とは、画面が大きく変化したときの最高出力ビットレートのことです。画面コンテンツの変化が少ない場合、実際のエンコードビットレートは低くなります。

[](id:Cross)
### 方法2：iOSプラットフォームアプリケーション間の共有

#### サンプルコード
[Github](https://github.com/c1avie/trtc_demo)の**trtc_demo/ios**ディレクトリに、アプリケーション間共有用のサンプルコードを設置しています。これには、次のようなテキストが含まれています。

```
├── Broadcast.Upload        //スクリーンキャプチャのプロセスBroadcast Upload Extensionコードの詳細は手順2をご参照ください。
│   ├── Broadcast.Upload.entitlements       //プロセス間通信の設定に使用されるAppGroup情報
│   ├── Broadcast.UploadDebug.entitlements  //プロセス間通信の設定に使用されるAppGroup情報（debug環境）
│   ├── Info.plist
│   └── SampleHandler.swift     // システムからのスクリーンキャプチャデータを受信するために使用されます
├── Resource                    // リソースファイル
├── Runner                      // TRTC簡易化Demo
├── TXLiteAVSDK_ReplayKitExt.framework      //TXLiteAVSDK_ReplayKitExt SDK
```

[README](https://github.com/c1avie/trtc_demo/blob/master/README.md)のガイドによって、このサンプルDemoを実行することができます。


#### 結合手順
iOSシステムでアプリケーション間画面共有を行うには、Extensionスクリーンキャプチャプロセスを追加し、メインアプリプロセスと連携してプッシュを行う必要があります。Extensionスクリーンキャプチャプロセスは、システムによってスクリーンキャプチャが必要なときに作成され、システムが収集した画面イメージの受信を担当します。従って、次の事項を行う必要があります。
1. App Groupを作成し、XCodeにおいて設定を行います（オプション）。このステップは、Extensionスクリーンキャプチャプロセスが、同じメインアプリプロセスとプロセス間通信できるようにすることを目的としています。
2. お客様のプロジェクトにおいて、Broadcast Upload ExtensionのTargetを新規作成し、拡張コモジュール用としてカスタマイズされた`TXLiteAVSDK_ReplayKitExt.framework`をSDK圧縮パッケージに統合します。
3. メインアプリ側の受信ロジックと結合し、メインアプリにBroadcast Upload Extensionからのスクリーンキャプチャデータを待機させます。
4. `pubspec.yaml`ファイルを編集して`replay_kit_launcher`プラグインを導入し、TRTC Demo Screenのようにボタンをクリックすれば画面共有の呼び出しを実現します（オプション）。
```
# trtc sdkとreplay_kit_launcherの導入
dependencies:
  tencent_trtc_cloud: ^0.2.1
  replay_kit_launcher: ^0.2.0+1
```

>! [手順1](#Step1)をスキップした場合、すなわちApp Groupを設定しない場合は（インターフェースはnullを渡します）、画面共有は実行できますが、安定性が若干損なわれます。手順はやや多いですが、できる限り正しいApp Groupを設定して、画面共有機能の安定性を確保してください。

[](id:createGroup)[](id:Step1)
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
1. Xcodeメニューの【File】 > 【New】 > 【Target...】を順にクリックし、【Broadcast Upload Extension】を選択します。
2. ポップアップされたダイアログボックスに関連情報を入力し、**【Include UI Extension】にはチェック"を入れずに**【Finish】をクリックして作成を完了します。
3. ダウンロードしたSDK圧縮パッケージのプロジェクトにTXLiteAVSDK_ReplayKitExt.frameworkをドラッグし、先ほど作成したTargetにチェックを入れます。
4. 新しく追加したTargetを選択し、【+ Capability】を順番にクリックして、【App Groups】をダブルクリックします。下図のとおりです。
 ![AddCapability](https://main.qcloudimg.com/raw/a2b38f1581a495f2a966f6eaf464e057.png)
 操作が完了すると、下図のようにファイルリストに`Target名.entitlements`という名前のファイルが生成されます。このファイルを選択し、+記号をクリックして上記の手順のApp Groupを入力すればOKです。
 ![AddGroup](https://main.qcloudimg.com/raw/b4904a8b425cf55e58497b35c0700966.png)
5. メインアプリのTargetを選択し、**上記の手順に従って、メインアプリのTargetに同様の処理を行います。**
6. 新規作成したTargetにおいて、Xcodeは「SampleHandler.swift」という名前のファイルを自動的に作成し、それを次のコードに置き換えます。**コード内のAPPGROUPを先ほど作成したApp Group Identifierに変更する必要があります**。
<dx-codeblock>
::: iOS swift

import ReplayKit
import TXLiteAVSDK_ReplayKitExt


let APPGROUP = "group.com.tencent.comm.trtc.demo"

class SampleHandler: RPBroadcastSampleHandler, TXReplayKitExtDelegate {

    let recordScreenKey = Notification.Name.init("TRTCRecordScreenKey")
    
    override func broadcastStarted(withSetupInfo setupInfo: [String : NSObject]?) {
        // User has requested to start the broadcast. Setup info from the UI extension can be supplied but optional.
        TXReplayKitExt.sharedInstance().setup(withAppGroup: APPGROUP, delegate: self)
    }
    
    override func broadcastPaused() {
        // User has requested to pause the broadcast. Samples will stop being delivered.
    }
    
    override func broadcastResumed() {
        // User has requested to resume the broadcast. Samples delivery will resume.
    }
    
    override func broadcastFinished() {
        // User has requested to finish the broadcast.
        TXReplayKitExt.sharedInstance() .finishBroadcast()
    }
    
    func broadcastFinished(_ broadcast: TXReplayKitExt, reason: TXReplayKitExtReason) {
        var tip = ""
        switch reason {
        case TXReplayKitExtReason.requestedByMain:
            tip = 「画面共有は終了しました」
            break
        case TXReplayKitExtReason.disconnected:
            tip = 「アプリケーションは切断されました」
            break
        case TXReplayKitExtReason.versionMismatch:
            tip = 「統合エラー（SDKバージョン番号が一致しません）」
            break
        default:
            break
        }
        
        let error = NSError(domain: NSStringFromClass(self.classForCoder), code: 0, userInfo: [NSLocalizedFailureReasonErrorKey:tip])
        finishBroadcastWithError(error)
    }
    
    override func processSampleBuffer(_ sampleBuffer: CMSampleBuffer, with sampleBufferType: RPSampleBufferType) {
        switch sampleBufferType {
        case RPSampleBufferType.video:
            // Handle video sample buffer
            TXReplayKitExt.sharedInstance() .sendVideoSampleBuffer(sampleBuffer)
            break
        case RPSampleBufferType.audioApp:
            // Handle audio sample buffer for app audio
            break
        case RPSampleBufferType.audioMic:
            // Handle audio sample buffer for mic audio
            break
        @unknown default:
            // Handle other sample buffer types
            fatalError("Unknown type of sample buffer")
        }
    }
}
:::
</dx-codeblock>

[](id:receive)
#### 手順3：メインアプリ側の受信ロジックとの結合
以下の手順に従って、メインアプリ側の受信ロジックと結合します。すなわち、ユーザーが画面共有をトリガーする前に、メインアプリを「待機」状態にして、Broadcast Upload Extensionプロセスからスクリーンキャプチャデータをいつでも受信できるようにします。
1. TRTCCloudがカメラのキャプチャをオフにしていることを確認します。オフになっていない場合は、 [stopLocalPreview](https://pub.flutter-io.cn/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopLocalPreview.html) を呼び出して、カメラのキャプチャをオフにしてください。
2. [startScreenCapture](https://pub.flutter-io.cn/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startScreenCapture.html)メソッドを呼び出し、[手順1](#createGroup)で設定したAppGroupを渡して、SDKを「待機」状態にします。
3. ユーザーが画面共有をトリガーするまで待機します。[手順4](#launch)における「トリガーボタン」が実装されていない場合、ユーザーがiOSシステムのコントロールセンターにおいて、スクリーンキャプチャボタンを長押しして画面共有をトリガーする必要があります。

4. [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa8ea0235691fc9cde0a64833249230bb)インターフェースを呼び出すことにより、いつでも画面共有を停止できます。
<dx-codeblock>
::: dart 
// 画面共有を開始するには、APPGROUPを上記の手順で作成したApp Groupに置き換える必要があります 
trtcCloud.startScreenCapture(
    TRTCVideoEncParam(
        videoFps: 10,
        videoResolution: TRTCCloudDef.TRTC_VIDEO_RESOLUTION_1280_720,
        videoBitrate: 1600,
        videoResolutionMode: TRTCCloudDef.TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT,
    ),
    iosAppGroup,
);

// 画面共有を停止します
await trtcCloud.stopScreenCapture();


// 画面共有の開始イベントの通知は、TRTCCloudListenerを介して受信できます
onRtcListener(type, param){
    if (type == TRTCCloudListener.onScreenCaptureStarted) {
      //画面共有の開始
    }
}
:::
</dx-codeblock>

[](id:launch)
#### 手順4：画面共有のトリガーボタンの追加（オプション）
[手順3](＃receive)までに、ユーザーがコントロールセンターからスクリーンキャプチャボタンを長押しして、画面共有を手動で開始する必要があります。以下の方法で、TRTC Demo Screenのように、ボタンをクリックすることでトリガーする効果を実現できます。

1. `replay_kit_launcher`プラグインをご使用のプロジェクトに導入します。
2. インターフェースにボタンを設置し、ボタンの応答関数において`ReplayKitLauncher.launchReplayKitBroadcast(iosExtensionName);`関数を呼び出すと、画面共有機能を呼び出すことができます。
```
// カスタムボタンによる応答メソッド
onShareClick() async {
   if (Platform.isAndroid) {
      if (await SystemAlertWindow.requestPermissions) {
        MeetingTool.showOverlayWindow();
      }
    } else {
      //画面共有機能は実機でのみテストすることができます
      ReplayKitLauncher.launchReplayKitBroadcast(iosExtensionName);
    }
}
```

## 画面共有の確認
- **Android/iOS画面共有の確認**
  ユーザーがAndroid / iOSを介して画面共有を実行する場合は、メインストリームを介して共有を実行することができます。ルームにいるその他ユーザーはTRTCCloudListener中の[onUserVideoAvailable](https://pub.flutter-io.cn/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html) イベントを介してこの通知を受け取ります。
  画面共有を確認する場合は、[startRemoteView](https://pub.flutter-io.cn/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startRemoteView.html)インターフェースを介してリモートユーザーのメインストリーム画面のレンダリングを起動することができます。

## よくあるご質問
 **1つのルームで同時にいくつの画面を共有できますか。**
現在、1つの TRTC オーディオ・ビデオルームで共有できる画面は1つだけです。
