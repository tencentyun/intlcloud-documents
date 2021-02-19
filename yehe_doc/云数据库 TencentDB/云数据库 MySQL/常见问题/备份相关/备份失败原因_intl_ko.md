### 단일 인스턴스의 테이블 수량 100만 초과
단일 인스턴스의 테이블 수량이 100만 개를 초과하면 백업에 실패할 수 있으며 데이터베이스 모니터링에도 영향을 미칠 수 있으므로 테이블 수량을 합리적인 수준으로 적용하시고, 단일 인스턴스 테이블 수량이 100만 개를 넘지 않도록 제어하시기 바랍니다.

### 기본 키 테이블이 없음으로 인한 대규모 트랜잭션
#### 원인 분석
인스턴스에 기본 키가 없는 테이블이 존재하고 binlog가 row 형식인 상황에서, sql 하나가 대량의 데이터를 업데이트/삭제했다면 슬레이브에서 다시 보기 시 대규모 트랜잭션이 발생할 수 있으며, 이에 따라 백업 스레드가 락을 획득하지 못해 백업에 실패할 수 있습니다.

#### 처리 방법
1. spl을 통해 인스턴스 중에서 기본 키가 없는 모든 테이블을 검사합니다.
```
select TABLE_SCHEMA,TABLE_NAME,TABLE_TYPE,ENGINE,TABLE_ROWS from information_schema.tables where (table_schema,table_name) not in (select table_schema,table_name from information_schema.columns where COLUMN_KEY='PRI') and table_schema not in ('sys','mysql','information_schema','performance_schema');
```
2. 기본 키가 없는 테이블에 기본 키를 추가합니다.
```
alter table table_name add primary key(`column_name`);
```
