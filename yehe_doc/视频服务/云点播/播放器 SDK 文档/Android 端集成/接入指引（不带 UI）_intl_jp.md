## 準備作業
1. より完全で包括的なプレーヤー機能を体験するには、[VOD](https://intl.cloud.tencent.com/product/vod)関連サービスを有効化することをお勧めします。未登録のユーザーはアカウントを登録し、[試用](https://intl.cloud.tencent.com/login)できます。VODサービスを使用しない場合は、この手順をスキップできますが、統合後にプレーヤーの基本機能のみを利用できます。
2. Android Studioをダウンロードします。[Android Studio公式サイト](https://developer.android.com/studio)にアクセスし、ダウンロードしてインストールすることができます。すでにダウンロードしている場合は、この手順をスキップできます。

## このドキュメントから把握できること
* Tencent Cloud View Cube Android Player SDKの統合方法
* プレーヤーSDKを使ったオンデマンド再生の方法
* プレーヤーSDKの基盤となる機能を使用したり多くの機能の実現方法

## SDKの統合
[](id:stepone)
### ステップ1：SDK開発キットの統合[](id:step1)

SDK開発キットをダウンロードして統合します。

[](id:addview)

### ステップ2：License権限承認の設定
すでにLicense権限承認を取得している場合は、[Tencent Cloud View Cubeコンソール](https://console.cloud.tencent.com/vcube) にて、License URLおよびLicense Keyを取得する必要があります。


License権限をまだ取得していない場合は、[お問い合わせ](https://intl.cloud.tencent.com/contact-us)を参照し、関連の権限承認を取得する必要があります。

License情報を取得後、SDKの関連インターフェースを呼び出す前に、以下のインターフェースでLicenseを初期化します。Application類で以下の設定を行うことをお勧めします。
```java
public class MApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        String licenceURL = ""; // 取得したlicence url
        String licenｃeKey = ""; // 取得したlicence key
        TXLiveBase.getInstance().setLicence(this, licenceURL, licenceKey);
        TXLiveBase.setListener(new TXLiveBaseListener() {
            @Override
            public void onLicenceLoaded(int result, String reason) {
                Log.i(TAG, "onLicenceLoaded: result:" + result + ", reason:" + reason);
            }
        });
    }
}
```

### ステップ3：Viewの追加
SDKは、デフォルトでビデオレンダリングのためのTXCloudVideoViewが提供されています。最初の手順では、レイアウト用のxmlファイルに次のコードを追加します：
```xml
<com.tencent.rtmp.ui.TXCloudVideoView
            android:id="@+id/video_view"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_centerInParent="true"
            android:visibility="gone"/>
```

[](id:step3)

### ステップ4：Playerの作成

次に、**TXVodPlayer**のオブジェクトを作成し、setPlayerViewインターフェースを使用して、インターフェースに追加したばかりの**video_view**コントロールに関連付けます。

```java
//mPlayerViewはステップ3で追加したビデオレンダリングviewです
TXCloudVideoView mPlayerView = findViewById(R.id.video_view);
//playerオブジェクトを作成します
TXVodPlayer mVodPlayer = new TXVodPlayer(getActivity());
//ビデオレンダリングviewにplayerオブジェクトを関連付けます
mVodPlayer.setPlayerView(mPlayerView);
```

[](id:step4)

### ステップ5：再生を開始

TXVodPlayerは2つの再生モードをサポートしており、必要に応じて選択できます。

<dx-tabs>
::: URL方式
  TXVodPlayerは内部で自動的に再生プロトコルを認識しますので、再生URLをstartVodPlay関数に渡すだけで完了です。

```java
// URLビデオリソースを再生
String url = "http://1252463788.vod2.myqcloud.com/xxxxx/v.f20.mp4";
mVodPlayer.startVodPlay(url); 


// ローカルビデオリソースを再生
String localFile = "/sdcard/video.mp4";
mVodPlayer.startVodPlay(localFile); 
```
:::
::: FileId方式
```objectivec
// 以下の新しいインターフェースの使用をお勧めします
// psignはプレーヤーの署名です。署名についての紹介および生成方法は、以下のリンクをご参照ください。https://www.tencentcloud.com/document/product/266/38099
TXPlayInfoParams playInfoParam = new TXPlayInfoParams(1252463788, // Tencent CloudアカウントのappId
    "4564972819220421305", // ビデオのfileId
    "psignxxxxxxx"); // プレーヤー署名
mVodPlayer.startVodPlay(playInfoParam);

// 古いインターフェースのため、非推奨です
TXPlayerAuthBuilder authBuilder = new TXPlayerAuthBuilder();
authBuilder.setAppId(1252463788);
authBuilder.setFileId("4564972819220421305");
mVodPlayer.startVodPlay(authBuilder); 
```
[メディア資産管理](https://console.cloud.tencent.com/vod/media)で該当するファイルをさがして、ファイル名の下でFileIdを確認できます。

FileId方式で再生すると、プレーヤーはリアルな再生アドレスをバックグラウンドにリクエストします。この時点でネットワークに異常が発生した場合、またはFileIdが存在しない場合は、`TXLiveConstants.PLAY_ERR_GET_PLAYINFO_FAIL`イベントが受信されます。そうでない場合は、リクエストが成功したことを示す`TXLiveConstants.PLAY_EVT_GET_PLAYINFO_SUCC`を受信します。
:::
</dx-tabs>


[](id:5)

### ステップ6：再生の終了

再生終了時、特に次回のstartVodPlayを行う前には、**viewコントロールの破棄**を忘れずに行ってください。この操作を行わない場合、大量のメモリリークや画面のちらつきといった問題が発生します。

また、再生インターフェースを終了する際には、必ずレンダリングViewの`onDestroy()`関数を呼び出すようにしてください。そうしないと、メモリリークや"Receiver not registered"というアラームが発生する可能性があります。

```java
@Override
public void onDestroy() {
    super.onDestroy();
    mVodPlayer.stopPlay(true); //trueは最後のフレームをクリアすることを意味します
    mPlayerView.onDestroy(); 
}
```
>? stopPlayのブール型パラメータには、「最後のフレームをクリアするかどうか」という意味があります。RTMP SDKの以前のバージョンでは、ライブストリーミングプレーヤーにpauseの概念がなかったため、このブール値は最後のフレームのクリアを制御するために使用されます。

オンデマンド再生終了後も最後のフレームの画面を残したい場合は、再生終了イベントを受信してから何もしないで、デフォルトで最後のフレームで停止することができます。

## 基本機能の使用
### 1、再生コントロール

#### 再生の開始

```java
// 再生の開始
mVodPlayer.startVodPlay(url)
```

#### 再生の一時停止

```java
// 再生の一時停止
mVodPlayer.pause();
```

#### 再生の再開

```java
// 再生の再開
mVodPlayer.resume();
```

#### 再生の終了

```java
// 再生の終了
mVodPlayer.stopPlay(true);
```

#### 再生位置の調整(Seek)

ユーザーが再生バーをドラッグすると、seekを呼び出して指定された位置から再生を開始することができ、プレーヤーSDKは正確なseekをサポートします。

```java
int time = 600; // int型の場合、単位を秒とします
// float time = 600; // floatタイプのとき、単位は秒
/// 再生位置の調整
mVodPlayer.seek(time);
```

#### 指定された時間から再生します

startVodPlayを最初に呼び出す前は、指定した時間からの再生がサポートされています。

```java
float startTimeInSecond = 60; // 単位：秒
mVodPlayer.setStartTime(startTimeInSecond);   // 再生開始時間の設定
mVodPlayer.startVodPlay(url);
```

### 2、画面調整

- **view：サイズと位置**
画面のサイズと位置を変更するには、SDK統合時の[Viewを追加](#addview)に追加された「video_view」コントロールのサイズと位置を直接調整してください。

- **setRenderMode：並べて表示または画像のサイズに合わせる**
<table>
<thead>
<tr>
<th>選択可能な値</th>
<th>意味</th>
</tr>
</thead>
<tbody><tr>
<td>RENDER_MODE_FULL_FILL_SCREEN</td>
<td>画像を拡大や縮小せず、画面のいっぱいに広げられ、はみ出した部分が切れます。このモードでは画面に黒い隙間はありませんが、画像の一部が切れて表示されない場合があります</td>
</tr>
<tr>
<td>RENDER_MODE_ADJUST_RESOLUTION</td>
<td>画像の最も長い辺に合わせて縦横の比率を保って拡大・縮小します。拡大・縮小後の幅と高さが表示領域を超えず、中央に表示されます。また画面に黒い隙間が残る場合があります</td>
</tr>
</tbody></table>

- **setRenderRotation：画面回転**
<table>
<thead>
<tr>
<th>選択可能な値</th>
<th>意味</th>
</tr>
</thead>
<tbody><tr>
<td>RENDER_ROTATION_PORTRAIT</td>
<td>通常再生（Homeキーは画面の下にある）</td>
</tr>
<tr>
<td>RENDER_ROTATION_LANDSCAPE</td>
<td>画面を時計回りに270度回転（Homeキーは画面の左にある）</td>
</tr>
</tbody></table>

```java
 // 画像を拡大や縮小せずに画面に広げます
mVodPlayer.setRenderMode(TXLiveConstants.RENDER_MODE_FULL_FILL_SCREEN);
// 通常再生（Homeキーは画面の下にある）
mVodPlayer.setRenderRotation(TXLiveConstants.RENDER_ROTATION_PORTRAIT);
```

### 3、速度を変えて再生します
VODプレーヤーは可変速再生をサポートしています。インターフェース`setRate`を使用してオンデマンド再生速度を設定します。0.5X、1.0X、1.2X、2Xなどの高速再生と低速再生をサポートしています。


```java
// 1.2倍の再生速度を設定します
mVodPlayer.setRate(1.2); 
```

### 4、ループ再生

```java
// ループ再生の設定
mVodPlayer.setLoop(true);
// 現在のループ再生状態を取得します
mVodPlayer.isLoop(); 
```

### 5、ミュート設定

```java
// ミュートを設定します。ミュートをオンにする場合はtrue、ミュートをオフにする場合はfalse
mVodPlayer.setMute(true);
```

### 6、スクリーンショット

**snapshot**を呼び出すことにより、現在のビデオから1つのフレーム画像をキャプチャすることができます。この機能は、現在のライブストリームのビデオ画面のみをキャプチャします。現在のインターフェース全体をキャプチャする必要がある場合は、AndroidのシステムAPIを呼び出してください。

```java
// スクリーンショット
mVodPlayer.snapshot(new ITXSnapshotListener() {
    @Override
    public void onSnapshot(Bitmap bmp) {
        if (null != bmp) {
           //スクリーンショットbitmapとして取得します
        }
    }
});
```


### 7、ピクチャ挿入広告
プレーヤーSDKは、広告宣伝などのためにインターフェースにピクチャを挿入することをサポートします。実現方式は次のとおりです：
* `autoPlay'をNOにすると、プレーヤーは正常にロードされますが、ビデオはすぐに再生を開始しません。
* ビデオはプレーヤーでロードされた後、再生が開始されていない間は、プレーヤーのインターフェースで画像広告が表示されます。
* 広告表示終了条件が満たされたら、resumeインターフェースを使用してビデオ再生を開始します。

```java
mVodPlayer.setAutoPlay(false)mVodPlayer.setAutoPlay(false);  // 自動再生をオフに設定します
mVodPlayer.startVodPlay(url);    // startVodPlayを呼び出すとビデオがロードされますが、ロードが成功しても自動的に再生されるわけではありません
// ......
// プレーヤー画面に広告を表示します
// ......  
mVodPlayer.resume();  // 広告表示が終わったらresumeを呼び出して動画再生を開始します
```

### 8、HTTP-REF
TXVodPlayConfigのheadersは、URLがあちこちにコピーされないようにするよく使われているRefererフィールド（Tencent Cloudは、より安全な署名の盗難防止用チェーンスキームを提供します）や、クライアントのID情報を検証するためのCookieフィールドなど、HTTPリクエストヘッダを設定するために使用されます。

```java
TXVodPlayConfig mPlayConfig = new TXVodPlayConfig();
Map<String, String> headers = new HashMap<>();
headers.put("Referer", "${Refer Content}");
mPlayConfig.setHeaders(headers);
mVodPlayer.setConfig(mPlayConfig);
```

### 9、ハードウェア・アクセラレーション
ブルーレイ（1080p）レベルの画質については、単にソフトウェアデコードを使用してスムーズな再生体験を得るのが難しいので、ゲームのライブ配信を中心としたシーンでは、ハードウェア・アクセラレーションをオンにすることをお勧めします。

ソフトウェアデコードとハードウェアデコードを切り替えるには、切り替える前に**stopPlay**、切り替えた後に**startVodPlay**を行う必要があります。この操作をしない場合、より深刻な画面の揺れや歪みといった問題が発生します。

```java
 mVodPlayer.stopPlay(true);
 mVodPlayer.enableHardwareDecode(true);
 mVodPlayer.startVodPlay(flvUrl, type);
```
### 10、シャープネスの設定
SDKはHLSのマルチビットレート形式をサポートしており、ユーザーは異なるビットレートの再生ストリームを簡単に切り替えることができ、シャープネスの異なる再生を実現することができます。PLAY_EVT_PLAY_BEGINイベントを受信した後に、以下の方法でシャープネスを設定することができます。

```java
ArrayList<TXBitrateItem> bitrates = mVodPlayer.getSupportedBitrates(); //マルチビットレート配列を取得します
int index = bitrates.get(i).index;  // 再生するビットレートの添字を指定します
mVodPlayer.setBitrateIndex(index);  // ビットレートを希望するシャープネスまで切り替えます
```

再生中はいつでも`mVodPlayer.setBitrateIndex(int)`でビットレートを切り替えることができます。切り替えの過程で、別のストリームのデータを再び取得します。SDKはTencent Cloudのマルチビットレートファイル向けに最適化され、ラグなしで切り替えることができます。
### 11、アダプティブビットレートストリーミング
SDKはHLSのアダプティブビットレートストリーミングをサポートし、関連機能をオンにすると、プレーヤーは現在の帯域幅に最適なビットレートを動的に選択して再生することができます。PLAY_EVT_PLAY_BEGINイベントを受信した後、以下の方法でアダプティブビットレートストリーミングをオンにすることができます。
```java
mVodPlayer.setBitrateIndex(-1); //indexパラメータ渡し-1
```
再生中はいつでも`mVodPlayer.setBitrateIndex(int)`で他のビットレートを切り替えることができます。切り替えた後、自動適応もオフにされます。

### 12、ビットレートのスムーズな切り替えの有効化

再生を開始する前に、ビットレートのスムーズな切り替えを有効化し、再生中にビットレートを切り替えることで、解像度のシームレスな切り替えが可能になります。ビットレートのスムーズな切り替えを無効にしている場合と比べて、切り替えの過程でやや時間がかかりますが、より良好な体験が得られます。ニーズに応じて設定することができます。

```java
TXVodPlayConfig mPlayConfig = new TXVodPlayConfig();
// trueに設定すると、IDRが合っている場合にビットレートをスムーズに切り替えることができます。falseに設定すると、マルチビットレートアドレスを開く速度が速くなります
mPlayConfig.setSmoothSwitchBitrate(true); 
mVodPlayer.setConfig(mPlayConfig);
```

###13、再生位置のリスニング

オンデマンド再生位置情報には、**ロードの進行状況**と**再生位置**の2種類があります。SDKでは、この2つの進行状況をイベント通知としてリアルタイムで通知しています。イベント通知の詳細については、[イベントリスニング](#listening)をご参照ください。

TXVodPlayerオブジェクトに**TXVodPlayerListener**リスナーをバインドできます。再生位置通知は**PLAY_EVT_PLAY_PROGRESS**イベントによってアプリケーションにコールバックされます。このイベントの追加情報には、上記の2つの進行状況メトリックが含まれます。



```java
mVodPlayer.setVodListener(new ITXVodPlayListener() {
    @Override
    public void onPlayEvent(TXVodPlayer player, int event, Bundle param) {
        if (event == TXLiveConstants.PLAY_EVT_PLAY_PROGRESS) {
            // ロードの進行状況（ミリ秒単位）
            int playable_duration_ms = param.getInt(TXLiveConstants.EVT_PLAYABLE_DURATION_MS);
            mLoadBar.setProgress(playable_duration_ms); // loadingバーを設定します

            // 再生位置（ミリ秒単位）
            int progress_ms = param.getInt(TXLiveConstants.EVT_PLAY_PROGRESS_MS);
            mSeekBar.setProgress(progress_ms);  // 再生バーを設定します

            // ビデオの長さ（ミリ秒単位）
            int duration_ms = param.getInt(TXLiveConstants.EVT_PLAY_DURATION_MS);
            // 時間表示の設定などに使用されます
        }
    }

    @Override
    public void onNetStatus(TXVodPlayer player, Bundle bundle) {
    }
});
```


### 14、再生ネットワーク速度のリスニング

[イベントリスニング](#listening)を使用すると、ビデオがカクカクするときに現在のネットワーク速度を表示できます。

* 現在のネットワーク速度は`onNetStatus`の`NET_STATUS_NET_SPEED`を使用して取得されます。具体的な使用方法については[ステータスフィードバック(onNetStatus)](#status)をご参照ください。
* `PLAY_EVT_PLAY_LOADING`イベントを受信した後、現在のネットワーク速度を表示します。
* `PLAY_EVT_VOD_LOADING_END`イベントを受信した後、現在のネットワーク速度を表示するviewを非表示にします。

```java
mVodPlayer.setVodListener(new ITXVodPlayListener() {
    @Override
    public void onPlayEvent(TXVodPlayer player, int event, Bundle param) {
        if (event == TXLiveConstants.PLAY_EVT_PLAY_LOADING) {
            // 現在のネットワーク速度を表示

        } else if (event == TXLiveConstants.PLAY_EVT_VOD_LOADING_END) {
            // 現在のネットワーク速度を表示するviewを非表示にします
        }
    }

    @Override
    public void onNetStatus(TXVodPlayer player, Bundle bundle) {
        // リアルタイムレートを取得（単位：kbps）
        int speed = bundle.getInt(TXLiveConstants.NET_STATUS_NET_SPEED);
    }
});
```

### 15、ビデオ解像度の取得

プレーヤーSDKは、URL文字列を通じて映像を再生します。URL自身に映像情報が含まれていません。関連情報を取得するには、クラウド上のサーバーにアクセスして関連ビデオ情報をロードする必要があります。したがって、SDKはイベント通知としてのみビデオ情報をアプリケーションに送信できます。詳細は[イベントリスニング](#listening)をご参照ください。

**解像度情報は次の2つの方法で取得できます**

方法1：`onNetStatus`の`NET_STATUS_VIDEO_WIDTH`と`NET_STATUS_VIDEO_HEIGHT`を通じてビデオの幅と高さを取得します。具体的な使用方法については[ステータスフィードバック(onNetStatus)](#status)をご参照ください。

方法2：プレーヤーからPLAY_EVT_VOD_PLAY_PREPAREDイベントコールバックを受信した後、`TXVodPlayer.getWidth()`と`TXVodPlayer.getHeight()`を直接呼び出して現在の幅と高さを取得します。

```java
mVodPlayer.setVodListener(new ITXVodPlayListener() {
    @Override
    public void onPlayEvent(TXVodPlayer player, int event, Bundle param) {
    }

    @Override
    public void onNetStatus(TXVodPlayer player, Bundle bundle) {
        // ビデオ幅の取得
        int videoWidth = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_WIDTH);
        // ビデオの高さの取得
        int videoHeight = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_HEIGHT);
    }
});

// ビデオの幅を取得します。プレーヤーからPLAY_EVT_VOD_PLAY_PREPAREDイベントがコールバックされた後に値を返します
mVodPlayer.getWidth();
mVodPlayer.getHeight();
```

### 16、再生バッファサイズ

通常の映像再生時にネットワークから予めバッファリングされる最大データサイズをコントロールします。設定されていない場合は、スムーズな再生を確保するため、プレーヤーのデフォルトのバッファポリシーが適用されます。

```java
TXVodPlayConfig config = new TXVodPlayConfig();
config.setMaxBufferSize(10);  // 再生時の最大バッファサイズ。単位：MB
mVodPlayer.setConfig(config);  // configをmVodPlayerに渡します
```

### 17、ビデオのローカルキャッシュ[](id：cache)

短いビデオ再生シーンでは、ビデオファイルのローカルキャッシュは非常に必要な機能であり、一般的なユーザーにとっては、一度見たビデオを再視聴するときに、もう1度トラフィックを消費しないでください。

- **対応形式：**SDKは、一般的なオンデマンド形式であるHLS (m3u8)およびMP4の2つのキャッシュ機能をサポートしています。
- **オンにするタイミング：**SDKでは、デフォルトでキャッシュ機能がオンにされません。また、ユーザのレビュー率が高くないシーンでは、この機能をオンにすることを推奨するものでもありません。
- **オンにする方式：**グローバルに有効になり、プレーヤーを使用するときにオンになります。この機能をオンにするには、ローカルキャッシュディレクトリとキャッシュサイズの2つのパラメータを設定してください。

```java
File sdcardDir = getApplicationContext().getExternalFilesDir(null);
if (sdcardDir != null) {
    //再生エンジンのグローバルキャッシュディレクトリを設定します
   TXPlayerGlobalSetting.setCacheFolderPath(sdcardDir.getPath() + "/txcache");
    //再生エンジンのグローバルキャッシュディレクトリとキャッシュサイズを設定します（//単位MB）
    TXPlayerGlobalSetting.setMaxCacheSize(200); 
}

// プレーヤーの使用
```

>?古いバージョンでは、TXVodPlayConfig#setMaxCacheItemsインターフェースを使用して設定され、すでに廃止されたため、使用は推奨されていません。

## 高級機能使用

### 1、ビデオのプリプレイ

#### ステップ1：ビデオプリプレイの使用

短いビデオ再生シーンでは、ビデオのプリプレイ機能がスムーズな再生に役立ちます。現在のビデオを再生している間に、次のビデオをバックグラウンドでロードします。これにより、ユーザーが実際に次のビデオに切り替えたときに、最初からロードする必要はなくなり、すぐに再生することが可能になります。

ビデオをプリプレイすると、素早い再生の効果が得られますが、パフォーマンスのオーバーヘッドが必要です。業務で同時にビデオをプリロードする必要がある場合は、[ビデオのプリダウンロード](#download)と組み合わせて使用することをお勧めします。

これは、ビデオ再生のシームレスな切り替えを実現するための技術的なサポートですT。XVodPlayerのsetAutoPlayを使用してこの機能を実装できます。具体的な使い方は次のとおりです：
<img src="https://qcloudimg.tencent-cloud.cn/raw/b2bd645f29af403bf2740156aee44092.jpg" style="zoom:67%;" />

```java
// ビデオAの再生：autoPlayがtrueに設定されている場合、startVodPlayの呼び出しにより、直ちにビデオのロードと再生が開始されます
String urlA = "http://1252463788.vod2.myqcloud.com/xxxxx/v.f10.mp4";
playerA.setAutoPlay(true);
playerA.startVodPlay(urlA);

// ビデオAを再生しながら、setAutoPlayをfalseに設定してビデオBをプリロードします
String urlB = @"http://1252463788.vod2.myqcloud.com/xxxxx/v.f20.mp4";
playerB.setAutoPlay(false);
playerB.startVodPlay(urlB); // すぐに再生を開始せず、ビデオのロードのみを開始します
```

ビデオAの再生が終了し、自動的に（あるいはユーザーが手動で）ビデオBに切り替えたときに、resume関数を呼び出すとすぐに再生できます。

>! autoPlayがfalseに設定されている場合、resumeを呼び出す前に、ビデオBの準備が完了していることを確認する必要があります。つまり、ビデオBのPLAY_EVT_VOD_PLAY_PREPARED（2013。プレーヤー準備が完了し、再生可能になりました）イベントを受信した後に呼び出されます。


```java
public void onPlayEvent(TXVodPlayer player, int event, Bundle param) {
    // ビデオAの再生が終了した時点で、ビデオBの再生を直接開始することで、シームレスに切り替えることができます
    if (event == PLAY_EVT_PLAY_END) {
           playerA.stop();
           playerB.setPlayerView(mPlayerView);
           playerB.resume();
        }
}
```

#### ステップ2：ビデオプリプレイのバッファー設定

- バッファを大きく設定することで、ネットワークの揺らぎに対応し、スムーズな再生を実現することができます。
- バッファを小さく設定すると、トラフィックの消費を抑えることができます。 

##### プリプレイバッファサイズ

このインターフェースは、プリロードシーン（ビデオの再生開始前で、playerのAutoPlayがfalseに設定されている場合）で、再生開始前の段階での最大バッファサイズを制御するために使用されます。

```java
TXVodPlayConfig config = new TXVodPlayConfig();
config.setMaxPreloadSize(2);  // プリプレイ時の最大バッファサイズ。単位：MB。業務状況に応じてトラフィックを節約するように設定します
mVodPlayer.setConfig(config);  // configをmVodPlayerに渡します
```

##### プリプレイバッファサイズ 

通常の映像再生時にネットワークから予めバッファリングされる最大データサイズをコントロールします。設定されていない場合は、スムーズな再生を確保するため、プレーヤーのデフォルトのバッファポリシーが適用されます。

```java
TXVodPlayConfig config = new TXVodPlayConfig();
config.setMaxBufferSize(10);  // 再生時の最大バッファサイズ。単位：MB
mVodPlayer.setConfig(config);  // configをmVodPlayerに渡します
```

[](id:download)
### 2、動画のプリダウンロード

プレーヤーのインスタンスを作成する必要がなく、ビデオの一部のコンテンツを事前にダウンロードすると、プレーヤを使用するときに、ビデオの再生開始速度が速くなり、より良い再生体験を提供できます。

再生サービスを使用する前に、[ビデオキャッシュ](#cache)が設定されていることを確認してください。

>? 
> 1. TXPlayerGlobalSettingはグローバルキャッシュ設定インターフェースです。以前のTXVodConfigのキャッシュ設定インターフェースは廃止されています。
> 2.  グローバルキャッシュのディレクトリとサイズの設定は、プレーヤーのTXVodConfigで構成されるキャッシュ設定よりも優先されます。

ユースケース：

```java
//まず再生エンジンのグローバルキャッシュディレクトリとキャッシュサイズを設定します
File sdcardDir = getApplicationContext().getExternalFilesDir(null);
//再生エンジンのグローバルキャッシュディレクトリとキャッシュサイズを設定します
if (sdcardDir != null) {
    TXPlayerGlobalSetting.setCacheFolderPath(sdcardDir.getPath() + "/PlayerCache");
    TXPlayerGlobalSetting.setMaxCacheSize(200); //単位MB
}

String palyrl = "http://****";
//プレダウンロードの開始
final TXVodPreloadManager downloadManager = TXVodPreloadManager.getInstance(getApplicationContext());
final int taskID = downloadManager.startPreload(playUrl, 3, 1920*1080, new ITXVodPreloadListener() {
    @Override
    public void onComplete(int taskID, String url) {
        Log.d(TAG, "preload: onComplete: url: " + url);
    }

    @Override
    public void onError(int taskID, String url, int code, String msg) {
        Log.d(TAG, "preload: onError: url: " + url + ", code: " + code + ", msg: " + msg);
    }

});

//事前ダウンロードをキャンセルします
downloadManager.stopPreload(taskID);
```

### 3. 動画のダウンロード
ビデオのダウンロードは、ネットワークが存在する状態でビデオをダウンロードし、そしてネットワークが存在しない環境で視聴することをサポートします。また、プレーヤーSDKはローカル暗号化能力を提供しており、ダウンロード後のローカルビデオは暗号化されたままであり、ビデオの復号化と再生には指定されたプレーヤーが必要であり、ダウンロード後のビデオの違法な伝播を効果的に防止し、ビデオの安全を保護することができます。

HLSストリーミングメディアはローカルに直接保存できないので、ローカルファイルを再生することでHLSをローカルにダウンロードした後に再生することもできません。この問題については、`TXVodDownloadManager'に基づくビデオダウンロードスキームを使用してHLSのオフライン再生を行うことができます。

>!
>-  `TXVodDownloadManager`は現時点では、MP4とFLV形式のファイルのキャッシュをサポートしておらず、非ネストのHLS形式ファイルのみサポートしています。
> - プレーヤーSDKは、MP4及びFLV形式のローカルファイル再生をサポートしています。

[](id:offline1)
#### ステップ1：準備作業

`TXVodDownloadManager`は単一のインスタンスとして設計されているので、複数のダウンロードオブジェクトを作成することはできません。使い方は次のとおりです：

```java
TXVodDownloadManager downloader = TXVodDownloadManager.getInstance();
downloader.setDownloadPath("<ダウンロードディレクトリを指定>");
```

[](id:offline2)
#### ステップ2:  ダウンロードの開始
ダウンロードの開始方法としては、[Fileid](#fileid)と[URL](#url)という2種類の方法があります。具体的な操作については以下のとおりです。
<dx-tabs>

::: Fileid方式[](id:fileid)
Fileidのダウンロードには、少なくともAppID、Fileid、qualityIdを渡してください。署名付きビデオはpSignを渡してください。userNameが具体的な値を渡さない場合、デフォルトで「default」になります。

**注意：暗号化されたビデオの場合はFileidによるダウンロードのみ可能です。psignパラメータは必ず入力しなければなりません。**

```java
//  QUALITYOD // 元の画質
// QUALITYFLU // 流暢
// QUALITYSD  // 標準画質
// QUALITYHD  // 高画質
TXVodDownloadDataSource source = new TXVodDownloadDataSource(1252463788, "4564972819220421305", QUALITYHD, "pSignxxxx", "");   //pSignは暗号化ビデオの署名です。fileIdを使用してダウンロードする場合は入力必須です
downloader.startDownload(source);
```

:::

::: URL方式[](id:url)
少なくともダウンロードアドレスのURLを渡す必要があります。ネストしたHLS形式はサポートしておらず、シングルビットストリームのHLSのダウンロードのみサポートしています。userNameは具体的な値が渡されない場合、デフォルトで「default」となります。

```java
downloader.startDownloadUrl("http://1500005830.vod2.myqcloud.com/43843ec0vodtranscq1500005830/00eb06a88602268011437356984/video_10_0.m3u8", "");
```
:::

</dx-tabs>


[](id:offline3)
#### ステップ3：タスク情報 
タスク情報を受信する前に、コールバックlistenerを設定してください。

```java
downloader.setListener(this);
```

受信可能なタスクコールバックは次のとおりです：

| コールバック情報 | 説明 |
|---------|---------|
| void onDownloadStart(TXVodDownloadMediaInfo mediaInfo)       | タスクが開始し、SDKのダウンロードが開始されたことを意味します                              |
| void onDownloadProgress(TXVodDownloadMediaInfo mediaInfo)    | タスクの進行状態。ダウンロード中にSDKは頻繁にこのインターフェースをコールバックします。現在の進行状況は`mediaInfo.getProgress()`で取得できます |
| void onDownloadStop(TXVodDownloadMediaInfo mediaInfo)        | タスクが停止しました。`stopDownload`を呼び出してダウンロードを停止して、このメッセージが表示されると、正常に停止したことを意味します |
|  void onDownloadFinish(TXVodDownloadMediaInfo mediaInfo) |  ダウンロード完了です。このコールバックを受信すると、すべてのダウンロードが完了したことを意味します。この時点で、ダウンロードしたファイルはTXVodPlayerで再生できます |
| void onDownloadError(TXVodDownloadMediaInfo mediaInfo, int error, String reason) | ダウンロードエラーです。ダウンロード中にネットワークが切断されると、このインターフェースがコールバックされると同時にダウンロードタスクが停止されます。エラーコードは、`TXVodDownloadManager`にあります|


downloaderは複数のタスクを同時にダウンロードできるので、コールバックインターフェースには`TXVodDownloadMediaInfo`オブジェクトが用意されています。URLやdataSourceにアクセスしてダウンロード元を判断し、同時にダウンロードの進行状況やファイルサイズなどの情報を得ることができます。

[](id:offline4)

#### ステップ4：ダウンロードの中断
ダウンロードを停止するには、`downloader.stopDownload()`メソッドを呼び出してください。パラメータは`downloader.startDownload()`から返されたオブジェクトです。**SDKは一時停止/再開をサポートしています。**ダウンロードディレクトリが変更されていない場合、同じファイルの次回のダウンロードは、前回停止した場所から再開されます。

#### ステップ5：ダウンロード管理
すべてのユーザーアカウントのダウンロードリスト情報と、指定されたユーザーアカウントのダウンロードリスト情報を取得できます。
```java
// すべてのユーザーのダウンロードリスト情報を取得します
// アクセス側は、ダウンロード情報内のuserNameに基づいて、各ユーザーのダウンロードリスト情報を区別することができます
List<TXVodDownloadMediaInfo> downloadInfoList = downloader.getDownloadMediaInfoList(); 
if (downloadInfoList == null || downloadInfoList.size() <= 0) return;
// デフォルトの「default」ユーザーのダウンロードリストを取得します
List<TXVodDownloadMediaInfo> defaultUserDownloadList = new ArrayList<>();
for(TXVodDownloadMediaInfo downloadMediaInfo : downloadInfoList) {
  if ("default".equals(downloadMediaInfo.getUserName())) {
  	defaultUserDownloadList.add(downloadMediaInfo);
  }
}
```

現在のダウンロードステータスを含むFileid関連のダウンロード情報を取得し、現在のダウンロードの進行状況を取得して、ダウンロードが完了したかどうかを判断するには、AppID、Fileid、qualityIdを渡してください。
```java
// fileId関連のダウンロード情報を取得します
TXVodDownloadMediaInfo downloadInfo = downloader.getDownloadMediaInfo(1252463788, "4564972819220421305", QUALITYHD);
// ダウンロードファイルの合計サイズを取得します（単位：Byte）。fileidダウンロードソースについてのみ有効です。
// 備考：合計サイズとはTencent Cloud VODコンソールにアップロードしたオリジナルファイルのサイズを指します。アダプティブビットレートストリーミング変換後のサブストリームのサイズは現時点では取得できません。
int size = downloadInfo.getSize();  // ダウンロードファイルの合計サイズを取得します
int duration = downloadInfo.getDuration();	// 合計使用時間を取得します
int playableDuration = downloadInfo.getPlayableDuration(); // ダウンロードした再生可能時間を取得します
float progress = downloadInfo.getProgress();	// ダウンロードの進行状況を取得します
String playPath = downloadInfo.getPlayPath(); // オフライン再生パスを取得し、プレーヤーに渡すとオフラインで再生できます
int downloadState = downloadInfo.getDownloadState(); // ダウンロードステータスを取得します。具体的にはSTATE_xxx定数をご参照ください
boolean isDownloadFinished = downloadInfo.isDownloadFinished(); // trueを返すと、ダウンロードが完了したことを意味します
```

URLに関連するダウンロード情報を取得するには、URL情報を渡してください。
```java
// urlのダウンロード情報を取得します
TXVodDownloadMediaInfo downloadInfo = downloader.getDownloadMediaInfo("http://1253131631.vod2.myqcloud.com/26f327f9vodgzp1253131631/f4bdff799031868222924043041/playlist.m3u8”);
```

ダウンロード情報と関連ファイルを削除するには、TXVodDownloadMediaInfoパラメータを渡してください。
```java
// ダウンロード情報の削除
boolean deleteRst = downloader.deleteDownloadMediaInfo(downloadInfo);
```

### 4、暗号化して再生します

ビデオ暗号化方式は、主にeラーニングなど、ビデオの著作権保護が必要なシナリオで使用されています。ビデオリソースを暗号化する場合、プレーヤーを変更するだけでなく、ビデオソース自体を暗号化・トランスコードする必要があり、バックエンドとエンドポイントという両方の開発エンジニアが関わる必要が出てきます。詳細については、[ビデオ暗号化ソリューション](https://www.tencentcloud.com/document/product/266/38131)をご参照ください。

Tencent CloudコンソールでappId、暗号化されたビデオのfileIdおよびpsignを取得した後、次の方法で再生を行うことができます。
```java
// psignはプレーヤーの署名です。署名についての紹介および生成方法は、以下のリンクをご参照ください。https://cloud.tencent.com/document/product/266/42436
TXPlayInfoParams playInfoParam = new TXPlayInfoParams(1252463788, // Tencent CloudアカウントのappId
    "4564972819220421305", // ビデオのfileId
    "psignxxxxxxx"); // プレーヤー署名
mVodPlayer.startVodPlay(playInfoParam);
```

###5、プレーヤーの設定 

startPlayを呼び出す前に、setConfigによってプレーヤーのパラメータを設定することができます。例えば、プレーヤーの接続タイムアウト時間の設定、プログレスコールバック間隔の設定、キャッシュファイル数の設定などです。TXVodPlayConfigがサポートするパラメータの詳細については、[基本設定インターフェース](https://www.tencentcloud.com/document/product/266/47851)をクリックしてご参照ください。使用例は、以下のとおりです。

```java
TXVodPlayConfig config = new TXVodPlayConfig();
config.setEnableAccurateSeek(true);  // 正確なseekを実行するかどうかを設定します。デフォルトはtrueです
config.setMaxCacheItems(5);  // キャッシュファイル数を5に設定します
config.setProgressInterval(200);  // 再生位置のコールバック間隔をミリ秒単位で設定します
config.setMaxBufferSize(50);  // 最大プリロードサイズ（単位MB）
mVodPlayer.setConfig(config);  // configをmVodPlayerに渡します
```

##### 再生開始時に解像度を指定します

マルチビットレートのHLSビデオソースを再生します。ビデオストリームの解像度情報を事前に知っていれば、再生開始前に再生するビデオ解像度を優先的に指定することができます。プレーヤーは、好みの解像度以下のストリームを探して再生を開始します。再生後は、setBitrateIndexを使用して必要なビットレートストリームに切り替える必要はありません。

```java
TXVodPlayConfig config = new TXVodPlayConfig();
// 渡すパラメータはビデオの幅と高さの積（幅*高さ）です。カスタマイズした値を渡すことができます
config.setPreferredResolution(TXLiveConstants.VIDEO_RESOLUTION_720X1280); 
mVodPlayer.setConfig(config);  // configをmVodPlayerに渡します
```

##### 再生位置のコールバック間隔を設定します

```
TXVodPlayConfig config = new TXVodPlayConfig();
config.setProgressInterval(200);  // 再生位置のコールバック間隔をミリ秒単位で設定します
mVodPlayer.setConfig(config);  // configをmVodPlayerに渡します
```

[](id:listening)

## プレーヤーイベント監視
TXVodPlayerオブジェクトにTXVodPlayリスナーをバインドすることができます。つまり、onPlayEvent（イベント通知）とonNetStatus（ステータスフィードバック）を使用してアプリケーションと情報を同期できます。

### 再生イベント通知（onPlayEvent）


| イベントID                                   | 数値  |  意味の説明                                                   |
| ----------------------------------------- | ---- | ---------------------------------------------------------- |
| PLAY\_EVT\_PLAY\_BEGIN                    | 2004 | ビデオ再生の開始                                               |
| PLAY\_EVT\_PLAY\_PROGRESS                 | 2005 | ビデオ再生の進行状況です。現在の再生の進行状況、ロードの進行状況および全体の長さを通知します      |
| PLAY\_EVT\_PLAY\_LOADING                  | 2007 | ビデオ再生をloading中です。再開できれば、その後にLOADING_ENDイベントが発生します |
| PLAY\_EVT\_VOD\_LOADING\_END              | 2014 | ビデオ再生ロードを終了します。ビデオは引き続き再生されます                        |
| TXVodConstants.VOD_PLAY_EVT_SEEK_COMPLETE | 2019 | Seekの完了です。バージョン10.3からサポートしています                                |
| VOD_PLAY_EVT_LOOP_ONCE_COMPLETE           | 6001 | ループ再生の1ループの再生終了（バージョン10.8からサポート）                |

#### 終了イベント
| イベントID                 |    数値  |  意味説明                |
| :-------------------  |:-------- |  :------------------------ |
| PLAY_EVT_PLAY_END       | 2006  | ビデオ再生終了                                           |
| PLAY_ERR_NET_DISCONNECT | -2301 | ネットワーク接続が切断され、何度も再接続しても回復できません。さらにリトライしたければ、手動で再起動後再生してください |
| PLAY_ERR_HLS_KEY        | -2305 | HLS復号キーの取得に失敗しました                                  |

#### 警告イベント
これらのイベントは、SDK内のイベントの一部を知らせるためだけに使用されていますが、気にしなくてもかまいません。

| イベントID                 |    数値  |  意味説明                |
| :-------------------  |:-------- |  :------------------------ |
| PLAY_WARNING_VIDEO_DECODE_FAIL   |  2101  | 現在のビデオフレームのデコードに失敗しました  |
| PLAY_WARNING_AUDIO_DECODE_FAIL   |  2102  | 現在のオーディオフレームのデコードに失敗しました  |
| PLAY_WARNING_RECONNECT           |  2103  | ネットワーク接続が切断されましたが、自動再接続が開始されました（再接続が3回を超えると、PLAY_ERR_NET_DISCONNECTが直接スローされます） |
| PLAY_WARNING_HW_ACCELERATION_FAIL|  2106  | ハードウェアデコードの開始に失敗しました。ソフトウェアデコードを使用してください   |

#### 接続イベント
サーバー接続イベント。主にサーバー接続時間の測定と統計に使用されます。

| イベントID                 |    数値  |  意味説明                |
| :-----------------------  |:-------- |  :------------------------ |
| PLAY_EVT_VOD_PLAY_PREPARED | 2013 | プレーヤーの再生準備が完了し、再生可能状態です。autoPlayがfalseに設定されている場合、このイベントを受信してからresumeを呼び出すと再生を開始します |
| PLAY_EVT_RCV_FIRST_I_FRAME | 2003 | ネットワークが最初のレンダリング可能なビデオパケット（IDR）を受信しました                      |


#### 画面イベント
次のイベントは、画面の変更情報を取得するために使用されます。

| イベントID                                   | 数値   | 意味の説明       |
| ----------------------------- | ---- | ---------- |
| PLAY\_EVT\_CHANGE\_RESOLUTION | 2009 | ビデオ解像度の変更   |
| PLAY\_EVT\_CHANGE\_ROTATION   | 2011 | MP4 ビデオ回転角度 |

#### ビデオ情報イベント
| イベントID                 |    数値  |  意味説明                |
| :-----------------------  |:-------- |  :------------------------ |
|TXLiveConstants.PLAY_EVT_GET_PLAYINFO_SUCC   | 2010 | 再生ファイル情報の取得に成功しました |

fileId方式によって再生し、リクエストが成功した場合（インターフェース：startVodPlay(TXPlayerAuthBuilder authBuilder)）、SDKはいくつかの情報を上位レイヤーに通知します。`TXLiveConstants.PLAY_EVT_GET_PLAYINFO_SUCC`イベントを受信後、paramを解析することでビデオ情報を取得できます。

|  ビデオ情報                                    | 意味の説明                                        |
| ------------------------------------------- | ------------------------------------------------- |
| EVT\_PLAY\_COVER\_URL                       | ビデオカバーアドレス                                   |
| EVT\_PLAY\_URL                              | ビデオ再生アドレス                                   |
| EVT\_PLAY\_DURATION                         | ビデオ時間                                       |
| EVT_DESCRIPTION                             | イベントの説明                                       |
| EVT_PLAY_NAME                               | ビデオ名                                       |
| TXVodConstants.EVT_IMAGESPRIT_WEBVTTURL     | スプライトイメージweb vtt説明ファイルのダウンロードURLです。バージョン10.2以降でサポートしています |
| TXVodConstants.EVT_IMAGESPRIT_IMAGEURL_LIST | スプライトイメージ画像のダウンロードURLです。バージョン10.2以降でサポートしています               |
| TXVodConstants.EVT_DRM_TYPE                 | 暗号化タイプです。バージョン10.2以降でサポートされています                     |


onPlayEventからビデオ再生プロセス情報を取得する例：

```java
mVodPlayer.setVodListener(new ITXVodPlayListener() {
    @Override
    public void onPlayEvent(TXVodPlayer player, int event, Bundle param) {
        if (event == TXLiveConstants.PLAY_EVT_VOD_PLAY_PREPARED) {
            // プレーヤーの準備ができているイベントを受信しました。この時点で、pause、resume、getWidth、getSupportedBitratesなどのインターフェースを呼び出すことができます
        } else if (event == TXLiveConstants.PLAY_EVT_PLAY_BEGIN) {
            // 再生開始イベントを受信しました
        } else if (event == TXLiveConstants.PLAY_EVT_PLAY_END) {
            // 開始終了イベントを受信しました
        }
    }

    @Override
    public void onNetStatus(TXVodPlayer player, Bundle bundle) {
    }
});
```

[](id:status)

### 再生ステータスのフィードバック（onNetStatus）
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

```java
mVodPlayer.setVodListener(new ITXVodPlayListener() {
    @Override
    public void onPlayEvent(TXVodPlayer player, int event, Bundle param) {
    }

    @Override
    public void onNetStatus(TXVodPlayer player, Bundle bundle) {
        //現在のCPU使用率を取得します
        CharSequence cpuUsage = bundle.getCharSequence(TXLiveConstants.NET_STATUS_CPU_USAGE);
        // ビデオ幅の取得
        int videoWidth = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_WIDTH);
        // ビデオの高さの取得
        int videoHeight = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_HEIGHT);
        // リアルタイムレートを取得（単位：kbps）
        int speed = bundle.getInt(TXLiveConstants.NET_STATUS_NET_SPEED);
        //現在のストリーミングメディアのビデオフレームレートを取得します
        int fps = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_FPS);
        //現在のストリーミングメディアのビデオビットレート（kbps単位）を取得します
        int videoBitRate = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_BITRATE);
        //現在のストリーミングメディアのオーディオビットレート（kbps単位）を取得します
        int audioBitRate = bundle.getInt(TXLiveConstants.NET_STATUS_AUDIO_BITRATE);
        //バッファ（jitterbuffer）のサイズを取得します。バッファの現在の長さは0であれば、カクカクする可能性が高いことを意味します
        int jitterbuffer = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_CACHE);
        //連続したサーバーののIPアドレスを取得します
        String ip = bundle.getString(TXLiveConstants.NET_STATUS_SERVER_IP);
    }
});
```

##  シーン化機能

### 1、SDKベースのDemoコンポーネント

Tencent Cloudは、Player SDKをベースとして以下のような[プレーヤーコンポーネント](https://www.tencentcloud.com/document/product/266/33975)を開発しました。品質モニタリング、ビデオ暗号化、超高速HD（TESHD）、解像度切り替え、ミニウィンドウ再生などの機能を一体化し、あらゆるオンデマンド(VOD)、ライブストリーミング再生のシナリオに対応します。完備された機能をパッケージ化するとともに、上位層のUIを提供することで、市場で人気を博す各種ビデオアプリに引けを取らない再生ソフトウェアを短時間で作成することができます。

### 2、オープンソースGithub

Tencent CloudはプレーヤーSDKに基づき、没入型ビデオプレーヤーコンポーネント、ビデオFeedストリーム、複数プレーヤーに再利用可能なコンポーネントなどを開発しており、リリースに伴い、ユーザーシナリオに基づくコンポーネントをより多く提供していきます。[Player_Android](https://github.com/LiteAVSDK/Player_Android)でダウンロードして体験いただけます。
