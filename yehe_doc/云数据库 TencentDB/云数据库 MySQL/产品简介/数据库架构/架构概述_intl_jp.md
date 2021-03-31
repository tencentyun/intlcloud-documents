TencentDB for MySQLは、単一ノード（元のBasic Edition）、2ノード（元のHigh-availability Edition）および3ノード（元のFinance Edition）の3つのアーキテクチャをサポートしています。
>?元の単一ノード高IOエディションも単一ノードアーキテクチャであり、その分離ポリシーは汎用型です。

## インスタンスアーキテクチャの確認
- インスタンスを購入時に[MySQL購入ページ](https://buy.cloud.tencent.com/cdb)にログインし、「アーキテクチャ」で対応するアーキテクチャを選択します。
- 購入後、 [MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンスリストの「構成情報」カラムでインスタンスのアーキテクチャを確認します。

## 各アーキテクチャの比較
<table>
<thead>
<tr><th>アーキテクチャ</th><th >2ノード</th><th>3ノード</th><th colspan=2>単一ノード</th>
</thead>
<tbody><tr>
<td><a href="https://cloud.tencent.com/document/product/236/53253">分離ポリシー</a></td>
<td>汎用型</td><td>汎用型</td><td>汎用型</td><td>基本型</td></tr>
<tr>
<td>サポートされているバージョン</td>
<td>MySQL 5.5、5.6、5.7、8.0</td><td>MySQL 5.6、5.7、8.0</td><td>MySQL 5.6、5.7、8.0</td><td>MySQL 5.7</td></tr>
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
<td>ローカル NVMe SSD </td><td>ローカル NVMe SSD </td><td>ローカル NVMe SSD</td><td>高性能クラウドディスク</td></tr>
<tr>
<td>性能</td>
<td>最大240,000 IOPS</td><td>最大240,000 IOPS</td><td>-</td><td>IOPS範囲の計算式：<br>{min 1500 + 8 * ディスク容量、max 4500}</td></tr>
<tr>
<td>ユースケース</td>
<td>ゲーム、インターネット、モノのインターネット、電子商取引、物流、保険、証券などの業界の応用</td>
<td>ゲーム、インターネット、モノのインターネット、電子商取引、物流、保険、証券などの業界の応用</td>
<td>読み取り/書き込み分離</td>
<td>個人学習、ミニWebサイト、非コアの小規模企業システムおよび中規模から大規模の企業の開発テスト環境</td></tr>
</tbody></table>

## 関連ドキュメント
- サポートするTencentDB for MySQLバージョン：MySQL 8.0、MySQL 5.7、MySQL 5.6、MySQL 5.5。詳細については、[データベースバージョン](https://intl.cloud.tencent.com/document/product/236/31896)をご参照ください。
- TencentDB for MySQLは、マスターインスタンスと読み取り専用インスタンスをサポートします。詳細については、[データベースインスタンスタイプ](https://intl.cloud.tencent.com/document/product/236/7268)をご参照ください。
- TencentDB for MySQLは、アーキテクチャのタイプによってサポートされている機能が異なります。詳細については、 [機能比較一覧](https://intl.cloud.tencent.com/document/product/236/36007)をご参照ください。
