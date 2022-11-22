ここでは、最短の時間でTUICallKitコンポーネントの統合を完了する方法についてご説明します。このドキュメントに沿って操作することで、1時間以内に次の重要手順を完了し、最終的にUIインターフェースを完備したビデオ通話機能を手にすることができます。

## 環境の準備

iOS 9.0 (API level 16)およびそれ以上。

[](id:step1)
##  ステップ1：サービスのアクティブ化

TUICallKitはTencent Cloudの[IM](https://www.tencentcloud.com/document/product/1047)と、[TRTC](https://www.tencentcloud.com/document/product/647)という2つの有料PaaSサービスをベースに構築したオーディオビデオ通信コンポーネントです。以下の手順で関連のサービスをアクティブ化し、60日間の無料トライアルサービスを体験することができます。

1. [IMコンソール](https://console.tencentcloud.com/im)にログインし、**新しいアプリケーションの作成**をクリックし、ポップアップしたダイアログボックスにアプリケーション名を入力して**OK**をクリックします。
![img](https://qcloudimg.tencent-cloud.cn/raw/c9a076ece348019d689c6c562b6a3c78.png)

2. 作成したアプリケーションをクリックし、基本設定ページに進み、ページ右下隅のTRTCサービスのアクティブ化機能エリアで無料体験をクリックすると、TUICallKitの7日間無料トライアルサービスをアクティブ化することができます。正式アプリケーションのリリースが必要な場合は、[お問い合わせ](https://intl.cloud.tencent.com/contact-us)ください。
![img](https://qcloudimg.tencent-cloud.cn/raw/4ee28e98dd28c9ae91078832f0105092.png)

>! IMのオーディオビデオ通話機能は業務ニーズに応じて差別化した有料バージョンをご提供しています。[お問い合わせ](https://intl.cloud.tencent.com/contact-us)いただくことで、含まれる機能をご確認の上、ご自身に合ったバージョンを選択してご購入いただけます。

3. 同じページで**SDKAppID**と**キー(SecretKey)**を見つけて記録します。この2つはその後の[ステップ4：TUIコンポーネントへのログイン](#step4)で使用します。
![img](https://qcloudimg.tencent-cloud.cn/raw/c3158845c9c0227a2da9eea8c0a975bb.png)


>? お知らせ：**無料体験**をクリックすると、それまでに[TRTC](https://www.tencentcloud.com/document/product/647/35078)サービスを使用したことがある一部のユーザーには、次のような内容が表示されることがあります。
```java
[-100013]:TRTC service is  suspended. Please check if the package balance is 0 or the Tencent Cloud accountis in arrears
```
新しいIMオーディオビデオ通話機能は、Tencent Cloudの[TRTC](https://www.tencentcloud.com/document/product/647/35078)と[IM](https://www.tencentcloud.com/document/product/1047)という2つの基本PaaSサービスを統合したもののため、[TRTC](https://www.tencentcloud.com/document/product/647/35078)の無料利用枠（10000分）が期限切れまたは使用済みの場合、このサービスをアクティブ化しようとすると失敗します。その場合は、[TRTCコンソール](https://console.tencentcloud.com/trtc/app)をクリックし、SDKAppIDに対応するアプリケーション管理ページを見つけ、図のように後払い機能をアクティブ化してから**アプリケーションを有効にする**ことで、オーディオビデオ通話機能を正常に体験することができるようになります。


[](id:step2)

## ステップ2：コンポーネントのインポート

CocoaPodsを使用してコンポーネントをインポートします。具体的な手順は次のとおりです。
1. `Podfile`ファイルに次の依存を追加します。

```shell
pod 'TUICallKit'
```

2. 次のコマンドを実行し、コンポーネントをインストールします。
```shell
pod install
```
TUICallKitの最新バージョンをインストールできない場合は、次のコマンドを実行して、ローカルのCocoaPodsリポジトリリストを更新します。
```shell
pod repo update
```

[](id:step3)
## ステップ3：プロジェクト設定の完了
オーディオビデオ機能を使用するには、マイクおよびカメラの使用権限を付与する必要があります。AppのInfo.plistで以下の2項を追加します。これらはシステムが権限付与ダイアログボックスをポップアップする際に表示される、マイクとカメラのメッセージにそれぞれ対応します。

```objectivec
<key>NSCameraUsageDescription</key>
<string>CallingAppはカメラへのアクセス権限が必要です。有効にした後にレコーディングしたビデオでなければ画面は出ません</string>
<key>NSMicrophoneUsageDescription</key>
<string>CallingAppはマイクへのアクセス権限が必要です。有効にした後にレコーディングしたビデオでなければ音声は出ません</string>
```
![img](https://qcloudimg.tencent-cloud.cn/raw/5579558165eae672db5259a8989fe5d4.png)

[](id:step4)
## ステップ4：TUIコンポーネントへのログイン
プロジェクトに次のコードを追加します。この役割は、TUICore内の関連インターフェースを呼び出して、TUIコンポーネントへのログインを完了することです。ログインに成功しなければTUICallKitの各機能を正常に使用できないため、この手順に異常がないことが重要です。関連のパラメータが正しく設定されているかどうかを注意深く確認してください。

<dx-codeblock>
:::  Objective-C Objectivec
// コンポーネントのログイン
[TUILogin login:1400000001           // ステップ1で取得したSDKAppIDに置き換えてください
         userID:@"denny"             // ご自身のUserIDに置き換えてください
         userSig:@"xxxxxxxxxxx"      // コンソールでUserSigを計算し、この位置に入力することができます
            succ:^{
    NSLog(@"login success");
} fail:^(int code, NSString *msg) {
    NSLog(@"login failed, code: %d, error: %@", code, msg);
}
:::
::: Swift
// コンポーネントのログイン
TUILogin.login(1400000001,                   // ステップ1で取得したSDKAppIDに置き換えてください
            userID: "denny",                 // ご自身のUserIDに置き換えてください
            userSig: "xxxxxxxxxxx") {        // コンソールでUserSigを計算し、この位置に入力することができます
    print("login success")
} fail: { (code, message) in
    print("login failed, code: \(code), error: \(message ?? "nil")")
}
:::
</dx-codeblock>

**パラメータの説明**：
ここではlogin関数内で使用するいくつかの重要パラメータについて詳しくご説明します。
- sdkAppId：ステップ1の最後の段階で取得済みです。ここでは説明を省略します。
- userId：現在のユーザーIDです。文字列タイプでは、アルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（\_）のみ使用できます。
- userSig：ステップ3で取得したSecretKeyを使用してSDKAppID、UserIDなどの情報を暗号化し、UserSigを取得します。これは認証用の証明書であり、現在のユーザーがTRTCサービスを使用できるかどうかをTencent Cloudが識別するために用いられます。コンソールの[UserSigの生成](https://console.tencentcloud.com/trtc/app)ボタンで、一時的に使用可能なUserSigを生成することができます。
その他の情報については、[UserSigの計算、使用方法](https://www.tencentcloud.com/document/product/647/35166)をご参照ください。

> ! 
>- **この手順は、現在開発者から最も多くのフィードバックが寄せられる手順でもあります。よくみられる問題には次のようなものがあります。** 
    - sdkAppIdの設定に誤りがある。国内サイトのSDKAppIDは一般的に140で始まる10桁の整数です。
    - userSigを誤って暗号化鍵（Secretkey）に設定している。userSigはSecretKeyを使用して、sdkAppId、userIdおよび有効期限などの情報を暗号化するためのものであり、Secretkeyは直接userSigに設定するものではありません。
    - userIdが「1」、「123」、「111」などの簡単な文字列で設定されている。**TRTCは同一のUserIDによる複数端末へのログインをサポートしていない**ため、複数人によるコラボレーション開発の場合、「1」、「123」、「111」のようなuserIdは同僚に占有されていることが多く、ログイン失敗につながりやすいです。このため、デバッグの際に、識別度の高いuserIdを設定することをお勧めします。
>- GithubのサンプルコードでgenTestUserSig関数を使用してローカルでuserSigを計算すると、現在のアクセスフローをさらに速くスタートさせることができますが、この方法ではSecretKeyがAppのコード内で開示されてしまい、その後のアップグレードおよびSecretKeyの保護にとって不利益になります。そのため、userSigの計算ロジックはサーバーに置いて実行し、またAppがTUICallKitコンポーネントを使用するたびに、リアルタイムに計算したuserSigをサーバーにリクエストするようにすることを強く推奨します。

[](id:step5)
## ステップ5：通話する
### 1対1ビデオ通話
TUICallKitのcall関数を呼び出し、 通話タイプと着呼者のuserIdを指定すると、音声またはビデオ通話を開始することができます。
<dx-codeblock>
:::  Objective-C Objectivec
// 1対1ビデオ通話を開始します(userIdはmikeとします)
[[TUICallKit createInstance] call:@"mike" callMediaType:TUICallMediaTypeVideo];
:::
::: Swift
// 1対1ビデオ通話を開始します(userIdはmikeとします)
TUICallKit.createInstance().call(userId: "mike", callMediaType: .video)
:::
</dx-codeblock>

| パラメータ       |  タイプ  | 意味 |
|-----|-----|-----|
| userId | String | ターゲットユーザーのUserID：`"mike"` |
| callMediaType |TUICallMediaType | 通話のメディアタイプ。例：`TUICallMediaTypeVideo` |

### グループ内ビデオ通話
TUICallKitのgroupCall関数を呼び出し、 通話タイプと着呼者のUserIDリストを指定すると、グループ内で音声またはビデオ通話を開始することができます。
<dx-codeblock>
:::  Objective-C Objectivec
[[TUICallKit createInstance] groupCall:@"12345678" userIdList:@[@"denny", @"mike", @"tommy"] callMediaType:TUICallMediaTypeVideo];
:::
::: Swift
TUICallKit.createInstance().groupCall(groupId: "12345678", userIdList: ["denny", "mike", "tommy"], callMediaType: .video)
:::
</dx-codeblock>

| パラメータ       |  タイプ  | 意味 |
|-----|-----|-----|
| groupId | String | グループID。例：`@"12345678"` |
| userIdList | Array | ターゲットユーザーのuserIdリスト。例：`@[@"denny", @"mike", @"tommy"]` |
| callMediaType | TUICallMediaType | 通話のメディアタイプ。例：`TUICallMediaTypeVideo` |

>? 
>- グループの作成の詳細については[IMグループ管理](https://www.tencentcloud.com/document/product/1047/48466)をご参照ください。もしくは[IM TUIKit](https://intl.cloud.tencent.com/document/product/1047/34286)を直接使用し、チャット、通話などのシナリオをワンストップで統合することもできます。
>- TUICallKitでは現在、グループ以外の多人数ビデオ通話はサポートしていません。もし必要な場合は、colleenyu@tencent.comまでぜひフィードバックをお寄せください。

[](id:step6)
## ステップ6：通話に応答する
**ステップ4**が完了し、通話リクエストを受信すると、TUICallKitコンポーネントは対応する応答画面を自動的に起動します。

[](id:step7)
## ステップ7：その他の特徴
### 1、ニックネーム&プロフィール画像の設定
カスタムニックネームまたはプロフィール画像を設定したい場合は、次のインターフェースを使用して更新できます。
<dx-codeblock>
:::  Objective-C Objectivec
[[TUICallKit createInstance] setSelfInfo:@"ニックネーム" avatar:@"プロフィール画像URL" succ:^{

} fail:^(int code, NSString *errMsg) {

}];
:::
::: Swift
TUICallKit.createInstance().setSelfInfo(nickname: "ニックネーム", avatar: "プロフィール画像URL", succ: {

}) { code, desc in

}
:::
</dx-codeblock>

> ! ユーザーのプライバシー上の制限により、フレンド以外との通話では、呼ばれるニックネームとプロフィール画像の更新が遅れる可能性があります。一度通話が成功するとスムーズに更新されるようになります。

### 2、オフライン通知
上記の手順が完了すると、オーディオビデオ通話の発信と接続が実現できますが、業務上「Appのプロセスが強制終了された後」または「APPがバックエンドに戻った後」もオーディオビデオ通話リクエストを正常に受信できる必要がある場合は、オフライン通知機能を追加する必要があります。詳細については[**オフライン通知（iOS）**](https://www.tencentcloud.com/document/product/647/51000)をご参照ください。

### 3、フローティングウィンドウ機能
業務上、フローティングウィンドウ機能を有効にする必要がある場合は、TUICallKitコンポーネントの初期化の際に次のインターフェースを呼び出してこの機能を有効化することができます。
 <dx-codeblock>
:::  Objective-C Objectivec
[[TUICallKit createInstance] enableFloatWindow:YES];
:::
::: Swift
TUICallKit.createInstance().enableFloatWindow(true)
:::
</dx-codeblock>

### 4. 通話ステータスの監視
業務上、通話の開始、終了、通話中のネットワーク品質などの**通話ステータスの監視**が必要な場合は、次のイベントを監視することができます。
<dx-codeblock>
:::  Objective-C Objectivec
[[TUICallEngine createInstance] addObserver:self];

- (void)onCallBegin:(TUIRoomId *)roomId callMediaType:(TUICallMediaType)callMediaType callRole:(TUICallRole)callRole {
  

}
- (void)onCallEnd:(TUIRoomId *)roomId callMediaType:(TUICallMediaType)callMediaType callRole:(TUICallRole)callRole totalTime:(float)totalTime {
  

}
- (void)onUserNetworkQualityChanged:(NSArray<TUINetworkQualityInfo *> *)networkQualityList {
  

}
:::
::: Swift
TUICallEngine.createInstance().add(self)

public func onCallBegin(roomId: TUIRoomId, callMediaType: TUICallMediaType, callRole: TUICallRole) {
        
}
public func onCallEnd(roomId: TUIRoomId, callMediaType: TUICallMediaType, callRole: TUICallRole, totalTime: Float) {
        
}
public func onUserNetworkQualityChanged(networkQualityList: [TUINetworkQualityInfo]) {
        
}
:::
</dx-codeblock>

### 5、カスタム着信音
着信音をカスタマイズしたい場合は、次のインターフェースによって設定できます。
<dx-codeblock>
:::  Objective-C Objectivec
[[TUICallKit createInstance] setCallingBell:filePath];
:::
::: Swift
TUICallKit.createInstance().setCallingBell(filePath: filePath)
:::
</dx-codeblock>


## よくあるご質問
### 1、「The package you purchased does not support this ability」というエラーが表示されました。

上記のエラーが表示された場合は、現在のアプリケーションのオーディオビデオ通話機能パッケージが期限切れまたはアクティブ化されていないことを表します。[ステップ1](#step1)を参照してオーディオビデオ通話機能を取得またはアクティブ化し、引き続きTUICallKitコンポーネントをご利用ください。

### 2、パッケージを購入するにはどうすればよいですか。

購入リンク[オーディオビデオ通話SDK価格一覧](https://www.tencentcloud.com/document/product/647/50553)をご参照ください。その他にご質問がありましたらページ右側をクリックし、パッケージのご購入前にお問い合わせください。もしくはQQグループ：**592465424**に参加し、問い合わせとフィードバックを行うことができます。

>? その他のヘルプ情報についての詳細は、[iOSについてのよくあるご質問](https://www.tencentcloud.com/document/product/647/51023)をご参照ください。

## ご意見とフィードバック

ご利用中にご提案やご意見などがございましたら、colleenyu@tencent.comまでフィードバックをお願いいたします。
