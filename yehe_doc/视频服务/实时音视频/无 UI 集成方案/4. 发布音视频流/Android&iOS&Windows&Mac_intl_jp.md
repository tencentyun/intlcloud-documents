このドキュメントでは、主にキャスターが自分のオーディオビデオストリームをリリースする方法を紹介します。いわゆる「リリース」とは、マイクとカメラをオンにして、ルーム内の他のユーザーが自分の音声とビデオを聞いたり見たりできるようにすることを意味します。

![](https://qcloudimg.tencent-cloud.cn/raw/b86c1df39b412bddf29d26bfaa9d5f02.png)
## 呼び出しガイド

[](id:step1)
### 手順1：事前手順の完了

[SDKのプロジェクトへのインポート](https://intl.cloud.tencent.com/document/product/647/35092)を参照して、SDKのインポートおよびApp権限の設定を完了します。

[](id:step2)
### 手順2：カメラプレビューをオンにする
**startLocalPreview**インターフェースを呼び出して、カメラプレビューをオンにすることができます。このとき、SDKはシステムにカメラの使用権限を申請し、カメラキャプチャプロセスはユーザーの承認が渡された後にのみ開始されます。

ローカル画面のレンダリングパラメータを設定する場合は、**setLocalRenderParams**インターフェースを呼び出してローカルプレビューのレンダリングパラメータを設定できます。最初にプレビューをオンにしてからプレビューパラメータを設定すると画面がジッターするのを防ぐために、プレビューパラメータを設定する必要がある場合は、プレビューを開始する前に呼び出すことをお勧めします。

カメラのさまざまな制御パラメータを制御する場合は、**TXDeviceManager**インターフェースを呼び出して、「フロントカメラとリアカメラの切り替え」、「フォーカスモードの設定」、「フラッシュのオン・オフの切り替え」などの一連の操作を実行できます。

美顔効果や画質調節をご希望の場合は、[画質設定](https://intl.cloud.tencent.com/document/product/647/35153)で詳しく紹介します。

<dx-codeblock>
::: Android java
// ローカル画面のプレビューモードを設定します。左右のイメージをオンにし、画面を塗りつぶしモードに設定します
TRTCCloudDef.TRTCRenderParams param = new TRTCCloudDef.TRTCRenderParams();
param.fillMode   = TRTCCloudDef.TRTC_VIDEO_RENDER_MODE_FILL;
param.mirrorType = TRTCCloudDef.TRTC_VIDEO_MIRROR_TYPE_AUTO;
mCloud.setLocalRenderParams(param);

// ローカルカメラのプレビューを開始します（localCameraVideoはローカルレンダリング画面をレンダリングするためのコントロールです）
TXCloudVideoView cameraVideo = findViewById(R.id.txcvv_main_local);
mCloud.startLocalPreview(true, cameraVideo);

// TXDeviceManagerを介して自動フォーカスをオンにし、フラッシュをオンにします
TXDeviceManager manager = mCloud.getDeviceManager();
if (manager.isAutoFocusEnabled()) {
    manager.enableCameraAutoFocus(true);
}
manager.enableCameraTorch(true);
:::
::: iOS  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// ローカル画面のプレビューモードを設定します。左右のイメージをオンにし、画面を塗りつぶしモードに設定します
TRTCRenderParams *param = [[TRTCRenderParams alloc] init];
param.fillMode   = TRTCVideoFillMode_Fill;
param.mirrorType = TRTCVideoMirrorTypeAuto;
[self.trtcCloud setLocalRenderParams:param];

// ローカルカメラのプレビューを開始します（localCameraVideoViewはローカルレンダリング画面をレンダリングするためのコントロールです）
[self.trtcCloud startLocalPreview:YES view:localCameraVideoView];

// TXDeviceManagerを介して自動フォーカスをオンにし、フラッシュをオンにします
TXDeviceManager *manager = [self.trtcCloud getDeviceManager];
if ([manager isAutoFocusEnabled]) {
    [manager enableCameraAutoFocus:YES];
}
[manager enableCameraTorch:YES];
:::
::: Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// ローカル画面のプレビューモードを設定します。左右のイメージをオンにし、画面を塗りつぶしモードに設定します
TRTCRenderParams *param = [[TRTCRenderParams alloc] init];
param.fillMode   = TRTCVideoFillMode_Fill;
param.mirrorType = TRTCVideoMirrorTypeAuto;
[self.trtcCloud setLocalRenderParams:param];

// ローカルカメラのプレビューを開始します（localCameraVideoViewはローカルレンダリング画面をレンダリングするためのコントロールです）
[self.trtcCloud startLocalPreview:localCameraVideoView];
:::
::: Windows  C++
// ローカル画面のプレビューモードを設定します。左右のイメージをオンにし、画面を塗りつぶしモードに設定します
liteav::TRTCRenderParams render_params;
render_params.mirrorType = liteav::TRTCVideoMirrorType_Enable;
render_params.fillMode = TRTCVideoFillMode_Fill;
trtc_cloud_->setLocalRenderParams(render_params);

// ローカルカメラのプレビューを開始します（viewはローカルレンダリング画面をレンダリングするためのコントロールハンドルです）
liteav::TXView local_view = (liteav::TXView)(view);
trtc_cloud_->startLocalPreview(local_view);
:::
</dx-codeblock>


[](id:step3)
### 手順3：マイクのキャプチャをオンにする
**startLocalAudio**を呼び出してマイクのキャプチャをオンにするができます。このインターフェースは、`quality`パラメータを使用してキャプチャモードを決定してください。このパラメータの名前はqualityと呼ばれますが、品質が高いほどより良いという意味ではありません。さまざまなサービスシーンで最適なパラメータを選択できます（このパラメータのより正確な意味はsceneです）。

- **SPEECH**
このモードのSDKオーディオモジュールは、音声信号の抽出に重点を置き、周囲の環境ノイズを可能な限りフィルタリングします。同時に、このモードのオーディオデータは、低品質ネットワークに対して最高の耐性を獲得するため、このモードは「ビデオ通話」や「オンライン会議」など、音声通信に重点を置いたシーンに特に適しています。
- **MUSIC**
このモードのSDKは、高いオーディオ処理帯域幅とステレオモードを使用します。キャプチャ品質を最大化すると同時に、オーディオDSP処理モジュールを最も弱いレベルに調整して音質を最大化します。したがって、このモードは「音楽ライブストリーミング」シーン、特にキャスターがプロのサウンドカードを使用するライブストリーミングシーンに適しています。
- **DEFAULT**
このモードのSDKは、スマート認識アルゴリズムを有効にして現在の環境を認識し、目的を明確にして最適な処理モードを選択します。ただし、最高の認識アルゴリズムでさえ不正確である場合もあります。製品の位置付けが明確な場合は、音声通信に重点を置いたSPEECHと音楽の音質に重点を置いたMUSICの両方から1つを選択することをお勧めします。

<dx-codeblock>
::: Android java
// マイクのキャプチャをオンにし、現在のシーンを音声モード（ノイズ抑制能力が高く、弱いネットワークに対する耐性が強い）に設定します
mCloud.startLocalAudio(TRTCCloudDef.TRTC_AUDIO_QUALITY_SPEECH );

// マイクのキャプチャをオンにし、現在のシーンを音楽モード（ハイファイキャプチャ、低音質損失、プロのサウンドカードでの使用を推薦）に設定します
mCloud.startLocalAudio(TRTCCloudDef.TRTC_AUDIO_QUALITY_MUSIC);
:::
::: iOS&Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// マイクのキャプチャをオンにし、現在のシーンを音声モード（ノイズ抑制能力が高く、弱いネットワークに対する耐性が強い）に設定します
[self.trtcCloud startLocalAudio:TRTCAudioQualitySpeech];

// マイクのキャプチャをオンにし、現在のシーンを音楽モード（ハイファイキャプチャ、低音質損失、プロのサウンドカードでの使用を推薦）に設定します
[self.trtcCloud startLocalAudio:TRTCAudioQualityMusic];
:::
::: Windows  C++
// マイクのキャプチャをオンにし、現在のシーンを音声モード（ノイズ抑制能力が高く、弱いネットワークに対する耐性が強い）に設定します
trtc_cloud_->startLocalAudio(TRTCAudioQualitySpeech);

// マイクのキャプチャをオンにし、現在のシーンを音楽モード（ハイファイキャプチャ、低音質損失、プロのサウンドカードでの使用を推薦）に設定します
trtc_cloud_->startLocalAudio(TRTCAudioQualityMusic);
:::
</dx-codeblock>

[](id:step4)
### 手順4：TRTCの入室

[入室](https://intl.cloud.tencent.com/document/product/647/47645)を参照して現在のユーザーが入室します。入室すると、SDKはルーム内の他のユーザーに自分のオーディオストリームをリリースします。

>! 当然ながら、入室（enterRoom）後にカメラプレビューとマイクキャプチャを開始することもできますが、ライブストリーミングシーンでは、キャスターにマイクのテストと美顔調整の時間を与える必要があるため、カメラとマイクを起動してから入室する方法は一般的です。

<dx-codeblock>
::: Android java
mCloud = TRTCCloud.sharedInstance(getApplicationContext());
mCloud.setListener(mTRTCCloudListener);

// TRTC入室パラメータを組み立てるには、TRTCParamsの各フィールドを独自のパラメータに置き換えてください
// Please replace each field in TRTCParams with your own parameters
TRTCCloudDef.TRTCParams param = new TRTCCloudDef.TRTCParams();
params.sdkAppId = 1400000123;  // Please replace with your own SDKAppID
params.userId = "denny";       // Please replace with your own userid  
params.roomId = 123321;        // Please replace with your own room number
params.userSig = "xxx";        // Please replace with your own userSig
params.role = TRTCCloudDef.TRTCRoleAnchor;

// 「オンラインライブストリーミング」のシーンの場合、ユースケースをTRTC_APP_SCENE_LIVEに設定してください
// If your application scenario is a video call between several people, please use "TRTC_APP_SCENE_LIVE"
mCloud.enterRoom(param, TRTCCloudDef.TRTC_APP_SCENE_LIVE);        
:::

::: iOS&Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
self.trtcCloud.delegate = self;

// TRTC入室パラメータを組み立てるには、TRTCParamsの各フィールドを独自のパラメータに置き換えてください
// Please replace each field in TRTCParams with your own parameters
TRTCParams *params = [[TRTCParams alloc] init];
params.sdkAppId = 1400000123;  // Please replace with your own SDKAppID
params.roomId = 123321; // Please replace with your own room number
params.userId = @"denny";   // Please replace with your own userid  
params.userSig = @"xxx"; // Please replace with your own userSig
params.role = TRTCRoleAnchor;

// 「オンラインライブストリーミング」のシーンの場合、ユースケースをTRTC_APP_SCENE_LIVEに設定してください
// If your application scenario is a video call between several people, please use "TRTC_APP_SCENE_LIVE"
[self.trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE];
:::

::: Windows  C++
trtc_cloud_ = getTRTCShareInstance();

// TRTC入室パラメータを組み立てるには、TRTCParamsの各フィールドを独自のパラメータに置き換えてください
// Please replace each field in TRTCParams with your own parameters
liteav::TRTCParams params;
params.sdkAppId = 1400000123;  // Please replace with your own SDKAppID
params.userId = "denny";       // Please replace with your own userid  
params.roomId = 123321;        // Please replace with your own room number
params.userSig = "xxx";        // Please replace with your own userSig
params.role = TRTCCloudDef.TRTCRoleAnchor;

// 「オンラインライブストリーミング」のシーンの場合、ユースケースをTRTC_APP_SCENE_LIVEに設定してください
// If your application scenario is a video call between several people, please use "TRTC_APP_SCENE_LIVE"
trtc_cloud_->enterRoom(params, liteav::TRTCAppSceneLIVE);
:::
</dx-codeblock>


[](id:step5)
### 手順5：ロール間の切り替え

**TRTCの「ロール」**
- 「ビデオ通話」(TRTC_APP_SCENE_VIDEOCALL )と「音声威通話」(TRTC_APP_SCENE_AUDIOCALL)の2つのシーンでは、入室時にロールを設定する必要はありません。その理由として、これらの2つのモードでは、各ユーザーはデフォルトでキャスター(Anchor)であるからです。
- 「ビデオライブストリーミング」(TRTC_APP_SCENE_LIVE)と「音声ライブストリーミング」(TRTC_APP_SCENE_VOICE_CHATROOM)の2つのシーンでは、各ユーザーは、入室時に「キャスター(Anchor)」または「視聴者(Audience)」のいずれかの自分の「ロール」を指定する必要があります。

**ロールの切り替え**
TRTCでは、「キャスター(Anchor)」のみがオーディオビデオストリームをリリースする権限を持っています。「視聴者(Audience(」はオーディオビデオストリームをリリースできません。
したがって、入室時に使用するロールが「視聴者(Audience)」である場合は、オーディオビデオストリームのリリース（「マイク・オン」とも呼ばれる）前に、**switchRole**インターフェースを呼び出してロールを「キャスター(Anchor)」に切り替える必要があります。

<dx-codeblock>
::: Android java
// 現在のロールが視聴者(Audience)の場合は、最初にswitchRoleを呼び出してキャスター(Anchor)に切り替えてください
// If your current role is 'audience', you need to call switchRole to switch to 'anchor' first
mCloud.switchRole(TRTCCloudDef.TRTCRoleAnchor);
mCloud.startLocalAudio(TRTCCloudDef.TRTC_AUDIO_QUALITY_DEFAULT);
mCloud.startLocalPreview(true, cameraVide);

// ロールの切り替えに失敗した場合、onSwitchRoleコールバックのエラーコードは0ではありません
// If switching operation failed, the error code of the 'onSwitchRole' is not zero
@Override
public void onSwitchRole(final int errCode, final String errMsg) {
    if (errCode != 0) {
        Log.d(TAG, "Switching operation failed...");
    }   
}
:::
::: iOS ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// 現在のロールが視聴者(Audience)の場合は、最初にswitchRoleを呼び出してキャスター(Anchor)に切り替えてください
// If your current role is 'audience', you need to call switchRole to switch to 'anchor' first
[self.trtcCloud switchRole:TRTCRoleAnchor];
[self.trtcCloud startLocalAudio:TRTCAudioQualityDefault];
[self.trtcCloud startLocalPreview:YES view:localCameraVideoView];

// ロールの切り替えに失敗した場合、onSwitchRoleコールバックのエラーコードは0ではありません
// If switching operation failed, the error code of the 'onSwitchRole' is not zero
- (void)onSwitchRole:(TXLiteAVError)errCode errMsg:(nullable NSString *)errMsg {
    if (errCode != 0) {
        NSLog(@"Switching operation failed... ");
    }   
}
:::
::: Mac ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// 現在のロールが視聴者(Audience)の場合は、最初にswitchRoleを呼び出してキャスター(Anchor)に切り替えてください
// If your current role is 'audience', you need to call switchRole to switch to 'anchor' first
[self.trtcCloud switchRole:TRTCRoleAnchor];
[self.trtcCloud startLocalAudio:TRTCAudioQualityDefault];
[self.trtcCloud startLocalPreview:localCameraVideoView];

// ロールの切り替えに失敗した場合、onSwitchRoleコールバックのエラーコードは0ではありません
// If switching operation failed, the error code of the 'onSwitchRole' is not zero
- (void)onSwitchRole:(TXLiteAVError)errCode errMsg:(nullable NSString *)errMsg {
    if (errCode != 0) {
        NSLog(@"Switching operation failed... ");
    }   
}
:::
::: Windows C++
// 現在のロールが視聴者(Audience)の場合は、最初にswitchRoleを呼び出してキャスター(Anchor)に切り替えてください
// If your current role is 'audience', you need to call switchRole to switch to 'anchor' first
trtc_cloud_->switchRole(liteav::TRTCRoleAnchor);
trtc_cloud_->startLocalAudio(TRTCAudioQualityDefault);
trtc_cloud_->startLocalPreview(hWnd);

// ロールの切り替えに失敗した場合、onSwitchRoleコールバックのエラーコードはERR_NULL（すなわち、0）ではありません
// If switching operation failed, the error code of the 'onSwitchRole' is not zero
void onSwitchRole(TXLiteAVError errCode, const char* errMsg) {
    if (errCode != ERR_NULL) {
        printf("Switching operation failed...");
    }
}
:::
</dx-codeblock>

**注：**ルームにキャスターが多すぎると、switchRoleはロールの切り替えに失敗し、エラーコードがTRTCのonSwitchRoleを介して通知されます。したがって、オーディオビデオストリームをリリースする必要がなくなったら（「マイク・オフ」とも呼ばれる）、switchRoleを再度呼び出して、「視聴者(Audience)」に切り替えてください。

>? 質問がある場合があるかもしれませんが、オーディオビデオストリームをリリースできるのはキャスターなら、すべてのユーザーにキャスターのロールで入室させることはできますか？答えは間違いなく「いいえ」です。その理由については、[1つのルームに同時に存在するオーディオとビデオのチャネルはいくつですか？](#speed1)ドキュメントをご参照ください。

## 拡張機能ガイド

[](id:speed1)
### 1. 1つのルームに同時に存在するオーディオとビデオのチャネルはいくつですか？
1つのTRTCルームに最大**50**チャネルのオーディオビデオストリームが同時に許可されます。「先着順」の原則に従って、余分なオーディオビデオストリームは破棄されます。
大部分のシーンでは、2人の間のビデオ通話から、数万人が同時に視聴するオンラインライブストリーミングまで、50のオーディオビデオストリームがユースケースのニーズを満たすことができますが、**ロール管理**を適切に行うことが前提です。

いわゆる「ロール管理」とは、入室するユーザーにロールをアサインする必要があるということです。
- ユーザー自体は、ライブストリーミングシーンの「キャスター」、またはオンライン教育シーンの「教師」、またはオンライン会議シーンの「ホスト」である場合、そのユーザーに「キャスター（Anchor）」のロールをアサインすることができます。
- ユーザー自体は、ライブストリーミングシーンの「視聴者」、またはオンライン教育シーンの「学生」、またはオンライン会議シーンの「オーディエンス」である場合、「視聴者」のロールをアサインする必要があります。そうしないと、膨大な数の人々が即時キャスターの制限数を「絞り出します」。

「視聴者」がオーディオビデオストリームをリリースする必要がある（「マイク・オン」）場合にのみ、switchRoleを介して「キャスター」のロールに切り替える必要があります。オーディオビデオストリームをリリースする必要がなくなった（「マイク・オフ」）場合は、すぐ視聴者のロールに戻してください。

合理的なロール管理により、通常、ルームでオーディオビデオストリームを同時にリリースする必要のある「キャスター」は50人以下であることがわかります。そうしないと、ルーム全体が「乱雑」になります。同時音声数が6チャンネルを超えると、一般の人が現在音声から話している相手を特定することは困難です。









