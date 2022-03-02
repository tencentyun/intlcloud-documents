## デモンストレーション
当社のAppを[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)してインストールし、多人数ビデオ会話の効果をご体験いただけます。これには、画面共有、美顔、低遅延ビデオ通話など、TRTCの多人数オーディオビデオシーン関連の機能が含まれています。




## ソリューションの優位性
- 超低遅延のオーディオビデオ通話、画面共有、美顔などの機能を統合し、多人数オーディオビデオルームの一般的な機能をカバーします。
- 二次開発の需要に応じて、カスタムUIやレイアウトを迅速に実装し、ビジネスの迅速な立ち上げに役立ちます。
- TRTCとIMの基本SDKをカプセル化し、基本的なロジックコントロールを実装し、呼び出しを容易にするインターフェースを提供します。

## アクセスガイド
多人数オーディオビデオルームの機能に素早くアクセスしたい場合は、当社が提供するAppを直接修正して適応させるか、App内のModuleを使用してカスタマイズしたUIを実装することができます。

[](id:ui_step1)
### 手順1：アプリケーションの新規作成
1. TRTCコンソールにログインし、**開発支援**>[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)を選択します。
2. `TestTUIRoom`などのアプリケーション名を入力して、**作成**をクリックします。
3. **ダウンロードしました。次のステップ**をクリックすると、この手順をスキップします。

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>!本機能はTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。

[](id:ui_step2)
### 手順2：Appソースコードのダウンロード
クリックして[TUIRoom](https://github.com/tencentyun/TUIRoom)に進み、ソースコードをCloneまたはダウンロードします。

[](id:ui_step3)
### 手順3：Appプロジェクトファイルの設定
1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `Example/Debug/GenerateTestUserSig.swift`ファイルを見つけて開きます。
3.`GenerateTestUserSig.swift`ファイル内の関連パラメータを設定します。
<ul style="margin:0"><li/>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。
<li/>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png" width="750" height="395"/>

4. 貼り付け完了後、**貼り付けました。次のステップ**をクリックすれば、作成が完了します。
5. コンパイル完了後、 **コンソール概要に戻る** をクリックすれば終了です。

>?
>- ここで言及するUserSigの発行方法は、クライアントコードの中でのSECRETKEY設定となりますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者がお客様のTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのAppクイックスタートおよび機能デバッグにのみ適しています**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[UserSigに関するご質問](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:ui_step4)
### 手順4：プロジェクトの実行
Xcode（11.0およびそれ以降のバージョン）を使用してソースコードプロセス`Example/DemoApp.xcworkspace`を開き、**実行**をクリックすれば、このAppのデバッグが開始されます。

[](id:ui_step5)
### 手順5：プロジェクトソースコードの修正
ソースコードの`Source`にはUIフォルダが含まれ、このフォルダはいずれもUIに関連するコードです。以下の表には各フォルダに対応するUIをリストアップし、二次調整に役立つようにしています。

| フォルダ | 機能説明 |
|:-------:|:--------|
| TUIRoomEnter | TUIRoomエントリーに関連する実装コードです。TUIRoomEntranceViewControllerクラスはPodsを外部に公開するパブリッククラスです。 |
| TUIRoomMain | TUIRoomメインインターフェースに関連するUI実装コードです。このクラスはPodsプライベートクラスです。 |
| TUIRoomMemberList | メンバーリストインターフェースに関連するUI実装コードです。このクラスはPodsプライベートクラスです。 |
| TUIRoomSet | インターフェース設定に関連するUI実装コードです。このクラスはPodsプライベートクラスです。 |

## 体験アプリケーション
>! 体験アプリケーションには、少なくとも2台のデバイスが必要です。
### エントリーインターフェース
図のように、**ルームの作成**または**ルームへの参加**を選択してください。

### ルーム作成ページ
ユーザーAが作成し、ルームナンバーはデフォルトで発行されます。**ルーム作成**をクリックすると、メインページに進むことができます。


### ルーム参加ページ
ユーザーBはユーザーAのルームナンバーを入力し、**ルームへの参加**をクリックすると、メインページに進むことができます。



### メインページ（ユーザーA）
<img src="https://qcloudimg.tencent-cloud.cn/raw/eebab2b82db719000f0dc376070a25e7.png" width=300px>


### 配信側リスト
配信側リストには現在のルームのメンバーを表示できます。相手がカメラとマイクを起動すると、相手の画面を見ること、相手の声を聞くことができます。

### 上部のコントロールバー
イヤホン/マイク切り替え、フロント/リアカメラ切り替え、ルーム情報、退出の機能を実装しました。

### 下部のツールバー
自身のマイク/カメラの制御、美顔、メンバーリスト、設定などの機能を実装しました。

### 美顔
ライブストリーミング中に画面に対し美顔およびエフェクト表示を行うことができます。



### 設定ウィンドウ
オーディオビデオ関連パラメータを設定でき、**画面共有**の開始をサポートします。



### 退室
- **キャスター**：ルームを解散し、全員を退室させます。
- **キャスター以外**：自ら退室します。

## UIカスタマイズの実装

[ソースコード](https://github.com/tencentyun/TUIRoom)の`Source`フォルダにはUIとPresenterが含まれ、Presenterフォルダには再利用できるオープンソースコンポーネントTUIRoomCoreが含まれています。`TUIRoomCore.h`ファイルでこのコンポーネントが提供するインターフェース関数を確認し、対応するインターフェースを使用してカスタマイズしたUIを実装することができます。
![#600px](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)

[](id:ui_step1)
### 手順1：SDKの統合 
多人数オーディオビデオコンポーネントTUIRoomは、TRTC SDKとIM SDKに依存しています。次の手順で2つのSDKをプロジェクトに統合することができます。

- **方法1：cocoapodsリポジトリを介する依存**
```
 pod 'TXIMSDK_iOS'
 pod 'TXLiteAVSDK_TRTC'
```
>? 2つのSDK製品の最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK)および[IM](https://github.com/tencentyun/TIMSDK)のGithubトップページで取得することができます。
- **方法2：ローカルを介する依存**
開発環境でのcocoapodsリポジトリへのアクセスが遅い場合は、ZIPパッケージを直接ダウンロードし、統合ドキュメントに従って手動でプロジェクトに統合することができます。
<table>
<thead><tr><th>SDK</th><th>ダウンロードページ</th><th>統合ガイド</th></tr></thead>
<tbody><tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35092">統合ドキュメント</a></td>
</tr>
<tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34307">統合ドキュメント</a></td>
</tr>
</tbody></table>

[](id:model_step2)
### 手順2：権限の設定
`info.plist`ファイルに`Privacy > Camera Usage Description`と`Privacy > Microphone Usage Description`を追加し、カメラとマイクの権限をリクエストする必要があります。

[](id:model_step3)
### 手順3：TUIRoomコンポーネントのインポート
**cocoapodsを使用してコンポーネントをインポート**することができます。具体的な手順は、以下のとおりです。
1. プロジェクトディレクトリの`Source`、`Resources`、`TCBeautyKit`、`TXAppBasic`フォルダ、`TUIRoom.podspec`ファイルをお客様のプロジェクトディレクトリ下へコピーします。
2. `Podfile`ファイル内に以下の依存関係を追加します。その後、`pod install`コマンドを実行すると、インポートが完了します。
```swift
# ローカル依存ライブラリ
def local
  pod 'TXAppBasic', :path => "../../TXAppBasic/"
  pod 'TCBeautyKit', :path => "../../TCBeautyKit/"
  pod 'TXLiteAVSDK_TRTC',:path => "../../../SDK/"
end

def pod_local(type)
  loadLocalPod('TUIRoom', type)
end

def loadLocalPod(name, type)
    pod "#{name}/#{type}", :path => "../"
end

target 'DemoApp' do
  local
  pod_local('TRTC')
end
```

[](id:model_step4)
### 手順4：コンポーネントの作成およびログイン
1.  TUICoreのTUILoginを呼び出してログインします。次の例をご参照ください。
```swift
TUILogin.initWithSdkAppID(Int32(SDKAPPID))
let userID = ProfileManager.shared().curUserID()
let userSig = GenerateTestUserSig.genTestUserSig(userID)
TUILogin.login(userID, userSig: userSig, succ: {
    debugPrint("login success") 
}, fail: { (code, errorDes) in
   debugPrint("login failed, code:\(code), error: \(errorDes ?? "nil")")
})
```
2. 正常にログインした後、TUIRoomCoreを呼び出してルームを作成することができます。
```swift
let roomId = 123
TUIRoomCore.shareInstance().createRoom("\(roomId)",speechMode: .freeSpeech,callback: { [weak self] code, message in
    if code == 0 {
       debugPrint("create room success") 
    }else{
    }
})
```
4. 作成に成功し、メインページに進みます。
```swift
let vc = TUIRoomMainViewController(roomId: roomId, isVideoOn: openCameraSwitch.isOn, isAudioOn: openMicSwitch.isOn)
TUIRoomCore.shareInstance().setDelegate(vc)
navigationController?.pushViewController(vc, animated: true)
```
![#600px](https://qcloudimg.tencent-cloud.cn/raw/8c3391905188089fecd17e23477d34ea.png)

[](id:model_step5)
### ステップ5：メンバーの入室
1. メンバーはTUICoreのTUILoginを呼び出してログインします。次の例をご参照ください。
```swift
TUILogin.initWithSdkAppID(Int32(SDKAPPID))
let userID = ProfileManager.shared().curUserID()
let userSig = GenerateTestUserSig.genTestUserSig(userID)
TUILogin.login(userID, userSig: userSig, succ: {
    debugPrint("login success") 
}, fail: { (code, errorDes) in
   debugPrint("login failed, code:\(code), error: \(errorDes ?? "nil")")
})
```
2. 正常にログインした後、TUIRoomCrreを呼び出して入室できます。
```swift
let roomId = 123
TUIRoomCore.shareInstance().enterRoom("\(roomId)", callback: { [weak self] code, message in
    if code == 0 {
	    debugPrint("enter room success") 
	}else{
	}
})
```
4. 入室に成功した後、再びメインページに進みます。
```swift
let vc = TUIRoomMainViewController(roomId: roomId, isVideoOn: openCameraSwitch.isOn, isAudioOn: openMicSwitch.isOn)
TUIRoomCore.shareInstance().setDelegate(vc)
navigationController?.pushViewController(vc, animated: true)
```
![#600px](https://qcloudimg.tencent-cloud.cn/raw/ffbda4de381ea198bf808de7d823ab59.png)

[](id:model_step6)
### 手順6：画面共有
1. TUIRoomCoreの`startScreenCapture`を呼び出して共有します。
2. ルーム内のその他メンバーは`onRemoteUserScreenVideoAvailable`のイベント通知を受信します。

```swift
// ボタンのクリックで画面共有を実現します
if #available(iOS 12.0, *) {
    // 画面共有
    let params = TRTCVideoEncParam()
    params.videoResolution = TRTCVideoResolution._1280_720
    params.resMode = TRTCVideoResolutionMode.portrait
    params.videoFps = 10
    params.enableAdjustRes = false
    params.videoBitrate = 1500
    TUIRoomCore.shareInstance().startScreenCapture(params)
    TUIRoomBroadcastExtensionLauncher.launch()
}else{
    view.window?.makeToast(.versionLowToastText)
}    
```

[](id:step)
### ステップ7：退室
- **キャスター**はdestoryRoomインターフェースを呼び出してルームを解散し、IMグループチャットを解散し、TRTCルームを退室します。 メンバー側は、グループを解散し、TRTCルームを退室するよう通知するonDestroyRoomコールバックメッセージを受信します。
- **メンバー**はleaveRoomインターフェースを呼び出してルームを解散し、IMグループチャットから退出し、TRTCルームを退室します。 その他のメンバー側は、メンバーが退室したことを通知するonRemoteUserLeaveコールバックメッセージを受信します。

```swift
if isHomeowner {
    TUIRoomCore.shareInstance().destroyRoom { [weak self] _, _ in
        guard let self = self else { return }
        self.navigationController?.popViewController(animated: true)
    }
}else{
    TUIRoomCore.shareInstance().leaveRoom { [weak self] _, _ in
        guard let self = self else { return }
        self.navigationController?.popViewController(animated: true)
    }
 }
```
