분산 데이터베이스의 분산 구조는 사용자가 인지할 수 없기 때문에 일반적으로 미리 테이블 구조만 생성하면 되며 다음 단계에서 mysqldump, Navicat 또는 SQLyog와 같은 MySQL 클라이언트를 사용하여 데이터를 마이그레이션할 수 있습니다.

1단계: 가져오기 및 내보내기 환경 준비
2단계: 원본 테이블의 테이블 구조 및 데이터 내보내기
3단계: 테이블 생성을 위한 명령 수정 및 대상 테이블에 테이블 구조 생성
4단계: 데이터 가져오기

## 1단계: 가져오기 및 내보내기 환경 준비
데이터를 마이그레이션하기 전에 다음을 준비해야 합니다.
- CVM 인스턴스
	- 2개의 CPU 코어, 8GB 메모리 및 500GB 이상의 디스크 용량(데이터 볼륨에 따라 다름) 사양 권장
	- Linux
	- MySQL 클라이언트 설치
	- 데이터 볼륨이 작은 경우(< 10GB) 별도의 준비 없이 공용 네트워크(인터넷)를 통해 직접 획득 가능
- TDSQL for MySQL
	- 예상대로 용량을 선택하고 원본 데이터베이스 문자 집합, 테이블 이름 대소문자 구분 및 innodb_page_size 값에 따라 초기화 수행
	- 모든 전역 권한이 활성화된 계정 생성(권장)
	- 필요한 경우 공용 IP 주소 활성화

## 2단계: 원본 테이블의 테이블 구조 및 데이터 내보내기
### 시연 환경
- 조작된 데이터베이스: caccts
- 조작된 테이블: t_acct_water_0
- 원본 데이터베이스: 단일 인스턴스 MySQL
- 대상 데이터베이스: TDSQL for Percona, MariaDB

### 원본 데이터베이스에서 테이블 구조 내보내기
`mysqldump -u username -p password -d dbname tablename > tablename.sql`을 실행하여 테이블 구조를 내보냅니다.
```
//명령 인스턴스
mysqldump -utest -ptest1234 -d -S /data/4003/prod/mysql.scok caccts t_acct_water_0 > table.sql
```

### 원본 데이터베이스에서 테이블 데이터 내보내기
`mysqldump -c -u username -p password dbname tablename > tablename.sql`을 실행하여 테이블 데이터를 내보냅니다.
```
//명령 인스턴스
mysqldump -c -t -utest -ptest1234  -S /data/4003/prod/mysql.scok caccts t_acct_water_0 > data.sql
```
>!-c 매개변수가 추가된 mysqldump를 사용하여 데이터를 내보내야 합니다. 이렇게 해야만 내보낸 모든 데이터 행이 열 이름 필드를 가질 수 있기 때문입니다. 열 이름 필드가 없는 sql 데이터 행은 TDSQL for Percona 또는 MariaDB에서 거부됩니다. -t는 테이블 데이터만 내보내고 테이블 구조는 내보내지 않음을 나타냅니다.

### CVM 인스턴스의 디렉터리에 파일 업로드
파일을 업로드하기 전에 CVM 인스턴스의 공용 IP 주소를 활성화해야 합니다. 그런 다음 [SCP를 통해 Linux CVM에 파일 업로드](https://intl.cloud.tencent.com/document/product/213/2133)의 지침에 따라 최소 방금 내보낸 다음 파일을 업로드해야 합니다.
- 테이블 구조 sql: table.sql
- 데이터 sql: data.sql

## 3단계: 테이블 생성을 위한 명령 수정 및 대상 테이블에 테이블 구조 생성
내보낸 테이블 구조 파일 table.sql을 열고 다음과 같은 명령문을 통해 기본 키와 shardkey를 추가하고 tablenew.sql로 저장합니다.
```
CREATE TABLE（
열 이름1 데이터 유형,
열 이름2 데이터 유형,
열 이름3 데이터 유형,
....，
PRIMARY KEY(‘열 이름n’)）
ENGINE=INNODB DEFAULT CHARSET=xxxx 
shardkey=keyname
```
>!기본 키와 shardkey를 설정해야 합니다. 테이블 이름의 대소문자 구분에 주의하십시오. 중복된 댓글은 삭제하는 것이 좋습니다. 그렇지 않으면 테이블이 성공적으로 생성되지 않을 수 있습니다.
>
![](https://mc.qcloudimg.com/static/img/1cd921ececbacf81226a69a0eb5b919a/image.png)

## 4단계: 데이터 가져오기
### TDSQL for Percona, MariaDB 인스턴스 연결
CVM 인스턴스에서 `mysql -u username -p password -h IP -P port `를 실행하여 MySQL 서버에 로그인하고 `use dbname`을 실행하여 데이터베이스에 들어갑니다.
>!먼저 데이터베이스를 생성해야 할 수도 있습니다.

### 테이블 구조 가져오기
업로드된 파일을 사용하여 `source` 명령을 실행하여 데이터를 가져옵니다.
1. 먼저 테이블 구조 가져오기: `source /파일 경로/tablenew.sql;`
2. 그런 다음 데이터 가져오기: `source /파일 경로/data.sql;`
3. 가져오기 결과 확인: `select  count(*) from tablename;`

>!먼저 테이블 생성 문을 가져온 다음 데이터를 가져와야 합니다. mysql의 source 명령을 통해 .sql 파일을 직접 가져올 수도 있습니다.

## 기타 솔루션
일반적으로 데이터를 가져오기 전에 대상 테이블에 지정된 shardkey로 해당 테이블 구조를 생성했다면 원활하게 데이터를 가져올 수 있습니다.
