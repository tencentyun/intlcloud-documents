## デモンストレーション
Appを[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)してインストールすると、TRTC通話の効果を体験できます。
<table>
<tr>
   <th>発呼側</th>
   <th>着呼側</th>
 </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/ef83db73d0a8c487e72986dd1f92e361.jpeg"/></td>
<td><img src="https://main.qcloudimg.com/raw/f57ed3a55112233b05260f5dc37342ca.jpeg"/></td>
</tr>
</table>



>! オーディオビデオ通話機能を素早く実装できるように、当社はTUICallingコンポーネントをリモデルし、通話UIをTUICallingコンポーネントの内部に実装しました。お客様がUIに気をつかう必要はありません。

[](id:ui)

## Appの実行と体験

[](id:ui.step1)

### 手順1：アプリケーションの新規作成
1. TRTCコンソールにログインし、**開発支援>[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)**を選択します。
2．アプリケーション名（例：`TestVideoCall`）を入力して、**作成**をクリックします。
3. **ダウンロードしました。次のステップ**をクリックすると、この手順をスキップします。

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)
>!本機能はTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。


[](id:ui.step2)
### 手順2：Appソースコードのダウンロード
クリックして[TUICalling](https://github.com/tencentyun/TUICalling)に進み、ソースコードをCloneまたはダウンロードします。

[](id:ui.step3)
### 手順3：Appプロジェクトファイルの設定
1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `iOS/Example/Debug/GenerateTestUserSig.swift`のファイルを見つけて開きます。
3.`GenerateTestUserSig.swift`ファイル内の関連パラメータを設定します。
<ul style="margin:0"><li/>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。
<li/>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. 貼り付け完了後、**貼り付けました。次のステップ**をクリックすれば、作成が完了します。
5. コンパイル完了後、 **コンソール概要に戻る** をクリックすれば終了です。

>!
>- ここで言及するUserSigの発行方法は、クライアントコードの中でのSECRETKEY設定となりますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者がお客様のTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのAppクイックスタートおよび機能デバッグにのみ適しています**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[UserSigに関するご質問](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:ui.step4)
### 手順4：Appの実行

Xcode（バージョン11.0以上）を使用してソースコードプロジェクト`TUICalling/Example/TUICallingApp.xcworkspace`を開き、**実行**をクリックすれば、このAppのデバッグが開始されます。



## 体験アプリケーション
>! 体験アプリケーションには、少なくとも2台のデバイスが必要です。

### ユーザーA
1. ユーザー名を入力し（**ユーザー名は一意のものとし、他のユーザーと重複しないようにしてください**）、ログインします。
2. 電話をかけたいuserIdを入力し、検索をクリックします。
3. **呼出**をクリックし、**ビデオ通話**を選択して電話をかけます（**着呼者がアプリケーション内にいることを保証してください。保証できない場合、電話をかけても失敗する可能性があります**）。<br>


### ユーザーB
1. ユーザー名を入力し（**ユーザー名は一意のものとし、他のユーザーと重複しないようにしてください**）、ログインします。
2. メインページに進み、通話応答を待ちます。



[](id:model)
## 具体的な接続フロー

[ソースコード](https://github.com/tencentyun/TUICalling/tree/master/Android/Source/src/main/java/com/tencent/liteav/trtccalling)の`Source`フォルダの中にはui、model、Serviceの3つのサブフォルダが含まれています。そのうち、Serviceフォルダには外部に公開しているオープンソースコンポーネントTUICallingManagerが含まれています。`TUICallingManager.h`ファイルの中でこのコンポーネントが提供するインターフェース関数を見つけることができます。
![](https://qcloudimg.tencent-cloud.cn/raw/0de26d679e6e0dc1d9aeadb6dbf6f8aa.png)


オープンソースコンポーネントTUICallingのTUICallingManagerをそのまま使用し、オーディオビデオ通話機能を手軽に実装することができます。もう複雑な通話UIやロジックの実装をご自身で行う必要はありません。

[](id:model.step1)
### 手順1：SDKの統合 

通話コンポーネントTRTCCallingは、TRTC SDKとIM SDKに依存し、次の手順で2つのSDKをプロジェクトに統合することができます。

- **方法1：cocoapodsリポジトリを介する依存**
<dx-codeblock>
::: swift
 pod 'TXIMSDK_iOS'
 pod 'TXLiteAVSDK_TRTC' 
:::
</dx-codeblock>
>?2つのSDK製品の最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK)と[IM](https://github.com/tencentyun/TIMSDK) のGithubトップページで取得することができます。
- **方法2：ローカルを介する依存**
開発環境でのcocoapodsリポジトリへのアクセスが遅い場合は、ZIPパッケージを直接ダウンロードし、統合ドキュメントに従って手動でプロジェクトに統合することができます。
<table>
<tr>
<th>SDK</th>
<th>ダウンロードページ</th>
<th>統合ガイド</th>
</tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35092">統合ドキュメント</a></td>
</tr>
<tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">統合ドキュメント</a></td>
</tr>
</table>

[](id:model.step2)
### 手順2：権限の設定

info.plistファイルに`Privacy - Camera Usage Description`、`Privacy - Microphone Usage Description`を追加し、カメラとマイクの権限を申請する必要があります。

[](id:model.step3)
### 手順3：TUICallingコンポーネントをインポート
**cocoapodsによってコンポーネントをインポートします**。具体的な手順については、以下のとおりです。
1. プロジェクトディレクトリ下の`Source`、`Resources`、`TXAppBasic`フォルダ、`TUICalling.podspec`ファイルをプロジェクトディレクトリ下へコピーします。
2. `Podfile`ファイル内に以下の依存関係を追加します。その後、`pod install`コマンドを実行すると、インポートが完了します。
<dx-codeblock>
::: swift
 pod 'TXAppBasic', :path => "../TXAppBasic/"
 pod 'TXLiteAVSDK_TRTC'
 pod 'TUICalling', :path => "../", :subspecs => ["TRTC"] 
:::
</dx-codeblock>

[](id:model.step4)

### 手順4：コンポーネントの初期化およびログイン

1. `TUICallingManager.sharedInstance()`を呼び出し、コンポーネントを初期化します。
2. `TUILogin.initWithSdkAppID(SDKAPPID)`を呼び出し、ログインを初期化します。
3. `TUILogin.login(userId, userSig)`を呼び出し、コンポーネントのログインを完了します。このうちの重要なパラメータの入力については、下表をご参照ください。
<table>
<tr><th>パラメータ名</th><th>作用</th></tr>
<tr>
<td>sdkAppID</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a> で SDKAppIDを表示できます。</td>
</tr><tr>
<td>userId</td>
<td>現在のユーザーID。文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。業務の実際のアカウントシステムと組み合わせてご自身で設定することをお勧めします。</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloudによって設計されたセキュリティ保護署名。計算方法については<a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSigの計算方法</a>をご参照ください。</td>
</tr></table>

<dx-codeblock>
::: swift
// コンポーネントの初期化
TUICallingManager.sharedInstance();
// ログイン
TUILogin.initWithSdkAppID(SDKAPPID)
TUILogin.login(userId, userSig) {
   print("login success")
} fail: { code, errorDes in
   print("login failed, code:\(code), error: \(errorDes ?? "nil")")
}
:::
</dx-codeblock>

[](id:model.step5)

### 手順5：オーディオビデオ通話の実装

1. 発信側：TUICallingManagerの`call();`メソッドを呼び出して通話リクエストを送信し、ユーザーIDの配列（userIDs）と通話タイプ（type）を渡します。通話タイプパラメータは`.audio`（オーディオ通話）または`.video`（ビデオ通話）を渡します。ユーザーID配列（userIDs）のuserIDが1つのみの時は、シングル通話と見なされ、ユーザーID配列（userIDs）のuserIDが複数（>=2）の時は多人数通話と見なされます。
2. 受信側：受信側がログイン状態の場合は、対応するインターフェースが自動的に起動します。受信側がログインしていない状態でも通話リクエストを受け取りたい場合は、[オフライン応答](#model.offline)をご参照ください。

<dx-codeblock>
::: swift
//1. リスナーの登録
TUICallingManager.shareInstance().setCallingListener(listener: TUICallingListerner())

// 2. カスタムページ設定の有無（デフォルトはオフ）
TUICallingManager.shareInstance().enableCustomViewRoute(enable: true)

// 3. リスナーコールバックメソッドの実装
public func shouldShowOnCallView() -> Bool {
    return true;
}

public func callStart(userIDs: [String], type: TUICallingType, role: TUICallingRole, viewController: UIViewController?) {         if let vc = viewController {
        callingVC = vc;
        vc.modalPresentationStyle = .fullScreen
            
        if var topController = UIApplication.shared.keyWindow?.rootViewController {
            while let presentedViewController = topController.presentedViewController {
                topController = presentedViewController
            }
                
            if let navigationVC = topController as? UINavigationController {
                if navigationVC.viewControllers.contains(self) {
                    present(vc, animated: false, completion: nil)
                }else{
                    navigationVC.popToRootViewController(animated: false)
                    navigationVC.pushViewController(self, animated: false)
                    navigationVC.present(vc, animated: false, completion: nil)
                }
            }else{
                topController.present(vc, animated: false, completion: nil)
            }
        }
    }
}

public func callEnd(userIDs: [String], type: TUICallingType, role: TUICallingRole, totalTime: Float) {
    callingVC.dismiss(animated: true, completion: nil)
}
    
public func onCallEvent(event: TUICallingEvent, type: TUICallingType, role: TUICallingRole, message: String) {
       	
}
// 4.電話をかけます
TUICallingManager.shareInstance().call(userIDs, .video)
:::
</dx-codeblock>

[](id:model.offline)


### 手順6：オフライン応答の実装

>?ビジネスの位置付けがオンラインカスタマーサービスなどのオフライン応答機能を必要としないシーンである場合は、上記[手順1]（＃model.step1）-[手順5]（＃model.step5）の対応で問題ありません。 しかし、ビジネスの位置付けがソーシャルシーンである場合は、オフライン応答を実装することをお勧めします。

IM SDKはオフラインプッシュをサポートしていますが、使用可能な基準を満たすためには相応の設定を行う必要があります。

1. Appleプッシュ証明書を申請する場合の具体的な操作については、[Appleプッシュ証明書の申請](https://intl.cloud.tencent.com/document/product/1047/34346)をご参照ください。
2. バックエンドおよびクライアントがオフラインプッシュを設定する場合の具体的な操作については、[オフラインプッシュ（iOS）](https://intl.cloud.tencent.com/document/product/1047/39157)をご参照ください。
3. 現在、TRTCCallingImplのsendModelシグナリング送信関数にオフライン送信関数が統合されており、Appのオフラインプッシュを設定した後、メッセージのオフラインプッシュを実装することができます。

[](id:api)

## コンポーネントAPIリスト

TUICallingコンポーネントのAPIインターフェースリストは次のとおりです。

| インターフェース関数        | インターフェースの機能                                                 |
| --------------- | --------------------------------------------------------- |
| call            | C2C通話に招待します         |
| receiveAPNSCalled          | 被招待者として着信に応答します                                      |
| setCallingListener          | リスナーを設定します                                     |
| setCallingBell          | 着信音の設定(30s以内を推奨)                                                 |
| enableMuteMode | ミュートモードをオンにします    |
| enableCustomViewRoute      | カスタムビューをオンにします。オンにすると、呼び出し/被呼び出し開始コールバックの中で、CallingViewのインスタンスを受信します。開発者自身が表示方式を決定します。注意：フルスクリーンまたはスクリーンと同じ比率で表示する必要があります。そうしない場合、表示に異常が生じます            |

