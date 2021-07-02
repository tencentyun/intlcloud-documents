## デモンストレーション
当社のDemoを[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)して、インストールし、複数人ビデオ会議の効果を体験いただけます。これには、画面共有、美顔、低レイテンシーのミーティングなどのTRTCの複数人ビデオミーティングのシーンにおける関連機能が含まれています。

迅速に複数人ビデオ会議の機能にアクセスしたい場合は、当社が提供するDemoをもとに直接修正を加えてフィットさせることも、当社が提供するTRTCMeetingの コンポーネントを使用してカスタマイズしたUIを実現することも可能です。

## Demo の UI の再利用

### 手順1：アプリケーションの新規作成

1．Tencent Real-Time Communicationコンソールにログインし、【開発支援】>【[Demoのクイック実行](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. 【今すぐスタート】をクリックし、例えば、`TestMeetingRoom`などアプリケーション名を入力して、【アプリケーション作成】をクリックします。

>?本機能は [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) と [IM](https://intl.cloud.tencent.com/document/product/1047) という2つの基本的な PaaS サービスを同時に使用し、TRTCをアクティブにした後、IM サービスを同期的にアクティブにすることができます。 IM は付加価値サービスであり、請求ルールの詳細については [Instant Messagingの価格説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。

### 手順2：SDKおよびDemoのソースコードをダウンロード
１．マウスを該当するカードまで移動し、【[Github](https://github.com/tencentyun/TRTCSDK/tree/master/iOS)】をクリックしてGithub（または【[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_iOS_latest.zip)】をクリック）にジャンプして、関連するSDK および付属のDemoのソースコードをダウンロードします。
 ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. ダウンロード完了後、Tencent Real-Time Communicationコンソールに戻り、【ダウンロードしました。次のステップ】をクリックすれば、SDKAppIDおよびキー情報をクエリできます。

### 手順3：Demoプロジェクトファイルの設定
1．[手順2](#ui.step2) でダウンロードしたソースコードパッケージを解凍します。
2. `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h` のファイルを探して開きます。
3. `GenerateTestUserSig.h`のファイルの関連するパラメータを設定します。
  <ul><li>SDKAPPID：デフォルトは0、実際のSDKAppIDを設定してください。</li>
  <li>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</li></ul> 
    <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4．Tencent Real-Time Communicationコンソールに戻り、【貼り付け完了。次のステップ】をクリックします。
5.【ガイドを閉じてコンソールへ進む】をクリックします。

>!本書で言及した新規UserSigの作成法は、クライアントコードでSECRETKEYを設定し、この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになり、そのため**のこの手法はローカルDemo実行および機能デバッグにのみ適合します**。
≻ UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

### 手順4：Demoの動作
Xcode（11.0以上のバージョン）を使用してソースコードプロセス `iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace`を開き、【実行】をクリックすれば本 Demoのデバッグを開始することができます。

### 手順5：Demo ソースコードの修正
ソースコードの``trtcmeetingdemo`` フォルダは、 ui と modelの2つのサブフォルダを含んでいます。ui フォルダにはインターフェースコードが含まれています。以下の表にはファイルまたはフォルダ及び対応する UIをリストアップして、二次調整を行いやすくしています。

| ファイルまたはフォルダ | 機能説明 |
|:-------:|:--------|
| SegmentVC | インターフェース関連のUI実装コードの設定。 |
| TRTCBroadcastExtensionLauncher.swift | スクリーンキャプチャのポップアップウィンドウ関連のUI実装コード。 |
| TRTCMeetingNewViewController | ビデオミーティング作成インターフェースのUI実装コード。 |
| TRTCMeetingMainViewController | ビデオルームインターフェースのUI実装コード。 |
| TRTCMeetingMemberViewController | 参加者リストのインターフェースのUI実装コード。 |
| TRTCMeetingMoreViewController | インターフェース関連のUI実装コードの設定。 |


<span id="model"> </span>
## UIカスタマイズの実装

[ソースコード]のtrtcmeetingdemoフォルダには、 ui と modelの2つのサブフォルダがあり、model フォルダには再利用できるオープンソースコンポーネント TRTCMeetingがあります。`TRTCMeeting.h`ファイルでこのコンポーネントが提供するインターフェース関数を見て、対応するインターフェースを使用して UI のカスタマイズを実現することができます。
![](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)


<span id="model.step1"> </span>
### 手順1： SDKへの統合
多人数ビデオミーティングのコンポーネント TRTCMeetingは、TRTC SDKとIM SDKに依存し、次の手順で2つの SDKをプロジェクトに統合することができます。

**方法一：cocoapodsリポジトリを介する依存**
```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```
>?2つのSDK製品の最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK) および [IM](https://github.com/tencentyun/TIMSDK) の Github トップページで取得することができます。

**方法二：ローカルを介する依存**
開発環境でのcocoapods リポジトリへのアクセスが遅い場合は、ZIPパッケージを直接ダウンロードし、統合ドキュメントに従って手動でプロジェクトに統合することができます。

| SDK | ダウンロードページ | ガイドの統合 |
|---------|---------|---------|
| TRTC SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/647/34615) | [統合ドキュメント](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/1047/33996) | [統合ドキュメント](https://intl.cloud.tencent.com/document/product/1047/34306) |

<span id="model.step2"> </span>
### 手順2：権限の設定
info.plist ファイルに Privacy > Camera Usage Description， Privacy > Microphone Usage Description を追加し、カメラとマイクの権限をリクエストする必要があります。

<span id="model.step3"> </span>
### 手順3：TRTCMeetingコンポーネントのインポート
`iOS/LiteAVDemo/TXLiteAVDemo/TRTCMeetingDemo/model`ディレクトリの中の全ファイルをお客様のプロジェクトにコピーします。

<span id="model.step4"> </span>
### 手順4：コンポーネントの作成およびログイン
1. `sharedInstance`インターフェースをコールすると、 TRTCMeeting コンポーネントのインスタンスオブジェクトを作成できます。
2. `setDelegate`関数をコールしてコンポーネントのイベント通知を登録します。
3. `login`関数をコールしてコンポーネントのログインを完了します。下表を参考にキーパラメータを入力してください。
<table> 
<tr>
<th>パラメータ名</th>
<th>作用</th>
</tr>
<tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">Tencent Real-Time Communicationコンソール</a> で SDKAppIDを表示できます。</td>
</tr>
<tr>
<td>userId</td>
<td>現在のユーザーID、文字列タイプでは、英語のアルファベット（a-z と A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については、 <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSigの計算方法</a>をご参照ください。</td>
</tr>
<tr>
<td>callback</td>
<td>ログインのコールバック。成功時に code は0になります。</td>
</tr>
</table>

```swift
let userID = ProfileManager.shared().curUserID()
let userSig = GenerateTestUserSig.genTestUserSig(userID)

TRTCMeeting.sharedInstance().login(SDKAPPID, userId: userID, userSig: userSig, callback: { code, message in
    if code == 0 {
        //ログイン成功
    }
})
```

<span id="model.step5"> </span>
### 手順5：多人数ミーティングの新規作成
1. キャスターは、[手順4](#model.step4) でログイン後、`setSelfProfile`をコールして自身のニックネームおよびプロファイル写真を設定することができます。
2. キャスターは、`setDelegate`を呼び出すことで、`createMeeting`のイベントの呼び出しを行い、新しいミーティングルームを作成できます。
3. キャスターは、`startCameraPreview`を呼び出してビデオ画面をキャプチャすることができ、`startMicrophone`を呼び出して音声をキャプチャすることができます。
4. キャスターに美顔のニーズがある場合、画面上に美顔調節ボタンを設置して呼び出し、`getBeautyManager`で美顔設定を行うことができます。
>エンタープライズ版以外のSDKは変顔やスタンプの機能をサポートしていません。
>

![](https://main.qcloudimg.com/raw/416a1afd87b196a6ef791bf63eeaa5e0.png)

```swift
// 1.キャスターは、ニックネームおよびプロファイル写真を設定します。
trtcMeeting.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

// 2.キャスターがルームを作成します。
trtcMeeting.createMeeting(roomId) { (code, msg) in
 if code == 0 {
   // ルーム作成の成功
  let localPreviewView=getRenderView(userId: selfUserId)!
  TRTCMeeting.sharedInstance().startCameraPreview(true, view: localPreviewView)
  TRTCMeeting.sharedInstance().startMicrophone();
  
  // デフォルトの美顔パラメータの使用
  beautyPannel.resetAndApplyValues()
  return;
 }
}
```

<span id="model.step6"> </span>
### 手順6：参加者の多人数ミーティングへの参加
1. 参加者は、[手順4](#model.step4) でログイン後、`setSelfProfile`をコールして自身のニックネームおよびプロファイル写真を設定することができます。
2. 参加者は、`enterMeeting`を呼び出し、ミーティングルーム番号を渡すと、ミーティングルームに入ることができます。
3. 参加者は、`startCameraPreview`を呼び出してビデオ画面をキャプチャすることができ、`startMicrophone`を呼び出して音声をキャプチャすることができます。
4. 他の参加者がカメラを立ち上げると、`onUserVideoAvailable`のイベントを受信します。この時`startRemoteView`を呼び出してuserIdを渡すと再生が開始されます。

![](https://main.qcloudimg.com/raw/f33213dea7a32ca9904c066952fcc535.png)

```swift
// 1.参加者がニックネームとプロファイル写真を設定します。
trtcMeeting.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

// 2.enterMeeting関数の実装
trtcMeeting.enterMeeting(roomId) { (code, msg) in
   if code == 0{
     trtcMeeting.startCameraPreview(true, view: localPreviewView)
     trtcMeeting.startMicrophone()
   }else{
      self.view.makeToast("ミーティングの参加に失敗しました：" + msg!)
   }
}
```

```swift
let renderView = getRenderView(userId: userId)
if available && renderView != nil {
  //コールバックを受信し、startRemoteViewを呼び出してuserIdを渡すと、再生が開始されます。
  TRTCMeeting.sharedInstance().startRemoteView(userId, view: renderView!) { (code, message) in
   debugPrint("startRemoteView" + "\(code)" + message!)
  }
}else{
 TRTCMeeting.sharedInstance().stopRemoteView(userId) { (code, message) in
   debugPrint("stopRemoteView" + "\(code)" + message!)
  }
}
//現在のインターフェースの更新
renderView?.refreshVideo(isVideoAvailable: available)
```

<span id="model.step7"> </span>
### 手順7：画面共有
1. `startScreenCapture`を呼び出し、エンコードパラメータとスクリーンキャプチャのプロセスのフローティングウィンドウを渡すと、画面共有機能が実装できます。具体的な情報は、[TRTC SDK](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97)をご参照ください。
3. ミーティング中の他の参加者が、`onUserVideoAvailable`のイベントの通知を受信します。

>!画面共有とカメラのキャプチャの2つは相互排他的な操作です。画面共有機能を立ち上げたい時は、先に`stopCameraPreview`を呼び出し、カメラのキャプチャをオフにしてください。

```swift
// 1.ボタンのクリックで画面共有を実現します。
if #available(iOS 12.0, *) {
  // スクリーンキャプチャの前にカメラのキャプチャをオフにする必要があります。
  self.setLocalVideo(isVideoAvailable: false)
  
  // 画面共有
  let params = TRTCVideoEncParam()
  params.videoResolution = TRTCVideoResolution._1280_720
  params.videoFps = 10
  params.videoBitrate = 1800
  TRTCMeeting.sharedInstance().startScreenCapture(params)
  TRTCBroadcastExtensionLauncher.launch()
}else{
  self.view.makeToast("システムのバージョンが12.0より低い場合は、システムをバージョンアップにしてください。")
}     
```

<span id="model.step8"> </span>
### 手順8：文字チャットと禁止ワードメッセージの実現
- `sendRoomTextMsg`によって通常のテキストメッセージを発信できるようになり、該当するルーム内の全てのキャスターおよび視聴者が`onRecvRoomTextMsg`のコールバックを受信することができます。
IMバックエンドは、デフォルトのNGワードフィルター規則を有し、NGワードと認識されたテキストメッセージはクラウドに転送されることはありません。

```swift
// 発信側：テキストメッセージの発信
TRTCMeeting.sharedInstance().sendRoomTextMsg("Hello Word!") { (code, message) in
  debugPrint("send result: ", code)
}

// 受信側：テキストメッセージのモニタ
func onRecvRoomTextMsg(_ message: String?, userInfo: TRTCMeetingUserInfo) {
  debugPrint(":\(String(describing: userInfo.userId))から受信したメッセージ\(String(describing: message))")
}
```

- `sendRoomCustomMsg`によってカスタマイズ（シグナリング）情報を発信することができます。そのルーム内の全てのキャスターおよび視聴者は`onRecvRoomCustomMsg`のコールバックを受信することができます。
カスタマイズメッセージは、通常カスタマイズしたシグナリングの転送に使用します（例：禁止ワードの会場内制御など）。

```swift
// 送信側：カスタマイズした Cmdで禁止ワードの通知を区別できます。
// eg:"CMD_MUTE_AUDIO"は禁止ワードの通知を表します。
TRTCMeeting.sharedInstance().sendRoomCustomMsg("CMD_MUTE_AUDIO", message: "1") { (code, message) in
  debugPrint("send result: ", code)
}

// 受信側：カスタマイズメッセージのモニタ
func onRecvRoomCustomMsg(_ cmd: String?, message: String?, userInfo: TRTCMeetingUserInfo) {
  if cmd == "CMD_MUTE_AUDIO" {
    debugPrint(":\(String(describing: userInfo.userId))から受信した禁止ワードの通知:\(String(describing: message))")
    TRTCMeeting.sharedInstance().muteLocalAudio(message == "1")
  }
}
```

