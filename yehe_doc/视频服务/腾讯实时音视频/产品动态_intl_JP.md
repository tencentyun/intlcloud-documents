
## 2021年03月
<table>
<tr><th width="20%">ダイナミックネーム</th>  <th width="50%">動的記述</th> <th width="15%">発表時間</th> <th width="15%">関連ドキュメント</th>
</tr><tr>
<td>Version 8.5リリース</td>
<td>すべてのプラットフォーム：<ul style="margin:0">
<li>ビデオ放送機能を追加しました。TXVODPlayerを使用してTRTCCloudとバインドし、オンデマンド再生中のコンテンツをTRTCのサブストリームプッシュで共有することができます。</li>
<li>サブストリームのユーザー定義キャプチャを追加しました。API <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aeeff994b8a298fa4948a11225312f629">sendCustomVideoData</a>をご参照ください。</li>
<li>カスタムサウンドミキサー機能を追加しました。自分のオーディオトラックをSDKのオーディオ処理フロー中にミキシングすることができます。SDKはまず2つのオーディオトラックをミキシングしてから再び一緒に公開します。API <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a6d04ce887009661a551e23c61d41571f">mixExternalAudioFrame</a>をご参照ください。</li>
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

