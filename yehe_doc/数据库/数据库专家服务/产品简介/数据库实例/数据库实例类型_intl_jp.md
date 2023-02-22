TencentDB for MySQLインスタンス、略してインスタンスは、Tencent Cloudで独立して動作するデータベース環境であり、ユーザーがTencentDB for MySQLサービスを購入する際の基本単位です。ユーザーはコンソールから、TencentDB for MySQLインスタンスを作成・変更・削除することができます。
それぞれのインスタンスは互いに独立し、リソースから隔離されています。インスタンス間でCPU・メモリ・IOなどを占有するといった問題はなく、各インスタンスはデータベースタイプ、バージョンなど独自の特性を持っています。システムには、インスタンスの動作を制御するための対応するパラメータがあります。

TencentDB for MySQLには次の3種類のデータベースインスタンスがあります：

<table>
<thead><tr>
<th>インスタンスタイプ</th><th width="20%">定義</th><th width="15%">アーキテクチャ</th><th>インスタンスリストが表示されるかどうか</th><th>機能</th></tr></thead>
<tbody><tr>
<td>マスターインスタンス</td><td>読み取り/書き込み可能なインスタンス</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/38331" target="_blank">シングルノード</a> <li><a href="https://intl.cloud.tencent.com/document/product/236/38329" target="_blank">デュアルノード</a><li><a href="https://intl.cloud.tencent.com/document/product/236/39783" target="_blank">トリプルノード</a></td>
<td>はい</td><td>マスターインスタンスは、読み取り専用インスタンスとディザスタリカバリインスタンスをマウントすることができ、読み取り/書き込み分離とオフサイトディザスターリカバリ機能を実装することができます</td></tr>
<tr>
<td>読み取り専用インスタンス</td><td>読み取り機能のみを提供するインスタンス</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38331" target="_blank">シングルノード</a></td><td>はい</td>
<td>読み取り専用インスタンスは単独で存在できず、マスターインスタンスに属する必要があります。唯一のデータソースはマスターインスタンスからの同期データのみで、マスターインスタンスと同じリージョンにのみ存在することができます</td></tr>
<tr>
<td>ディザスタリカバリインスタンス</td><td>クロスアベイラビリティーゾーンおよびクロスリージョンのディザスタリカバリ機能を提供するインスタンス</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/38329" target="_blank">2ノード</a><li><a href="https://intl.cloud.tencent.com/document/product/236/39783" target="_blank">3ノード</a><td>はい</td>
<td>ディザスタリカバリインスタンスは同期中にのみ読み取り可能です。ディザスタリカバリインスタンスは、マスターインスタンスとの同期関係を能動的に切断でき、マスターインスタンスに能動的に昇格させることができます。つまり、読み取り/書き込みのアクセス機能を提供することができます。この場合、マスターインスタンスとは離れた場所に配置することをお勧めします</td></tr>
</tbody></table>

### 関連情報
- 読み取り専用インスタンスの作成方法と注意事項については、[読み取り専用インスタンスの作成](https://intl.cloud.tencent.com/document/product/236/7270)をご参照ください。
- 読み取り専用インスタンスのROグループの作成と設定については、[読み取り専用インスタンスの管理](https://intl.cloud.tencent.com/document/product/236/11361)をご参照ください。
- ディザスタリカバリインスタンスの作成方法と注意事項については、[ディザスタリカバリインスタンスの管理](https://intl.cloud.tencent.com/document/product/236/7272)をご参照ください。
