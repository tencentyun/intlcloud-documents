ビデオ通話機能をすばやく実装する必要がある場合、当社が提供するDemoをもとに直接適応に変更を加えることも、当社が提供するTRTCCallingコンポーネントでカスタマイズしたUIを実装することもできます。

## DemoのUIの再利用

### 手順1：アプリケーションの新規作成

1．TRTCコンソールにログインし、【開発支援】>【[Demoクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2．`TestVideoCall`などアプリケーション名を入力して、【作成】をクリックします。

>!本機能はTencent Cloudの[TRTC](https://intl.cloud.tencent.com/document/product/647/35078)と[IM](https://intl.cloud.tencent.com/document/product/1047)という2つの基本的なPaaSサービスを同時に使用し、TRTCをアクティブにした後、IMサービスを同期的にアクティブにすることができます。IMは付加価値サービスであり、課金ルールの詳細については 、[Instant Messagingの価格説明](https://intl.cloud.tencent.com/document/product/1047/34350)をご参照ください。


[](id:ui.step2)
### 手順2：SDKおよびDemoソースコードをダウンロード
1. 実際のビジネスニーズに応じて、SDKと付属の[Demoソースコード](https://github.com/tencentyun/TRTCFlutterScenesDemo)をダウンロードします。
2. ダウンロード完了後、【ダウンロードしました。次のステップ】をクリックします。
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:ui.step3)
### 手順3：Demoプロジェクトファイルの設定
1. 設定変更ページに進み、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `/example/lib/debug/GenerateTestUserSig.dart`ファイルを見つけて開きます。
3.`GenerateTestUserSig.dart`ファイル内の関連パラメータを設定します。
<ul><li/>SDKAPPID：デフォルトはPLACEHOLDER。実際のSDKAppIDを設定してください。
	<li/>SECRETKEY：デフォルトはPLACEHOLDER。実際のキー情報を設定してください。</ul>
	<img src="https://main.qcloudimg.com/raw/fba60aa9a44a94455fe31b809433cfa4.png"/>
4. 貼り付け完了後、【貼り付けました。次のステップ】をクリックすれば、作成が完了します。
5. コンパイル完了後、【コンソール概要に戻る】をクリックすればOKです。
>!
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**のこの手法は、ローカルのDemoクイックスタートおよび機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:ui.step4)

### 手順4：Demoの実行

>! Android端末は実際のマシンで実行する必要があり、エミュレーターのデバッグはサポートされていません。

1. `flutter pub get`を実行します。
2. コンパイルを実行し、デバッグを行います。
<dx-tabs>
:::  Android\s端末
1. `flutter run`を実行します。
2. Android Studio（3.5およびそれ以降のバージョン）を使用して、ソースプロジェクトを開き、【実行】をクリックすれば完了です。
:::
::: iOS\s端末
1. XCode（11.0およびそれ以降のバージョン）を使用して、ソースコードディレクトリの `/iosプロジェクト` を開きます。
2. コンパイルを行い、Demoプロジェクトを実行します。
:::
</dx-tabs>

[](id:ui.step5)
### 手順5：Demoソースコードの修正
[ソースコード](https://github.com/tencentyun/TRTCFlutterScenesDemo)フォルダ`TRTCCallingDemo` には2つのサブフォルダuiとmodelが含まれ、そのうちuiフォルダにはインターフェースコードが含まれています。

| ファイルまたはフォルダ            | 機能の説明                                                     |
| ----------------------- | ------------------------------------------------------------ |
| TRTCCallingVideo.dart   | オーディオビデオ通話のメインインターフェースが表示され、このインターフェースで通話の応答と拒否が完了します。 |
| TRTCCallingContact.dart | 連絡先を選択するためのインターフェースを表示するために使用され、このインターフェースを介して登録済みユーザーを検索し、通話を開始できます |

[](id:model)
## カスタマイズUIの実装
[ソースコード](https://github.com/tencentyun/TRTCFlutterScenesDemo)フォルダ`TRTCCallingDemo`には2つのサブフォルダuiとmodelが含まれ、そのうちmodelフォルダには当社が実装した再利用可能なオープンソースコンポーネントTRTCCallingが含まれています。このコンポーネントが提供するインターフェース関数は`TRTCCalling.dart`ファイルで確認できます。
![](https://main.qcloudimg.com/raw/78cc06cd53538243bc52abc381350c55.jpg)

オープンソースコンポーネントTRTCCallingを使用すれば、自分のUIを実装することができます。すなわちmodelパーツを再利用するだけで、自分でUIパーツを実装できます。

[](id:model.step1)
### 手順1：SDKへの統合
オーディオビデオ通話コンポーネントTRTCCallingは、[TRTC SDK](https://pub.dev/packages/tencent_trtc_cloud)と[IM SDK](https://pub.dev/packages/tencent_im_sdk_plugin)に依存しています。`pubspec.yaml`を設定することで、更新を自動的にダウンロードできます。

プロジェクトの`pubspec.yaml`に次の依存関係を記述します。
```
dependencies:
  tencent_trtc_cloud: 最新バージョン番号
  tencent_im_sdk_plugin: 最新バージョン番号
```

[](id:model.step2)
### 手順2：権限の設定および難読化ルール

<dx-tabs>
::: iOS\s端末
`Info.plist`にカメラとマイクの権限申請を追加する必要があります。
```
<key>NSMicrophoneUsageDescription</key>
<string>通常の音声通話が行えるようにマイクの権限を承認します</string>
```
:::
::: Android\s端末
1. `/android/app/src/main/AndroidManifest.xml`ファイルを開きます。
2. `xmlns:tools="http://schemas.android.com/tools"` をmanifestの中に追加します。
3. `tools:replace="android:label"をapplicationの中に追加します。
>? この手順を実行しないと、[Android Manifest merge failedコンパイルの失敗](https://intl.cloud.tencent.com/document/product/647/39242)という問題が発生します。

![図](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)
:::
</dx-tabs>

[](id:model.step3)
### 手順3：TRTCCalling コンポーネントをインポート
次のディレクトリ内のすべてのファイルをプロジェクトにコピーします。
```
/lib/TRTCCallingDemo/model
```

[](id:model.step4)
### 手順4：コンポーネントの初期化およびログイン
1. `TRTCCalling.sharedInstance()`を呼び出して、コンポーネントインスタンスを取得します。
2. `login(SDKAppID, userId, userSig, callback)`を呼び出し、コンポーネントのログインを完了します。このうちいくつかの重要パラメータの入力については、下表をご参照ください。
 <table>
<tr><th>パラメータ名</th><th>作用</th></tr>
<tr>
<td>SDKAppID</td>
<td><a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a> で SDKAppIDを表示できます。</td>
</tr><tr>
<td>userId</td>
<td>現在のユーザーID。文字列タイプでは、英語のアルファベット（a-zとA-Z）、数字（0-9）、ハイフン（-）とアンダーライン（_）のみ使用できます。</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloudによって設計されたセキュリティ保護署名。計算方法については<a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSigの計算方法</a>をご参照ください。</td>
</tr></table>
<dx-codeblock>
::: java 
// 初期化
sCall = await TRTCCalling.sharedInstance();
sCall.login(1400000123, "userA", "xxxx");
:::
</dx-codeblock>

[](id:model.step5)
### 手順5：1v1ビデオ通話を実現
1. 発信者：`TRTCCalling`の`call()`メソッドを呼び出して通話リクエストを開始し、ユーザーID（userid）と通話タイプ（type）を渡して、通話タイプパラメータを`TRTCCalling.typeVideoCall`に渡します。
2. 受信者：受信者がログイン状態の場合は、`onInvited()`という名称のイベント通知を受け取ります。コールバックにおける`callType`のパラメータは発信者が入力した通話タイプであり、このパラメータを介して対応するインターフェースを起動することができます。
3. 受信者：電話に対応したい場合、受信者は`accept()`関数をコールすると同時に`openCamera()`関数を呼び出して、自身のローカルCCDカメラを起動します。受信者は`reject()`を呼び出し、この通話を拒否することもできます。
4. 双方のオーディオビデオチャネルが確立した後、通話する双方は`onUserVideoAvailable()`という名称のイベント通知を受け取ります。これは、相手方のビデオ画面を取得済みであることを示しています。このとき、双方のユーザーは`startRemoteView()`を呼び出し、リモートのビデオ画面を表示することができます。リモートの音声はデフォルトで自動再生に設定されています。


[](id:api)
## コンポーネントAPIリスト
TRTCCallingコンポーネントのAPIインターフェースリストは次のとおりです。

| インターフェース関数           | インターフェースの機能                                                  |
| ------------------ | --------------------------------------------------------- |
| registerListener   | TRTCCalling監視装置を追加します。ユーザーはこの監視装置を介してステータス通知を取得することができます |
| unRegisterListener | 監視装置を削除します                                               |
| destroy            | インスタンスを破棄します                                                  |
| login              | IMにログインします。すべての機能を使用するためには、まずログインする必要があります                 |
| logout             | IMからログアウトします。ログアウト後はダイヤル操作ができません                         |
| call               | C2Cの通話に招待します。被招待者はonInvitedのイベント通知を受け取ります         |
| accept             | 被招待者として通話に応答します                                      |
| reject             | 被招待者として通話を拒否します                                      |
| hangup             | 通話を終了します                                                  |
| startRemoteView    | リモートユーザーのカメラデータを指定のTXCloudVideoViewにレンダリングします    |
| stopRemoteView     | 任意のリモートユーザーのカメラデータのレンダリングを停止します                          |
|openCamera         | カメラを起動し、指定のTXCloudVideoViewにレンダリングします            |
| closeCamera        | カメラを終了します                                                |
| switchCamera       | フロント/リアカメラを切り替えます                                            |
| setMicMute         | micをミュート/非ミュートに設定します                                              |
| setHandsFree       | ハンズフリーを起動するかどうかを設定します                                              |

