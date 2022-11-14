
## 2022年07月
<table>
<thead><tr><th width=20%>ダイナミックネーム</th><th width=50%>動的記述</th><th width=15%>リリース時間</th><th width=15%>関連ドキュメント</th></tr></thead>
<tbody>
<tr>
<td>パスワードの複雑さをサポートする</td>
<td>TencentDB for MySQLはパスワードの複雑さをサポートし、データベースアクセスパスワードの強度を高め、データベースの安全性を保障します。</td>
<td>2022-07-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/49197" target="_blank">パスワードの複雑さを設定する</a></td></tr>
</tbody></table>

## 2022年6月
<table>
<thead><tr><th width=20%>ダイナミックネーム</th><th width=50%>動的記述</th><th width=15%>リリース時間</th><th width=15%>関連ドキュメント</th></tr></thead>
<tbody>
<tr>
<td>SSL暗号化をサポートしています</td>
<td>TencentDB for MySQLは、SSL暗号化をサポートしています。暗号化伝送チャネル確立を実現し、通信データの安全性と完全性を向上させました</td>
<td>2022-06-27</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/48452" target="_blank">SSL暗号化設定</a></td></tr>
</tbody></table>

## 2022年4月
<table>
<thead><tr><th width=20%>ダイナミックネーム</th><th width=50%>動的記述</th><th width=15%>リリース時間</th><th width=15%>関連ドキュメント</th></tr></thead>
<tbody>
<tr>
<td>スマートパラメータチューニングをサポートしています</td>
<td>TencentDB for MySQLは、スマートパラメータチューニング機能をサポートしています。ユーザーによるデータベース機能の向上を支援します。</td>
<td>2022-04-25</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/47701" target="_blank">スマートパラメータチューニング</a></td></tr>
<tr>
<td>TXRocksエンジンをサポートしています</td>
<td>TencentDB for MySQLは、TXRocksトランザクション型ストレージエンジンをサポートしています。性能はInnoDBとほぼ同じですが、ストレージ容量はInnoDBと比べてさらに節約されているため、トランザクションの読み取り/書き込みにパフォーマンスが要求され、データのストレージ量が大きい業務に適しています。</td>
<td>2022-04-18</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/47015" target="_blank">TXRocks概要</a></td></tr>
<tr>
<td>定期バックアップをサポートしています</td>
<td>定期バックアップを使用することにより、2つのサイクルプランでバックアップされます。単一サイクルでのバックアップポリシーと比べて、より一層のコスト節約を実現できます。</td>
<td>2022-04-02</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/37796" target="_blank">バックアップデータベース</a></td></tr>
</tbody></table>


## 2022年02月
<table>
<tr><th width=20%>ニュース名</th><th width=50%>ニュース概要</th><th width=10%>リリース時間</th><th width=20%>関連記事</th></tr>
<tbody>
<tr>
<td>データベースプロキシが接続プールをサポート</td>
<td>TencentDB for MySQLのデータベースプロキシが接続プール機能をサポートするようになりました。サポートするセッションレベル接続プールは、ショートコネクショントランザクションが新しい接続を頻繁に確立することによるデータベースインスタンスの高負荷を解決できます。</td>
<td>2022-02</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/45622" target="_blank">接続プールの概要</a></td></tr>
<tr>
<tr>
<td>データベースプロキシ機能の最適化と更新</td>
<td>TencentDB for MySQLのデータベースプロキシは、機能の最適化と更新により、プロキシカーネルのサブバーション更新、ネットワーク切替、自動設定調整をサポートし、より優れた性能と利便性を提供します。</td>
<td>2022-02</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/45627" target="_blank">プロキシカーネルのサブバーション更新</a><br
><li><a href="https://intl.cloud.tencent.com/document/product/236/45628" target="_blank">データベースプロキシのネットワーク切替</a><br
><li><a href="https://intl.cloud.tencent.com/document/product/236/45629" target="_blank">データベースプロキシの設定調整</a></td></tr>
</tbody></table>

## 2021年12月
<table>
<tr><th width=20%>更新</th><th width=50%>説明</th><th width=10%>発表時間</th><th width=20%>関連ドキュメント</th></tr>
<tbody>
<tr>
<td>ROグループ遅延設定の最適化</td>
<td>TencentDB for MySQL ROの遅延設定を、インスタンス設定からROグループ設定に変更して、ROグループに設定された遅延と排除ポリシーが相互排他を起こさないようにし、ROインスタンス遅延の管理を簡素化します。ROグループの統一IPアドレスでアクセスする場合に、遅延ROインスタンスがあることが原因で、アクセスデータが予想と異なることはありません。</td>
<td>2021-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/41085" target="_blank">読み取り専用インスタンスの遅延レプリケーションの管理</a></td></tr>
<tr>
<td>アベイラビリティーゾーンの移行のサポート</td>
<td>TencentDB for MySQLは、アベイラビリティーゾーンを移行する機能をリリースしました。この機能は、ビジネスへの近場からのアクセス、リソースの拡張を実現し、リージョンにおけるさまざまなアベイラビリティーゾーンでのリソースの最大限の活用を可能にします。</td>
<td>2021-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/44337" target="_blank">アベイラビリティーゾーンの移行</a></td></tr>
<tr>
<td>パラメータテンプレートと新規購入インスタンスの最適化</td>
<td>TencentDB for MySQLは、パラメータの関連機能と出荷フローの最適化を行います。今回の最適化には、パラメータテンプレートの作成、パラメータの比較、パラメータテンプレートの適用、パラメータの変更などの機能や変更可能なパラメータおよび新規購入インスタンスの最適化の更新が含まれます。</td>
<td>2021-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/43459" target="_blank">パラメータテンプレートと新規購入インスタンスの最適化</a></td></tr>
</tbody></table>


## 2021年07月
<table>
<tr><th width=20%>更新</th><th width=50%>説明</th><th width=10%>発表時間</th><th width=20%>関連ドキュメント</th></tr>
<tbody>
<tr>
<td>スピーディな設定変更のサポート</td>
<td>TencentDB for MySQLには新しくスピーディな設定変更機能が追加されています。残りのローカルリソースが十分にある場合、データベースの設定が調整されると、スピーディな設定変更機能がトリガーされます。スピーディな設定変更にはデータ移行は伴わないため、準備段階での待機時間が短縮され、よりすばやくインスタンス仕様の調整が行えます。</td>
<td>2021-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/19707" target="_blank">データベースインスタンス仕様の調整</a></td></tr>
</tbody></table>

## 2021年04月
<table>
<tr><th width=20%>更新</th><th width=50%>説明</th><th width=10%>発表時間</th><th width=20%>関連ドキュメント</th></tr>
<tbody>
<tr>
<td>binlog使用容量のディスク総使用容量への計上についての説明</td>
<td>binlogの書き込み速度はデータベース稼働時の性能に影響します。TencentDB for MySQLの性能および安定性を向上させるため、TencentDB for MySQLでは、binlogのストレージに対するアップグレード実施し、今回のアップグレードによって、インスタンスbinlogのストレージメディアを高性能SSD（ユーザーインスタンスのストレージキャパシティ）に移行します。</td>
<td>2021-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/40209" target="_blank">binlog使用容量のディスク総使用容量への計上についての説明</a></td></tr>
<tr>
<td>ローカルbinlogの保存期間の設定をサポートします</td>
<td>TencentDB for MySQLは、コンソールからのローカルbinlog保存期間の設定をサポートしています。</td>
<td>2021-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/40186" target="_blank">ローカルbinlogの保存設定</a></td></tr>
</tbody></table>

## 2021年03月
<table>
<tr><th width=20%>更新</th><th width=50%>説明</th><th width=10%>発表時間</th><th width=20%>関連ドキュメント</th></tr>
<tbody>
<tr>
<td>製品アーキテクチャ（名称）のアップグレード</td>
<td>TencentDB for MySQL製品アーキテクチャを単一ノード（元のBasic Edition）、2ノード（元のHigh-availability Edition）および3ノード（元のFinance Edition）にアップグレードし、分離ポリシーに基本型、汎用型および専用型を追加します。各アーキテクチャ機能に変更はありません。</td>
<td>2021-03</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/38328" target="_blank">アーキテクチャの概要</a><li><a href="https://intl.cloud.tencent.com/document/product/236/39794">分離ポリシー</a></td></tr>
<tr>
<td>読み取り専用インスタンスは独立したイントラネットアドレスをサポートします</td>
<td>読み取り専用インスタンスは独立したイントラネットアドレスの有効化をサポートし、イントラネットのIPとポートのカスタム変更をサポートします。</td>
<td>2021-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/7270" target="_blank">読み取り専用インスタンスの作成</a></td></tr>
</tbody></table>

## 2020年11月
<table>
<tr>
<th width=20%>更新</th>
<th width=50%>説明</th>
<th width=10%>発表時間</th>
<th width=20%>関連ドキュメント</th>
</tr>
<tbody>
<tr>
<td>クローンインスタンスをサポートします</td>
<td>TencentDB for MySQLは、クローン作成により、インスタンスをログバックアップ保存期間中の任意の時点に復元し、さらに指定された物理バックアップのバックアップセットへ復元する機能をサポートしています。</td>
<td>2020-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38864" target="_blank">クローンインスタンス</a></td>
</tr>
</tbody></table>

## 2020年10月
<table>
<tr>
<th width=20%>更新</th>
<th width=50%>説明</th>
<th width=10%>発表時間</th>
<th width=20%>関連ドキュメント</th>
</tr>
<tbody><tr>
<td>購入画面の機能が最適化されました</td>
<td>TencentDB for MySQLの購入画面で、アラームポリシー、パラメータテンプレート、クロスプロジェクトを指定してセキュリティグループをバインドする機能をサポートします。</td>
<td>2020-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/37785" target="_blank">MySQLインスタンスの作成</a></td
</tr>
<tr>
<td>8.0はTDE機能（透過的データ暗号化）をサポートします</td>
<td>TencentDB for MySQL 8.0バージョンはTDE（透過的データ暗号化）機能をサポートします。</td>
<td>2020-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38491" target="_blank">Transparent Data Encryptionの有効化</a></td>
</tr>
</tbody></table>

## 2020年08月
<table>
<tr>
<th width=20%>更新</th>
<th width=50%>説明</th>
<th width=10%>発表時間</th>
<th width=20%>関連ドキュメント</th>
</tr>
<tbody><tr>
<td>MySQL 8.0をサポートします</td>
<td>TencentDB for MySQL 8.0をサポートし、完備された管理制御サービスとTXSQLカーネルを結合させ、より速く、より安定したエンタープライズ向けのサービスを提供します。豊富な業界シナリオで、お客様の業界のグレードアップを支援します。</td>
<td>2020-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31896" target="_blank">データベースバージョン</a></td>
</tr>
</tbody></table>

## 2020年07月
<table>
<tr>
<th width=20%>更新</th>
<th width=50%>説明</th>
<th width=10%>発表時間</th>
<th width=20%>関連ドキュメント</th>
</tr>
<tbody><tr>
<td>インスタンスへのパラメータテンプレートの利用をサポートします</td>
<td>TencentDB for MySQLはパラメータテンプレートにより複数のインスタンスのパラメータを同時に変更する機能をサポートします。またカスタマイズした時間を選択してパラメータ変更のタスクを実行することができ、パラメータ変更タスクのキャンセルもサポートします。</td>
<td>2020-07</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/35793" target="_blank">インスタンスのパラメータ設定</a><li><a href="https://intl.cloud.tencent.com/document/product/236/31906" target="_blank">パラメータテンプレートの使用</a></td>
</tr>
<tr>
<td>TDE機能（透過的データ暗号化）をサポートします</td>
<td>TencentDB for MySQLでは、TDE（透過的データ暗号化）機能を提供しています。TDEとは、データの暗号化/復号操作をユーザーに対して透明にすることを指し、データファイルに対するリアルタイムな I/Oの暗号化と復号化をサポートしています。データをディスクに書き込む前に暗号化して、ディスクから内部記憶装置に読み込む時に復号しますので、静的データの暗号化におけるコンプライアンス要件を満たすことができます。</td>
<td>2020-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38491" target="_blank">Transparent Data Encryptionの有効化</a></td>
</tr>
</tbody></table>

## 2020年06月
<table>
<tr>
<th width=20%>更新</th>
<th width=50%>説明</th>
<th width=10%>発表時間</th>
<th width=20%>関連ドキュメント</th>
</tr>
<tbody><tr>
<td>カーネルマイナーバージョンの手動アップデートをサポートします</td>
<td>TencentDB for MySQLは、カーネルのマイナーバージョンの手動アップデートをサポートします。カーネルマイナーバージョンをアップデートすれば、新機能を利用でき、パフォーマンスを向上させ、トラブルシューティングなどを実現することが可能です。</td>
<td>2020-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/36816" target="_blank">カーネルマイナーバージョンのアップデート</a></td>
</tr>
</tbody></table>

## 2020年04月
<table>
<thead>
<tr>
<th width=20%>更新</th>
<th width=50%>説明</th>
<th width=10%>発表時間</th>
<th width=20%>関連ドキュメント</th>
</tr>
</thead>
<tbody><tr>
<td>High-Availability Edition （1マスター/2スレーブ）をFinance Editionに改名します</td>
<td>Finance Editionには、1マスター/2スレーブの3ノードのアーキテクチャを採用しており、強い同期のレプリケーション方式をサポートします。リアルタイムなホットバックアップにより、データの高い一貫性が確保され、金融業界レベルの信頼性と高可用性を実現します。</td>
<td>2020-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">データベースアーキテクチャ</a></td>
</tr>
<tr>
<td>古いIPアドレスの回収時間をカスタマイズできます</td>
<td>ネットワークが切り替えられた場合、古いIPアドレスの回収時間を0～168時間の範囲で設定できます。古いIPアドレスの回収時間を0時間に設定すると、ネットワークの切り替え後にすぐに古いIPアドレスが回収されます。</td>
<td>2020-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31915" target="_blank">ネットワーク切り替え</a></td>
</tr>
</tbody></table>

## 2020年01月

<table>
<thead>
<tr>
<th width=20%>更新</th>
<th width=50%>説明</th>
<th width=10%>発表時間</th>
<th width=20%>関連ドキュメント</th>
</tr>
</thead>
<tbody><tr>
<td>TencentDB for DBbrainをサポートします</td>
<td>TencentDB for DBbrain (DBbrain)とは、データベースのインテリジェント診断と最適化を行う製品です。同時に、ユーザーと協力してソースの予防を行い、リアルタイムにデータベースを保護して、障害原因を効率よく特定し、解決策をユーザーに提供します。</td>
<td>2020-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1035/36027" target="_blank">TencentDB for DBbrain</a></td>
</tr>
<tr>
<td>スローログの詳細、エラーログの詳細のクエリをサポートします</td>
<td>TencentDB for MySQL（Basic Editionを含まない）インスタンスは操作ログ管理機能を提供します。コンソールの操作ログページで、インスタンスのスローログの詳細、エラーログの詳細、ロールバックログの表示及びスローログのダウンロードを行うことができます。</td>
<td>2020-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/34588" target="_blank">操作ログ</a></td>
</tr>
</tbody></table>

## 2019年12月

<table>
<thead>
<tr>
<th width=20%>更新</th>
<th width=50%>説明</th>
<th width=10%>発表時間</th>
<th width=20%>関連ドキュメント</th>
</tr>
</thead>
<tbody><tr>
<td>MySQLバックアップの商用化料金</td>
<td>MySQLインスタンスのバックアップが無料スペースを超えた分について、課金が開始されます。バックアップが商用化されると、データ圧縮、バックアップの安定性、バックアップの可用性が大幅に向上し、バックアップがさらに保障されます。ユーザーはバックアップの保持期間や頻度を短縮させるなどで、バックアップの支出を削減できます。</td>
<td>2019-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/32344" target="_blank">バックアップスペースの課金方法</a></td>
</tr>
</tbody></table>

## 2019年11月
<table>
<thead>
<tr>
<th width=20%>更新</th>
<th width=50%>説明</th>
<th width=10%>発表時間</th>
<th width=20%>関連ドキュメント</th>
</tr>
</thead>
<tbody><tr>
<td>イベントアラームをサポートします</td>
<td>OOM、マスター/スレーブの切り替え、読み取り専用インスタンスの削除、サーバー障害によるインスタンスのマイグレーションなどのイベントをサブスクライブすることで、インスタンスの実行状態をいち早く把握できます。</td>
<td>2019-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8457" target="_blank">アラーム機能</a></td>
</tr>
</tbody></table>

## 2019年09月

<table>
<thead>
<tr>
<th width=20%>更新</th>
<th width=50%>説明</th>
<th width=10%>発表時間</th>
<th width=20%>関連ドキュメント</th>
</tr>
</thead>
<tbody><tr>
<td>データベースバックアップページのリリース</td>
<td>リリースされたTencentDB for MySQLバックアップページは、概要とバックアップリストの2つのコンテンツに分かれています。概要ページではバックアップスペースの詳細と使用動向を簡単に確認でき、バックアップリストではデータバックアップリストとログバックアップリストを明確に理解できます。</td>
<td>2019-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/33131" target="_blank">バックアップスペースの確認</a></td>
</tr>
</tbody></table>

## 2019年05月

<table>
<thead>
<tr>
<th width=20%>更新</th>
<th width=50%>説明</th>
<th width=10%>発表時間</th>
<th width=20%>関連ドキュメント</th>
</tr>
</thead>
<tbody><tr>
<td>自動バックアップのバックアップタイプはすべて物理バックアップにアップグレードしました</td>
<td>TencentDB for MySQLは現在、物理バックアップのみをサポートします。既存の自動バックアップが論理バックアップであるインスタンスは、物理バックアップに自動的に切り替えられます。論理バックアップが必要な場合は、TencentDB for MySQLコンソールの手動バックアップ機能を使用するか、API呼び出しによって論理バックアップを生成できます。</td>
<td>2019-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/32340" target="_blank">バックアップ方式</a></td>
</tr>
<tr>
<td>「南京1区」サービス提供開始しました</td>
<td>TencentDB for MySQLが南京1区で利用可能になりました。MySQLは現在、華東地区で上海と南京の2地域に設置されています。</td>
<td>2019-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8458" target="_blank">リージョンとアベイラビリティーゾーン</a></td>
</tr>
</tbody></table>

## 2019年03月

<div class="doc-table-wrap"><table>
<thead>
<tr>
<th width=20%>更新</th>
<th width=50%>説明</th>
<th width=10%>発表時間</th>
<th width=20%>関連ドキュメント</th>
</tr>
</thead>
<tbody><tr>
<td>VPC間での切り替えをサポートします</td>
<td>VPC AからVPC Bへの切り替え、すなわち、単一のTencentDBインスタンスのVPC AからVPC Bへの切り替えをサポートします。</td>
<td>2019-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31915" target="_blank">ネットワーク切り替え</a></td>
</tr>
</tbody></table></div>

## 2019年02月

<table>
<thead>
<tr>
<th width=20%>更新</th>
<th width=50%>説明</th>
<th width=10%>発表時間</th>
<th width=20%>関連ドキュメント</th>
</tr>
</thead>
<tbody><tr>
<td>クイック接続チェック</td>
<td>コンソールにはクイック接続チェックツールが用意されており、パブリックネットワーク・プライベートネットワークの接続問題を迅速に特定し、適切なソリューションを提供することができます。</td>
<td>2019-02</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31927" target="_blank">クイック接続チェックツール</a></td>
</tr>
</tbody></table>

## 2018年06月

<table>
<thead>
<tr>
<th width=20%>更新</th>
<th width=50%>説明</th>
<th width=10%>発表時間</th>
<th width=20%>関連ドキュメント</th>
</tr>
</thead>
<tbody><tr>
<td>Basic Editionインスタンスの購入をサポートします</td>
<td>Basic Editionは単一ノードを使用してデプロイされ、コンピューティングとストレージは分離されています。コンピューティングノードに障害が発生した場合、ノードを交換することで迅速な復元を実現できます。Basic Editionの基盤となるストレージメディアは、90%のI/Oケースに適した高性能ディスクを使用しており、高品質かつ低価格、優れて安定したパフォーマンスを実現しています。</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">データベースアーキテクチャ</a></td>
</tr>
<tr>
<td>ネットワーク切り替えをサポートします</td>
<td>クラシックネットワークからVPCへの切り替え、および同じVPC内のサブネット間の切り替えをサポートします。</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31915" target="_blank">ネットワーク切り替え</a></td>
</tr>
<tr>
<td>セルフ接続検出をサポートします</td>
<td>データベースが正常に接続されているかをテストします。</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31927" target="_blank">クイック接続チェックツール</a></td>
</tr>
<tr>
<td>ダウングレードと返金をサポートします</td>
<td>データベース構成をダウングレードし、残りの費用を返金することができます。</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/32345" target="_blank">インスタンス調整の料金の説明</a></td>
</tr>
<tr>
<td>MySQL 5.7のデータマイグレーションをサポートします</td>
<td>DTSデータマイグレーションはMySQL 5.7をサポートします。</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/34103" target="_blank">MySQLデータのオンラインインポート</a></td>
</tr>
<tr>
<td>製品名の変更</td>
<td>CDB for MySQLからTencentDB for MySQLに名称を変更します。</td>
<td>2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236" target="_blank">TencentDB for MySQL </a></td>
</tr>
</tbody></table>

## 2017年08月

<table>
<thead>
<tr>
<th width=20%>更新</th>
<th width=50%>説明</th>
<th width=10%>発表時間</th>
<th width=20%>関連ドキュメント</th>
</tr>
</thead>
<tbody><tr>
<td>読み取り専用インスタンスはエラスティック仕様をサポートします</td>
<td>マスターインスタンスと同じ仕様にする必要がありません。</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/7270" target="_blank">読み取り専用インスタンス</a></td>
</tr>
<tr>
<td>1minの監視時間粒度をサポートします</td>
<td>1minの時間粒度でデータベースを監視できます。</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8455" target="_blank">監視機能</a></td>
</tr>
<tr>
<td>物理バックアップをサポートします</td>
<td>物理バックアップでデータを保存できます。</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/32340" target="_blank">バックアップ方式</a></td>
</tr>
<tr>
<td>手動バックアップをサポートします</td>
<td>バックアップ時間と保持期間を設定でき、最大732日のバックアップをサポートします。</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/32340" target="_blank">バックアップ方式</a></td>
</tr>
<tr>
<td>セキュリティグループをサポートします</td>
<td>セキュリティグループはステートフルなパケットフィルタリング機能を持つ仮想ファイアウォールであり、1台または複数台のTencentDBインスタンスのネットワークアクセスコントロールを設定するために使用され、Tencent Cloudによって提供される重要なネットワーク安全分離手段です。</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/14470" target="_blank">TencentDBセキュリティグループ</a></td>
</tr>
<tr>
<td>データサブスクリプションをサポートします</td>
<td>DTSを使用すると、ユーザーがTencentDBの増分アップデートデータをリアルタイムで取得でき、自社のサービスニーズに合わせて増分データを使用できます。</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/8774" target="_blank">データサブスクリプション</a></td>
</tr>
<tr>
<td>TencentDBインスタンス間のデータマイグレーションをサポートします</td>
<td>DTSデータマイグレーションが様々なネットワーク環境に対応します</td>
<td>2017-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/571/34103" target="_blank">MySQLデータのオンラインインポート</a></td>
</tr>
</tbody></table>

## 2017年06月

<table>
<thead>
<tr>
<th width=20%>更新</th>
<th width=50%>説明</th>
<th width=10%>発表時間</th>
<th width=20%>関連ドキュメント</th>
</tr>
</thead>
<tbody><tr>
<td>MySQL 5.7をサポートします</td>
<td>MySQL 5.6カーネルに加えて、MySQL 5.7（Perconaサーバー）が新しく追加されました。MySQL 5.7のサポート機能に加えて、水平スケーリング、読み取り/書き込み分離などのネイティブ機能も継承されています。</td>
<td>2017-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31896" target="_blank">データベースバージョン</a></td>
</tr>
</tbody></table>

## 2016年03月

<table>
<thead>
<tr>
<th width=20%>更新</th>
<th width=50%>説明</th>
<th width=10%>発表時間</th>
<th width=20%>関連ドキュメント</th>
</tr>
</thead>
<tbody><tr>
<td>読み取り専用インスタンス機能のリリース</td>
<td>TencentDB for MySQLは、ユーザーによる1つまたは複数の読み取り専用インスタンスの作成をサポートし、また、ユーザーによる読み取り/書き込み分離と1つのマスターと複数のスレーブのユースケースをサポートすることで、データベースの読み取り負荷能力を明らかに向上させることができます。</td>
<td>2016-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/7270" target="_blank">読み取り専用インスタンス</a></td>
</tr>
<tr>
<td>従量課金インスタンスをサポートします</td>
<td>データベースサービスは時間単位で提供されます。</td>
<td>2016-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/18335" target="_blank">課金概要</a></td>
</tr>
</tbody></table>
