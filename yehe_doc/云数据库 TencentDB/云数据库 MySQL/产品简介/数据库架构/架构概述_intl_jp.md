TencentDB for MySQLは高可用性エディション、ファイナンスエディション、単一ノード高IOエディション、ベーシックエディションの4つのアーキテクチャをサポートしています。単一ノード高IOエディションは現在、[読み取り専用インスタンス](https://intl.cloud.tencent.com/document/product/236/7270)にのみ適用します。

## インスタンスアーキテクチャの確認
- 購入時に[MySQL購入ページ](https://buy.cloud.tencent.com/cdb)にログインし、「アーキテクチャ」で対応するアーキテクチャを選択します。
![](https://main.qcloudimg.com/raw/5bbc8288b981097d8f6b36e150ddf7e2.png)
- 購入後、[MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンスリストの「構成」カラムでインスタンスのアーキテクチャを確認します。
![](https://main.qcloudimg.com/raw/f0618995c7b9f4821c0d4f18ce4a6f45.png)


## 各アーキテクチャの比較
<table>
<thead>
<tr><th width="15%">アーキテクチャ</th><th width="20%">高可用性エディション</th><th width="20%">ファイナンスエディション</th><th width="20%">単一ノード高IOエディション</th><th width="25%">ベーシックエディション</th></tr>
</thead>
<tbody><tr>
<td>サポートされているバージョン</td>
<td>MySQL 5.5、5.6、5.7、8.0</td>
<td>MySQL 5.6、5.7、8.0</td>
<td>MySQL 5.6、5.7、8.0</td>
<td>MySQL 5.7</td>
</tr>
<tr>
<td>ノード</td>
<td>1マスター1スレーブ</td>
<td>1マスター2スレーブ</td>
<td>単一ノード</td>
<td>単一ノード</td>
</tr>
<tr>
<td>マスター・スレーブのレプリケーション方式</td>
<td>非同期（デフォルト）、半同期</td>
<td>非同期（デフォルト）、強い同期、半同期</td>
<td>-</td>
<td>-</td>
</tr>
<tr>
<td>インスタンス可用性</td>
<td>99.95%</td>
<td>99.99%</td>
<td>-</td>
<td>-</td>
</tr>
<tr>
<td>基盤となるストレージ</td>
<td>ローカルNVMe SSDハードディスク</td>
<td>ローカルNVMe SSDハードディスク</td>
<td>ローカルNVMe SSDハードディスク</td>
<td>高性能クラウドディスク</td>
</tr>
<tr>
<td>性能</td>
<td>IOPSは最大240000</td>
<td>IOPSは最大240000</td>
<td>-</td>
<td>IOPS範囲の計算式：<br>{min 1500 + 8 * ディスク容量、max 4500}</td>
</tr>
<tr>
<td>適用シナリオ</td>
<td>ゲーム、インターネット、モノのインターネット、電子商取引、物流、保険、証券などの業界の応用</td>
<td>ゲーム、インターネット、モノのインターネット、電子商取引、物流、保険、証券などの業界の応用</td>
<td>リード・ライト分離ニーズの応用</td>
<td>個人学習、ミニWebサイト、非コアの小規模企業システムおよび中規模から大規模の企業の開発テスト環境</td>
</tr>
</tbody></table>

## 関連ドキュメント
- サポートするTencentDB for MySQLバージョン：MySQL 8.0、MySQL 5.7、MySQL 5.6、MySQL 5.5。詳細については[データベースバージョン](https://intl.cloud.tencent.com/document/product/236/31896)をご参照ください。
- TencentDB for MySQLでサポートされているインスタンスのタイプ：マスターインスタンス、読み取り専用インスタンス、災害復旧インスタンス。詳細については[データベースインスタンスタイプ](https://intl.cloud.tencent.com/document/product/236/7268)をご参照ください。
- TencentDB for MySQLは、アーキテクチャのタイプによってサポートされている機能が異なります。詳細については、[機能の違いのリスト](https://intl.cloud.tencent.com/document/product/236/36007)をご参照ください。
