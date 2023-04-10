TencentDB for MySQLは、単一ノード（クラウドディスクバージョン）、2ノード（元の高可用性バージョン）および3ノード（元のファイナンスバージョン）の3つのアーキテクチャをサポートしています。
>?単一ノード（クラウドディスクバージョン）のアーキテクチャは、現在サポートしているリージョンは上海、成都、広州、北京、香港で、その他のリージョンも順次オープンしていきます。
>
## インスタンスアーキテクチャの確認
- 購入時に[MySQL購入ページ](https://buy.cloud.tencent.com/cdb)にログインし、**アーキテクチャ**で対応するアーキテクチャを選択します。
- 購入後、[MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンスリストの**構成情報**でインスタンスのアーキテクチャを確認します。

## 各アーキテクチャの比較
<table>
<thead>
<tr><th>アーキテクチャ</th><th >2ノード</th><th>3ノード</th><th colspan=2>単一ノード</th>
</thead>
<tbody><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/39794">分離ポリシー</a></td>
<td>汎用型</td><td>汎用型</td><td>汎用型（読取専用インスタンス）</td><td>基本型</td></tr>
<tr>
<td>サポートされているバージョン</td>
<td>MySQL 5.5、5.6、5.7、8.0</td><td>MySQL 5.6、5.7、8.0</td><td>MySQL 5.6、5.7、8.0</td><td>MySQL 5.7、8.0</td></tr>
<tr>
<td>ノード</td>
<td>1マスター1スレーブ</td><td>1マスター2スレーブ</td><td>単一ノード</td><td>単一ノード</td></tr>
<tr>
<td>マスター・スレーブのレプリケーション方式</td>
<td>非同期（デフォルト）、半同期</td><td>非同期（デフォルト）、強い同期、半同期</td><td>-</td><td>-</td></tr>
<tr>
<td>インスタンス可用性</td>
<td>99.95%</td><td>99.99%</td><td>-</td><td>-</td></tr>
<tr>
<td>基盤となるストレージ</td>
<td>ローカルNVMe SSDディスク</td><td>ローカルNVMe SSDディスク</td><td>ローカルNVMe SSDディスク</td><td>SSD CBS<br>拡張型SSD CBS</td></tr>
<tr>
<td>性能</td>
<td>IOPS最大240000</td><td>IOPS最大240000</td><td>IOPS最大240000</td><td><li>SSD CBSランダムIOPS性能計算式：<br>min{1800 + 30 × 容量(GB), 26000}<li>SSD CBSスループット性能計算式(MB/s)：<br>min{120 + 0.2 × 容量(GB), 260}<li>拡張型SSD CBSランダムIOPS性能計算式：<br>min{1800 + 50 × 容量（GB）, 50000}<li>拡張型SSD CBSスループット性能計算式(MB/s)：<br>min{120 + 0.5 × 容量(GB), 350}</td></tr>
<tr>
<td>ユースケース</td>
<td>ゲーム、インターネット、モノのインターネット、電子商取引、物流、保険、証券などの業界の応用</td>
<td>ゲーム、インターネット、モノのインターネット、電子商取引、物流、保険、証券などの業界の応用</td>
<td>読み取り/書き込み分離要求の応用</td>
<td>個人学習、ミニWebサイト、非コアの小規模企業システムおよび中規模から大規模の企業の開発テスト環境</td></tr>
</tbody></table>

##  関連ドキュメント
- サポートするTencentDB for MySQLバージョン：MySQL 8.0、MySQL 5.7、MySQL 5.6、MySQL 5.5。詳細については、[データベースバージョン](https://intl.cloud.tencent.com/document/product/236/31896)をご参照ください。
- TencentDB for MySQLは、マスターインスタンス、読み取り専用インスタンスおよびディザスタリカバリインスタンスをサポートします。詳細については、[データベースインスタンスタイプ](https://intl.cloud.tencent.com/document/product/236/7268)をご参照ください。
- TencentDB for MySQLは、アーキテクチャのタイプによってサポートされている機能が異なります。詳細については、 [機能比較一覧](https://intl.cloud.tencent.com/document/product/236/36007)をご参照ください。
