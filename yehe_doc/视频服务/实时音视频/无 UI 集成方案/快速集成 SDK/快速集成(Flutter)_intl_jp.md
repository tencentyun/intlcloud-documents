ここでは、主にTencent CloudのTRTC SDK(Flutter)をプロジェクトに素早く統合する方法を紹介します。以下の手順に従って設定すれば、 SDK の統合作業を完了できます。

>! 現在Windows/MacOs端末は画面共有およびデバイス選択の機能をサポートしていません。

## 環境要件
- Flutter 2.0以降のバージョン。
- **Android端末向け開発：**
  - Android Studio 3.5以降のバージョン。
  - AppにはAndroid 4.1以降のバージョンのデバイスが必要です。
**iOS & macOS端末向け開発：**
  - Xcode 11.0以降のバージョン。
  - osxシステムには10.11以降のバージョンが必要です。
  - プロジェクトが有効な開発者による署名を設定済みであることを確認してください。
- **Windows端末向け開発：**
	- OS:Windows 7 SP1以降のバージョン(x86-64に基づく64ビットOS）。
    - ディスク容量：IDEと一部のツールのインストールに必要な容量を除く、少なくとも1.64 GB以上の空き容量を確保するようにしてください。
	- [Visual Studio 2019](https://visualstudio.microsoft.com/zh-hans/downloads/)をインストールします。

## SDKの統合

Flutter SDKは[pubライブラリ](https://pub.dev/packages/tencent_trtc_cloud)に公開されています。`pubspec.yaml`を設定することで、更新を自動的にダウンロードできます。
1. プロジェクトの`pubspec.yaml`に次の依存関係を記述します。
```
dependencies:
  tencent_trtc_cloud:最新バージョン番号
```
2. **カメラ**と**マイク**の許可が有効になると、音声通話機能が起動します。
  <dx-tabs>
  ::: iOS\s端末
  1. `Info.plist`にカメラとマイクの許可申請を追加する必要があります。
```
<key>NSCameraUsageDescription</key>
<string>通常のビデオ通話が行えるようにカメラを許可します</string>
<key>NSMicrophoneUsageDescription</key>
<string>通常の音声通話が行えるようにマイクの権限を承認します</string>
```
2. フィールド`io.flutter.embedded_views_preview`を追加し、値をYESに設定します。
   :::
   ::: macOS\s端末

  1.`Info.plist`にカメラとマイクの許可申請を追加する必要があります。
```
<key>NSCameraUsageDescription</key>
<string>通常のビデオ通話が行えるようにカメラを許可します</string>
<key>NSMicrophoneUsageDescription</key>
<string>通常の音声通話が行えるようにマイクの権限を承認します</string>
<key>NSPhotoLibraryUsageDescription</key>
<string>Appがアルバムにアクセスするにはユーザーの同意が必要である。</string>
```
2. `macos/Runner/*.entitlements`ファイルの中で`com.apple.security.network.client`、`com.apple.security.network.server`を追加する必要があります。
    追加した後は次の図のようになります。
    ![](https://main.qcloudimg.com/raw/13f3eab720ec1da03b149db1a7240d6d.png)

3. Link Binary with Librariesの項目をクリックして展開し、一番下の「+」記号のアイコンをクリックして依存ライブラリを追加します。
    ![](https://main.qcloudimg.com/raw/17046154417930f9d31b6452782df55d.jpg)

4. 必要な依存ライブラリ`libbz2.1.0.tbd`を追加します。
    追加した後は次の図のようになります。
    ![](https://imgcache.qq.com/operation/dianshi/other/lib.7518607f9764321c99fbcf14348715b65563bca2.png)
    :::
    ::: Android\s端末

    1. /android/app/src/main/AndroidManifest.xml`ファイルを開きます。
    
    2. `xmlns:tools="http://schemas.android.com/tools"`をmanifestの中に追加します。
    
    3. `tools:replace="android:label"をapplicationの中に追加します。
    

<dx-alert infotype="explain">この手順を実行しないと、[Android Manifest merge failedコンパイルの失敗](https://intl.cloud.tencent.com/document/product/647/39242)という問題が発生します。</dx-alert>

![アイコン](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)
:::
::: Windows\s端末
1. Windowsサポートを有効にする：`flutter config --enable-windows-desktop`。
2. `flutter run -d windows`。
:::
</dx-tabs>


## よくあるご質問
- [iOSのパッケージングの実行時にCrashした場合はどうすればいいですか。](https://intl.cloud.tencent.com/document/product/647/39242)
- [iOSでビデオが表示できない場合（Androidでは正常）はどうすればいいですか。](https://intl.cloud.tencent.com/document/product/647/39242)
- [SDKのバージョンを更新した後、iOS CocoaPodsの実行にエラーが出た場合はどうすればいいですか。](https://intl.cloud.tencent.com/document/product/647/39242)
- [Android Manifest merge failedでコンパイルに失敗した場合はどうすればいいですか。](https://intl.cloud.tencent.com/document/product/647/39242)
- [署名がないため、実機でのデバック時にエラーが出た場合はどうすればいいですか。](https://intl.cloud.tencent.com/document/product/647/39242)
- [プラグインの中のswiftファイルを追加・削除した後、build（ビルド）時に対応するファイルが見つからないのはなぜですか。](https://intl.cloud.tencent.com/document/product/647/39242)
- [Run（実行）時にエラー：「Info.plit, error: No value at that key path or invalid key path: NSBonjourServices」が出た場合はどうすればいいですか。](https://intl.cloud.tencent.com/document/product/647/39242)
- [Pod install時にエラーが出た場合はどうすればいいですか。](https://intl.cloud.tencent.com/document/product/647/39242)
- [Run（実行）時にiOS版で依存エラーが出た場合はどうすればいいですか。](https://intl.cloud.tencent.com/document/product/647/39242)

