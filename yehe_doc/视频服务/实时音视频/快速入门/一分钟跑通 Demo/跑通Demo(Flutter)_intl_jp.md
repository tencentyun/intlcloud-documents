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

- [Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)および [実名認証](https://intl.cloud.tencent.com/document/product/378/3629)を完了していること。実名認証を行っていないユーザーは、中国大陸のTRTCのインスタンスを購入できません。

## 操作手順

[](id:step1)
### 手順1：アプリケーションの新規作成
1．Tencent Real-Time Communicationコンソールにログインし、【開発支援】>【[Demoのクイック実行](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。
2．【今すぐ開始】をクリックし、例えば、`TestTRTC`などアプリケーション名を入力して、【アプリケーションの作成】をクリックします。

[](id:step2)
### 手順2：SDKおよびDemoのソースコードをダウンロード
1. 【[GitHub](https://github.com/c1avie/trtc_demo)】をクリックして GitHubに移動し、関連するSDKおよび付属のDemoソースコードをダウンロードします。
2. ダウンロード完了後、Tencent Real-Time Communicationコンソールに戻り、【ダウンロードしました。次のステップ】をクリックすれば、SDKAppIDおよびキー情報をクエリできます。


[](id:step3)
### 手順3：Demoプロジェクトファイルの設定
1. [手順2](#step2)でダウンロードしたソースコードパッケージを解凍します。
2. `/example/lib/debug/GenerateTestUserSig.dart` ファイルを見つけて開きます。
3. `GenerateTestUserSig.dart`ファイル内の関連パラメータを設定します。
 - SDKAPPID：デフォルトはPLACEHOLDER、実際のSDKAppIDを設定してください。
 - SECRETKEY：デフォルトはPLACEHOLDER、実際のキー情報を設定してください。
 - Tencent Real-Time Communicationコンソールに戻り、【貼り付け完了。次のステップ】をクリックします。
 - 【ガイドを閉じてコンソールへ進む】をクリックします。


>!
> - 本書で言及した新規UserSigの作成法は、クライアントコードでSECRETKEYを設定し、この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになり、そのため**のこの手法はローカルDemo実行および機能デバッグにのみ適合します**。
>
> - UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。 UserSigが必要なときは、Appから業務サーバーにリクエストを発出しダイナミックUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

### 手順4：コンパイル動作
1. `flutter pub get`を実行します。
2. コンパイルを実行し、デバッグを行います。

#### Android
 - 1. `flutter run`を実行します。
 - 2. Android Studio（3.5およびそれ以降のバージョン）を使用して、ソースプロジェクトを開きます。
 - 3. 【実行】をクリックします。

#### iOS
 - 1. XCode（11.0およびそれ以降のバージョン）を使用して、ソースディレクトリの `/iosプロジェクト` を開きます。
 - 2. コンパイルを行い、Demoプロジェクトを実行します。





## よくあるご質問

- [2台のスマホで同時にDemoを実行する場合、お互いの画面が見えないのはなぜですか？](https://intl.cloud.tencent.com/document/product/647/39242#que1)
- [ファイアウォールにはどのような制限がありますか？](hhttps://intl.cloud.tencent.com/document/product/647/39242#que2)
- [iOSパッケージはCrashを実行しますか？](https://intl.cloud.tencent.com/document/product/647/39242#que3)
- [iOSでビデオを表示できません（Androidでは正常です）。なぜですか？](https://intl.cloud.tencent.com/document/product/647/39242#que4)
- [SDKバージョンを更新した後、iOS CocoaPodsはエラーを報告しますか？](https://intl.cloud.tencent.com/document/product/647/39242#que5)
- [Android Manifest merge failedとは、コンパイルに失敗したのですか？](https://intl.cloud.tencent.com/document/product/647/39242#que6)
- [署名がないことで、実機でのデバッグでエラーが報告されますか？](https://intl.cloud.tencent.com/document/product/647/39242#que7)
- [プラグインのswiftファイルを追加または削除した後、buildする際に対応するファイルが見つからなくなりますか？](https://intl.cloud.tencent.com/document/product/647/39242#que8)
- [実行エラー“Info.plit, error: No value at that key path or invalid key path: NSBonjourServices”とは？](https://intl.cloud.tencent.com/document/product/647/39242#que9)
- [Pod installエラーとは？](https://intl.cloud.tencent.com/document/product/647/39242#que10)
- [実行時にiOSのバージョンに依存するエラーが報告されますか？](https://intl.cloud.tencent.com/document/product/647/39242#que11)



