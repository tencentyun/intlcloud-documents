このドキュメントでは、ライブストリーミング製品の機能を説明します。より具体的な機能の説明と使用方法については、対応する詳細なドキュメントをご確認ください。





### ライブストリーミングのプッシュ
<table>
<tr><th width=15%>機能名</th><th>機能概要</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/7968" target="_blank">プッシュプロトコル</a></td><td>RTMPプロトコルのプッシュをサポートしています。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31558" target="_blank">プッシュ方式</a></td><td>Tencent LVBのiOS、Android、Web版などのプッシュSDKを統合したApp、および一般的なサードパーティー製プッシュソフトウェア（OBS/XSplit/FMLEなど）をサポートしています。</td></tr>
<tr><td>プッシュデバイス</td><td>一般的なサードパーティー製RTMPプッシュハードウェアおよびエンコーダ装置またはボックスなどのデバイスをサポートしています。</td></tr>
</table>


### ライブストリーミング再生
<table>
<tr><th width=15%>機能名</th><th>機能概要</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/7968" target="_blank">再生プロトコル</a></td><td>RTMP、FLV 、HLSの3種類の再生プロトコルをサポートしています。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31559" target="_blank">再生方式</a></td><td>Tencent LVBのiOS、Android、Web版などのプレーヤーSDK、および一般的なサードパーティー製 FLV、RTMP、HLS形式のプレーヤーをサポートしています。</td></tr>
<tr><td>再生制御</td><td>入力ストリームと仕様が一致するオリジナルストリームを再生、またはリアルタイムのトランスコーディングを経たストリームを再生できます。</td></tr>
</table>


 ### ライブストリーミング管理
 <table>
<tr><th width=15%>機能名</th><th>機能概要</th></tr>
<tr><td>管理方式</td><td>ライブストリーミング管理コンソールでのグラフィック化による管理、またはLVB Cloud APIの呼び出しによる管理をサポートしています。</td></tr>
</table>

### ライブストリーミングコンソール
<table>
<tr><th width=15%>機能名</th><th>機能概要</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31054" target="_blank">概要</a></td><td>ライブストリーミングのリアルタイムな帯域幅、トラフィックなどのデータを確認できます。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/35970" target="_blank">ドメイン名管理</a></td><td>ライブストリーミングのプッシュおよび再生ドメイン名の新規追加、修正、使用禁止、削除ができ、ドメイン名CNAMEの設定、HTTPS証明書、プッシュおよび再生認証なども可能です。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31068" target="_blank">ライブストリーミング管理</a></td><td>オンラインまたは履歴のライブストリーミング情報を確認します。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/34223" target="_blank">機能コンポーネント</a></td><td>ライブストリーミングレコーディング、トランスコーディング、スクリーンキャプチャ、ポルノ検出、ウォーターマーク、コールバックなどの設定情報を確認または修正します。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31076" target="_blank">統計分析</a></td><td>ライブストリーミングサービスの帯域幅、トラフィック、リクエスト数、並列接続数、スクリーンキャプチャ数、チャネル数、レコーディングパス数などの利用量統計情報を確認します。</td></tr>
<tr><td>ライブストリーミング SDK</a></td><td>MLVB SDKの品質監視データ、およびMLVBのマイク接続分数の情報を確認します。</td></tr>
</table>


### ライブストリーミングのセキュリティ
<table>
<tr><th width=15%>機能名</th><th>機能概要</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31059" target="_blank">プッシュ認証</a></td><td>プッシュURLのホットリンク防止をサポートし、認証Keyおよび期限切れの時間をカスタマイズできます。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31060" target="_blank">再生認証</a></td><td>ブラックリスト/ホワイトリストによるホットリンク防止、Refererによるリンク不正アクセス防止、再生URLのホットリンク防止、再生のリモート認証をサポートしています。</td></tr>
</table>

​    
###  APIの管理
<table>
<tr><th width=15%>機能名</th><th>機能概要</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">ドメイン名管理に関するAPI</a></td>
            <td>ドメイン名の追加、ドメイン名の削除、ドメイン名情報の確認、ドメイン名リストの確認、ドメイン名の有効化、ドメイン名の使用禁止、再生ドメイン名情報の修正が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">リアルタイムログに関するAPI</a></td>
            <td>ログURLの一括取得が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">再生遅延管理に関するAPI</a></td>
            <td>再生の遅延、ライブストリーミング再生遅延リストの取得、再生遅延のリカバーが可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">レコーディング管理に関するAPI</a></td>
            <td>レコーディングタスクの作成、レコーディングルールの作成、レコーディングテンプレートの作成、レコーディングタスクの削除、レコーディングルールの削除、レコーディングテンプレートの削除、レコーディングルールリストの取得、単独のレコーディングテンプレートの取得、レコーディングテンプレートリストの取得、レコーディングテンプレート設定の修正、レコーディングタスクの終了が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">スクリーンキャプチャ・ポルノ検出に関するAPI</a></td>
            <td>スクリーンキャプチャルールの作成、スクリーンキャプチャテンプレートの作成、スクリーンキャプチャルールの削除、スクリーンキャプチャテンプレートの削除、スクリーンキャプチャルールリストの取得、単独のスクリーンキャプチャテンプレートの取得、スクリーンキャプチャテンプレートリストの取得、スクリーンキャプチャテンプレートの修正が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">ウォーターマーク管理に関するAPI</a></td>
            <td>ウォーターマークの追加、ウォーターマークルールの作成、ウォーターマークの削除、ウォーターマークルールの削除、単独のウォーターマークの取得、ウォーターマークルールリストの取得、ウォーターマークリストの確認、ウォーターマークの更新が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">LVBコールバックに関するAPI</a></td>
            <td>コールバックルールの作成、コールバックテンプレートの作成、コールバックルールの削除、コールバックテンプレートの削除、コールバックルールリストの取得、単独のコールバックテンプレートの取得、コールバックテンプレートリストの取得、コールバックテンプレートの修正が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">LVBプルに関するAPI</a></td>
            <td>プル設定の追加、プル設定の削除、プル設定の確認、プル設定の更新、プル設定状態の修正が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">LVB管理に関するAPI</a></td>
            <td>プッシュ禁止リストの取得、プッシュ切断イベントの確認、ライブストリーミング中のストリーミングの確認、ストリーミング履歴リストの確認、ストリーミング状態の確認、ライブストリーミングの切断、ライブストリーミングのプッシュ禁止、ライブストリーミングプッシュの回復が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">LVBトランスコードに関するAPI</a></td>
            <td>トランスコーディングルールの作成、トランスコーディングテンプレートの作成、トランスコーディングルールの削除、トランスコーディングテンプレートの削除、トランスコーディングルールリストの取得、単独のトランスコーディングテンプレートの取得、トランスコーディングテンプレートリストの取得、トランスコーディングテンプレート設定の修正が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">統計クエリーに関するAPI</a></td>
            <td>LVB課金帯域幅およびトラフィックデータのクエリー、省およびプロバイダーグルーブごとの再生データのクエリー、再生 HTTP ステータスコードの詳細データのクエリー、リアルタイムのドメイン名次元の下り再生データのクエリー、ライブストリーミングパッケージ情報のクエリーなどの機能がサポートされています。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">証明書管理に関するAPI</a></td>
            <td>ドメイン名証明書のバインディング、証明書の追加、証明書の削除、証明書情報の取得、証明書情報リストの取得、ドメイン名証明書情報の取得、証明書の修正、ドメイン名および証明書バインディング情報の修正、ドメイン名証明書のバインディング解除が可能です。</td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30760">認証管理に関するAPI</a></td>
            <td>再生認証keyの確認、プッシュ認証keyの確認、再生認証keyの修正、プッシュ認証keyの修正が可能です。</td>
</tr>
</table>


### 付加価値サービス
<table>
<tr><th width=15%>機能名</th><th>機能概要</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31561" target="_blank">LVBトランスコード</a></td><td> ライブストリーミングに対して多様な仕様のトランスコーディングをサポートしています。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31562" target="_blank">LVBスクリーンキャプチャ</a></td><td>APIを介してライブストリーミング中にスクリーンキャプチャし、Tencent Cloud COSのサーバーに保存します。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31564" target="_blank">LVB識別</a></td><td>AIがライブストリーミングのスクリーンキャプチャのポルノを識別し、識別結果を返す機能をサポートしています。 </td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31563" target="_blank">ライブストリーミングレコーディング</a></td><td>APIを介して ライブストリーミングのプロセスをレコーディングし、Tencent Cloud VODプラットフォームに保存する機能をサポートしています。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31565" target="_blank">LVBタイムシフト</a></td><td>ユーザーがライブストリーミングのストリーミング中に過去の任意の時間のライブストリーミングコンテンツを再生する機能をサポートしています。</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/31567" target="_blank">LVB Global Content Delivery</a></td><td>海外でのTencent LVBサービスの利用をサポートしています。</td></tr>
</table>



### ライブストリーミングSDK
<table>
<tr><th width=15%>機能名</th><th>機能概要</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/zh/document/product/1071" target="_blank">MLVB SDK</a></td><td>ライブストリーミングプッシュ、基本美顔、フィルタ、ライブストリーミング再生、ライブストリーミングタイムシフト再生を一体化したライブストリーミングSDKを提供します。 </td></tr>
<tr><td>美顔特殊効果 SDK</a></td><td>Tencent Cloudと天天P図（Pitu）、Tencent youtu labが共同で打ち出した高度な動画処理ソリューションとなり、ライブストリーミングの動画撮影のためにフィルタ、美顔・スタイリング、スタンプ、ジェスチャー識別などの多数のリアルタイム特殊効果機能を提供して、様々な撮影シナリオをカバーし、ユーザーの多様な撮影ニーズを満たします。</td></tr>
<tr><td>ILVB（ソリューション）</a></td><td>MLVB SDKのライブストリーミングマイク接続機能をベースとするインタラクティブなソリューションです。</td></tr>
</table>

