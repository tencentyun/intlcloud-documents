## 適用ケース
TRTCは、4種類の異なる入室モードをサポートしています。このうち、ビデオ通話（VideoCall）および音声通話（VoiceCall）を総称して通話モードといい、ビデオ・インタラクティブストリーミング（Live）およびボイス・インタラクティブストリーミング（VoiceChatRoom）を総称して [ライブストリーミングモード](https://intl.cloud.tencent.com/document/product/647/35107)といいます。
通話モードでのTRTCは、1つのルームに最大で300人の同時オンラインをサポートし最大で50人の同時発言をサポートします。1対1のビデオ通話、300人のビデオミーティング、オンライン問診、リモート面接、ビデオカスタマーサービス、オンライン人狼ゲームなどのユースケースに適合しています。

## 原理解析
TRTCクラウドサービスは、「インターフェースモジュール」および「プロキシモジュール」という2種類の異なるタイプのサーバーノードから構成されています。
-   **インターフェースモジュール**
この種のノードは、最も良質の回線および高性能の機器を採用しており、エンドツーエンドの低遅延マイク接続通話の処理に優れますが、単位時間当たりの費用はやや高くなります
-   **プロキシモジュール**
この種のノードは、通常の回線および性能も一般的な機器を採用しており、同時進行性の高いプルストリーミング再生のニーズの処理にすぐれ、単位当たりの費用はやや低くなります。

通話モードでは、TRTCルームのすべてのユーザーはインターフェースモジュールに割り当てられます。各ユーザーは「キャスター」に相当し、各ユーザーは随時発言でき（同時アップストリームの最大制限は50）、このためオンラインミーティングなどのユースケースに適していますが、1つのルームの人数制限は300人になります。
![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## サンプルコード
[Github](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTC-API-Example-OC)にログインし、本ドキュメントに関連するサンプルコードを取得することができます。
![](https://main.qcloudimg.com/raw/468128bcaf078183eed097f7ee5f9c21.png)

>Githubへのアクセスが遅い場合は、[TXLiteAVSDK_TRTC_iOS_latest.zip](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_iOS_latest.zip)を直接ダウンロードすることもできます。

## 操作手順
[](id:step1)
### 手順1：SDKへの統合
以下の方式を選択して **TRTC SDK** をプロジェクトに統合することができます。
#### 方法1： CocoaPodsを使用して統合
1. **CocoaPods**をインストールします。具体的な操作は [CocoaPods公式サイトインストールの説明](https://guides.cocoapods.org/using/getting-started.html)をご参照ください。
2. 現在の項目ルートディレクトリの`Podfile`ファイルを開き、以下のコンテンツを追加します。
>?このディレクトリに`Podfile`ファイルがない場合は、まず`pod init`コマンドを実行しファイルを新規作成してから、以下の内容を追加してください。
>
```
target 'Your Project' do
        pod 'TXLiteAVSDK_TRTC'
end
```
3. 以下のコマンドを実行して **TRTC SDK** をインストールします。
```
pod install
```
インストールが成功したら、現在の項目ルートディレクトリに **xcworkspace** ファイルが生成されます。
4. 新規作成した **xcworkspace** ファイルを開けばOKです。

#### 方法2：ZIPパッケージをダウンロードして手動で統合
一時的にCocoaPods環境をインストールしたくない場合、またはインストール済みだがCocoaPodsライブラリへのアクセスがやや遅い場合は、 [ZIP圧縮パッケージ](https://intl.cloud.tencent.com/document/product/647/34615)を直接ダウンロードして、[クイックインテグレーション(iOS)](https://intl.cloud.tencent.com/document/product/647/35092)を参照してSDKをプロジェクトに統合することができます。

[](id:step2)
### 手順2：メディアデバイスの権限追加
`Info.plist`ファイルにカメラおよびマイクのアクセス許可のリクエストを追加します。

| Key | Value |
|---------|---------|
| Privacy - Camera Usage Description | カメラ使用の許可をリクエストする理由を記述。例えば、ビデオチャットでビデオを表示するには、カメラへのアクセスが必要です |
| Privacy - Microphone Usage Description | マイク使用の許可をリクエストする理由を記述。例えば、チャットで音声を送信するには、マイクへのアクセスが必要です |

[](id:step3)
### 手順3：SDKインスタンスを初期化し、イベントコールバックを監視する

1. [sharedInstance()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab6884975e069628328d05cf0e2c3dc67)インターフェースを使用して、`TRTCCloud`インスタンスを作成します。
```
// trtcCloudインスタンスを作成
_trtcCloud = [TRTCCloud sharedInstance];
_trtcCloud.delegate = self;
```
2. `delegate`属性を設定しイベントのコールバックを登録し、関連イベントおよびエラー通知をモニタします。
<dx-codeblock>
::: iOS object-c
// エラー通知は監視すべきもので、捕捉してユーザーに通知する必要があります
- (void)onError:(TXLiteAVError)errCode errMsg:(NSString *)errMsg extInfo:(NSDictionary *)extInfo {
    if (ERR_ROOM_ENTER_FAIL == errCode) {
        [self toastTip:@"入室失敗"];
        [self.trtcCloud exitRoom];
    }
}
:::
</dx-codeblock>

[](id:step4)
### 手順4：入室パラメータTRTCParamsを組み立てる
[enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)インターフェースを呼び出す時に、キーパラメータ[TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams)を入力する必要があります。このパラメータに含まれる入力必須のフィールドは下表に示すとおりです。

| パラメータ名 | フィールドタイプ | 補足説明 |記入例 |
|---------|---------|---------|---------|
| sdkAppId | 数字 | アプリケーションID。<a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a>でSDKAppIDを表示できます。|1400000123 |
| userId | 文字列 | アルファベットの大文字、小文字（a-z、A-Z）、数字（0-9）、下線およびハイフンのみを許可。 | test_user_001 |
| userSig | 文字列 | userIdを基にuserSigを計算します。計算方法は[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。| eJyrVareCeYrSy1SslI... |
| roomId | 数字 | デフォルトでは文字列のタイプのルームナンバーをサポートしていません、文字列タイプのルームナンバーは入室速度に影響します。文字列タイプのルームナンバーをサポートする必要が確実にある場合は、 [チケットを提出](https://console.cloud.tencent.com/workorder/category) してご連絡ください。 | 29834 |

>! TRTCは、2つの同じuserIdによる同時入室をサポートしていません。同時に入室した場合は相互に干渉します。

[](id:step5)
### 手順5：ルームの新規作成および入室
1. [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)を呼び出せば、TRTCParamsパラメータの`roomId`が示すオーディオ・ビデオルームに入室できます。該当するルームが存在しない場合は、SDKがフィールド`roomId`の値をルームナンバーとする新しいルームを自動的に作成します。
2. ユースケースに基づき適切な**`appScene`**パラメータを設定してください。誤った選択をすると、ラグ率または画面の解像度が想定レベルに到達しなくなります。
 - ビデオ通話は、`TRTCAppScene.videoCall`に設定してください。
 - 音声通話は、`TRTCAppScene.audioCall`に設定してください。
3. 入室に成功したら、SDKは`onEnterRoom(result)`イベントをコールバックします。そのうち、パラメータ`result`が0より大きいときは入室成功を示し、具体的な数値は入室のために消費した時間になります。単位はミリ秒（ms）です。`result`が0より小さいときは入室失敗を示し、具体的な数値は入室失敗のエラーコードになります。

<dx-codeblock>
::: iOS object-c
- (void)enterRoom() {
    TRTCParams *params = [TRTCParams new];
    params.sdkAppId = SDKAppID;
    params.roomId = _roomId;
    params.userId = _userId;
    params.role = TRTCRoleAnchor;
    params.userSig = [GenerateTestUserSig genTestUserSig:params.userId];
    [self.trtcCloud enterRoom:params appScene:TRTCAppSceneVideoCall];
}

- (void)onEnterRoom:(NSInteger)result {
    if (result > 0) {
        [self toastTip:@"入室成功"];
    } else {
        [self toastTip:@"入室失敗"];
    }
}
:::
</dx-codeblock>

>! 
>- 入室に失敗した場合は、SDKは同時に`onError`イベントもコールバックし、パラメータ`errCode`（[エラーコード](https://intl.cloud.tencent.com/document/product/647/35124)）、`errMsg`（エラー原因）および`extraInfo`（保留パラメータ）を返します。
>- すでに特定のルームにいる場合は、まず`exitRoom()`を呼び出して現在のルームを退出すると、もう一つのルームに入ることができるようになります。
>- 各端末のユースケースappSceneについては、統一する必要があります。統一していない場合、想定外のトラブルが生じる恐れがあります。

[](id:step6)
### 手順6：リモート側のオーディオビデオストリーミングの閲覧
SDKは自動閲覧および手動閲覧をサポートします。

#### 自動閲覧モード（デフォルト）
自動閲覧モードでは、特定のルームに入った後、SDKはルームのその他のユーザーのオーディオストリームを自動で受信します。これによって最適な「インスタントブロードキャスティング効果が得られます。
1. ルーム内の他のユーザーがオーディオデータをアップストリームすると、[onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5)のイベント通知を受信して、SDKがそのリモートユーザーの音声を自動再生します。
2. [muteRemoteAudio(userId, mute: true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afede3cc79a8d68994857b410fb5572d2)によって、特定のuserIdのオーディオデータを遮断することができ、[muteAllRemoteAudio(true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a75148bf8a322c852965fe774cbc7dd14)によって、すべてのリモートユーザーのオーディオデータを遮断することもできます。遮断後、SDKは、当該リモートユーザーのオーディオデータをそれ以降プルしなくなります。
3. ルームのその他のユーザーがビデオデータをアップストリームすると、[onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80)のイベント通知を受信しますが、このとき、SDKは、ビデオデータをどのように表示するかの指令を受け取っていないため、ビデオデータを自動処理しません。[startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49)メソッドを呼び出し、リモートユーザーのビデオデータと`view`（表示）を関連付けする必要があります。
4. [setRemoteViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afda6658d1bf7dc9bc1445838b95d21ff)によって、ビデオ画面の表示モードを指定することができます。
 - Fillモード：塗りつぶしを意味し、画面は同じ比率で拡大およびトリミングできますが、黒い縁取りは付きません。
 - Fitモード：適応を意味し、画面は同じ比率で縮小してスクリーンにフィットしてそのコンテンツを完全に表示しますが、黒い縁取りが付くことがあります。
5. [stopRemoteView(userId)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2b7e96e4b527798507ff743c61a6a066)によって、特定のuserIdのビデオデータを遮断することができ、また[stopAllRemoteView()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aaa75cd1b98c226bb7b8a19412b204d2b)によって、すべてのリモートユーザーのビデオデータを遮断することもできます。遮断後、SDKは、当該リモートユーザーのビデオデータをそれ以降プルしなくなります。

<dx-codeblock>
::: iOS object-c
// インスタンスコード：通知に基づきリモート側ユーザーのビデオ画面を閲覧（または閲覧の取り消し）します。
- (void)onUserVideoAvailable:(NSString *)userId available:(BOOL)available {
    UIView* remoteView = remoteViewDic[userId];
    if (available) {
        [_trtcCloud startRemoteView:userId streamType:TRTCVideoStreamTypeSmall view:remoteView];
    } else {
        [_trtcCloud stopRemoteView:userId streamType:TRTCVideoStreamTypeSmall];
    }
}
:::
</dx-codeblock>

>? `onUserVideoAvailable()`イベントのコールバック受信した後、すぐに`startRemoteView()`を呼び出してビデオストリームを閲覧しない場合、SDKが5s以内にリモートからのビデオデータの受信を停止します。

#### 手動閲覧モード
[setDefaultStreamRecvMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ada2e2155e0e7c3001c6bb6dca1d93048)インターフェースによって、SDKを手動閲覧モードに指定できます。手動閲覧モードでは、SDKはルーム内の他のユーザーの音声・ビデオデータを自動受信しません。手動で、API関数を介してトリガーする必要があります。

1. **入室前**に、[setDefaultStreamRecvMode(false, video: false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ada2e2155e0e7c3001c6bb6dca1d93048)インターフェースを呼び出して、SDKを手動閲覧モードに設定します。
2. ルーム内の他のユーザーがオーディオデータをアップストリームすると、[onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5)のイベント通知を受信します。この時、[muteRemoteAudio(userId, mute: false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afede3cc79a8d68994857b410fb5572d2)メソッドを呼び出すことで、そのユーザーのオーディオデータを手動で閲覧する必要があります。SDKはそのユーザーのオーディオデータを受信した後、デコードして再生します。
3. ルーム内の他のユーザーがビデオデータをアップストリームすると、[onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80)イベントの通知を受信します。この時は、[startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49)メソッドを呼び出すことで、そのユーザーのビデオデータを手動で閲覧する必要があります。SDKが、そのユーザーのビデオデータを受信後、デコードして再生します。

[](id:step7)
### 手順7：ローカルのオーディオビデオストリーミングの公開
1. [startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3177329bc84e94727a1be97563800beb)を呼び出すと、ローカルのマイク集音を起動させ、採集した音声をエンコードして送信することができます。
2. [startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3fc1ae11b21944b2f354db258438100e)を呼び出すと、ローカルのカメラを起動させ、キャプチャした画面をエンコードして送信することができます。
3. [setLocalViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a961596f832657bfca81fd675878a2d15)を呼び出すと、ローカルのビデオ画面の表示モードを設定することができます。
 - Fillモードは塗りつぶしを意味し、画面は同じ比率で拡大およびトリミングできますが、黒い縁取りは付きません。
 - Fitモードは適応を意味し、画面は同じ比率で縮小してスクリーンにフィットしてそのコンテンツを完全に表示しますが、黒い縁取りが付くことがあります。
4. [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e)インターフェースを呼び出すと、ローカルビデオのエンコードパラメータを設定できます。このパラメータにより、ルーム内の他のユーザーが視聴する際の画面の[画質](https://intl.cloud.tencent.com/document/product/647/35153)が決定されます。

<dx-codeblock>
::: iOS object-c
//サンプルコード：ローカルのオーディオビデオストリーミングの公開
[self.trtcCloud startLocalPreview:_isFrontCamera view:self.view];
[self.trtcCloud startLocalAudio:TRTCAudioQualityMusic];
:::
</dx-codeblock>

>! Mac版SDKは、デフォルトでは、現在のシステムのデフォルトのカメラおよびマイクを使用します。[setCurrentCameraDevice()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aae9955bb39985586f7faba841d2692fc)および[setCurrentMicDevice()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5141fec83e7f071e913bfc539c193ac6)を呼び出すことで、その他のカメラおよびマイクを選択することができます。

[](id:step8)
### 手順8：現在のルームから退出する

[exitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a715f5b669ad1d7587ae19733d66954f3)メソッドを呼び出してルームを退出します。SDKは退室する時に、カメラ、マイクなどのハードウェアデバイスを停止してリリースする必要があるたため、退室の動作は瞬時に完了するものではなく、[onExitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a6a98fcaac43fa754cf9dd80454897bea)のコールバックを受信してはじめて、実際の退室操作が完了します。

<dx-codeblock>
::: iOS object-c
// 退室を呼び出した後は、onExitRoomイベントのコールバックをお待ちください
[self.trtcCloud exitRoom];

- (void)onExitRoom:(NSInteger)reason {
    NSLog(@"ルームから退出: reason: %ld", reason)
}
:::
</dx-codeblock>

>! Appの中で多くの音声ビデオのSDKを同時に統合した場合は、`onExitRoom`コールバックを受信してからその他の音声ビデオSDKを起動してください。そうしない場合は、ハード上の占有問題が生じることがあります。
