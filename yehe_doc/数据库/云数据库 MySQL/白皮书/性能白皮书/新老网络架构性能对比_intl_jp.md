TencentDB for MySQLはデータベースインスタンスのネットワークアーキテクチャをアップグレードしました。新しいバージョンのネットワークアーキテクチャは、より良いパフォーマンスと遅延時間の短縮を可能にし、より強力なネットワークサービスを提供します。この文書では、新旧のネットワークアーキテクチャに関するパフォーマンステストの比較について説明します。
>?
>- **2022年11月9日以降、新しく購入したインスタンスは、まったく新しいネットワークアーキテクチャを採用します**。遅延時間が短縮され、パフォーマンスが向上します。
>- **2022年12月31日に、既存のデータベースインスタンスのネットワークアーキテクチャの切り替えが完了します**。切り替え中、ユーザーのアクセスに影響を及ぼすことはありません。
>- 単一ノードのクラウドディスクインスタンスは既に最適なネットワークアーキテクチャであり、インスタンスの詳細ページには新しいネットワークアーキテクチャであるかどうかが表示されません。
>- 基幹ネットワークでは、新しいネットワークアーキテクチャを使用できません。新しいアーキテクチャを使用する場合は、先に[Virtual Private Cloudに切り替え](https://intl.cloud.tencent.com/document/product/236/31915)てから、ネットワークアーキテクチャがアップグレードされるまでお待ちください。
>- ネットワークアーキテクチャのアップグレードの詳細については、[ネットワークアーキテクチャアップグレードのお知らせ](https://www.tencentcloud.com/document/product/236/51945)をご参照ください。

## テスト環境
- リージョン/アベイラビリティーゾーン：北京 - 北京六区。
- クライアント仕様：S5.2XLARGE16、8コア、16GB。
- クライアントオペレーティングシステム：TencentOS Server 3.2。
- ネットワーク：Cloud Virtual Machine (CVM)と MySQLインスタンスのネットワークタイプはいずれもプライベートネットワーク(VPC)であり、同一サブネットに所属します。
- ストレージ種類：ローカルSSDディスク
- テストインスタンスの仕様：汎用型、4コア、16GB。
- パラメータテンプレート：高性能テンプレート
- コピー方法：非同期レプリケーション。

## テストツール
基準テストツール「SysBench」でテストを行います。SysBenchは、プラットフォームをまたいだ、マルチスレッドのモジュール化をサポートしている基準テストツールであり、システムが高い負荷のデータベースを実行する場合の関連コアパラメータのパフォーマンスをテストするために使用されます。複雑なデータベース基準設定やデータベースのインストールをせずに、データベースシステムのパフォーマンスを迅速に把握することが可能です。耐圧テストでは、SysBenchバージョン1.0.20が使用されます。

## テストシナリオ
今回の耐圧テストは、書き込み専用シナリオ、読み取り専用シナリオ、読み取りと書き込みの混合シナリオという3つのシナリオで行われます。各シナリオでは、2～3000スレッドで耐圧テストが行われ、耐圧テストでのQPS値はパフォーマンス結果の指標となります。

## テスト方法
**ステップ1：データの準備**
下記のコマンドを実行します。
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX
--mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=10000000
--tables=10 --events=0 --time=300 --threads={2~3000} oltp_read_write prepare
```

**ステップ2：workloadの実行**
書き込み専用、読み取り専用、および読み取りと書き込みの混合シナリオからそれぞれworkloadを実行します。適切に設定ように注意してください。
- OLTP書き込み専用シナリオ
下記のコマンドを実行します：
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX
--mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=10000000
tables=10 --events=0 --time=300 --threads={2~3000} --=95---=1
run
```
- OLTP読み取り専用シナリオ
下記のコマンドを実行します：
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX
--mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=10000000
--tables=10 --events=0 --time=300 --threads={2~3000} --percentile=95 --skip-trx=1 --report-interval=1
oltp_read_only
run
```
- OLTP読み取りと書き込みの混合シナリオ
下記のコマンドを実行します：
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX
--mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=10000000
--tables=10 --events=0 --time=300  --threads={2~3000} --percentile=95 --report-interval=1 oltp_read_write
run
```

**ステップ3：データのクリーンアップ**
実行テストの完了後、データのクリーンアップを行い、下記のコマンドを実行します：
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX
--mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600   --threads=XXX --percentile=95  oltp_read_write cleanup
```

## テスト指標
テスト指標は、1秒あたりのリクエストの実行数QPS（Queries Per Second）です。

## テスト結果
**書き込み専用シナリオのテスト結果**
書き込み専用シナリオでは、TencentDB for MySQLの新しいアーキテクチャのパフォーマンスはスレッド数とともに向上し、常に元のアーキテクチャのパフォーマンスより高くなります。スレッド数が256の場合、最高のQPSに達します。スレッド数が512の場合、新しいアーキテクチャのQPS値は元のアーキテクチャのQPSより20%高くなります。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/EXhD388_PRELIM__%E4%BA%91%E6%95%B0%E6%8D%AE%E5%BA%93%20MySQL_%E6%B5%81%E7%A8%8B%E5%9B%BE_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-1.png)

**読み取り専用シナリオのテスト結果**
読み取り専用シナリオでは、スレッド数が少ない場合、TencentDB for MySQLの新しいアーキテクチャのQPSが大幅に増加し、直線的に上昇する傾向があります。スレッド数が64に達すると、QPSの上昇が穏やかになります。全体的なパフォーマンスは、常に元のアーキテクチャより高く、そしてスレッド数が16の場合に元のアーキテクチャのQPSより22%高くなります。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/EXhD388_PRELIM__%E4%BA%91%E6%95%B0%E6%8D%AE%E5%BA%93%20MySQL_%E6%B5%81%E7%A8%8B%E5%9B%BE_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-1.png)

**読み取りと書き込みの混合シナリオのテスト結果**
読み取りと書き込みの混合シナリオでは、スレッド数が少ない場合、TencentDB for MySQLの新しいアーキテクチャのQPSが大幅に増加します。スレッド数が512に達すると、全体的なQPSが穏やかに低下します。このとき、新しいアーキテクチャのQPSは最大値に達し、元のアーキテクチャのQPSより18%高くなります。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/p62d341_PRELIM__%E4%BA%91%E6%95%B0%E6%8D%AE%E5%BA%93%20MySQL_%E6%B5%81%E7%A8%8B%E5%9B%BE_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-3.png)

## 結論
>?上記のパフォーマンステスト結果はあくまでも参考です。
>
上記の3つのシナリオのテストと比較によると、新しいバージョンのTencentDB for MySQLネットワークアーキテクチャのパフォーマンスは、元のアーキテクチャのパフォーマンスよりもはるかに高く、3つのシナリオでは、スレッド数は2～3000であり、耐圧テストのQPS値は平均で20%以上上昇し、新しいバージョンのネットワークアーキテクチャのパフォーマンスが大幅に向上しました。
