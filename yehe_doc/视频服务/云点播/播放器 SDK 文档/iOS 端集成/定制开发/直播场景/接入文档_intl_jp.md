このドキュメントでは、モバイルライブストリーミングSDKを使用してライブブロードキャスト再生を実装する方法について紹介します。

## サンプルコード
開発者の導入フィードバックの高頻度問題について、Tencent Cloudはもっと簡潔なAPI-Exampleプロジェクトを提供し、開発者は迅速に関連APIの使用を理解することができますので、ご検討よろしくお願いいたします。

| 使用しているプラットフォーム |                         GitHubアドレス                          |
| :------: | :----------------------------------------------------------: |
|   iOS    | [Github](https://github.com/tencentyun/MLVBSDK/tree/master/iOS/MLVB-API-Example-OC) |
| Android  | [Github](https://github.com/tencentyun/MLVBSDK/tree/master/Android/MLVB-API-Example) |

## 準備作業
1. より良い製品体験のため、[CSS](https://intl.cloud.tencent.com/product/css)を有効にすることをお勧めします。CSSサービスを使用しない場合、このステップをスキップできます。
2. Xcodeをダウンロードします。すでにダウンロードしている場合は、この手順をスキップして、App Storeに移動し、ダウンロードとインストールを実行できます。
3. Cocoapodsをダウンロードします。すでにダウンロードしている場合は、この手順をスキップして、[Cocoapods公式サイト](https://cocoapods.org/)に移動し、ガイドに従ってインストールできます。


## このドキュメントから把握できること
* iOSプレーヤーSDKを統合する方法
* プレーヤーSDKを使ったライブブロードキャスト再生の方法
* プレーヤーSDKの基盤となる機能を使用したり多くのライブブロードキャスト再生機能の実現方法

## SDKの統合
### ステップ1：SDK開発パッケージをダウンロード
SDK開発パッケージをダウンロードし、SDK統合ガイドラインに従って、SDKをAppプロジェクトに組み込みます。


### ステップ2：Playerの作成
ビデオクラウドSDKのTXLivePlayerモジュールは、オンデマンド再生機能の実装を行います。
```objectivec
TXLivePlayer _txLivePlayer = [[TXLivePlayer alloc] init];
```

### ステップ3：レンダリングView
次はプレーヤーのビデオ画面を表示する場所を探します。iOSでは基本的なインターフェースのレンダリング単位としてviewが使われていますので、viewを用意してレイアウトを調整してください。

```objectivec
// レンダリング領域を決定するviewをsetupVideoWidgetでプレーヤーにバインドします。最初のパラメータframeはバージョン1.5.2以降で廃止されました
[_txLivePlayer setupVideoWidget:CGRectMake(0, 0, 0, 0) containView:_myView insertIndex:0];
```

内部原理的には、プレーヤーは提供されたview（サンプルコードの\_myView）に画面を直接レンダリングするのではなく、このviewの上にOpenGLレンダリング用のサブビュー(subView)を作成します。

レンダリングされた画面のサイズを変更する場合は、一般的なviewのサイズと位置を変更してください。SDKでは、ビデオ画面がviewのサイズと位置に合わせてリアルタイムで調整されます。

![](https://qcloudimg.tencent-cloud.cn/raw/235b2e8e6fc3eb328ba05a4c5d251da7.jpg)
 <dx-alert infotype="explain" title="如何做动画？">
viewをアニメーションにするのは自由ですが、ここのアニメーションで変更するターゲット属性はframe属性ではなくtransform属性であることに注意してください。

```objectivec
  [UIView animateWithDuration:0.5 animations:^{
            _myView.transform = CGAffineTransformMakeScale(0.3, 0.3); // 1/3のサイズに缩小
        }];
```
</dx-alert>

### ステップ4：再生を開始
```objectivec
NSString* flvUrl = @"http://2157.liveplay.myqcloud.com/live/2157_xxxx.flv";
[_txLivePlayer startPlay:flvUrl type:PLAY_TYPE_LIVE_FLV];
```

| 選択可能な値                  | 列挙値 | 意味                               |
|---------|---------|---------|
| PLAY_TYPE_LIVE_RTMP     | 0      | 渡したURLはRTMPのライブストリーミングアドレスです        |
| PLAY_TYPE_LIVE_FLV      | 1      | 渡したURLはFLVのライブストリーミングアドレスです         |
| PLAY_TYPE_LIVE_RTMP_ACC | 5      | 低レイテンシのリンクアドレス（マイク接続シーンのみに適用） |
| PLAY_TYPE_VOD_HLS       | 3      | 渡したURLはHLS(m3u8)の再生アドレスです  |


<dx-alert infotype="explain" title="关于 HLS（m3u8）">
Appでは、ライブストリーミングビデオソースを再生するためにHLSを使用することは推奨されません（オンデマンドに適していますが）。レイテンシが高すぎるため、AppではLIVE_FLVまたはLIVE_RTMP再生プロトコルを使用することが推奨されます。
</dx-alert>

### ステップ5：再生の終了
再生の終了時に現在のUIを終了する場合は、**removeVideoWidget**を使用してviewコントロールを破棄してください。破棄しないと、メモリリークやスプラッシュスクリーンの問題が発生します。

```objectivec
// 再生の停止
[_txLivePlayer stopPlay];
[_txLivePlayer removeVideoWidget]; // viewコントロールを破棄することを忘れないでください
```

## 機能使用
この節では、一般的なライブブロードキャスト再生機能の使用方法を紹介します。


### 1、画面調整
- **view：サイズと位置**
画面のサイズと位置を変更する場合は、setupVideoWidgetのパラメータviewのサイズと位置を直接変更すると、SDKはビデオ画面を自分のviewのサイズと位置に合わせてリアルタイムで調整することができます。

- **setRenderMode：並べて表示or画像のサイズに合わせる**
<table>
<thead>
<tr>
<th>選択可能な値</th>
<th>意味</th>
</tr>
</thead>
<tbody><tr>
<td>RENDER_MODE_FILL_SCREEN</td>
<td>画像を拡大や縮小せず、画面のいっぱいに広げられ、はみ出した部分が切れます。このモードでは画面に黒い隙間はありませんが、画像の一部が切れて表示されない場合があります。</td>
</tr>
<tr>
<td>RENDER_MODE_FILL_EDGE</td>
<td>画像の最も長い辺に合わせて縦横の比率を保って拡大・縮小します。拡大・縮小後の幅と高さが表示領域を超えず、中央に表示されます。また画面に黒い隙間が残る場合があります。</td>
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



### 2、再生の一時停止
ライブブロードキャスト再生の場合、本当の意味で一時停止するわけではありませんが、ライブストリーミングの一時停止は、**画面がフリーズする**と**音声がオフになる**だけで、クラウドのビデオソースは更新されているので、resumeを呼び出すと最新の時点から再生が開始されますが、オンデマンドとは大きく異なります（オンデマンドプレーヤーの一時停止や再開は、ローカルビデオファイルを再生する場合と同じように動作します）。

```objectivec
// 一時停止
[_txLivePlayer pause];
// 再開
[_txLivePlayer resume];
```

### 3、メッセージ受信
この機能は、ストリーミングプッシュ側でいくつかのカスタムメッセージをオーディオビデオ回線とともに視聴者側に直接配信することができます。次のようなシナリオが適用されます：
（1） 冲頂大会：ストリーミングプッシュ側は<strong>問題</strong>を視聴者側に配信し、「音声-画像-問題」の完璧な同期を実現することができます。
（2） ショーライブ：ストリーミングプッシュ側で<strong>歌詞</strong>を視聴者側に配信し、リアルタイムで歌詞の効果を描くことができ、ビデオエンコードの品質低下の影響を受けることはありません。
（3） オンライン教育：ストリーミングプッシュ側で<strong>レーザーポインター</strong>と<strong>落書き</strong>操作を視聴者側に配信し、再生側でリアルタイムに円を描いたり、罫線を引くことができます。

この機能は、次の方法で使用できます：
- TXLivePlayConfigの**enableMessage**を**YES**に設定します。
- TXLivePlayerは**TXLivePlayListener**経由でメッセージを受信しています。メッセージ番号：**PLAY_EVT_GET_MESSAGE（2012）**

```objectiveC
 -(void) onPlayEvent:(int)EvtID withParam:(NSDictionary *)param {
    [self asyncRun:^{
        if (EvtID == PLAY_EVT_GET_MESSAGE) {
            dispatch_async(dispatch_get_main_queue(), ^{
                if ([_delegate respondsToSelector:@selector(onPlayerMessage:)]) {
                    [_delegate onPlayerMessage:param[@"EVT_GET_MSG"]];
                }
            });
        }
    }];
}
```

### 4、スクリーンショット
**snapshot**を呼び出すことにより、現在のライブストリーミング画面から1つのフレーム画像をキャプチャすることができます。この機能は、現在のライブストリームのビデオ画面のみをキャプチャします。現在のインターフェース全体をキャプチャする必要がある場合は、iOSのシステムAPIを呼び出してください。



### 5、傍受録画
傍受録画はライブブロードキャスト再生シーンにおける拡張機能です。視聴者はライブストリーミングを視聴する際、録画ボタンをクリックすることでライブストリーミングの内容を録画し、動画配信プラットフォーム（Tencent Cloudのオンデマンドシステムなど）を通じて発表することができます。これにより、WeChatのモーメンツなどのSNS上でUGCメッセージの形で拡散することができます。



```objectivec
// 次のコードは、ライブブロードキャスト再生シーンでの録画機能を示すために使用されます
//
// 同期録画の進行状況と結果に使用されるTXVideoRecordListenerを指定します
_txLivePlayer.recordDelegate = recordListener;
// 録画を開始します。録画ボタンの応答関数の中に入れます。現在はビデオソースの録画のみがサポートされています。弾幕メッセージなどは現在サポートされていません
[_txLivePlayer startRecord: RECORD_TYPE_STREAM_SOURCE]; 
// ...
// ...
//録画を終了します。終了ボタンの応答関数の中にに入れます
[_txLivePlayer stopRecord];                             
```
- 録画の進行状況は時間単位で、TXVideoRecordListenerのonRecordProgressから通知されます。
- 記録されたファイルはMP4ファイルとして、TXVideoRecordListenerのonRecordCompleteから通知されます。
- ビデオのアップロードと発行はTXUGCPublishによって実行され、具体的な使い方は[ショート動画 - ファイル発行](https://intl.cloud.tencent.com/document/product/1069/38016)をご参照ください。


### 6、シームレスなシャープネス切り替え
日常的に使う中で、ネットワークの状況はどんどん変化していきます。ネットワークが劣っている場合は、画質を適度に落としてラグを減らすのが望ましいです。逆に通信速度は良い場合、高画質で視聴できます。
従来のストリーム切り替え方式はもう一度の再生が一般的で、切り替えの前後で画面がつながらなかったり、黒画面になったり、カクカクしたりする問題が発生します。シームレス切り替え方式を使用すると、ライブストリーミングを中断することなく、別のストリームに直接切り替えることができます。

シャープネス切り替えはライブストリーミング開始後、任意の時間に呼び出すことができます。呼び出し方法は次のとおりです
```objectivec
// 再生しているのはストリームhttp://5815.liveplay.myqcloud.com/live/5815_62fe94d692ab11e791eae435c87f075e.flvで、
// 現在、ビットレート900kbpsの新しいストリームに切り替えます
[_txLivePlayer switchStream:@"http://5815.liveplay.myqcloud.com/live/5815_62fe94d692ab11e791eae435c87f075e_900.flv"];
```

>?解像度のシームレス切り替え機能はPTSに合わせるようバックグラウンドで設定する必要があり、必要に応じて[チケットを提出](https://console.cloud.tencent.com/workorder)し、使用を申請することができます。

### 7、ライブストリーミングのタイムシフト視聴
タイムシフト機能はTencent Cloudが打ち出した特色のある機能で、ライブストリーミング中に、いつでも任意の放送履歴の時点まで遡って視聴することができ、その時点でライブストリーミングをずっと視聴することができます。ゲームや球技の試合など、インタラクティブ性は高くないが、視聴の連続性が強いシーンには最適です。

```objectivec
// 放送のタイムシフト視聴を設定する前にstartPlayを呼び出します
// 再生の開始...
[TXLiveBase setAppID:@"1253131631"]; // appIdの設定
[_txLivePlayer prepareLiveSeek];     // ライブストリーミング開始時刻をバックグラウンドでリクエストします
```
正しく設定されている場合、PLAY_EVT_PLAY_PROGRESSイベントでは、現在の進行状況は0から始まるのではなく、実際のライブストリーミング開始時刻に基づいて計算されます。
seekメソッドを呼び出すと、履歴イベントポイントからライブストリーミングを再開できます
```objectivec
[_txLivePlayer seek:600]; // 10分目から再生します
```

タイムシフトの導入には、次の2つ設定をバックグラウンドでオンにしてください。

1. 録画：タイムシフトの長さ、タイムシフトの保存の時間長さを設定します。
2. 再生：タイムシフトしてメタデータを取得します。

>? タイムシフト機能はパブリックベータテスト申請フェーズにあり、必要に応じて[チケットを提出](https://console.cloud.tencent.com/workorder)し、使用を申請することができます。

### 8、遅延調整
Tencent CloudSDKのLVB機能は、ffmpegに基づいて二次的に開発されたものではなく、独自に開発した再生エンジンを採用しています。そのため、オープンソースプレーヤーに比べ、ライブストリーミングの遅延制御の面でより良いパフォーマンスを発揮しており、私達は3種類の遅延調整モードを提供し、それぞれにショー、ゲームおよび混合シーンに適しています。

- **3つのモードの特性比較**
<table>
<thead>
<tr>
<th>制御モード</th>
<th>ラグ率</th>
<th>平均遅延</th>
<th>適用ケース</th>
<th>原理概要</th>
</tr>
</thead>
<tbody><tr>
<td>快速モード</td>
<td>流暢性が高い</td>
<td>2s～ 3s</td>
<td>美女ショー（冲頂大会）</td>
<td>遅延制御にメリットがあり、遅延時間に敏感なシーンに適します </td>
</tr>
<tr>
<td>流暢モード</td>
<td>ラグ率が一番低い</td>
<td>&gt;= 5s</td>
<td>ゲームのライブ放送（企鵝電竞）</td>
<td>超大ビットレートのゲームライブ放送（PUBGなど）に適しており、ラグ率が一番低い</td>
</tr>
<tr>
<td>自動モード</td>
<td>ネットワーク自己適応</td>
<td>2s～8s</td>
<td>混合シーン</td>
<td>視聴者側のネットワーク速度がよければ、遅延が低い。視聴者のネットワーク速度が低ければ、遅延が高い</td>
</tr>
</tbody></table>

-**3モードの呼び出しコード**
```objectivec
TXLivePlayConfig*  _config = [[TXLivePlayConfig alloc] init];
//自動モード
_config.bAutoAdjustCacheTime   = YES;
_config.minAutoAdjustCacheTime = 1; 
_config.maxAutoAdjustCacheTime = 5;
//快速モード
_config.bAutoAdjustCacheTime   = YES;
_config.minAutoAdjustCacheTime = 1;
_config.maxAutoAdjustCacheTime = 1;
//流暢モード
_config.bAutoAdjustCacheTime   = NO;
_config.cacheTime              = 5;

[_txLivePlayer setConfig:_config];

//設定が完了してから再生を開始します
```

>? ラグと遅延の最適化に関する技術知識については、[動画がカクカクするときの対処法](https://intl.cloud.tencent.com/document/product/1071/39362)をご覧ください。

### 9、超低遅延再生
<strong>400ms</strong>程度の超低遅延再生**をサポートしていることは、Tencent Cloudのライブブロードキャスト再生プレーヤーの特徴です。<strong>オンラインクレーンゲーム</strong>や<strong>キャスターマイク接続</strong>など、時間遅延が非常に要求される場面で使用することができます。この特徴について、次のことを知っておく必要があります：

- **この機能を有効にする必要はありません**
この機能はあらかじめ有効にする必要はないが、ライブストリームは必ずTencent Cloudに置かれる必要があり、クラウド業者を跨いで低遅延リンクを実現する難しさは技術面だけのものではありません。

- **再生アドレスには盗難防止チェーンが必要**
再生URLは通常のCDN URLではなく、必ず盗難防止チェーン署名が必要です。盗難防止チェーン署名の計算方法は[txTime&txSecret](https://intl.cloud.tencent.com/document/product/267/31560)をご参照ください。

- **再生タイプにACCを指定してください**
startPlay関数を呼び出すときは、typeに**PLAY_TYPE_LIVE_RTMP_ACC**を指定する必要があります。SDKはRTMP-UDPプロトコルを使用してライブストリームをプルします。

- **この機能には同時再生の制限があります**
現在、最大10チャネルの同時再生が可能で、この制限が設けられた理由は技術力の制限ではありません。その代わりに、インタラクティブなシーンでの使用のみを考え（例えば、マイク接続の場合はキャスターのみ、あるいはオンラインクレーンゲームのストリーミングではクレーンゲーム機を操作するプレイヤーのみに使用する）、むやみに低遅延を追求することによって不必要な費用の損失が発生することを避けてください（低遅延回線の価格はCDN回線よりも高い）。

- **Obsの遅延は基準未達です**
ストリーミングプッシュ側[TXLivePusher](https://intl.cloud.tencent.com/document/product/1071/38157)の場合は、[setVideoQuality](https://intl.cloud.tencent.com/document/product/1071/38157)を使用して、`quality`をMAIN_PUBLISHERまたはVIDEO_CHATに設定してください。Obsはストリーミングプッシュ側のオーバヘッドが大きく、低レイテンシの効果を果たすことが困難です。

- **この機能は再生時間に応じて課金されます**
本機能は再生時間に応じて課金されます。料金はストリーミングプルのチャネル数やオーディオ・ビデオ・ストリームのビットレートには関係ありません。価格は[価格一覧](https://intl.cloud.tencent.com/document/product/1071/38114)をご参照ください。

### 10、ビデオ情報の取得
プレーヤーSDKは、URL文字列を通じて映像を再生します。URL自身に映像情報が含まれていません。関連情報を取得するには、クラウド上のサーバーにアクセスして関連ビデオ情報をロードする必要があります。したがって、SDKはイベント通知としてのみビデオ情報をアプリケーションに送信できます。詳細は[イベントリスニング](#monitor)をご参照ください。

例えば、`onNetStatus`の`NET_STATUS_VIDEO_WIDTH`と`NET_STATUS_VIDEO_HEIGHT`を通じてビデオの幅と高さを取得します。具体的な使用方法については[ステータスフィードバック（onNetStatus）](#onNetStatus)をご参照ください。

[](id:monitor)
## イベント監視
`TXLivePlayer`オブジェクトに`TXLivePlayListener`をバインドすると、SDKの内部ステータス情報が`onPlayEvent`([イベント通知](#onPlayEvent))と`onNetStatus`([ステータスフィードバック](#onNetStatus))を介して通知されます。

[](id:onPlayEvent)
### イベント通知（onPlayEvent）
#### 1. 再生イベント
| イベントID                 |    数値  |  意味説明                |
| :-------------------  |:-------- |  :------------------------ |
| PLAY_EVT_CONNECT_SUCC     |  2001    | サーバーが接続されました                |
| PLAY_EVT_RTMP_STREAM_BEGIN|  2002    | サーバーに接続され、ストリーミングプルを開始しました（RTMPアドレスが再生された場合にのみスローされます）。 |
| PLAY_EVT_RCV_FIRST_I_FRAME | 2003 | ネットワークが最初のレンダリング可能なビデオパケット（IDR）を受信しました                      |
|PLAY_EVT_PLAY_BEGIN    |  2004|  ビデオ再生開始。もしくるくると回る表示が出たら停止する必要があります |
|PLAY_EVT_PLAY_LOADING	|  2007|  ビデオ再生のloading。再開可能な場合、その後にBEGINイベントが発生します|
|PLAY_EVT_GET_MESSAGE	|  2012|  オーディオビデオストリームに含まれるメッセージを受信するために使用され、詳細は[メッセージ受信](#Message)をご参照ください|

- **PLAY_LOADING受信後に再生画面を非表示にしないでください**
PLAY_LOADING -> PLAY_BEGINの時間は5sまたは5msのようなの不確定な長さであるため、LOADING中は画面を非表示にし、BEGIN中は画面を表示することを検討する顧客もいます。この場合、特にライブシーンでは画面がちらつくことがあります。動画再生画面に半透明のloading動画を重ねるのがお勧めです。

#### 2. 終了イベント
| イベントID                 |    数値  |  意味説明                |
| :-------------------  |:-------- |  :------------------------ |
| PLAY_EVT_PLAY_END       | 2006  | ビデオ再生終了                                           |
| PLAY_ERR_NET_DISCONNECT | -2301 | ネットワーク接続が切断され、何度も再接続しても回復できません。さらにリトライしたければ、手動で再起動後再生してください |

- **ライブストリーミングが終了したことをどう判断しますか？**
さまざまな標準に基づく実装の原理は異なりますが、多くのライブストリーミングでは終了イベント（2006）がスローされないことがよくあります。この場合に予想されるのは、キャスターがストリーミングプッシュを終了すると、SDKはすぐにデータストリームのプル失敗（WARNING_RECONNECT）を発見し、再試行を開始し、3回の再試行が失敗した後にPLAY_ERR_NET_DISCONNECTイベントがスローされます。

 したがって、2006と-2301の両方が、ライブストリーミング終了の判定イベントとして監視してください。


#### 3. 警告イベント
これらのイベントは、ホワイトボックス化されたSDKの設計理念に基づいて、イベント情報を同期化しているだけですので、お客様は気にする必要はありません

| イベントID                 |    数値  |  意味説明                |
| :-------------------  |:-------- |  :------------------------ |
| PLAY_WARNING_VIDEO_DECODE_FAIL   |  2101  | 現在のビデオフレームのデコードに失敗しました  |
| PLAY_WARNING_AUDIO_DECODE_FAIL   |  2102  | 現在のオーディオフレームのデコードに失敗しました  |
| PLAY_WARNING_RECONNECT           |  2103  | ネットワーク接続が切断され、自動再接続が有効にされています（再接続回数が3回を超えるとPLAY_ERR_NET_DISCONNECTがスローされます）|
| PLAY_WARNING_RECV_DATA_LAG       |  2104  | 不安定なネットワークパケット：ダウンストリーム帯域幅が不足しているか、キャスター側からのストリーミングが不均一であることが原因であると考えられます|
| PLAY_WARNING_VIDEO_PLAY_LAG      |  2105  | 現在、ビデオ再生時にラグが発生しています|
| PLAY_WARNING_HW_ACCELERATION_FAIL|  2106  | ハードウェアデコードの開始に失敗しました。ソフトウェアデコードを使用してください   |
| PLAY_WARNING_VIDEO_DISCONTINUITY |  2107  | 現在のビデオフレームは連続しておらず、フレームが失われる可能性があります|
| PLAY_WARNING_DNS_FAIL            |  3001  | RTMP-DNS解決に失敗しました（RTMPアドレスが再生された場合にのみスローされます）|
| PLAY_WARNING_SEVER_CONN_FAIL     |  3002  | RTMPサーバー接続が失敗しました（RTMPアドレスが再生された場合にのみスローされます）|
| PLAY_WARNING_SHAKE_FAIL          |  3003  | RTMPサーバーのハンドシェイクが失敗しました（RTMPアドレスが再生された場合にのみスローされます）|

[](id:onNetStatus)
### ステータスのフィードバック(onNetStatus)
通知は1秒ごとにトリガされ、現在のプッシャ状態をリアルタイムでフィードバックすることを目的としています。これは自動車のダッシュボードのように、現在のSDK内部の特定の状況を知らせることができ、現在のビデオ再生の状態などを理解できるようになります。

|   評価パラメータ                   |  意味説明                   |
| :------------------------  |  :------------------------ |
| NET_STATUS_CPU_USAGE     | 現在の瞬時CPU使用率 |
| NET_STATUS_VIDEO_WIDTH | ビデオ解像度 - 幅 |
| NET_STATUS_VIDEO_HEIGHT| ビデオ解像度 - 高さ |
|	NET_STATUS_NET_SPEED     | 現在のネットワークデータの受信速度 |
|	NET_STATUS_NET_JITTER    | ネットワークのジッタ状況。ジッタが大きいほどネットワークが不安定になります |
|	NET_STATUS_VIDEO_FPS     | 現在のストリーミングメディアのビデオフレームレート    |
|	NET_STATUS_VIDEO_BITRATE | 現在のストリーミングメディアのビデオビットレート（kbps単位）|
|	NET_STATUS_AUDIO_BITRATE | 現在のストリーミングメディアのオーディオビットレート（kbps単位）|
|	NET_STATUS_CACHE_SIZE    | バッファ（jitterbuffer）のサイズ。バッファの現在の長さは0であれば、カクカクする可能性が高いことを意味します|
| NET_STATUS_SERVER_IP | 接続されたサーバIP |


