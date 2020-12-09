本節では、LVBの機能について説明します。機能の説明と利用方法の詳細については、対応するドキュメントをご参照ください。



### ライブブロードキャストプッシュ
<table>
<tr><th width=15%>機能名</th><th>機能概要</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/7968" target="_blank">プッシュプロトコル</a></td><td>RTMPプロトコルを使用したプロトコルをサポートします。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31558" target="_blank">プッシュ方式</a></td><td>Tencent Cloud LVBを統合したiOS、Android、またはWebなどのプッシュSDKのアプリケーション、およびOBS、XSplit、FMLEなどの一般的なサードパーティのプッシュソフトウェアをサポートします。</td></tr>
<tr><td>プッシュデバイス</td><td>一般的なサードパーティのRTMPプッシュハードウェア、エンコーダ、およびセットトップボックスなどをサポートします。</td></tr>
</table>


### LVB再生
<table>
<tr><th width=15%>機能名</th><th>機能概要</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/7968" target="_blank">再生プロトコル</a></td><td>RTMP、FLV、およびHLS再生プロトコルをサポートします。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31559" target="_blank">再生方式</a></td><td>Tencent Cloud LVB iOS、Android、Web などのPlayer+、および一般的なサードパーティのFLV、RTMP、HLS プレイヤーをサポートします。</td></tr>
<tr><td>再生制御</td><td>入力ストリームと同じ仕様の元のストリーム、またはリアルタイムでトランスコードされたストリームを再生できます。</td></tr>
</table>


 ### LVB管理
 <table>
<tr><th width=15%>機能名</th><th>機能概要</th></tr>
<tr><td>管理方法</td><td>LVBコンソールでのグラフィック化管理をサポートします。または、LVBのTencentCloud APIを呼び出して管理することも可能です。</td></tr>
</table>

### LVBコンソール
<table>
<tr><th width=15%>機能名</th><th>機能概要</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31054" target="_blank">概要</a></td><td>利用可能なLVBリソースパッケージトラフィックとLVBのリアルタイム帯域幅、トラフィックなどのデータを表示します。</td></tr>
<tr><td>ドメイン名管理</td><td>LVBプッシュドメイン名と再生ドメイン名の追加、変更、無効化、削除を行い、ドメイン名CNAMEレコード、HTTPS証明書、プッシュおよび再生認証などを設定できます。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31068" target="_blank">LVBストリーム管理</a></td><td>オンラインまたはLVBストリームの履歴情報をクエリーできます。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/34223" target="_blank">機能モジュール</a></td><td>LVBレコーディング、トランスコーディング、スクリーンキャプチャ、ポルノ検出、ウォーターマーク、コールバックなどの設定情報をクエリーまたは変更します。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31076" target="_blank">統計分析</a></td><td>LVBサービスの帯域幅、トラフィック、リクエスト数、同時接続数、スクリーンキャプチャ数、チャネル数、およびレコーディングチャネル数などの使用量をクエリーします。</td></tr>
<tr><td>LVB SDK</td><td>MLVB SDKの品質監視データとMLVBマイク接続時間（分単位）をクエリーします。</td></tr>
</table>


### LVBのセキュリティ
<table>
<tr><th width=15%>機能名</th><th>機能概要</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31059" target="_blank">プッシュ認証</a></td><td>プッシュURLリンク不正アクセス防止をサポートし、認証キーと時間切れ時間をカスタマイズできます。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31060" target="_blank">再生認証</a></td><td>ブラックリスト/ホワイトリストリンク不正アクセス防止、Refererリンク不正アクセス防止、および再生URLのリンク不正アクセス防止とリモート再生認証をサポートします。</td></tr>
</table>

​	
###  API 管理
<table>
<tr><th width=15%>機能名</th><th>機能概要</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E5.9F.9F.E5.90.8D.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">ドメイン名管理関連API</a></td>
			<td>ドメイン名の追加と削除、ドメイン名情報のクエリー、ドメイン名リストのクエリー、ドメイン名の有効化と無効化、および再生ドメイン名情報の変更に使用されます。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E5.AE.9E.E6.97.B6.E6.97.A5.E5.BF.97.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">リアルタイムロギング関連API</a></td>
			<td>ログURLを一括取得できます。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E5.BB.B6.E6.92.AD.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">遅延再生管理関連API</a></td>
			<td>再生の遅延、遅延再生リストの取得、または再生の再開に使用されます。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E5.BD.95.E5.88.B6.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">レコーディング管理関連API</a></td>
			<td>レコーディングタスクの作成、レコーディングルールの作成、レコーディングテンプレートの作成、レコーディングタスクの削除、レコーディングルールの削除、レコーディングテンプレートの削除、レコーディングルールリストの取得、単一のレコーディングテンプレートの取得、レコーディングテンプレートリストの取得、レコーディングテンプレート設定の変更、およびレコーディングの終了に使用されます。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E6.88.AA.E5.9B.BE.E9.89.B4.E9.BB.84.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">スクリーンキャプチャポルノ検出関連API</a></td>
			<td>スクリーンキャプチャルールの作成、スクリーンキャプチャテンプレートの作成、スクリーンキャプチャルールの削除、スクリーンキャプチャテンプレートの削除、スクリーンキャプチャルールリストの取得、単一のスクリーンキャプチャテンプレートの取得、スクリーンキャプチャテンプレートリストの取得、およびスクリーンキャプチャテンプレートの変更に使用されます。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E6.B0.B4.E5.8D.B0.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">ウォーターマーク管理関連API</a></td>
			<td>ウォーターマークの追加、ウォーターマークルールの作成、ウォーターマークの削除、ウォーターマークルールの削除、単一のウォーターマークの取得、ウォーターマークルールリストの取得、ウォーターマークリストのクエリー、またはウォーターマークの更新に使用されます。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E7.9B.B4.E6.92.AD.E5.9B.9E.E8.B0.83.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">LVBコールバック関連API</a></td>
			<td>コールバックルールの作成、コールバックテンプレートの作成、コールバックルールの削除、コールバックテンプレートの削除、コールバックルールリストの取得、単一のコールバックテンプレートの取得、コールバックテンプレートリストの取得、およびコールバックテンプレートの変更に使用されます。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E7.9B.B4.E6.92.AD.E6.8B.89.E6.B5.81.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">LVBプル関連API</a></td>
			<td>プル設定の追加、削除、クエリー、更新、およびプル設定状態の変更に使用されます。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E7.9B.B4.E6.92.AD.E6.B5.81.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">LVBストリーム管理関連API</a></td>
			<td>ストリーム禁止リストの取得、ストリーム中断イベントのクエリー、ライブブロードキャスト中のストリームのクエリー、ストリーム履歴リストのクエリー、ストリームステータスのクエリー、ライブブロードキャストストリームの中断、ライブブロードキャストストリームのプッシュ禁止、およびライブブロードキャストストリームのプッシュ再開に使用されます。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E7.9B.B4.E6.92.AD.E8.BD.AC.E7.A0.81.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">ライブブロードキャストトランスコード関連API</a></td>
			<td>トランスコーディングルールの作成、トランスコーディングテンプレートの作成、トランスコーディングルールの削除、トランスコーディングテンプレートの削除、トランスコーディングルールリストの取得、単一のトランスコーディングテンプレートの取得、トランスコーディングテンプレートリストの取得、またはトランスコーディングテンプレート設定の変更に使用されます。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E7.BB.9F.E8.AE.A1.E6.9F.A5.E8.AF.A2.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">統計クエリー関連API</a></td>
			<td>課金可能なLVB帯域幅とトラフィックデータのクエリー、地区とキャリアによる再生データのクエリー、HTTP再生ステータスコードの詳細のクエリー、ドメイン名レベルでのリアルタイムの下り再生データのクエリー、およびLVBパッケージ情報のクエリーに使用されます。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E8.AF.81.E4.B9.A6.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">証明書管理関連API</a></td>
			<td>ドメイン名への証明書バインディング、証明書の追加、証明書の削除、証明書情報の取得、証明書情報リストの取得、ドメイン名証明書情報の取得、証明書の変更、ドメイン名と証明書とのバインディング情報の変更、およびドメイン名からの証明書バインド解除が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760#.E9.89.B4.E6.9D.83.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3">認証管理関連API</a></td>
			<td>再生認証キーのクエリー、プッシュ認証キーのクエリー、再生認証キーの変更、およびプッシュ認証キーの変更に使用されます。</td>
</tr>
</table>


### 付加価値サービス
<table>
<tr><th width=15%>機能名</th><th>機能概要</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31561" target="_blank">LVBトランスコーディング</a></td><td> ライブスブロードキャストトリームをさまざまな仕様でトランスコーディングできます。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31562" target="_blank">LVBスクリーンキャプチャ</a></td><td>APIを介して、LVB中にスクリーンショットをキャプチャして、Tencent Cloud COSに保存します。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31564" target="_blank">LVB審査</a></td><td>ライブブロードキャストストリームのポルノ検出、暴力・テロ、および政治絡みなどのAIベースのインテリジェントな審査をサポートします。</td></tr>
<tr><td>LVBトランスコーディング</td><td>APIを介してライブブロードキャストストリームをレコーディングして、Tencent Cloud VODプラットフォームに保存することができます。</td></tr>
<tr><td>LVBタイムシフト</td><td>ライブストリーミング中の過去の任意の時点のコンテンツを再生できます。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31567" target="_blank">LVBグローバルアクセラレーション</a></td><td>中国本土以外でのTencent Cloud LVBサービスの使用をサポートします。</td></tr>
</table>



### ライブブロードキャストSDK
<table>
<tr><th width=15%>機能名</th><th>機能概要</th></tr>
<tr><td>Mobile Live Video Broadcasting SDK</td><td>LVBプッシュ、基本的な美顔フィルター、通常フィルター、LVB再生、LVBタイムシフトなどの機能を提供する統合ライブブロードキャストSDKです。</td></tr>
<tr><td>美顔エフェクトSDK</td><td>Tencent Cloud、天天P図、およびYouTuラボが共同で開発した高度なビデオ処理ソリューションであり、LVBビデオ撮影にフィルター、美顔フィルター、ステッカー、ジェスチャー認識などのさまざまなリアルタイム特殊エフェクトを提供しており、さまざまな撮影シナリオをカバーし、利用者の多様な撮影需要に対応します。</td></tr>
<tr><td>ILVB（ソリューション</td><td>MLVB SDKに基づくインタラクティブなライブブロードキャストマイク接続ソリューションです。</td></tr>
<tr><td>ミニプログラム・LVB（ソリューション）</td><td>LVBタグやLVBプラグインなどの機能を提供し、ユーザー保有ミニプログラムへの統合をサポートして、さまざまな資格を有する顧客にクロスプラットフォームLVB向けのミニプログラムLVBソリューションを提供します。</td></tr>
</table>

