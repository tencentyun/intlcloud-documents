한 분산 데이터베이스에서 다른 데이터베이스로 데이터를 가져오기 위한 솔루션은 특별합니다. mysqldump는 가져오기 단계를 요약하기 위해 아래 예시로 사용됩니다.

## 1. mysqldump 설치(MariaDB용)
Linux CVM 인스턴스를 구입하고 `yum install mariadb-server`를 실행하여 mysqldump를 설치합니다.

## 2. 테이블 구조 내보내기
```
mysqldump --compact --single-transaction -d -uxxx -pxxx  -hxxx.xxx.xxx.xxx -Pxxxx  db_name table_name   >  schema.sql
```
>?필요에 따라 db_name 및 table_name 매개변수를 선택하십시오.

## 3. 데이터 내보내기
mysqldump를 사용하여 데이터 내보내기:
[TDSQL for MySQL 콘솔](https://console.cloud.tencent.com/dcdb)의 매개변수 설정에서 net_write_timeout 매개변수를 설정합니다. set global net_write_timeout=28800
```
mysqldump --compact --single-transaction --no-create-info -c -uxxx  -pxxx -hxxx.xxx.xxx.xxx -Pxxxx db_name table_name  > data.sql
```
>?db_name 및 table_name 매개변수는 필요에 따라 선택해야 합니다. 내보낸 데이터를 다른 TDSQL for MySQL 환경으로 가져오려면 -c 옵션을 추가해야 하며 -c와 db_name 사이에 공백이 있어야 합니다.
>
![](https://main.qcloudimg.com/raw/567f47f17939e809a7e0aa2f06627353.png)

## 4. 대상 인스턴스에 db 생성
```
mysql --default-character-set=utf8 -uxxx -pxxx -hxxx.xxx.xxx.xxx -Pxxxx -e "create database dbname;";
```
- --default-character-set=utf8: 대상 테이블을 기반으로 설정합니다.
- -uxxx: 권한 있는 계정(-u: 키워드).
- -pxxx: 암호(-p: 키워드).
- -hxxx.xxx.xxx.xxx -Pxxxx: 데이터베이스 인스턴스의 IP 및 포트입니다.
- dbname: db 이름.

## 5. 테이블 구조를 대상 인스턴스로 가져오기
```
mysql --default-character-set=utf8 -uxxx -pxxx -hxxx.xxx.xxx.xxx -Pxxxx dbname < schema.sql
```
- --default-character-set=utf8: 대상 테이블을 기반으로 설정합니다.
- -uxxx: 권한 있는 계정(-u: 키워드).
- -pxxx: 암호(-p: 키워드).
- -hxxx.xxx.xxx.xxx -Pxxxx: 데이터베이스 인스턴스의 IP 및 포트입니다.
- dbname: db 이름.

## 6. 대상 인스턴스로 테이블 데이터 가져오기
```
mysql --default-character-set=utf8 -uxxx -pxxx -hxxx.xxx.xxx.xxx -Pxxxx dbname < data.sql
```
>?원본 테이블에서 자동 증가 필드를 사용하고 가져오기 중 ‘Column 'xx' specified twice’ 오류가 발생하면 schema.sql을 처리해야 합니다.
   자동 증분 필드(cat schema.sql | tr "`" " " > schema_tr.sql )에서 역따옴표를 제거하고 drop database한 다음 처리된 schema_tr.sql을 사용하여 3 - 5단계를 반복합니다.
	 
![](https://main.qcloudimg.com/raw/b55fe0763f4e8fd1795fec478e9dc0c1.png)
