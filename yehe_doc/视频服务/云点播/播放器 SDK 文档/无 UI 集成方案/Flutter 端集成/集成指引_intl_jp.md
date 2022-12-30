## 環境の準備

- Flutter 2.0およびそれ以降のバージョン。
- Androidの開発：
  -  Android Studio 3.5およびそれ以降のバージョン。
  -  AppにはAndroid 4.1およびそれ以降のバージョンのデバイスが必要です。
- iOSの開発：
  - Xcode 11.0およびそれ以降のバージョン。
  - OSXシステムのバージョンは10.11およびそれ以降が必要です。
  - プロジェクトが有効な開発者による署名を設定済みであることを確認してください。

## SDKのダウンロード

Tencent Cloud View Cube Flutterプレーヤーのプロジェクトアドレスは、[Player Flutter](https://github.com/LiteAVSDK/Player_Flutter)です。

## クイックインテグレーション

### プロジェクトのpubspec.yamlへの依存の追加

LiteAVSDK PlayerまたはProfessionalバージョンをベースにした統合をサポートしています。プロジェクトの必要性に応じて統合することができます。

1. LiteAVSDK_Playerバージョンの最新バージョンを統合します。デフォルトでもこのバージョンの統合となります。`pubspec.yaml`に次の設定を追加します。
```yaml
super_player:
  git:
    url: https://github.com/LiteAVSDK/Player_Flutter
    path: Flutter
```
LiteAVSDK_Professionalの最新バージョンを統合する場合は、`pubspec.yaml`内の設定を次のように変更します。
```yaml
super_player:
  git:
    url: https://github.com/LiteAVSDK/Player_Flutter
    path: Flutter
    ref: Professional
```
指定するプレーヤーバージョンのSDKを統合したい場合は、次のように、refの依存するtagによって対応するバージョンを指定することができます。
```yaml
super_player:
  git:
    url: https://github.com/LiteAVSDK/Player_Flutter
    path: Flutter
    ref: release_player_v1.0.6 

# release_player_v1.0.6はAndroid端末ではTXLiteAVSDK_Player_10.6.0.11182バージョン、iOS端末ではTXLiteAVSDK_Player_10.6.11821バージョンを統合することを表します。
```

その他のアーカイブtagについては[releaseリスト](https://github.com/LiteAVSDK/Player_Flutter/releases)をご参照ください。

2. 統合後、コードエディタ付属のUIによってFlutterの依存を取得することができます。次のコマンドを直接使用して取得することもできます

```yaml
flutter packages get
```

3. 使用中に、次のコマンドによって既存のFlutter依存を更新することができます。

```dart
flutter pub upgrade
```

### ネイティブの設定を追加

#### Android端末の設定
1. Androidの`AndroidManifest.xml`に次の設定を追加します。
```xml
<!--ネットワーク権限-->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!--Storage-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

2. Androidディレクトリ下の`build.gradle`がmavenCenterを使用していて、依存を正常にダウンロードできることを確認します
```groovy
repositories {
  mavenCentral()
}
```

3. ネイティブSDKの依存バージョンを更新する必要がある場合は、Androidディレクトリ下の`build`フォルダを手動で削除するか、または次のコマンドを使用して強制的に更新することができます。
```shell
./gradlew build
```

4. Androidのピクチャーインピクチャー機能を使用したい場合は、exampleコンポーネント内のandroidディレクトリ下の`FTXFlutterPipActivity.java`を統合し、ピクチャーインピクチャー機能を正常に使用できるようにする必要があります。


#### iOS端末の設定

注意：**iOS端末は現在エミュレーターでのデバッグ実行をサポートしていません。開発デバッグは実機で実行することをお勧めします**。

1. iOSの`Info.plist`に次の設定を追加します。
```xml
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSAllowsArbitraryLoads</key>
    <true/>
</dict>
```
2. iOSは`pod`方式をネイティブに使用して依存するため、`podfile`ファイルを編集して、Player+のバージョンを指定します。デフォルトではPlayer版SDKを統合します。
```xml
pod 'TXLiteAVSDK_Player'	        //Player版
```
 Professional版SDKを統合します。
```
pod 'TXLiteAVSDK_Professional' 	//Professional版
```

バージョンを指定しない場合は、デフォルトで最新バージョンの`TXLiteAVSDK_Player`がインストールされます。

3. 一部の状況（新バージョンのリリースなど）では、iOSプレーヤーの依存を強制的に更新する必要があります。iOSディレクトリ下で次のコマンドを使用して更新を行うことができます。
```shell
rm -rf Pods
rm -rf Podfile.lock
pod update
```

## ビデオ再生Licenseの統合
すでにLicense権限承認を取得している場合は、[Tencent Cloud View Cubeコンソール](https://www.tencentcloud.com/account/login)  にて、License URLおよびLicense Keyを取得する必要があります。

License権限承認を取得していない場合は、先に[ビデオ再生License](https://www.tencentcloud.com/document/product/266/51098)をご参照の上、関連の権限承認を取得する必要があります。

プレーヤーを統合する前に、[Tencent Cloudアカウントの登録](https://www.tencentcloud.com/account/login)が必要です。登録完了後、ビデオ再生機能Licenseを申請し、次の方式で統合します。アプリケーション起動時に行うことをお勧めします。

Licenseを統合していない場合、再生中に異常が発生することがあります。
```dart
String licenceURL = ""; // 取得したlicence url
String licenｃeKey = ""; // 取得したlicence key
SuperPlayerPlugin.setGlobalLicense(licenceURL, licenceKey);
```

## ハイレベルカスタム開発ガイド

Tencent Cloud Player+ Flutterプラグインはネイティブプレーヤー機能をパッケージ化したものです。ハイレベルなカスタム開発を行う必要がある場合は、次の方法を用いることをお勧めします。

- VOD再生をベースにして、インターフェースクラスを`TXVodPlayerController`とするか、またはライブストリーミング再生をベースにして、インターフェースクラスを`TXLivePlayerController`としてカスタム開発を行います。プロジェクトではカスタム開発Demoをご提供しています。exampleプロジェクト内の`DemoTXVodPlayer`および`DemoTXLivePlayer`をご参照ください。

- プレーヤーコンポーネント`SuperPlayerController`はVODとCSSをパッケージ化し、同時に簡単なUIインタラクションをご提供しています。このため、この部分のコードがexampleディレクトリ内に存在します。プレーヤーコンポーネントをカスタマイズしたい場合は、次のように操作します。

  プレーヤーコンポーネントの関連コード（コードディレクトリ：`exmple/lib/superplayer`）をプロジェクトにコピーし、カスタム開発を行います。

## よくあるご質問

1. iOS端末での実行の際に、`No visible @interface for 'TXLivePlayer' declares the selector 'startLivePlay:type:'`のような、インターフェースが見つからないというエラーが発生しました。
次のコマンドを使用して、iOS SDKを更新することができます。
```shell
rm -rf Pods
rm -rf Podfile.lock
pod update
```

2. tencent_trtc_cloudとFlutterプレーヤーを同時に統合すると、SDKまたはシンボルの競合が発生しました。

   よくある異常ログ：`java. lang.RuntimeException: Duplicate class com.tencent.liteav.TXLiteAVCode found in modules classes.jar`

   この場合はflutterプレーヤーのProfessionalバージョンを統合し、tencent_trtc_cloudとflutterプレーヤーの両方を同一のバージョンのLiteAVSDK_Professionalに依存させる必要があります。依存するLiteAVSDK_Professionalのバージョンは必ず同じにしなければならないことにご注意ください。

   例えば、Android端末のTXLiteAVSDK_Professional_10.3.0.11196およびiOS端末のTXLiteAVSDK_Professional to 10.3.12231に依存する場合、依存ステートメントは次のようになります。
   ```xml
   tencent_trtc_cloud: 2.3.8
   
   super_player:
     git:
       url: https://github.com/LiteAVSDK/Player_Flutter
       path: Flutter
       ref: release_pro_v1.0.3.11196_12231
   ```
3. 同時に複数のプレーヤーインスタンスを使用する必要があり、再生するビデオを頻繁に切り替えると、画面が不鮮明になります。
	各プレーヤーコンポーネントのコンテナを破棄する際、プレーヤーの`dispose`メソッドを呼び出し、プレーヤーを解放します。
4. Flutterの依存に関するその他の一般的な問題：
 - 「No issues found!」が表示されるまで、`flutter doctor`コマンドを実行して実行環境をチェックします。
 - `flutter pub get`を実行し、すべての依存コンポーネントが正常に更新されていることを確認します。

## その他の機能

プロジェクト内のexampleを実行してすべての機能を体験できます（example実行ガイド）。

Player SDK公式サイトではiOS、Android、Web端末のDemoを体験できます。[ここをクリックしてください](https://www.tencentcloud.com/document/product/266/42091) 。

