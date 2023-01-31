## 製品機能リスト
このドキュメントでは、さまざまなタイプのTencentDB for MySQLアーキテクチャでサポートされている機能の相違点およびこれから更新する最新機能について説明します。ユーザーは各アーキテクチャの機能をより良く理解し、最新の機能をより早く体験し、必要に応じてインスタンスを検討して購入することできます。
>?
>- 次の表の「-」は非対応を示します。
>-　対応するテーブルの表題をクリックすると、機能相違リストと更新前の機能リストの表示を切り替えることができます。

<table>
<thead><tr><th>機能属性</th><th>機能名称</th><th>2ノード</th><th>3ノード</th><th colspan = "2" >1ノード</th></tr></thead>
<tbody>
<tr>
<td rowspan="10">ライフサイクル</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/39794" target="_blank">分離ポリシー</a></td><td>汎用型、個別型</td><td>汎用型、個別型</td><td>汎用型（読取専用インスタンス）</td><td>基本型（クラウドディスク版）</td></tr>
<tr>
<td></td><td><li>MySQL 5.5</li><li>MySQL 5.6</li><li>MySQL 5.7</li><li>MySQL 8.0</li></td><td><li>MySQL 5.6</li><li>MySQL 5.7</li><li>MySQL 8.0</li></td><td><li>MySQL 5.6</li><li>MySQL 5.7</li><li>MySQL 8.0</li></td><td>MySQL 5.7、8.0に対応</td></tr>
<tr>
<td>ノード数</td><td>2</td><td>3</td><td>1</td><td>1</td></tr>
<tr>
<td>メモリ/ハードディスク</td><td>最高720GB/12TB</td><td>最高720GB/12TB</td><td>最高720GB/12TB</td><td>最高16GB/30T</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/37785" target="_blank">インスタンス作成</a></td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/7270" target="_blank">読取専用インスタンスの作成</a></td><td>対応（MySQL5.6、5.7、8.0のみ）</td><td>対応</td><td>対応</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/7272" target="_blank">ディザスタリカバリインスタンスの作成</a></td><td>対応（MySQL 5.6、5.7、8.0のみ）</td><td>対応</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31895" target="_blank">インスタンス廃棄</a></td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/47702" target="_blank">自動期間更新</a></td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td rowspan="4">インスタンス管理</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/10929" target="_blank">インスタンスメンテナンス時間の設定</a></td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8460" target="_blank">インスタンスにプロジェクトを指定</a></td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/19707" target="_blank">構成調整</a></td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/44337" target="_blank">アベイラビリティーゾーンの移行</a></td><td>対応</td><td>対応</td><td>-</td><td>-</td></tr>
<tr>
<td rowspan="2">アップデート</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8126" target="_blank">データベースエンジンバージョンのアップデート</a></td><td>対応（MySQL 5.5、5.6のみ）</td><td>対応</td><td>対応</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/36816" target="_blank">カーネルマイナーバージョンのアップデート</a></td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td>アーキテクチャのアップグレード</td><td><a href="https://intl.cloud.tencent.com/document/product/236/35986" target="_blank">2ノードから3ノードへのアップグレード</a></td><td>対応</td><td>-</td><td>-</td><td>-</td></tr>
<tr>
<td rowspan="2">対応エンジン</td>
<td>InnoDB</td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/47015" target="_blank">RocksDB</a></td><td>対応</td><td>対応</td><td>-</td><td>-</td></tr>
<tr>
<td rowspan="7">バックアップとロールバック</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/37796" target="_blank">自動バックアップ</a></td><td>対応</td><td>対応</td><td>-</td><td>対応</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/37796" target="_blank">手動バックアップ</a></td><td>対応</td><td>対応</td><td>-</td><td>対応</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38326" target="_blank">バックアップ削除</a></td><td>対応</td><td>対応</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38864" target="_blank">インスタンスクローン</a></td><td>対応</td><td>対応</td><td>-</td><td>対応</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/7276" target="_blank">ロールバック</a></td><td>対応</td><td>対応</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/37796" target="_blank">定期バックアップ保持</a></td><td>対応</td><td>対応</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://www.tencentcloud.com/document/product/236/51881" target="_blank">バックアップ暗号化</a></td><td>対応</td><td>対応</td><td>-</td><td>-</td></tr>
<tr>
<td rowspan="4">監視とアラーム</td>
<td>リソース監視</td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td>エンジン監視</td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td>配置監視</td><td>対応</td><td>対応</td><td>-</td><td>-</td></tr>
<tr>
<td>アラーム</td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td rowspan="6">アカウント管理</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31900" target="_blank">アカウント作成</a></td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/49197" target="_blank">パスワードの複雑さを設定する</a></td><td>対応</td><td>対応</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31901" target="_blank">パスワードリセット</a></td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31902" target="_blank">アカウント権限の変更</a></td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31903" target="_blank">アクセス認証済みのホストアドレスの変更</a></td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31904" target="_blank">アカウント削除</a></td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td>データベース管理</td><td><a href="https://intl.cloud.tencent.com/document/product/236/39221">DMCコンソール</a></td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td rowspan="4">データセキュリティ</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/14470">セキュリティグループ</a></td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/43496">データベース監査</a></td><td>対応（MySQL 5.6、5.7のみ）</td><td>対応</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38491">透明データの暗号化をオンにする</a></td><td>対応（MySQL 5.7、8.0のみ）</td><td>対応（MySQL 5.7、8.0のみ）</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/48452">SSL暗号化の設定</a></td><td>対応（MySQL 5.6、5.7、8.0のみ）</td><td>対応（MySQL 5.6、5.7、8.0のみ）</td><td>-</td><td>-</td></tr>
<tr>
<td rowspan="3">データチャネル</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8463">DTSサービス移行</a></td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8464">オフライン移行</a></td><td>対応</td><td>対応</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8466">SQLファイルのインポート</a></td><td>対応</td><td>対応</td><td>-</td><td>-</td></tr>
<tr>
<td rowspan="2">パラメータ管理</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/35793">インスタンスパラメータの設定</a></td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/47701">スマートパラメータの調整</a></td><td>対応</td><td>対応</td><td>-</td><td>-</td></tr>
<tr>
<td>ネットワーク</td><td><a href="https://intl.cloud.tencent.com/document/product/236/31915">ネットワーク切り替え</a></td><td>対応</td><td>対応</td><td>対応</td><td>対応</td></tr>
<tr>
<td rowspan="2">パフォーマンス</td><td><a href="https://intl.cloud.tencent.com/document/product/236/42048">データベースエージェント</a></td><td>対応</td><td>対応</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://www.tencentcloud.com/document/product/236/42048">データベースエージェント（新版）</a></td><td>対応</td><td>対応</td><td>-</td><td>-</td></tr>
</tbody>
</table>
