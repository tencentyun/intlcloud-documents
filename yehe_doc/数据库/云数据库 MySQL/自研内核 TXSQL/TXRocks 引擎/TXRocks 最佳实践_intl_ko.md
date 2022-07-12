이 문서는 TXRocks 엔진을 사용하여 데이터베이스에 방대한 양의 데이터 가져오기를 가속화하는 방법을 설명합니다.

## 배경
- **시나리오**: TXRocks 엔진을 사용하여 데이터베이스로 방대한 양의 데이터 가져오기를 가속화해야 합니다.
- **영향**: ‘Rows inserted during bulk load must not overlap existing rows’ 오류는 대량의 데이터를 가져올 때 보고될 수 있습니다.

## 옵션 1
1. 보조 인덱스를 삭제하고 기본 키 인덱스만 유지합니다.
2. 사양 및 데이터 볼륨에 따라 메모리 매개변수를 조정합니다.
>?사양 및 데이터 볼륨에 따라 rocksdb_merge_buf_size 및 rocksdb_merge_combine_read_size 매개변수의 값을 적절하게 늘립니다.
>
 - rocksdb_merge_buf_size는 인덱스 생성 시 k-way merge에서 각 way의 데이터 볼륨을 나타냅니다. rocksdb_merge_combine_read_size는 k-way merge에 사용된 총 메모리를 나타냅니다.
 - rocksdb_block_cache_size는 rocksdb_block_cache의 크기를 나타냅니다. k-way merge 중에는 일시적으로 값을 줄이는 것이 좋습니다.
3. bulk load를 사용하여 데이터를 가져옵니다.
```
SET session rocksdb_bulk_load_allow_unsorted=1;
SET session rocksdb_bulk_load=1;
...
데이터 가져오기
...
SET session rocksdb_bulk_load=0;
SET session rocksdb_bulk_load_allow_unsorted=0;
```
>?가져온 데이터가 정렬되면 rocksdb_bulk_load_allow_unsorted를 구성할 필요가 없습니다.
4. 모든 데이터를 가져온 후 보조 인덱스를 하나씩 다시 만듭니다.
>!
>- 보조 인덱스 생성에는 k-way merge가 포함됩니다. rocksdb_merge_buf_size는 각 방법의 데이터 볼륨을 나타내고, rocksdb_merge_combine_read_size' k-way merge에 사용된 총 메모리를 나타냅니다.
>- 예를 들어 OOM을 방지하려면 rocksdb_merge_buf_size를 64MB 이상으로 설정하고 rocksdb_merge_combine_read_size를 1GB 이상으로 설정하는 것이 좋습니다. 모든 데이터를 가져온 후에는 매개변수를 원래 값으로 수정해야 합니다.
>- 각각의 보조 인덱스를 생성할 때 많은 메모리를 사용하므로 동시에 많은 양을 생성하지 않는 것이 좋습니다.

## 옵션 2
가져오기 성능을 향상시키기 위해 데이터 가져오기 중에 unique_check를 비활성화할 수 있습니다.
```
SET unique_checks=OFF;
...
데이터 가져오기
...
SET unique_checks=ON;
```
>!작업이 완료되면 unique_checks를 다시 ON으로 설정해야 합니다. 그렇지 않으면 후속 일반 트랜잭션 쓰기에서 insert 작업의 고유성이 확인되지 않습니다.
