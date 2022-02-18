## デモンストレーション
当社のAppを[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)してインストールし、多人数ビデオミーティングの効果を体験いただけます。これには、画面共有、美顔、低遅延ミーティングなど、TRTCの多人数ビデオミーティングシナリオ関連の機能が含まれています。




多人数ビデオミーティングの機能に素早くアクセスしたい場合は、当社が提供するAppを直接修正して適応させるか、当社が提供するTUIMeetingのコンポーネントを使用してカスタマイズしたUIを実装することができます。

## AppのUIの再利用
[](id:ui_step1)
### 手順1：アプリケーションの新規作成
1. TRTCコンソールにログインし、**開発支援>[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)**を選択します。
2. アプリケーション名（例：`TestMeetingRoom`）を入力し、**作成**をクリックします。
3. **ダウンロードしました。次のステップ**をクリックすると、この手順をスキップします。

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>!本機能はTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。

[](id:ui_step2)
### 手順2：Appソースコードのダウンロード
[TUIMeeting](https://github.com/tencentyun/TUIMeeting)をクリックして当該ページに入り、ソースコードをCloneまたはダウンロードします。

[](id:ui_step3)
### 手順3：Appプロジェクトファイルの設定
1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `TUIMeeting/Debug/GenerateTestUserSig.swift`ファイルを見つけて開きます。
3.`GenerateTestUserSig.swift`ファイル内の関連パラメータを設定します。
<ul style="margin:0"><li/>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。
<li/>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. 貼り付け完了後、**貼り付けました。次のステップ**をクリックすれば、作成が完了します。
5. コンパイル完了後、 **コンソール概要に戻る** をクリックすれば終了です。


>!
>- ここで言及するUserSigの発行方法は、クライアントコードの中でのSECRETKEY設定となりますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者がお客様のTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのAppクイックスタートおよび機能デバッグにのみ適しています**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[UserSigに関するご質問](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:ui_step4)
### 手順4：プロジェクトの実行
Xcode（バージョン11.0以上）を使用してソースコードプロジェクト`TUIMeeting/TUIMeetingApp.xcworkspace`を開き、**実行**をクリックすれば、このAppのデバッグが開始されます。

[](id:ui_step5)
### 手順5：プロジェクトソースコードの修正
ソースコードの中の`Source`フォルダには、Sourceとmodelの2つのサブフォルダが含まれ、uiフォルダの中はいずれもインターフェースコードです。以下の表に、ファイルまたはフォルダおよびそれに対応するUIをリストアップし、二次調整に役立つようにしています。

| ファイルまたはフォルダ | 機能の説明                             |
|:-------:|:--------|
| TRTCMeetingNewViewController.swift | ビデオミーティング作成インターフェースのUI実装コード。このクラスはPodsを外部に公開するパブリッククラスです。 |
| SegmentVC | インターフェース関連のUI実装コードの設定。 |
| TRTCBroadcastExtensionLauncher.swift | スクリーンキャプチャのポップアップウィンドウ関連のUI実装コード。このクラスはPodsプライベートクラスです。 |
| TRTCMeetingMainViewController.swift | ビデオルームインターフェースのUI実装コード。このクラスはPodsプライベートクラスです。 |
| TRTCMeetingMemberViewController.swift | 参加者リストインターフェースのUI実装コード。このクラスはPodsプライベートクラスです。 |
| TRTCMeetingMoreViewController.swift | インターフェース関連のUI実装コードの設定。このクラスはPodsを外部に公開するパブリッククラスです。 |


## 体験アプリケーション
>! 体験アプリケーションには、少なくとも2台のデバイスが必要です。

### ユーザーA
1. ユーザー名を入力し（**ユーザー名は一意のものとし、他のユーザーと重複しないようにしてください**）、ログインします。
2. コードを入力し、**ミーティングに参加**をクリックします。
3. ルームトピックを入力し、**チャット開始**をクリックします。

### ユーザーB
1. ユーザー名を入力し（**ユーザー名は一意のものとし、他のユーザーと重複しないようにしてください**）、ログインします。
2. ユーザーAが作成したコードを入力し、**ミーティングに参加**をクリックします。

[](id:model)
## UIカスタマイズの実装

[ソースコード](https://github.com/tencentyun/TUIMeeting)の`Source`フォルダには、uiとmodelという2つのサブフォルダがあり、modelフォルダには再利用できるオープンソースコンポーネントTRTCMeetingが含まれています。`TRTCMeeting.h`ファイルでこのコンポーネントが提供するインターフェース関数を確認し、対応するインターフェースを使用してカスタマイズしたUIを実装することができます。
![](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)


[](id:model.step1)
### 手順1：SDKの統合 
多人数ビデオミーティングのコンポーネントTUIMeetingは、TRTC SDKとIM SDKに依存しています。次の手順で2つのSDKをプロジェクトに統合することができます。

**方法1：cocoapodsリポジトリを介する依存**
<dx-codeblock>
::: swift
 pod 'TXIMSDK_iOS'
 pod 'TXLiteAVSDK_TRTC'
:::
</dx-codeblock>

>? 2つのSDK製品の最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK)および[IM](https://github.com/tencentyun/TIMSDK)のGithubトップページで取得することができます。

**方法2：ローカルを介する依存**
開発環境でのcocoapodsリポジトリへのアクセスが遅い場合は、ZIPパッケージを直接ダウンロードし、統合ドキュメントに従って手動でプロジェクトに統合することができます。

| SDK | ダウンロードページ | ガイドの統合 |
|---------|---------|---------|
| TRTC SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/647/34615) | [統合ドキュメント](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK | [DOWNLOAD](https://intl.cloud.tencent.com/document/product/1047/33996) | [統合ドキュメント](https://intl.cloud.tencent.com/document/product/1047/34306) |

[](id:model.step2)
### 手順2：権限の設定
info.plistファイルに`Privacy > Camera Usage Description`， `Privacy > Microphone Usage Description`を追加し、カメラとマイクの権限をリクエストする必要があります。

[](id:model.step3)
### 手順3：TUIMeetingコンポーネントのインポート
**cocoapodsを使用してコンポーネントをインポート**することができます。具体的な手順は、以下のとおりです。
1. プロジェクトディレクトリ下の`Source`、`Resources`、`TCBeautyKit`、`TXAppBasic`フォルダ、`TUIMeeting.podspec`ファイルをお客様のプロジェクトディレクトリ下へコピーします。
2. `Podfile`ファイル内に以下の依存関係を追加します。その後、`pod install`コマンドを実行すると、インポートが完了します。
```swift
 pod 'TXAppBasic', :path => "TXAppBasic/"
 pod 'TCBeautyKit', :path => "TCBeautyKit/"
 pod 'TXLiteAVSDK_TRTC'
 pod 'TUIMeeting', :path => "./", :subspecs => ["TRTC"] 
```

[](id:model.step4)
### 手順4：コンポーネントの作成およびログイン
1. `sharedInstance`インターフェースを呼び出すと、TRTCMeetingコンポーネントのインスタンスオブジェクトを作成できます。
2. `setDelegate`関数を呼び出してコンポーネントのイベント通知を登録します。
3. `login`関数を呼び出してコンポーネントのログインを完了します。下表を参考にキーパラメータを入力してください。
<table> 
<tr>
<th>パラメータ名</th>
<th>機能</th>
</tr><tr>
<td>sdkAppId</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a> で SDKAppIDを表示できます。</td>
</tr><tr>
<td>userId</td>
<td>現在のユーザーID。文字列タイプでは、英語のアルファベット（a-z、A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。業務の実際のアカウントシステムと組み合わせてご自身で設定することをお勧めします。</td>
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
1. キャスターは、[手順4](#model.step4)でログインした後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. キャスターは、`setDelegate`を呼び出して、`createMeeting`のイベントの呼び出しを実行し、新しいミーティングルームを作成することができます。
3. キャスターは、`startCameraPreview`を呼び出してビデオ画面をキャプチャすることができ、`startMicrophone`を呼び出して音声をキャプチャすることもできます。
4. キャスターに美顔のニーズがある場合は、インターフェース上に美顔調節ボタンを設定して呼び出すことができ、`getBeautyManager`を介して美顔設定を行います。
>? エンタープライズ版以外のSDKは変顔やスタンプの機能をサポートしていません。

![](https://main.qcloudimg.com/raw/416a1afd87b196a6ef791bf63eeaa5e0.png)

```swift
// 1.キャスターは、ニックネームおよびプロフィール画像を設定します
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
1. 参加者は、[手順4](#model.step4)でログインした後、`setSelfProfile`を呼び出して自身のニックネームおよびプロフィール画像を設定することができます。
2. 参加者は、`enterMeeting`を呼び出し、ミーティングルーム番号を渡すと、ミーティングルームに参加できます。
3. 参加者は、`startCameraPreview`を呼び出してビデオ画面をキャプチャでき、`startMicrophone`を呼び出して音声をキャプチャできます。
4. 他の参加者がカメラを起動すると、`onUserVideoAvailable`のイベントを受信します。この時、 `startRemoteView`を呼び出してuserIdを渡すと、再生が開始されます。

![](https://main.qcloudimg.com/raw/f33213dea7a32ca9904c066952fcc535.png)

```swift
// 1.参加者がニックネームとプロフィール画像を設定します
trtcMeeting.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

// 2.enterMeeting関数を実装します
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
  //コールバックを受信し、startRemoteViewを呼び出してuserIdを渡すと、再生が開始されます
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

[](id:model.step7)
### 手順7：画面共有
1. `startScreenCapture`を呼び出し、エンコードパラメータとスクリーンキャプチャプロセスのフローティングウィンドウを渡すと、画面共有機能を実装できます。具体的な情報については、[TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97)をご参照ください。
2. ミーティング中の他の参加者が、`onUserVideoAvailable`のイベントの通知を受信します。

>!画面共有とカメラのキャプチャの2つは相互排他的な操作です。画面共有機能を立ち上げたい時は、先に`stopCameraPreview`を呼び出し、カメラのキャプチャをオフにしてください。

```swift
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
}else{
  self.view.makeToast("システムのバージョンが12.0より低い場合は、システムをバージョンアップにしてください。")
}     
```

[](id:model.step8)
### 手順8：文字チャットとミュートメッセージの実現
- `sendRoomTextMsg`によって通常のテキストメッセージを送信できるようになり、該当するルーム内の全てのキャスターおよび視聴者が`onRecvRoomTextMsg`のコールバックを受信することができます。
IMバックエンドは、デフォルトでNGワードフィルター規則を有し、NGワードと認識されたテキストメッセージはクラウドに転送されることはありません。
```swift
// 送信側：テキストメッセージの送信
TRTCMeeting.sharedInstance().sendRoomTextMsg("Hello Word!") { (code, message) in
  debugPrint("send result: ", code)
}

// 受信側：テキストメッセージのモニタリング
func onRecvRoomTextMsg(_ message: String?, userInfo: TRTCMeetingUserInfo) {
  debugPrint(":\(String(describing: userInfo.userId))から受信したメッセージ\(String(describing: message))")
}
```
- `sendRoomCustomMsg`によってカスタマイズ（シグナリング）情報を発信することができます。そのルーム内のすべてのキャスターおよび視聴者は`onRecvRoomCustomMsg`のコールバックを受信することができます。
カスタムメッセージは、通常カスタマイズしたシグナリングの転送に使用します（例：ミュートの会場内制御など）。
```swift
// 送信側：カスタマイズしたCmdでミュートの通知を区別できます
// eg:"CMD_MUTE_AUDIO"はミュートの通知を表します
TRTCMeeting.sharedInstance().sendRoomCustomMsg("CMD_MUTE_AUDIO", message: "1") { (code, message) in
  debugPrint("send result: ", code)
}

// 受信側：カスタムメッセージのモニタリング
func onRecvRoomCustomMsg(_ cmd: String?, message: String?, userInfo: TRTCMeetingUserInfo) {
  if cmd == "CMD_MUTE_AUDIO" {
    debugPrint(":\(String(describing: userInfo.userId))からミュート通知を受信しました:\(String(describing: message))")
    TRTCMeeting.sharedInstance().muteLocalAudio(message == "1")
  }
}
```
