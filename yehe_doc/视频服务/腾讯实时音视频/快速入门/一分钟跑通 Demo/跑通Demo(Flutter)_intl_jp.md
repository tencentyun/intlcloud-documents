ここでは、主にTencent Cloud TRTC Demo(Flutter)を素早く実行する方法をご紹介します。

## 環境要件
- Flutter 1.12およびそれ以降のバージョン。
- Androidの開発：
  -  Android Studio 3.5およびそれ以降のバージョン。
  -  AppにはAndroid 4.1およびそれ以降のバージョンのデバイスが必要です。
- iOSの開発：
  - Xcode 11.0およびそれ以降のバージョン。
  - プロジェクトが有効な開発者による署名を設定済みであることを確認してください。

## 前提条件

[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)および [実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了していること。実名認証を行っていないユーザーは、中国大陸のTRTCのインスタンスを購入できません。

## 操作手順

[](id:step1)

### 手順1：アプリケーションの新規作成
1．Tencent Real-Time Communicationコンソールにログインし、【開発支援】>【[Demoのクイックスタート](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2. アプリケーション名（例：TestTRTC）を入力し、【作成】をクリックします。

[](id:step2)
### 手順2：SDKおよびDemoのソースコードをダウンロード
1. 実際の業務のニーズにもとづき、SDKおよびセットのDemoソースコードをダウンロードします。
2. ダウンロード完了後、【ダウンロードしました。次のステップ】をクリックします。


[](id:step3)
### 手順3：Demoプロジェクトファイルの設定
1. 設定変更画面に入り、ダウンロードしたソースコードパッケージに基づき、対応する開発環境を選択します。
2. `/lib/debug/GenerateTestUserSig.dart` ファイルを見つけて開きます。
3. `GenerateTestUserSig.java`ファイル内の関連パラメータを設定します。
<ul><li/>SDKAPPID：デフォルトはPLACEHOLDER、実際のSDKAppIDを設定してください。
	<li/>SECRETKEY：デフォルトはPLACEHOLDER、実際のキー情報を設定してください。</ul>
4. 貼り付け完了後、【貼り付けました。次のステップ】をクリックすれは作成が完了します。
5. コンパイル完了後、【コンソール概要に戻る】をクリックすればOKです。

>!
>-ここで言及した新規UserSigの作成法は、クライアントコードでSECRETKEYを設定し、この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになり、そのため**のこの手法はローカルDemo実行および機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出しダイナミックUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

### 手順4：コンパイル動作
1. `flutter pub get`を実行します。
2. コンパイルを実行し、デバッグを行います。
####  Android端末
1. `flutter run`を実行します。
2. Android Studio（3.5およびそれ以降のバージョン）を使用して、ソースプロジェクトを開きます。
3. 【実行】をクリックします。
#### iOS端末
1. XCode（11.0およびそれ以降のバージョン）を使用して、ソースディレクトリの `/iosプロジェクト` を開きます。
2. コンパイルを行い、Demoプロジェクトを実行します。



## よくあるご質問

- [2台のスマホで同時にDemoを実行すると、お互いの画面が見えないのはなぜですか。](https://intl.cloud.tencent.com/document/product/647/39242)
- [ファイアウォールにはどのような制限がありますか。](https://intl.cloud.tencent.com/document/product/647/39242)
- [iOSのパッケージングの実行時にCrashした場合はどうすればいいですか。](https://intl.cloud.tencent.com/document/product/647/39242)
- [iOSでビデオが表示できない場合（Androidでは正常）はどうすればいいですか。](https://intl.cloud.tencent.com/document/product/647/39242)
- [SDKのバージョンを更新した後、iOS CocoaPodsの実行にエラーが出た場合はどうすればいいですか。](https://intl.cloud.tencent.com/document/product/647/39242)
- [Android Manifest merge failedでコンパイルに失敗した場合はどうすればいいですか。](https://intl.cloud.tencent.com/document/product/647/39242)
- [署名がないため、実機でのデバック時にエラーが出た場合はどうすればいいですか。](https://intl.cloud.tencent.com/document/product/647/39242)
- [プラグインの中のswiftファイルを追加・削除した後、build（ビルド）時に対応するファイルが見つからないのはなぜですか。](https://intl.cloud.tencent.com/document/product/647/39242)
- [Run（実行）時にエラー：“Info.plit, error: No value at that key path or invalid key path: NSBonjourServices”が出た場合はどうすればいいですか。](https://intl.cloud.tencent.com/document/product/647/39242)
- [Pod install時にエラーが出た場合はどうすればいいですか。](https://intl.cloud.tencent.com/document/product/647/392420)
- [Run（実行）時にiOS版で依存エラーが出た場合はどうすればいいですか。](https://intl.cloud.tencent.com/document/product/647/392421)



