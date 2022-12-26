ここでは、主にTRTC Demo(Flutter)を素早く実行する方法をご紹介します。

>! 現在Windows/MacOs端末は画面共有およびデバイス選択の機能をサポートしていません。

## 環境要件
- Flutter 2.0およびそれ以降のバージョン。
- **Android端末向け開発：**
  -  Android Studio 3.5およびそれ以降のバージョン。
  -  AppにはAndroid 4.1およびそれ以降のバージョンのデバイスが必要です。
**iOS & macOS端末向け開発：**
  - Xcode 11.0およびそれ以降のバージョン。
  - osxシステムには10.11およびそれ以降のバージョンが必要です。
  - プロジェクトが有効な開発者による署名を設定済みであることを確認してください。
- **Windows 端末向け開発：**
    - OS:Windows 7 SP1およびそれ以降のバージョン(x86-64に基づく64ビットOS）。
    - ディスク容量：IDEと一部のツールのインストールに必要な容量を除く、少なくとも1.64 GB以上の空き容量を確保するようにしてください。
    - [Visual Studio 2019](https://visualstudio.microsoft.com/zh-hans/downloads/)をインストールします。

##  前提条件
[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com)をすでに行っていること。

## 操作手順

### ステップ1：アプリケーションの新規作成

1. TRTCコンソールにログインし、【[アプリケーション管理](https://console.tencentcloud.com/trtc/app)】を選択します。
2. 【アプリケーションの作成】をクリックし、`APIExample`などのアプリケーション名を入力します。すでにアプリケーションを作成している場合は、【既存のアプリケーションを選択】にチェックを入れ、【次のステップ】をクリックします。
   ![](https://qcloudimg.tencent-cloud.cn/raw/6704c9f7eb9e18e422c513cb9a2a3926.png)

### ステップ2：サンプルコードのダウンロード

1. UIなしの統合を選択後、ご自身の業務プラットフォームに合わせて、【[Github](https://github.com/LiteAVSDK/TRTC_Flutter/tree/master/TRTC-Simple-Demo)】で、関連するSDKと付属のDemoソースコードをダウンロードします。
2. ダウンロード完了後、【次のステップ】をクリックします。
   ![](https://qcloudimg.tencent-cloud.cn/raw/d28964ad85dddd85833a28310a62d514.png)

### ステップ3：プロジェクトの設定

1. サンプルプロジェクトのクイックスタート段階で【デバッグ段階】を選択します。その後、ご自身のSDKAppID、Secret keyを記録しておきます。
   ![](https://qcloudimg.tencent-cloud.cn/raw/82a45972f2d12763a6dc80eee6c952c0.png)
2. ダウンロードしたサンプルコードを開き、`/lib/debug/GenerateTestUserSig.dart`ファイルを見つけて開き、`GenerateTestUserSig.dart`ファイル内の関連パラメータを設定します。
   - SDKAPPID：デフォルトはPLACEHOLDERです。実際のSDKAppIDを設定してください。
   - SECRETKEY：デフォルトはPLACEHOLDERです。実際のSecret keyを設定してください。
3. プロジェクトの設定はこれで完了です。【次のステップ】をクリックしてください。

>?
>- ここで言及したUserSigの発行方法は、クライアントコードにSECRETKEYを設定しますが、この手法のSECRETKEYは逆コンパイルによって逆クラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この手法は、ローカルのTRTC-Simple-Demoクイックスタートおよび機能デバッグにのみ適しています**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供する方法となります。 UserSigが必要なときは、Appから業務サーバーにリクエストを送信し動的にUserSigを取得します。詳細は[サーバーでのUserSig新規作成](https://www.tencentcloud.com/document/product/647/35166)をご参照ください。

### ステップ4：コンパイル実行

1. `flutter pub get`を実行します
2. プロジェクトをコンパイル、実行またはデバッグします。

#### Androidのデバッグ：

1. `flutter run`を実行できます
2. Android Studio（3.5およびそれ以降のバージョン）を使用して、ソースプロジェクトを開くことができます。【実行】をクリックすれば完了です。

#### iOSのデバッグ：

1. `cd ios`を実行します
2. `pod install`を実行します
3. XCode（バージョン11.0以上）を使用してソースコードディレクトリ下の`/ios`プロジェクトを開き、Demoプロジェクトをコンパイルして実行すれば完了です。

#### windowsのデバッグ：

1. windowsサポート`flutter config --enable-windows-desktop`を有効にします
2. `flutter run -d windows`を実行します

#### macOSのデバッグ

1.  macOSサポートを有効にする：`flutter config --enable-macos-desktop`。
2. `cd macos`を実行します
3. `pod install`を実行します
4. `flutter run -d macos`を実行します


## よくあるご質問
###  TRTCのログはどうやって確認しますか。
TRTCログは、デフォルトで圧縮および暗号化され、接尾辞は `.xlog`です。アドレスは次のとおりです。
- **iOS 端末**：sandbox の `Documents/log`。
- **Android 端末**：
	- 6.7とそれ以前のバージョン：`/sdcard/log/tencent/liteav`
	- 6.8以後のバージョン：`/sdcard/Android/data/パッケージ名/files/log/tencent/liteav/`

### iOSでビデオが表示できない（Androidは正常）場合はどうすればよいですか？
お客様のプロジェクトの info.plist の`io.flutter.embedded_views_preview` の値がYESになっていることを確認してください。 

### Android Manifest merge failedでコンパイルに失敗した場合は？
`/example/android/app/src/main/AndroidManifest.xml` ファイルを開いてください。
    
1. `xmlns:tools="http://schemas.android.com/tools"` をmanifestの中に追加します。
2. `tools:replace="android:label"をapplicationの中に追加します。
![Illustration](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)

>? 詳細については、 [Flutterに関するご質問](https://intl.cloud.tencent.com/document/product/647/39242)をご参照ください。

