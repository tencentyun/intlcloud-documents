
ここでは、ライブストリーミングやオンデマンド再生に使用するWeb (TCPlayer)に関するパラメータとAPIについてご説明します。このドキュメントは、Javascriptの基本的な知識を持つ開発者向けです。

## パラメータの初期化
プレーヤーの初期化には2つのパラメータが必要です。1つ目はプレーヤーコンテナID、2つ目は関数パラメータオブジェクトです。
```
var player = TCPlayer('player-container-id', options);
```

### optionsパラメータリスト
optionsオブジェクトの設定可能なパラメータ：

| 名称    | タイプ                      | デフォルト値                        |説明 |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
|  appID|  String |   なし |入力必須。|
|  fileID|  String|なし|入力必須。|
|  sources|  Array|なし|プレーヤー再生アドレスです。形式：[{ src: '//path/to/video.mp4', type: 'video/mp4' }]|
|  width|  String/Number|  なし| プレーヤー領域の幅を指定します。単位はピクセルで、必要に応じて設定します。プレーヤーサイズはCSSで制御できます。|
|  height |  String/Number|  なし|  プレーヤー領域の高さを指定します。単位はピクセルで、必要に応じて設定します。プレーヤーサイズはCSSで制御できます。|
|  controls|  Boolean|  true|  プレーヤーのコントロールバーを表示するかどうかです。|
|  poster|  String|  なし| カバー画像の完全なアドレスを設定します（アップロードされたビデオに生成されたカバー画像がある場合、生成されたカバー画像が最初に使用されます。詳細については、[VOD - ビデオ管理](https://intl.cloud.tencent.com/document/product/266/33896)をご参照ください。 |
|  autoplay|  Boolean|  false|  自動的に再生するかどうかです。|
|  playbackRates|  Array| [0.5，1，1.25，1.5，2]|  変速再生倍率オプションを設定します。HTML5再生モードでのみ有効です。|
|  loop|Boolean|  false|  ループ再生を行うかどうかです。|
|  muted|  Boolean|  false|  再生時にミュートするかどうかです。|
|  preload|  String|  auto|  プリロードを行うかどうかです。3つの属性「auto」、「meta」、「none」があり、モバイル端末ではシステムの制限により、autoは無効に設定されています。|
|  swf|  String|  なし|  FlashプレーヤーswfファイルのURLです。|
|  posterImage|  Boolean|  true|  カバーを表示するかどうかです。|
|  bigPlayButton|  Boolean|  true|  中央の再生ボタンを表示するかどうかです（ブラウザが乗っ取られた場合の埋め込み再生ボタンは削除できません）。|
|  language|  String|  "zh-CN" |  言語を設定します。オプション値は"zh-CN"/"en"です |
|  languages|  Object|  なし|  多言語辞書を設定します。|
|  controlBar|  Object|  なし|  コントロールバーの属性のパラメータの組み合わせを設定します。詳細は後述します。|
|  reportable|  Boolean |  true | データレポートをオンにするかどうかを設定します。|
|  plugins|  Object|  なし|  プラグインの機能属性のパラメータの組み合わせを設定します。詳細は後述します。|
|  hlsConfig|  Object| なし|  hls.jsの起動時の設定です。詳細は公式ドキュメント[hls.js](https://github.com/video-dev/hls.js/blob/master/docs/API.md#fine-tuning)をご参照ください。|
|  webrtcConfig|  Object|  なし|  webrtcの起動時の設定です。詳細は後述します。|


>! controls、playbackRates、loop、preload、posterImageこれらのパラメータは、ブラウザが乗っ取られた場合の再生ステータスでは無効です。

#### controlBarパラメータリスト
controlBarパラメータは、プレーヤーコントロールバーの機能を設定することができます。サポートされている属性は以下のとおりです。

| 名称    | タイプ                      | デフォルト値                        |説明 |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
|  playToggle| Boolean|  true|  再生と一時停止の切り替えボタンを表示するかどうかです。|
|  progressControl|  Boolean| true|  再生プログレスバーを表示するかどうかです。|
|  volumePanel|  Boolean|  true|  ボリューム制御を表示するかどうかです。|
|  currentTimeDisplay|  Boolean|  true|  ビデオの現在時刻を表示するかどうかです。|
|  durationDisplay|  Boolean|  true|  ビデオの長さを表示するかどうかです。|
|  timeDivider|  Boolean|  true|  時間の区切りを表示するかどうかです。|
|  playbackRateMenuButton|  Boolean|  true|  再生速度選択ボタンを表示するかどうかです。|
|  fullscreenToggle|  Boolean|  true|  フルスクリーンボタンを表示するかどうかです。|
|  QualitySwitcherMenuButton|  Boolean|  true|  解像度の切り替えメニューを表示するかどうかです。|

>! controlBarパラメータは、ブラウザが乗っ取られた場合の再生ステータスでは無効になります。

#### pluginsプラグインパラメーターリスト
pluginsパラメータは、プレーヤープラグインの機能を設定することができ、サポートされている属性は以下のとおりです。

| 名称    | タイプ                      | デフォルト値                        |説明 |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
|  ContinuePlay|  Object|  なし|  再生継続機能を制御します。サポートされている属性は以下のとおりです。<br><li>auto: Booleanは、再生中に自動再生継続するかどうかです<br><li>text: Stringプロンプトテキスト<br><li>btnText: Stringボタンテキスト|
| VttThumbnail | Object | なし | サムネイルの表示を制御します。サポートされている属性は以下のとおりです。<<br><li>vttUrl: String vttファイルの絶対アドレス、<br><li>basePath: String画像のパスを渡す必要があります。必須ではありませんが、渡されない場合、vttUrlのpath<br><li>imgUrl: String画像の絶対アドレスを使用します。必須ではありません |
| ProgressMarker | Boolean | なし | プログレスバー表示の制御 |
| DynamicWatermark | Object | なし | ダイナミックウォーターマークを制御します。サポートされている属性は以下のとおりです。<br><li>content: Stringテキストウォーターマークの内容を渡す必要があります。<br><li>speed: Numberウォーターマーク移動速度で、値の範囲は0～1です。必須ではありません |
| ContextMenu | Object | なし | オプション値は以下のとおりです。<br><li>mirror: Booleanは、イメージ表示をサポートするかどうかを制御します。<br><li>statistic: Booleanは、表示データプロンプトをサポートするかどうかを制御します。<br><li>levelSwitch: Objectは、解像度の切り替え時のテキストプロンプトを制御します。<br><li>&emsp;{<br><li>&emsp;&emsp;open: Booleanは、 プロンプトを有効にするかどうかです。<br><li>&emsp;&emsp;switchingText: String,解像度の切り替え時のプロンプトテキスト<br><li>&emsp;&emsp;switchedText: String,切り替え成功時のプロンプトテキスト<br><li>&emsp;&emsp;switchErrorText: String,切り替え失敗時のプロンプトテキスト<br><li>&emsp;}|


#### webrtcConfigパラメータリスト
webrtcConfigパラメータは、webrtc再生プロセスの動作表現を制御し、以下の属性をサポートします。

| 名称    | タイプ                      | デフォルト値                        |説明 |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
|  connectRetryCount| Number|  3|  SDKとサーバーの再接続回数|
|  connectRetryDelay|  Number| 1|  SDKとサーバーの再接続時の遅延|
|  receiveVideo|  Boolean|  true|  ビデオストリームをプルするかどうか|
|  receiveAudio|  Boolean|  true|  オーディオストリームをプルするかどうか|
|  showLog|  Boolean|  false|  コンソールにログを出力するかどうか|


<br>

## オブジェクト方法
プレーヤーリターンオブジェクトを初期化するメソッドのリスト

| 名称    | パラメータおよびタイプ                 | 戻り値およびタイプ                        |説明 |
|------------|-----------------------------------|-----------------------------------|---------------------------------------|
|  src()|  (String)|  なし|  再生アドレスを設定します。|
|  ready(function)|  (Function)|  なし|  プレーヤーの初期化が完了したときのコールバックを設定します。|
|  play()|  なし|  なし|  再生およびレジュームを再生します。|
|  pause()|  なし|  なし|  再生を一時停止します。|
|  currentTime(seconds)|  (Number)|  (Number)|  現在の再生タイムポイントを取得するか、またはビデオの長さを超えられない再生タイムポイントを設定します。|
|  duration()|  なし|  (Number)|  ビデオの長さを取得します。|
|  volume(percent)|  (Number)[0，1][オプション]|  (Number)/設定時には返しません|  プレーヤーのボリュームを取得または設定します。|
|  poster(src)|  (String)|  (String)/設定時には返しません|  プレーヤーカバーを取得または設定します。|
|  requestFullscreen()|  なし|  なし|  フルスクリーンモードにします。|
|  exitFullscreen()|  なし|  なし|  フルスクリーンモードを終了します。|
|  isFullscreen()|  なし|  Boolean| フルスクリーンモードになったかどうかを返します。|
|  on(type，listener)|  (String, Function)|  なし|  イベントをリスニングします。|
|  one(type，listener)|  (String, Function)|  なし|  イベントのリスニングします。イベント処理関数は最大1回のみ実行されます。|
|  off(type，listener)|  (String, Function)|  なし|  イベントリスニングのバインドを解除します。|
|  buffered()|  なし|  TimeRanges|  ビデオバッファの間隔を返します。|
|  bufferedPercent()|  なし|  値の範囲[0，1]|  ビデオの長さに対するバッファの長さのパーセンテージを返します。|
|  width()|  (Number)[オプション]|  (Number)/設定時には返しません|  プレーヤー領域の幅を取得または設定します。プレーヤーサイズがCSSによって設定されている場合、このメソッドは無効になります。|
|  height()|  (Number)[オプション]|  (Number)/設定時には返しません|  プレーヤー領域の幅を取得または設定します。プレーヤーサイズがCSSによって設定されている場合、このメソッドは無効になります。|
|  videoWidth()|  なし|  (Number)|  ビデオ解像度の幅を取得します。|
|  videoHeight()|  なし|  (Number)|  ビデオ解像度の高さを取得します。|
|  dispose()|  なし|  なし|  プレーヤーを破壊します。|

>! オブジェクトのメソッドは同期的に呼び出すことはできません。対応するイベント（loadedmetadataなど）がトリガーしてから呼び出す必要があります。ready、on、oneおよびoffは除きます。

## イベント
プレーヤーは返されたオブジェクトを初期化することでイベントをリスニングできます。事例：
```
var player = TCPlayer('player-container-id', options);
// player.on(type, function);
player.on('error', function(error) {
   // 処理
});
```
ここでのtypeはイベントのタイプであり、サポートされるイベントは以下のとおりです。

| 名称           | 説明                    |
|------------|---------------------------------|
|  play|  再生が開始され、play()メソッドが呼び出されたとき、またはautoplayがtrueに設定されたときにトリガーされます。このとき、pausedの属性はfalseになります。|
|  playing|  一時停止またはバッファによる停止後、再生が再開されたとき、paused属性がfalseの場合にトリガーされます。このイベントは通常、ビデオが実際に再生されるタイミングを示すために用いられ、playイベントは再生を開始するだけで、画面のレンダリングは開始しません。|
|  loadstart|  データロード開始時にトリガーされます。|
|  durationchange|  ビデオの長さのデータが変更したときにトリガーされます。|
|  loadedmetadata|  すでにロードされているビデオのmetadataです。|
|  loadeddata|  現在のフレームのデータがロードされていますが、ビデオの次のフレームを再生するのに十分なデータがない場合、このイベントがトリガーされます。|
|  progress|  メディアデータ取得時にトリガーされます。|
|  canplay|  プレーヤーがビデオ再生を開始できるようになったときにトリガーされます。|
|  canplaythrough|  プレーヤーが、バッファのために停止することなく、指定されたビデオの再生の継続が期待される場合にトリガーされます。|
|  error|  ビデオ再生時にエラーが発生した場合にトリガーされます。|
|  pause|  一時停止時にトリガーされます。|
|  ratechange|  再生速度に変更があったときにトリガーされます。|
|  seeked|  指定された再生位置の検索終了時にトリガーされます。|
|  seeking|  指定された再生位置の検索開始時にトリガーされます。|
|  timeupdate|  現在の再生位置の変更です。これは、currentTimeに変更があったと解釈することができます。|
|  volumechange|  ボリュームまたはmutedの属性値に変更があったときにトリガーされます。|
|  waiting|  再生の停止です。コンテンツの次のフレームが使用できない場合にトリガーされます。|
|  ended|  ビデオ再生が終了したときにトリガーされます。このとき、currentTime値はメディアリソースの最大値と等しくなります。|
|  resolutionswitching|  解像度の切り替えが進行中です。|
|  resolutionswitched|  解像度の切り替えが終了しました。|
|  fullscreenchange| フルスクリーンステータスへの切り替え時にトリガーされます。|
|  webrtcevent | 再生時のイベントの集合です。|
|  webrtcstats | webrtc再生時の統計情報です。|


### WebrtcEventリスト

プレーヤーは、webrtceventを介してwebrtcを配信するプロセスにおけるすべてのイベントを取得できます。事例：
```
var player = TCPlayer('player-container-id', options);
player.on('webrtcevent', function(event) {
   // コールバックパラメータeventからイベントのステータスコードと関連データを取得します
});
```
webrtceventのステータスコードは以下のとおりです

| ステータスコード | コールバックパラメータ | 説明 |
|------|-------|-------|
| 1001 | なし | プルが開始しました |
| 1002 | なし | サーバーに接続しました |
| 1003 | なし | ビデオ再生が開始されました |
| 1004 | なし | プルが停止し、ビデオ再生が終了しました |
| 1005 | なし | サーバーへの接続に失敗し、自動再接続の回復が開始されました |
| 1006 | なし | ストリームデータをブランクで取得します |
| 1007 | localSdp | シグナリングサーバーへのリクエストを開始します |
| 1008 | remoteSdp | シグナリングサーバーへのリクエストが成功しました |
| 1009 | なし | バッファ待機中のプルのラグ |
| 1010 | なし | プルのラグが終了し再生を再開しました |


## エラーコード
プレーヤーerrorイベントをトリガーすると、リスナー関数はエラーコードを返します。3桁以上のエラーコードは、メディアデータインターフェースのエラーコードです。エラーコードのリストは、以下のとおりです。

| 名称 | 説明                                           |
|------|----------------------------------------------|
| -1   | プレーヤーは使用可能なビデオアドレスを検出できませんでした。                  |
| -2   | ビデオデータ取得がタイムアウトしました。                               |
| 1    | ビデオデータのロード処理が中断されました。<br>考えられる原因：<br><li> ネットワークの接続が中断した。<br><li> ブラウザが異常終了した。<br>解決策：<br><li> ブラウザコンソールのネットワークリクエスト情報を調べて、ネットワークリクエストが正常かどうかを確認します。<br><li>再生フローを再実行します。                             |
| 2    | ネットワークの問題により、ビデオのロードに失敗しました。<br>考えられる原因：ネットワークの接続が中断した。<br>解決策:<br><li> ブラウザコンソールのネットワークリクエスト情報を調べて、ネットワークリクエストが正常かどうかを確認します。<br><li>再生フローを再実行します。                     |
| 3    | ビデオのデコード中にエラーが発生しました。<br>考えられる原因：ビデオデータが異常で、デコーダがデコードに失敗した。<br>解決策：<br><li> 再度トランスコードを行い、再生し、トランスコードの過程で発生した問題を解消します。<br><li> オリジナルビデオに問題がないことを確認します。 <br><li> テクニカルサポートにご連絡いただき、再生パラメータをお知らせいただければ、場所を特定し、トラブルシューティングを行います。                |
| 4    | サポートされていない形式、またはサーバーやネットワークに問題があるため、ビデオのロードができません。<br>考えられる原因：<br><li> ビデオデータを取得できないか、CDNリソースが存在していないか、ビデオデータが返されない。<br><li> 現在の再生環境では、このビデオ形式はサポートされていない。<br>解決策：<br><li> ブラウザコンソールのネットワークリクエスト情報を調べて、ネットワークリクエストが正常かどうかを確認します。<br><li> 対応するビデオ形式の再生スクリプトが、使用説明書に従ってロードされていることを確認します。<br><li> 現在のブラウザとページ環境が、再生するビデオ形式に対応しているかどうかを確認します。 <br><li> テクニカルサポートにご連絡いただき、再生パラメータをお知らせいただければ、場所を特定し、トラブルシューティングを行います。     |
| 5    | ビデオの復号中にエラーが発生しました。<br>考えられる原因：<br><li> 復号キーが正しくない。<br><li> リクエストキーインターフェースが異常を返した。<br><li> 現在の再生環境では、ビデオの復号はサポートされていません。<br>解決策：<br><li> キーが正しく、キーのインターフェースが正しく返ってくるかを確認します。<br><li> テクニカルサポートにご連絡いただき、再生パラメータをお知らせいただければ、場所を特定し、トラブルシューティングを行います。<br>                                  |
| 10   | オンデマンドメディアデータインターフェースのリクエストがタイムアウトしました。メディアデータを取得するときに、プレーヤーが3回再試行しても応答がない場合、このエラーがスローされます。<br>考えられる原因：<br><li> 現在のネットワーク環境では、メディアデータインターフェースに接続できないか、メディアデータインターフェースが乗っ取られている。<br><li> メディアデータインターフェースの異常。<br>解決策：<br><li> 弊社が提供するDemoページを開いて、正しく再生されるかどうか試してみてください。 <br><li>テクニカルサポートにご連絡いただき、再生パラメータをお知らせいただければ、場所を特定し、トラブルシューティングを行います。<br>                           |
| 11   | オンデマンドメディアデータインターフェースからデータが返されませんでした。メディアデータを取得するときに、プレーヤーが3回再試行してもデータが返されない場合、このエラーがスローされます。<br>考えられる原因：<br><li> 現在のネットワーク環境では、メディアデータインターフェースに接続できないか、メディアデータインターフェースが乗っ取られている。<br><li> メディアデータインターフェースの異常。<br>解決策：<br><li> 弊社が提供するDemoページを開いて、正しく再生されるかどうか試してみてください。 <br><li>テクニカルサポートにご連絡いただき、再生パラメータをお知らせいただければ、場所を特定し、トラブルシューティングを行います。<br>                           |
| 12   | オンデマンドメディアデータインターフェースから異常なデータが返されました。メディアデータを取得するときに、プレーヤーが3回再試行して解析不能なデータを返した場合、このエラーがスローされます。<br>考えられる原因：<br><li> 現在のネットワーク環境では、メディアデータインターフェースに接続できないか、メディアデータインターフェースが乗っ取られている。<br><li> 再生パラメータに誤りがあり、メディアデータインターフェースで処理できない。<br><li>メディアデータインターフェースの異常。<br>解決策：<br><li> 弊社が提供するDemoページを開いて、正しく再生されるかどうか試してみてください。 <br><li>テクニカルサポートにご連絡いただき、再生パラメータをお知らせいただければ、場所を特定し、トラブルシューティングを行います。<br>                           |
| 13   | 現在のプレーヤーで再生可能なビデオデータが検出されないので、ビデオのトランスコード操作を行ってください。 |
| 14   | HTML5 + hls.jsモードでhlsを再生すると、ネットワークの異常が発生します。異常の詳細はevent.sourceで確認できます。詳細については、hls.jsの公式ドキュメント[Network Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#network-errors)をご参照ください。 |
| 15   | HTML5 + hls.jsモードでhlsを再生すると、マルチメディアの異常が発生します。異常の詳細はevent.sourceで確認できます。詳細については、hls.jsの公式ドキュメント[Media Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#media-errors)をご参照ください。 |
| 16   | HTML5 + hls.jsモードでhlsを再生すると、多重化の異常が発生します。異常の詳細はevent.sourceで確認できます。詳細については、hls.jsの公式ドキュメント[Mux Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#mux-errors)をご参照ください。 |
| 17   | HTML5 + hls.jsモードでhlsを再生すると、その他の異常が発生します。異常の詳細はevent.sourceで確認できます。詳細については、hls.jsの公式ドキュメント[Other Errors](https://github.com/video-dev/hls.js/blob/master/docs/API.md#other-errors)をご参照ください。 |
| 10008| メディアデータサービスでは、再生パラメータに対応するメディアデータが見つかりませんでした。リクエストパラメータappID fileIDが正しいか、対応するメディアデータが削除されていないか確認してください。 |

