## 2021年12月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th> <th width="15%">発表時間</th> <th width="15%">関連ドキュメント</th>
</tr><tr>
<td>Version 9.4リリース</td>
<td>すべてのプラットフォーム：<ul style="margin:0">
<li>入室速度を向上させ、入室にかかる時間の変動を少なくしました。</li>
<li>音声スポットライト機能を追加しました。大規模音声マイク接続のシーンに適しており、大人数で同時にマイクをオンにするようなノイズのある環境下でも、主要なユーザーの音声にスポットを当てることができます。<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a0e6e6434aaa03ce878280125a9c0fa4b" target="_blank">setRemoteAudioParallelParams</a>インターフェースから設定が可能です。</li>
</ul>
<br>Windows: <ul style="margin:0">
オーディオゲインアルゴリズムを最適化し、一部のデバイスで発生する、ゲインが大きすぎるために雑音が目立つ問題を解決しました。
</ul>
<br>iOS: <ul style="margin:0">
24ビットwav形式のBGMファイルのサポートを追加しました。
</ul>
<br>Android: <ul style="margin:0">
<li>画面共有時のスクリーンキャプチャの解像度を調整し、常に画面の解像度に合わせることで、共有された画面に黒枠が出るなどの問題を回避しました。</li>
<li>ビデオハードウェアデコードの互換性を向上させ、一部の携帯電話で再生時のビデオ解像度が変化した際にブラックスクリーンが発生する可能性がある問題を解決しました。</li>
</ul>
<br>Android&iOS: <ul style="margin:0">
このバージョンは国家プライバシーセキュリティ基準の規定に適合し、Tencent社内での複数製品に対する検証を経ています。
</ul>
<br>Mac: <ul style="margin:0">
<li>システム音声キャプチャ<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486" target="_blank">startSystemAudioLoopback</a>のダブルサウンドチャンネルのサポートを追加しました。</li>
<li>スクリーンキャプチャ中にマウスキャプチャを有効にすると、CPUとメモリの使用率が高くなる問題を解決しました。</li>
</ul>
</td>
<td>2021-12-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>
</tr>
</table>



## 2021年11月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th> <th width="15%">発表時間</th> <th width="15%">関連ドキュメント</th>
</tr><tr>
<td>Version 9.3リリース</td>
<td>すべてのプラットフォーム：<ul style="margin:0">
<li>脆弱なネットワーク状況におけるビデオの秒速開始スピードを最適化しました。</li>
<li>脆弱なネットワークの制御ポリシーを最適化しました。同じシナリオでもよりスムーズです。</li>
<li>TCP伝送プロトコルに対するサポートを最適化しました。複雑なネットワーク環境により良く対応します。</li>
<li>スピードテスト機能を最適化し、現在のネットワーク帯域幅に対する検査をサポートしました。</li>
</ul></td>
<td>2021-11-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>
</tr>
</table>

## 2021年09月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th> <th width="15%">発表時間</th> <th width="15%">関連ドキュメント</th>
</tr><tr>
<td>Version 9.2リリース</td>
<td>すべてのプラットフォーム：<ul style="margin:0">
	<li>声のトーンを設定する機能を追加しました。</li>
	<li>脆弱なネットワーク環境でジッター防止アルゴリズムを最適化すると、ビデオ再生がよりスムーズになります。</li>
</ul><br>Windows: <ul style="margin:0">
	<li>TRTCAudioQualityMusicは、高音質シーンに適応エコーキャンセレーション機能を追加し、音質とエコーキャンセレーション強度のバランスを自動的に調整します。</li>
	<li>AGCアルゴリズムを最適化して、音量の小さすぎ・大きすぎといった問題の発生確率を低減します。</li>
</ul><br>Android&iOS: <ul style="margin:0">
	<li>Socks5プロキシをサポートしています。</li>
	<li>コーラスモードの3Aポリシーを最適化しました。</li>
</ul><br>Android: <ul style="margin:0">
	<li>ハードウェアデコードによって引き起こされるANRの問題を最適化しました。</li>
	<li>カメラのローカルプレビュー角度の互換性を最適化しました。</li>
	<li>最初のフレームの秒速開始速度を最適化しました。</li>
</ul></td>
<td>2021-09-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>
</tr><tr>
<td>Version 9.1リリース</td>
<td>すべてのプラットフォーム：<ul style="margin:0">
	<li>C++インターフェースはオーディオフレームのコールバック形式設定をサポートしています。 </li>
	<li>弱いネットワーク環境でのオーディオビデオエクスペリエンスを最適化しました。</li>
</ul><br>Windows: <ul style="margin:0">
	<li>ビデオ放送のac3形式のサポートを追加しました。</li>
	<li>カメラ情報で、サポートされている解像度リストの取得ができるようになりました。具体的には<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXDeviceManager__cplusplus.html#ad502f48cb2a4470943134e4b48904450">ITXDeviceCollection.getDeviceProperties</a>をご参照ください。</li>
	<li>Nvidia、Intel、AMDのハードウェアデコードをサポートしました。</li>
</ul><br>Mac: <ul style="margin:0">
ローカルメディアレコーディングのサポートを追加しました。
</ul><br>Android: <ul style="margin:0">
	<li>退室時のオーディオ状態の管理を最適化しました。</li>
	<li>オーディオキャプチャ起動失敗後の復元ロジックを最適化し、成功率を向上させました。</li>
	<li>特定の条件下でビデオ画面に白飛びが発生する問題を修正しました。</li>
</ul></td>
<td>2021-09-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>
</tr>
</table>


## 2021年08月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th> <th width="15%">発表時間</th> <th width="15%">関連ドキュメント</th>
</tr><tr>
<td>Version 9.0リリース</td>
<td>すべてのプラットフォーム：<ul style="margin:0">
<li>カスタムオーディオトラックの音量設定をサポートしています。詳細については、 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#ae0031e4af8bb120ef6de164d99886418">setMixExternalAudioVolume</a>をご参照ください。</li>
<li>ステータスコールバックは、オーディオとビデオのパケット損失率を区別できます。詳細については、 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCStatistic__cplusplus.html#structliteav_1_1TRTCRemoteStatistics" >TRTCRemoteStatistics</a>をご参照ください。</li>
<li>サブスクリプションプロセスを最適化し、手動サブスクリプションのインスタントブロードキャスティング速度をアップしました。</li>
<li>特定シナリオでのonExitRoomコールバック重複の問題を修復しました。</li>
</ul><br>iOS: <ul style="margin:0">
システムの収音量の設定をサポートしています。詳細については、<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afc45226807d84673bab78b21d1be54ae">setSystemAudioLoopbackVolume</a>をご参照ください。
</ul></td>
<td>2021-08-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>
</tr>
</table>

## 2021年07月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th> <th width="15%">発表時間</th> <th width="15%">関連ドキュメント</th>
</tr><tr>
<td>Version 8.9リリース</td>
<td>すべてのプラットフォーム：<ul style="margin:0">
<li>特定シナリオでの音声再生時に出現するガタツキの問題を最適化しました。</li>
<li>クラウドプロキシサポートを追加し、企業ファイアウォール内部の環境に対するセキュリティコンフィグレーションの親和性をより高めました。</li>
<li>インターフェースmuteLocalVideoとmuteRemoteVideoStreamにストリームタイプのサポートを追加しました。</li>
<li>WiFiルーターへのユーザーのネットワーク品質を判断するため、統計ステータスコールバックonStatisticsにローカルゲートウェイ遅延に対する統計gatewayRttを追加しました。</li>
<li>オーディオレコーディングインターフェースstartAudioRecordingは、より多くのオーディオ形式へのレコーディングをサポートしています。</li>
</ul><br>Android: <ul style="margin:0">
<li>画面のインスタントブロードキャスティング速度を最適化しました。</li>
<li>通話音声がよりクリアになるよう、オーディオ前処理アルゴリズムをアップグレードしました。</li>
<li>OpenGL環境をより柔軟に使用できるよう、カスタムレンダリングは外部GLContextの指定をサポートしています。</li>
</ul><br>Windows: <ul style="margin:0">
<li> NVIDIAプラットフォームのハードコーディングをサポートし、プッシュストリーミングのパフォーマンスを向上させました。</li>
<li>システム再生音声（startSystemAudioLoopback）収音時のスピーカーデバイスの指定をサポートしています。</li>
</ul></td>
<td>2021-07-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>
</tr>
</table>


## 2021年06月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th> <th width="15%">発表時間</th> <th width="15%">関連ドキュメント</th>
</tr><tr>
<td>Version 8.8リリース</td>
<td>すべてのプラットフォーム：<ul style="margin:0">
mixExternalAudioFrameの使いやすさを最適化したため、呼び出しのタイミングを完全に制御する必要がなくなりました。
</ul><br>Android&Mac&iOS: <ul style="margin:0">
オーディオ再生の外部接続や制御をサポートしています。API <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#addb4c87719393cd4c4765d66a8cd9803" target="_blank">enableCustomAudioRendering</a>をご参照ください。
</ul><br>Mac: <ul style="margin:0">
画面共有でマウスキャプチャを有効にする場合のCPUのオーバーヘッドを低減しました。
</ul><br>Windows: <ul style="margin:0">
<li/>より迅速かつタイムリーに調整を行えるよう、AGC音声ゲイン効果を最適化しました。
<li/>ウィンドウフィルタリングが有効になっている場合の画面共有のパフォーマンスオーバーヘッドを最適化しました。
</ul></td>
<td>2021-06-21</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>
</tr>
</table>

## 2021年05月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th> <th width="15%">発表時間</th> <th width="15%">関連ドキュメント</th>
</tr><tr>
<td>Version 8.7リリース</td>
<td>すべてのプラットフォーム：<ul style="margin:0">
<li>外部接続オーディオデバイスの異常検出を追加しました。onStatisticsコールバックを登録した後、<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCTypeDef__cplusplus.html#structtrtc_1_1TRTCLocalStatistics">TRTCLocalStatistics</a>のaudioCaptureStateを使用して、長時間のミュート、音割れ、異常な中断といった問題をリアルタイムで検出できます。</li>
<li>BGMリソース管理を最適化し、メモリ使用量を速やかに解放します。</li>
<li>プッシュ側がバックエンドに戻ってビデオのアップロードを一時停止すると、再生側は<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudCallback__cplusplus.html#a091f1c94ff1e2bc39c36e9d34285e87a">onUserVideoAvailable(false)</a> の通知を速やかに受信できます。</li>
</ul><br>Mac: <ul style="margin:0">
画面共有時のマウスキャプチャのCPUとメモリの使用量を最適化しました。
</ul><br>Windows: <ul style="margin:0">
ユーザー定義キャプチャはRGBA形式でのビデオデータの入力をサポートしています。
</ul></td>
<td>2021-05-25</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>
</tr><tr>
<td>Version 8.6リリース</td>
<td>すべてのプラットフォーム：<ul style="margin:0">
<li>ネットワークフロー制御アルゴリズムを最適化して、オーディオ・ビデオの送信品質をさらに向上させました。</li>
<li>ロールの切り替え、マイクのオン・オフ時のオーディオ再生のスムーズさを最適化しました。</li>
</ul><br>iOS&Mac&Windows: <ul style="margin:0">
音声処理モジュールを最適化して、SPEECHモードとDEFAULTモードの音声品質を向上させました。
</ul><br>iOS&Mac: <ul style="margin:0">
高CPUシナリオでのカスタムオーディオキャプチャの適応性を最適化しました。
</ul><br>iOS&Android: <ul style="margin:0">
デスクトップバージョンに合わせて、スクリーンキャプチャビデオのサブストリームを介した共有をサポートしています。
</ul><br>Windows: <ul style="margin:0">
メモリ割り当てロジックを最適化し、安定性を向上させました。
</ul><br>Mac: <ul style="margin:0">
Apple M1アーキテクチャのネイティブサポートを追加しました。
</ul></td>
<td>2021-05-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>
</tr></table>



## 2021年03月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th> <th width="15%">発表時間</th> <th width="15%">関連ドキュメント</th>
</tr><tr>
<td>Version 8.5リリース</td>
<td>すべてのプラットフォーム：<ul style="margin:0">
<li>ビデオ放送機能を追加しました。TXVODPlayerを使用してTRTCCloudとバインドし、オンデマンド再生中のコンテンツをTRTCのサブストリームプッシュで共有することができます。</li>
<li>サブストリームのユーザー定義キャプチャを追加しました。API<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a1d8de868187164e20d0e657e44da0bc6">sendCustomVideoData</a>をご参照ください。</li>
<li>カスタムサウンドミキサー機能を追加しました。自身のオーディオトラックをSDKのオーディオ処理フロー中にミキシングすることができます。SDKはまず2つのオーディオトラックをミキシングし、その後、同時に公開します。API<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a3c99feacd22af10926d5a521ca598ecd">mixExternalAudioFrame</a>をご参照ください。</li>
<li>ビデオのみのミクスストリーミング指定をサポートし、ミクスストリーミングの制御がさらに柔軟になりました。</li>
<li>ステータスのコールバックによりエンドツーエンド遅延が増加します。</li>
</ul>
<br>Windows: <ul style="margin:0">
スライドウィンドウを選択して画面共有を実行する時の、放映ウィンドウへの自動切り替えをサポートしています。
</ul>
<br>Mac: <ul style="margin:0">
<li>画面共有機能を最適化しました。共有ターゲットウィンドウ内で同時指定した他のウィンドウと共に共有することができます。API<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2e101f0ff00c8752eea1fa9a1a432233">addIncludedShareWindow</a>をご参照ください。</li>
<li>startSystemAudioLoopbackはダブルサウンドチャンネルをサポートしています。</li>
</ul>
</td>
<td>2021-03-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>
</tr></table>




## 2021年02月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th> <th width="15%">発表時間</th> <th width="15%">関連ドキュメント</th>
</tr><tr>
<td>Version 8.4リリース</td>
<td>すべてのプラットフォーム：<ul style="margin:0">
<li>ローカルのオーディオ・ビデオ録画機能を新規追加しました。キャスターはプッシュ中にローカルのオーディオおよびビデオからmp4ファイルを作成することができます。<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5075d55a6fc31895eedd5b23a1b8826b">startLocalRecording</a>をご参照ください。</li>
<li><a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb">Music</a>モードの音質を最適化し、cloubhouseのような音声ライブストリーミングシーンに適しています。</li>
<li>オーディオ・ビデオリンクのネットワーク耐性を最適化しました。著しく劣るネットワーク環境でも、そのうち70%のオーディオ・ビデオは比較的スムーズなままです。</li>
</ul>
<br>Windows: <ul style="margin:0">
<li>一部のシーンでのライブストリーミングの音質を最適化し、音声障害の問題を大幅に減少させました。</li>
<li>パフォーマンスを最適化しました。一部のユースケースでパフォーマンスが旧バージョンより20%～30%向上しました。</li>
<li>プロセスの音量調節機能を追加しました。<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXDeviceManager__cplusplus.html#af6722fa5e6e45738e007004c374948b1">setApplicationPlayVolume</a>を使用すると、システムの音量ミキサーの音量を設定することができます。</li>
</ul>
<br>Mac: <ul style="margin:0">
<li>Macのオペレーティングシステムの出力音声のキャプチャのサポートが開始されました。これはWindows端末と同一のSystemLoopback機能で、この機能を使用するとSDKは現在のシステムの音声をキャプチャすることができます。この機能を有効化すると、キャスターは他のユーザーに対して音楽または映画ファイルのライブストリーミングを実行することが容易になります。</li>
<li>画面共有ではローカルプレビュー機能のサポートを開始しました。画面共有のプレビュー内容を、小さなウィンドウを介してユーザーに表示することができます。</li>
</ul>
</td>
<td>2021-02-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>
</tr></table>



## 2021年01月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th> <th width="15%">発表時間</th> <th width="15%">関連ドキュメント</th>
</tr><tr>
<td>Version 8.3リリース</td>
<td>すべてのプラットフォーム：<ul style="margin:0">自身でビデオデータを収集し、同時にTRTC SDK標準搭載のオーディオモジュールを使用する必要がある場合は、音声と画像が同期しないという問題が生じる可能性があります。これはSDK内部のタイムラインに固有の制御ロジックがあるためで、このために<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ae5f2a974fa23954c5efd682dc464cdee">generateCustomPTS</a>インターフェースを提供しています。収集した1フレームのビデオ画面でこのインターフェースを呼び出して現在のPTS（タイムスタンプ）を記録し、その後<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a76e8101153afc009f374bc2b242c6831">sendCustomVideoData</a>を呼び出して、このタイムスタンプが得られれば、音声と画像の同期を良好に保証することができます。</ul>
<br>iOS &amp; Android &amp; Mac：<ul style="margin:0">オーディオモジュールの最適化によって、<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab8f8aaa19d70c6a2c9d62ecceb6e974d">enableCustomAudioCapture</a>を使用してオーディオデータを収集しSDKに送信し処理するときにも、SDKが良好なエコー抑制効果およびノイズ低減効果を維持できるようになります。</ul>
<br>iOS &amp; Android：<ul style="margin:0">TRTC SDKに基づいて自身の音声特殊効果及び音声処理のロジックを継続して強化する必要がある場合は、8.3バージョンを使用すればさらに簡単にできます。これは<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4b58b1ee04d0c692f383084d87111f86">setCapturedRawAudioFrameDelegateFormat</a>などのインターフェースによって、オーディオサンプルレート、オーディオサウンドチャンネル数およびサンプリングポイントなどのオーディオデータのコールバック形式を設定し、自身でお気に入りのオーディオ形式でこれらのオーディオデータを処理できるためです。</ul>
<br>Windows：<ul style="margin:0">SDKバージョンはドメイン名形式のSocks5プロキシアドレスへのサポートを強化しました。</td>
<td>2021-01-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>
</tr></table>


## 2020年12月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th> <th width="15%">発表時間</th> <th width="15%">関連ドキュメント</th>
</tr><tr>
<td>Flutter SDKのリリース</td>
<td>この <a href="https://pub.dev/packages/tencent_trtc_cloud">Flutter SDK</a> はTencent Real-Time CommunicationのiOS、AndroidプラットフォームのSDKをベースにパッケージ化したものです。</td>
<td>2020-12-30</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39243">Demoクイックスタート（Flutter）</a></td>
</tr><tr>
<td>Version 8.2リリース</td>
<td>
iOS&Android：<ul style="margin:0">ローカルで収集したものと再生したすべてのオーディオデータをミキシングするコールバックを追加しました。ローカルでのオーディオレコーディングがさらに使いやすくなります。</ul>
<br>Android: <ul style="margin:0">
	<li/>ビデオレンダリングコンポーネントTXCloudVideoViewは、<code>addVideoView(new TextureView(getApplicationContext()))</code>インターフェースを介してTextureViewを使用したローカルレンダリングをサポートしています。
	<li/>カスタムレンダリングのコールバックはRGBA形式のビデオデータをサポートしています。
	</li>オンラインライブストリーミングエンコードの品質を最適化し、ビデオ画面をさらに鮮明にします。
</ul>
<br>Mac&iOS：<ul style="margin:0">カスタムレンダリングモードでもTRTCCloud.snapshotVideoを呼び出してビデオストリームの画像をキャプチャすることができます。</ul>
<br>Windows: <ul style="margin:0">
	<li/>ローカルカメラによるリモートビデオストリームのスクリーンキャプチャの収集および再生をサポートしています。<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a8cf480979530c705c04d3c1715787f6c">ITRTCCloud.snapshotVideo</a>をご参照ください。
	<li/>画面共有は、addExcludedShareWindowインターフェースおよびaddIncludedShareWindowインターフェースによって、指定したウィンドウを排除または強制的に含むことをサポートすることで、よりフレキシブルな画面共有機能を実現します。
	<li/>エコー除去アルゴリズムを最適化し、エコー除去効果をさらに向上させます。
</ul>
</td>
<td>2020-12-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>
</tr><tr>
<td>Version 8.1リリース</td>
<td>
すべてのプラットフォーム：<ul style="margin:0">
	<li/>統計情報（onStatistics）でリモートビデオラグ関連の統計指標を追加しました。
	<li/>音量調節インターフェースsetAudioPlayoutVolume（100-150）によって音声のゲイン効果をサポートしています。
	<li/>イヤホン装着時の音声処理アルゴリズムを最適化して音声の音質を向上させます。
</ul>
<br>iOS&Android：<ul style="margin:0"> setLocalVideoProcessListenerインターフェースを追加し、サードパーティの美顔SDKの統合をより良好にサポートできるようになりました。
</ul>
<br>Android：<ul style="margin:0">オーディオの前処理アルゴリズムを最適化し、音質に対する3Aアルゴリズムの影響を低下させます。
</ul>
<br>Windows: <ul style="margin:0">
 C# 最新版APIに同期してアップグレードしました。
</ul>
</td>
<td>2020-12-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>
</tr>
</table> 

##  2020年11月
<table>
<tr><th width="20%">ダイナミックネーム</th><th width="50%">動的記述</th><th width="15%">発表時間</th>  <th width="15%">関連ドキュメント</th> 
<tr>
<td>Version 8.0リリース</td>
<td>
すべてのプラットフォーム：<ul style="margin:0">
	<li/>C++の統一APIを追加しました。 cpp_interface/<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html">ITRTCCloud.h</a>をご参照ください。
	- 文字列によるルーム番号をサポートしています。TRTCParams.strRoomIdをご参照ください。
	<li/>TXDeviceManagerデバイス管理タイプを追加しました。
	<li/>API TRTCCloud.switchRoomを追加しました。収集を止めずに、直接ルームを切り替えできるようになりました。
	<li/>リモートビデオ画面のレンダリングを開始する、API TRTCCloud.startRemoteViewを追加しました。
	<li/>リモートビデオ画面のレンダリングを停止する、API TRTCCloud.stopRemoteViewを追加しました。
	<li/>デバイス管理タイプを取得する、API TRTCCloud.getDeviceManagerを追加しました。
	<li/>ローカルオーディオの収集およびアップストリームを有効にする、API TRTCCloud.startLocalAudioを追加しました。
	<li/>リモート画像のレンダリング設定を行う、API TRTCCloud.setRemoteRenderParamsを追加しました。
	<li/>ローカル画像のレンダリング設定を行う、API TRTCCloud.setLocalRenderParamsを追加しました。
	<li/>手動受信モードでロール切り替え時のインスタントブロードキャスティング効果を最適化しました。
	<li/>オーディオ受信ロジックを最適化して音声効果を向上させました。
	<li/>sendCustomCmdMsgの信頼性を最適化しました。
</ul>
<br>Android: <ul style="margin:0">
	ソフトウェアとハードウェアデコードを切り替えるためのロジックを最適化しました。
</ul>
<br>Windows: <ul style="margin:0">
	<li/>System loopbackオーディオ収集音質およびエコー除去効果を最適化しました。
	<li/>オーディオデバイス選択ロジックを最適化し、無音声の割合を低下させました。
	<li/>二者間通話時の切断効果を最適化しました。
</ul>
</td>  
<td>2020-11-13</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>
</tr><tr>
<td>課金の変更</td>
<td>MCUクラスターを使用してCloud MixTranscodingを行うサービスが商業的な課金を正式に開始します。
</td>
<td>2020-11-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/38929">Cloud MixTranscodingの課金説明</a></td>
</tr>
</table> 

## 2020年10月
<table>
<tr><th width="20%">ダイナミックネーム</th><th width="50%">動的記述</th><th width="15%">発表時間</th>  <th width="15%">関連ドキュメント</th> 
<tr>
<td>Version 7.9リリース</td>
<td>
すべてのプラットフォーム：<ul style="margin:0">
	<li/>暗号化のカスタマイズをサポートして、ユーザーはエンコード後のオーディオ、ビデオのデータについて公開されたC言語インターフェースを介して二次処理を行うことができます。
	<li/>TRTCRemoteStatisticsにオーディオラグ情報コールバックのaudioTotalBlockTimeおよびaudioBlockRateを追加しました。
	<li/>マニュアル閲覧モードで、視聴者とキャスターのロールの相互切り替え時の音声のスムーズさを最適化しました。
	<li/>オーディオビデオ通話中の脆弱なネットワーク耐性を最適化しました。良好でないネットワーク環境でより良質なオーディオストリームのスムーズさが持てます。
</ul>
<br>Android: <ul style="margin:0">
	<li/>大部分のAndroidモデルにインイヤーモニタリング効果の最適化を行い、インイヤーモニタリングのディレイをより快適なレベルに引き下げました。
	<li/>Musicモード（startLocalAudio時に指定）でのP2Pディレイをさらに最適化しました。
</ul>
<br>iOS: <ul style="margin:0">
オーディオモジュールの起動速度を最適化して、最初のオーディオフレームがより速く収集され、配信できるようにしました。
</ul>
<br>Mac: <ul style="margin:0">
画面共有はフィルター選定したウィンドウをサポートし、ユーザーは自身で共有したくないウィンドウを排除できることから、ユーザーのプライバシーをより良好に保護することができます。
</ul>
<br>Windows: <ul style="margin:0">
	<li/>画面共有は、「共有中」の表示枠を示す色および枠線の幅の設定をサポートしています。
	<li/>画面共有はすべてのデスクトップ画面を共有するとき、高性能モードを有効にすることをサポートしています。
	<li/>システムループバックのエコー除去アルゴリズムを最適化して、システムループバック（SystemLoopback）を起動したとき、より良好なエコー除去機能を持たせました。
	<li/>画面共有機能のウィンドウキャプチャの遮蔽対策機能を最適化し、フィルターウィンドウの設定をサポートしています。
</ul>
</td>
<td>2020-10-27</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>
</tr>
</table> 

## 2020年09月
<table>
<tr><th width="20%">ダイナミックネーム</th><th width="50%">動的記述</th><th width="15%">発表時間</th>  <th width="15%">関連ドキュメント</th> 
<td>Version 7.8リリース</td>
<td>
Android: <ul style="margin:0">
<li>代替画像のプッシュをサポートしています。使用方法は <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a78195189ea5f3db9a05338f585bb925d">TRTCCloud.setVideoMuteImage</a>をご参照ください。
<li>音声のルーティングポリシーを最適化しました。イヤホン装着時に音声がイヤホンからのみ再生されるようサポートしています。
<li>一部システムで低レイテンシーでのキャプチャ再生をサポートして、Androidシステムの通話遅延を低減させました。
<li>VODPlayerおよびtrtcの同時使用をサポートし、さらにエコー除去をサポートしています。
</ul>
<br>iOS: <ul style="margin:0">
VODPlayerおよびtrtcの同時使用をサポートし、さらにエコー除去をサポートしています。
</ul>
<br>iOS&Mac: <ul style="margin:0">
代替画像のプッシュをサポートしています。使用方法は <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ad730c168c066599b6c4c987fd7b7c3a2">TRTCCloud.setVideoMuteImage</a>をご参照ください。
</ul>
<br>Mac: <ul style="margin:0">
<li>Mac：システム音量変化コールバックを追加しました。詳細については <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#ad87c12c924b781b3b8429f8e8aafc338">TRTCCloudDelegate.onAudioDevicePlayoutVolumeChanged</a>をご参照ください。
</ul>
<br>Windows: <ul style="margin:0">
<li>スクリーン間で指定したエリアの画面共有をサポートします。
<li>ウィンドウ共有を追加し、指定したウィンドウをフィルターする遮蔽対策をサポートしています。詳細については <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ac2a8a65dc2c1d0e4ffbd89eeae768fff">TRTCCloud.addExcludedShareWindow</a> および <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a0bbbff5ea3cd764dbaaad0db887760bf">TRTCCloud.removeExcludedShareWindow</a>をご参照ください。
<li>システム音量変化コールバックを追加しました。詳細については<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#a39cf2644243dceaccd82933f11f4db12">ITRTCCloudCallback.onAudioDevicePlayoutVolumeChanged</a>をご参照ください。
<li>バーチャルカメラe2eSoft Vacmと互換性を持たせました。
<li>startLocalPreviewとstartCameraDeviceTestを同時に呼び出せるようにしました。
<li>画面共有が主経路を経由するのをサポートすると同時に、startLocalPrevieを呼び出してローカルプレビューを開始します。
<li>SDK内部の再生バッファに起因するオーディオディレイが大きくなる問題を低減させました。
<li>オーディオ起動ロジックを最適化して、再生のみの状態でマイクを占有しないようにしました。
</ul>
</td>
<td>2020-09-29</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>
<tr></tr> 
<tr>
<td>Version 7.7リリース</td>
<td>
すべてのプラットフォーム：<ul style="margin:0">
パス（画面共有のこと）のインスタントブロードキャスティングの速度を最適化しました。
</ul>
<br>iOS: <ul style="margin:0">
内部スレッドモデルを最適化しました。30チャネル以上で同時再生するシナリオでの操作の安定性を向上させます。
</ul>
<br>iOS&Android: <ul style="margin:0">
<li>Audioモジュールの性能を最適化しました。最初のフレームの収集ディレイを向上させたことで、新バージョンでは最初のオーディオフレームをより速く取得できます。
<li>オンデマンドプレーヤー（VodPlayer）およびTRTCを同時使用するときの音量および音質表現を最適化しました。
<li>wavオーディオ形式のBGMおよび音響効果ファイルへのサポートを強化しました。
</ul>
<br>Windows: <ul style="margin:0">
<li>ローエンドのカメラでのCPU使用率が高すぎる問題を最適化しました。
<li>複数のUSBカメラおよびマイクの互換性を最適化して、デバイスのアクティブ化の成功率を向上させました。
<li>カメラおよびマイクデバイスの選択ポリシーを最適化して、カメラまたはマイクを使用中に抜き差しすることでキャプチャに不具合が生じる問題を回避させました。
</ul>
</td>
<td>2020-09-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>
</tr>
</table>


## 2020年08月
<table>
<tr><th width="20%">ダイナミックネーム</th><th width="50%">動的記述</th><th width="15%">発表時間</th>  <th width="15%">関連ドキュメント</th> 
<tr>
<td>Version 7.6リリース</td>
<td>
すべてのプラットフォーム：<ul style="margin:0">
<li>enterRoomのプロトコルポリシーを最適化してルーム追加速度を引き上げ、成功率を高めました。
<li>複数のオーディオを同時閲覧するときの全体性能の消耗およびラグの問題を最適化しました。
</ul>
<br>Android: <ul style="margin:0">
<li> TRTCCloudListenerにonCapturedRawAudioFrameコールバックを追加し、他のいくつかのコールバック関数名を修正しました。順次onLocalProcessedAudioFrame、onRemoteUserAudioFrameとonMixedPlayAudioFrameに修正します。
</ul>
<br>iOS: <ul style="margin:0">
<li> Viewレンダリング領域のリアルタイム調整のエクスペリエンスを最適化するために、updateLocalViewとupdateRemoteViewインターフェースを追加しました。
<li> TRTCCloudDelegateにonCapturedRawAudioFrameコールバックを追加し、他のいくつかのコールバック関数名を修正しました。順次onLocalProcessedAudioFrame、onRemoteUserAudioFrameとonMixedPlayAudioFrameに修正します。
</ul>
<br>Windows: <ul style="margin:0">
<li> HWNDタイプのレンダリングウィンドウのリアルタイム調整のエクスペリエンスを最適化するために、updateLocalViewとupdateRemoteViewインターフェースを追加しました。
<li>現在のWindowsPCがミュートに設定されているかどうかを取得するため、getCurrentMicDeviceMuteインターフェースを追加しました。
<li>現在のWindowsPCをグローバルミュートとして設定するため、setCurrentMicDeviceMuteインターフェースを追加しました。
</ul>
<br>Mac: <ul style="margin:0">
<li> Viewレンダリング領域のリアルタイム調整のエクスペリエンスを最適化するために、updateLocalViewとupdateRemoteViewインターフェースを追加しました。
<li>現在のMac PCがミュートに設定されているかどうかを取得するため、getCurrentMicDeviceMuteインターフェースを追加しました。
<li>現在のMac PCをグローバルミュートとして設定するため、setCurrentMicDeviceMuteインターフェースを追加しました。
<li>画面共有で、指定ウィンドウにある指定エリアの共有についてサポートを開始しました。
</ul>
</td>
<td>2020-08-21</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>
</tr>

</table>

## 2020年07月

<table>
<tr><th width="20%">ダイナミックネーム</th><th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
<tr>
<td>Version 7.5リリース</td>
<td>すべてのプラットフォーム：<ul style="margin:0">
<li>デュアルスタックIPV6およびIPV6 onlyのへのサポートを追加しました。</li>
<li>非常に小さなクラスのサポートに使用するため、複数ルームへの入室プルストリーミング機能を追加しました。</li>
<li>クラウドMCUミクスストリーミングの背景画像の設定サポートを追加しました（監督管理の必要性から、画像はまずTRTCコンソールを経由してからアップロードする必要があります）。</li>
<li>クラウドMCUミクスストリーミングでA+B=>CおよびA+B=>Aの2種類のモードのサポートを追加しました。</li>
<li>リアルタイムなステータスコールバックのonStatisticsで、再生バッファ時間フィールドのjitterBufferDelayを追加しました。</li>
<li>エンドツーエンドのマイク接続遅延を低減し、7.5バージョンのエンドツーエンド通話およびマイク接続遅延は、7.4バージョンから40%短縮しました。</li>
<li>モバイル端末のインイヤーモニタリング遅延を低減し、インイヤーモニタリングへのボイスチェンジおよびリバーブなどの音響効果の設定をサポートしています。</li>
<li>再生側ネットワークジッター評価アルゴリズムを最適化して再生ディレイを低減させました。</li>
</ul>
<br>Android: <ul style="margin:0">
<li>Android SDKのエンドツーエンドマイク接続通話の遅延を低減させました。</li>
<li>インイヤーモニタリングレイテンシーをさらに最適化しました。</li>
<li>再生viewを動的に切り替えるときに画面が黒くなる問題を最適化しました。</li>
</ul>
<br>iOS: <ul style="margin:0">
<li>インイヤーモニタリングレイテンシーをさらに最適化しました。</li>
<li>マイクデバイスの起動成功率を最適化しました。 </li>
</ul>
<br>Windows: <ul style="margin:0">
<li>socks5プロキシはユーザー名のパスワードチェックをサポートしています。</li>
<li>垂直画面解像度を使用してプッシュする場合に、一部のカメラでフレームレートが極端に低くなる問題を最適化しました。</li>
</ul></td>
<td>2020-07-31</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>
</tr><tr>
<td>CAM リソースレベルの権限付与をサポート</td>
<td>Tencent Real-Time CommunicationはCAMリソースレベルの権限付与をサポートし、開発者は自身の必要に応じてサブアカウントに適切なTRTCアクセス権限を割り当てることができます</td>
<td>2020-07-29</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/38319">アクセス管理</a></td>
</tr><tr>
<td>パッケージは残量アラームの設定をサポートしています</td>
<td>コンソールにパッケージ残量アラームスイッチを追加しました。起動後、パッケージ残量がアラーム値まで消費されると、ショートメッセージ、サイト内メッセージ、メールによるリマインダーが送信されます。</td>
<td>2020-07-20</td>
<td><a href="https://console.cloud.tencent.com/trtc/package">コンソールパッケージ管理</a></td>
</tr><tr>
<td>課金の変更</td>
<td>クラウドレコーディングに<b>レコーディング時間</b>に応じた課金のサポートを追加しました。</td>
<td>2020-07-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/38385">クラウドレコーディングの課金説明</a></td>
</tr>
</table>

## 2020年06月

<table>
<tr><th width="20%">ダイナミックネーム</th><th width="50%">動的記述</th><th width="15%">発表時間</th><th width="15%">関連ドキュメント</th>
<tr>
<td>Version 7.4リリース</td>
<td>
すべてのプラットフォーム：<ul style="margin:0">
  <li>各プラットフォームバージョンのSPEECH音質モードで音声通話の遅延が予想よりも大きいという問題を最適化しました。 </li>
  <li>入室プロセスの戦略を最適化し、すべてのプラットフォームの入室成功率を向上させました。 </li>
  <li>インイヤーモニタリングは音量設定をサポートしています。 </li></ul>
<br>iOS: <ul style="margin:0">
  iOS バージョンはAirPlayのミラーリング（旧バージョンは通話音量を使用したミラーリングができませんでした）をサポートしています。 
</ul>
<br>Windows: <ul style="margin:0">
  <li>システムオーディオループバック（startSystemAudioLoopback）起動後のエコー問題を回避するため、Windowsプラットフォームのエコーキャンセル（AEC）効果を最適化しました。</li>
  <li>Windowsプラットフォームでのカメラキャプチャのデバイスの互換性を強化しました。 </li>
  <li>Windowsプラットフォームでのオーディオデバイス（マイクとスピーカー）のデバイスの互換性を強化しました。 </li>
</ul>
</td>
<td>2020-06-24</td>
<td>-</td>
</tr>
<tr>
<td>Version 7.3リリース</td>
<td>
すべてのプラットフォーム：<ul style="margin:0">
  <li>全リンク128kbps高音質ステレオサウンドをサポートしています。setAudioQuality(TRTCAudioQualityMusic)インターフェースを介して設定できます。</li>
  <li>SPEECH音声モードをサポートしています。ミーティングシナリオでの音声通話に適しており、より強力なアクティブノイズキャンセリング（ANS）機能を有しています。setAudioQuality(TRTCAudioQualitySpeech) を介して設定できます。 </li>
  <li>原音と伴唱を分離したカラオケシナリオのサポートに使用する、複数チャンネルでのBGM並行再生をサポートしています。またBGMのリピート再生もサポートしています。 </li>
  <li>古いインターフェースと互換性のある状況で、全く新しい音響効果管理インターフェースTXAudioEffectManagerを追加しました。よりフレキシブルで多様性がある音響効果機能のサポートに使用します。 </li>
  <li>ビデオコーデックパラメータsetVideoEncoderParamにminVideoBitrateオプションを追加しました。画質への要求が高いライブストリーミングのお客様に設定することを推奨します。</li>
  <li>まずmuteLocalVideoを呼び出してから、startLocalPreviewを呼び出すことで、「プレビューのみでプッシュなし」効果の実装をサポートしています。また、enterRoomの前にstartLocalPreviewを呼び出しても、該当の機能を実装できます。</li>
   </ul>
<br>iOS: <ul style="margin:0"> 
     <li> iOSシステムレベルのスクリーンキャプチャソリューションを追加し、TencentMeetingと同様のシステム全体の画面共有効果を実現しました。またアクセスのしやすさを最適化し、この機能への半日以内でのアクセスの完了を実現しました。 </li>
  <li> インイヤーモニタリングはオーバーレイリバーブなどの音声効果をサポートしています。</li>
   </ul>
<br>Android&Windows: <ul style="margin:0">      
  オーディオでは過渡的なノイズ低減サポートを追加しました。setAudioQuality(TRTCAudioQualitySpeech)によってアクティブにすることができます。 
</ul>
<br>Android: <ul style="margin:0">      
  音響効果ファイルはassetパッケージの音響効果ファイルをサポートしています。
</ul>
<br>Windows: <ul style="margin:0">  
   ボイスチェンジャーなどの音響効果機能のサポートを追加しました。
</ul>
</td>
<td>2020-06-01</td>
<td>-</td>
</tr></table>


## 2020年05月

<table>
<tr><th width="20%">ダイナミックネーム</th><th width="50%">動的記述</th><th width="15%">発表時間</th>  <th width="15%">関連ドキュメント</th> 
<tr>      
         <td>課金の変更</td>   
         <td>音声時間はルーム内のすべてのユーザーの合計滞在時間から、ビデオストリームをサブスクライブするときのすべてのユーザーの滞在時間を差し引いたものに変更されます。<br>補足説明：<ul style="margin:0;"><li>複数のオーディオストリームを同時にサブスクライブした同じユーザーの音声時間は重複されません。</li>
<li>ビデオストリームがサブスクライブされていない場合は、オーディオストリームがサブスクライブされているかどうかを問わず、音声時間としてカウントされます。</li>
     <li>ビデオ時間の計算ルールは変更されません。ビデオストリームにサブスクライブしたすべてのユーザーの合計継続時間となります。</li>
</ul></td>   
       <td>2020-05-01</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34610">課金概要</a></td>   
     </tr> 
</table>

## 2020年04月

<table>
<tr><th width="20%">ダイナミックネーム</th><th width="50%">動的記述</th><th width="15%">発表時間</th>  <th width="15%">関連ドキュメント</th> 
<tr><td>通話品質監視関連インターフェースのリリース</td>   
    <td><ul style="margin:0;"><li>一度に最大100のルーム情報を返し、直近5日以内のデータを確認できる、SDKAppID のルームリスト照会インターフェースを追加しました。</li>
     <li>指定時間内のユーザーリストおよび通話品質データを照会できる、ユーザーリストと通話指標照会インターフェースを追加しました。</li>
     <li>指定時間内の過去のルームとユーザー数を照会できる、過去のルームおよびユーザー数照会インターフェースを追加しました。</li>
     <li>24時間以内のルーム数と通話人数を照会できる、リアルタイム通話スケール照会インターフェースを追加しました。</li>
     <li>24時間以内の入室成功率、最初のフレームのインスタントブロードキャスティング率、オーディオ・ビデオラグ率データを照会できる、リアルタイム品質照会インターフェースを追加しました。</li>
     <li>アップおよびダウンストリームのパケット損失データを含む、24時間以内のプライベートネットワークステータスを照会できる、リアルタイムネットワークステータス照会インターフェースを追加しました。</li>
</ul></td>   
    <td>2020-04-29</td>   
		<td><a href="https://intl.cloud.tencent.com/document/product/647/34260">API 概要</a></td> 
</tr><tr>
    <td>SDK Version 7.2 リリース</td>   
  <td><br>Android: <ul style="margin:0;">
     <li>Androidは携帯電話のスクリーンキャプチャのサポートを追加しました。携帯端末のスクリーンキャプチャのライブストリーミングに適しています。</li>
     <li>ミドルレンジ、ローエンドのAndroid携帯電話における通話シナリオの性能消耗を最適化し、音声体験を向上させます。</li>
  </ul><br>iOS: <ul style="margin:0;">
      <li>モバイルApp内スクリーンキャプチャとライブストリーミングに適した、App内スクリーンキャプチャのサポートを追加しました。</li>
      <li> iOSローエンド端末の音声品質を最適化し、音声効果を改善しました。</li>
  </ul><br>iOS&Android：<ul style="margin:0;">フィルターやクロマキーなどの視覚効果インターフェースを最適化しました。
  </ul><br>Windows：<ul style="margin:0;">Windows側のgetCurrentCameraDeviceのロジックを最適化しました。カメラを使用しない場合は、最初のデバイスがデフォルトのデバイスとして返されます。
  </ul></td>   
  <td>2020-04-16</td>   
  <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>   
</tr><tr>      
  <td>コンソール使用量統計モジュールの改訂</td>   
  <td>使用量統計モジュールが改訂され、音声、SD、HDおよびFHDのリアルタイムの課金分数を表示できるようになりました。データは5分ごとに更新されます。</td>   
  <td>2020-04-01</td>   
  <td>-</td>   
</tr> 
</table>

## 2020年03月

<table>
<tr><th width="20%">ダイナミックネーム</th><th width="50%">動的記述</th><th width="15%">発表時間</th>  <th width="15%">関連ドキュメント</th> 
<tr>      
         <td>SDK Version 7.1 リリース</td>   
         <td>すべてのプラットフォーム：<ul style="margin:0;"><li>ミクスストリーミングプリセットテンプレートの使いやすさを最適化しました。</li>
     <li>入室時にAuto-relayする問題を修正しました。</li>
     <li>ミクスストリーミングを最適化し、成功率を向上させました。</li>
</ul><br>Android: <ul style="margin:0;">
		 <li>入室して頻繁にAGCを切り替えると、処理した音声がすべてゼロ（0）になってしまう問題を修正しました。</li>
     <li>C++ STL基本ライブラリの全静的コンパイル。</li>
     <li>通話音量はデフォルトでANS、AGCが有効化され、通話モードでの音質を向上させました。</li>
</ul><br>iOS：<ul style="margin:0;"><li>入室前にstartLocalPreviewし、その後、入室した場合にプレビューが黒くなる問題を修正しました。</li>
     <li> iOS 13.3システムの一部モデルでの深刻なエコーの問題を解決しました。</li>
     <li>BGM再生は拡張子のないオーディオファイルをサポートしています。</li>
</ul><br>Mac&Windows: <ul style="margin:0;">
     <li>画面共有はビッグストリームからのプッシュをサポートしています。</li>
</ul></td>   
       <td>2020-03-27</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>   
     </tr> 
   <tr>      
         <td>「オーディオ・ビデオ一般パッケージ」の公開</td>   
         <td>固定パッケージとカスタムパッケージを含み、音声、SD、HDおよびFHD時間の同時割引のために使用できる、オーディオ・ビデオ一般パッケージを公開しました。音声、SD、HDおよびFHDの1分間の課金につき、それぞれ1分、2分、4分、15分の一般パッケージ時間が差し引かれます。</td>   
       <td>2020-03-11</td>   
       <td>-</td>   
     </tr> 
</table>

## 2020年02月

<table>
<tr><th width="20%">ダイナミックネーム</th><th width="50%">動的記述</th><th width="15%">発表時間</th>  <th width="15%">関連ドキュメント</th> 
<tr>      
         <td>クラウド自動レコーディングの最適化</td>   
         <td>アプリケーションに応じて自動クラウドレコーディングのオン/オフを個別に切り替える設定をサポートしています。各アプリケーションで個別のレコーディングファイルの形式とコールバックアドレスを設定できます。</td>   
       <td>2020-02-14</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/35426">クラウドレコーディングと再生を実現</a></td>   
     </tr> 
</table>

## 2020年01月

<table>
<tr><th width="20%">ダイナミックネーム</th><th width="50%">動的記述</th><th width="15%">発表時間</th>  <th width="15%">関連ドキュメント</th> 
<tr>      
         <td>SDK Version 6.9リリース</td>   
         <td>すべてのプラットフォーム：<ul style="margin:0;"><li>enterRoom パラメータTRTCParamsにstreamId属性を追加しました。現在のユーザーがCDNでライブストリームIDを設定するために使用し、ライブCDNがさらにバインドしやすくなります。</li>
     <li>enterRoomパラメータTRTCParamsにcloudRecordFileName属性を追加しました。今回のライブストリーミングのクラウドレコーディングでのファイル名を設定するために使用し、ビデオストリームの中断に対する記録サービスの耐性を最適化し、リモートでレコーディングされたファイルをより完全なものにします。</li>
     <li>シナリオTRTCAppSceneAudioCallを追加しました。これはenterRoomで設定できます。このシナリオでは、TRTC SDKは音声通話に全面的な最適化を行っています。</li>
     <li>シナリオTRTCAppSceneVoiceChatRoomを追加しました。これはenterRoomで設定できます。TRTC SDKを有効にすると、特に音声インタラクティブチャットルームでのシナリオ向けに最適化されます。</li>
     <li>ビデオ画面では1080P高解像度キャプチャをサポートしています。携帯電話でライブストリーミングしてPCで視聴するケースで、さらに優れた画面解像度を得ることができます。</li>
     <li>API追加：pauseAudioEffect、resumeAudioEffectの音響効果は、一時停止/回復の制御をサポートしています。</li>
     <li>API追加：setBGMPlayoutVolume、setBGMPublishVolumeによって、BGMは、ローカル再生およびプッシュMix音量の個別の設定をサポートしています。</li>
     <li>API追加：setRemoteSubStreamViewRotationのサブストリームビデオ再生は、レンダリング回転角度の調整をサポートしています。</li>
</ul><br>iOS&Android：<ul style="margin:0;"> API追加：snapshotVideo() はローカルおよびリモートビデオ画面のスクリーンキャプチャをサポートしています。
</ul><br>Android：<ul style="margin:0;"><li>グローバル音量タイプモードを追加：setSystemVolumeType(TRTCSystemVolumeTypeVOIP)、即ち、通話音量の一貫提供は、主にBluetoothイヤホンが標準装備マイクの集音切り替え問題を解決するために使用されます。</li>
     <li>Android 10.0システムへのサポートを追加しました。</li>
</ul><br>Windows：<ul style="margin:0;"><li>C#版SDKは実際のウィンドウレンダリングとカスタムレンダリングをサポートしています。</li>
     <li>C#版SDKはローカルオーディオレコーディング機能をアライメントします。</li>
</ul></td>   
       <td>2020-01-14</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>   
     </tr> 
   <tr>      
         <td>「通話品質監視ダッシュボードv2.0」のリリース</td>   
         <td><ul style="margin:0;"><li>クライアントSDKの報告データは最速3秒で照会できます。</li>
     <li>開発者がいつでも照会しやすいよう、データは15日間ストレージされます。</li>
     <li>Webフロントエンドは10秒以内に6人の5時間のデータをすべてレンダリングできます。</li>
     <li>受信側/送信側で詳細なマルチビューデータと詳細なイベント表示を提供します。</li>
     <li>単一ページに完全なリンク情報を表示し、データを同期して比較します。</li>
     <li>Tencentの自社開発品質評価システムは、実際のユースケースに最適です。</li>
     <li>ユーザーエクスペリエンスを重視し、データは理解しやすく、詳細で、使いやすいものとなっています。</li>
</ul></td>   
       <td>2020-01-07</td>   
       <td>-</td>   
     </tr> 
</table>

## 2019年12月

<table>
<tr><th width="20%">ダイナミックネーム</th><th width="50%">動的記述</th><th width="15%">発表時間</th>  <th width="15%">関連ドキュメント</th>
<tr>      
<td> CAMサービスレベルの権限付与をサポート</td>   
<td>Tencent Real-Time CommunicationがCAMに接続され、サービスレベルの権限付与をサポートしています。</td>   
<td>2019-12-31</td>   
<td><a href="https://intl.cloud.tencent.com/document/product/598/10588"> CAMの製品をサポート</a></td> 
</tr>
<tr>      
<td>課金の変更</td>   
<td> SDの解像度の上限が640×360から640×480に引き上げられました。つまり、640×480以下の解像度がSDとして課金されます。</td>   
<td>2019-12-04</td>   
<td>-</td>   
</tr>
</table>



## 2019年11月

<table>
<tr><th width="20%">ダイナミックネーム</th><th width="50%">動的記述</th><th width="15%">発表時間</th>  <th width="15%">関連ドキュメント</th> 
<tr>      
         <td>コンソール v2.0のリリース</td>   
         <td>フレームワークを設計しなおし、使いやすさを向上させるために左側のナビゲーションバーを追加しました。機能に応じて、概要、使用量統計、監視ダッシュボード、開発支援、パッケージ管理およびアプリケーション管理などのモジュールに区分されています。</td>   
       <td>2019-11-18</td>   
       <td>-</td>   
     </tr> 
   <tr>      
         <td>SDK Version 6.8 リリース</td>   
         <td>すべてのプラットフォーム：<ul style="margin:0;"><li>入室に非自動プルを指定できる機能を追加しました。</li>
     <li>コールバックonRemoteUserEnterRoom / onRemoteUserLeaveRoomを追加しました。マイク・オンになっていないキャスターの入退室通知をサポートしています。</li>
     <li>pts生成メカニズムを最適化しました。</li>
     <li>ネットワークの切り替え後に、優れたアクセスポイントの自動選択を最適化しました。</li>
     <li>startRemoteViewは事前呼び出しをサポートしています。</li>
</ul><br>Android：<ul style="margin:0;">インイヤーモニタリング機能を追加しました。</ul>
<br>iOS&Android: <ul style="margin:0;">
		<li>エンタープライズ版では、美肌、キラキラした目、白い歯、しわ取り、下まぶたのたるみ除去などを含む、Pituの新機能を追加しました。</li>
		<li>インターフェースgetBeautyManagerを追加し、美顔、Pituアニメーションエフェクトのインターフェースを集約しました。</li>
</ul>
<br>Mac：<ul style="margin:0;">Mac10.15の互換性問題を解決しました。
</ul>
<br>Windows：<ul style="margin:0;"><li>スクリーンキャプチャは遮蔽対策をサポートしています。</li>
     <li>socks5 プロキシをサポートしています。</li>
     <li>Windows C#でユーザーのレンダリングコールバックが削除されると、他のユーザーがデータを受信できなくなる現象を修正しました。</li>
     <li>Windows C#のパフォーマンスを最適化しました。</li>
</ul>
</td>   
<td>2019-11-15</td>   
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>   
</tr> 
</table>

## 2019年10月

<table>
<tr><th width="20%">ダイナミックネーム</th><th width="50%">動的記述</th><th width="15%">発表時間</th>  <th width="15%">関連ドキュメント</th> 
<tr>      
    <td>課金の変更&お試しパックの限度の拡充</td>   
    <td><ul style="margin:0;">
            <li>音声およびビデオの個別課金をサポートしています。ビデオはSD、HD、FHDに応じてそれぞれ課金されます。料金一覧：音声7元/1000分、SD14元/1000分、HD28元/1000分、FHD105元/1000分。</li>
           <li>固定パッケージとカスタムパッケージを含む、まったく新しい音声、SD、HDパッケージが同時にリリースされます。すべてのパッケージの有効期間は1年間です。</li>
           <li>2019年10月11日より、初めてTRTCコンソールでアプリケーションを作成するお客様が自動的に取得するお試しパックのオーディオ・ビデオ時間が1000分から10000分に延長されます。有効期限は1年間で、音声、SD、HDおよびFHDの順に時間を差し引くことができます。</li>
           <li>初めてTRTCコンソールでアプリケーションを作成する時間が2019年10月11日よりも前のお客様、または音声およびビデオが区分されていない旧パッケージを購入済みのお客様には引き続き「音声およびビデオ同一課金」の課金方式を適用します。旧パッケージ（1000分お試しパック、6.6元300分体験パック、5万分入門パック、25万分標準パック、100万分企業パックおよび300万分プレミアパックを含む）を使い切った翌月または期限切れの翌月に新パッケージ（音声、SD、HDの固定パッケージとカスタムパッケージを含む）を購入でき、新パッケージ購入後に、「音声およびビデオ個別課金」の課金方式に切り替えることができます。課金方式の変更操作はキャンセルできません。</li>
</ul></td>   
       <td>2019-10-11</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34610">課金概要</a></td>   
     </tr> 
</table>

## 2019年09月

<table>
<tr><th width="20%">ダイナミックネーム</th><th width="50%">動的記述</th><th width="15%">発表時間</th>  <th width="15%">関連ドキュメント</th> 
<tr>      
         <td>SDK Version 6.7 リリース</td>   
         <td>すべてのプラットフォーム：<ul style="margin:0;"><li>転送消費時間を最適化しました。</li>
     <li>1人のユーザーの再生音量を個別に調節する機能をサポートしています。</li>
</ul><br>Android：<ul style="margin:0;"><li>AAR パッケージに権限取得設定を追加しました。</li>
     <li>Android 8.0以降のシステムにCPU占有評価を追加しました。</li>
     </ul><br>iOS：<ul style="margin:0;">インイヤーモニタリングのサポートを追加しました。</ul><br>
     Windows：<ul style="margin:0;"><li>音響効果インターフェースのサポートを追加しました。</li>
     <li>64ビット C# APIのサポートを追加しました。</li>
</ul><br>Mac：<ul style="margin:0;">入室とフレームレートを最適化しました。</ul></td>   
       <td>2019-09-30</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>   
     </tr> 
   <tr>      
         <td>SDK Version 6.6バージョンの最適化</td>   
         <td>すべてのプラットフォーム：<ul style="margin:0;"><li>システム音量タイプ設定インターフェースを追加しました。</li>
     <li>音響効果インターフェースを追加し、短い音響効果の再生をサポートします。</li></ul><br>
     iOS：<ul style="margin:0;"> iOS 13との互換性を持たせました。</ul><br>
     Mac：<ul style="margin:0;">一部モデルのノイズ、音の歪みといった互換性の問題を解決しました。</ul><br>
     iOS&Android：<ul style="margin:0;">カスタムオーディオコールバックデータの修正をサポートしています。</ul><br>
     Windows&Mac：<ul style="margin:0;">AGCのサポートを追加し、一部モデルの音が小さいという問題を解決しました。</ul></td>   
       <td>2019-09-10</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>   
     </tr> 
</table>

## 2019年08月

<table>
<tr><th width="20%">ダイナミックネーム</th><th width="50%">動的記述</th><th width="15%">発表時間</th>  <th width="15%">関連ドキュメント</th> 
<tr>      
         <td>コンソールの「初心者ガイド」をリリース</td>   
         <td>初心者ガイドを追加しました。わずか4ステップでTencent Real-Time CommunicationDemoをクイックスタートできます。</td>   
       <td>2019-08-16</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/35083">1分間でDemoを開始</a></td>   
     </tr> 
   <tr>      
         <td>SDK Version 6.6リリース</td>   
         <td>すべてのプラットフォーム：<ul style="margin:0;"><li>入室を最適化し、入室の消費時間を削減すると同時に、入室の成功率を向上させました。</li>
     <li>オーディオローカルレコーディング機能を追加しました。</li>
     <li> muteリモートビデオインターフェースをサポートしています。</li>
     <li>最初のフレームオーディオ、最初のフレームビデオ送信のコールバックインターフェースを追加しました。</li>
     <li>入室エラーコードを統一しました。onEnterRoomのコールバックを使用し、resultが0未満は入室エラーを意味します。</li>
     <li>Demoを最適化し、低遅延の大型ルームのサポートを追加しました。</li>
</ul><br>Android：<ul style="margin:0;"><li>ローカルプレビュー角度が正しくない問題を修正しました。</li>
     <li>ローカルおよびリモート側のレンダリングでSurfaceView方式をサポートします。</li>
</ul><br>Windows：<ul style="margin:0;">エコーキャンセレーションライブラリをアップグレードし、システムミキシングを実現すると同時に，一部のサンプリング設定ANSが有効にならない問題、一部デバイスの音が小さい問題を解決しました。</ul>
<br>iOS&Android：<ul style="margin:0;"><li>プレーヤーに音量設定インターフェースおよび音量レベルコールバックインターフェースを追加しました。</li>
     <li>カスタムしたビデオ配信で、ローカルのレンダリングをサポートしています。</li>
     <li>ユーザー定義キャプチャの配信ビデオで1080Pをサポートしています。</li>
</ul></td>   
       <td>2019-08-02</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>   
     </tr> 
</table>

## 2019年06月

<table>
<tr><th width="20%">ダイナミックネーム</th><th width="50%">動的記述</th><th width="15%">発表時間</th>  <th width="15%">関連ドキュメント</th> 
<tr>      
     <td>SDK Version 6.5リリース</td>   
     <td>すべてのプラットフォーム：<ul style="margin:0;">
        <li>ライブストリーミングモード（TRTCAppSceneLIVE）に「低遅延の大型ルーム」機能を追加しました。 
            <ul style="margin:0;"><li>オーディオ・ビデオ専用に最適化されたUDPプロトコルを採用し、弱いネットワークに対する耐性を強化しました。</li>
                                  <li>平均の視聴ディレイを1秒として、視聴者とキャスター間のインタラクティブな積極性を引き上げました。</li>
                                  <li>最大10万人の同じルームへの入室をサポートしています。</li></ul></li>
     <li>音量評価アルゴリズム（enableAudioVolumeEvaluation）を最適化し、音量評価の感度をさらに高めました。</li>
     <li>高ディレイおよび高パケット損失のネットワーク環境下のQoEアルゴリズムを最適化して、弱いネットワークに対する耐性を強化しました。</li>
     <li>onStatistics状態のコールバックを最適化しました。存在するストリーミングのみをコールバックします。</li>
     <li>ビデオ通話（TRTCAppSceneVideoCall）モードでのQoEアルゴリズムを最適化し、1対1の通話モードでの弱いネットワークでのスムーズさをさらに向上させました。</li>
     <li>デコーダの性能を最適化し、ローエンドのAndroid携帯電話のディレイが次第に高くなるBugを修正しました。</li>
     <li>弱いネットワーク環境で音声、画像が同期しないBugを最適化しました。</li>
     <li>muteLocalVideoの後に、再生側画面の回復速度を取り消すよう最適化しました。</li>
     <li>ライブストリーミングTXLivePlayerがバッファロジックの再生を最適化してラグ率を低減させました。</li>
</ul><br>インターフェースの変更：<ul style="margin:0;"><li>ユーザーロール：入室時のロール（キャスター、視聴者）指定に使用するため、TRTCParamsにrole属性を追加しました。</li>
     <li>ロールの切り替え：switchRole、入室中に、視聴者とキャスターのマイク接続に使用するため、キャスター、視聴者のロールを動的に切り替えます。</li>
     <li>コールバックの追加：ロール切り替えの成功または失敗のコールバックonSwitchRole。</li>
     <li>コールバックの変更：onFirstVideoFrameインターフェースにstreamTypeパラメータを追加し、ビデオストリームタイプを指定します。</li>
     <li>Windows: getCurrentCameraDevice、getCurrentMicDevice、getCurrentSpeakerDeviceインターフェースのリターンタイプをITRTCDeviceInfo *に調整し、getDeviceNameとgetDevicePIDをサポートします。</li>
</ul></td>   
       <td>2019-06-12</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>   
     </tr>
   <tr>      
         <td>無料「お試しパック」のリリース</td>   
         <td><ul style="margin:0;"><li>2019年6月1日より、初めてTRTCコンソールでアプリケーションを作成するお客様は、オーディオ・ビデオ時間1000分が含まれるお試しパックを自動的に取得します。有効期間は1年間です（初めてアプリケーションを作成した当日から翌年のその月の最終日まで）。</li>
     <li>2019年6月1日より、新たに購入する体験パック、入門パック、標準パックおよび企業パックの有効期間を一律1年間に延長します。</li>
</ul></td>   
       <td>2019-06-01</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>   
     </tr> 
</table>

## 2019年04月

<table>
<tr><th width="20%">ダイナミックネーム</th><th width="50%">動的記述</th><th width="15%">発表時間</th>  <th width="15%">関連ドキュメント</th> 
<tr>      
         <td>SDK Version 6.4リリース</td>   
         <td>すべてのプラットフォーム：<ul style="margin:0;"><li>弱いネットワーク環境下でのスムーズさを向上させました。</li>
     <li>音量のコールバックアルゴリズムを最適化し、音量コールバックの数値をより適正なものにしました。</li>
     <li>カスタマイズしたオーディオ、ビデオのデータ配信で、外部指定データのタイムスタンプをサポートします。</li>
     <li> ミクスストリーミングsetMixTranscodingConfig APIの設定コールバック関数を追加しました。</li>
     <li>setMixTranscodingConfigインターフェースを強化しました。roomIDパラメータをサポートして、ルーム間のマイク接続ミクスストリーミングに使用します。</li>
     <li> setMixTranscodingConfigインターフェースを強化しました。pureAudioパラメータをサポートし、音声のみの通話における音声ミクスストリーミングとレコーディングに使用します。</li>
</ul><br>Android：<ul style="margin:0;"><li>エンタープライズ版のサポートを追加しました（デカ目、小顔、フェイスラインシェイプ 及び動的エフェクトの付属機能を追加しました）。</li>
     <li>ローエンドAndroidデバイスで720pビデオをデコードする性能の問題を最適化しました。</li>
     <li>ローカルでのイメージおよびエンコーダ出力のイメージを表示するインターフェースを追加しました。</li>
</ul><br>Windows：<ul style="margin:0;"><li> Duilib ライブラリに基づく全機能バージョン Demoを追加しました。</li>
     <li>カメラ設定選択ポリシーを最適化し、デバイス選択で deviceIdの伝達をサポートします。</li>
     <li>一部Windowsバージョンでの美顔およびレンダリングモジュールの互換性と性能の問題を最適化しました。</li>
</ul><br>iOS&Mac：<ul style="margin:0;"><li>記号重複Bugを修正しました。</li>
     <li>iOS ローエンドマシンの性能を最適化しました。</li>
     <li>iOS エンタープライズ版のサポートを追加しました（デカ目、小顔、フェイスラインシェイプ および動的エフェクトの付属機能を追加しました）。</li>
     <li>ローカルでのイメージおよびエンコーダ出力のイメージを表示するインターフェースを追加しました。</li>
     <li>sendCustomVideoDataはNSDataデータ形式をサポートしています。</li>
</ul></td>   
       <td>2019-04-25</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>   
     </tr> 
   <tr>      
         <td>SDK Version 6.3リリース</td>   
         <td><ul style="margin:0;"><li>Androidプラットフォームで64ビットのサポートを追加しました。</li>
     <li>カスタマイズしたビデオ収集用インターフェースの追加：TRTCCloud >> sendCustomVideoData。</li>
     <li>カスタマイズしたオーディオ収集用インターフェースの追加：TRTCCloud >> sendCustomAudioData。</li>
     <li>カスタマイズしたビデオレンダリング用インターフェースの追加：TRTCCloud >> setLocalVideoRenderDelegate + setRemoteVideoRenderDelegate。</li>
     <li>カスタマイズしたオーディオデータコールバックインターフェースの追加：TRTCCloud >> setAudioFrameDelegate，サポート：<ul style="margin:0;">
     <li>マイク収音データを返します：TRTCAudioFrameDelegate >> onCapturedAudioFrame</li>
     <li> 各リモートユーザーのオーディオデータを返します：TRTCAudioFram eDelegate >> onPlayAudioFrame</li>
     <li>ミキシング後にスピーカーに送信され再生されるオーディオデータを返します：TRTCAudio FrameDelegate >>onMixedPlayAudioFrame</li>
</ul></ul></td>   
       <td>2019-04-02</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>   
     </tr> 
   <tr>      
         <td>月次機能使用料のキャンセル</td>   
         <td>2019年3月より、1500元/月の月次機能使用料の徴収を停止します。課金の変更は2019年4月1日にプッシュされる請求書に反映されます。</td>   
       <td>2019-04-01</td>   
       <td>-</td>   
     </tr> 
</table>

## 2019年03月

<table>
<tr><th width="20%">ダイナミックネーム</th><th width="50%">動的記述</th><th width="15%">発表時間</th>  <th width="15%">関連ドキュメント</th> 
<tr>      
         <td>SDK Version 6.2リリース</td>   
         <td>Windows：<ul style="margin:0;"><li>TRTCCloud クラスを純粋仮想インターフェースITRTCCloudに変更し、LoadLibiraryを介したDLLの動的ロードをサポートします。</li>
     <li>オーディオデータコールバックITRTCAudioFrameCallbackを追加しました。</li>
     <li> cameraの互換性およびキャプチャ性能を最適化しました。</li></ul><br>
     Android、iOS、Mac、Windows：<ul style="margin:0;"><li>既存の2つのTRTC ルームを相互接続できる、ルーム間通話機能connectOtherRoomを追加しました。この機能はライブストリーミングルームのキャスターPK機能に使用できます。</li>
     <li>sendSEIMsg()インターフェースを追加しました。ビデオフレームのSEIヘッダ情報を介してカスタムメッセージの配信をサポートします。通常、ビデオストリームでタイムスタンプ情報の詰め込みに使用します。</li>
     <li>CPU使用率と安定性を最適化しました。</li>
     <li>純音声通話シナリオ（人狼ゲームなど）でのRelayed Push機能を修正しました。TRTCParamのbussInfoフィールドと合わせて使用する必要があります。</li>
     <li>弱いネットワーク（劣悪なネットワーク環境）における画面解像度を向上させました。</li>
     <li> TRTCCloudのマルチインスタンス機能を消去し、作成モードをシングルトンモードに変更して、複数のTRTCCloudインスタンスが相互にネットワークリソースを占有することによる体験効果への影響を回避します。</li>
     <li>フィルター濃度設定インターフェースsetFilterConcentration() を追加しました。</li>
</ul></td>   
       <td>2019-03-08</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>   
     </tr> 
</table>

## 2019年01月

<table>
<tr><th width="20%">ダイナミックネーム</th><th width="50%">動的記述</th><th width="15%">発表時間</th>  <th width="15%">関連ドキュメント</th> 
<tr>      
         <td>SDK Version 6.1リリース</td>   
         <td><ul style="margin:0;"><li>Windows、Macで画面共有をサポートします。</li>
     <li>画面共有ストリーミングの視聴をサポートします。</li>
     <li>カスタマイズしたビデオデータの配信をサポートします。</li>
     <li>CDNの転送およびミクスストリーミングの実装を最適化しました。</li>
     <li>入室時にライブストリーミングシナリオとビデオ通話シナリオを区別します。</li>
     <li>安定性を向上させ、一部に偶発的に発生するcrashを解決しました。</li>
     <li> iOS、Windowsメモリの使用量を最適化しました。</li>
     <li> トラフィックコントロールを最適化して弱いネットワークのパフォーマンスを向上させました。</li>
</ul></td>   
       <td>2019-01-31</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>   
     </tr> 
   <tr>      
         <td>SDK Version 6.0リリース（TRTC SDK初回バージョン）</td>   
         <td><ul style="margin:0;"><li>アーキテクチャをLiteAVカーネルに更新しました。</li>
     <li>全く新しいQoSアルゴリズムを採用して、ラグ率をさらに低くし、スムーズさをさらに高くしました。</li>
     <li>全く新しいAudioモジュールを採用して、各種ネットワーク状況下での音質を高度に最適化しました。</li>
     <li>大小ストリーミングのデュアルチャンネルエンコード機能（WindowsおよびMacデバイスでのみアクティブにすることを推奨）をサポートしています。</li>
     <li>CDNの転送およびミクスストリーミング機能をサポートしています。</li>
</ul></td>   
       <td>2019-01-18</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDKダウンロード</a></td>   
     </tr> 
</table>


