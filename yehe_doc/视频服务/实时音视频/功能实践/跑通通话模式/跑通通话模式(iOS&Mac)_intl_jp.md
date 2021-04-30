## 適用ケース
TRTC は、4種類の異なる入室モードをサポートしています。このうち、ビデオ通話（VideoCall）および音声通話（VoiceCall）を総称して通話モードといい、ビデオ・インタラクティブストリーミング（Live）およびボイス・インタラクティブストリーミング（VoiceChatRoom）を総称して [ライブストリーミングモード](https://intl.cloud.tencent.com/document/product/647/35107)といいます。
通話モードでのTRTCは、1つのルームに最大で300人の同時オンラインをサポートし最大で50人の同時発言をサポートします。1対1のビデオ通話、300人のビデオミーティング、オンライン問診、リモート面接、ビデオカスタマーサービス、オンライン人狼ゲームなどのユースケースに適合しています。

## 原理解析
TRTC クラウドサービスは、2種類の異なるタイプのサーバーノードから構成されており、それぞれ“インターフェースモジュール”および“プロキシモジュール”からなっています。
- **インターフェースモジュール**
この種のノードは、最も良質の回線および高性能の機器を採用しており、エンドツーエンドの低遅延マイク接続通話の処理に優れますが、単位時間当たりの費用はやや高くなります
- **プロキシモジュール**
この種のノードは、通常の回線および性能も一般的な機器を採用しており、同時進行性の高いプルストリーミング再生のニーズの処理にすぐれ、単位当たりの費用はやや低くなります。

通話モードでは、TRTCルームのすべてのユーザーはインターフェースモジュールに分配されます。各ユーザーは“キャスター”に相当し、各ユーザーは随時発言でき（同時アップストリームの最大制限は50）、このためオンラインミーティングなどのユースケースに適していますが、1つのルームの人数制限は300人になります。


## サンプルコード
 [Github] にログインし、本ファイルに関連するサンプルコードを取得することができます。
![](https://main.qcloudimg.com/raw/9cc33faf91173116e2d259f6b8b97d55.png)

> Githubへのアクセスが遅い場合は、 [TXLiteAVSDK_TRTC_iOS_latest.zip](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html)を直接ダウンロードすることもできます。

##　操作手順
<span id="step1"></span>
### 手順1： SDKへの統合
以下の方式を選択して **TRTC SDK** を項目に統合することができます。
#### 方法一： CocoaPods を使用して統合
1.  **CocoaPods**をインストールします。具体的な操作は [CocoaPods 公式サイトインストールの説明](https://guides.cocoapods.org/using/getting-started.html)をご参照ください。
2. 現在の項目ルートディレクトリの`Podfile`ファイルを開き、以下のコンテンツを追加します。
>このディレクトリに`Podfile`ファイルがない場合は、まず`pod init`コマンドを実行しファイルを新規作成してから、以下の内容を追加してください。
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

<span id = "step2"></span>
### 手順2：メディアデバイスの権限追加
`Info.plist`ファイルにカメラおよびマイクのアクセス許可のリクエストを追加します。

| Key | Value |
|---------|---------|
| Privacy - Camera Usage Description | カメラ使用の許可をリクエストする理由を記述。例えば、ビデオチャットでビデオを表示するには、カメラへのアクセスが必要です |
| Privacy - Microphone Usage Description | マイク使用の許可をリクエストする理由を記述。例えば、チャットで音声を送信するには、マイクへのアクセスが必要です |

<span id = "step3"></span>
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

<span id = "step4"></span>
### 手順4：入室パラメータ TRTCParamsの組み立て
 [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) インターフェースをコールするとき、キーパラメータ [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams)を入力する必要があります。このパラメータに含まれる入力必須のフィールドは下表に示すとおりです。

| パラメータ名 | フィールドタイプ | 補足説明 |記入例 |
|---------|---------|---------|---------|
| sdkAppId | 数字 | アプリケーション ID， <a href="https://console.cloud.tencent.com/trtc/app">Tencent Real-Time Communicationコンソール</a> でSDKAppIDを表示できます。|1400000123 |
| userId | 文字列 | アルファベットの大文字、小文字（a-z、A-Z）、数字（0-9）、下線およびハイフンのみを許可。 | test_user_001 |
| userSig | 文字列 |  userId を基に userSigを計算します。計算方法は [ UserSigの計算方法](https://intl.cloud.tencent.com/document/product/647/35166) を参照してください。| eJyrVareCeYrSy1SslI... |
| roomId | 数字 | デフォルトでは文字列のタイプのルームナンバーをサポートしていません、文字列タイプのルームナンバーは入室速度に影響します。文字列タイプのルームナンバーをサポートする必要が確実にある場合は、 [チケットを提出](https://console.cloud.tencent.com/workorder/category) してご連絡ください。 | 29834 |

> TRTC は同時に2つの同じ userIdで入室できません。そうしないと相互に干渉することになります。

<span id = "step5"></span>
### 手順5：新規作成および入室
1  [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) をコールすれば、 TRTCParams のパラメータの`roomId`が示すオーディオ・ビデオルームを追加できます。このルームが存在しない場合は、SDK はフィールド`roomId`の値をルームナンバーとして新しいルームを自動的に作成します。
2. ユースケースに基づき適切な**`appScene`**パラメータを設定してください。誤った選択をすると、ラグ率または画面の解像度が想定レベルに到達しなくなります。
 - ビデオ通話は、`TRTCAppScene.videoCall`に設定してください。
 - 音声通話は、`TRTCAppScene.audioCall`に設定してください。
3. 入室に成功したら、SDK は`onEnterRoom(result)`イベントをコールバックします。そのうち、パラメータ`result`が0より大きいときは入室成功を示し、具体的な数値は入室してからの消費時間になります。単位はミリ秒（ms）です。`result`が0より小さいときは入室失敗を示し、具体的な数値は入室失敗のエラーコードになります。

```swift
func enterRoom() {
    let params = TRTCParams.init()
    params.sdkAppId = sdkappid
    params.userId   = userid
    params.userSig  = usersig
    params.roomId   = 908
    trtcCloud.enterRoom(params, appScene: TRTCAppScene.videoCall)
}

func onEnterRoom(_ result: Int) {
    if result > 0 {
        toastTip("入室成功，総消費時間[∖(result)]ms")
    } else {
        toastTip("入室失敗，エラーコード[∖(result)]")
    }
}
```

> 
>- 入室に失敗した場合は、SDK は同時に`onError`イベントもコールバックし、パラメータ`errCode`（[エラーコード](https://intl.cloud.tencent.com/document/product/647/35124)）、`errMsg`（エラー原因）および`extraInfo`（予約済みパラメータ）を返します。
>- 既に特定のルームにいる場合は、まず`exitRoom()`をコールして現在のルームを退出すると、もう一つのルームに入ることができるようになります。

<span id = "step6"></span>
### 手順6：リモート側のオーディオ・ビデオストリーミングの閲覧
SDKは自動閲覧および手動閲覧をサポートします。

#### 自動閲覧モード（デフォルト）
自動閲覧モードでは、特定のルームに入った後、SDKはルームのその他のユーザーのオーディオストリームを自動で受信します。これによって最適な“インスタントブロードキャスティング”効果が得られます。
1. ルームのその他のユーザーが音声データをアップストリームするとき、 [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5)  イベントの通知を受け取り、SDK はこれらのリモート側ユーザーの音声を自動再生します。
2.  [muteRemoteAudio(userId, mute: true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afede3cc79a8d68994857b410fb5572d2)によって、特定の userId の音声データを遮断し、 [muteAllRemoteAudio(true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a75148bf8a322c852965fe774cbc7dd14) によって、すべてのリモート側ユーザーの音声データを遮断することもできます。遮断後にSDK はリモート側ユーザーに対応する音声データをこれ以上継続してプルすることはありません。
3. ルームのその他のユーザーがビデオデータをアップストリームするとき、 [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80)イベントの通知を受信します。しかし、このとき SDKはビデオデータをどのように表示するかの指令を受信していないため、ビデオデータを自動処理しません。 [startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) メソッドをコールしてリモート側ユーザーのビデオデータと`view`表示を関連付けする必要があります。
4.  [setRemoteViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afda6658d1bf7dc9bc1445838b95d21ff) によってビデオ画面の表示モードを指定することができます。
 - Fill モード：塗りつぶしを意味し、画面は同じ比率で拡大およびトリミングできますが、黒い縁取りは付きません。
 - Fit モード：適応を意味し、画面は同じ比率で縮小してスクリーンにフィットしてそのコンテンツを完全に表示しますが、黒い縁取りが付くことがあります。
5. [stopRemoteView(userId)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2b7e96e4b527798507ff743c61a6a066) によって、特定の userId のビデオデータを遮断し、[stopAllRemoteView()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aaa75cd1b98c226bb7b8a19412b204d2b) によって、すべてのリモート側のユーザーのビデオデータを遮断することもできます。遮断後、SDK はリモート側ユーザーに対応するビデオデータを継続してプルすることはありません。

```swift
// インスタンスコード：通知に基づきリモート側ユーザーのビデオ画面を閲覧（または閲覧の取り消し）します。
func onUserVideoAvailable(_ userId: String, available: Bool) {
    let remoteView = remoteViewDic[userId] as! UIView
    if available {
        trtcCloud.startRemoteView(userId, view: remoteView)
        trtcCloud.setRemoteViewFillMode(userId, mode: TRTCVideoFillMode.fit)
    } else {
        trtcCloud.stopRemoteView(userId)
    }
}
```

> `onUserVideoAvailable()`イベントのコールバックを受信後、すぐに`startRemoteView()`をコールしてビデオストリーミングを閲覧していない場合は、SDK は5s以内にリモートからのビデオデータの受信を停止します。

#### 手動閲覧モード
[setDefaultStreamRecvMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ada2e2155e0e7c3001c6bb6dca1d93048) インターフェースによって、 SDK を手動閲覧モードに指定できます。手動閲覧モードでは、SDK はルームのその他のユーザーの音声ビデオデータを自動受信しませんので、手動で API 関数を通じてトリガーさせる必要があります。

1. **入室前**に [setDefaultStreamRecvMode(false, video: false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ada2e2155e0e7c3001c6bb6dca1d93048) インターフェースをコールして、 SDK を手動閲覧モードに設定します。
2. ルームのその他のユーザーが音声データをアップストリームするとき、 [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5) イベントの通知を受信します。この時、 [muteRemoteAudio(userId, mute: false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afede3cc79a8d68994857b410fb5572d2) をコールすることで、そのユーザーの音声データを手動で閲覧する必要があります。SDK はそのユーザーの音声データを受信後、デコードして再生します。
3. ルームのその他のユーザーがビデオデータをアップストリームするとき、 [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80)イベントの通知を受信します。この時  [startRemoteView(userId, view: view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) メソッドをコールしてそのユーザーのビデオデータを手動で閲覧する必要があります。SDKは、そのユーザーのビデオデータを受信後、デコードして再生します。

<span id = "step7"></span>
### 手順7：ローカルのオーディオ・ビデオストリーミングの公開
1. [startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3177329bc84e94727a1be97563800beb) をコールして、ローカルのマイク集音を起動し、集音した音声をエンコードして送信します。
1. [startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3fc1ae11b21944b2f354db258438100e) をコールして、ローカルのカメラを起動し、収集したビデオをエンコードして送信します。
3.  [setLocalViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a961596f832657bfca81fd675878a2d15) をコールすると、ローカルのビデオ画面の表示モードを設定することができます。
 - Fill モードは塗りつぶしを意味し、画面は同じ比率で拡大およびトリミングできますが、黒い縁取りは付きません。
 - Fit モードは適応を意味し、画面は同じ比率で縮小してスクリーンにフィットしてそのコンテンツを完全に表示しますが、黒い縁取りが付くことがあります。
4.  [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e) インターフェースをコールすると、ローカルビデオのエンコードパラメータを設定できますが、そのパラメータはルームのその他ユーザーが視聴する画面の [画質](https://intl.cloud.tencent.com/document/product/647/35153)を決定します。

```swift
//サンプルコード：ローカルのオーディオ・ビデオストリーミングの公開
trtcCloud.setLocalViewFillMode(TRTCVideoFillMode.fit)
trtcCloud.startLocalPreview(frontCamera, view: localView)
trtcCloud.startLocalAudio()
```

> Mac 版 SDK は、デフォルトで現在のシステムでデフォルトのカメラおよびマイクを使用します。 [setCurrentCameraDevice()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aae9955bb39985586f7faba841d2692fc) および[setCurrentMicDevice()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5141fec83e7f071e913bfc539c193ac6) をコールすることで、その他のカメラおよびマイクを選択することができます。

<span id = "step8"></span>
### 手順8：現在のルームからの退出

[exitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a715f5b669ad1d7587ae19733d66954f3) メソッドをコールしてルームを退出すると、SDK は、退室するときカメラ、マイクなどのハードデバイスを停止またはリリースする必要があるため、退室動作は一瞬で完了するものではなく、[onExitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a6a98fcaac43fa754cf9dd80454897bea)のコールバックを受信してから、実際に退室操作を完了したとみなす必要があります。

```swift
// 退室のコール後は、onExitRoom イベントのコールバックをお待ちください
trtcCloud.exitRoom()

func onExitRoom(_ reason: Int) {
    print("ルームから離れる[∖(roomId)]: reason[∖(reason)]")
}
```

>  App の中で多くの音声ビデオの SDKを同時に統合した場合は、`onExitRoom`コールバックを受信してからその他の音声ビデオ SDKを起動してください。そうしない場合は、ハード上の占有問題が生じることがあります。
