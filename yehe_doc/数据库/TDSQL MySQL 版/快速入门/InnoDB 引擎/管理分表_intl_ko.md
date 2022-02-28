본문은 TDSQL for MySQL의 몇 가지 간단한 데이터베이스 작업을 설명하기 위해 샤딩된 테이블을 예로 들어 설명합니다.

## 테이블 생성
- 분할된 테이블, 분할되지 않은 테이블 및 브로드캐스트 테이블 간의 차이점에 대한 자세한 내용은 [개요](https://intl.cloud.tencent.com/document/product/1042/38142)를 참고하십시오.
- 샤드키(shardkey)에 대한 제한 사항에 대한 자세한 내용은 [테이블 생성](https://intl.cloud.tencent.com/document/product/1042/38506)을 참고하십시오.
- 샤딩된 테이블을 생성하려면 샤드키(shardkey)를 지정해야 합니다. 샘플 코드는 다음과 같습니다.
```
mysql> create table test1(id int primary key,name varchar(20),addr varchar(20))shardkey=id;
Query OK,0 rows affected(0.15 sec)
```
		
## 데이터 삽입
>!샤드키는 insert 문에 포함되어야 하며 그렇지 않으면 작업이 거부됩니다.

방금 만든 테이블에 데이터를 삽입합니다. 샘플 코드는 다음과 같습니다.
```
mysql> insert into test1(id,name) VALUES(1,'test');
Query OK,1 rows affected(0.08 sec)
mysql> insert into test3(name,addr) values('example','shenzhen');
ERROR 7013 (HY000): Proxy ERROR:get_shardkeys return error
```

## 데이터 쿼리
>!데이터를 쿼리할 때 요청이 분산 경로에 따라 해당 샤드로 자동 라우팅되어 최고의 효율성을 달성할 수 있도록 명령문에 샤드키를 포함하는 것이 좋습니다. 그렇지 않으면 TDSQL이 자동으로 전체 테이블을 스캔한 다음 게이트웨이에서 결과를 집계하므로 효율성이 저하됩니다.

데이터 쿼리를 위한 샘플 코드는 다음과 같습니다.
```
mysql> select id from test1 where id=1;
```

## 데이터 삭제
>!delete 문에는 where 절이 포함되어야 하며 where 절에 샤드키를 포함하는 것이 좋습니다.

데이터 삭제를 위한 샘플 코드는 다음과 같습니다.
```
mysql> delete from test1 where id=1;
Query OK, 1 row affected (0.02 sec)
```
