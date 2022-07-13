このドキュメントでは、モバイルライブストリーミングSDKを使用してライブブロードキャスト再生を実装する方法について紹介します。

## サンプルコード
開発者の導入フィードバックの高頻度問題について、Tencent Cloudはもっと簡潔なAPI-Exampleプロジェクトを提供し、開発者は迅速に関連APIの使用を理解することができますので、ご検討よろしくお願いします。

| 使用しているプラットフォーム |                         GitHubアドレス                          |
| :------: | :----------------------------------------------------------: |
|   iOS    | [Github](https://github.com/tencentyun/MLVBSDK/tree/master/iOS/MLVB-API-Example-OC) |
| Android  | [Github](https://github.com/tencentyun/MLVBSDK/tree/master/Android/MLVB-API-Example) |

## 準備作業
1. より良い製品体験のため、[CSS](https://intl.cloud.tencent.com/product/css)を有効にすることをお勧めします。CSSサービスを使用しない場合、このステップをスキップできます。
2. Android Studioをダウンロードします。[Android Studio公式サイト](https://developer.android.com/studio)にアクセスし、ダウンロードしてインストールすることができます。すでにダウンロードしている場合は、この手順をスキップできます。


## このドキュメントから把握できること
* AndroidプレーヤーSDKを統合する方法
* プレーヤーSDKを使ったライブブロードキャスト再生の方法
* プレーヤーSDKの基盤となる機能を使用したり多くのライブブロードキャスト再生機能の実現方法



## SDKの統合
### ステップ1：SDK開発パッケージをダウンロード
SDK開発パッケージをダウンロードし、SDK統合ガイドラインに従って、SDKをAppプロジェクトに組み込みます。


### ステップ2：Viewの追加
SDKは、デフォルトでビデオレンダリングのためのTXCloudVideoViewが提供されています。最初の手順では、レイアウト用のxmlファイルに次のコードを追加します：
```xml
<com.tencent.rtmp.ui.TXCloudVideoView
            android:id="@+id/video_view"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_centerInParent="true"
            android:visibility="gone"/>
```

### ステップ3：Playerの作成
ビデオクラウドSDKの**TXLivePlayer**モジュールは、ライブブロードキャスト再生機能を実装し、**setPlayerView**インターフェースを使用して、インターフェースに追加したばかりの**video_view**コントロールに関連付けます。
```java
//mPlayerViewはステップ1で追加したインターフェースviewです
TXCloudVideoView mView = (TXCloudVideoView) view.findViewById(R.id.video_view);

//playerオブジェクトを作成します
TXLivePlayer mLivePlayer = new TXLivePlayer(getActivity());

//キーとなるplayerオブジェクトとインターフェースview
mLivePlayer.setPlayerView(mView);
```

### ステップ4：再生を開始
```java
String flvUrl = "http://2157.liveplay.myqcloud.com/live/2157_xxxx.flv";
mLivePlayer.startPlay(flvUrl, TXLivePlayer.PLAY_TYPE_LIVE_FLV); //推奨FLV
```

| 選択可能な値                  | 列挙値 | 意味                               |
| ----------------------- | ------ | ---------------------------------- |
| PLAY_TYPE_LIVE_RTMP     | 0      | 渡したURLはRTMPのライブストリーミングアドレスです        |
| PLAY_TYPE_LIVE_FLV      | 1      | 渡したURLはFLVのライブストリーミングアドレスです         |
| PLAY_TYPE_LIVE_RTMP_ACC | 5      | 低レイテンシのリンクアドレス（マイク接続シーンのみに適用） |
| PLAY_TYPE_VOD_HLS       | 3      | 渡したURLはHLS (m3u8)の再生アドレスです  |


>?Appでは、ライブストリーミングビデオソースを再生するためにHLSを使用することは推奨されません（オンデマンドに適していますが）。レイテンシが高すぎるため、AppではLIVE_FLVまたはLIVE_RTMP再生プロトコルを使用することが推奨されます。

### ステップ5：再生の終了
再生が終了したら、特に次のstartPlayの前に**viewコントロールを破棄してください**。そうしないと、**大量のメモリリークやスプラッシュスクリーンの問題が発生します**。

また、再生インターフェースを終了する際には、**必ずレンダリングViewの`onDestroy()`関数**を呼び出すようにしてください。そうでない場合、**メモリリークや"Receiver not registered"**というアラームが発生する可能性があります。
```java
@Override
public void onDestroy() {
    super.onDestroy();
    mLivePlayer.stopPlay(true); // true は最後のフレームをクリアすることを意味します
    mView.onDestroy(); 
}
```

stopPlayのブール型パラメータは、「最後のフレームをクリアするかどうか」を意味します。以前のバージョンのRTMP SDKのライブストリーミングプレーヤーにはpauseという概念がなかったので、このブール値で最後のフレームの画面のクリアをコントロールします。

オンデマンド再生終了後も最後のフレームの画面を残したい場合は、再生終了イベントを受信してから何もしないで、デフォルトで最後のフレームで停止することができます。


## 機能使用
この節では、一般的なライブブロードキャスト再生機能の使用方法を紹介します。

### 1、画面調整
- **view：サイズと位置**
画面のサイズと位置を変更するには、**ステップ1**に追加したvideo_viewコントロールのサイズと位置を直接調整すればよいです。

- **setRenderMode：並べて表示または画像のサイズに合わせる**

| 選択可能な値                        | 意味                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| RENDER_MODE_FULL_FILL_SCREEN  | 画像を拡大や縮小せず、画面のいっぱいに広げられ、はみ出した部分が切れます。このモードでは画面に黒い隙間はありませんが、画像の一部が切れて表示されない場合があります |
| RENDER_MODE_ADJUST_RESOLUTION | 画像の最も長い辺に合わせて縦横の比率を保って拡大・縮小します。拡大・縮小後の幅と高さが表示領域を超えず、中央に表示されます。また画面に黒い隙間が残る場合があります |

- **setRenderRotation：画面回転**

| 選択可能な値                        | 意味                                                         |
| ------------------------- | ------------------------------------------ |
| RENDER_ROTATION_PORTRAIT  | 通常再生（Homeキーは画面の下にある）            |
| RENDER_ROTATION_LANDSCAPE | 画面を時計回りに270度回転（Homeキーは画面の左にある） |

```Java
// 塗りつぶしモードの設定
mLivePlayer.setRenderMode(TXLiveConstants.RENDER_MODE_ADJUST_RESOLUTION);
// 画面レンダリング方向の設定
mLivePlayer.setRenderRotation(TXLiveConstants.RENDER_ROTATION_LANDSCAPE);
```




### 2、再生の一時停止
ライブブロードキャスト再生の場合、本当の意味で一時停止するわけではありませんが、ライブストリーミングの一時停止は、**画面がフリーズする**と**音声がオフになる**だけで、クラウドのビデオソースは更新されているので、resumeを呼び出すと最新の時点から再生が開始されますが、オンデマンドとは大きく異なります（オンデマンドプレーヤーの一時停止や再開は、ローカルビデオファイルを再生する場合と同じように動作します）。

```java
// 一時停止
mLivePlayer.pause();
// 再開
mLivePlayer.resume();
```

### 3、メッセージ受信
この機能は、ストリーミングプッシュ側でいくつかのカスタムメッセージをオーディオビデオ回線とともに視聴者側に直接配信することができます。次のようなシナリオが適用されます：

- 冲頂大会：ストリーミングプッシュ側は**問題**を視聴者側に配信し、「音声-画像-問題」の完璧な同期を実現することができます。
- ショーライブ：ストリーミングプッシュ側で**歌詞**を視聴者側に配信し、リアルタイムで歌詞の効果を描くことができ、ビデオエンコードの品質低下の影響を受けることはありません。
- オンライン教育：ストリーミングプッシュ側で**レーザーポインター**と**落書き**操作を視聴者側に配信し、再生側でリアルタイムに円を描いたり、罫線を引くことができます。

この機能は、次の方法で使用できます：
- TXLivePlayConfigの**setEnableMessage**を**true**に設定します。
- TXLivePlayerは**TXLivePlayListener**経由でメッセージを受信しています。メッセージ番号：**PLAY_EVT_GET_MESSAGE（2012）**

```java
//Androidサンプルコード
    mTXLivePlayer.setPlayListener(new ITXLivePlayListener() {
        @Override
        public void onPlayEvent(int event, Bundle param) {
            if (event == TXLiveConstants.PLAY_ERR_NET_DISCONNECT) {
                roomListenerCallback.onDebugLog("[AnswerRoom] プル失敗：ネットワーク切断");
                roomListenerCallback.onError(-1, "ネットワーク切断、プル失敗");
            }
            else if (event == TXLiveConstants.PLAY_EVT_GET_MESSAGE) {
                String msg = null;
                try {
                    msg = new String(param.getByteArray(TXLiveConstants.EVT_GET_MSG), "UTF-8");
                    roomListenerCallback.onRecvAnswerMsg(msg);
                } catch (UnsupportedEncodingException e) {
                    e.printStackTrace();
                }
            }
        }
        @Override
        public void onNetStatus(Bundle status) {
        }
        });
```

### 4、スクリーンショット
**snapshot**を呼び出すことにより、現在のライブストリーミング画面から1つのフレーム画像をキャプチャすることができます。この機能は、現在のライブストリームのビデオ画面のみをキャプチャします。現在のインターフェース全体をキャプチャする必要がある場合は、AndroidのシステムAPIを呼び出してください。



```java
mLivePlayer.snapshot(new ITXSnapshotListener() {
    @Override
    public void onSnapshot(Bitmap bmp) {
        if (null != bmp) {
           //スクリーンショットbitmapとして取得します
        }
    }
});
```

###5、傍受録画
傍受録画はライブブロードキャスト再生シーンにおける拡張機能です。視聴者はライブストリーミングを視聴する際、録画ボタンをクリックすることでライブストリーミングの内容を録画し、動画配信プラットフォーム（Tencent Cloudのオンデマンドシステムなど）を通じて発表することができます。これにより、WeChatのモーメンツなどのSNS上でUGCメッセージの形で拡散することができます。



```java
//同期録画の進行状況と結果に使用されるITXVideoRecordListenerを指定します
mLivePlayer.setVideoRecordListener(recordListener);
//録画を開始します。録画ボタンの応答関数の中に入れます。現在はビデオソースの録画のみがサポートされています。弾幕メッセージなどは現在サポートされていません
mLivePlayer.startRecord(int recordType);
// ...
// ...
//録画を終了します。終了ボタンの応答関数の中にに入れます
mLivePlayer.stopRecord();
```

- 録画の進行状況は時間単位で、ITXVideoRecordListenerのonRecordProgressから通知されます。
- 記録されたファイルはMP4ファイルとして、ITXVideoRecordListenerのonRecordCompleteから通知されます。
- ビデオのアップロードと発行はTXUGCPublishによって実行され、具体的な使い方は[ショート動画 - ファイル発行](https://intl.cloud.tencent.com/document/product/1069/38026)をご参照ください。

### 6、シームレスなシャープネス切り替え
日常的に使う中で、ネットワークの状況はどんどん変化していきます。ネットワークが劣っている場合は、画質を適度に落としてラグを減らすのが望ましいです。逆に通信速度は良い場合、高画質で視聴できます。
従来のストリーム切り替え方式はもう一度の再生が一般的で、切り替えの前後で画面がつながらなかったり、黒画面になったり、カクカクしたりする問題が発生します。シームレス切り替え方式を使用すると、ライブストリーミングを中断することなく、別のストリームに直接切り替えることができます。

シャープネス切り替えはライブストリーミング開始後、任意の時間に呼び出すことができます。呼び出し方法は次のとおりです
```java
// 再生しているのはストリームhttp://5815.liveplay.myqcloud.com/live/5815_62fe94d692ab11e791eae435c87f075e.flvで、
// 現在、ビットレート900kbpsの新しいストリームに切り替えます
mLivePlayer.switchStream("http://5815.liveplay.myqcloud.com/live/5815_62fe94d692ab11e791eae435c87f075e_900.flv");
```

>?解像度のシームレス切り替え機能はPTSに合わせるようバックグラウンドで設定する必要があり、必要に応じて[チケットを提出](https://console.cloud.tencent.com/workorder)し、使用を申請することができます。

### 7、ライブストリーミングのタイムシフト視聴
タイムシフト機能はTencent Cloudが打ち出した特色のある機能で、ライブストリーミング中に、いつでも任意の放送履歴の時点まで遡って視聴することができ、その時点でライブストリーミングをずっと視聴することができます。ゲームや球技の試合など、インタラクティブ性は高くないが、視聴の連続性が強いシーンには最適です。

```java
// 放送のタイムシフト視聴を設定する前にstartPlayを呼び出します
// 再生の開始...
TXLiveBase.setAppID("1253131631"); // appIdの設定
mLivePlayer.prepareLiveSeek();     // ライブストリーミング開始時刻をバックグラウンドでリクエストします
```
正しく設定されている場合、PLAY_EVT_PLAY_PROGRESSイベントでは、現在の進行状況は0から始まるのではなく、実際のライブストリーミング開始時刻に基づいて計算されます。
seekメソッドを呼び出すと、履歴イベントポイントからライブストリーミングを再開できます
```java
mLivePlayer.seek(600); // 10分目から再生します
```

タイムシフトの導入には、次の設定をバックグラウンドでオンにしてください。

- 録画：タイムシフトの長さ、タイムシフトの保存の時間長さを設定します。
- 再生：タイムシフトしてメタデータを取得します。

タイムシフト機能はパブリックベータテスト申請フェーズにあり、必要に応じて[チケットを提出](https://console.cloud.tencent.com/workorder)し、使用を申請することができます。

### 8、遅延調整
Tencent CloudSDKのLVB機能は、ffmpegに基づいて二次的に開発されたものではなく、独自に開発した再生エンジンを採用しています。そのため、オープンソースプレーヤーに比べ、ライブストリーミングの遅延制御の面でより良いパフォーマンスを発揮しており、私達は3種類の遅延調整モードを提供し、それぞれにショー、ゲームおよび混合シーンに適しています。

- **3つのモードの特性比較**

| 制御モード | ラグ率     | 平均遅延 | 適用シナリオ             | 原理概要                                                 |
| -------- | ---------- | -------- | -------------------- | -------------------------------------------------------- |
| 快速モード | 流暢性が高い | 2s ～ 3s  | 美女ショー（冲頂大会） | 遅延制御にメリットがあり、遅延時間に敏感なシーンに適します       |
| 流暢モード | ラグ率が一番低い | >= 5s    | ゲームのライブ放送（企鵝電竞） | 超大ビットレートのゲームライブ放送（PUBGなど）に適しており、ラグ率が一番低い   |
| 自動モード | ネットワーク自己適応 | 2s ～ 8s  | 混合シーン             | 視聴者側のネットワーク速度がよければ、遅延が低い。視聴者のネットワーク速度が低ければ、遅延が高い |


-**3モードの呼び出しコード**
```java
TXLivePlayConfig mPlayConfig = new TXLivePlayConfig();
//
//自動モード
mPlayConfig.setAutoAdjustCacheTime(true);
mPlayConfig.setMinAutoAdjustCacheTime(1);
mPlayConfig.setMaxAutoAdjustCacheTime(5);
//
//快速モード
mPlayConfig.setAutoAdjustCacheTime(true);
mPlayConfig.setMinAutoAdjustCacheTime(1);
mPlayConfig.setMaxAutoAdjustCacheTime(1);
//
//流暢モード
mPlayConfig.setAutoAdjustCacheTime(false);
mPlayConfig.setCacheTime(5);
//
mLivePlayer.setConfig(mPlayConfig);
//設定が完了してから再生を開始します
```

>?ラグと遅延の最適化に関する技術知識については、[動画がカクカクするときの対処法](https://intl.cloud.tencent.com/document/product/1071/39362)をご覧ください。

### 9、超低遅延再生
**400ms程度の超低遅延再生**をサポートしていることは、Tencent Cloudのライブブロードキャスト再生プレーヤーの特徴です。**オンラインクレーンゲームやキャスターマイク接続**など、時間遅延が非常に要求される場面で使用することができます。この特徴について、次のことを知っておく必要があります：

- **この機能を有効にする必要はありません**
この機能はあらかじめ有効にする必要はありませんが、ライブストリームは必ずTencent Cloudに置かれる必要があり、クラウド業者を跨いで低遅延リンクを実現する難しさは技術面だけのものではありません。

- **再生アドレスには盗難防止チェーンが必要**
再生URLは通常のCDN URLではなく、必ず盗難防止チェーン署名が必要です。盗難防止チェーン署名の計算方法は[**txTimeとtxSecret**](https://intl.cloud.tencent.com/document/product/267/31560)をご参照ください。

- **再生タイプにACCを指定する必要があります**
startPlay関数を呼び出すときは、typeに**PLAY_TYPE_LIVE_RTMP_ACC**を指定してください。SDKはRTMP-UDPプロトコルを使用してライブストリームをプルします。

- **この機能には同時再生の制限があります**
現在、最大**10チャネル**の同時再生が可能で、この制限が設けられた理由は技術力の制限ではありません。その代わりに、インタラクティブなシーンでの使用のみを考え（例えば、マイク接続の場合はキャスターのみ、あるいはオンラインクレーンゲームのストリーミングではクレーンゲーム機を操作するプレイヤーのみに使用する）、むやみに低遅延を追求することによって不必要な費用の損失が発生することを避けてください（低遅延回線の価格はCDN回線よりも高い）。

- **Obsの遅延は基準未達です**
ストリーミングプッシュ側[TXLivePusher](https://intl.cloud.tencent.com/document/product/1071/38158)の場合は、[setVideoQuality](https://intl.cloud.tencent.com/document/product/1071/38158)を使用して、`quality`をMAIN_PUBLISHERまたはVIDEO_CHATに設定してください。Obsはストリーミングプッシュ側のオーバヘッドが大きく、低レイテンシの効果を果たすことが困難です。

- **この機能は再生時間に応じて課金されます**
本機能は再生時間に応じて課金されます。料金はストリーミングプルのチャネル数やオーディオ・ビデオ・ストリームのビットレートには関係ありません。価格は[価格一覧](https://intl.cloud.tencent.com/document/product/1071/38114)をご参照ください。


### 10、ビデオ情報の取得
プレーヤーSDKは、URL文字列を通じて映像を再生します。URL自身に映像情報が含まれていません。関連情報を取得するには、クラウド上のサーバーにアクセスして関連ビデオ情報をロードする必要があります。したがって、SDKはイベント通知としてのみビデオ情報をアプリケーションに送信できます。詳細は[イベントリスニング](#monitor)をご参照ください。

例えば、`onNetStatus`の`NET_STATUS_VIDEO_WIDTH`と`NET_STATUS_VIDEO_HEIGHT`を通じてビデオの幅と高さを取得します。具体的な使用方法については[ステータスフィードバック(onNetStatus)](#onNetStatus)をご参照ください。

[](id:monitor)
## イベント監視
`TXLivePlayer`オブジェクトに`TXLivePlayListener`をバインドすると、SDKの内部ステータス情報が`onPlayEvent`([イベント通知](#onPlayEvent))と`onNetStatus`([ステータスフィードバック](#onNetStatus))を介して通知されます。

[](id:onPlayEvent)
### イベント通知(onPlayEvent)
#### 1. 再生イベント
| イベントID                 |    数値  |  意味説明                |
| ---------------------------- | ---- | ---------------------------------------------------------- |
| PLAY\_EVT\_PLAY\_BEGIN       | 2004 | ビデオ再生開始                                               |
| PLAY\_EVT\_PLAY\_PROGRESS    | 2005 | ビデオ再生位置。現在の再生位置、ロードの進行状態と全体時間を通知します      |
| PLAY\_EVT\_PLAY\_LOADING     | 2007 | ビデオ再生のloading。再開可能な場合、その後にLOADING\_ENDイベントが発生します |
| PLAY\_EVT\_VOD\_LOADING\_END | 2014 | ビデオ再生のloadingが終了し、ビデオが引き続き再生します                        |

**PLAY_LOADINGを受信した後に再生画面を非表示にしないでください**：PLAY_LOADING -> PLAY_BEGINの時間は5sまたは5msのようなの不確定な長さであるため、LOADING中は画面を非表示にし、BEGIN中は画面を表示することを検討するユーザーもいます。この場合、特にライブシーンでは画面がちらつくことがあります。**動画再生画面に半透明のloading動画を重ねるのがお勧めです。**

#### 2. 終了イベント
| イベントID                 |    数値  |  意味説明                |
| :---------------------- | :---- | :----------------------------------------------------- |
| PLAY_EVT_PLAY_END       | 2006  | ビデオ再生終了                                           |
| PLAY_ERR_NET_DISCONNECT | -2301 | ネットワーク接続が切断され、何度も再接続しても回復できません。さらにリトライしたければ、手動で再起動後再生してください |
| PLAY_ERR_HLS_KEY        | -2305 | HLS復号キーの取得に失敗しました                                  |

**ライブストリーミングが終了したことをどう判断しますか？**
さまざまな標準に基づく実装の原理は異なりますが、多くのライブストリーミングでは終了イベント(2006)がスローされないことがよくあります。この場合に予想されるのは、キャスターがストリーミングプッシュを終了すると、SDKはすぐにデータストリームのプル失敗(WARNING_RECONNECT)を発見し、再試行を開始し、3回の再試行が失敗した後にPLAY_ERR_NET_DISCONNECTイベントがスローされます。

したがって、2006と−2301の両方が、ライブストリーミング終了の判定イベントとして監視してください。

#### 3. 警告イベント
これらのイベントは、SDK内のイベントの一部を知らせるためだけに使用されていますが、気にする必要はありません。

| イベントID                 |    数値  |  意味説明                |
| :-------------------------------- | :--- | :----------------------------------------------------------- |
| PLAY_WARNING_VIDEO_DECODE_FAIL   |  2101  | 現在のビデオフレームのデコードに失敗しました  |
| PLAY_WARNING_AUDIO_DECODE_FAIL   |  2102  | 現在のオーディオフレームのデコードに失敗しました  |
| PLAY_WARNING_RECONNECT            | 2103 | ネットワーク接続が切断され、自動再接続が有効にされています（再接続回数が3回を超えるとPLAY_ERR_NET_DISCONNECTがスローされます） |
| PLAY_WARNING_HW_ACCELERATION_FAIL|  2106  | ハードウェアデコードの開始に失敗しました。ソフトウェアデコードを使用してください   |

[](id:onNetStatus)
### ステータスのフィードバック(onNetStatus)
通知は1秒ごとにトリガされ、現在のプッシャ状態をリアルタイムでフィードバックすることを目的としています。これは自動車のダッシュボードのように、現在のSDK内部の特定の状況を知らせることができ、現在のビデオ再生の状態などを理解できるようになります。
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
<td>NET_STATUS_CACHE_SIZE</td><td>バッファ(jitterbuffer)のサイズ。バッファの現在の長さは0であれば、カクカクする可能性が高いことを意味します</td>
</tr><tr>
<td>NET_STATUS_SERVER_IP</td><td>接続されたサーバIP</td>
</tr></table>