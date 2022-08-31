## 準備作業
1. より完全で全面的なプレーヤー機能を体験していただくために、[VOD](https://intl.cloud.tencent.com/product/vod)関連サービスをアクティブ化することをお勧めします。アカウント登録がないユーザーは、アカウントを登録して[トライアル](https://intl.cloud.tencent.com/login)を行うことができます。VODサービスをご利用にならない場合はこの手順を省略できますが、統合後に使用できるのはプレーヤーの基本機能のみとなります。
2. Android Studioをダウンロードします。[Android Studio公式サイト](https://developer.android.com/studio)でダウンロードとインストールを行うことができます。ダウンロード済みの場合はこの手順を省略できます。

## ここでは次の内容について知ることができます
* AndroidプレーヤーSDKの統合方法
* プレーヤーSDKを使用したVOD再生方法
* プレーヤーSDKの基本機能を使用して、より多くの機能を実装する方法

## SDKの統合
[](id:stepone)
### ステップ1：SDK開発キットのダウンロード[](id:step1)
[ダウンロード](https://vcube.cloud.tencent.com/home.html)からSDK開発キットをダウンロードし、SDK統合ガイドラインに従ってSDKをAppプロジェクトに組み込みます。




### ステップ2：Viewの追加
SDKはデフォルトでビデオレンダリング用にTXCloudVideoViewをご提供しています。最初のステップとして、以下のようにレイアウトxmlファイルにコードを追加します。
```xml
<com.tencent.rtmp.ui.TXCloudVideoView
            android:id="@+id/video_view"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_centerInParent="true"
            android:visibility="gone"/>
```

[](id:step3)

### ステップ3：Playerの作成

次に、**TXVodPlayer**のオブジェクトを作成し、setPlayerViewインターフェースを使用して、先ほどインターフェースに追加した**video_view**コントロールにバインドします。

```java
//mPlayerViewとは、ステップ2で追加したビデオレンダリングviewです
TXCloudVideoView mPlayerView = findViewById(R.id.video_view);
//playerオブジェクトの作成
TXVodPlayer mVodPlayer = new TXVodPlayer(getActivity());
//playerオブジェクトとビデオレンダリングviewとのバインド
mVodPlayer.setPlayerView(mPlayerView);
```

[](id:step4)

### ステップ4：再生の起動

TXVodPlayerは2種類の再生モードをサポートしており、ニーズに応じて選択することができます。

<dx-tabs>
::: URL方式による方法
  TXVodPlayerは内部で自動的に再生プロトコルを認識しますので、再生URLをstartPlay関数に渡すだけで完了です。

```java
// URLビデオリソースの再生
String url = "http://1252463788.vod2.myqcloud.com/xxxxx/v.f20.mp4";
mVodPlayer.startPlay(url); 


// ローカルビデオリソースの再生
String localFile = "/sdcard/video.mp4";
mVodPlayer.startPlay(localFile); 
```
:::
::: FileId方式による方法
```objectivec
// 以下の新しいインターフェースの使用をお勧めします
TXPlayInfoParams playInfoParam = new TXPlayInfoParams(1252463788, // Tencent CloudアカウントのappId
    "4564972819220421305", // ビデオのfileId
    "psignxxxxxxx"); // 暗号化されたビデオの場合は、以下を入力する必要があります
mVodPlayer.startPlay(playInfoParam);

// 古いインターフェースのため、非推奨です
TXPlayerAuthBuilder authBuilder = new TXPlayerAuthBuilder();
authBuilder.setAppId(1252463788);
authBuilder.setFileId("4564972819220421305");
mVodPlayer.startPlay(authBuilder); 
```
[メディア資産管理](https://console.cloud.tencent.com/vod/media)で対応するビデオファイルを検索することができます。FileIdは、ファイルの名前の下に表示されます。

FileId方式で再生する場合、プレーヤーはバックグラウンドに実際の再生アドレスをリクエストします。この時点でネットワークの異常やFileIdが存在しない場合、`TXLiveConstants.PLAY_ERR_GET_PLAYINFO_FAIL`イベントを受信します。逆に、`TXLiveConstants.PLAY_EVT_GET_PLAYINFO_SUCC`を受信した場合、リクエストが成功したことを意味します。
:::
</dx-tabs>


[](id:5)

### ステップ5：再生終了

再生終了時、特に次のstartPlayを行う前には、**viewコントロールの破棄**を忘れずに行ってください。この操作をしない場合、大量のメモリリークや画面のちらつきといった問題が発生します。

また、再生画面を終了する際には、レンダリングViewの`onDestroy()`関数の呼び出しを忘れずに行ってください。この操作をしない場合、メモリリークや「Receiver not registered」といったアラームが発生することがあります。

```java
@Override
public void onDestroy() {
    super.onDestroy();
    mVodPlayer.stopPlay(true); // trueは、最後のフレームをクリアすることを意味します
    mPlayerView.onDestroy(); 
}
```
>?stopPlayのブール型パラメータには、「最後のフレームをクリアするかどうか」という意味があります。RTMP SDKの以前のバージョンでは、ライブストリーミングプレーヤーにpauseの概念がなかったため、このブール値は最後のフレームのクリアを制御するために使用されます。

オンデマンド再生の終了後も、最後のフレームを残したい場合は、再生終了イベントを受信後に何もしないことによって、デフォルトで最後のフレームで停止することができます。

## 基本機能の使用
### 1、再生の制御

#### 再生開始

```java
// 再生開始
mVodPlayer.startPlay(url)
```

#### 再生一時停止

```java
// 再生一時停止
mVodPlayer.pause();
```

#### 再生再開

```java
// 再生再開
mVodPlayer.resume();
```

#### 再生終了

```java
// 再生終了
mVodPlayer.stopPlay(true);
```

#### 進捗の調整（Seek）

ユーザーがプログレスバーをドラッグすると、seekを呼び出して指定した位置から再生を開始することができます。プレーヤーSDKは正確なseekをサポートします。

```java
int time = 600; // intタイプのとき、単位は秒
// float time = 600; // floatタイプのとき、単位は秒
// 進捗の調整
mVodPlayer.seek(time);
```

#### 指定した時間からの再生

startPlayを最初に呼び出す前に、指定した時間からの再生がサポートされています。

```java
float startTimeInMS = 600; // 単位：ミリ秒
mVodPlayer.setStartTime(startTimeInMS);   // 再生開始時間の設定
mVodPlayer.startPlay(url);
```

### 2、画面調整

- **view：サイズと位置**
画面のサイズや位置を変えるには、SDK統合時に[Viewの追加](#addview)で追加した「video_view」コントロールのサイズや位置を調整するだけで完了です。
- **setRenderMode：全体に表示または適応**
<table>
<thead>
<tr>
<th>オプション値</th>
<th>意味</th>
</tr>
</thead>
<tbody><tr>
<td>RENDER_MODE_FULL_FILL_SCREEN</td>
<td>画像をアスペクト比を維持したまま画面全体に表示し、余分な部分をトリミングします。このモードでは画面に黒枠が残りませんが、一部の領域がトリミングされるため、完全に表示されない場合があります</td>
</tr>
<tr>
<td>RENDER_MODE_ADJUST_RESOLUTION</td>
<td>画像は、アスペクト比を維持したまま、最も長い辺に合わせてスケーリングされます。スケーリングされた幅と高さは表示領域を超えることなく中央に表示され、画面に黒枠が残る場合があります</td>
</tr>
</tbody></table>
- **setRenderRotation：画面の回転**
<table>
<thead>
<tr>
<th>オプション値</th>
<th>意味</th>
</tr>
</thead>
<tbody><tr>
<td>RENDER_ROTATION_PORTRAIT</td>
<td>通常再生（Homeボタンは画面直下）</td>
</tr>
<tr>
<td>RENDER_ROTATION_LANDSCAPE</td>
<td>画面が時計回りに270度回転します（Homeは画面真左）</td>
</tr>
</tbody></table>
```java
 // 画像を画面全体にアスペクト比を維持したまま表示
mVodPlayer.setRenderMode(TXLiveConstants.RENDER_MODE_FULL_FILL_SCREEN);
// 通常再生（Homeボタンは画面直下）
mVodPlayer.setRenderRotation(TXLiveConstants.RENDER_ROTATION_PORTRAIT);
```



### 3、可変速再生
VODプレーヤーは可変速再生をサポートしており、インターフェース`setRate`を通じてオンデマンド再生レートを設定することにより、0.5X、1.0X、1.2X、2Xなどの高速再生と低速再生をサポートしています。


```java
// 1.2倍速再生に設定
mVodPlayer.setRate(1.2); 
```

### 4、ループ再生

```java
// ループ再生の設定
mVodPlayer.setLoop(true);
// 現在のループ再生ステータスの取得
mVodPlayer.isLoop(); 
```

### 5、ミュート設定

```java
// ミュートの設定です。trueはミュートオン、falseはミュートオフを表します
mVodPlayer.setMute(true);
```

### 6、スクリーンキャプチャ

**snapshot**を呼び出すと、現在のビデオを1つのフレームとしてキャプチャできます。この機能は、現在のCSSストリームのビデオ画面のみをキャプチャします。現在のUI全体をキャプチャする必要がある場合は、AndroidシステムAPIを呼び出して実行してください。



```java
// スクリーンキャプチャ
mVodPlayer.snapshot(new ITXSnapshotListener() {
    @Override
    public void onSnapshot(Bitmap bmp) {
        if (null != bmp) {
           //スクリーンキャプチャbitmapの取得
        }
    }
});
```


### 7、ロール画像広告
プレーヤーSDKは広告宣伝用として、インターフェースへのロール画像の追加をサポートしています。実装方法は以下のとおりです。
* `autoPlay`をNOにすると、この時点でプレーヤーは正常にロードされますが、ビデオはすぐに再生を開始しません。
* プレーヤーがロードされてからビデオが始まる前に、プレーヤーのインターフェースでロール画像広告を確認することができます。
* 広告の表示終了条件に達したら、resumeインターフェースでビデオ再生を開始します。

```java
mVodPlayer.setAutoPlay(false);  //  自動再生しないように設定します
mVodPlayer.startPlay(url);    // startPlayを呼び出すとビデオがロードされますが、ロードが成功しても自動的に再生されるわけではありません
// ......
// プレーヤーインターフェースへの広告表示
// ......  
mVodPlayer.resume();  // 広告表示後、resumeを呼び出してビデオ再生を開始します
```

### 8,HTTP-REF
TXVodPlayConfigのheadersは、URLがコピーされるのを防ぐためによく使われるRefererフィールド（Tencent Cloudは、よりセキュアな署名のリンク不正アクセス防止方式を提供できます）や、クライアントのID情報を検証するためのCookieフィールドなど、HTTPリクエストヘッダーの設定に使用することができます。
### 9、ハードウェアアクセラレーション
Blu-rayレベル(1080p)の画質の場合、ソフトウェアデコードだけではスムーズな再生は困難です。そのため、ゲームのライブストリーミングがメインのシナリオでは、一般的にハードウェアアクセラレーションをオンにすることをお勧めします。

ソフトウェアデコードとハードウェアデコードを切り替えるには、切り替える前に**stopPlay**、切り替えた後に**startPlay**を行う必要があります。この操作をしない場合、より深刻な画面の揺れや歪みといった問題が発生します。

```java
 mVodPlayer.stopPlay(true);
 mVodPlayer.enableHardwareDecode(true);
 mVodPlayer.startPlay(flvUrl, type);
```
### 10、解像度の設定
SDKは、HLSのマルチビットレート形式をサポートしています。これはユーザーが異なるビットレートの再生ストリームを切り替えるのに便利で、異なる解像度で再生するという目的を達成することができます。PLAY_EVT_PLAY_BEGINイベントを受信した後、以下の方法で解像度を設定することができます。

```java
ArrayList<TXBitrateItem> bitrates = mVodPlayer.getSupportedBitrates(); //マルチビットレートアレイの取得
int index = bitrates.get(i).index;  // 再生するビットレートの添え字を指定します
mVodPlayer.setBitrateIndex(index);  // ビットレートを希望の解像度に切り替えます
```

再生中は、`mVodPlayer.setBitrateIndex(int)`を通じていつでもビットレートを切り替えることができます。切り替え中、別のストリームのデータを再度プルします。SDKは、Tencent Cloudのマルチビットレートファイルに最適化されているため、ラグが発生することなく切り替えが可能です。
### 11、ビットレートストリーミングアダプティブ
SDKは、HLSのマルチビットレートアダプティブをサポートしています。関連機能をオンにすると、プレーヤーが現在の帯域幅に基づいて再生に最適なビットレートを動的に選択することが可能です。PLAY_EVT_PLAY_BEGINイベントを受信した後、以下の方法でビットレートストリーミングアダプティブをオンにすることができます。
```java
mVodPlayer.setBitrateIndex(-1); //indexパラメータは-1で渡されます
```
再生中はいつでも`-[mVodPlayer setBitrateIndex(int)`で別のビットレートに切り替えることができ、切り替えた後はビットレートストリーミングアダプティブはオフになります。

### 12、再生進捗のリスニング

VOD再生中の進捗情報には、**ロード進捗**と**再生進捗**という2種類があります。現在、SDKはこれら2つの進捗をイベント通知という形でリアルタイムに通知しています。イベント通知の詳細については、[イベントリスニング](#listening)をご参照ください。

**TXVodPlayerListener**リスナーをTXVodPlayerオブジェクトにバインドすると、進捗通知は、**PLAY_EVT_PLAY_PROGRESS**イベントを通じてアプリケーションにコールバックされます。このイベントの追加情報には、上記の2つの進捗指標が含まれます。




```java
mVodPlayer.setVodListener(new ITXVodPlayListener() {
    @Override
    public void onPlayEvent(TXVodPlayer player, int event, Bundle param) {
        if (event == TXLiveConstants.PLAY_EVT_PLAY_PROGRESS) {
            // ロードの進行状況です。単位はミリ秒
            int playable_duration_ms = param.getInt(TXLiveConstants.EVT_PLAYABLE_DURATION_MS);
            mLoadBar.setProgress(playable_duration_ms); // loadingプログレスバーの設定

            // 再生の進行状況です。単位はミリ秒
            int progress_ms = param.getInt(TXLiveConstants.EVT_PLAY_PROGRESS_MS);
            mSeekBar.setProgress(progress_ms);  // 再生プログレスバーの設定

            // ビデオの総尺です。単位はミリ秒
            int duration_ms = param.getInt(TXLiveConstants.EVT_PLAY_DURATION_MS);
            // 表示時間の設定などに使用できます
        }
    }

    @Override
    public void onNetStatus(TXVodPlayer player, Bundle bundle) {
    }
});
```


### 13、再生インターネット速度のリスニング

[イベントリスニング](#listening)を使用すると、ビデオの再生時にラグが発生した際、その時点のネットワーク速度を表示することができます。

* `onNetStatus`の`NET_STATUS_NET_SPEED`で現在のネットワーク速度を取得します。具体的な使用方法については、[ステータスフィードバック（onNetStatus）](#status)をご参照ください。
* `PLAY_EVT_PLAY_LOADING`イベントをリスニングした後に、現在のネットワーク速度を表示します。
* `PLAY_EVT_VOD_LOADING_END`イベントを受信した後、現在のネットワーク速度を表示するviewを非表示にします。

```java
mVodPlayer.setVodListener(new ITXVodPlayListener() {
    @Override
    public void onPlayEvent(TXVodPlayer player, int event, Bundle param) {
        if (event == TXLiveConstants.PLAY_EVT_PLAY_LOADING) {
            // 現在のタスクを表示します

        } else if (event == TXLiveConstants.PLAY_EVT_VOD_LOADING_END) {
            // 現在のネットワーク速度を表示するビューを非表示にします
        }
    }

    @Override
    public void onNetStatus(TXVodPlayer player, Bundle bundle) {
        // リアルタイムレートの取得。単位はkbps
        int speed = bundle.getInt(TXLiveConstants.NET_STATUS_NET_SPEED);
    }
});
```

### 14、ビデオ解像度の取得

プレーヤーSDKはURL文字列を介してビデオを再生します。URLそのものにはビデオ情報は含まれません。関連情報を取得するには、クラウドサーバーにアクセスしてビデオ情報をロードする必要があるため、SDKはビデオ情報をイベント通知としてのみお客様のアプリケーションに送信します。詳細については、[イベントリスニング](#listening)をご参照ください。

**解像度の情報は、以下の2種類の方法によって取得できます**

方法1：`onNetStatus`の`NET_STATUS_VIDEO_WIDTH`と`NET_STATUS_VIDEO_HEIGHT`により、ビデオの幅と高さを取得します。具体的な使用方法については、[ステータスフィードバック（onNetStatus）](#status)をご参照ください。

方法2：プレーヤーからPLAY_EVT_VOD_PLAY_PREPAREDイベントコールバックを受信した後、`TXVodPlayer.getWidth()`と`TXVodPlayer.getHeight()`を直接呼び出して現在の幅と高さを取得します。

```java
mVodPlayer.setVodListener(new ITXVodPlayListener() {
    @Override
    public void onPlayEvent(TXVodPlayer player, int event, Bundle param) {
    }

    @Override
    public void onNetStatus(TXVodPlayer player, Bundle bundle) {
        //ビデオ幅の取得
        int videoWidth = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_WIDTH);
        //ビデオ高さの取得
        int videoHeight = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_HEIGHT);
    }
});

// ビデオの幅と高さを取得します。プレーヤーからPLAY_EVT_VOD_PLAY_PREPAREDイベントコールバックを受信した後で値を返す必要があります
mVodPlayer.getWidth();
mVodPlayer.getHeight();
```

### 15、再生バッファサイズ

通常のビデオ再生時に、事前にネットワークからバッファするデータの最大サイズを制御します。設定されていない場合は、プレーヤーのデフォルトのバッファポリシーに従って、スムーズな再生が確保されます。

```java
TXVodPlayConfig config = new TXVodPlayConfig();
config.setMaxBufferSize(10);  // 再生時の最大バッファサイズです。単位：MB
mVodPlayer.setConfig(config);  // configをmVodPlayerに渡します
```

### 16、ビデオローカルキャッシュ[](id:cache)

UGSVのビデオ再生シナリオでは、ビデオファイルのローカルキャッシュは非常に重要な機能です。一般ユーザーにとっては、一度視聴したビデオを再度視聴する際にトラフィックを消費しないことが望ましいからです。

- **サポートされている形式：**SDKは、HLS(m3u8)とMP4という2種類の一般的なオンデマンド形式のキャッシュ機能をサポートしています。
- **オンのタイミング：**SDKは、デフォルトではキャッシュ機能がオンになりませんので、ユーザーの再生率が高くないシナリオでは、この機能をオンにすることはお勧めしません。
- **オンにする方法：**グローバルに有効で、プレーヤーを使用するときにオンになります。この機能をオンにするには、ローカルキャッシュディレクトリとキャッシュサイズという2つのパラメータを設定する必要があります。

```java
File sdcardDir = getApplicationContext().getExternalFilesDir(null);
if (sdcardDir != null) {
    //再生エンジンのグローバルキャッシュディレクトリの設定
   TXPlayerGlobalSetting.setCacheFolderPath(sdcardDir.getPath() + "/txcache");
    //グローバルキャッシュディレクトリと再生エンジンのキャッシュサイズを設定します。//単位はMBです
    TXPlayerGlobalSetting.setMaxCacheSize(200); 
}

//プレーヤーの使用
```

>?TXVodPlayConfig#setMaxCacheItemsインターフェースで設定された旧バージョンは廃止されているため、非推奨です。

##  高度な機能の使用

### 1、ビデオのプリ再生

#### ステップ1：ビデオのプリ再生・使用

UGSV再生シナリオでは、ビデオのプリロード機能がスムーズな視聴に大変役立ちます。現在のビデオを視聴中に、次に再生するビデオをバックグラウンドでロードし、ユーザーが実際に次のビデオに切り替えたときに、最初からロードする必要がなく、すぐに再生することができます。

ビデオのプリ再生は、秒単位で開けるという効果を発揮しますが、ある程度のパフォーマンスオーバーヘッドがあります。業務にたくさんのビデオプリロードのニーズがある場合、[ビデオのプリダウンロード](#download)と併用することをお勧めします。

これは、ビデオ再生中のシームレスな切り替えを後押しする技術で、TXVodPlayerのsetAutoPlayスイッチを使ってこの機能を実装することができます。具体的な方法は、以下のとおりです。
![](https://qcloudimg.tencent-cloud.cn/raw/b2bd645f29af403bf2740156aee44092.jpg)

```java
// ビデオAの再生：autoPlayがtrueに設定されている場合、startPlayの呼び出しにより、直ちにビデオのロードと再生が開始されます
String urlA = "http://1252463788.vod2.myqcloud.com/xxxxx/v.f10.mp4";
playerA.setAutoPlay(true);
playerA.startPlay(urlA);

// ビデオAを再生すると同時に、ビデオBをプリロードします。これは、setAutoPlayをfalseに設定すると行われます
String urlB = @"http://1252463788.vod2.myqcloud.com/xxxxx/v.f20.mp4";
playerB.setAutoPlay(false);
playerB.startPlay(urlB); // すぐに再生を開始せず、ビデオのロードのみを開始します
```

ビデオAの再生が終了し、自動的に（またはユーザーが手動で）ビデオBに切り替えたとき、resume関数を呼び出し、すぐに再生できるようにします。

>! autoPlayをfalseに設定した後、resumeを呼び出す前にビデオBの準備ができていることを確認する必要があります。すなわち、ビデオBのPLAY_EVT_VOD_PLAY_PREPARED（2013、プレーヤーは再生可能状態）イベントをリスニングした後に呼び出す必要があります。


```java
public void onPlayEvent(TXVodPlayer player, int event, Bundle param) {
    // ビデオAの再生が終了すると、そのままビデオBの再生が始まるので、シームレスな切り替えが可能です
    if (event == PLAY_EVT_PLAY_END) {
           playerA.stop();
           playerB.setPlayerView(mPlayerView);
           playerB.resume();
        }
}
```

#### ステップ2：ビデオのプリ再生・バッファの設定

- バッファを大きめに設定すると、ネットワークの変動に対応しやすくなり、スムーズな再生という目的を達成できます。
- バッファを小さめに設定すると、トラフィックの消費を抑えることができます。 

##### プリ再生バッファサイズ

このインターフェースは、プリロードシナリオ（ビデオ再生が開始され、playerのAutoPlayがfalseに設定される前）向けで、最大バッファサイズを制御するために使用されます。

```java
TXVodPlayConfig config = new TXVodPlayConfig();
config.setMaxPreloadSize(2);  // プリ再生の最大バッファサイズです。単位はMBで、業務の状況に応じてトラフィックを節約するように設定します
mVodPlayer.setConfig(config);  // configをmVodPlayerに渡します
```

##### 再生バッファサイズ 

通常のビデオ再生時に、事前にネットワークからバッファするデータの最大サイズを制御します。設定されていない場合は、プレーヤーのデフォルトのバッファポリシーに従って、スムーズな再生が確保されます。

```java
TXVodPlayConfig config = new TXVodPlayConfig();
config.setMaxBufferSize(10);  // 再生時の最大バッファサイズです。単位：MB
mVodPlayer.setConfig(config);  // configをmVodPlayerに渡します
```

[](id:download)
### 2、ビデオプリダウンロード

プレーヤーインスタンスを作成する必要がなく、ビデオコンテンツの一部があらかじめダウンロードされています。そのためプレーヤーを使用すると、ビデオの再生速度がアップし、より良い再生エクスペリエンスを提供することができます。

再生サービスを利用する前に、[ビデオキャッシュ](#cache)が設定されていることを確認してください。

>? 
> 1. TXPlayerGlobalSettingはグローバルキャッシュ設定インターフェースです。以前のTXVodConfigのキャッシュ設定インターフェースは廃止されています。
> 2.  グローバルキャッシュのディレクトリとサイズの設定は、プレーヤーのTXVodConfigで構成されるキャッシュ設定よりも優先されます。

ユースケース：

```java
//まずグローバルキャッシュディレクトリと再生エンジンのキャッシュサイズを設定します
File sdcardDir = getApplicationContext().getExternalFilesDir(null);
//再生エンジンのグローバルキャッシュディレクトリとキャッシュサイズを設定します
if (sdcardDir != null) {
    TXPlayerGlobalSetting.setCacheFolderPath(sdcardDir.getPath() + "/PlayerCache");
    TXPlayerGlobalSetting.setMaxCacheSize(200); //単位はMB
}

String palyrl = "http://****";
//プリダウンロードの開始
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

//プリダウンロードのキャンセル
downloadManager.stopPreload(taskID);
```

### 3、ビデオのダウンロード
ビデオをダウンロードすると、ユーザーがインターネットに接続している状態でビデオをダウンロードした場合、インターネットに接続していない状態でもビデオを視聴することができます。また同時に、プレーヤーSDKはローカル暗号化機能を提供しており、ダウンロードしたローカルビデオは暗号化された状態のまま、指定されたプレーヤーでのみ復号し再生することができるので、ダウンロードしたビデオの違法配信を効果的に防止し、ビデオのセキュリティを保護することができます。

HLSストリームメディアはローカルに直接保存できないため、ローカルファイルの再生によってHLSをローカルにダウンロードして再生することはできません。この問題については、`TXVodDownloadManager`ベースのビデオダウンロード方式によって、HLSをオフラインで再生することが可能です。

> !
> - `TXVodDownloadManager`は現時点では、MP4とFLV形式のファイルのキャッシュをサポートしておらず、非ネストのHLS形式ファイルのみサポートしています。
> - プレーヤーSDKは、MP4およびFLV形式のローカルファイルの再生をサポートしています。

[](id:offline1)
#### ステップ1：準備作業

`TXVodDownloadManager`は単一のインスタンスとして設計されているので、複数のダウンロードオブジェクトを作成することはできません。使い方は以下のとおりです。

```java
TXVodDownloadManager downloader = TXVodDownloadManager.getInstance();
downloader.setDownloadPath("<ダウンロード先のディレクトリを指定してください>"];
```

[](id:offline2)
#### ステップ2：ダウンロードの開始
ダウンロードの開始方法としては、[URL](#url)と[Fileid](#fileid)という2種類の方法があります。具体的な操作については以下のとおりです。
<dx-tabs>
::: URL方式[](id:url)
少なくともダウンロードアドレスのURLを渡す必要があります。ネストしたHLS形式はサポートしておらず、非ネストしたHLS形式のみサポートしています。userNameは具体的な値が渡されない場合、デフォルトは「default」となります。
```java
downloader.startDownloadUrl("http://1500005830.vod2.myqcloud.com/43843ec0vodtranscq1500005830/00eb06a88602268011437356984/video_10_0.m3u8", "");
```
:::
::: Fileid方式[](id:fileid)
Fileidのダウンロードには、少なくともAppID、FileidおよびqualityIdを渡す必要があります。署名付きビデオはpSignを渡す必要があります。userNameは具体的な値が渡されない場合、デフォルトは「default」となります。
```java
//  QUALITYOD // オリジナル画像
// QUALITYFLU // LD
// QUALITYSD  // SD
// QUALITYHD  // HD
TXVodDownloadDataSource source = new TXVodDownloadDataSource(1252463788, "4564972819220421305", QUALITYHD, "", "");
downloader.startDownload(source);
```
:::
</dx-tabs>


[](id:offline3)
#### ステップ3：タスク情報 
タスク情報を受信する前に、コールバックlistenerを設定する必要があります。

```java
downloader.setListener(this);
```

受信する可能性のあるタスクコールバックは、以下のとおりです。

| コールバック情報 | 説明 |
|---------|---------|
| void onDownloadStart(TXVodDownloadMediaInfo mediaInfo) | タスクの開始です。SDKのダウンロードが開始されたことを示します |
| void onDownloadProgress(TXVodDownloadMediaInfo mediaInfo) | タスクの進行状況です。ダウンロード中、SDKはこのインターフェースを頻繁にコールバックするので、`mediaInfo.getProgress()`で現在の進捗を取得できます |
| void onDownloadStop(TXVodDownloadMediaInfo mediaInfo) | タスクの停止です。`stopDownload`を呼び出してダウンロードを停止すると、ダウンロードの停止に成功したことを示すこのメッセージが表示されます |
|  void onDownloadFinish(TXVodDownloadMediaInfo mediaInfo) |  ダウンロード完了です。このコールバックを受信すると、すべてのダウンロードが完了したことを意味します。この時点で、ダウンロードしたファイルはTXVodPlayerで再生できます |
| void onDownloadError(TXVodDownloadMediaInfo mediaInfo, int error, String reason) | ダウンロードエラーです。ダウンロード中にネットワークが切断されると、このインターフェースがコールバックされると同時にダウンロードタスクが停止されます。エラーコードは、`TXVodDownloadManager`にあります|


downloaderは複数のタスクを同時にダウンロードできるので、コールバックインターフェースには`TXVodDownloadMediaInfo`オブジェクトが含まれます。お客様は、URLやdataSourceにアクセスしてダウンロード元を特定したり、ダウンロードの進捗やファイルサイズなどの情報を取得したりできます。

[](id:offline4)

#### ステップ4：ダウンロードの中断
ダウンロードを停止するには、`downloader.stopDownload()`メソッドを呼び出してください。パラメータは、`downloader.startDownload()`によって返されるオブジェクトです。**SDKは、中断からの再開をサポート**しています。ダウンロードディレクトリが変更されていない場合、同じファイルの次のダウンロードは最後に停止したところから再び開始されます。

#### ステップ5：管理のダウンロード
すべてのユーザーアカウントのダウンロードリスト情報を取得します。指定したユーザーアカウントのダウンロードリスト情報も取得することができます。
```java
// すべてのユーザーダウンロードリスト情報の取得
// アクセス側はダウンロード情報に含まれるuserNameに基づいて、異なるユーザーのダウンロードリスト情報を区別することができます
List<TXVodDownloadMediaInfo> downloadList = downloader.getDownloadMediaInfoList(); 
if (downloadInfoList == null || downloadInfoList.size() <= 0) return;
// デフォルトの「default」ユーザーのダウンロードリストの取得
List<TXVodDownloadMediaInfo> defaultUserDownloadList = new ArrayList<>();
for(TXVodDownloadMediaInfo downloadMediaInfo : downloadInfoList) {
  if ("default".equals(downloadMediaInfo.getUserName())) {
  	defaultUserDownloadList.add(downloadMediaInfo);
  }
}
```

Fileidに関するダウンロード情報を取得します。現在のダウンロード状況、ダウンロードの進捗の取得、ダウンロード完了の判断などが含まれます。AppID、FileidおよびqualityIdを渡す必要があります。
```java
// fileIdに関するダウンロード情報の取得
TXVodDownloadMediaInfo downloadInfo = downloader.getDownloadMediaInfo(1252463788, "4564972819220421305", QUALITYHD);
int duration = downloadInfo.getDuration();	// 総時間の取得
int playableDuration = downloadInfo.getPlayableDuration(); // ダウンロード済みの再生可能時間の取得
float progress = downloadInfo.getProgress();	// ダウンロード進行状況の取得
String playPath = downloadInfo.getPlayPath(); // オフライン再生パスを取得し、プレーヤーに渡すことでオフライン再生が可能になります
int downloadState = downloadInfo.getDownloadState(); // ダウンロードステータスの取得、詳細については、STATE_xxx定数をご参照ください
boolean isDownloadFinished = downloadInfo.isDownloadFinished(); // ダウンロードが完了した場合、trueを返します
```

URLのダウンロード情報を取得するには、URLの情報を渡す必要があります。
```java
// 特定のurlダウンロード情報の取得
TXVodDownloadMediaInfo downloadInfo = downloader.getDownloadMediaInfo("http://1253131631.vod2.myqcloud.com/26f327f9vodgzp1253131631/f4bdff799031868222924043041/playlist.m3u8");
```

ダウンロード情報および関連ファイルを削除する場合は、TXVodDownloadMediaInfoパラメータを渡す必要があります。
```java
// ダウンロード情報の削除
boolean deleteRst = downloader.deleteDownloadMediaInfo(downloadInfo);
```


### 4、暗号化再生

ビデオ暗号化方式は、主にオンライン教育など、ビデオの著作権保護が必要なシナリオで使用されています。ビデオソースを暗号化する場合、プレーヤーを変更するだけでなく、ビデオソース自体を暗号化・トランスコードする必要があり、バックエンドとエンドポイントという両方の開発エンジニアが関わる必要が出てきます。詳細については、[ビデオ暗号化ソリューション](https://intl.cloud.tencent.com/document/product/266/38131)をご参照ください。

### 5、プレーヤーの設定 

statPlayを呼び出す前に、setConfigによってプレーヤーのパラメータを設定することができます。例としては、プレーヤー接続タイムアウトの設定、プログレスコールバック間隔の設定、キャッシュファイル数の設定などです。TXVodPlayConfigがサポートするパラメータの詳細については、[基本設定インターフェース](https://intl.cloud.tencent.com/document/product/266/47841)をクリックしてご参照ください。使用例は、以下のとおりです。

```java
TXVodPlayConfig config = new TXVodPlayConfig();
config.setEnableAccurateSeek(true);  // 正確にseekするかどうかを設定します。デフォルトはtrueです
config.setMaxCacheItems(5);  // キャッシュファイル数を5に設定します
config.setProgressInterval(200);  // プログレスコールバック間隔を設定します。単位はミリ秒です
config.setMaxBufferSize(50);  // 最大プリロードサイズ。単位はMBです
mVodPlayer.setConfig(config);  // configをmVodPlayerに渡します
```

##### 再生開始時の解像度の指定

HLSのマルチビットレートのビデオソースを再生する場合、ビデオストリームの解像度情報があらかじめわかっていれば、再生開始前にビデオ解像度を優先的に指定して再生することができます。プレーヤーは、再生開始時に希望する解像度以下のストリームを探すため、再生開始後にsetBitrateIndexによって希望するビットレートストリーミングに切り替える必要はありません。

```java
TXVodPlayConfig config = new TXVodPlayConfig();
// 入力パラメータは、ビデオの幅と高さの積（幅×高さ）で、カスタム値として渡すことができます
config.setPreferredResolution(TXLiveConstants.VIDEO_RESOLUTION_720X1280); 
mVodPlayer.setConfig(config);  // configをmVodPlayerに渡します
```

##### 再生進捗コールバック時間間隔の設定

```
TXVodPlayConfig config = new TXVodPlayConfig();
config.setProgressInterval(200);  // プログレスコールバック間隔を設定します。単位はミリ秒です
mVodPlayer.setConfig(config);  // configをmVodPlayerに渡します
```

[](id:listening)

## プレーヤーイベントのリスニング
TXVodPlayListenerリスナーをTXVodPlayerオブジェクトにバインドすると、onPlayEvent（イベント通知）とonNetStatus（ステータスフィードバック）を介して、アプリケーションに情報を同期させることができます。

### 再生イベント通知（onPlayEvent）


| イベントID                                   | 数値  |  意味の説明                                                   |
| ----------------------------------------- | ---- | ---------------------------------------------------------- |
| PLAY\_EVT\_PLAY\_BEGIN                    | 2004 | ビデオ再生の開始                                               |
| PLAY\_EVT\_PLAY\_PROGRESS                 | 2005 | ビデオ再生の進行状況です。現在の再生の進行状況、ロードの進行状況および全体の長さを通知します      |
| PLAY\_EVT\_PLAY\_LOADING                  | 2007 | ビデオ再生をloading中です。再開できれば、その後にLOADING_ENDイベントが発生します |
| PLAY\_EVT\_VOD\_LOADING\_END              | 2014 | ビデオ再生ロードを終了します。ビデオは引き続き再生されます                        |
| TXVodConstants.VOD_PLAY_EVT_SEEK_COMPLETE | 2019 | Seekの完了です。バージョン10.3からサポートしています|

#### イベント終了
| イベントID               |   数値  |  意味の説明                |
| :-------------------  |:-------- |  :------------------------ |
|PLAY_EVT_PLAY_END      |  2006|  ビデオ再生を終了します   |
|PLAY_ERR_NET_DISCONNECT |  -2301  |  ネットワーク接続が切断され、かつ複数回再接続しても再開できません。これ以上のリトライを行うには、ご自身で再生を再起動してください |
|PLAY_ERR_HLS_KEY       | -2305 | HLS復号keyの取得に失敗しました |

#### 警告イベント
以下のイベントは、SDK内のイベントをお知らせするためにのみ使用されるため、無視してかまいません。

| イベントID                 |    数値  |  意味の説明                    |
| :-------------------  |:-------- |  :------------------------ |
| PLAY_WARNING_VIDEO_DECODE_FAIL   |  2101  | 現在のビデオフレームのデコードに失敗しました  |
| PLAY_WARNING_AUDIO_DECODE_FAIL   |  2102  | 現在のオーディオフレームのデコードに失敗しました  |
| PLAY_WARNING_RECONNECT           |  2103  | ネットワーク接続が切断されましたが、自動再接続が開始されました（再接続が3回を超えると、PLAY_ERR_NET_DISCONNECTが直接スローされます） |
| PLAY_WARNING_HW_ACCELERATION_FAIL|  2106  | ハードウェアデコードの開始に失敗しました。ソフトウェアデコードを使用してください   |

#### 接続イベント
サーバーへの接続に関するイベント、主にサーバー接続時間の測定や統計を行うために使用されています。

| イベントID                     |    数値  |  意味の説明                    |
| :-----------------------  |:-------- |  :------------------------ |
| PLAY_EVT_VOD_PLAY_PREPARED     |  2013    | プレーヤーは再生可能状態です。autoPlayがfalseに設定されている場合、再生を開始するにはこのイベントを受信した後にresumeを呼び出す必要があります|
| PLAY_EVT_RCV_FIRST_I_FRAME|  2003    | ネットワークが最初のレンダリング可能なビデオデータパッケージ（IDR）を受信しました  |


#### 画面イベント
以下のイベントは、画面変更情報の取得に使用されます。

| イベントID                                   | 数値   | 意味の説明       |
| ----------------------------- | ---- | ---------- |
| PLAY\_EVT\_CHANGE\_RESOLUTION | 2009 | ビデオ解像度の変更    |
| PLAY\_EVT\_CHANGE\_ROTATION   | 2011 | MP4ビデオの回転角度 |

#### ビデオ情報イベント
| イベントID                     |    数値  |  意味の説明                    |
| :-----------------------  |:-------- |  :------------------------ |
|TXLiveConstants.PLAY_EVT_GET_PLAYINFO_SUCC   | 2010 | 再生ファイル情報の取得に成功しました |

fileId方式によって再生し、リクエストが成功した場合（インターフェース：startPlay(TXPlayerAuthBuilder authBuilder)）、SDKはいくつかの情報を上位レイヤーに通知します。`TXLiveConstants.PLAY_EVT_GET_PLAYINFO_SUCC`イベントを受信後、paramを解析することでビデオ情報を取得できます。

|  ビデオ情報                                    | 意味の説明                                        |
| ------------------------------------------- | ---------------------------------------------- |
| EVT\_PLAY\_COVER\_URL                       | ビデオカバーアドレス                                   |
| EVT\_PLAY\_URL                              | ビデオ再生アドレス                                   |
| EVT\_PLAY\_DURATION                         | ビデオ時間                                       |
| EVT_TIME                                    | イベント発生時間                                   |
| EVT_UTC_TIME                                | UTC時間                                        |
| EVT_DESCRIPTION                             | イベントの説明                                       |
| EVT_PLAY_NAME                               | ビデオ名                                       |
| TXVodConstants.EVT_IMAGESPRIT_WEBVTTURL     | スプライトイメージweb vtt説明ファイルのダウンロードURLです。バージョン10.2以降でサポートしています |
| TXVodConstants.EVT_IMAGESPRIT_IMAGEURL_LIST | スプライトイメージ画像のダウンロードURLです。バージョン10.2以降でサポートしています            |
| TXVodConstants.EVT_DRM_TYPE                 | 暗号化タイプです。バージョン10.2以降でサポートされています                     |


onPlayEventによるビデオ再生プロセスにおける取得情報の例：

```java
mVodPlayer.setVodListener(new ITXVodPlayListener() {
    @Override
    public void onPlayEvent(TXVodPlayer player, int event, Bundle param) {
        if (event == TXLiveConstants.PLAY_EVT_VOD_PLAY_PREPARED) {
            // 準備が完了したイベントをプレーヤーが受信すると、この時点でpause、resume、getWidth、getSupportedBitratesなどのインターフェースを呼び出すことができます
        } else if (event == TXLiveConstants.PLAY_EVT_PLAY_BEGIN) {
            // 再生開始イベントの受信
        } else if (event == TXLiveConstants.PLAY_EVT_PLAY_END) {
            // 開始終了イベントの受信
        }
    }

    @Override
    public void onNetStatus(TXVodPlayer player, Bundle bundle) {
    }
});
```

[](id:status)

### 再生ステータスフィードバック（onNetStatus）
ステータスフィードバックは、0.5秒ごとに1回トリガーされますが、プッシャーの現在のステータスをリアルタイムにフィードバックすることが目的です。車のダッシュボードのように、SDK内の状況の一部を具体的に教えてくれるので、現在のビデオ再生状況などを把握することができます。
<table>
<thead><tr><th>評価パラメータ</th><th>意味の説明</th></tr>
<tr>
<td>NET_STATUS_CPU_USAGE</td><td>現在の瞬間的なCPU使用率</td>
</tr><tr>
<td>NET_STATUS_VIDEO_WIDTH</td><td>ビデオ解像度 - 幅</td>
</tr><tr>
<td>NET_STATUS_VIDEO_HEIGHT</td><td>ビデオ解像度 - 高さ</td>
</tr><tr>
<td>NET_STATUS_NET_SPEED</td><td>現在のネットワークデータ受信速度</td>
</tr><tr>
<td>NET_STATUS_VIDEO_FPS</td><td>現在のストリームメディアのビデオフレームレート</td>
</tr><tr>
<td>NET_STATUS_VIDEO_BITRATE</td><td>現在のストリームメディアのビデオビットレートです。単位はkbps</td>
</tr><tr>
<td>NET_STATUS_AUDIO_BITRATE</td><td>現在のストリームメディアのオーディオビットレートです。単位はkbps</td>
</tr><tr>
<td>NET_STATUS_VIDEO_CACHE</td><td>バッファ(jitterbuffer)サイズです。現在のバッファの長さは0で、ラグから遠くないことを意味しています</td>
</tr><tr>
<td>NET_STATUS_SERVER_IP</td><td>接続先サーバーIP</td>
</tr></table>
onNetStatusによるビデオ再生プロセスにおける取得情報の例：

```java
mVodPlayer.setVodListener(new ITXVodPlayListener() {
    @Override
    public void onPlayEvent(TXVodPlayer player, int event, Bundle param) {
    }

    @Override
    public void onNetStatus(TXVodPlayer player, Bundle bundle) {
        //現在のCPU使用率の取得
        CharSequence cpuUsage = bundle.getCharSequence(TXLiveConstants.NET_STATUS_CPU_USAGE);
        //ビデオ幅の取得
        int videoWidth = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_WIDTH);
        //ビデオ高さの取得
        int videoHeight = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_HEIGHT);
        //リアルタイムレートの取得。単位はkbps
        int speed = bundle.getInt(TXLiveConstants.NET_STATUS_NET_SPEED);
        //現在のストリームメディアのビデオフレームレートの取得
        int fps = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_FPS);
        //現在のストリームメディアのビデオビットレートを取得します。単位はkbps
        int videoBitRate = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_BITRATE);
        //現在のストリームメディアのオーディオビットレートを取得します。単位はkbps
        int audioBitRate = bundle.getInt(TXLiveConstants.NET_STATUS_AUDIO_BITRATE);
        //バッファ(jitterbuffer)サイズを取得します。現在のバッファの長さは0で、ラグから遠くないことを意味しています
        int jitterbuffer = bundle.getInt(TXLiveConstants.NET_STATUS_VIDEO_CACHE);
        //接続されているサーバーのIPアドレスの取得
        String ip = bundle.getString(TXLiveConstants.NET_STATUS_SERVER_IP);
    }
});
```

## シナリオ化機能

### 1、SDKベースのDemoコンポーネント

Tencent Cloudは、プレーヤーSDKをベースとして以下のような[プレーヤーコンポーネント](https://intl.cloud.tencent.com/document/product/266/33975)を開発しました。品質モニタリング、ビデオ暗号化、超高速HD(TESHD)、解像度切り替え、ミニウィンドウ再生などの機能を一体化し、あらゆるオンデマンド(VOD)、ライブストリーミング再生のシナリオに対応します。完備された機能をパッケージ化するとともに、上位層のUIを提供することで、市場で人気を博す各種ビデオアプリに引けを取らない再生ソフトウェアを短時間で作成することができます。

### 2、オープンソースGithub

Tencent Cloudは、プレーヤーSDKをベースとして、没入型ビデオプレーヤーコンポーネント、ビデオFeedストリーム、マルチプレーヤー再利用コンポーネントなどを開発しました。今後はバージョンアップを重ねながら、ユーザーシナリオに基づいたコンポーネントをご提供していく予定です。[Player_Android](https://github.com/LiteAVSDK/Player_Android)からダウンロードし、体験することができます。
