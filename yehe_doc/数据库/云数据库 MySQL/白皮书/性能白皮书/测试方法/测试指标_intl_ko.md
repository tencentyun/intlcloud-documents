본 문에서는 TencentDB for MySQL 성능 테스트의 테스트 지표를 소개합니다.

## 테스트 지표
- **초당 실행된 트랜잭션 수 TPS(Transactions Per Second)**
데이터베이스의 초당 트랜잭션 수는 COMMIT 성공 횟수를 기준으로 합니다.
- **초당 실행된 요청 수 QPS(Queries Per Second)**
INSERT, SELECT, UPDATE, DETELE, COMMIT 등을 포함하여 데이터베이스에서 초당 실행된 SQL 수입니다.
- **모든 event의 평균 소요 시간 avg_lat(Average Latency)**

