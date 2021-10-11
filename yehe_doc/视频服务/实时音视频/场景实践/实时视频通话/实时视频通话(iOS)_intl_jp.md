## デモンストレーション
Appを[ダウンロード](https://intl.cloud.tencent.com/document/product/647/35076)してインストールし、リアルタイムビデオ通話の効果を体験できます。



ビデオ通話機能をすばやく実装する必要がある場合、当社が提供するAppをもとに直接適応に変更を加えることも、当社が提供するTUICallingコンポーネントでカスタマイズしたUIを実装することもできます。

>! 当社はTRTCVideoCallコンポーネントを過去に提供していましたが、旧バージョンのコンポーネントは[コンポーネントリポジトリ](https://github.com/tencentyun/LiteAVClassic)に移動済みです。TUICallingコンポーネントはIMシグナリングのインターフェースを使用するため、旧コンポーネントとの互換性がなくなります。

[](id:ui)

## AppのUIの再利用

[](id:ui.step1)

### 手順1：アプリケーションの新規作成
1．TRTCコンソールにログインし、【開発支援】>【[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2．`TestVideoCall`などアプリケーション名を入力して、【作成】をクリックします。

3. ダウンロード完了後、【ダウンロードしました。次のステップ】をクリックし、次へ進みます。

![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
>!本機能はTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については、[Instant Messagingの料金説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。


[](id:ui.step2)
### 手順2：Appソースコードのダウンロード
クリックして[TUICalling](https://github.com/tencentyun/TUICalling)に進み、ソースコードをCloneまたはダウンロードします。

[](id:ui.step3)
### 手順3：Appプロジェクトファイルの設定
1. 設定変更ページに進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `TUICalling/Debug/GenerateTestUserSig.swift`ファイルを見つけて開きます。
3.`GenerateTestUserSig.swift`ファイル内の関連パラメータを設定します。
<ul style="margin:0"><li/>SDKAPPID：デフォルトは0。実際のSDKAppIDを設定してください。
<li/>SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。</ul>

4. 貼り付け完了後、【貼り付けました。次のステップ】をクリックすれば、作成が完了します。
5. コンパイル完了後、【コンソール概要に戻る】をクリックすればOKです。

>!
>- ここで言及したUserSigの作成法は、クライアントコードにSECRETKEYを設定しますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのAppクイックスタートおよび機能デバッグにのみ適しています**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを送信し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:ui.step4)
### 手順4：Appの実行

Xcode（11.0およびそれ以降のバージョン）を使用してソースコードプロセス`TUICalling/TUICallingApp.xcworkspace`を開き、【実行】をクリックすれば、このAppのデバッグが開始されます。

[](id:ui.step5)
### 手順5：Appソースコードの修正

ソースコードフォルダ`Source`に2つのサブフォルダuiとmodelが含まれ、その内、uiフォルダに含まれるのはすべてインターフェースコードです。

|             ファイルまたはフォルダ             | 機能の説明                                                 |
| ------------------------------------ | ------------------------------------------------------- |
|  TRTCCallingVideoViewController.swift  |ビデオ通話のメインインターフェースが表示され、このインターフェースで通話の応答と拒否が完了します。|
|  TRTCCallingAudioViewController.swift  |音声通話のメインインターフェースが表示され、このインターフェースで通話の応答と拒否が完了します。 |


## 体験アプリケーション
>! 体験アプリケーションには、少なくとも2台のデバイスが必要です。

### ユーザーA
1. 図のように、ユーザー名を入力し（**ユーザー名は一意のものとし、他のユーザーと重複しないようにしてください**）、ログインします。
2. 下図のように、電話をかける相手ユーザーの名前を入力し、【検索】をクリックします。
3. 【呼び出し】をクリックし、【ビデオ通話】を選択します（**着呼者がアプリケーション内にいることを保証してください。保証できない場合、電話をかけても失敗するかもしれません**）。

### ユーザーB
1. 図のように、ユーザー名を入力し（**ユーザー名は一意のものとし、他のユーザーと重複しないようにしてください**）、ログインします。
2. メインページに進み、通話応答を待ちます。


[](id:model)
## カスタマイズUIの実装

[ソースコード](https://github.com/tencentyun/TUICalling)フォルダ`Source`には2つのサブフォルダuiとmodelが含まれ、そのうちmodelフォルダには当社が実装した再利用可能なオープンソースコンポーネントTRTCCallingが含まれています。このコンポーネントが提供するインターフェース関数は`TRTCCalling.h`ファイルで確認できます。
![](https://main.qcloudimg.com/raw/9b4087b68541912ce9e7a48955cd48e8.png)

オープンソースコンポーネントTRTCCallingを使用すれば、自分のUIを実装することができます。すなわちmodelパーツを再利用するだけで、自分でUIパーツを実装できます。

[](id:model.step1)
### 手順1：SDKへの統合

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
 pod 'TXAppBasic', :path => "TXAppBasic/"
 pod 'TXLiteAVSDK_TRTC'
 pod 'TUICalling', :path => "./", :subspecs => ["TRTC"] 
:::
</dx-codeblock>

[](id:model.step4)
### 手順4：コンポーネントの初期化およびログイン

1. プッシュ関連情報を設定します。
<dx-codeblock>
::: swift
 [TRTCCalling shareInstance].imBusinessID = your business ID;
 [TRTCCalling shareInstance].deviceToken =  deviceToken;
:::
</dx-codeblock>
>?  imBusinessIDは、[IMコンソール](https://console.cloud.tencent.com/im)に進んでAPNs証明書をアップロードすると発行されます。その後すぐにAppDelegateを介してAppleバックエンドにコールバックがリクエストされると、対応するdeviceToken値が返されます。具体的な操作については、[オフラインプッシュ](https://intl.cloud.tencent.com/document/product/1047/34347)をご参照ください。
2. `login(sdkAppID: UInt32, user: String, userSig: String, success: @escaping (() -> Void), failed: @escaping ((_ code: Int, _ message: String) -> Void))` を呼び出し、コンポーネントのログインを完了します。なおいくつかの重要パラメータの入力については下表をご参照ください。
<table>
<tr><th>パラメータ名</th><th>作用</th></tr>
<tr>
<td>sdkAppID</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a> で SDKAppIDを表示できます。</td>
</tr><tr>
<td>user</td>
<td>現在のユーザーID。文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。</td>
</tr><tr>
<td>userSig</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSigの計算方法</a>。</td>
</tr></table>
<dx-codeblock>
::: Objective-C Objective-C
// ログイン
[[TRTCCalling shareInstance] login:SDKAPPID user:userID userSig:userSig success:^{
        NSLog(@"Video call login success.");
} failed:^(int code, NSString *error) {
        NSLog(@"Video call login failed.");
}];
:::
</dx-codeblock>


[](id:model.step5)
### 手順5：1v1通話の実現

1. 発信者：`TRTCCalling`の`call(userId, callType)`を呼び出し、`userId`パラメータをユーザーIDとし、`callType`パラメータを通話タイプとして、パラメータ`CallType_Video`を渡すと、ビデオ通話のリクエストを開始することができます。
2. 受信者：受信者がログイン状態の場合は、`onInvited()`という名称のコールバックを受け取り、コールバックにおける`callType`のパラメータは発信者が入力した通話タイプであり、このパラメータを介して対応するインターフェースを起動することができます。受信者がログインしていない状態でも通話リクエストを受け取りたい場合は、[オフライン応答](#offline)をご参照ください。
3. 受信者：電話に対応したい場合、受信者は`accept()`関数を呼び出すことができ、ビデオ通話である場合は、同時に`openCamera()`関数を呼び出して、自身のローカルカメラを起動します。受信者は`reject()`を呼び出し、この通話を拒否することもできます。
4. 双方のオーディオビデオチャネルが確立した後、通話する双方はさらに`onUserVideoAvailable()`という名称のコールバックを受け取ります。これは、相手方のビデオ画面を取得済みであることを示しています。このとき、双方のユーザーは`startRemoteView()`を呼び出し、リモートのビデオ画面を表示することができます。リモートの音声はデフォルトで自動再生に設定されています。

<dx-codeblock>
::: Objective-C Objective-C
// 1.監視のコールバック
[[TRTCCalling shareInstance] addDelegate:delegate];

// 応答/拒否
// BもIMシステムにログインしている場合は、onInvited(A, null, false) のコールバックを受け取ることができます。
// TRTCCallingのacceptメソッドを呼び出して受信することができます / TRTCCallingのreject メソッドを呼び出して拒否することができます
-(void)onInvited:(NSString *)sponsor
         userIds:(NSArray<NSString *> *)userIds
     isFromGroup:(BOOL)isFromGroup
        callType:(CallType)callType {
    [[TRTCCalling shareInstance] accept];
}

// 2.相手方の画面の視聴
// Aがカメラを起動しているので、Bは通話を受信した後、onUserVideoAvailable(A, true)のコールバックを受け取ります
- (void)onUserVideoAvailable:(NSString *)uid available:(BOOL)available {
  if (available) {
    UIView* renderView =[[UIView alloc] init];
    [[TRTCCalling shareInstance] startRemoteView:uid view:renderView]; // 相手方の画面を見ることができます
  } else {
    [[TRTCCalling shareInstance] stopRemoteView:uid]; // 画面のレンダリングを停止します
  }
}

// 3.コンポーネントの他の機能の関数を呼び出し、通話を開始したり終了したりします
// 注意：ログインしなければ正常に呼び出すことはできません
// ビデオ通話を開始します
[[TRTCCalling shareInstance] call:@"ターゲットユーザー" type:CallType_Video];
// 通話を終了します
[[TRTCCalling shareInstance] hangup];
// 拒否します
[[TRTCCalling shareInstance] reject];
:::
</dx-codeblock>

[](id:model.step6)
### 手順6：多人数のビデオ通話を実現

1. 発信者：多人数のビデオ通話では、`TRTCCalling`の`groupCall()`関数を呼び出し 、ユーザーリスト（userIdList）、グループIM ID（groupId）、通話タイプ（callType） を入力する必要があります。なおuserIdListは入力必須パラメータ、groupIdはオプションパラメータ、callType`はビデオタイプ`CallType_Video`とします。
2. 受信者： `onInvited()`という名称のコールバックを介してこの呼び出しリクエストを受け取ることができます。なおパラメータリストは発信者が入力したパラメータリストであり、`callType` パラメータは通話タイプであって、このパラメータを介して対応するインターフェースを起動することができます。
3. 受信者：コールバックを受け取った後、`accept()` メソッドを呼び出し、この通話に応答することができます。`reject()` メソッドを呼び出して通話の拒否を選択することもできます。
4. 一定時間（デフォルトは30s）を超えて応答しなかった場合、受信者は`onCallingTimeOut()`のコールバックを受け取り、発信者は`onNoResp()`というコールバックを受け取ります。通話発信者が複数の着信に応答しない場合は`hangup()`のイベント通知を受け取り 、各受信者は`onCallingCancel()`という コールバックを受け取ります。
5. 現在の多人数の通話から退出したい場合は、`hangup()`メソッドを呼び出します。
6. 通話中にユーザーが途中参加または退出する場合、他のユーザーは`onUserEnter()`または `onUserLeave()`というコールバックを受け取ります。

>?インターフェース`groupCall:type:groupID:`における`groupID`パラメータはIM SDKにおけるグループIDです。このパラメータを設定すると、通話リクエストメッセージのシグナリングメッセージはグループIDを介して発信されます。このメッセージブロードキャスト方式は簡単で信頼性の高い方法です。設定しない場合は、`TRTCalling`コンポーネントが単発メッセージで1人1人に通知を行います。

<dx-codeblock>
::: Objective-C Objective-C
// 前記省略...
// ダイヤルするユーザーリストをまとめます
NSArray *callList = @[];
[callList addObject:@"b"];
[callList addObject:@"c"];
[callList addObject:@"d"];
// IMグループ内で開始されていない場合は、groupIdを空文字列とすることができます。
[[TRTCCalling shareInstance] groupCall:callList type:CallType_Video groupID:@""];

//自身のカメラを起動します
[[TRTCCalling shareInstance] openCamera:true view:renderView];
:::
</dx-codeblock>

[](id:offline)
### 手順7：オフライン応答の実装

>?ビジネスの位置付けがオンラインカスタマーサービスなどのオフライン応答機能を必要としないシーンである場合は、上記[手順1]（＃model.step1）-[手順6]（＃model.step6）の対応で問題ありません。 しかし、ビジネスの位置付けがソーシャルシーンである場合は、オフライン応答を実装することをお勧めします。

IM SDKはオフラインプッシュをサポートしていますが、使用可能な基準を満たすためには相応の設定を行う必要があります。

1. Appleプッシュ証明書を申請する場合の具体的な操作については、[Appleプッシュ証明書の申請](https://intl.cloud.tencent.com/document/product/1047/34346)をご参照ください。
2. バックエンドおよびクライアントがオフラインプッシュを設定する場合の具体的な操作については、[オフラインプッシュ（iOS）](https://intl.cloud.tencent.com/document/product/1047/34347)をご参照ください。
3. login関数の`param.busiId`を対応する証明書IDに修正します。

[](id:api)

## コンポーネントAPIリスト

TRTCCallingコンポーネントのAPIインターフェースリストは次のとおりです。

| インターフェース関数        | インターフェースの機能                                                 |
| --------------- | -------------------------------------------------------- |
| addDelegate     | TRTCCallingプロキシコールバックを設定すると、ユーザーはこのコールバックを介してステータス通知を受け取ることができます |
| login           | IMにログインします。すべての機能を使用するためには、まずログインする必要があります                |
| logout          | IMからログアウトします。ログアウト後はダイヤル操作ができません                        |
| call            | C2Cの通話に招待します。被招待者はonInvitedのコールバックを受け取ります         |
|groupCall       | IMグループの通話に招待します。被招待者はonInvitedのコールバックを受け取ります     |
| accept          | 被招待者として通話に応答します                                     |
| reject          | 被招待者として通話を拒否します                                     |
| hangup          | 通話を終了します                                                 |
| startRemoteView | リモートユーザーのカメラデータを指定のUIViewにレンダリングします    |
| stopRemoteView  | 任意のリモートユーザーのカメラデータ のレンダリングを停止します                         |
|openCamera      | カメラを起動し、指定のTXCloudVideoViewにレンダリングします            |
| closeCamera     | カメラを終了します                                               |
| switchCamera    | 前後カメラを切り替えます                                           |
| setMicMute      | micをミュート/非ミュートに設定します                                             |
| setHandsFree    | ハンズフリーを起動するかどうかを設定します                                             |
