## 適用ケース
TRTC は、4種類の異なる入室モードをサポートしています。このうち、ビデオ通話（VideoCall）および音声通話（VoiceCall）を総称して[通話モード](https://intl.cloud.tencent.com/document/product/647/35102)といい、ビデオ・インタラクティブストリーミング（Live）およびボイス・インタラクティブストリーミング（VoiceChatRoom）を総称してライブストリーミングモードモードといいます。
ライブストリーミングモードでの TRTCは、1つのルームで最大10万人が同時にオンラインでつながるのをサポートし、300ms未満のマイク接続の遅延、1000ms未満の視聴遅延、およびマイクのオン・オフのスムーズな切り替え技術を備えています。低遅延のILVB、10万人のインタラクティブな授業、ビデオ婚活、eラーニング、リモート研修、超大型会議などのユースケースに適用しています。

## 原理解析
TRTC クラウドサービスは、2種類の異なるタイプのサーバーノードから構成されており、それぞれ“インターフェースモジュール”および“プロキシモジュール”からなっています。
- **インターフェースモジュール**
この種のノードは、最も良質の回線および高性能の機器を採用しており、エンドツーエンドの低遅延マイク接続通話の処理に優れますが、単位時間当たりの費用はやや高くなります
- **プロキシモジュール**
この種のノードは、通常の回線および性能も一般的な機器を採用しており、同時進行性の高いプルストリーミング再生のニーズの処理にすぐれ、単位当たりの費用はやや低くなります。

ライブストリーミングモードでは、TRTC はロールのコンセプトを導入し、ユーザーは「キャスター」および「視聴者」の2種類のロールに分けられ、「キャスター」はインターフェースモジュールに配分され、「視聴者」はプロキシモジュールに分配されます。同一ルームの視聴者の上限は10万人です。
「視聴者」をマイク・オンにしたい場合、まずロール（switchRole）を「キャスター」に切り替えると発言できます。ロールを切り替えることで、ユーザーをプロキシモジュールからインターフェースモジュールに移動させ、TRTC 特有の低遅延視聴技術およびスムーズなマイクのオン/オフ切替技術は、すべての切り替え時間を非常に短くすることができます。



## サンプルコード
 [Github]にログインし、本ファイルに関連するサンプルコードを取得することができます。
![](https://main.qcloudimg.com/raw/7c894fa62fdffe32db8f8d7979d27501.png)

>Githubへのアクセスが遅い場合は、 [TXLiteAVSDK_TRTC_iOS_latest.zip](http://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_iOS_latest.zip)を直接ダウンロードすることもできます。


## 操作手順
<span id="step1"> </span>
### 手順1： SDKへの統合
以下の方式を選択して **TRTC SDK** を項目に統合することができます。
#### 方法一： CocoaPods を使用して統合
1.  **CocoaPods**をインストールします。具体的な操作は [CocoaPods 公式サイトインストールの説明](https://guides.cocoapods.org/using/getting-started.html)をご参照ください。
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

#### 方法二：ZIP パッケージをダウンロードして手動で統合
一時的に CocoaPods 環境をインストールしたくない場合、またはインストール済みだが CocoaPods ライブラリへのアクセスがやや遅い場合は、 [ZIP 圧縮パッケージ](https://intl.cloud.tencent.com/document/product/647/34615)を直接ダウンロードして、 [クイックインテグレーション(iOS)](https://intl.cloud.tencent.com/document/product/647/35092)を参照して SDK をプロジェクトに統合することができます。

<span id="step2"> </span>
### 手順2：メディアデバイスの権限追加
`Info.plist`ファイルにカメラおよびマイクのアクセス許可のリクエストを追加します。

| Key | Value |
|---------|---------|
| Privacy - Camera Usage Description | カメラ使用の許可をリクエストする理由を記述。例えば、ビデオチャットでビデオを表示するには、カメラへのアクセスが必要です |
| Privacy - Microphone Usage Description | マイク使用の許可をリクエストする理由を記述。例えば、チャットで音声を送信するには、マイクへのアクセスが必要です |

<span id="step3"> </span>
### 手順3： SDKのインスタンスを初期化してイベントのコールバックをモニタ

1.  [sharedInstance()](https://intl.cloud.tencent.com/document/product/647/35119) インターフェースを使用して`TRTCCloud`インスタンスを作成します。
```swift
//  trtcCloud インスタンスを作成
let trtcCloud: TRTCCloud = TRTCCloud.sharedInstance()
trtcCloud.delegate = self
```
2. `delegate`属性を設定しイベントのコールバックを登録し、関連 イベントおよびエラー通知をモニタします。
```swift
// エラー通知はモニタされるべきもので、入手してユーザーに通知する必要があります
func onError(_ errCode: TXLiteAVError, errMsg: String?, extInfo: [AnyHashable : Any]?) {
        if ERR_ROOM_ENTER_FAIL == errCode {
                toastTip("入室失敗[\(errMsg ?? "")]")
        exitRoom()
        }
}
```

<span id="step4"> </span>
### 手順4：入室パラメータ TRTCParamsの組み立て
 [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) インターフェースをコールするとき、キーパラメータ [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams)を記入する必要があります。このパラメータに含まれる記入必須のフィールドは下表に示すとおりです。

| パラメータ名 | フィールドタイプ | 補足説明 |記入例 |
|---------|---------|---------|---------|
| sdkAppId | 数字 | アプリケーション ID， <a href="https://console.cloud.tencent.com/trtc/app">Tencent Real-Time Communicationコンソール</a> でSDKAppIDを表示できます。|1400000123 |
| userId  | 文字列 | アルファベットの大文字、小文字（a-z、A-Z）、数字（0-9）、下線およびハイフンのみを許可。 | test_user_001 |
| userSig | 文字列 |  userId を基に userSigを計算します。計算方法は [ UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166) を参照してください。| eJyrVareCeYrSy1SslI... |
| roomId | 数字 | デフォルトでは文字列のタイプのルームナンバーをサポートしていません、文字列タイプのルームナンバーは入室速度に影響します。文字列タイプのルームナンバーをサポートする必要が確実にある場合は、 [チケットを提出](https://console.cloud.tencent.com/workorder/category) してご連絡ください。 | 29834 |

>! TRTC は同時に2つの同じ userIdで入室できません。そうしないと相互に干渉することになります。


<span id="step5"> </span>
### 手順5：キャスター端末でのカメラのプレビューおよびマイク集音の起動
1. キャスター端末が[startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3fc1ae11b21944b2f354db258438100e) をコールすると、ローカルのカメラのプレビューを起動することができ、SDKはシステムにカメラのアクセス許可をリクエストします。
2. キャスター端末が [setLocalViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a961596f832657bfca81fd675878a2d15) をコールすると、ローカルのビデオ画面の表示モードを設定することができます。
 - Fill モードは塗りつぶしを意味し、画面は同じ比率で拡大およびトリミングできますが、黒い縁取りは付きません。
 - Fit モードは適応を意味し、画面は同じ比率で縮小してスクリーンにフィットしてそのコンテンツを完全に表示しますが、黒い縁取りが付くことがあります。
3. キャスター端末が [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e) インターフェースをコールすると、ローカルビデオのエンコードパラメータを設定できますが、そのパラメータはルームのその他ユーザーが視聴する画面の [画質](https://intl.cloud.tencent.com/document/product/647/35153)を決定します。
4. キャスター端末が[startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3177329bc84e94727a1be97563800beb) をコールすると、マイクを起動し、SDKはシステムにマイクの使用権限をリクエストします。

```swift
//サンプルコード：ローカルのオーディオ・ビデオストリーミングの公開
trtcCloud.setLocalViewFillMode(TRTCVideoFillMode.fit)
trtcCloud.startLocalPreview(frontCamera, view: localView)
//ローカルビデオエンコードパラメータの設定
let encParams = TRTCVideoEncParam.init()
encParams.videoResolution = TRTCVideoResolution._960_540
encParams.videoBitrate    = 1200
encParams.videoFps        = 15
trtcCloud.setVideoEncoderParam(encParams)
trtcCloud.startLocalAudio()
```

<span id="step6"> </span>
### 手順6：キャスター端末による美顔効果の設定

1.キャスター端末が[getBeautyManager()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4fb05ae6b5face276ace62558731280a)をコールすると、美顔設定インターフェースを取得することができます[TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#interfaceTXBeautyManager)。
2. キャスター端末が [setBeautyStyle()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#a8f2378a87c2e79fa3b978078e534ef4a) をコールすると、美顔スタイルを設定できます：
 - Smooth：スムース。明らかな効果が感じられます。インフルエンサーのスタイルに近づけます。
 - Nature：ナチュラル。美肌補正のアルゴリズムは顔の詳細な質感を維持し、より自然な感じになります。
 - Pitu ： [企業版](https://intl.cloud.tencent.com/document/product/647/34615) のみサポートしています。

3.キャスター端末が [setBeautyLevel()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#af864d9466d5161e1926e47bae0e3f027) をコールすると、顔加工法のレベルを設定します。通常、5の設定でOKです。

4.キャスター端末が [setBeautyLevel()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#a199b265f6013e0cca0ff99f731d60ff4) をコールすると、美白レベルを設定します。通常、5の設定でOKです。

5.iPhoneのカメラの色調はデフォルトだと黄色味がかっているため、[setFilter()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a1b0c2a9e82a408881281c7468a74f2c0)を呼び出して、キャスターに美白特殊効果を追加し、美白特殊効果に対応するフィルターファイルを、以下のアドレスからダウンロードすることをお勧めします。[フィルターファイル](https://liteav.sdk.qcloud.com/doc/res/trtc/filter/filterPNG.zip)。



<span id="step7"> </span>
### 手順7：キャスター端末によるルーム新規作成およびプッシュの開始
1.キャスター端末が[TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams)のフィールド`role`を **`TRTCRoleType.anchor`**に設定し、現在のユーザーのキャラクターをキャスターとして表示します。
2.キャスター端末が[enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)をコールすると、TRTCParams パラメータフィールド`roomId`の値をルームナンバーとするオーディオ・ビデオルームを作成し、**`appScene`**パラメータを指定します。
 - TRTCAppScene.LIVE：ビデオ・インタラクティブストリーミングモード。ここではこのモードを例として取り上げます。
 - TRTCAppScene.voiceChatRoom：ボイス・インタラクティブストリーミングモード。

3. ルームの新規作成が成功したら、キャスター端末は音声ビデオデータのデコードおよび伝送フローを開始します。同時にSDK は [onEnterRoom(result)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a6960aca54e2eda0f424f4f915908a3c5)  イベントをコールバックします。パラメータ`result`が0より大きいときは入室成功を意味し、具体的な数値は入室してからの消費時間であり、単位はミリ秒（ms）です；`result`が0より小さい時は入室失敗を意味し、具体的な数値は入室失敗のエラーコードになります。

```swift
func enterRoom() {
    let params = TRTCParams.init()
    params.sdkAppId = sdkappid
    params.userId   = userid
    params.userSig  = usersig
    params.roomId   = 908
    trtcCloud.enterRoom(params, appScene: TRTCAppScene.LIVE)
}

func onEnterRoom(_ result: Int) {
    if result > 0 {
        toastTip("入室成功，総消費時間[∖(result)]ms")
    } else {
        toastTip("入室失敗，エラーコード[∖(result)]")
    }
}
```

<span id="step8"> </span>
### 手順8：視聴者端末が入室しライブストリーミングを視聴
1.視聴者端末が[TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams)のフィールド`role`を**`TRTCRoleType.audience`**に設定し、現在のユーザーのキャラクターを視聴者として表示します。
2. 視聴者端末が [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) をコールすると、 TRTCParams パラメータのフィールド`roomId`が示すオーディオ・ビデオルームに入室し、**`appScene`**パラメータを指定します。
 - TRTCAppScene.LIVE：ビデオ・インタラクティブストリーミングモード。ここではこのモードを例として取り上げます。
 - TRTCAppScene.voiceChatRoom：ボイス・インタラクティブストリーミングモード。
3. キャスターの画面の視聴：
 - 視聴者端末が事前にキャスターの userIdを知っていて、入室に成功後、直接キャスターの`userId`を使用して [startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49)をコールすると、キャスターの画面を表示することができます。
 - 視聴者端末がキャスターの userIdを知らず、視聴者端末が入室に成功後に[onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80)イベント通知を受信してから、コールバックにより受け取ったキャスター`userId`を使用して[startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49)をコールすると、キャスターの画面を表示することができます。


<span id="step9"> </span>
### 手順9：視聴者とキャスターとのマイク接続
1.視聴者端末が[switch(TRTCRoleType.anchor)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5f4598c59a9c1e66938be9bfbb51589c)をコールすると、ロールをキャスター(TRTCRoleType.anchor)に切り替えます。
2. 視聴者端末が[startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3fc1ae11b21944b2f354db258438100e) をコールすると、ローカルの画面をアクティブにすることができます。
3. 視聴者端末が[startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3177329bc84e94727a1be97563800beb) をコールすると、マイクの集音を開始します。

```swift
//サンプルコード：視聴者マイク・オン
trtcCloud.switch(TRTCRoleType.anchor)
trtcCloud.startLocalAudio()
trtcCloud.startLocalPreview(frontCamera, view: localView)

//サンプルコード：視聴者マイク・オフ
trtcCloud.switch(TRTCRoleType.audience)
trtcCloud.stopLocalAudio()
trtcCloud.stopLocalPreview()
```


<span id="step10"> </span>
### 手順10：キャスター間でのルームを跨いだマイク接続PKの実施

TRTC ではの異なるオーディオ・ビデオルームのキャスターが2人、当初のライブストリーミングを退出しないというユースケースにおいて、“ルームを跨いだ通話”機能によってマイク接続通話機能をプルして“ルームを跨いだマイク接続PK”を実施することができます。

1.キャスター A は、[connectOtherRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a062bc48550b479a6b7c1662836b8c4a5)インターフェースをコールします。インターフェースパラメータは現在、JSON形式を採用しており、キャスターBの`{"roomId": 978,"userId": "userB"}`のフォーマットに組み立てられた`roomId`と`userId`のパラメータをインターフェース関数に渡す必要があります。
2．ルームを跨ぐことに成功した後は、キャスター A は [onConnectOtherRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a69e5b1d59857956f736c204fe765ea9a) イベントコールバックを受け取ります。同時に、2つのライブストリーミングルームのすべてのユーザーはいずれも [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80)  および [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5)  イベント通知を受け取ります。
 例えば、ルーム「001」のキャスターAがルーム「002」のキャスターBと`connectOtherRoom()`を介してルーム間通話する場合、ルーム「001」のユーザーはキャスターBの`onUserVideoAvailable(B, available: true)`コールバックと`onUserAudioAvailable(B, available: true)`コールバックを受信します。ルーム「002」のユーザーはキャスターAの`onUserVideoAvailable(A, available: true)`コールバックと`onUserAudioAvailable(A, available: true)`コールバックを受信します。
3.2つのルームにいるユーザーは、[startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49)をコールすることで、もう一方のルームのキャスターの画面を表示することができ、音声は自動再生されます。

```swift
//サンプルコード：ルームを跨いだマイク接続PK
let jsonDict = [ "roomId" : "978", "userId" : "userB" ]
guard let jsonData = try? JSONSerialization.data(withJSONObject: jsonDict,
                 options: JSONSerialization.WritingOptions.prettyPrinted) else {
    fatalError("JSONSerialization failed")
}
let jsonString = String.init(data: jsonData, encoding: String.Encoding.utf8)
trtcCloud.connectOtherRoom(jsonString)
```

<span id="step11"> </span>
### 手順11：現在のルームからの退出

[exitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a715f5b669ad1d7587ae19733d66954f3) メソッドをコールしてルームを退出すると、SDK は、退室するときカメラ、マイクなどのハードデバイスを停止またはリリースする必要があるため、退室動作は一瞬で完了するものではなく、[onExitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a6a98fcaac43fa754cf9dd80454897bea)のコールバックを受信してから、実際に退室操作を完了したとみなす必要があります。

```swift
// 退室のコール後は、onExitRoom イベントのコールバックをお待ちください
trtcCloud.exitRoom()

func onExitRoom(_ reason: Int) {
    print("ルームから離れる[∖(roomId)]: reason[∖(reason)]")
}
```

>!  App の中で多くの音声ビデオの SDKを同時に統合した場合は、`onExitRoom`コールバックを受信してからその他の音声ビデオ SDKを起動してください。そうしない場合は、ハード上の占有問題が生じることがあります。

