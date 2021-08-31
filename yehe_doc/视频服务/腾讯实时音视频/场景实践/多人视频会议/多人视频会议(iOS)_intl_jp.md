## デモンストレーション
当社のDemoを[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)からインストールし、多人数ビデオミーティングの効果をご体験いただけます。これには、画面共有、美顔、低レイテンシーのミーティングなどのTRTCの多人数ビデオミーティングのシーンにおける関連機能が含まれています。

多人数ビデオミーティングの機能に速やかにアクセスしたい場合は、当社が提供するDemoをもとに直接適応に変更を加えることも、当社が提供するTRTCMeetingのコンポーネントを使用してUIのカスタマイズを実現することも可能です。

## DemoのUIの再利用
[](id:ui_step1)
### 手順1：アプリケーションの新規作成
1．TRTCコンソールにログインし、【開発支援】>【[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. 例えば、`TestMeetingRoom`などのアプリケーション名を入力して、【作成】をクリックします。

>!本機能はTencent Cloud[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの価格説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。

[](id:ui_step2)
### 手順2：SDKおよびDemoソースコードをダウンロード
1. 実際の業務ニーズに基づき、SDKおよび付属のDemoソースコードをダウンロードします。
2. ダウンロード完了後、【ダウンロードしました。次のステップ】をクリックします。

[](id:ui_step3)
### 手順3：Demoプロジェクトファイルの設定
1. 設定変更画面に入り、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h`のファイルを見つけて開きます。
3. `GenerateTestUserSig.h`のファイルの関連するパラメータを設定します。
<ul style="margin:0"><li/>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。
<li/>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. 貼り付け完了後、【貼り付けました。次のステップ】をクリックすれば、作成が完了します。
5. コンパイル完了後、【コンソール概要に戻る】をクリックすればOKです。


>!
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるよようになります。そのため**のこの手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

### 手順4：Demoの実行
Xcode（11.0以上のバージョン）を使用してソースコードプロセス`iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace`を開き、【実行】をクリックすれば、このDemoのデバッグが開始されます。

### 手順5：Demoソースコードの修正
ソースコードの``trtcmeetingdemo``フォルダは、uiとmodelという2つのサブフォルダを含んでいます。uiフォルダにはインターフェースコードが含まれています。以下の表にはファイルまたはフォルダおよび対応するUIをリストアップして、二次調整を行いやすくしています。

| ファイルまたはフォルダ | 機能説明 |
|:-------:|:--------|
| SegmentVC | インターフェース関連のUI実装コードの設定。 |
| TRTCBroadcastExtensionLauncher.swift | スクリーンレコーディングのポップアップウィンドウ関連のUI実装コード。 |
| TRTCMeetingNewViewController | ビデオミーティング作成インターフェースのUI実装コード。 |
| TRTCMeetingMainViewController | ビデオルームインターフェースのUI実装コード。 |
| TRTCMeetingMemberViewController | 参加者リストのインターフェースのUI実装コード。 |
| TRTCMeetingMoreViewController | インターフェース関連のUI実装コードの設定。 |


[](id:model)
## UIカスタマイズの実現

[ソースコード](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCMeetingDemo)のtrtcmeetingdemoフォルダは、uiとmodelという2つのサブフォルダを含んでいます。modelフォルダには再利用できるオープンソースコンポーネントTRTCMeetingが含まれています。`TRTCMeeting.h`ファイルでこのコンポーネントが提供するインターフェース関数を見て、対応するインターフェースを使用してUIのカスタマイズを実現することができます。
![](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)


[](id:model.step1)
### 手順1：SDKへの統合
多人数ビデオミーティングのコンポーネントTRTCMeetingは、TRTC SDKとIM SDKに依存し、次の手順で2つのSDKをプロジェクトに統合することができます。

**方法1：cocoapodsリポジトリを介する依存**
```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```
>?2つのSDK製品の最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK)および[IM](https://github.com/tencentyun/TIMSDK)のGithubトップページで取得することができます。

**方法2：ローカルを介する依存**
開発環境でのcocoapodsリポジトリへのアクセスが遅い場合は、ZIPパッケージを直接ダウンロードし、統合ドキュメントに従って手動でプロジェクトに統合することができます。

| SDK | ダウンロードページ | ガイドの統合 |
|---------|---------|---------|
| TRTC SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/647/34615) | [統合ドキュメント](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/1047/33996) | [統合ドキュメント](https://intl.cloud.tencent.com/document/product/1047/34306) |

[](id:model.step2)
### 手順2：権限の設定
info.plistファイルにPrivacy > Camera Usage Description、Privacy > Microphone Usage Descriptionを追加し、カメラとマイクの権限をリクエストする必要があります。

[](id:model.step3)
### 手順3：TRTCMeetingコンポーネントのインポート
`iOS/LiteAVDemo/TXLiteAVDemo/TRTCMeetingDemo/model`ディレクトリの中の全ファイルをお客様のプロジェクトにコピーします。

<span id="model.step4"></span>
### 手順4：コンポーネントの作成およびログイン
1. `sharedInstance`インターフェースを呼び出すと、TRTCMeetingコンポーネントのインスタンスオブジェクトを作成できます。
2. `setDelegate`関数を呼び出してコンポーネントのイベント通知を登録します。
3. `login`関数を呼び出してコンポーネントのログインを完了します。下表を参考にキーパラメータを入力してください。
<table> 
<tr>
<th>パラメータ名</th>
<th>作用</th>
</tr><tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a> でSDKAppIDを表示できます。</td>
</tr><tr>
<td>userId</td>
<td>現在のユーザーID。文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については、<a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSigの計算方法</a>をご参照ください。</td>
</tr><tr>
<td>callback</td>
<td>ログインのコールバック。成功時にcodeは0になります。</td>
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

[](id:model.step5)
### 手順5：多人数ミーティングの新規作成
1. キャスターは、[手順4](#model.step4) でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. キャスターは、`setDelegate`を呼び出すことで、`createMeeting`のイベントの呼び出しを行い、新しいミーティングルームを作成できます。
3. キャスターは、`startCameraPreview`を呼び出してビデオ画面をキャプチャすることができ、`startMicrophone`を呼び出して音声をキャプチャすることもできます。
4. キャスターに美顔のニーズがある場合、インターフェース上に美顔調節ボタンを設置して呼び出し、`getBeautyManager`で美顔設定を行うことができます。
>? エンタープライズ版以外のSDKは変顔やスタンプの機能をサポートしていません。

![](https://main.qcloudimg.com/raw/416a1afd87b196a6ef791bf63eeaa5e0.png)

```
// 1.キャスターは、ニックネームおよびプロフィール画像を設定します。
trtcMeeting.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

// 2.キャスターがルームを作成します
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


[](id:model.step6)
### 手順6：参加者の多人数ミーティングへの参加
1. 参加者は、[手順4](#model.step4) でログイン後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. 参加者は、`enterMeeting`を呼び出し、ミーティングルーム番号を渡すと、ミーティングルームに入ることができます。
3. 参加者は、`startCameraPreview`を呼び出してビデオ画面をキャプチャすることができ、`startMicrophone`を呼び出して音声をキャプチャすることもできます。
4. 他の参加者がカメラを立ち上げると、`onUserVideoAvailable`のイベントを受信します。この時`startRemoteView`を呼び出してuserIdを渡すと再生が開始されます。

![](https://main.qcloudimg.com/raw/f33213dea7a32ca9904c066952fcc535.png)

```
// 1.参加者がニックネームとプロフィール画像を設定します
trtcMeeting.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

// 2.enterMeeting関数を実装します
trtcMeeting.enterMeeting(roomId) { (code, msg) in
   if code == 0{
     trtcMeeting.startCameraPreview(true, view: localPreviewView)
     trtcMeeting.startMicrophone()
   } else {
      self.view.makeToast("ミーティングの参加に失敗しました：" + msg!)
   }
}
```

```
let renderView = getRenderView(userId: userId)
if available && renderView != nil {
  //コールバックを受信し、startRemoteViewを呼び出してuserIdを渡すと、再生が開始されます
  TRTCMeeting.sharedInstance().startRemoteView(userId, view: renderView!) { (code, message) in
   debugPrint("startRemoteView" + "\(code)" + message!)
  }
} else {
 TRTCMeeting.sharedInstance().stopRemoteView(userId) { (code, message) in
   debugPrint("stopRemoteView" + "\(code)" + message!)
  }
}
//現在のインターフェースの更新
renderView?.refreshVideo(isVideoAvailable: available)
```

[](id:model.step7)
### 手順7：画面共有
1. `startScreenCapture`を呼び出し、エンコードパラメータとスクリーンレコーディングのプロセスのフローティングウィンドウを渡すと、画面共有機能が実装できます。具体的な情報については、[TRTC SDK](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97)をご参照ください。
2. ミーティング中の他の参加者が、`onUserVideoAvailable`のイベントの通知を受信します。

>!画面共有とカメラのキャプチャの2つは相互排他的な操作です。画面共有機能を立ち上げたい時は、先に`stopCameraPreview`を呼び出し、カメラのキャプチャをオフにしてください。

```
// 1.ボタンのクリックで画面共有を実現します
if #available(iOS 12.0, *) {
  // スクリーンレコーディングの前にカメラのキャプチャをオフにする必要があります
  self.setLocalVideo(isVideoAvailable: false)

  // 画面共有
  let params = TRTCVideoEncParam()
  params.videoResolution = TRTCVideoResolution._1280_720
  params.videoFps = 10
  params.videoBitrate = 1800
  TRTCMeeting.sharedInstance().startScreenCapture(params)
  TRTCBroadcastExtensionLauncher.launch()
} else {
  self.view.makeToast("システムのバージョンが12.0より低い場合は、システムをバージョンアップにしてください。")
}     
```

[](id:model.step8)
### 手順8：文字チャットとミュートメッセージの実現
- `sendRoomTextMsg`によって通常のテキストメッセージを発信できるようになり、該当するルーム内の全てのキャスターおよび視聴者が`onRecvRoomTextMsg`のコールバックを受信することができます。
IMバックエンドは、デフォルトのセンシティブワードフィルタルールを備えており、センシティブワードと認識されたテキストメッセージはクラウドに転送されることはありません。
```
// 発信側：テキストメッセージの発信
TRTCMeeting.sharedInstance().sendRoomTextMsg("Hello Word!") { (code, message) in
  debugPrint("send result: ", code)
}
// 受信側：テキストメッセージの監視
func onRecvRoomTextMsg(_ message: String?, userInfo: TRTCMeetingUserInfo) {
  debugPrint(":\(String(describing: userInfo.userId))から受信したメッセージ\(String(describing: message))")
}
```
- `sendRoomCustomMsg`によってカスタマイズ（シグナリング）情報を発信することができます。そのルーム内のすべてのキャスターおよび視聴者は`onRecvRoomCustomMsg`のコールバックを受信することができます。
カスタムメッセージは、通常カスタマイズしたシグナリングの転送に使用します（例：ミュートの会場内制御など）。
```
// 送信側：カスタマイズしたCmdでミュートの通知を区別できます
// eg:"CMD_MUTE_AUDIO"はミュートの通知を表します
TRTCMeeting.sharedInstance().sendRoomCustomMsg("CMD_MUTE_AUDIO", message: "1") { (code, message) in
  debugPrint("send result: ", code)
}
// 受信側：カスタムメッセージの監視
func onRecvRoomCustomMsg(_ cmd: String?, message: String?, userInfo: TRTCMeetingUserInfo) {
  if cmd == "CMD_MUTE_AUDIO" {
    debugPrint(":\(String(describing: userInfo.userId))からミュート通知を受信しました:\(String(describing: message))")
    TRTCMeeting.sharedInstance().muteLocalAudio(message == "1")
  }
}
```

