## 데이터 내보내기
TDSQL for MySQL은 mysqldump로 데이터 내보내기를 지원합니다. 내보내기 전에 [TDSQL for MySQL 콘솔](https://console.cloud.tencent.com/dcdb)에서 net_write_timeout 매개변수를 설정해야 합니다(`set global net_write_timeout=28800`). 명령 라인 유틸리티는 TDSQL for MySQL의 승인을 받지 않았으므로 콘솔에서만 매개변수를 설정할 수 있습니다.
```
mysqldump --compact --single-transaction --no-create-info -c db_name table_name  -utest -h10.xx.xx.34 -P3336  -ptest123
```

>?db 및 table 매개변수는 실제 상황에 따라 지정해야 합니다. 내보낸 데이터를 MySQL 환경용 TDSQL의 다른 세트로 가져오려면 -c 옵션을 추가해야 합니다.


## 데이터 가져오기
TDSQL for MySQL은 load data outfile에서 지정한 데이터를 가져오기 위한 전문 툴을 제공합니다. 이 툴은 shardkey 라우팅 규칙에 따라 소스 파일을 여러 파일로 분할하고 각 파일을 해당 백엔드 데이터베이스로 전달합니다.

[툴 다운로드](https://tdsqlfilebackup-1252014656.cos.ap-chengdu.myqcloud.com/load_data.tar)

```
[tdengine@TENCENT64 ~/]$./load_data

format:./load_data mode0/mode1 proxy_host proxy_port user password db_table shardkey_index file field_terminate filed_enclosed

example:./load_data mode1 10.xx.xx.10 3336 test test123 shard.table  1 '/tmp/datafile'  ' ' ''
```

>!
>- 소스 파일은 줄 바꿈으로 '\n'을 사용해야 합니다.
>- mode0은 소스 파일이 샤딩되지만 가져오지는 않음을 의미하며 일반적으로 디버깅에 사용됩니다. 데이터를 가져오려면 mode1을 사용하십시오.
>- shardkey_index는 0부터 시작합니다. shardkey가 두 번째 필드인 경우 shardkey_index는 1이어야 합니다.

