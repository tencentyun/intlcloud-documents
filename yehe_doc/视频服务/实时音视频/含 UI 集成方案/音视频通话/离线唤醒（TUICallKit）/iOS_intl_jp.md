オフライン通知機能は、Appがバックエンドで実行中またはオフライン状態の場合でも、オーディオビデオ通話の着信を受信できる機能です。TUICallKitはAppleが提供するシステムレベルのプッシュチャネル（APNs）を使用してメッセージの通知を行います。

## ステップ1：オフラインプッシュの設定

1. **APNs証明書の申請**：具体的には[オフラインプッシュ(iOS)](https://www.tencentcloud.com/document/product/1047/39157#.E6.AD.A5.E9.AA.A41.EF.BC.9A.E7.94.B3.E8.AF.B7-apns-.E8.AF.81.E4.B9.A6)のステップ1をご参照ください。

2. **IMコンソール設定**：具体的には[オフラインプッシュ(iOS)](https://www.tencentcloud.com/document/product/1047/39157#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E4.B8.8A.E4.BC.A0.E8.AF.81.E4.B9.A6.E5.88.B0.E6.8E.A7.E5.88.B6.E5.8F.B0)のステップ2をご参照ください。

3. **Appへの毎回のログイン時に、AppleからdeviceTokenを取得します**。具体的には[オフラインプッシュ(iOS)](https://www.tencentcloud.com/document/product/1047/39157#.E6.AD.A5.E9.AA.A43.EF.BC.9Aapp-.E5.90.91.E8.8B.B9.E6.9E.9C.E5.90.8E.E5.8F.B0.E8.AF.B7.E6.B1.82-devicetoken)のステップ3をご参照ください。

4. **IM SDKにログイン後、deviceTokenをTencent Cloudにアップロードします**。具体的には[オフラインプッシュ(iOS)](https://www.tencentcloud.com/document/product/1047/39157#.E6.AD.A5.E9.AA.A44.EF.BC.9A.E7.99.BB.E5.BD.95-im-sdk-.E5.90.8E.E4.B8.8A.E4.BC.A0-devicetoken-.E5.88.B0.E8.85.BE.E8.AE.AF.E4.BA.91)のステップ4をご参照ください。

>? その後の手順はTUICallKitがすでに完了していますので、[オフラインプッシュ(iOS)](https://www.tencentcloud.com/document/product/1047/39157)のその他の手順を参照する必要はありません。

## ステップ2：プロジェクトの設定

アプリケーションプログラムに必要な権限を追加する必要があります。Xcodeプロジェクトでプッシュ通知機能を有効にしてください。

**Xcode**プロジェクトを開き、**Project** > **Target** > **Capabilities**ページで赤枠内の＋ボタンをクリックし、**Push Notifications**を選択して追加します。追加後の結果は図の黄色枠のようになります。

![](https://qcloudimg.tencent-cloud.cn/image/document/954340261de64a1aab536cf8744d6136.png)

上記の手順が完了し、プロジェクトを実行すると、`TUICallKit`のオフライン通知機能を体験できるようになります。

## よくあるご質問 

### 1、プッシュ通知を受信できず、バックエンドでbad devicetokenというエラーが表示されました。

AppleのdeviceTokenは現在のコンパイル環境に関連しています。IMSDKにログイン後にdeviceTokenをTencent Cloudにアップロードした際に使用した証明書IDがtokenと一致しなかった場合、エラーが表示されます。

Release環境を使用してコンパイルした場合、`- application:didRegisterForRemoteNotificationsWithDeviceToken:`のコールバックで返されるのはリリース環境のtokenです。この場合、businessIDには本番環境の証明書IDを設定する必要があります。

Debug環境を使用してコンパイルした場合、`- application:didRegisterForRemoteNotificationsWithDeviceToken:`のコールバックで返されるのは開発環境のtokenです。この場合、businessIDには開発環境の証明書IDを設定する必要があります。

```objectivec
V2TIMAPNSConfig *confg = [[V2TIMAPNSConfig alloc] init];
/* ユーザーは自身でAppleに開発者証明書を登録します。開発者アカウントに証明書(p12ファイル)をダウンロードして生成し、生成したp12ファイルをTencent証明書管理コンソールに渡すと、コンソールは証明書IDを自動生成し、証明書IDを以下のbusiIdパラメータに渡します。*/
//証明書IDをプッシュします
confg.businessID = sdkBusiId;
confg.token = self.deviceToken;
[[V2TIMManager sharedInstance] setAPNS:confg succ:^{

} fail:^(int code, NSString *msg) {

}];
```

### 2、iOS開発環境で、登録してもdeviceTokenが返されないことや、APNsのtokenリクエストに失敗したと表示されることがあります。

この問題の現象はAPNsサービスが不安定なために発生します。次の方法で解決を試みることができます。

1. スマートフォンにSIMカードを挿入し、4Gネットワークを使用してテストを行う。

2. アンインストールして再インストール、Appの再起動、シャットダウンして再起動を行ってからテストを行う。

3. 本番環境のパッケージを作成してテストを行う。

4. 他のiOSシステムのスマートフォンに代えてテストを行う。
