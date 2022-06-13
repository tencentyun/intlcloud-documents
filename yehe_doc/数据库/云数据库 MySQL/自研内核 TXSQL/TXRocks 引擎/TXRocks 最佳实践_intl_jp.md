このドキュメントは、TXRocksを使用するベストプライクティスとして、大量のデータをインポートするときのインポート速度が向上することについてご説明します。

## 背景
- **シナリオ**：大量のデータをTXRocksエンジンのデータベースにインポートする場合、インポートを高速化する必要があります。
- **影響**：大量のデータをインポートすると、エラー`Rows inserted during bulk load must not overlap existing rows`が発生する可能性があります。

## 処理方法1
1. 最初にセカンダリインデックスを削除します（プライマリキーインデックスのみを保持します）。
2. 仕様とユーザーデータ量に基づいてメモリ関連パラメータを調整します。
>?仕様とデータ量に応じて、パラメータrocksdb_merge_buf_sizeとrocksdb_merge_combine_read_sizeを適切に大きくする必要があります。
>
 - rocksdb_merge_buf_sizeは、インデックス作成中にマルチパスマージのときの1パスあたりのデータ量を表し、rocksdb_merge_combine_read_sizeは、マルチパスマージのときの各ウェイで消費される合計メモリを表します。
 - rocksdb_block_cache_sizeは、rocksdb_block_cacheのサイズを表します。マルチパスマージのときには、一時的に小さくすることをお勧めします。
3. bulk load方式によるデータのインポート。
```
SET session rocksdb_bulk_load_allow_unsorted=1;
SET session rocksdb_bulk_load=1;
...
データのインポート
...
SET session rocksdb_bulk_load=0;
SET session rocksdb_bulk_load_allow_unsorted=0;
```
>?インポートしたデータが順序付けられている場合は、rocksdb_bulk_load_allow_unsortedを設定する必要はありません。
4. セカンダリインデックスの再構築には、すべてのデータのインポートが完了した後で、セカンダリインデックスを1つずつ再構築することができます。
>!
>- セカンダリインデックスの作成にはマルチパスマージが含まれます。rocksdb_merge_buf_sizeは1パスあたりのデータサイズ、rocksdb_merge_combine_read_sizeはマージ中にマルチパスマージに使用された合計メモリーサイズです。
>- 例えば、rocksdb_merge_buf_sizeを64MB以上、rocksdb_merge_combine_read_sizeを1GB以上に設定することをお勧めします。OOMを回避するには、データのインポートが完了したら必ず元のパラメータ値に戻します。
>- また、各セカンダリインデックス作成プロセスでは多くのメモリが消費されるため、同時に複数のセカンダリインデックスを作成することは推奨されません。

## 処理方法2
データのインポート中にunique_checkをオフにすると、インポートにおけるパフォーマンスが向上します。
```
set global unique_checks=OFF;
...
データのインポート
...
set global unique_checks=ON;
```
>!処理が完了したら、unique_checksを必ずONに戻してください。そうしないと、その後の通常のトランザクションによって書き込まれるinsert操作は一意性をチェックしません。
