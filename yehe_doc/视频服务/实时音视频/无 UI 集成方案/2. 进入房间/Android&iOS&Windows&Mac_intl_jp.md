このドキュメントでは、主にTRTCルームに入る方法を紹介します。オーディオビデオルームに入った後でのみ、ユーザーはルーム内の他のユーザーのオーディオビデオストリームをサブスクリプションしたり、自分のオーディオビデオストリームをルーム内の他のユーザーに公開したりできます。
![](https://qcloudimg.tencent-cloud.cn/raw/6000fddd57940b43688685b247941fbf.png)

## 呼び出しガイド

[](id:step1)
### 手順1：SDKをインポートし、Appの権限を設定します
[SDKのプロジェクトへのインポート](https://intl.cloud.tencent.com/document/product/647/35092)を参照して、SDKをインポートします。

[](id:step2)
### 手順2：SDKインスタンスを作成し、イベント監視装置（リスナー）を設定します
各プラットフォームの初期化インターフェースを呼び出して、TRTCのオブジェクトインスタンスを作成します。
<dx-codeblock>
::: Android java
// SDKインスタンス（シングルトンモード）を作成し、イベント監視装置（リスナー）を設定します
// Create trtc instance(singleton)  and set up event listeners
mCloud = TRTCCloud.sharedInstance(getApplicationContext());
mCloud.setListener(this);
:::
::: iOS&Mac ObjC
// SDKインスタンス（シングルトンモード）を作成し、イベント監視装置（リスナー）を設定します
// Create trtc instance(singleton)  and set up event listeners
_trtcCloud = [TRTCCloud sharedInstance];
_trtcCloud.delegate = self;
:::
::: Windows C++
// SDKインスタンス（シングルトンモード）を作成し、イベント監視装置（リスナー）を設定します
// Create trtc instance(singleton)  and set up event listeners
trtc_cloud_ = getTRTCShareInstance();
trtc_cloud_->addCallback(this);
:::
</dx-codeblock>

[](id:step3)
### 手順3：SDKイベントを監視します
イベントコールバックインターフェイスを設定することにより、SDKの実行中に発生するエラー情報、警告情報、トラフィック統計情報、ネットワーク品質情報、およびさまざまなオーディオビデオイベントを監視できます。
<dx-codeblock>
::: Android
独自のクラスに**TRTCCloudListener**を継承させ、onError関数をオーバーロードし、最後に** setListener **インターフェイスを介してthisポインターをSDKに設定して、現在のクラスでSDKからのコールバックイベントを監視できます。
```java
// SDKイベントを監視し、「カメラが許可されていません」などのエラーログを印刷します
// Listen to the "onError" event and print logs for errors such as "camera is not authorized"
mCloud = TRTCCloud.sharedInstance(getApplicationContext());
mCloud.setListener(this);

@Override
public void onError(int errCode, String errMsg, Bundle extraInfo) {
    if (errCode == TXLiteAVCode.ERR_CAMERA_NOT_AUTHORIZED) {
        Log.d(TAG, "Current application is not authorized to use the camera");
    }
}
```
:::
::: iOS&Mac ObjC
独自のクラスに**TRTCCloudDelegate**を継承させ、onError関数をオーバーロードし、最後にTRTCCCloudの**delegate**属性を介してthisポインターをSDKに設定して、現在のクラスでSDKからのコールバックイベントを監視できます。
```ObjectiveC
// SDKイベントを監視し、「カメラが許可されていません」などのエラーログを印刷します
// Listen to the "onError" event and print logs for errors such as "camera is not authorized"
_trtcCloud = [TRTCCloud sharedInstance];
_trtcCloud.delegate = self;

- (void)onError:(TXLiteAVError)errCode
         errMsg:(nullable NSString *)errMsg
        extInfo:(nullable NSDictionary *)extInfo{
    if (ERR_CAMERA_NOT_AUTHORIZED == errCode) {
        NSString *errorInfo = @"Current application is not authorized to use the camera：";
        errorInfo = [errorInfo stringByAppendingString errMsg];
        [self toastTip:errorInfo];
    }
}
```
:::
::: Windows C++
独自のクラスに**ITRTCCloudCallback**を継承させ、onError関数をオーバーロードし、最後に**addCallback**インターフェイスを介してthisポインターをSDKに設定して、現在のクラスでSDKからのコールバックイベントを監視できます。
```C++
// SDKイベントを監視し、「カメラが許可されていません」などのエラーログを印刷します
// Listen to the "onError" event and print logs for errors such as "camera is not authorized"
trtc_cloud_ = getTRTCShareInstance();
trtc_cloud_->addCallback(this);

// "onError」関数をオーバーロードします
void onError(TXLiteAVError errCode, const char* errMsg, void* extraInfo) {
    if (errCode == ERR_CAMERA_NOT_AUTHORIZED) {
        printf("Current application is not authorized to use the camera");
    }
}
```
:::
</dx-codeblock>

[](id:step4)
### 手順4：入室パラメータTRTCParamsを準備します
enterRoomインターフェースを呼び出すとき、2つの主要なパラメーター、つまり`TRTCParams`と`TRTCAppScene`を入力してください。これらについては、以下で詳しく説明します：

#### パラメータ1：TRTCAppScene
このパラメータは、ユースケース、つまり**オンラインライブストリーミング**または**リアルタイム通話**を指定するために使用されます：
- **リアルタイム通話：**
`TRTCAppSceneVideoCall`と`TRTCAppSceneAudioCall`の2つのオプションがあり、それぞれビデオ通話と音声通話です。このモードは、1対1のオーディオビデオ通話、または参加者が300人未満のオンライン会議に適しています。

- **オンラインライブストリーミング：**
`TRTCAppSceneLIVE`と`TRTCAppSceneVoiceChatRoom`の2つのオプションがあり、それぞれビデオライブストリーミングとオーディオライブストリーミングです。このモードは、10万人未満のオンラインライブストリーミングシナリオに適していますが、以下に説明するTRTCParamsパラメータで**ロール（role）**のフィールドを指定する必要があります。つまり、ルーム内のユーザーは、**ホスト(anchor)**と**視聴者(audience)**の2つの異なる役割に分けられます。

#### パラメータ2：TRTCParams
TRTCParamsは多くのフィールドで構成されていますが、通常は次のフィールドへの入力のみを気にしてください：

| パラメータ名 | フィールドの意味 | 補足説明 | データのタイプ |記入例 |
|---------|---------|---------|---------|---------|
| SDKAppID | アプリケーションID | このSDKAppIDは<a href="https://console.cloud.tencent.com/trtc/app">Tencent Real-Time Communicationコンソール</a>にあります。見つからない場合は、「アプリケーションの作成」ボタンをクリックして新しいアプリケーションを作成してください。| 数字 | 1400000123 |
| userId | ユーザーID | すなわちユーザー名です。大文字と小文字の英字（a-z、A-Z）、数字（0-9）、アンダースコア、およびハイフンのみが許可されます。TRTCは、2つの異なるデバイスで同時に入室する同じuserIdをサポートしていないことに注意してください。そうでない場合には、互いに干渉します。| 文字列 | 「denny」または「123321」|
| userSig | 入室認証証明書 | SDKAppIDとuserIdを使用してuserSigを計算できます。計算方法については、[UserSigの計算と使用](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください 。|文字列| eJyrVareCeYrSy1SslI... |
| roomId | ルーム番号 | 数値タイプのルーム番号。strRoomIdとroomIdを混在させることはできないため、文字列タイプのルーム番号を使用する場合は、roomIdフィールドの代わりに**strRoomId**フィールドを使用することに注意してください。| 数字 | 29834 |
| strRoomId | ルーム番号 | 文字列タイプのルーム番号。strRoomIdとroomIdを混在させることはできません。「123」と123は、TRTCバックグラウンドサービスの同じ部屋ではありません。。  | 数字 | 29834 |
| role | ロール | 「キャスター」と「視聴者」の2つの役割に分かれています。このフィールドは、TRTCAppSceneが`TRTCAppSceneLIVE`または`TRTCAppSceneVoiceChatRoom`として指定されている場合にのみ指定してください。| 列挙値 | TRTCRoleAnchorまたはTRTCRoleAudience   |

>!
>- TRTCは、2つの異なるデバイスで同時に入室する同じuserIdをサポートしません。そうでない場合には、互いに干渉します。
>- 各端末のユースケースappSceneについては、統一してください。統一していない場合、想定外のトラブルが生じる恐れがあります。


[](id:step5)
### 步骤5：入室（enterRoom）
手順4の2つのパラメーター（TRTCAppSceneとTRTCParams）を準備した後、enterRoomインターフェース関数を呼び出して入室できます。

<dx-codeblock>
::: Android  Java
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

::: iOS&Mac  objectivec
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
trtc_cloud_->addCallback(this);

// TRTC入室パラメータを組み立てるには、TRTCParamsの各フィールドを独自のパラメータに置き換えてください
// Please replace each field in TRTCParams with your own parameters
liteav::TRTCParams params;
params.sdkAppId = 1400000123;  // Please replace with your own SDKAppID
params.userId = "denny";       // Please replace with your own userid  
params.roomId = 123321;        // Please replace with your own room number
params.userSig = "xxx";        // Please replace with your own userSig
params.role = liteav::TRTCRoleAnchor;

// 「オンラインライブストリーミング」のシーンの場合、ユースケースをTRTC_APP_SCENE_LIVEに設定してください
// If your application scenario is a video call between several people, please use "TRTC_APP_SCENE_LIVE"
trtc_cloud_->enterRoom(params, liteav::TRTCAppSceneLIVE);        
:::
</dx-codeblock>

**イベントコールバック**
正常に成功したら、SDKはonEnterRoom (result)イベントをコールバックします。ここで、resultは、入室にかかった時間をミリ秒(ms)の単位で表す0より大きい値になります。
入室に失敗したら、SDKはonEnterRoom(result)イベントもコールバックしますが、パラメータ`result`は負の数になり、その値は入室失敗のエラーコードです。
<dx-codeblock>
::: Android Java
// SDKのonEnterRoomイベントを監視し、入室に成功したかどうかを確認します
// Listen to the onEnterRoom event of the SDK and learn whether the room is successfully entered
@Override
public void onEnterRoom(long result) {
    if (result > 0) {
        Log.d(TAG, "Enter room succeed");
    }else{
        Log.d(TAG, "Enter room failed");
    }
}
:::
::: iOS&Mac ObjC
// SDKのonEnterRoomイベントを監視し、入室に成功したかどうかを確認します
// Listen to the onEnterRoom event of the SDK and learn whether the room is successfully entered
- (void)onEnterRoom:(NSInteger)result {
    if (result > 0) {
        [self toastTip:@"Enter room succeed!"];
    }else{
        [self toastTip:@"Enter room failed!"];
    }
}
:::
::: Windows C++
// SDKのonEnterRoomイベントを監視し、入室に成功したかどうかを確認します
// override to the onEnterRoom event of the SDK and learn whether the room is successfully entered
void onEnterRoom(int result) {
    if (result > 0) {
        printf("Enter room succeed");
    }else{
        printf("Enter room failed");
    }
}
:::
</dx-codeblock>
