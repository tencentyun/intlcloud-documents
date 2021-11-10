ユーザーがより迅速にコンソールについて理解し使用できるよう、ここでは一般的なサービスを様々なユーザーのそれぞれのニーズにもとづき、区分して整理しました。現在、コンソールは、各種ユースケースに使用される基本サービス、シナリオサービス、設定サービス、データサービスなどのモジュールに区分されています。

## 基本サービス
基本サービスは主にVOD基本サービスへのアクセスを提供するもので、ビデオのアップロード、処理および配信などのVODの基本機能が実現できます。基本的なVODサービスのみを使用したい場合は、この基本サービスモジュール内で操作するだけで済みます。
<table>
<tr><th width="17%">機能名</th><th>機能説明</th></tr>
<tr>
<td ><a href = "https://intl.cloud.tencent.com/document/product/266/2841">サービス概要</a></td>
<td><ul style = "margin-bottom: 0px;"><li>現在のアカウントの課金方式および課金帯域幅などの課金状況を確認できます。</li><li>ストレージ容量、トランスコード時間、使用トラフィック、使用帯域幅、審査時間を確認できます。</li></ul></td>
</tr><tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/33890">ビデオ管理</a></td>
<td><ul style= "margin: 0"><li>ビデオ、オーディオ、画像のアップロード、削除、確認、編集、フィルタリングなどの操作を行うことができます。</li><li>トランスコード、ウォーターマーク追加、ビデオ審査などのMPS操作を行うことができます。</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/39706">タスク管理</a></td>
<td>VOD内タスク処理の進捗および詳細を確認できます。</td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/14059">タスクフロー</a></td>
<td><ul style= "margin: 0"><li>オーディオビデオトランスコード、超高速HD（TESHD）、アダプティブビットレートストリーミング、ウォーターマーク、スクリーンキャプチャ、アニメーション画像生成、インテリジェント認識などのMPSテンプレートの設定を行うことができます。</li><li>タスクフローテンプレートを設定し、オーディオビデオに対しフロー化された処理を行うことができます。</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/33896#editing-basic-info">ビデオ再生</a></td>
<td><ul style= "margin: 0"><li>ビデオアクセラレーション再生リンクを取得できます。</li><li>ビデオとのリンクに対し認証とアクセス制御の設定を行うことができます。</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/7836">Player+</a></td>
<td><ul style= "margin: 0"><li>複数端末（iOS、Web、Android）の複数バージョンのプレーヤーをサポートしています。</li><li>サードパーティのプレーヤーのクラウドPAASリソースへのアクセスを可能にするプレーヤーAdapterバージョンを提供します。</li><li>解像度自動切換え、ファーストビューの高速表示、ジェスチャー制御などの多くの機能を提供します。</li><li>複数のコーデックのビデオ再生をサポートしています。</li></ul></td>
</tr>
</table>


## シナリオサービス
シナリオサービスでは、メディア資産冷却、インテリジェントビデオ認識、アプリケーション管理、License管理などを含む、VODのユースケースから派生したアップグレードサービスをご提供しています。関連のサービスを使用したい場合は、このモジュールで操作を行うことができます。
<table>
<tr><th width="17%">機能名</th><th>機能説明</th></tr>
<tr>
<td ><a href = "https://intl.cloud.tencent.com/document/product/266/42092">メディア資産冷却</a></td>
<td><ul style = "margin-bottom: 0px;"><li>メディアリソースのストレージタイプを変更できます。メディア資産冷却およびデータ取得機能を提供し、ユーザーのストレージコストを効果的に削減できます。</li><li>インテリジェント冷却ポリシーを設定し、指定したメディアリソース対する自動冷却を行うことができます。</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/33897">インテリジェントビデオ認識</a></td>
<td><ul style= "margin: 0"><li>インテリジェントビデオ認識のタスク結果を確認し、ビデオ内に不適切な内容が存在しないかを確認することで、ユーザーが健全なソーシャルネットワーク環境を構築できるよう支援することができます。</li><li>インテリジェント認識の結果に基づき、ビデオに対して新たな認識タスクを開始できます。</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/42093">アプリケーション管理</a></td>
<td><ul style= "margin: 0"><li>サブアプリケーションを作成してリソースを隔離できます。</li><li>サブアプリケーションに対して編集、無効化、破棄、有効化などの操作を行うことができます。</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/39429">License管理</a></td>
<td>UGSV SDK Licenseを管理できます。</td>
</tr>
</table>



## 設定サービス
設定サービスでは、ドメイン名管理、アップロードストレージ設定、コールバック設定、Super Player設定など、VODのカスタマイズ設定サービスをご提供します。これらが必要な場合は、このモジュールで関連の設定を実行できます。
<table>
<tr><th width="17%">機能名</th><th>機能説明</th></tr>
<tr>
<td ><a href = "https://intl.cloud.tencent.com/document/product/266/35572">ドメイン名管理</a></td>
<td><ul style = "margin-bottom: 0px;"><li>カスタムドメイン名を追加し、ドメイン名に対してCNAMEを設定できます。</li><li>既存のドメイン名について証明書管理、ホットリンク防止設定および海外CDN設定操作を実行できます。</li><li>デフォルト配信ドメイン名を設定できます。</li></ul></td>
</tr><tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/18874">アップロードストレージ設定</a></td>
<td><ul style= "margin: 0"><li>アップロードファイルのカテゴリー管理を行うことができます。</li><li>メディア資産のストレージリージョンをアクティブ化し、アップロードファイルのデフォルトのストレージリージョンを設定することができます。</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/14055">コールバック設定</a></td>
<td>イベント通知の方法、具体的なイベントおよび通知受信アドレスを設定できます。</td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/38261">Super Playerの設定</a></td>
<td>Super Playerの指定するアダプティブビットレートストリーミング、スプライトイメージ、解像度の名称などの設定を行うことができます。</td>
</tr>
</table>


## データサービス
データサービスは、トラフィック/帯域幅、ストレージ、トランスコード、インテリジェントビデオ認識などの使用量統計データ、ならびにVODファイルのアクセスおよび再生状況を時間単位で照会できる専門的なデータ統計およびデータ分析サービスを提供します。またユーザーのデータモニタリングおよびリソース管理に役立つログダウンロード機能を提供します。
<table>
<tr><th width="17%">機能名</th><th>機能説明</th></tr>
<tr>
<td ><a href = "https://intl.cloud.tencent.com/document/product/266/30421">使用量の統計</a></td>
<td>帯域幅/トラフィック、ストレージ容量、トランスコード、インテリジェントビデオ認識を確認できます。</td>
</tr><tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/30422">データ分析</a></td>
<td><ul style= "margin: 0"><li>独立IPアクセス総数、リクエスト総数などのアクセス状況のデータを確認できます。</li><li>ファイル再生状況、再生回数TOP100ビデオなどの再生状況データを確認できます。</li></ul></td>
</tr>
<tr>
<td><a href = "https://intl.cloud.tencent.com/document/product/266/7983">ログダウンロード</a></td>
<td>ドメイン名へのアクセス状況の詳細情報をダウンロードできます。1時間単位のCDNログ情報を提供しています。</td>
</tr>
</table>


