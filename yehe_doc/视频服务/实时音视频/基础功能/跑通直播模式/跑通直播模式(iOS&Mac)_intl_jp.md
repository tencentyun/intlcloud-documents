## ユースケース
TRTCは、4種類の異なる入室モードをサポートしています。このうち、ビデオ通話（VideoCall）および音声通話（VoiceCall）を総称して[通話モード](https://intl.cloud.tencent.com/document/product/647/35102)といい、ビデオ・インタラクティブストリーミング（Live）およびボイス・インタラクティブストリーミング（VoiceChatRoom）を総称してライブストリーミングモードといいます。
ライブストリーミングモードでのTRTCは、1つのルームで最大10万人の同時接続をサポートし、300ms未満のマイク接続遅延、1000ms未満の視聴遅延およびマイクのオン・オフのスムーズな切り替え技術を備えています。低レイテンシーインタラクティブストリーム、10万人のインタラクティブ教室、ビデオ婚活、eラーニング、リモート研修、超大規模ミーティングなどのユースケースに適しています。

## 原理解析
TRTCクラウドサービスは、「インターフェースモジュール」および「プロキシモジュール」という2種類の異なるタイプのサーバーノードから構成されています。
-   **インターフェースモジュール**
この種のノードは、最も良質の回線および高性能の機器を採用しており、エンドツーエンドの低遅延マイク接続通話の処理に優れています。
-   **プロキシモジュール**
この種のノードは、通常の回線および性能も一般的な機器を採用しており、同時進行性の高いプルストリーミング再生ニーズの処理にすぐれています。

ライブストリーミングモードでは、TRTCはロールのコンセプトを導入し、ユーザーは「キャスター」および「視聴者」の2種類のロールに分けられ、「キャスター」はインターフェースモジュールに配分され、「視聴者」はプロキシモジュールに分配されます。同一ルームの視聴者の上限は10万人です。
「視聴者」をマイク・オンにしたい場合、まずロール（switchRole）を「キャスター」に切り替えると発言できます。ロールを切り替えることで、ユーザーをプロキシモジュールからインターフェースモジュールに移動させ、TRTC特有の低遅延視聴技術およびスムーズなマイクのオン/オフ切替技術によって、すべての切り替え時間を非常に短くすることができます。

![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## サンプルコード
[Github](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTC-API-Example-OC) にログインし、本ファイルに関連するサンプルコードを取得することができます。
![](https://main.qcloudimg.com/raw/91ba84ef5cee887717ba69e97d939fcd.png)

>Githubへのアクセスが遅い場合は、[TXLiteAVSDK_TRTC_iOS_latest.zip](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_iOS_latest.zip)を直接ダウンロードすることもできます。


## 操作手順
[](id:step1)
### 手順1：SDKの統合 
以下の方式を選択して **TRTC SDK** をプロジェクトに統合することができます。
#### 方法1： CocoaPodsを使用して統合
1. **CocoaPods**をインストールします。具体的な操作は [CocoaPods公式サイトインストールの説明](https://guides.cocoapods.org/using/getting-started.html)をご参照ください。
2. 現在のプロジェクトのルートディレクトリの`Podfile`ファイルを開き、以下のコンテンツを追加します。
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
インストールが成功したら、現在のプロジェクトのルートディレクトリに **xcworkspace** ファイルが生成されます。
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

1. [sharedInstance()](https://intl.cloud.tencent.com/document/product/647/35119) インターフェースを使用して`TRTCCloud`インスタンスを作成します。
<dx-codeblock>
::: iOS object-c
// trtcCloudインスタンスを作成
_trtcCloud = [TRTCCloud sharedInstance];
_trtcCloud.delegate = self;
:::
</dx-codeblock>
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
| userId | 文字列 | アルファベットの大文字、小文字（a-z、A-Z）、数字（0-9）、下線およびハイフンのみを許可。ビジネスの実際のアカウントシステムを組み合わせて設定することをお勧めします。 | test_user_001 |
| userSig | 文字列 | userIdを基にuserSigを計算します。計算方法は[UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。| eJyrVareCeYrSy1SslI... |
| roomId | 数字 | 数字タイプのルームナンバー。文字列形式のルームナンバーを使用したい場合は、TRTCParamsのstrRoomIdをご使用ください。 | 29834 |

>! 
>- TRTCは、2つの同じuserIdによる同時入室をサポートしていません。同時に入室した場合、相互に干渉します。
>- 各端末のユースケースappSceneについては、統一する必要があります。統一していない場合、想定外のトラブルが生じる恐れがあります。


[](id:step5)
### 手順5：キャスター端末でのカメラのプレビューとマイク集音を起動する
1. キャスター側は、[startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3fc1ae11b21944b2f354db258438100e)を呼び出すと、ローカルのカメラのプレビューを起動することができ、SDKがシステムにカメラの使用許可をリクエストします。
2. キャスター側は、[setLocalViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a961596f832657bfca81fd675878a2d15)を呼び出すと、ローカルのビデオ画面の表示モードを設定することができます。
 - Fillモードは塗りつぶしを意味し、画面は同じ比率で拡大およびトリミングできますが、黒い縁取りは付きません。
 - Fitモードは適応を意味し、画面は同じ比率で縮小してスクリーンにフィットしてそのコンテンツを完全に表示しますが、黒い縁取りが付くことがあります。
3. キャスター側は、[setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e)インターフェースを呼び出すと、ローカルビデオのエンコードパラメータを設定できます。このパラメータにより、ルーム内の他のユーザーが視聴する際の画面の[画質](https://intl.cloud.tencent.com/document/product/647/35153)が決定されます。
4. キャスター側は、[startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3177329bc84e94727a1be97563800beb)を呼び出すと、マイクを起動でき、SDKがシステムにマイクの使用許可をリクエストします。

<dx-codeblock>
::: iOS object-c
//サンプルコード：ローカルのオーディオ・ビデオストリーミングの公開
[self.trtcCloud startLocalPreview:_isFrontCamera view:self.view];

//ローカルビデオコーデックパラメータの設定
TRTCVideoEncParam *encParams = [TRTCVideoEncParam new];
encParams.videoResolution = TRTCVideoResolution_640_360;
encParams.videoBitrate = 550;
encParams.videoFps = 15;
    
[self.trtcCloud setVideoEncoderParam:encParams];
:::
</dx-codeblock>

[](id:step6)
### 手順6：キャスター端末により美顔エフェクトを設定する

1.キャスター側は、[getBeautyManager()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4fb05ae6b5face276ace62558731280a)を呼び出すと、美顔設定インターフェース[[TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#interfaceTXBeautyManager)を取得できます。
2. キャスター側は、[setBeautyStyle()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#a8f2378a87c2e79fa3b978078e534ef4a)を呼び出すと、美顔スタイルを設定できます。
 - Smooth：スムース。明らかな効果が感じられます。インフルエンサーのスタイルに近づけます。
 - Nature：ナチュラル。美肌補正のアルゴリズムは顔の詳細な質感を維持し、より自然な感じになります。
 - Pitu ：[エンタープライズ版](https://intl.cloud.tencent.com/document/product/647/34615#Enterprise) のみサポートしています。
3. キャスター側は、[setBeautyLevel()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#af864d9466d5161e1926e47bae0e3f027)を呼び出すと、美肌補正レベルを設定できます。通常、5の設定でOKです。
4. キャスター側は、[setWhitenessLevel()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#a199b265f6013e0cca0ff99f731d60ff4)を呼び出すと、美白レベルを設定できます。通常、5の設定でOKです。
5.iPhoneのカメラの色調はデフォルトだと黄色味がかっているため、[setFilter()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a1b0c2a9e82a408881281c7468a74f2c0)を呼び出して、キャスターに美白特殊効果を追加することをお勧めします。美白特殊効果に対応するフィルターのファイルのダウンロードアドレスは、次となります。[フィルターファイル](https://liteav.sdk.qcloud.com/doc/res/trtc/filter/filterPNG.zip)。

[](id:step7)
### 手順7：キャスター端末からルームを新規作成し、プッシュを開始する
1. キャスター側は、[TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams)のフィールド`role`を **`TRTCRoleType.anchor`**に設定します。これは現在のユーザーのロールがキャスターであることを表します。
2. キャスター側は、[enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)を呼び出すと、TRTCParamsパラメータのフィールド`roomId`の値をルームナンバーとするオーディオ・ビデオルームを作成し、**`appScene`**パラメータを指定することができます。
 - TRTCAppScene.LIVE：ビデオ・インタラクティブストリーミングモード。ここではこのモードを例として取り上げます。
 - TRTCAppScene.voiceChatRoom：ボイス・インタラクティブストリーミングモード。
3. ルームの新規作成が成功すると、キャスター側は、音声ビデオデータのエンコードおよび伝送フローを開始します。同時にSDKが[onEnterRoom(result)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a6960aca54e2eda0f424f4f915908a3c5)  イベントをコールバックします。パラメータ`result`が0より大きいときは入室成功を意味し、具体的な数値は入室してからの消費時間であり、単位はミリ秒（ms）です；`result`が0より小さい時は入室失敗を意味し、具体的な数値は入室失敗のエラーコードになります。

<dx-codeblock>
::: iOS object-c
- (void)enterRoom() {
    TRTCParams *params = [TRTCParams new];
    params.sdkAppId = SDKAppID;
    params.roomId = _roomId;
    params.userId = _userId;
    params.role = TRTCRoleAnchor;
    params.userSig = [GenerateTestUserSig genTestUserSig:params.userId];
    [self.trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE];
}

- (void)onEnterRoom:(NSInteger)result {
    if (result > 0) {
        [self toastTip:@"入室成功"];
    }else{
        [self toastTip:@"入室失敗"];
    }
}
:::
</dx-codeblock>

[](id:step8)
### 手順8：視聴者が入室しライブストリーミングを視聴する
1. 視聴者側は、[TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams)のフィールド`role`を**`TRTCRoleType.audience`**に設定します。これは現在のユーザーのロールが視聴者であることを表します。
2. 視聴者側は、[enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)を呼び出すと、TRTCParamsパラメータのフィールド`roomId`が示すオーディオ・ビデオルームに入室し、**`appScene`**パラメータを指定することができます。
 - TRTCAppScene.LIVE：ビデオ・インタラクティブストリーミングモード。ここではこのモードを例として取り上げます。
 - TRTCAppScene.voiceChatRoom：ボイス・インタラクティブストリーミングモード。
3. キャスター画面の視聴：
 - 視聴者側が事前にキャスターのuserIdを知っている場合は、入室に成功した後、直接キャスターの`userId`を使用して[startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49)を呼び出せば、キャスターの画面を表示することができます。
 - 視聴者側がキャスターのuserIdを知らない場合は、視聴者側が、入室に成功すると[onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80)のイベント通知を受信しますので、コールバックにより受け取ったキャスター`userId`を使用して、[startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49)を呼び出せば、キャスターの画面を表示することができます。


[](id:step9)
### 手順9：視聴者とキャスターとのマイク接続
1. 視聴者側が[switch(TRTCRoleType.TRTCRoleAnchor)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5f4598c59a9c1e66938be9bfbb51589c)を呼び出し、ロールをキャスター（TRTCRoleType.TRTCRoleAnchor）に切り替えます。
2. 視聴者側が[startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3fc1ae11b21944b2f354db258438100e)を呼び出すと、ローカルの画面をアクティブにすることができます。
3. 視聴者側が[startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3177329bc84e94727a1be97563800beb)を呼び出すと、マイクの集音が開始されます。

<dx-codeblock>
::: iOS object-c
//サンプルコード：視聴者マイク・オン
[self.trtcCloud switchRole:TRTCRoleAnchor];
[self.trtcCloud startLocalAudio:TRTCAudioQualityMusic];
[self.trtcCloud startLocalPreview:_isFrontCamera view:self.view];

//サンプルコード：視聴者マイク・オフ
[self.trtcCloud switchRole:TRTCRoleAudience];
[self.trtcCloud stopLocalAudio];
[self.trtcCloud stopLocalPreview];
:::
</dx-codeblock>

[](id:step10)
### 手順10：キャスター間でルーム間マイク接続PKを行う

TRTCでは、異なるオーディオ・ビデオルームにいる2人のキャスターが当初のライブストリーミングルームを退出しない場合にも、「ルーム間通話」機能によってマイク接続通話機能をプルし、「ルーム間マイク接続PK」を行うことができます。

1.キャスターAが、[connectOtherRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a062bc48550b479a6b7c1662836b8c4a5)インターフェースを呼び出します。インターフェースパラメータは現在、JSON形式を採用しており、キャスターBの`roomId`と`userId`を接合して、形式が`{"roomId": "978","userId": "userB"}`となるパラメータをインターフェース関数に渡す必要があります。
2. クロスルームに成功すると、キャスターAは [onConnectOtherRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a69e5b1d59857956f736c204fe765ea9a)のイベントコールバックを受け取ります。同時に、2つのライブストリーミングルームのすべてのユーザーが[onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80)と[onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5)のイベント通知を受け取ります。
 例えば、ルーム「001」のキャスターAがルーム「002」のキャスターBと`connectOtherRoom()`を介してルーム間通話をする場合、ルーム「001」のユーザーはキャスターBの`onUserVideoAvailable(B, available: true)`コールバックと`onUserAudioAvailable(B, available: true)`コールバックを受信します。ルーム「002」のユーザーはキャスターAの`onUserVideoAvailable(A, available: true)`コールバックと`onUserAudioAvailable(A, available: true)`コールバックを受信します。
3. 2つのルームにいるユーザーは、[startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49)を呼び出すことで、もう一方のルームのキャスターの画面を表示することができ、音声が自動再生されます。

<dx-codeblock>
::: iOS object-c
//サンプルコード：ルーム間マイク接続PK
NSMutableDictionary * jsonDict = [[NSMutableDictionary alloc] init];
[jsonDict setObject:@([_otherRoomIdTextField.text intValue]) forKey:@"roomId"];
[jsonDict setObject:_otherUserIdTextField.text forKey:@"userId"];
NSData* jsonData = [NSJSONSerialization dataWithJSONObject:jsonDict options:NSJSONWritingPrettyPrinted error:nil];
NSString* jsonString = [[NSString alloc] initWithData:jsonData encoding:NSUTF8StringEncoding];
[self.trtcCloud connectOtherRoom:jsonString];
:::
</dx-codeblock>

[](id:step11)
### 手順11：現在のルームから退出する

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

