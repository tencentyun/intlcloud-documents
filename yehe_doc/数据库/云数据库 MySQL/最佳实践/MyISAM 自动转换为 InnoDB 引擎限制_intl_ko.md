본 문서에서는 MyISAM 엔진을 InnoDB 엔진으로 자동 전환한 후 테이블 생성 시 발생하는 오류 솔루션을 소개합니다.

### 상황
TencentDB for MySQL에서는 기본적으로 InnoDB 스토리지 엔진을 지원하며, MySQL 5.6 및 그 이상의 버전에서는 MyISAM 엔진과 Memory 엔진을 지원하지 않습니다. 자세한 내용은 [데이터베이스 스토리지 엔진](https://intl.cloud.tencent.com/document/product/236/9535)을 참조하십시오.
데이터베이스를 TencentDB for MySQL 5.6 및 그 이상의 버전으로 마이그레이션 혹은 업그레이드할 경우, 시스템이 자동으로 MyISAM 엔진을 InnoDB 엔진으로 변환합니다.

MyISAM 엔진은 Auto Increment 포함 Compound Primary Key를 지원하지만 InnoDB 엔진은 지원하지 않습니다. 따라서 MyISAM 엔진을 InnoDB 엔진으로 전환하면 테이블 생성 시 오류가 발생할 수 있습니다. 오류 정보는 다음과 같습니다.`ERROR 1075 (42000):Incorrect table definition;there can be only one auto column and it must be defined as a key`.

Auto Increment를 위한 인덱스를 생성하는 방식으로 InnoDB 엔진의 Auto Increment 포함 Compound Primary Key 구문을 구현하시길 권장합니다.

## InnoDB 엔진에서 Auto Increment 포함 Compound Primary Key의 수정 방안
1. 기존 테이블 생성 오류 SQL 명령:
```
 create table t_complexkey
 ( 
 id int(8) AUTO_INCREMENT, 
 name varchar(19), 
 value varchar(10), 
 primary key (name,id),
 ) ENGINE=MyISAM DEFAULT CHARSET=utf8;
```
다음 이미지와 같이 오류 생성:
![](https://main.qcloudimg.com/raw/4ff00d33bc2d14b0a229dae99ab40b5d.png)
2. 인덱스 생성 수정 후의 SQL 명령:
```
 create table t_complexkey
 ( 
 id int(8) AUTO_INCREMENT, 
 name varchar(19), 
 value varchar(10), 
 primary key (name,id),
 key key_id (id)  ## 자동 증가열에 대해 인덱스 생성
 ) ENGINE=MyISAM DEFAULT CHARSET=utf8;
```
다음 이미지와 같이 생성 성공:
![](https://main.qcloudimg.com/raw/34925406c1d5c36a7357f1735342907b.png)
3. 조회 생성 후의 테이블 구조:
```
show create table t_complexkey;
```
![](https://main.qcloudimg.com/raw/8509780314f54ecebe54283c579b49f8.png)

