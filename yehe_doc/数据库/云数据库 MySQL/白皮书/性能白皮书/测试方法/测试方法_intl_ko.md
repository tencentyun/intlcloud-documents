
본 문에서는 TencentDB for MySQL 성능 테스트 방법을 소개합니다.

## 작업 단계
SysBench를 사용하여 TencentDB for MySQL 인스턴스의 읽기/쓰기 하이브리드 성능을 테스트합니다.
1. 데이터를 준비합니다.
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600  oltp_read_write prepare
```
2. workload를 실행합니다.
```
sysbench --db-driver=mysql  --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600   --threads=XXX --percentile=95 --report-interval=1 oltp_read_write run
```
3. 데이터를 제거합니다.
```
sysbench --db-driver=mysql  --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600   --threads=XXX --percentile=95  oltp_read_write cleanup
```
