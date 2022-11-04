Tencent Cloud View Cube Flutterプレーヤーは、Tencent Cloudによるオープンソースのプレーヤーコンポーネントです。簡単な数行のコードで、Tencent Videoのような強力な再生機能を備えることができます。画面の縦横切り替え、解像度の選択、ジェスチャー、ミニウィンドウなどの基本機能を備えるほか、ビデオキャッシュ、ソフトウェア/ハードウェアデコードの切り替え、倍速再生などの特殊機能もサポートしています。システムのプレーヤーよりも、サポートする形式が多く、互換性に優れ、機能もより強力です。同時に、CSSストリーム（FLV+RTMP）再生をサポートし，トップ画面の秒速起動、低遅延などの優位性、解像度のシームレスな切り替え、CSSタイムシフトなどの高度な機能を備えています。
このプレーヤーはオンデマンドおよびCSS再生をベースとしたFlutterプラグインであり、AndroidおよびiOSの両プラットフォームを同時にサポートしています。完全に無料のオープンソースであり、再生アドレスソースに対する制限がないので、安心してご使用いただけます。

## SDKのダウンロード

Tencent Cloud View Cube Flutterプレーヤーのプロジェクトアドレスは、[Player Flutter](https://github.com/LiteAVSDK/Player_Flutter)です。

## プロジェクトの概要

Tencent Cloud View Cube·Player+はオーディオビデオ端末SDK（Tencent Cloud View Cube）のサブ製品SDKの一つであり、Tencent Cloudの強力なバックエンド機能とAIテクノロジーをベースに、ビデオオンデマンドとライブストリーミング再生機能をご提供する、優れた再生媒体です。Tencent CloudのVideo on Demand（VOD）またはCloud Streaming Services（CSS）と組み合わせて使用することで、スムーズで安定した再生パフォーマンスをすぐに体験できます。様々なユースケースに対応し、お客様の多様なニーズを満たすことができるため、お客様は安心して業務に専念でき、超高速で高画質な再生という新体験を存分に楽しむことができます。

このプロジェクトではVOD再生とCSS再生をご提供します。プレーヤーをベースに、ご自身の再生業務を構築することができます。

- [VOD再生](https://github.com/LiteAVSDK/Player_Flutter/blob/main/Flutter/docs/VOD再生.md)：`TXVodPlayerController`でAndroidおよびiOSという2つのプラットフォームのVOD Player SDKに対し、インターフェースのパッケージ化を行います。`TXVodPlayerController`を統合することで、VOD再生業務の開発を行うことができます。詳細な使用例については、`DemoTXVodPlayer`をご参照ください。
- [CSS再生](https://github.com/LiteAVSDK/Player_Flutter/blob/main/Flutter/docs/直播播放.md)：`TXLivePlayerController`でAndroidおよびiOSという2つのプラットフォームのライブストリーミングPlayer SDKに対し、インターフェースのパッケージ化を行います。`TXLivePlayerController`を統合することで、CSS再生業務の開発を行うことができます。詳細な使用例については、`DemoTXLivePlayer`をご参照ください。

接続コストを削減するため、exampleでプレーヤーコンポーネント（UI付きのプレーヤー）をご提供しています。プレーヤーの簡単な数行のコードによってビデオ再生業務を構築できます。ご自身のプロジェクトのニーズに基づいて、プレーヤーコンポーネントの関連コードをプロジェクトに適用し、ニーズに応じてUIとインタラクションの細部を調整することができます。

- [プレーヤーコンポーネント](https://github.com/LiteAVSDK/Player_Flutter/blob/main/Flutter/docs/播放器组件.md)：`SuperPlayerController`プレーヤーコンポーネントは、VODとライブストリーミングを再パッケージ化し、スピーディーで簡単な統合を可能にします。現在はBeta版のため、機能はまだ整備中です。詳細な使用例については、`DemoSuperplayer`をご参照ください。

## クイックインテグレーション

### pubspec.yamlの設定

1. LiteAVSDK_Playerバージョンを統合します。デフォルトでもこのバージョンの統合となります。

   ```
   pubspec.yaml
   ```

   に次の設定を追加します。

   ```yaml
   super_player:
     git:
       url: https://github.com/LiteAVSDK/Player_Flutter
       path: Flutter
   ```

2. LiteAVSDK_Professionalバージョンを統合したい場合は、

   ```
   pubspec.yaml
   ```

   内の設定を次のように変更します。

   ```yaml
   super_player:
     git:
       url: https://github.com/LiteAVSDK/Player_Flutter
       path: Flutter
       ref: Professional
   ```

3. 依存パッケージを更新します。

   ```yaml
   flutter packages get
   ```

### ネイティブの設定を追加

#### Androidの設定

Androidの`AndroidManifest.xml`に次の設定を追加します。

```xml
<!--ネットワーク権限-->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!--VODプレーヤーのフローティングウィンドウ権限-->
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<!--Storage-->
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```



#### iOSの設定

1. iOSの

   ```
   Info.plist
   ```

   に次の設定を追加します。

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
       <key>NSAllowsArbitraryLoads</key>
       <true/>
   </dict>
   ```

2. iOSは

   ```
   pod
   ```

   方式をネイティブに使用して依存するため、

   ```
   podfile
   ```

   ファイルを編集して、Player SDKのバージョンを指定します。デフォルトではPlayer版SDKを統合します。

   ```xml
   pod 'TXLiteAVSDK_Player'            //Player版
   ```

3. Professional版SDKを統合します。

   ```
   pod 'TXLiteAVSDK_Professional'     //Professional版
   ```

バージョンを指定しない場合は、デフォルトで最新バージョンの`TXLiteAVSDK_Player`がインストールされます。

### 統合の過程でのよくあるご質問

- `flutter doctor`コマンドを実行して実行環境を確認すると、「No issues found!」が表示されました。
- `flutter pub get`を実行し、すべての依存コンポーネントが正常に更新されていることを確認します。

## ビデオ再生機能Licenseおよび統合の申請

すでに関連するLicense権限承認を取得している場合は、[Tencent Cloud View Cubeコンソール](https://console.cloud.tencent.com/vcube)にて、License URLおよびLicense Keyを取得する必要があります。
License権限をまだ取得していない場合は、[お問い合わせ](https://intl.cloud.tencent.com/contact-us)いただき、関連の権限承認を取得する必要があります。

プレーヤーを統合する前に、[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/login)が必要です。登録完了後、ビデオ再生機能Licenseを申請し、次の方式で統合します。アプリケーション起動時に行うことをお勧めします。

Licenseを統合していない場合、再生中に異常が発生することがあります。

```dart
String licenceURL = ""; // 取得したlicence url
String licenｃeKey = ""; // 取得したlicence key
SuperPlayerPlugin.setGlobalLicense(licenceURL, licenceKey);
```



## VODプレーヤーの使用

VODプレーヤーのコアクラスは`TXVodPlayerController`です。詳細なDemoについては`DemoTXVodPlayer`をご参照ください。
バージョン10.7.0より、正常に再生を行うには、{@link SuperPlayerPlugin#setGlobalLicense}でのLicenceの設定が必要になりました。これを行わなければ再生が失敗します（ブラックスクリーン）。設定はグローバルで1回行うだけです。ライブストリーミングLicence、UGSV Licenceおよびビデオ再生Licenceがすべて使用できます。上記のLicenceをまだ取得していない場合は、テスト版Licenceを無料でクイック申請して再生できますが、正式版Licenseのご購入は必要です。



```dart
import 'package:flutter/material.dart';
import 'package:super_player/super_player.dart';

class Test extends StatefulWidget {
  @override
  State<StatefulWidget> createState() => _TestState();
}

class _TestState extends State<Test> {
  late TXVodPlayerController _controller;

  double _aspectRatio = 16.0 / 9.0;
  String _url =
          "http://1400329073.vod2.myqcloud.com/d62d88a7vodtranscq1400329073/59c68fe75285890800381567412/adp.10.m3u8";

  @override
  void initState() {
    super.initState();
    String licenceUrl = ""; // 取得したlicence url
    String licenseKey = ""; // 取得したlicence key
    SuperPlayerPlugin.setGlobalLicense(licenceUrl, licenseKey);
    _controller = TXVodPlayerController();
    initPlayer();
  }

  Future<void> initPlayer() async {
    await _controller.initialize();
    await _controller.startVodPlay(_url);
  }

  @override
  Widget build(BuildContext context) {
    return Container(
            height: 220,
            color: Colors.black,
            child: AspectRatio(aspectRatio: _aspectRatio, child: TXPlayerVideo(controller: _controller)));
  }
}
```



## プレーヤーコンポーネントの使用

プレーヤーコンポーネントのコアクラスは、`SuperPlayerVideo`です。作成後すぐにビデオを再生できます。
バージョン10.7.0より、正常に再生を行うには、{@link SuperPlayerPlugin#setGlobalLicense}でのLicenceの設定が必要になりました。これを行わなければ再生が失敗します（ブラックスクリーン）。設定はグローバルで1回行うだけです。ライブストリーミングLicence、UGSV Licenceおよびビデオ再生Licenceがすべて使用できます。上記のLicenceをまだ取得していない場合は、テスト版Licenceを無料でクイック申請して再生できますが、正式版Licenseのご購入は必要です。



```dart
import 'package:flutter/material.dart';
import 'package:super_player/super_player.dart';

/// flutter superplayer demo
class DemoSuperplayer extends StatefulWidget {
  @override
  State<StatefulWidget> createState() => _DemoSuperplayerState();
}

class _DemoSuperplayerState extends State<DemoSuperplayer> {
  List<SuperPlayerModel> videoModels = [];
  bool _isFullScreen = false;
  SuperPlayerController _controller;

  @override
  void initState() {
    super.initState();
    String licenceUrl = "購入したlicenseのurlを入力";
    String licenseKey = "購入したlicenseのkeyを入力";
    SuperPlayerPlugin.setGlobalLicense(licenceUrl, licenseKey);
    _controller = SuperPlayerController(context);
    FTXVodPlayConfig config = FTXVodPlayConfig();
    config.preferredResolution = 720 * 1280;
    _controller.setPlayConfig(config);
    _controller.onSimplePlayerEventBroadcast.listen((event) {
      String evtName = event["event"];
      if (evtName == SuperPlayerViewEvent.onStartFullScreenPlay) {
        setState(() {
          _isFullScreen = true;
        });
      } else if (evtName == SuperPlayerViewEvent.onStopFullScreenPlay) {
        setState(() {
          _isFullScreen = false;
        });
      }else{
        print(evtName);
      }
    });
    initData();
  }

  @override
  Widget build(BuildContext context) {
    return WillPopScope(
        child: Container(
          child: Scaffold(
            backgroundColor: Colors.transparent,
            appBar: _isFullScreen
                ? null
                : AppBar(
                    backgroundColor: Colors.transparent,
                    title: const Text('SuperPlayer'),
                  ),
            body: SafeArea(
              child: Builder(
                builder: (context) => getBody(),
              ),
            ),
          ),
        ),
        onWillPop: onWillPop);
  }

  Future<bool> onWillPop() async {
    return !_controller.onBackPress();
  }

  Widget getBody() {
    return Column(
      children: [_getPlayArea()],
    );
  }

  Widget _getPlayArea() {
    return SuperPlayerView(_controller);
  }

  Widget _getListArea() {
    return Container(
      margin: EdgeInsets.only(top: 10),
      child: ListView.builder(
        itemCount: videoModels.length,
        itemBuilder: (context, i) => _buildVideoItem(videoModels[i]),
      ),
    );
  }

  Widget _buildVideoItem(SuperPlayerModel playModel) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        ListTile(
            leading: Image.network(playModel.coverUrl),
            title: new Text(
              playModel.title,
              style: TextStyle(color: Colors.white),
            ),
            onTap: () => playCurrentModel(playModel)),
        Divider()
      ],
    );
  }

  void playCurrentModel(SuperPlayerModel model) {
    _controller.playWithModelNeedLicence(model);
  }

  void initData() async {
    SuperPlayerModel model = SuperPlayerModel();
    model.videoURL = "http://1500005830.vod2.myqcloud.com/6c9a5118vodcq1500005830/48d0f1f9387702299774251236/gZyqjgaZmnwA.m4v";
    model.playAction = SuperPlayerModel.PLAY_ACTION_AUTO_PLAY;
    model.title = "Tencent Cloudオーディオビデオ";
    _controller.playWithModelNeedLicence(model);
  }

  @override
  void dispose() {
    // must invoke when page exit.
    _controller.releasePlayer();
    super.dispose();
  }
}
```

## ハイレベルカスタム開発ガイド

Tencent Cloud Player+ Flutterプラグインはネイティブプレーヤー機能をパッケージ化したものです。ハイレベルなカスタム開発を行う必要がある場合は、次の方法を用いることをお勧めします。

- VOD再生をベースにして、インターフェースクラスを`TXVodPlayerController`とするか、またはライブストリーミング再生をベースにして、インターフェースクラスを`TXLivePlayerController`としてカスタム開発を行います。プロジェクトではカスタム開発Demoをご提供しています。exampleプロジェクト内の`DemoTXVodPlayer`および`DemoTXLivePlayer`をご参照ください。

- プレーヤーコンポーネント`SuperPlayerController`はVODとCSSをパッケージ化し、同時に簡単なUIインタラクションをご提供しています。このため、この部分のコードがexampleディレクトリ内に存在します。プレーヤーコンポーネントをカスタマイズしたい場合は、次のように操作します。

  プレーヤーコンポーネントの関連コード（コードディレクトリ：`exmple/lib/superplayer`）をプロジェクトにコピーし、カスタム開発を行います。

## その他の機能

完全な機能は、2次元コードをスキャニングし、ビデオクラウドツールキットをダウンロードして体験するか、またはプログラムのDemoを直接実行することもできます。
![img](https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png)