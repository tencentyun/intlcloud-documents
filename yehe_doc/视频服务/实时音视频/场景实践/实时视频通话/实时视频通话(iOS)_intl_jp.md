## デモンストレーション













ビデオ通話機能をすばやく実装する必要がある場合、当社が提供するDemoをもとにアダプターを修正するか、または当社が提供するTRTCCalling コンポーネントでUIのカスタマイズを実装することができます。

>! 当社は TRTCVideoCall コンポーネントを過去に提供していましたが、旧バージョンのコンポーネントは [コンポーネントリポジトリ](https://github.com/tencentyun/LiteAVClassic) に移動済みです。TRTCCalling コンポーネントはIM シグナリングのインターフェースを使用するため、旧コンポーネントとの互換性がなくなります。

<span id="ui"> </span>

## Demo の UI を再利用

<span id="ui.step1"></span>

### 手順1：アプリケーションの新規作成

1．Tencent Real-Time Communicationコンソールにログインし、【開発支援】>【[Demoのクイック実行](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2．【今すぐ開始】をクリックし、例えば、`TestVideoCall`などアプリケーション名を入力して、【アプリケーションの作成】をクリックします。

>! 本機能はTencent Cloud [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) と [IM](https://intl.cloud.tencent.com/document/product/1047) という2つの基本的な PaaS サービスを同時に使用し、TRTCをアクティブにした後、IM サービスを同期的にアクティブにすることができます。 IM は付加価値サービスであり、請求ルールの詳細については [Instant Messagingの価格説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。 

<span id="ui.step2"></span>

### 手順2：SDKおよびDemoのソースコードをダウンロード

１．マウスを該当するカードまで移動し、【[Github](https://github.com/tencentyun/TRTCSDK/tree/master/iOS)】をクリックしてGithub（または【[ZIP](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_iOS_latest.zip)】をクリック）にジャンプして、関連するSDK および付属のDemoソースコードをダウンロードします。
   ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. ダウンロード完了後、Tencent Real-Time Communicationコンソールに戻り、【ダウンロードしました。次のステップ】をクリックすれば、SDKAppIDおよびキー情報をクエリできます。

<span id="ui.step3"></span>

### 手順3：Demoプロジェクトファイルの設定

1．[手順2](#ui.step2) でダウンロードしたソースコードパッケージを解凍します。
2.  `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h` ファイルを探して開きます。
3.  `GenerateTestUserSig.h`ファイルの関連パラメータを設定します。
	- SDKAPPID：デフォルトは0、実際のSDKAppIDを設定してください。
	- SECRETKEY：デフォルトは空文字列。実際のキー情報を設定してください。
![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
4．Tencent Real-Time Communicationコンソールに戻り、【貼り付け完了。次のステップ】をクリックします。
5.【ガイドを閉じてコンソールへ進む】をクリックします。

>!
>-本書で言及した新規UserSigの作成法は、クライアントコードでSECRETKEYを設定し、この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになり、そのため**のこの手法はローカルDemo実行および機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166#Server)をご参照ください。

<span id="ui.step4"></span>

### 手順4：Demoの動作

Xcode（11.0以上のバージョン）を使用してソースコードプロセス `iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace`を開き、【実行】をクリックすれば本 Demoのデバッグを開始することができます。

<span id="ui.step5"></span>

### 手順5：Demo ソースコードの修正

ソースコードフォルダ `TRTCCallingDemo`に2つのサブフォルダui と modelが含まれ、その内、ui フォルダに含まれるのはすべてインターフェースコードです。

|             ドキュメントまたはフォルダ             | 機能の説明                                                 |
| ------------------------------------ | ------------------------------------------------------- |
|  TRTCCallingVideoViewController.swift  |ビデオ通話のメインインターフェースが表示され、このインターフェースで通話の応答と拒否が完了します。
|  TRTCCallingAudioViewController.swift  |音声通話のメインインターフェースが表示され、このインターフェースで通話の応答と拒否が完了します。 |
| TRTCCallingContactViewController.swift | 連絡先を検索するためのインターフェースを表示するために使用されます。                               |


<span id="model"> </span>

## UIカスタマイズの実装

[ソースコード] フォルダ `TRTCCallingDemo` 中には2つのサブフォルダ ui と modelが含まれ、その内、 model フォルダには当社が実装した再利用可能なオープンソースコンポーネント TRTCCallingが含まれています。 このコンポーネントが提供するインターフェース関数は `TRTCCalling.h` ファイルで確認できます。
![](https://main.qcloudimg.com/raw/9b4087b68541912ce9e7a48955cd48e8.png)

オープンソースコンポーネント TRTCCalling を使用して自身の UIを実装することができます。つまり model パーツを再利用するだけで、自身で UI パーツを実装できます。

<span id="model.step1"> </span>

### 手順1： SDKへの統合

通話コンポーネント TRTCCallingは、TRTC SDK と IM SDKに依存し、次の手順で2つの SDKをプロジェクトに統合することができます。

- **方法一：cocoapodsリポジトリを介する依存**
```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```
>?2つの SDK 製品の最新バージョン番号は、[TRTC](https://github.com/tencentyun/TRTCSDK) と [IM](https://github.com/tencentyun/TIMSDK) の Github トップページで取得することができます。
- **方法二：ローカルを介する依存**
開発環境でのcocoapods リポジトリへのアクセスが遅い場合は、ZIPパッケージを直接ダウンロードし、統合ドキュメントに従って手動でプロジェクトに統合することができます。
<table>
<tr>
<th>SDK</th>
<th>ダウンロードページ</th>
<th>統合ガイド</th>
</tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35093">統合ファイル</a></td>
</tr>
<tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">統合ファイル</a></td>
</tr>
</table>

<span id="model.step2"> </span>

### 手順2：権限の設定

info.plist ファイルに `Privacy - Camera Usage Description`， `Privacy - Microphone Usage Description`を追加し、カメラとマイクの権限を申請する必要があります。

<span id="model.step3"> </span>

### 手順3：TRTCCalling コンポーネントをインポート

次のディレクトリ内のすべてのファイルをプロジェクトにコピーします。
```
iOS/TRTCSceneDemo/TXLiteAVDemo/TRTCCallingDemo/model 
```

<span id="model.step4"> </span>

### 手順4：コンポーネントの初期化およびログイン

1. プッシュ関連情報を設定します。
```
[TRTCCalling shareInstance].imBusinessID = your business ID;
[TRTCCalling shareInstance].deviceToken =  deviceToken;
```
2.  `login(sdkAppID: UInt32, user: String, userSig: String, success: @escaping (() -> Void), failed: @escaping ((_ code: Int, _ message: String) -> Void))` をコールし、コンポーネントのログインを完了します。なおいくつかの重要パラメータの入力については下表をご参照ください。
<table>
<tr><th>パラメータ名</th><th>作用</th></tr>
<tr>
<td>sdkAppID</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">Tencent Real-Time Communicationコンソール</a> で SDKAppIDを表示できます。</td>
</tr><tr>
<td>user</td>
<td>現在のユーザーID、文字列タイプでは、英語のアルファベット（a-z と A-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。</td>
</tr><tr>
<td>userSig</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSigの計算方法</a>。</td>
</tr></table>
<pre>
// ログイン
[[TRTCCalling shareInstance] login:SDKAPPID user:userID userSig:userSig success:^{
        NSLog(@"Video call login success.");
} failed:^(int code, NSString *error) {
        NSLog(@"Video call login failed.");
}];
</pre>

<span id="model.step5"> </span>

### 手順5： 1v1 通话の実現

1. 発信者： `TRTCCalling` の `call(userId, callType)`をコールし、`userId` パラメータをユーザーIDとし、 `callType`パラメータを通話タイプとして、パラメータ`CallType_Video`を渡すと、ビデオ通話のリクエストを開始することができます。
2. 受信者：受信者がログイン状態の場合は、`onInvited()`という名称のコールバックを受け取り、コールバックにおける `callType` のパラメータは発信者が入力した通話タイプであり、このパラメータを介して対応するインターフェースを起動します。受信者がログインしていない状態でも通話リクエストを受け取りたい場合は、[オフライン応答](#model.offline)をご参照ください。
3. 受信者：電話に対応したい場合、受信者は `accept()` 関数をコールすることができ、ビデオ通話である場合は、同時に `openCamera()` 関数をコールして、自身のローカルカメラを起動します。受信者は`reject()` をコールし、この通話を拒否することもできます。
4. 双方のオーディオ・ビデオチャネルが確立した後、通話する双方はさらに `onUserVideoAvailable()`という名称のコールバックを受け取り、相手方のビデオ画面を取得済みであることが表示されます。この時、双方のユーザーは`startRemoteView()`をコールし、リモートのビデオ画面を表示することができます。リモートの音声はデフォルトで自動再生に設定されています。

```Objective-C
// 1.監視のコールバック
[[TRTCCalling shareInstance] addDelegate:delegate];

// 応答/拒否
// B もIMシステムにログインしている場合は、 onInvited(A, null, false) のコールバックを受け取ることができます。
//  TRTCCallingのacceptメソッドをコールして受信することができます / TRTCCallingのreject メソッドをコールして拒否することができます
-(void)onInvited:(NSString *)sponsor
         userIds:(NSArray<NSString *> *)userIds
     isFromGroup:(BOOL)isFromGroup
        callType:(CallType)callType
    [[TRTCCalling shareInstance] accept];
}

// 2.相手方の画面を観覧します
//  Aがカメラを起動していることから、Bは通話を受信した後 onUserVideoAvailable(A, true)のコールバックを受け取ることができます
- (void)onUserVideoAvailable:(NSString *)uid available:(BOOL)available {
	if (available) {
		UIView* renderView =[[UIView alloc] init];
		[[TRTCCalling shareInstance] startRemoteView:uid view:renderView]; // 相手方の画面を見ることができます
	}else{
		[[TRTCCalling shareInstance] stopRemoteView:uid]; // 画面のレンダリングを停止します
	}
}

// 3.コンポーネントの他の機能の関数をコールし、通話を開始したり終了したりします
// 注意：ログインしなければ正常にコールできません
// ビデオ通話を開始します
[[TRTCCalling shareInstance] call:@"ターゲットユーザー" type:CallType_Video];
// 通話を終了します
[[TRTCCalling shareInstance] hangup];
// 拒否します
[[TRTCCalling shareInstance] reject];

```


<span id="model.step6"> </span>

### 手順6：多人数のビデオ通話を実現

1. 発信者：多人数のビデオ通話では、`TRTCCalling` の `groupCall()` 関数をコールし 、ユーザーリスト（userIdList）、グループIM  ID（groupId）、通話タイプ（callType） を入力する必要があります。なお userIdList は入力必須パラメータ、groupId はオプションパラメータ、`callType`はビデオタイプ`CallType_Video`とします。
2. 受信者： `onInvited()`という名称のコールバックを介してこの呼び出しリクエストを受け取ることができます。なおパラメータリストは発信者が入力したパラメータリストであり、`callType` パラメータは通話タイプであって、このパラメータを介して対応するインターフェースを起動することができます。
3. 受信者：コールバックを受け取った後、`accept()` メソッドをコールし この通話に応答することができます。`reject()` メソッドをコールして通話の拒否を選択することもできます。
4. 一定時間（デフォルトは30s）を超えて応答しなかった場合、受信者は `onCallingTimeOut()` のコールバックを受け取り、発信者は `onNoResp()` というコールバックを受け取ります。通話発信者が複数の着信に応答しない場合は `hangup()`のイベント通知を受け取り 、各受信者は `onCallingCancel()`という コールバックを受け取ります。
5. 現在の多人数の通話から退出したい場合は、`hangup()` メソッドをコールします。
6. 通話中にユーザーが途中参加し、または退出する場合、他のユーザーは `onUserEnter()` または  `onUserLeave()` というコールバックを受け取ります。

>?インターフェース `groupCall:type:groupID:`における `groupID` パラメータは IM SDKにおけるグループ IDです。このパラメータを設定すると、通話リクエストメッセージがグループメッセージシステムを介して発信され、このメッセージブロードキャスト方式は簡単で信頼性の高い方法です。設定しない場合は、`TRTCalling` コンポーネントが単発メッセージで1人1人に通知を行います。

```Objective-C
// 前記省略...
// ダイヤルするユーザーリストをまとめます
NSArray *callList = @[];
[callList addObject:@"b"];
[callList addObject:@"c"];
[callList addObject:@"d"];
// あるIM グループ内で開始されていない場合は、groupIdを空文字列とすることができます。
[[TRTCCalling shareInstance] groupCall:callList type:CallType_Video groupID:@""];

//自身のカメラを起動します
[[TRTCCalling shareInstance] openCamera:true view:renderView];
```

<span id="offline"> </span>

### 手順7：オフライン応答の実装

>?ビジネスの位置付けがオンラインカスタマーサービスなどのオフライン応答機能を必要としないシーンである場合は、上記[手順1]（＃model.step1）-[手順6]（＃model.step6）の対応で問題ありません。 しかし、ビジネスの位置付けがソーシャルシーンである場合は、オフライン応答を実装することをお勧めします。

IM SDKはオフラインプッシュをサポートしていますが、使用可能な基準を満たすためには相応の設定を行う必要があります。

1. Apple プッシュ証明書を申請する場合の具体的な操作については[Apple プッシュ証明書申請](https://intl.cloud.tencent.com/document/product/1047/34346)をご参照ください。
2. バックエンドおよびクライアントがオフラインプッシュを設定する場合の具体的な操作については、 [オフラインプッシュ（iOS）](https://intl.cloud.tencent.com/document/product/1047/34347)をご参照ください。
3. login 関数の `param.busiId` を対応する証明書IDに修正します。

<span id="api"> </span>

## コンポーネント API リスト

TRTCCalling コンポーネントの API インターフェースリストは次のとおりです。

| インターフェース関数        | インターフェースの機能                                                  |
| --------------- | -------------------------------------------------------- |
| addDelegate     | TRTCCallingプロキシコールバックを設定すると、ユーザーはこのコールバックを介してステータス通知を受け取ることができます |
| login           | IMにログインします。すべての機能を使用するためには、まずログインする必要があります                |
| logout          | IMからログアウトします。ログアウト後はダイヤル操作ができません                         |
| call            | C2C の通話に招待します。被招待者は onInvited のコールバックを受け取ります         |
|groupCall       | IM グループの通話に招待します。被招待者は onInvited のコールバックを受け取ります     |
| accept          | 被招待者として通話に応答します                                      |
| reject          | 被招待者として通話を拒否します                                      |
| hangup          | 通話を終了します                                                  |
| startRemoteView | リモートユーザーのカメラデータを指定の UIView にレンダリングします    |
| stopRemoteView  | 任意のリモートユーザーのカメラデータ のレンダリングを停止します                         |
|openCamera      | カメラを起動し、指定の TXCloudVideoView にレンダリングします            |
| closeCamera     | カメラを終了します                                               |
| switchCamera    | 前後カメラを切り替えます                                           |
| setMicMute      | micをミュート/非ミュートに設定します                                             |
| setHandsFree    | ハンズフリーを起動するかどうかを設定します                                             |
