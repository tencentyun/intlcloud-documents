本書では、Tencent Cloud IM SDKをご利用のFlutterプロジェクトに速やかに統合する方法を説明します。

## 環境要件

| プラットフォーム | バージョン                                                   |
| ---------------- | ------------------------------------------------------------ |
| Flutter          | 2.2.0以降                                                    |
| Android          | Android Studio 3.5以降。AppはAndroid 4.1以降のデバイスを使用すること |
| iOS              | Xcode 11.0以降。物理デバイスでデバッグする時、プロジェクトに有効な開発者署名が設定されていること |

## サポートするプラットフォーム

FlutterのすべてのプラットフォームをサポートするIM SDKとTUIKitの構築に取り組み、1つのコードセットですべてのプラットフォームで実行することを支援します。

| プラットフォーム                                             | サポート状態          |
| ------------------------------------------------------------ | --------------------- |
| iOS                                                          | サポート              |
| Android                                                      | サポート              |
| [Web](#web)                                                  | 4.1.1+2以降でサポート |
| [macOS](#pc)                                                 | 4.1.9以降でサポート   |
| [Windows](#pc)                                               | 4.1.9以降でサポート   |
| [クロスプラットフォーム](https://www.tencentcloud.com/document/product/1047/51456) （Flutter SDKを既存のネイティブAppに追加） | 5.0.0以降でサポート   |

>? Web/macOS/Windowsプラットフォームの場合、追加して実施することがあるので、詳しくは、本書の[Webとの互換性](#web) と[Desktopとの互換性](#pc)をご参照ください。

## 体験DEMO

正式に開始する前に、DEMOを使って、IM FlutterのクロスプラットフォームSDKとTUIKitの機能を体験できます。

**以下の各バージョンのDEMOは、同じFlutterプロジェクトでパッケージングされています。**Desktop(macOS/Windows)プラットフォームでは、SDKはサポートされています。DEMOは近日中にアクティベートする予定です。

<table style="text-align:center; vertical-align:middle; max-width: 800px">
  <tr>
    <th style="text-align:center;">モバイルAPP</th>
    <th style="text-align:center;">WEB - H5</th>
  </tr>
  <tr>
    <td><div style="display: flex; justify-content: center; align-items: center; flex-direction: column; padding-top: 10px">iOS/Android APP。プラットフォームを自動的に判断してダウンロード<img style="max-width:200px; margin: 20px 0 20px 0" src="https://qcloudimg.tencent-cloud.cn/raw/ca2aaff551410c74fce48008c771b9f6.png"/></div></td>
    <td><div style="display: flex; justify-content: center; align-items: center; flex-direction: column; padding-top: 10px">QRコードをスキャンしオンラインWeb版のDEMOを体験<img style="max-width:200px; margin: 20px 0 20px 0" src="https://qcloudimg.tencent-cloud.cn/raw/3c79e8bb16dd0eeab35e894a690e0444.png"/></div></td>
  </tr>
</table>

## IM SDKの統合

[pub add](https://pub.dev/packages/tencent_cloud_chat_sdk)を使用しTencent Cloud IM SDK (Flutter)を直接統合するか、pubspec.yamlにIM SDKを書き込むことで統合を実装できます。

### flutter pub addのインストール

端末のウィンドウに以下のコマンドを入力します（事前にFlutter環境をインストールしてください）。

```
flutter pub add tencent_cloud_chat_sdk
```

>?ご利用のプロジェクトが[Web](#web) または [Desktop(macOS、Windows)](#pc)にも使用された場合、本書の最後に記載した追加手順も実施してください。

### pubspec.yamlへの書込み

```
dependencies:
  tencent_cloud_chat_sdk: "最新版" //https://pub.dev/packages/tencent_cloud_chat_sdkでim flutter sdkの最新版を確認して使用できる
```

この場合、ご利用のeditorは自動的にflutter pub getを実行する可能性があります。実行していない場合、Tencent Cloud Command Line Interfaceに手動でflutter pub getを入力してください。

ご利用のプロジェクトでWebをサポートする必要があれば、以下を実施する前に、[Webとの互換性の章を確認](#web)して、JSファイルを導入してください。

### SDKの導入と初期化

```
import 'package:tencent_cloud_chat_sdk/tencent_cloud_chat_sdk.dart';
```

## Flutter for Webサポート[](id:web)

IM SDK(tencent_cloud_chat_sdk) 4.1.1+2以降では、Web側と完全に互換性を持っています。

Android側とiOS側に比べ、以下を追加して実施する必要があります。具体的には、以下のとおりです：

### Flutter 3.xへのアップデート

Flutter 3.xにはWeb性能向けの最適化が多く取り込まれているため、Flutter 3.xを使用しFlutter Webプロジェクトを開発することを強くお勧めします。

### JSの導入

>?既存のFlutterプロジェクトでWebがサポートされない場合、プロジェクトのルートディレクトリで`flutter create .`を実行し、Webへのサポートを追加します。

プロジェクトの`web/`ディレクトリに入って、`npm`または`yarn`を実行してJSの依存パッケージをインストールします。プロジェクトを初期化する時、案内に従って実行すればよいです。

```shell
cd web

npm init

npm i tim-js-sdk

npm i tim-upload-plugin
```

`web/index.html`を開き、`<head> </head>`にJSファイルを導入します。具体的には、以下のとおりです：

```html
<script src="./node_modules/tim-upload-plugin/index.js"></script>
<script src="./node_modules/tim-js-sdk/tim-js-friendship.js"></script>
```

![](https://staticintl.cloudcachetci.com/yehe/backend-news/AhQ9056_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_1672108602242.png)

### Flutter for Web追加SDKの導入

```dart
flutter pub add tencent_im_sdk_plugin_web
```

## Flutter for Desktop(PC)サポート[](id:pc)

UIなしIM SDK(tencent_cloud_chat_sdk) 4.1.9以降では、macOS側、Windows側と完全に互換性を持っています。

Android側とiOS側に比べ、以下を追加して実施する必要があります。具体的には、以下のとおりです：

### Flutter 3.xへのアップデート

Flutter 3.0以降のみでdesktop側のパッケージングを実行できるため、必要に応じて、Flutter 3.xにアップデートしてください。

### Flutter for Desktop追加SDKの導入

```dart
flutter pub add tencent_im_sdk_plugin_desktop
```

#### macOSの変更

`macos/Runner/DebugProfile.entitlements`ファイルを開きます。

`<dict></dict>`に`key-value`キー値ぺアを追加します。

```
<key>com.apple.security.app-sandbox</key>
<false/>
```

## よくあるご質問

### flutter pub get/add実行失敗の解決方法は？

公式サイトの説明を参照し[国内イメージ](https://flutter.cn/community/china)を設定してください。
