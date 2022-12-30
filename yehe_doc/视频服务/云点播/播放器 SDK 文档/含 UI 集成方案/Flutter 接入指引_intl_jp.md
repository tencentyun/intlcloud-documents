## SDKのダウンロード

Tencent Cloud View Cube Flutter Player SDKのアドレスは、[Player Flutter](https://github.com/LiteAVSDK/Player_Flutter/tree/main/Flutter)です。

## 対象となる読者

このドキュメントの内容の一部は、Tencent Cloud専用の機能となっていますので、使用前に、[Tencent Cloud](https://intl.cloud.tencent.com/) 関連サービスのアクティブ化を行ってください。アカウント登録がないユーザーは登録し、[無料試用](https://intl.cloud.tencent.com/login)が可能です。

## このドキュメントから把握できること

* Tencent Cloud View Cube Flutter Player SDKの統合方法
* プレーヤーコンポーネントを使用したVOD再生方法

## プレーヤーコンポーネントの概要

FlutterプレーヤーコンポーネントはFlutter Player SDKをベースにして拡張したものです。プレーヤーコンポーネントはVODプレーヤーにより多くの機能を統合し、その機能には全画面切り替え、解像度切り替え、
プログレスバー、再生制御、カバータイトル表示などの一般的な機能が含まれ、VODプレーヤーを使用する場合に比べてより便利になっています。より便利かつスピーディーにFlutterのビデオ再生機能を統合したい場合はFlutterプレーヤーコンポーネントを選択できます。

サポート機能リスト：

- 全画面再生

- 再生中画面自動回転

- カスタムビデオカバー

- 解像度切り替え

- 音声および明るさ調整

- 倍速再生

- ハードウェアアクセラレーションオン/オフ

- ピクチャーインピクチャー（PIP）（AndroidおよびiOSプラットフォームでサポート）

- スプライトイメージおよびキーフレームキーモーメント情報

  その他にもさまざまな機能を開発中です

## 統合ガイド[](id:Guide)

1. プロジェクトのexampleにある`superplayer`ディレクトリをご自身のFlutterプロジェクトにコピーします
2. 次のように、使用したいページに`superplayer`の依存パッケージをインポートします
```dart
import 'superplayer/demo_superplayer_lib.dart';
```

## SDKの統合[](id:stepone)

### ステップ1：ビデオ再生機能Licenseおよび統合の申請[](id:step1)

プレーヤーを統合する前に、[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/login)が必要です。登録完了後、ビデオ再生機能Licenseを申請し、次の方式で統合します。アプリケーション起動時に行うことをお勧めします。

Licenseを統合していない場合、再生中に異常が発生することがあります。

```dart
String licenceURL = ""; // 取得したlicence url
String licenｃeKey = ""; // 取得したlicence key
SuperPlayerPlugin.setGlobalLicense(licenceURL, licenceKey);
```

### ステップ2：SDKへのアクセス環境の設定

お客様がより高品質かつ安全でコンプライアンスに則ったビジネスを展開し、各国・地域の規制の要求事項を満たすよう、Tencent Cloudは2つのSDKアクセス環境を提供します。グローバルユーザにサービスを提供している場合、以下のインターフェースでグローバルアクセス環境を設定することをお勧めします。

```dart
SuperPlayerPlugin.setGlobalEnv("GDPR");
```

### ステップ3：controllerの作成[](id:step2)

```dart
SuperPlayerController _controller = SuperPlayerController(context);
```

### ステップ4：プレーヤーの設定[](id:step3)

```dart
FTXVodPlayConfig config = FTXVodPlayConfig();
// preferredResolutionを設定しない場合、マルチビットレートビデオの再生時に解像度720 * 1280のビットレートを優先的に再生します
config.preferredResolution = 720 * 1280;
_controller.setPlayConfig(config);
```

FTXVodPlayConfigの詳細設定はFlutter VODプレーヤーの設定プレーヤーインターフェースを参照できます。

### ステップ5：イベント監視の設定[](id:step4)

```dart
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
```

### ステップ6：レイアウトの追加[](id:step5)

```dart
Widget _getPlayArea() {
    return Container(
    height: 220,
    child: SuperPlayerView(_controller),
  );
}
```

### ステップ7：リターンイベント監視の追加[](id:step6)

リターンイベント監視を追加し、ユーザーがリターンイベントをトリガーした際に、プレーヤーが全画面などの状態にある場合は全画面を優先的に終了し、再度トリガーされて初めてページを終了するようにします。
**全画面再生状態から直接ページを終了したい場合、この監視は実装しなくてもかまいません**

```dart
  @override
Widget build(BuildContext context) {
  return WillPopScope(
      child: Container(
        decoration: BoxDecoration(
            image: DecorationImage(
              image: AssetImage("images/ic_new_vod_bg.png"),
              fit: BoxFit.cover,
            )),
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
```

### ステップ8：再生開始[](id:step7)
<dx-tabs>
::: url方式による方法
```dart
SuperPlayerModel model = SuperPlayerModel();
model.videoURL = "http://1400329073.vod2.myqcloud.com/d62d88a7vodtranscq1400329073/59c68fe75285890800381567412/adp.10.m3u8";
_controller.playWithModelNeedLicence(model);
```
:::

::: fileId方式
```dart
SuperPlayerModel model = SuperPlayerModel();
model.appId = 1500005830;
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "8602268011437356984";
// psignはプレーヤーの署名です。署名についての紹介および生成方法は、以下のリンクをご参照ください。https://www.tencentcloud.com/document/product/266/38099
model.videoId.pSign = "psignXXX"
_controller.playWithModelNeedLicence(model);
```

[メディア資産管理](https://console.cloud.tencent.com/vod/media)で該当するファイルをさがして、ファイル名の下でFileIdを確認できます。

FileId方式で再生する場合、プレーヤーはバックグラウンドに実際の再生アドレスをリクエストします。この時点でネットワークに異常がある場合やFileIdが存在しない場合は、SuperPlayerViewEvent.onSuperPlayerErrorイベントを受信します

:::
</dx-tabs>


### ステップ9：再生終了[](id:step8)

再生終了時、特に次回のstartVodPlayを行う前には、**controllerの破棄メソッドの呼び出しを忘れずに行ってください**。この操作を行わない場合、大量のメモリリークや画面のちらつきといった問題が発生します。また、ページを終了する際、ビデオ再生を確実に終了できるようにしてください。
```dart
  @override
void dispose() {
  // must invoke when page exit.
  _controller.releasePlayer();
  super.dispose();
}
```

## プレーヤーコンポーネントインターフェースリスト[](id:sdkList)

### 1、ビデオ再生

**注意**

バージョン10.7より、startPlayはstartVodPlayに変更され、正常に再生を行うには{@link SuperPlayerPlugin#setGlobalLicense}でのLicenceの設定が必要になりました。これを行わなければ再生が失敗します（ブラックスクリーン）。設定はグローバルで1回行うだけです。ライブストリーミングLicence、UGSV Licenceおよびビデオ再生Licenceがすべて使用できます。上記のLicenceをまだ取得していない場合は、[テスト版Licenceを無料でクイック申請](https://www.tencentcloud.com/document/product/266/51098)すれば正常に再生できますが、正式版Licenseは[購入](https://www.tencentcloud.com/document/product/266/51098#.E8.B4.AD.E4.B9.B0.E5.B9.B6.E6.96.B0.E5.BB.BA.E6.AD.A3.E5.BC.8F.E7.89.88-license)する必要があります。

**説明**

ビデオ再生を開始します。

**インターフェース**

```dart
_controller.playWithModelNeedLicence(model);
```

**パラメータの説明**

1. SuperPlayerModel

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| appId | int | アプリケーションappId。fileId再生の場合は入力必須 |
| videoURL | String | ビデオurl。url再生の場合は入力必須 |
| multiVideoURLs | List<String> | マルチビットレートurl。マルチビットレートurl再生の場合は入力必須 |
| defaultPlayIndex | int | デフォルトの再生ビットレート番号。multiVideoURLsと合わせて使用します |
| videoId | SuperPlayerVideoId | fileIdストレージオブジェクト。以下で詳しく説明します |
| title | String | ビデオタイトル。ユーザーはこのフィールドを設定することでタイトルをカスタマイズし、プレーヤー内部のサーバーからリクエストされたタイトルを上書きすることができます |
| coverUrl | String | Tencentサーバーからプルするカバー画像。この値はSuperVodDataLoaderから自動的に割り当てられます |
| customeCoverUrl | String | カスタムビデオカバー。このフィールドは優先的に判断され、このパラメータを定義することでカスタムカバーを実装できます |
| duration | int | ビデオの長さ。単位：秒 |
| videoDescription | String | ビデオの説明 |
| videoMoreDescription | String | ビデオの詳細説明 |
| playAction | int | actionにはPLAY_ACTION_AUTO_PLAY、PLAY_ACTION_MANUAL_PLAYおよびPLAY_ACTION_PRELOADが含まれます。パラメータの意味については以下で詳しく説明します |

2. SuperPlayerVideoId

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| fileId | String | ファイルid。入力必須 |
| psign | String | プレーヤー署名。署名の説明と生成方法。 |

3. playAction

 -  PLAY_ACTION_AUTO_PLAY : playWithModelを呼び出すと、ビデオの再生を自動的に開始します。
 -  PLAY_ACTION_MANUAL_PLAY : playWithModelを呼び出した後、手動で再生する必要があり、かつプレーヤーは実際にビデオをロードせず、カバー画像を表示するだけです。PLAY_ACTION_PRELOADと異なり、ビデオ再生リソースは何も消費しません。
 -  PLAY_ACTION_PRELOAD : playWithModelを呼び出すと、カバー画像を表示し、ビデオの再生は開始しませんが、プレーヤーは実際にはビデオをロードしています。PLAY_ACTION_MANUAL_PLAYと比べて再生開始速度が速いです。

### 2、再生の一時停止

**説明**

ビデオ再生を一時停止します

**インターフェース**

```dart
_controller.pause();
```

### 3、再生の継続

**説明**

ビデオ再生を継続します

**インターフェース**

```dart
_controller.resume();
```
### 4、再生再開

**説明**

ビデオ再生を再開します

**インターフェース**

```dart
_controller.reStart();
```

### 5、プレーヤーのリセット

**説明**

プレーヤーの状態をリセットし、ビデオの再生を停止します

**インターフェース**

```dart
_controller.resetPlayer();
```

### 6、プレーヤーの解放

**説明**

プレーヤーリソースを解放し、再生を停止します。このメソッドを呼び出すと、controllerは再利用できなくなります

**インターフェース**

```dart
_controller.releasePlayer();
```

### 7、プレーヤーのリターンイベント

**説明**

プレーヤーリターンイベントがトリガーされた際、このメソッドは主に全画面再生モードでの「戻る」の判断および処理に用いられます。trueを返す : 全画面終了などの操作を実行し、リターンイベントを消費します。  false：イベントを消費していません

**インターフェース**

```dart
_controller.onBackPress();
```

### 8、解像度切り替え

**説明**

現在再生中のビデオの解像度をリアルタイムに切り替えます

**インターフェース**

```dart
_controller.switchStream(videoQuality);
```

**パラメータの説明**

videoQualityは再生開始後、通常_controller.currentQualiyListおよび_controller.currentQualityによって取得できます。前者は解像度のリスト、後者はデフォルトの解像度です。**解像度切り替え機能はSuper Playerにすでに統合されています。全画面に切り替えた後、右下隅の解像度をクリックして切り替えることができます。**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| index | int | 解像度番号 |
| bitrate | int | 解像度ビットレート |
| width | int | この解像度でのビデオの幅 |
| height | int | この解像度でのビデオの高さ |
| name | String | 解像度の略称 |
| title | String | 表示に用いる解像度名 |
| url | String | 解像度url。マルチビットレートの場合に用いるurlです。任意入力 |

### 9、進捗の調整(seek)

**説明**

現在のビデオの再生進行状況を調整します

**インターフェース**

```dart
_controller.seek(progress);
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| progress | double | 調整したい時間。単位：秒 |

### 10、Super Playerの設定

**説明**

Super Playerを設定します

**インターフェース**

```dart
_controller.setPlayConfig(config);
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| connectRetryCount | int | プレーヤーの再接続回数。SDKとサーバーの接続が異常によって切断された場合、SDKはサーバーとの再接続を試行します。この値によってSDKの再接続回数を設定します |
| connectRetryInterval | int | プレーヤーの再接続間隔。SDKとサーバーの接続が異常によって切断された場合、SDKはサーバーとの再接続を試行します。この値によって2回の再接続間隔時間を設定します |
| timeout | int | プレーヤーの接続タイムアウト時間 |
| playerType | int | プレーヤータイプ。0 VOD、1 ライブストリーミング、2 ライブストリーミングプレイバック |
| headers | Map | カスタムhttp headers |
| enableAccurateSeek | bool | 正確にseekするかどうか。デフォルトではtrueです |
| autoRotate | bool | mp4ファイルを再生する際、trueに設定すると、ファイル内の回転角度に応じて自動的に回転します。回転角度はPLAY_EVT_CHANGE_ROTATIONイベントから取得できます。デフォルトではtrueです |
| smoothSwitchBitrate | bool | マルチビットレートHLSのスムーズな切り替え。デフォルトではfalseです。falseに設定すると、マルチビットレートアドレスを開く速度が速くなります。trueに設定すると、IDRが合っている場合にビットレートをスムーズに切り替えることができます |
| cacheMp4ExtName | String | mp4キャッシュファイルの拡張子。デフォルトではmp4です |
| progressInterval | int | プログレスコールバック間隔を設定します。設定しない場合、SDKはデフォルトで0.5秒ごとに1回コールバックを行います。単位はミリ秒|
| maxBufferSize | int | 最大再生バッファサイズ（単位：MB） 。この設定はplayableDurationに影響します。設定値が大きいほど事前キャッシュが多くなります|
| maxPreloadSize | int | プリロードの最大バッファサイズ（単位：MB） |
| firstStartPlayBufferTime | int | 最初のバッファリングでロードする必要があるデータ時間（単位：ms）。デフォルト値は100ms|
| nextStartPlayBufferTime | int | バッファ時（バッファデータが不十分であることによる二次バッファ、またはseekによるドラッグバッファ）に少なくともどのくらいのデータをキャッシュするとバッファを終了できるかです（単位：ms）。デフォルト値は250ms|
| overlayKey | String | HLSセキュリティ強化暗号化/復号key|
| overlayIv | String | HLSセキュリティ強化暗号化/復号Iv|
| extInfoMap | Map | 周知する必要がないいくつかの特別な設定|
| enableRenderProcess | bool | ロード後にレンダリングの後処理サービスを許可するかどうかです。デフォルトでは有効です。有効化後に解像度プラグインが存在した場合は、デフォルトでロードします|
| preferredResolution | int | 優先的に再生する解像度。preferredResolution = width * height|

### 11、ハードウェアデコードの有効化/無効化

**説明**

ハードウェアデコード再生機能を有効化または無効化します

**インターフェース**

```dart
_controller.enableHardwareDecode(enable);
```

### 12、再生状態の取得

**説明**

現在のプレーヤーの再生状態を取得します

**インターフェース**

```dart
SuperPlayerState superPlayerState = _controller.getPlayerState();
```

**パラメータの説明**

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| INIT | SuperPlayerState | 初期状態 |
| PLAYING | SuperPlayerState | 再生中 |
| PAUSE | SuperPlayerState | 一時停止中 |
| LOADING | SuperPlayerState | バッファ中 |
| END | SuperPlayerState | 再生終了 |

### 13、ピクチャーインピクチャーモードに進む

**説明**

このメソッドを呼び出すと、ビデオはピクチャーインピクチャーモードに進みます。このモードはandroid 7.0以上で、かつピクチャーインピクチャーモードをサポートしているモデルでのみサポートしています

**インターフェース**

```dart
_controller.enterPictureInPictureMode(
backIcon: "images/ic_pip_play_replay.png",
playIcon: "images/ic_pip_play_normal.png",
pauseIcon: "images/ic_pip_play_pause.png",
forwardIcon: "images/ic_pip_play_forward.png");
```

**パラメータの説明**

このパラメータはandroidプラットフォームにのみ適用可能です

| パラメータ名      | タイプ   | 説明             |
| ------ | ------ | ------------------ |
| backIcon | String | 戻るボタンアイコン。androidプラットフォームの制限により、アイコンのサイズは1M以下となります。渡さなくてもよく、その場合はシステム付属のアイコンを使用します |
| playIcon | String | 再生ボタンアイコン。androidプラットフォームの制限により、アイコンのサイズは1M以下となります。渡さなくてもよく、その場合はシステム付属のアイコンを使用します |
| pauseIcon | String | 一時停止ボタンアイコン。androidプラットフォームの制限により、アイコンのサイズは1M以下となります。渡さなくてもよく、その場合はシステム付属のアイコンを使用します |
| forwardIcon | String | 早送りボタンアイコン。androidプラットフォームの制限により、アイコンのサイズは1M以下となります。渡さなくてもよく、その場合はシステム付属のアイコンを使用します |

## イベント通知

### 1、再生状態の監視

**説明**

ビデオ再生の状態、パッケージ化後の状態の変化を監視します

**コード**

```dart
_playController.onPlayStateBroadcast.listen((event) {
  SuperPlayerState state = event['event'];
});
```

**イベントの説明**

イベントは列挙クラスSuperPlayerStateによって渡されます

| ステータス | 意味               |
| ------ |------------------ |
| INIT | 初期状態 |
| PLAYING | 再生中 |
| PAUSE | 一時停止中 |
| LOADING  | バッファ中 |
| END | 再生終了 |

### 2、再生イベントの監視

**説明**

プレーヤーの操作イベントを監視します

**コード**

```dart
_controller.onSimplePlayerEventBroadcast.listen((event) {
    String evtName = event["event"];
    if (evtName == SuperPlayerViewEvent.onStartFullScreenPlay) {
        setState(() {
        _ isFullScreen = true;
        });
    } else if (evtName == SuperPlayerViewEvent.onStopFullScreenPlay) {
        setState(() {
          _isFullScreen = false;
        });
    }else{
        print(evtName);
    }
});
```

**イベントの説明**


| ステータス | 意味               |
| ------ |------------------ |
| onStartFullScreenPlay | 全画面再生の開始 |
| onStopFullScreenPlay | 全画面再生の終了 |
| onSuperPlayerDidStart | 再生開始の通知 |
| onSuperPlayerDidEnd  | 再生終了の通知 |
| onSuperPlayerError | 再生エラーの通知 |
| onSuperPlayerBackAction | リターンイベント |

## 高度な機能

### 1、fileIdによるビデオデータの事前リクエスト

SuperVodDataLoaderによってビデオデータを事前にリクエストすることで、再生開始速度を速めることができます

**コード例**

```dart
SuperPlayerModel model = SuperPlayerModel();
model.appId = 1500005830;
model.videoId = new SuperPlayerVideoId();
model.videoId.fileId = "8602268011437356984";
model.title = "VOD";
SuperVodDataLoader loader = SuperVodDataLoader();
// model内の必要なパラメータはSuperVodDataLoaderで直接割り当てます
loader.getVideoData(model, (resultModel) {
  _controller.playWithModelNeedLicence(resultModel);
})
```


### 2、ピクチャーインピクチャーモードの使用

#### 1、Androidプラットフォームの設定

1.1 自身のプロジェクトのandroidパッケージでAndroidManifest.xmlを見つけ、プロジェクトのエントリーactivityノードに以下の設定を追加します

```xml
android:supportsPictureInPicture="true"
android:resizeableActivity="true"
android:configChanges="screenSize|smallestScreenSize|screenLayout|orientation"

// 自身のプロジェクトのandroidパッケージでbuild.graldeを見つけ、compileSdkVersionおよびtargetSdkVersionのバージョンが31以上であることを確認します
```

1.2 pip activityの継承

githubプロジェクトのexample/android内のFTXFlutterPipActivity.javaを自身のエントリーActivityの同ディレクトリ下にコピーし、自身のActivityの親クラスをこのクラスに変更します。

#### 2、iOSプラットフォームの設定
   2.1 自身のプロジェクトのtarget下でSigning & Capabilitiesを選択してBackground Modesを追加し、Audio,AirPlay,and Picture in Pictureにチェックを入れます。

#### 3、superPlayerサンプルコードのコピー

githubプロジェクトのexample/lib内のsuperplayerパッケージを自身のlibディレクトリ下にコピーし、サンプルコード内のdemo_superplayer.dartを参照してSuper Playerを統合します。
そうするとSuper Playerの再生画面右側中央にピクチャーインピクチャーモードのボタンが現れ、クリックしてピクチャーインピクチャーモードに進むことができます。

#### 4、ピクチャーインピクチャーモードのライフサイクルの監視

SuperPlayerPluginのonExtraEventBroadcastを使用すると、ピクチャーインピクチャーモードのライフサイクルを監視することができます。サンプルコードは次のとおりです

```dart
SuperPlayerPlugin.instance.onExtraEventBroadcast.listen((event) {
  int eventCode = event["event"];
  if (eventCode == TXVodPlayEvent.EVENT_PIP_MODE_ALREADY_EXIT) {
    // exit pip mode
  } else if (eventCode == TXVodPlayEvent.EVENT_PIP_MODE_REQUEST_START) {
    // enter pip mode
  } else if (eventCode == TXVodPlayEvent.EVENT_PIP_MODE_ALREADY_ENTER) {
    // already enter pip mode
  } else if (eventCode == TXVodPlayEvent.EVENT_IOS_PIP_MODE_WILL_EXIT) {
    // will exit pip mode
  } else if (eventCode == TXVodPlayEvent.EVENT_IOS_PIP_MODE_RESTORE_UI) {
    // restore UI only support iOS
  } 
});
```

#### 5、ピクチャーインピクチャーモード開始エラーコード

ピクチャーインピクチャーモードに進むのに失敗した場合、ログプロンプトのほかにtoastプロンプトも表示され、superplayer_widget.dartの_onEnterPipModeメソッド内でエラー状態の修正処理を行うことができます。エラーコードの意味は次のとおりです。

| パラメータ名 | 値   | 説明               |
| ------ | ------ | ------------------ |
| NO_ERROR | 0 | 起動に成功しました。エラーはありません |
| ERROR_PIP_LOWER_VERSION | -101 | androidのバージョンが低すぎ、ピクチャーインピクチャーモードをサポートしていません |
| ERROR_PIP_DENIED_PERMISSION | -102 | ピクチャーインピクチャーモードの権限が有効になっていないか、または現在のデバイスがピクチャーインピクチャーをサポートしていません |
| ERROR_PIP_ACTIVITY_DESTROYED | -103 | 現在の画面がすでに破棄されています |
| ERROR_IOS_PIP_DEVICE_NOT_SUPPORT | -104 | デバイスまたはシステムバージョンがサポートされていません（PIPはiPad iOS9以降でサポート） | only support iOS|
| ERROR_IOS_PIP_PLAYER_NOT_SUPPORT | -105 | プレーヤーをサポートしていません | only support iOS|
| ERROR_IOS_PIP_VIDEO_NOT_SUPPORT | -106 | ビデオをサポートしていません | only support iOS|
| ERROR_IOS_PIP_IS_NOT_POSSIBLE | -107 | PIPコントローラは利用できません | only support iOS|
| ERROR_IOS_PIP_FROM_SYSTEM | -108 | PIPコントローラエラー | only support iOS|
| ERROR_IOS_PIP_PLAYER_NOT_EXIST | -109 | プレーヤーオブジェクトが存在しません | only support iOS|
| ERROR_IOS_PIP_IS_RUNNING | -110 | PIP機能はすでに実行されています | only support iOS|
| ERROR_IOS_PIP_NOT_RUNNING | -111 | PIP機能は起動していません | only support iOS|

#### 6、現在のデバイスがピクチャーインピクチャーをサポートしているかどうかの判断

現在のデバイスでピクチャーインピクチャーを有効にできるかどうかは、SuperPlayerPluginのisDeviceSupportPipを使用して判断できます。コードの例は次のとおりです

```dart
int result = await SuperPlayerPlugin.isDeviceSupportPip();
if(result == TXVodPlayEvent.NO_ERROR) {
  // pip support
}
```

resultの返す結果の意味はピクチャーインピクチャーモードのエラーコードと一致しています。
