## 対象となる読者

このドキュメントの内容の一部は、Tencent Cloud専用の機能となっていますので、使用前に、[Tencent Cloud](https://intl.cloud.tencent.com/) 関連サービスのアクティブ化を行ってください。アカウント登録がないユーザーは登録し、[無料試用](https://intl.cloud.tencent.com/login)が可能です。

## このドキュメントから把握できること
* Tencent Cloud View Cube Flutter Player SDKの統合方法
* プレーヤーSDKを使ったオンデマンド再生の方法
* プレーヤーSDKの基盤となる機能を使用したり多くの機能の実現方法

## 基礎知識
ここでは、主にビデオクラウドSDKのオンデマンド再生機能についてご説明します。その前に、役立つ基本知識についていくつかご紹介します。

- **ライブストリーミングとオンデマンド**
  ライブストリーミング（LIVE）のビデオソースはキャスターがリアルタイムにプッシュします。このため、キャスターがプッシュを停止すれば、再生側の画面もそれに伴って停止します。また、リアルタイムなライブストリーミングのため、プレーヤーでライブストリーミングURLを再生する際にプログレスバーは表示されません。

オンデマンド（VOD）のビデオソースはクラウドのビデオファイルで、クラウド側から削除されない限り、ビデオは随時再生することができます。再生中はプログレスバーで再生位置をコントロールできます。典型的なオンデマンドのケースには、Tencent VideoやYouku Tudouなどの動画サイト上のビデオ視聴があります。

- **プロトコルのサポート**
  通常使用するオンデマンドプロトコルは次のとおりです。現在比較的主流なのはHLS（「http」で始まり「.m3u8」で終わる）オンデマンドアドレスです。
  ![](https://qcloudimg.tencent-cloud.cn/raw/5143d2e31ddbdcb77294fa72b045abb2.jpeg)

## 特記事項
ビデオクラウドSDKには**再生アドレスのソースに対する制限はありません**。つまり、再生アドレスがTencent Cloudのものであってもなくても再生が可能です。ただし、ビデオクラウドSDKのプレーヤーがサポートしているのはFLV、RTMP、HLS（m3u8）の3種類の形式のライブストリーミングアドレスと、MP4、HLS（m3u8）、FLVの3種類の形式のオンデマンドアドレスのみです。

## SDKの統合[](id:stepone)

### ステップ1：SDK開発キットの統合[](id:step1)

SDK開発キットをダウンロードして統合します。

### ステップ2：controllerの作成[](id:step2)

```dart
TXVodPlayerController _controller = TXVodPlayerController();
```

### ステップ3：イベント監視の設定[](id:step3)

```dart
// ビデオの幅と高さの変化を監視します。適切な幅と高さの比率を設定します。幅と高さの比率はカスタム設定も可能で、ビデオのテクスチャも比率に応じて引き伸ばされます
_controller.onPlayerNetStatusBroadcast.listen((event) async {
  double w = (event["VIDEO_WIDTH"]).toDouble();
  double h = (event["VIDEO_HEIGHT"]).toDouble();

  if (w > 0 && h > 0) {
    setState(() {
      _aspectRatio = 1.0 * w / h;
    });
  }
});
```

### ステップ4：レイアウトの追加[](id:step4)
```dart
@override
Widget build(BuildContext context) {
return Container(
  decoration: BoxDecoration(
      image: DecorationImage(
        image: AssetImage("images/ic_new_vod_bg.png"),
        fit: BoxFit.cover,
      )),
  child: Scaffold(
      backgroundColor: Colors.transparent,
      appBar: AppBar(
        backgroundColor: Colors.transparent,
        title: const Text('VOD'),
      ),
      body: SafeArea(
          child: Container(
            height: 150,
            color: Colors.black,
            child: Center(
              child: _aspectRatio > 0
                  ? AspectRatio(
                aspectRatio: _aspectRatio,
                child: TXPlayerVideo(controller: _controller),
              ) : Container(),
            ),
          ))));
}
```

### ステップ5：プレーヤーの初期化[](id:step5)

```dart
// プレーヤーを初期化し、共有テクスチャを割り当てます
await _controller.initialize();
```

### ステップ6：再生開始[](id:step6)
<dx-tabs>
::: url方式による方法
TXVodPlayerControllerは内部で自動的に再生プロトコルを認識しますので、再生URLをstartVodPlay関数に渡すだけで完了です。
```dart
// ビデオリソースを再生します
String _url =
    "http://1400329073.vod2.myqcloud.com/d62d88a7vodtranscq1400329073/59c68fe75285890800381567412/adp.10.m3u8";
await _controller.startVodPlay(_url);
```
:::
::: fileld方式による方法
```dart
// psignはプレーヤーの署名です。署名についての紹介および生成方法は、以下のリンクをご参照ください。https://www.tencentcloud.com/document/product/266/38099
TXPlayInfoParams params = TXPlayInfoParams(appId: 1252463788,
        fileId: "4564972819220421305", psign: "psignxxxxxxx");
await _controller.startVodPlayWithParams(params);
```
[メディア資産管理](https://console.cloud.tencent.com/vod/media)で該当するファイルをさがして、ファイル名の下でFileIdを確認できます。

FileId方式で再生すると、プレーヤーはリアルな再生アドレスをバックグラウンドにリクエストします。この時点でネットワークに異常が発生した場合、またはFileIdが存在しない場合は、`TXLiveConstants.PLAY_ERR_GET_PLAYINFO_FAIL`イベントが受信されます。そうでない場合は、リクエストが成功したことを示す`TXLiveConstants.PLAY_EVT_GET_PLAYINFO_SUCC`を受信します。
:::
</dx-tabs>


### ステップ7：再生終了[](id:step7)
再生終了時、特に次回のstartVodPlayを行う前には、**controllerの破棄メソッドの呼び出しを忘れずに行ってください**。この操作を行わない場合、大量のメモリリークや画面のちらつきといった問題が発生します。
```dart
@override
void dispose() {
  _controller.dispose();
  super.dispose();
}
```

## 基本機能の使用

### 1、再生コントロール

#### 再生の開始

```dart
// 再生の開始
_controller.startVodPlay(url)
```

#### 再生の一時停止

```dart
// 再生の一時停止
_controller.pause();
```

#### 再生の再開

```dart
// 再生の再開
_controller.resume();
```

#### 再生の終了

```dart
// 再生の終了
_controller.stopPlay(true);
```

#### プレーヤーの終了

```dart
// controllerの解放
_controller.dispose();
```

#### 再生位置の調整(Seek)

ユーザーが再生バーをドラッグすると、seekを呼び出して指定された位置から再生を開始することができ、プレーヤーSDKは正確なseekをサポートします。

```dart
double time = 600; // double。単位は秒です
/// 再生位置の調整
_controller.seek(time);
```

#### 指定された時間から再生します

startVodPlayを最初に呼び出す前は、指定した時間からの再生がサポートされています。

```dart
float startTimeInSecond = 60; // 単位は秒です
_controller.setStartTime(startTimeInSecond);   // 再生開始時間の設定
_controller.startVodPlay(url);
```

### 2、速度を変えて再生します

VODプレーヤーは可変速再生をサポートしています。インターフェース`setRate`を使用してオンデマンド再生速度を設定します。0.5X、1.0X、1.2X、2Xなどの高速再生と低速再生をサポートしています。

```dart
// 1.2倍の再生速度を設定します
_controller.setRate(1.2); 
```

### 3、ループ再生

```dart
// ループ再生の設定
_controller.setLoop(true);
// 現在のループ再生状態を取得します
_controller.isLoop(); 
```

### 4、ミュート設定

```dart
// ミュートを設定します。ミュートをオンにする場合はtrue、ミュートをオフにする場合はfalse
_controller.setMute(true);
```

### 5、ロール画像広告

プレーヤーSDKは、広告宣伝などのためにインターフェースにピクチャを挿入することをサポートします。実現方式は次のとおりです：

* `autoPlay'をNOにすると、プレーヤーは正常にロードされますが、ビデオはすぐに再生を開始しません。
* ビデオはプレーヤーでロードされた後、再生が開始されていない間は、プレーヤーのインターフェースで画像広告が表示されます。
* 広告表示終了条件が満たされたら、resumeインターフェースを使用してビデオ再生を開始します。
```dart
_controller.setAutoPlay(false);  // 自動再生しないように設定します
_controller.startVodPlay(url);    // startVodPlayを呼び出すとビデオがロードされますが、ロードが成功しても自動的に再生されるわけではありません
// ......
// プレーヤー画面に広告を表示します
// ......  
_controller.resume();  // 広告表示後、resumeを呼び出してビデオ再生を開始します
```

### 8、HTTP-REF

TXVodPlayConfigのheadersは、URLがあちこちにコピーされないようにするよく使われているRefererフィールド（Tencent Cloudは、より安全な署名の盗難防止用チェーンスキームを提供します）や、クライアントのID情報を検証するためのCookieフィールドなど、HTTPリクエストヘッダを設定するために使用されます。

```dart
FTXVodPlayConfig playConfig = FTXVodPlayConfig();
Map<String, String> httpHeaders = {'Referer': 'Referer Content'};
playConfig.headers = httpHeaders;
_controller.setConfig(playConfig);
```

### 9、ハードウェア・アクセラレーション

ブルーレイ（1080p）レベルの画質については、単にソフトウェアデコードを使用してスムーズな再生体験を得るのが難しいので、ゲームのライブ配信を中心としたシーンでは、ハードウェア・アクセラレーションをオンにすることをお勧めします。

ソフトウェアデコードとハードウェアデコードを切り替えるには、切り替える前に**stopPlay**、切り替えた後に**startVodPlay**を行う必要があります。この操作をしない場合、より深刻な画面の揺れや歪みといった問題が発生します。

```dart
 _controller.stopPlay(true);
 _controller.enableHardwareDecode(true); 
 _controller.startVodPlay(url);
```

### 10、シャープネスの設定

SDKはHLSのマルチビットレート形式をサポートしており、ユーザーは異なるビットレートの再生ストリームを簡単に切り替えることができ、シャープネスの異なる再生を実現することができます。PLAY_EVT_PLAY_BEGINイベントを受信した後に、以下の方法でシャープネスを設定することができます。

```dart
List _supportedBitrates = (await _controller.getSupportedBitrates())!;; //マルチビットレート配列を取得します
int index = _supportedBitrates[i];  // 再生するビットレートの添え字を指定します
_controller.setBitrateIndex(index);  // ビットレートを希望の解像度に切り替えます
```

再生中は、`_controller.setBitrateIndex(int)`を通じていつでもビットレートを切り替えることができます。切り替え中、別のストリームのデータを再度プルします。SDKは、Tencent Cloudのマルチビットレートファイルに最適化されているため、ラグが発生することなく切り替えが可能です。

### 11、アダプティブビットレートストリーミング

SDKはHLSのアダプティブビットレートストリーミングをサポートし、関連機能をオンにすると、プレーヤーは現在の帯域幅に最適なビットレートを動的に選択して再生することができます。PLAY_EVT_PLAY_BEGINイベントを受信した後、以下の方法でアダプティブビットレートストリーミングをオンにすることができます。

```dart
_controller.setBitrateIndex(-1); //indexパラメータは-1で渡されます
```

再生中はいつでも`_controller.setBitrateIndex(int)`で別のビットレートに切り替えることができ、切り替えた後はビットレートストリーミングアダプティブはオフになります。

### 12、ビットレートのスムーズな切り替えの有効化

再生を開始する前に、ビットレートのスムーズな切り替えを有効化し、再生中にビットレートを切り替えることで、解像度のシームレスな切り替えが可能になります。ビットレートのスムーズな切り替えを無効にしている場合と比べて、切り替えの過程でやや時間がかかりますが、より良好な体験が得られます。ニーズに応じて設定することができます。

```dart
FTXVodPlayConfig playConfig = FTXVodPlayConfig();
/// trueに設定すると、ビットレートをスムーズに切り替えることができます。falseに設定すると、マルチビットレートアドレスを開く速度が速くなります
playConfig.smoothSwitchBitrate = true;
_controller.setConfig(playConfig);
```

###13、再生位置のリスニング

VOD再生中の進捗情報には、**ロード進捗**と**再生進捗**という2種類があります。現在、SDKはこれら2つの進捗をイベント通知という形でリアルタイムに通知しています。

プレーヤーのイベントは`onPlayerEventBroadcast`インターフェースを通じて監視します。進捗通知は**PLAY_EVT_PLAY_PROGRESS**イベントを通じてアプリケーションにコールバックされます。

```dart
_controller.onPlayerEventBroadcast.listen((event) async {
  if(event["event"] == TXVodPlayEvent.PLAY_EVT_PLAY_PROGRESS) {// その他の詳細についてはiOSまたはAndroidネイティブSDKのステータスコードをご参照ください
    // 再生可能時間、すなわちロードの進行状況です。単位はミリ秒
    double playableDuration = event[TXVodPlayEvent.EVT_PLAYABLE_DURATION_MS].toDouble();
    // 再生の進行状況です。単位は秒
    int progress = event[TXVodPlayEvent.EVT_PLAY_PROGRESS].toInt();
    // ビデオ合計時間です。単位は秒
    int duration = event[TXVodPlayEvent.EVT_PLAY_DURATION].toInt();
  }
});
```

### 14、再生ネットワーク速度のリスニング

`onPlayerNetStatusBroadcast`インターフェースを通じてプレーヤーのネットワーク状態を監視します（例： `NET_STATUS_NET_SPEED`）。

```dart
_controller.onPlayerNetStatusBroadcast.listen((event) {
	(event[TXVodNetEvent.NET_STATUS_NET_SPEED]).toDouble();
});
```

### 15、ビデオ解像度の取得

Player SDKはURL文字列を介してビデオを再生します。URLそのものにはビデオ情報は含まれません。関連情報を取得するには、クラウドサーバーにアクセスしてビデオ情報をロードする必要があるため、SDKはビデオ情報をイベント通知としてのみお客様のアプリケーションに送信します。

**解像度情報は次の2つの方法で取得できます**

方法1：`onPlayerNetStatusBroadcast`の`NET_STATUS_VIDEO_WIDTH`と`NET_STATUS_VIDEO_HEIGHT`により、ビデオの幅と高さを取得します

方法2：プレーヤーからPLAY_EVT_VOD_PLAY_PREPAREDイベントコールバックを受信した後、`getWidth()`と`getHeight()`を直接呼び出して現在の幅と高さを取得します。

```dart
 _controller.onPlayerNetStatusBroadcast.listen((event) {
  double w = (event[TXVodNetEvent.NET_STATUS_VIDEO_WIDTH]).toDouble();
  double h = (event[TXVodNetEvent.NET_STATUS_VIDEO_HEIGHT]).toDouble();
});

// ビデオの幅を取得します。プレーヤーからPLAY_EVT_VOD_PLAY_PREPAREDイベントがコールバックされた後に値を返します
_controller.getWidth();
_controller.getHeight();
```

### 16、再生バッファサイズ

通常の映像再生時にネットワークから予めバッファリングされる最大データサイズをコントロールします。設定されていない場合は、スムーズな再生を確保するため、プレーヤーのデフォルトのバッファポリシーが適用されます。

```dart
FTXVodPlayConfig playConfig = FTXVodPlayConfig();
playConfig.maxBufferSize = 10;  ///  再生時の最大バッファサイズです。単位：MB
_controller.setConfig(playConfig);
```

### 17、ビデオのローカルキャッシュ[](id：cache)

短いビデオ再生シーンでは、ビデオファイルのローカルキャッシュは非常に必要な機能であり、一般的なユーザーにとっては、一度見たビデオを再視聴するときに、もう1度トラフィックを消費しないでください。

- **対応形式：**SDKは、一般的なオンデマンド形式であるHLS (m3u8)およびMP4の2つのキャッシュ機能をサポートしています。
- **オンにするタイミング：**SDKでは、デフォルトでキャッシュ機能がオンにされません。また、ユーザのレビュー率が高くないシーンでは、この機能をオンにすることを推奨するものでもありません。
- **オンにする方式：**グローバルに有効になり、プレーヤーを使用するときにオンになります。この機能をオンにするには、ローカルキャッシュディレクトリとキャッシュサイズの2つのパラメータを設定してください。

```dart
//再生エンジンのグローバルキャッシュディレクトリとキャッシュサイズを設定します（//単位MB）
SuperPlayerPlugin.setGlobalMaxCacheSize(200);
//再生エンジンのグローバルキャッシュディレクトリを設定します
SuperPlayerPlugin.setGlobalCacheFolderPath("postfixPath");
```

## 高級機能使用

### 1、ビデオのプリプレイ

#### ステップ1：ビデオプリプレイの使用

短いビデオ再生シーンでは、ビデオのプリプレイ機能がスムーズな再生に役立ちます。現在のビデオを再生している間に、次のビデオをバックグラウンドでロードします。これにより、ユーザーが実際に次のビデオに切り替えたときに、最初からロードする必要はなくなり、すぐに再生することが可能になります。

ビデオをプリプレイすると、素早い再生の効果が得られますが、パフォーマンスのオーバーヘッドが必要です。業務で同時にビデオをプリロードする必要がある場合は、[ビデオのプリダウンロード](#download)と組み合わせて使用することをお勧めします。

これは、ビデオ再生中のシームレスな切り替えを後押しする技術で、TXVodPlayerControllerのsetAutoPlayスイッチを使ってこの機能を実装することができます。具体的な方法は、以下のとおりです。
<img src="https://qcloudimg.tencent-cloud.cn/raw/b2bd645f29af403bf2740156aee44092.jpg" width=700px>

```dart
// ビデオAの再生：autoPlayがtrueに設定されている場合、startVodPlayの呼び出しにより、直ちにビデオのロードと再生が開始されます
String urlA = "http://1252463788.vod2.myqcloud.com/xxxxx/v.f10.mp4";
controller.setAutoPlay(isAutoPlay: true);
controller.startVodPlay(urlA);

// ビデオAを再生しながら、setAutoPlayをfalseに設定してビデオBをプリロードします
String urlB = "http://1252463788.vod2.myqcloud.com/xxxxx/v.f20.mp4";
controller.setAutoPlay(isAutoPlay: false);
controller.startVodPlay(urlB); // すぐに再生を開始せず、ビデオのロードのみを開始します
```

ビデオAの再生が終了し、自動的に（あるいはユーザーが手動で）ビデオBに切り替えたときに、resume関数を呼び出すとすぐに再生できます。

>! autoPlayがfalseに設定されている場合、resumeを呼び出す前に、ビデオBの準備が完了していることを確認する必要があります。つまり、ビデオBのPLAY_EVT_VOD_PLAY_PREPARED（2013。プレーヤー準備が完了し、再生可能になりました）イベントを受信した後に呼び出されます。


```dart
controller.onPlayerEventBroadcast.listen((event) async {//サブスクリプション状態の変化
  if(event["event"] == TXVodPlayEvent.PLAY_EVT_PLAY_END) {
    await _controller_A.stop();
    await _controller_B.resume();
  }
});
```

#### ステップ2：ビデオプリプレイのバッファー設定

- バッファを大きく設定することで、ネットワークの揺らぎに対応し、スムーズな再生を実現することができます。
- バッファを小さく設定すると、トラフィックの消費を抑えることができます。 

##### プリプレイバッファサイズ

このインターフェースは、プリロードシーン（ビデオの再生開始前で、playerのAutoPlayがfalseに設定されている場合）で、再生開始前の段階での最大バッファサイズを制御するために使用されます。

```dart
TXVodPlayConfig config = new TXVodPlayConfig();
config.setMaxPreloadSize(2);  // プリプレイ時の最大バッファサイズ。単位：MB。業務状況に応じてトラフィックを節約するように設定します
mVodPlayer.setConfig(config);  // configをmVodPlayerに渡します
```

##### プリプレイバッファサイズ 

通常の映像再生時にネットワークから予めバッファリングされる最大データサイズをコントロールします。設定されていない場合は、スムーズな再生を確保するため、プレーヤーのデフォルトのバッファポリシーが適用されます。

```dart
FTXVodPlayConfig config = FTXVodPlayConfig();
config.maxBufferSize = 10; // 再生時の最大バッファサイズです。単位はMBです。
_controller.setPlayConfig(config); // configをcontrollerに渡します
```

[](id:download)

### 2、動画のプリダウンロード

プレーヤーのインスタンスを作成する必要がなく、ビデオの一部のコンテンツを事前にダウンロードすると、プレーヤを使用するときに、ビデオの再生開始速度が速くなり、より良い再生体験を提供できます。

再生サービスを使用する前に、[ビデオキャッシュ](#cache)が設定されていることを確認してください。

ユースケース：

```dart
//再生エンジンのグローバルキャッシュディレクトリとキャッシュサイズを設定します
SuperPlayerPlugin.setGlobalMaxCacheSize(200);
// このキャッシュパスはデフォルトではappサンドボックスのディレクトリ下に設定されます。postfixPathは対応するキャッシュディレクトリのものを渡すだけでよく、絶対パス全体を渡す必要はありません。
// Androidプラットフォーム：ビデオはsdcardのAndroid/data/your-pkg-name/files/testCacheディレクトリにキャッシュされます。 
// iOSプラットフォーム：ビデオはサンドボックスのDocuments/testCacheディレクトリにキャッシュされます。
SuperPlayerPlugin.setGlobalCacheFolderPath("postfixPath");

String palyrl = "http://****";
//プレダウンロードの開始
int taskId = await TXVodDownloadController.instance.startPreLoad(palyrl, 3, 1920*1080,
  onCompleteListener:(int taskId,String url) {
    print('taskID=${taskId} ,url=${url}');
  }, onErrorListener: (int taskId, String url, int code, String msg) {
    print('taskID=${taskId} ,url=${url}, code=${code} , msg=${msg}');
  } 
);

//事前ダウンロードをキャンセルします
TXVodDownloadController.instance.stopPreLoad(taskId);
```

### 3. 動画のダウンロード

ビデオのダウンロードは、ネットワークが存在する状態でビデオをダウンロードし、そしてネットワークが存在しない環境で視聴することをサポートします。また、プレーヤーSDKはローカル暗号化能力を提供しており、ダウンロード後のローカルビデオは暗号化されたままであり、ビデオの復号化と再生には指定されたプレーヤーが必要であり、ダウンロード後のビデオの違法な伝播を効果的に防止し、ビデオの安全を保護することができます。

HLSストリームメディアはローカルに直接保存できないため、ローカルファイルの再生によってHLSをローカルにダウンロードして再生することはできません。この問題については、`TXVodDownloadController`ベースのビデオダウンロード方式によって、HLSをオフラインで再生することが可能です。
>?
> -  `TXVodDownloadController`は現時点ではMP4とFLV形式のファイルのキャッシュをサポートしておらず、非ネストのHLS形式ファイルのみサポートしています。
> -  Player SDKは、MP4およびFLV形式のローカルファイルの再生をサポートしています。

[](id:offline1)

#### ステップ1：準備作業

`TXVodDownloadController`は単一のインスタンスとして設計されているので、複数のダウンロードオブジェクトを作成することはできません。使い方は以下のとおりです。

```dart
// このキャッシュパスはデフォルトではappサンドボックスのディレクトリ下に設定されます。postfixPathは対応するキャッシュディレクトリのものを渡すだけでよく、絶対パス全体を渡す必要はありません。
// Androidプラットフォーム：ビデオはsdcardのAndroid/data/your-pkg-name/files/testCacheディレクトリにキャッシュされます。 
// iOSプラットフォーム：ビデオはサンドボックスのDocuments/testCacheディレクトリにキャッシュされます。
SuperPlayerPlugin.setGlobalCacheFolderPath("postfixPath");
```

[](id:offline2)

#### ステップ2:  ダウンロードの開始

ダウンロードの開始方法としては、[Fileid](#fileid)と[URL](#url)という2種類の方法があります。具体的な操作については以下のとおりです。
<dx-tabs>

::: Fileid方式[](id:fileid)
Fileidのダウンロードには、少なくともAppID、Fileid、qualityIdを渡してください。署名付きビデオはpSignを渡してください。userNameが具体的な値を渡さない場合、デフォルトで「default」になります。

>!暗号化されたビデオの場合はFileidによるダウンロードのみ可能です。psignパラメータは必ず入力しなければなりません。

```dart
// QUALITY_OD // オリジナル画像
// QUALITY_FLU // LD
// QUALITY_SD  // SD
// QUALITY_HD  // HD

TXVodDownloadMedialnfo medialnfo = TXVodDownloadMedialnfo();
TXVodDownloadDataSource dataSource = TXVodDownloadDataSource();
dataSource.appId = 1252463788;
dataSource.fileId = "4564972819220421305";
dataSource.quality = DownloadQuality.QUALITY_HD;
dataSource.pSign = "pSignxxxx";
medialnfo.dataSource = dataSource;
TXVodDownloadController.instance.startDonwload(medialnfo);
```
:::

::: URL方式[](id:url)
少なくともダウンロードアドレスのURLを渡す必要があります。ネストしたHLS形式はサポートしておらず、シングルビットストリームのHLSのダウンロードのみサポートしています。userNameは具体的な値が渡されない場合、デフォルトで「default」となります。

```dart
TXVodDownloadMedialnfo medialnfo = TXVodDownloadMedialnfo();
medialnfo.url = "http://1500005830.vod2.myqcloud.com/43843ec0vodtranscq1500005830/00eb06a88602268011437356984/video_10_0.m3u8";
TXVodDownloadController.instance.startDonwload(medialnfo);
```

:::

</dx-tabs>


[](id:offline3)

#### ステップ3：タスク情報 

タスク情報を受信する前に、コールバックlistenerを設定してください。

```dart
TXVodDownloadController.instance.setDownloadObserver((event, info) {

}, (errorCode, errorMsg, info) {

});
```

受信する可能性のあるタスクイベントには次のものがあります。

| イベント                                                  | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| EVENT_DOWNLOAD_START       | タスクの開始。SDKがダウンロードを開始したことを表します                              |
| EVENT_DOWNLOAD_PROGRESS    | タスクの進行状況。ダウンロード中、SDKはこのインターフェースを頻繁にコールバックします。`mediaInfo.getProgress()`で現在の進捗を取得できます |
| EVENT_DOWNLOAD_STOP        | タスクの停止。`stopDownload`を呼び出してダウンロードを停止した際、このメッセージを受信すると停止に成功したことを表します |
| EVENT_DOWNLOAD_FINISH      | ダウンロードの完了。このコールバックを受信すると、すべてのダウンロードが完了したことを意味します。この時点で、ダウンロードしたファイルはTXVodPlayerで再生することができます |


downlodOnErrorListenerメソッドがコールバックされた場合はダウンロードエラーを表します。ダウンロード中にネットワークが切断されると、このインターフェースがコールバックされ、同時にダウンロードタスクが停止します。

downloaderは複数のタスクを同時にダウンロードできるので、コールバックインターフェースには`TXVodDownloadMediaInfo`オブジェクトが含まれます。URLやdataSourceにアクセスしてダウンロード元を特定したり、ダウンロードの進捗やファイルサイズなどの情報を取得したりできます。

[](id:offline4)

#### ステップ4：ダウンロードの中断

ダウンロードを停止するには、`TXVodDownloadController.instance.stopDownload()`メソッドを呼び出してください。パラメータはダウンロードの開始時に渡された`TXVodDownloadMedialnfo`オブジェクトです。**SDKは、中断からの再開をサポート**しています。ダウンロードディレクトリが変更されていない場合、同じファイルの次のダウンロードは最後に停止したところから再び開始されます。

#### ステップ5：ダウンロード管理

すべてのユーザーアカウントのダウンロードリスト情報と、指定されたユーザーアカウントのダウンロードリスト情報を取得できます。

```dart
// すべてのユーザーのダウンロードリスト情報を取得します
// アクセス側は、ダウンロード情報内のuserNameに基づいて、各ユーザーのダウンロードリスト情報を区別することができます
List<TXVodDownloadMedialnfo> downloadInfoList = await TXVodDownloadController.instance.getDownloadList();
```

現在のダウンロードステータスを含むFileid関連のダウンロード情報を取得し、現在のダウンロードの進行状況を取得して、ダウンロードが完了したかどうかを判断するには、AppID、Fileid、qualityIdを渡してください。

```dart
// 特定のビデオに関連するダウンロード情報を取得します
TXVodDownloadMedialnfo downloadInfo = await TXVodDownloadController.instance.getDownloadInfo(medialnfo);
int? duration = downloadInfo.duration;	// 合計時間を取得します
int? playableDuration = downloadInfo.playableDuration; // ダウンロード済みの再生可能時間を取得します
double? progress = downloadInfo.progress;	// ダウンロード進行状況を取得します
String? playPath = downloadInfo.playPath; // オフライン再生パスを取得し、プレーヤーに渡すことでオフライン再生が可能になります
int? downloadState = downloadInfo.downloadState; // ダウンロードステータスを取得します。詳細については、STATE_xxx定数をご参照ください
```

```dart
// ダウンロード情報の削除
bool result = await TXVodDownloadController.instance.deleteDownloadMediaInfo(medialnfo);
```

### 4、暗号化して再生します

ビデオ暗号化方式は、主にeラーニングなど、ビデオの著作権保護が必要なシナリオで使用されています。ビデオリソースを暗号化する場合、プレーヤーを変更するだけでなく、ビデオソース自体を暗号化・トランスコードする必要があり、バックエンドとエンドポイントという両方の開発エンジニアが関わる必要が出てきます。詳細については、[ビデオ暗号化ソリューション](https://www.tencentcloud.com/document/product/266/38131)をご参照ください。

Tencent CloudコンソールでappId、暗号化されたビデオのfileIdおよびpsignを取得した後、次の方法で再生を行うことができます。

```dart
// psignはプレーヤーの署名です。署名についての紹介および生成方法は、以下のリンクをご参照ください。https://www.tencentcloud.com/document/product/266/38099
TXPlayInfoParams params = TXPlayInfoParams(appId: 1252463788,
        fileId: "4564972819220421305", psign: "psignxxxxxxx");
_controller.startVodPlayWithParams(params);
```

###5、プレーヤーの設定 

startPlayを呼び出す前に、setConfigによってプレーヤーのパラメータを設定することができます。例えば、プレーヤーの接続タイムアウト時間の設定、プログレスコールバック間隔の設定、キャッシュファイル数の設定などです。TXVodPlayConfigがサポートするパラメータの詳細については、[基本設定インターフェース](https://www.tencentcloud.com/document/product/266/47851)をクリックしてご参照ください。使用例は、以下のとおりです。

```dart
FTXVodPlayConfig config = FTXVodPlayConfig();
// preferredResolutionを設定しない場合、マルチビットレートビデオの再生時に解像度720 * 1280のビットレートを優先的に再生します
config.preferredResolution = 720 * 1280;
config.enableAccurateSeek = true;  // 正確にseekするかどうかを設定します。デフォルトではtrueです
config.progressInterval = 200;  // プログレスコールバック間隔を設定します。単位はミリ秒です
config.maxBufferSize = 50;  // 最大プリロードサイズ。単位はMBです
_controller.setPlayConfig(config);
```

##### 再生開始時に解像度を指定します

マルチビットレートのHLSビデオソースを再生します。ビデオストリームの解像度情報を事前に知っていれば、再生開始前に再生するビデオ解像度を優先的に指定することができます。プレーヤーは、好みの解像度以下のストリームを探して再生を開始します。再生後は、setBitrateIndexを使用して必要なビットレートストリームに切り替える必要はありません。

```dart
FTXVodPlayConfig config = FTXVodPlayConfig();
// 入力パラメータは、ビデオの幅と高さの積（幅×高さ）で、カスタム値として渡すことができます。デフォルトでは720 * 1280です
config.preferredResolution = 720 * 1280;
_controller.setPlayConfig(config);
```

##### 再生位置のコールバック間隔を設定します

```dart
FTXVodPlayConfig config = FTXVodPlayConfig();
config.progressInterval = 200;  // プログレスコールバック間隔を設定します。単位はミリ秒です
_controller.setPlayConfig(config);
```

[](id:listening)

## プレーヤーイベント監視

`TXVodPlayerController`の`onPlayerEventBroadcast`を通じてプレーヤーの再生イベントを監視し、それによってアプリケーションに情報を同期させることができます。

### 再生イベント通知（onPlayerEventBroadcast）


| イベントID                                   | 数値  |  意味の説明                                                   |
| ----------------------------------------- | ---- | ---------------------------------------------------------- |
| PLAY\_EVT\_PLAY\_BEGIN                    | 2004 | ビデオ再生の開始                                               |
| PLAY\_EVT\_PLAY\_PROGRESS                 | 2005 | ビデオ再生の進行状況です。現在の再生の進行状況、ロードの進行状況および全体の長さを通知します      |
| PLAY\_EVT\_PLAY\_LOADING                  | 2007 | ビデオ再生をloading中です。再開できれば、その後にLOADING_ENDイベントが発生します |
| PLAY\_EVT\_VOD\_LOADING\_END              | 2014 | ビデオ再生ロードを終了します。ビデオは引き続き再生されます                        |
| VOD_PLAY_EVT_SEEK_COMPLETE | 2019 | Seekの完了です。バージョン10.3からサポートしています                                |

#### 終了イベント

| イベントID                 |    数値  |  意味説明                |
| :---------------------- | :---- | :----------------------------------------------------- |
| PLAY_EVT_PLAY_END       | 2006  | ビデオ再生終了                                           |
| PLAY_ERR_NET_DISCONNECT | -2301 | ネットワーク接続が切断され、何度も再接続しても回復できません。さらにリトライしたければ、手動で再起動後再生してください |
| PLAY_ERR_HLS_KEY        | -2305 | HLS復号キーの取得に失敗しました                                  |

#### 警告イベント

これらのイベントは、SDK内のイベントの一部を知らせるためだけに使用されていますが、気にしなくてもかまいません。

| イベントID                 |    数値  |  意味説明                |
| :-------------------------------- | :--- | :----------------------------------------------------------- |
| PLAY_WARNING_VIDEO_DECODE_FAIL   |  2101  | 現在のビデオフレームのデコードに失敗しました  |
| PLAY_WARNING_AUDIO_DECODE_FAIL   |  2102  | 現在のオーディオフレームのデコードに失敗しました  |
| PLAY_WARNING_RECONNECT            | 2103 | ネットワーク接続が切断され、自動再接続が有効にされています（再接続回数が3回を超えるとPLAY_ERR_NET_DISCONNECTがスローされます） |
| PLAY_WARNING_HW_ACCELERATION_FAIL|  2106  | ハードウェアデコードの開始に失敗しました。ソフトウェアデコードを使用してください   |

#### 接続イベント

サーバー接続イベント。主にサーバー接続時間の測定と統計に使用されます。

| イベントID                 |    数値  |  意味説明                |
| :------------------------- | :--- | :----------------------------------------------------------- |
| PLAY_EVT_VOD_PLAY_PREPARED | 2013 | プレーヤーの再生準備が完了し、再生可能状態です。autoPlayがfalseに設定されている場合、このイベントを受信してからresumeを呼び出すと再生を開始します |
| PLAY_EVT_RCV_FIRST_I_FRAME | 2003 | ネットワークが最初のレンダリング可能なビデオパケット（IDR）を受信しました                      |


#### 画面イベント

次のイベントは、画面の変更情報を取得するために使用されます。

| イベントID                 |    数値  |  意味説明                |
| ----------------------------- | ---- | ---------------- |
| PLAY\_EVT\_CHANGE\_RESOLUTION | 2009 | ビデオ解像度の変更   |
| PLAY\_EVT\_CHANGE\_ROTATION   | 2011 | MP4 ビデオ回転角度 |

#### ビデオ情報イベント

| イベントID                 |    数値  |  意味説明                |
| :----------------------------------------- | :--- | :------------------- |
| PLAY_EVT_GET_PLAYINFO_SUCC | 2010 | 再生ファイル情報の取得に成功しました |

fileId方式によって再生し、リクエストが成功した場合（インターフェース：startVodPlay(TXPlayerAuthBuilder authBuilder)）、SDKはいくつかの情報を上位レイヤーに通知します。`TXLiveConstants.PLAY_EVT_GET_PLAYINFO_SUCC`イベントを受信後、paramを解析することでビデオ情報を取得できます。

|  ビデオ情報                                    | 意味の説明                                        |
| ------------------------------------------- | ------------------------------------------------- |
| EVT\_PLAY\_COVER\_URL                       | ビデオカバーアドレス                                   |
| EVT\_PLAY\_URL                              | ビデオ再生アドレス                                   |
| EVT\_PLAY\_DURATION                         | ビデオ時間                                       |
| EVT_TIME                                    | イベント発生時間                                   |
| EVT_UTC_TIME                                | UTC時間                                        |
| EVT_DESCRIPTION                             | イベントの説明                                       |
| EVT_PLAY_NAME                               | ビデオ名                                       |
| EVT_IMAGESPRIT_WEBVTTURL     | スプライトイメージweb vtt説明ファイルのダウンロードURLです。バージョン10.2以降でサポートしています |
| EVT_IMAGESPRIT_IMAGEURL_LIST | スプライトイメージ画像のダウンロードURLです。バージョン10.2以降でサポートしています               |
| EVT_DRM_TYPE                 | 暗号化タイプです。バージョン10.2以降でサポートしています                        |


onPlayerEventBroadcastによるビデオ再生プロセス情報取得の例：

```dart
_controller.onPlayerEventBroadcast.listen((event) async {
  if (event["event"] == TXVodPlayEvent.PLAY_EVT_PLAY_BEGIN || event["event"] == TXVodPlayEvent.PLAY_EVT_RCV_FIRST_I_FRAME) {
  // code ...
  } else if (event["event"] == TXVodPlayEvent.PLAY_EVT_PLAY_PROGRESS) {
  // code ...
  }
});
```

[](id:status)

### 再生ステータスフィードバック（onPlayerNetStatusBroadcast）

ステータスフィードバックは0.5秒ごとにトリガされ、現在のプッシャ状態をリアルタイムでフィードバックすることを目的としています。これは自動車のダッシュボードのように、現在のSDK内部の特定の状況を知らせることができ、現在のビデオ再生の状態などを理解できるようになります。

<table>
<tr><th>評価パラメータ</th><th>意味説明</th></tr>
<tr>
<td>NET_STATUS_CPU_USAGE</td><td>現在の瞬時CPU使用率</td>
</tr><tr>
<td>NET_STATUS_VIDEO_WIDTH</td><td>ビデオ解像度 - 幅</td>
</tr><tr>
<td>NET_STATUS_VIDEO_HEIGHT</td><td>ビデオ解像度 - 高さ</td>
</tr><tr>
<td>NET_STATUS_NET_SPEED</td><td>現在のネットワークデータの受信速度</td>
</tr><tr>
<td>NET_STATUS_VIDEO_FPS</td><td>現在のストリーミングメディアのビデオフレームレート</td>
</tr><tr>
<td>NET_STATUS_VIDEO_BITRATE</td><td>現在のストリーミングメディアのビデオビットレート（kbps単位）</td>
</tr><tr>
<td>NET_STATUS_AUDIO_BITRATE</td><td>現在のストリーミングメディアのオーディオビットレート（kbps単位）</td>
</tr><tr>
<td>NET_STATUS_VIDEO_CACHE</td><td>バッファ（jitterbuffer）のサイズ。バッファの現在の長さは0であれば、カクカクする可能性が高いことを意味します</td>
</tr><tr>
<td>NET_STATUS_SERVER_IP</td><td>接続されたサーバIP</td>
</tr></table>

onNetStatusからビデオ再生プロセス情報を取得する例：

```dart
_controller.onPlayerNetStatusBroadcast.listen((event) async {
  int videoWidth = event[TXVodNetEvent.NET_STATUS_VIDEO_WIDTH];
});
```


### ビデオ再生ステータスフィードバック

ビデオ再生ステータスは毎回再生ステータスが切り替わるたびに通知されます。

イベントは列挙クラスTXPlayerStateによって渡されます

| ステータス | 意味   |
| ------ | ------ |
| paused | 再生一時停止 |
| failed | 再生失敗 |
| buffering | バッファ中 |
| playing | 再生中 |
| stopped | 再生停止 |
| disposed | コントロール解放 |


onPlayerStateによるビデオ再生ステータス取得の例：

```dart
_controller.onPlayerState.listen((val) { });
```

### システム音量の監視

ビデオ再生音量の監視を便利に行えるようにするため、SDKはflutter層でネイティブ層の音量変化通知に対しイベントパッケージ化を行い、SuperPlayerPluginによって現在のデバイスの音量変化を直接監視できるようにしました。

onEventBroadcastによるデバイス音量ステータス取得の例：

```dart
SuperPlayerPlugin.instance.onEventBroadcast.listen((event) {
  int eventCode = event["event"];
});
```

関連イベントの意味は次のとおりです。

| ステータス | 値 | 意味   |
| ------ |------ | ------ |
| EVENT_VOLUME_CHANGED | 1 | 音量に変化が発生しました |
| EVENT_AUDIO_FOCUS_PAUSE | 2 | 音量出力再生フォーカスが失われました。Androidのみで使用 |
| EVENT_AUDIO_FOCUS_PLAY | 3 | 音量出力フォーカスを取得しました。Androidのみで使用 |

### ピクチャーインピクチャーイベントの監視

SDKの使用するピクチャーインピクチャーはシステムベースで提供されるピクチャーインピクチャー機能であるため、ピクチャーインピクチャーモードに入った後、ユーザーが現在の画面に対しレスポンスの調整を行えるよう、一連の通知を提供しています。

| ステータス | 値 | 意味   |
| ------ |------ | ------ |
| EVENT_PIP_MODE_ALREADY_ENTER | 1 | ピクチャーインピクチャーモードになっています |
| EVENT_PIP_MODE_ALREADY_EXIT | 2 | ピクチャーインピクチャーモードは終了しています |
| EVENT_PIP_MODE_REQUEST_START | 3 | ピクチャーインピクチャーモードに入るためのリクエストを開始します |
| EVENT_PIP_MODE_UI_STATE_CHANGED | 4 | pip UIのステータスに変更が発生しました。android 31以上のみで有効になります |
| EVENT_IOS_PIP_MODE_RESTORE_UI | 5 | UIをリセットしました。IOSのみで有効になります |
| EVENT_IOS_PIP_MODE_WILL_EXIT | 6 | ピクチャーインピクチャーモードを終了します。IOSのみで有効になります |

onExtraEventBroadcastを使用したピクチャーインピクチャーイベントの監視の例は次のとおりです。

```dart
SuperPlayerPlugin.instance.onExtraEventBroadcast.listen((event) {
  int eventCode = event["event"];
});
```
