本書では、CSS製品の機能について説明します。機能と使用方法の詳細については、対応するドキュメントをご参照ください。

### CSSプッシュ
<table>
<tr><th width=17%>機能名</th><th>機能概要</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/7968">プッシュプロトコル</a></td><td>RTMPプロトコルとWebRTCプロトコルを使用したプッシュをサポートします。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31558">プッシュ方法</a></td><td>iOS、Android、Web版のTencent Cloud RT-Cube・MLVB SDKを統合することで、また、OBS、XSplit、FMLE などよく使用されるサードパーティー製のプッシュソフトウェアを使用することでプッシュすることをサポートします。 </td></tr>
<tr><td>プッシュデバイス</td><td>よく使用されるサードパーティー製のRTMPプッシュハードウェアおよびエンコーダ、またはボックスなどのデバイスをサポートします。</td></tr>
</table>

### CSS再生
<table>
<tr><th width=17%>機能名</th><th>機能概要</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/7968">再生プロトコル</a></td><td>RTMP、FLV 、HLS、UDPの4種類の再生プロトコルをサポートします。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31559">再生方法</a></td><td>iOS、Android、Web版のTencent Cloud RT-Cube・MLVB SDKを統合することで、また、FLV、RTMP、HLSなどよく使用されるサードパーティー製のプレイヤーを使用することで再生することをサポートします。</td></tr>
<tr><td>再生制御</td><td>入力ストリームと仕様が一致するオリジナルストリームおよびリアルタイムでトランスコーディングしたストリームを再生できます。</td></tr>
</table>

 ### CSS管理
 <table>
<tr><th width=17%>機能名</th><th>機能概要</th></tr>
<tr><td>管理方法</td><td>CSS管理コンソールでのUI管理とCSS APIの呼出しによる管理をサポートします。</td></tr>
</table>

### CSSコンソール
<table>
<tr><th width=17%>機能名</th><th>機能概要</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31054">概要</a></td><td>利用可能なCSSリソースパックのトラフィックとCSSのリアルタイム帯域幅、トラフィックなどのデータをリアルタイムで確認できます。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/35970">ドメイン名管理</a></td><td>CSSプッシュと再生ドメイン名の新規追加、変更、使用禁止、削除ができます。ドメイン名CNAME、HTTPS証明書、プッシュと再生認証などの設定も可能です。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31068">CSSストリーム管理</a></td><td>オンラインになっているCSSストリームの情報またはCSSストリームの履歴情報を検索できます。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/34223">機能モジュール</a></td><td>CSSレコーディング、トランスコーディング、スクリーンキャプチャ、ポルノ検出、ウォーターマーク、コールバックなどの設定情報を検索または変更します。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31076">統計分析</a></td><td>CSSサービスの帯域幅、トラフィック、リクエスト数、同時接続数、スクリーンキャプチャ数、チャネル数、およびレコーディングチャネル数などの使用量を検索します。</td></tr>
</table>


### CSSセキュリティ
<table>
<tr><th width=17%>機能名</th><th>機能概要</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31059">プッシュ認証</a></td><td>プッシュURLのホットリンク防止をサポートし、認証Keyと有効期間をカスタマイズできます。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31060">再生認証</a></td><td>ブラックリスト/ホワイトリストによるホットリンク防止、Refererによるリンク不正アクセス防止、再生URLのホットリンク防止、再生のリモート認証をサポートしています。</td></tr>
<tr><td><a href="https://www.tencentcloud.com/document/product/267/48068">DRM暗号化</a></td><td>Widevine、Fairplay、NormalAESをベースにしたDRM暗号化プロトコルを使用したライブストリーミング暗号化、レコーディング防止、ホットリンク防止などのサービスをサポートし、お客様のビデオ内容のセキュリティを確保します。</td></tr>
</table>

###  API管理
<table>
<tr><th width=17%>機能名</th><th>機能概要</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">ドメイン名管理に関するAPI</a></td>
<td>ドメイン名の追加、ドメイン名の削除、ドメイン名情報の確認、ドメイン名リストの確認、ドメイン名の有効化、ドメイン名の使用禁止、再生ドメイン名情報の変更が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">再生遅延管理に関するAPI</a></td>
<td>再生の遅延、ライブストリーミング再生遅延リストの取得、再生遅延のリカバーが可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">レコーディング管理に関するAPI</a></td>
<td>レコーディングタスクの作成、レコーディングルールの作成、レコーディングテンプレートの作成、レコーディングタスクの削除、レコーディングルールの削除、レコーディングテンプレートの削除、レコーディングルールリストの取得、単独のレコーディングテンプレートの取得、レコーディングテンプレートリストの取得、レコーディングテンプレート設定の変更、レコーディングタスクの終了が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">スクリーンキャプチャ・ポルノ検出に関するAPI</a></td>
<td>スクリーンキャプチャルールの作成、スクリーンキャプチャテンプレートの作成、スクリーンキャプチャルールの削除、スクリーンキャプチャテンプレートの削除、スクリーンキャプチャルールリストの取得、単独のスクリーンキャプチャテンプレートの取得、スクリーンキャプチャテンプレートリストの取得、スクリーンキャプチャテンプレートの変更が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">ウォーターマーク管理に関するAPI</a></td>
<td>ウォーターマークの追加、ウォーターマークルールの作成、ウォーターマークの削除、ウォーターマークルールの削除、単独のウォーターマークの取得、ウォーターマークルールリストの取得、ウォーターマークリストの確認、ウォーターマークの更新が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">CSSコールバックに関するAPI</a></td>
<td>コールバックルールの作成、コールバックテンプレートの作成、コールバックルールの削除、コールバックテンプレートの削除、コールバックルールリストの取得、単独のコールバックテンプレートの取得、コールバックテンプレートリストの取得、コールバックテンプレートの変更が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">CSSプルに関するAPI</a></td>
<td>プル設定の追加、プル設定の削除、プル設定の確認、プル設定の更新、プル設定状態の変更が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">CSS管理に関するAPI</a></td>
<td>プッシュ禁止リストの取得、プッシュ切断イベントの確認、ライブストリーミング中のストリーミングの確認、ストリーミング履歴リストの確認、ストリーミング状態の確認、ライブストリーミングの切断、ライブストリーミングのプッシュ禁止、ライブストリーミングプッシュの回復が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">CSSトランスコーディングに関するAPI</a></td>
<td>トランスコーディングルールの作成、トランスコーディングテンプレートの作成、トランスコーディングルールの削除、トランスコーディングテンプレートの削除、トランスコーディングルールリストの取得、個別トランスコーディングテンプレートの取得、トランスコーディングテンプレートリストの取得、トランスコーディングテンプレート設定の変更が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">統計・確認に関するAPI</a></td>
<td>CSS課金帯域幅とトラフィックデータの確認、省/プロバイダー別のグルーブごとの再生データの確認、再生HTTPステータスコードの詳細データの確認、ドメイン名によるリアルタイムダウンストリームの再生データの確認、ライブストリーミングパッケージの情報の確認などの機能をサポートします。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">証明書管理に関するAPI</a></td>
<td>ドメイン名による証明書のバインディング、証明書の追加/削除、証明書情報の取得、証明書情報リストの取得、ドメイン名証明書情報の取得、証明書の変更、ドメイン名と証明書のバインディング情報の変更、ドメイン名による証明書のバインディング解除が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">認証管理に関するAPI</a></td>
<td>再生認証keyの確認/変更、プッシュ認証keyの確認、プッシュ認証keyの変更が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">CSSタイムシフトに関するAPI</a></td>
<td>タイムシフトテンプレートの作成/削除/変更/取得、タイムシフトルールの作成/削除、タイムシフトルールリストの取得、タイムシフトストリームレコーディング詳細の検索、タイムシフトストリームリストの検索が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">CSSミックストリーミングに関するAPI</a></td>
<td>共通ミックストリーミングの作成/キャンセルが可能です。</td>
</tr>
</table>


### 付加価値サービス
<table>
<tr><th width=17%>機能名</th><th>機能概要</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31561">CSSトランスコーディング</a></td><td>CSSストリームを異なる仕様でトランスコーディングすることをサポートします。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31563">CSSレコーディング</a></td><td>APIを使用しライブストリーミングをレコーディングし、Tencent CloudのVODプラットフォームまたはCOSプラットフォームに保存することをサポートします。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31562">CSSスクリーンをキャプチャ</a></td><td>APIを使用しライブストリーミングのスクリーンをキャプチャし、Tencent CloudのCOSに保存することをサポートします。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31564">CSS識別</a></td><td>AIを活用しライブストリーミングのスクリーンキャプチャに対してポルノを識別し、識別結果を返すことをサポートします。 </td></tr>
<tr><td><a href="https://www.tencentcloud.com/document/product/1071/42210">新しいリアルタイムコミュニケーション（RTC）</a></td><td>TRTCをベースにして実装した超低遅延リアルタイムコミュニケーション機能をサポートします。</td></tr>
<tr><td><a href="https://www.tencentcloud.com/document/product/267/31565">新しいCSSタイムシフト</a></td><td>ライブストリーミングのストリーミング中に過去の任意時間のライブストリーミングコンテンツを再生する機能をサポートします。</td></tr>
<tr><td><a href="https://www.tencentcloud.com/document/product/267/53400">CSSスタンバイストリーム</a></td><td>ライブストリーミング中にストリーミング中止の場合、入力ソースを自動的にスタンバイストリームに切り替えて、プライマリストリームが復元されると、自動的にプライマリストリームに切り替える機能をサポートします。</td></tr>
</table>


### MLVB SDK
<table>
<tr><th width=17%>機能名</th><th>機能概要</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/1071">MLVB SDK</a></td><td>CSSプッシュ、基本美顔、フィルタ、CSS再生、CSSタイムシフト再生を一体化したMLVB SDKを提供します。</td></tr>
<tr><td><a href="https://www.tencentcloud.com/document/product/1143">Tencent Effect SDK(美顔エフェクトSDK)</a></td><td>Tencent Cloudは天天P図（Pitu）およびTencent youtu labと共同で打ち出した高度な動画処理ソリューションであり、ライブストリーミングの動画撮影向けに、フィルタ、美顔・スタイリング、スタンプ、ジェスチャー識別など充実したリアルタイムエフェクト機能を提供し、様々な撮影シーンをカバーして、ユーザーの多様な撮影ニーズを満たします。</td></tr>
</table>