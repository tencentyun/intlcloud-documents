Tencent Cloud View Cube Flutter Super Playerは、Tencent Cloudによるオープンソースのプレーヤーコンポーネントです。簡単な数行のコードで、Tencent Videoのような強力な再生機能を備えることができます。画面の縦横切り替え、解像度の選択、ジェスチャー、ミニウィンドウなどの基本機能を備えるほか、ビデオキャッシュ、ソフトウェア/ハードウェアデコードの切り替え、倍速再生などの特殊機能もサポートしています。システムのプレーヤーよりも、サポートする形式が多く、互換性に優れ、機能もより強力です。同時に、CSSストリーム（flv+rtmp）再生をサポートし，トップ画面の秒速起動、低遅延などの優位性、解像度のシームレスな切り替え、CSSタイムシフトなどの高度な機能を備えています。

このプレーヤーはSuperPlayerのFlutterプラグインを基にしており、AndroidおよびiOSの両プラットフォームを同時にサポートしています。完全に無料のオープンソースであり、再生アドレスソースに対する制限がないので、安心してご使用いただけます。

## SDKのダウンロード

Tencent Cloud View Cube Flutter Super Playerのプロジェクトアドレスは、[SuperPlayer Flutter](https://github.com/tencentyun/SuperPlayer/tree/main/Flutter)です。 

## 対象となる読者

このドキュメントの内容の一部は、Tencent Cloud専用の機能となっていますので、使用前に、[Tencent Cloud](https://cloud.tencent.com)関連サービスのアクティブ化を行ってください。アカウント登録がないユーザーは登録し、[無料試用](https://intl.cloud.tencent.com/login)が可能です。

## 統合ガイド[](id:Guide)

1. `pubspec.yaml`に設定を追加します。
```yaml
  super_player:
    git:
      url: https://github.com/tencentyun/SuperPlayer
      path: Flutter
```

2. 依存パッケージの更新
```yaml
   flutter pub upgrade
```
4. ネイティブの設定を追加します。

### Android設定[](id:Android_config)

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

AndroidはネイティブPlayer+に依存しています。ディレクトリの`example/android/superplayerkit`フォルダをプロジェクトディレクトリにコピーし、`setings.gradle`に`include ':superplayerkit'`を挿入します。もちろん、公式サイトで適切なバージョンを検索してインポートすることもできます。

### iOSの設定[](id:iOS_config)

iOSの`Info.plist`に次の設定を追加します。
```xml
    <key>NSAppTransportSecurity</key>
    <dict>
        <key>NSAllowsArbitraryLoads</key>
        <true/>
    </dict>
```

iOSは`pod`方式をネイティブに使用して依存するため、`podfile`ファイルを編集して、プレーヤーのバージョンを指定します。
```xml
pod 'SuperPlayer/Player', '3.3.9'
```

バージョンを指定しない場合は、デフォルトで最新の`SuperPlayer`がインストールされます。

### Flutterでの呼び出し[](id:Flutter_call)

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'dart:async';
import 'package:super_player/super_player.dart';

class TestSuperPlayer extends StatefulWidget {
  @override
  _TestSuperPlayerState createState() => _TestSuperPlayerState();
}

class _TestSuperPlayerState extends State<TestSuperPlayer> {

  SuperPlayerViewConfig _playerConfig;
  SuperPlayerViewModel _playerModel;
  SuperPlayerPlatformViewController _playerController;
  String _url = "http://liteavapp.qcloud.com/live/liteavdemoplayerstreamid_demo1080p.flv";
  int _appId = 0;
  String _fileId = "";

  @override
  void initState() {
    // TODO: implement initState
    super.initState();
    _playerConfig = SuperPlayerViewConfig();
    _playerModel = SuperPlayerViewModel();
    _playerModel.videoURL = _url;
  }

 @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
            ackgroundColor: Colors.blueGrey,
            title: const Text('SuperPlayer'),
        ),
        body: Builder(
        builder: (context) =>
        SafeArea(
            child: Container(
            color: Colors.blueGrey,
            child: Column(
                children: [
                AspectRatio(
                    aspectRatio: 16.0/9.0,
                    child:SuperPlayerVideo(
                        onCreated: (SuperPlayerPlatformViewController vc) {
                            _playerController = vc;
                            await _playerController.setPlayConfig(_playerConfig);
                            await _playerController.playWithModel(_playerModel);// 再生を開始
                        },
                    )
                ),
                ],
            ),
            ),
        )
        ),
    );
  }

```



## プレーヤーの使用[](id:usePlayer)

プレーヤーのメインクラスは、`SuperPlayerVideo`です。作成後すぐにビデオを再生できます。

```dart
  void initState() {
    // TODO: implement initState
    super.initState();
    _playerConfig = SuperPlayerViewConfig();
    _playerModel = SuperPlayerViewModel();
    _playerModel.videoURL = _url;
  }
```

```dart
@override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
            ackgroundColor: Colors.blueGrey,
            title: const Text('SuperPlayer'),
        ),
        body: Builder(
            builder: (context) =>
                SafeArea(
                    child: Container(
                        color: Colors.blueGrey,
                        child: Column(
                            children: [
                                AspectRatio(
                                    aspectRatio: 16.0/9.0,
                                    child:SuperPlayerVideo(
                                        onCreated: (SuperPlayerPlatformViewController vc) {
                                            _playerController = vc;
                                            await _playerController.setPlayConfig(_playerConfig);
                                            await _playerController.playWithModel(_playerModel);// 再生を開始
                                        },
                                    )
                                ),
                            ],
                        ),
                    ),
                )
        ),
    );
  }
```

コードを実行すると、携帯電話で再生したビデオを視聴でき、インターフェース上の機能もほとんどが使用可能な状態になります。



## 複数の解像度[](id:resolution)

上述のサンプルコードは解像度が1種類のみですが、複数の解像度を追加したい場合もとても簡単です。例えば、ライブストリーミングでは、[CSSコンソール](https://console.cloud.tencent.com/live/livemanage)を開き、再生したいCSSストリームを探して、詳細に移動します。


ここに各種解像度、形式の再生アドレスがあります。FLVアドレスを使用して再生することをお勧めします。コードは次のとおりです

```dart
  void initState() {
    // TODO: implement initState
    super.initState();
    _playerConfig = SuperPlayerViewConfig();
    _playerModel = SuperPlayerViewModel();
    SuperPlayerUrl url1 = SuperPlayerUrl();
    url1.title = "FHD";
    url1.url = "http://5815.liveplay.myqcloud.com/live/5815_89aad37e06ff11e892905cb9018cf0d4.flv";

    SuperPlayerUrl url2 = SuperPlayerUrl();
    url2.title = "FHD";
    url2.url = "http://5815.liveplay.myqcloud.com/live/5815_89aad37e06ff11e892905cb9018cf0d4.flv";

    SuperPlayerUrl url3 = SuperPlayerUrl();
    url3.title = "FHD";
    url3.url = "http://5815.liveplay.myqcloud.com/live/5815_89aad37e06ff11e892905cb9018cf0d4.flv";

    _playerModel.multiVideoURLs = [url1, url2, url3];
    _playerModel.videoURL = url1.url;// デフォルトの再生解像度を設定
  }
```

```dart
@override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Colors.blueGrey,
        title: const Text('SuperPlayer'),
      ),
      body: Builder(
        builder: (context) =>
        SafeArea(
          child: Container(
            color: Colors.blueGrey,
            child: Column(
              children: [
                AspectRatio(
                    aspectRatio: 16.0/9.0,
                    child:SuperPlayerVideo(
                      onCreated: (SuperPlayerPlatformViewController vc) async {
                        _playerController = vc;
                        await _playerController.setPlayConfig(_playerConfig);
                        await _playerController.playWithModel(_playerModel);// 再生を開始
                      },
                    )
                ),
              ],
            ),
          ),
        )
      ),
    );
  }

```

プレーヤーでこれら複数の解像度を確認することができ、クリックすれば、すぐに切り替えることができます。



## タイムシフト再生[](id:timeShift)

プレーヤーのタイムシフトを有効にするのはとても簡単で、再生前にappIdを設定するだけです。

```dart
SuperPlayerViewModel playModel = SuperPlayerViewModel();
playModel.appId = 1252463788;// ここでappIDに変更
```

>?appIdを【Tencent Cloudコンソール】>【[アカウント情報](https://console.cloud.tencent.com/developer)】で表示します。

再生中のCSSストリームは下のプログレスバーで確認できます。ドラッグすれば指定の位置まで戻ることができ、【ライブストリーミングに戻る】をクリックすれば最新のCSSストリームを視聴することができます。



>?タイムシフト機能はパブリックベータテスト申請フェーズにあり、必要に応じて[チケットを提出](https://console.cloud.tencent.com/workorder)し、使用を申請することができます。

## FileId再生
解像度の設定にurlを入力するよりも、さらに簡単な使用方法がfileIdを使用して再生する方法です。fileIdは、通常、ビデオのアップロード後にサーバーから返されます。
1. クライアントからビデオが公開されると、サーバーがfileIdをクライアントに返します。
2. サーバーからのビデオアップロード時、アップロード確認の通知に対応するfileIdが含まれています。


ファイルがすでにTencent Cloudに存在する場合は、[メディア資産管理](https://console.cloud.tencent.com/vod/media)にアクセスし、対応するファイルを検索することができます。クリックして、右側のビデオ詳細でappIdとfileIdを確認することができます。


再生fileIdのコードは次のとおりです。

```dart
SuperPlayerViewModel playModel = SuperPlayerViewModel();
playModel.appId = 1252463788;// ここでappIDに変更
SuperPlayerVideoId videoId = SuperPlayerVideoId();
videoId.fileId = "4564972819219071679";
playModel.videoId = videoId;

_playerController.playWithModel(playModel);
```

ビデオがアップロードされると、バックグランドで自動的にトランスコードされます（すべてのトランスコード形式については、[トランスコードテンプレート](https://console.cloud.tencent.com/vod/video-process/template)）をご参照ください。トランスコード完了後、プレーヤーは複数の解像度を自動的に表示します。

## その他の機能[](id:moreFeature)

完全な機能は、2次元コードをスキャニングし、ビデオクラウドツールキットをダウンロードして体験するか、またはプログラムのDemoを直接実行することもできます。
<img src="https://main.qcloudimg.com/raw/6790ddaf4ffe4afd0ceb96b309a16496.png" width="150">
