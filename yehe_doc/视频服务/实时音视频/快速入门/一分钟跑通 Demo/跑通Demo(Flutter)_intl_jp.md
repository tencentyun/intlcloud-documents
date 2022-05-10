ここでは、主にTRTC Demo（Flutter）を素早く実行する方法について説明します。

>! 現在、Flutter SDKはAndroidとiOSのみ対応しています。

## 環境要件
- Flutter 2.0以降のバージョン。
- **Android端末向け開発：**
  - Android Studio 3.5以降のバージョン。
  - AppにはAndroid 4.1以降のバージョンのデバイスが必要です。
- **iOS & macOS端末向け開発：**
  - Xcode 11.0以降のバージョン。
  - osxシステムには10.11以降のバージョンが必要です。
  - プロジェクトが有効な開発者による署名を設定済みであることを確認してください。
- **Windows 端末向け開発：**
    - OS：Windows 7 SP1以降のバージョン（x86-64に基づく64ビットOS）。
    - ディスク容量：IDEと一部のツールのインストールに必要な容量を除く、少なくとも1.64 GB以上の空き容量を確保するようにしてください。
    - [Visual Studio 2019](https://visualstudio.microsoft.com/zh-hans/downloads/)をインストールします。

## 前提条件
 すでに[Tencent Cloudアカウントを登録](https://intl.cloud.tencent.com)済みです。

## 操作手順
[](id:step1)

### ステップ1：アプリケーションの新規作成
1. TRTCコンソールにログインし、【開発支援】>【[Demoのクイック実行](https://console.cloud.tencent.com/trtc/quickstart)】を選択します。

2. 【アプリケーションの作成】をクリックし、`TestTRTC`などのアプリケーション名を入力します。すでにアプリケーションを作成している場合、【既存のアプリケーションを選択】をクリックします。

3. 実際の業務ニーズに応じてタグを追加または編集し、【作成】をクリックします。

   ![](https://qcloudimg.tencent-cloud.cn/raw/7d1d1940f02ee954c369b5f749e0c663.png)
>?
>- アプリケーション名には、数字、中国語と英語の文字、アンダーラインのみを含めることができます。長さは15文字以内とします。
>- タグはTencent Cloudのさまざまなリソースを識別して管理するために使用されます。たとえば、企業に複数の事業部門があり、各部門に1つ以上のTRTCアプリケーションがある場合、企業はTRTCアプリケーションにタグを追加することで部門情報にマークを付けることができます。タグは入力必須ではありません。実際のビジネスニーズに応じてタグを追加または編集できます。

[](id:step2)
### ステップ2：SDKおよびDemoソースコードのダウンロード
1. 実際の業務ニーズに応じて、SDKと関連の[Demoソースコード](https://github.com/LiteAVSDK/TRTC_Flutter/tree/master/TRTC-Simple-Demo)をダウンロードします。
2. ダウンロード完了後、【ダウンロード済み。次へ】をクリックします。
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)


[](id:step3)
### ステップ3：Demoプロジェクトファイルの設定
1. 設定変更画面に進み、ダウンロードしたソースコードパッケージに基づいて対応する開発環境を選択します。
2. `TRTC-Simple-Demo/example/lib/debug/GenerateTestUserSig.dart` ファイルを見つけて開きます。
3. `GenerateTestUserSig.dart` ファイル内の関連パラメータを設定します：
<ul><li/>SDKAPPID：デフォルト値はPLACEHOLDERです。実際のSDKAppIDに設定してください。
	<li/>SECRETKEY：デフォルト値はPLACEHOLDERです。実際のキー情報に設定してください。</ul>
<img src="https://qcloudimg.tencent-cloud.cn/raw/e210b7b71cf273de59d6e2df917101e4.png"/>

4. 貼り付け完了後、【貼り付け済み。次へ】をクリックすれば、作成が完了します。
5. コンパイル完了後、【コンソールの概要ページに戻る】をクリックすればOKです。

>?
>- ここで言及したUserSigの新規作成ソリューションでは、クライアントコードでSECRETKEYを設定します。この手法のうちSECRETKEYは逆コンパイルによって逆向きにクラッキングされやすく、キーがいったん漏洩すると、攻撃者はTencent Cloudトラフィックを盗用できるようになります。そのため**この方法は、ローカルのDemoクイック実行および機能デバッグにのみ適合します**。
>- UserSigの正しい発行方法は、UserSigの計算コードをサーバーに統合し、Appのインターフェース向けに提供します。UserSigが必要なときは、Appから業務サーバーにリクエストを発出し動的にUserSigを取得します。詳細は[UserSigに関するご質問](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。

[](id:step4)

### ステップ4：コンパイル実行
1. `flutter pub get`を実行します。
2. コンパイルを実行し、デバッグを行います。
<dx-tabs>
:::  Android\s端末
1. `flutter run`を実行します。
2. Android Studio（3.5およびそれ以降のバージョン）を使用して、ソースプロジェクトを開き、【実行】をクリックすれば完了です。
:::
::: iOS\s端末
1. iosディレクトリ`podinstall`に移動します。
2. XCode（11.0およびそれ以降のバージョン）を使用してソースディレクトリ配下の`/ios`プロジェクトを開き、Demoプロジェクトをコンパイルして実行します。
:::
::: Windows\s端末
1. Windowsサポートの有効化：`flutter config --enable-windows-desktop`。
2. `flutter run -d windows`。
:::
::: macOS\s端末
1. macOSサポートの有効化：`flutter config --enable-macos-desktop`。
2. macosディレクトリ`pod install`に移動します。
2. `flutter run -d macos`を実行します。
:::
</dx-tabs>

## よくあるご質問
### TRTCのログはどのように確認しますか？
TRTCログは、デフォルトで圧縮および暗号化され、接尾辞は`.xlog`です。アドレスは次のとおりです。
- **iOS 端末**：sandbox の `Documents/log`。
- **Android 端末**：
	- 6.7とそれ以前のバージョン：`/sdcard/log/tencent/liteav`
	- 6.8以降のバージョン：`/sdcard/Android/data/パッケージ名/files/log/tencent/liteav/`

### iOSでビデオが表示できない（Androidは正常）場合はどうすればよいですか？
お客様のプロジェクトの info.plist の`io.flutter.embedded_views_preview` の値がYESになっていることを確認してください。 

### Android Manifest merge failedというコンパイルエラーが発生した場合はどうすればよいですか？？
`/example/android/app/src/main/AndroidManifest.xml` ファイルを開いてください。
    1. `xmlns:tools="http://schemas.android.com/tools"` をmanifestの中に追加します。
        2. `tools:replace="android:label"をapplicationの中に追加します。
![アイコン](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)

>? 詳細については、[Flutterに関するご質問](https://intl.cloud.tencent.com/document/product/647/39242)をご参照ください。

