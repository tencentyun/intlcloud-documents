### 테스트 툴
데이터베이스의 표준 성능 테스트 툴은 sysbench 0.5입니다.

툴 변경 설명:
sysbench가 자체 보유한 otlp 스크립트에 대해 수정을 진행하여 읽기, 쓰기의 비율을 1:1로 수정했으며, 테스트 명령어 매개변수인 oltp_point_selects와 oltp_index_updates를 실행하여 읽기 쓰기 비율을 제어할 수도 있습니다. 본 문서의 테스트 사례는 select 포인트 4개, update 포인트 1개를 사용하여 읽기 쓰기의 비율을 4:1로 유지합니다.

#### 툴 설치
본 문서의 테스트에서는 Sysbench 0.5 버전을 사용하며, 설치 방법은 아래와 같습니다.
```
git clone https://github.com/akopytov/sysbench.git
git checkout 0.5
yum -y install make automake libtool pkgconfig libaio-devel
yum -y install mariadb-devel
./autogen.sh
./configure
make -j
make install
```
>?위는 CVM(CentOS 시스템)에 대해 스트레스 테스트를 진행할 때의 설치 방법이며, 다른 운영 체제에 설치하려면 [Sysbench 공식 문서](https://github.com/akopytov/sysbench?spm=a2c4g.11186623.2.12.36061072oZL2qS)를 참조 바랍니다.

## 테스트 환경

|유형|설명|
|--|--|
|인스턴스 물리적 기기|고가용성 버전-단일 기기에 최대 488GB 메모리, 6TB 디스크 데이터베이스 지원|
|인스턴스 사양|현재 판매 중인 주요 사양(아래 문서 [테스트 사례](#cscs) 참조)|
|클라이언트 설정| 4코어 8GB 메모리|
|클라이언트 수량|1 - 6개(사양 업그레이드 시, 클라이언트 수량도 확장해야 합니다)|
|네트워크 환경|10기가 네트워크 데이터 센터, 네트워크 딜레이 < 0.05ms|
|환경 부하|mysql 설치 시 기기의 부하 > 70%(비단독 인스턴스에 대해)|

- 클라이언트 사양 설명: 단일 클라이언트에서 데이터베이스 인스턴스의 성능에 대한 스트레스 테스트를 진행하기 위해서는 비교적 높은 사양의 클라이언트 기기 사용이 권장됩니다. 클라이언트의 사양이 낮으면 여러 개의 클라이언트를 사용한 스트레스 테스트를 진행해 인스턴스 데이터의 총합을 구하시기를 권장합니다.
- 네트워크 딜레이 설명: 테스트 환경에서는 클라이언트 기기와 데이터베이스 인스턴스가 같은 가용존에 있어야 하며, 테스트 결과는 네트워크의 영향을 받지 않습니다.

## 테스트 방법
### 1. DB 테이블 구조 테스트
```
CREATE TABLE `sbtest1` ( 
`id` int(10) unsigned NOT NULL AUTO_INCREMENT, 
`k` int(10) unsigned NOT NULL DEFAULT '0', 
`c` char(120) NOT NULL DEFAULT '', 
`pad` char(60) NOT NULL DEFAULT '',
 PRIMARY KEY (`id`), KEY `k_1` (`k`) 
) ENGINE=InnoDB DEFAULT CHARSET=utf8；
```

### 2. 데이터 행 형식 테스트
```
id: 1
k: 20106885
c: 08566691963-88624912351-16662227201-46648573979-64646226163-77505759394-75470094713-41097360717-15161106334-50535565977
pad: 63188288836-92351140030-06390587585-66802097351-4928296184
```


### 3. 데이터 준비
```
sysbench --mysql-host=xxxx --mysql-port=xxxx --mysql-user=xxx --mysql-password=xxx --mysql-db=test --mysql-table-engine=innodb --test=tests/db/oltp.lua --oltp_tables_count=20 --oltp-table-size=10000000  --rand-init=on prepare
```

데이터 준비 매개변수 설명:
- `--test=tests/db/oltp.lua`, tests/db/oltp.lua 스크립트를 호출해 oltp 모드 테스트를 진행함을 의미합니다.
- `--oltp_tables_count=20`, 테스트에 사용되는 테이블 수량이 20개라는 의미입니다.
- `--oltp-table-size=10000000`, 각 테스트 테이블에 입력된 데이터 행 수가 1000만 행이라는 의미입니다.
- `--rand-init=on`, 각 테스트 테이블 모두 랜덤 데이터로 입력되었음을 의미합니다.
   

### 4. 성능 스트레스 테스트 명령어
```
sysbench --mysql-host=xxxx --mysql-port=xxx --mysql-user=xxx --mysql-password=xxx --mysql-db=test --test=/root/sysbench_for_z3/sysbench/tests/db/oltp.lua --oltp_tables_count=xx --oltp-table-size=xxxx --num-threads=xxx --oltp-read-only=off --rand-type=special --max-time=600 --max-requests=0 --percentile=99 --oltp-point-selects=4 run
```

성능 스트레스 테스트 매개변수 설명:
- `--test=/root/sysbench_for_z3/sysbench/tests/db/oltp.lua`, /root/sysbench_for_z3/sysbench/tests/db/oltp.lua 스크립트를 호출해 oltp 모드의 테스트를 진행함을 의미합니다.
- `--oltp_tables_count=20`, 이번 테스트에 사용되는 테이블 수량이 20개라는 의미입니다.
- `--oltp-table-size=10000000`, 이번 테스트에 사용되는 테이블 행 수가 모두 1000만 행이라는 의미입니다.
- `--num-threads=128`, 이번 테스트의 클라이언트 동시 연결 수가 128임을 의미합니다.
- `--oltp-read-only=off`, off는 테스트 시 읽기 전용 테스트 모델을 종료하고 읽기 및 쓰기 하이브리드 모델을 사용한다는 의미입니다.
- `--rand-type=special`, 랜덤 모델이 특정 유형임을 의미합니다.
- `--max-time=1800`, 이번 테스트의 실행 시간을 의미합니다.
- `--max-requests=0`, 0은 총 요청 수가 제한되지 않으며, max-time에 따라 테스트함을 의미합니다.
- `--percentile=99`, 샘플링 레이트를 의미하며, 기본값은 95%입니다. 99는 1%의 긴 요청을 버리면 나머지 99% 안에서 최댓값을 취한다는 의미입니다.
- `--oltp-point-selects=4`, oltp 스크립트 중 sql 테스트 명령어로, select 작업 횟수가 4라는 의미이며 기본값은 1입니다.

### 5. 시나리오 모델
본 문서에서는 기본적으로 시나리오 스크립트 our_oltp.lua를 사용하며, 이를 4개의 select 포인트 쿼리와 1개의 update(인덱스 열)로 수정하여 읽기와 쓰기의 비율이 4:1로 적용됩니다.
최대 설정 유형에 대해서는 데이터 시나리오에 매개변수 최적화 모델을 추가했으며, 테스트 결과는 아래의 [테스트 결과](#document_test_result)를 참조 바랍니다.

<span id="cscs"></span>
## 매개변수 테스트

|인스턴스 사양|스토리지 용량|테이블 수량|테이블 행 수|데이터 세트 크기|동시 접속 수|실행 시간(분)|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1코어 1GB|200GB| 4|2000만|19GB|128|30|
|1코어 2GB|200GB| 4 | 4000만| 38GB|128|30|
|2코어 4GB|200GB|8|4000만|76GB|128|30|
|4코어 8GB|200GB|15|4000만|142GB|128|30|
|4코어 16GB|400GB|25|4000만|238GB|128|30|
|8코어 32GB|700GB|25|4000만|238GB|128|30|
|16코어 64GB|1TB|40|4000만|378GB|256|30|
|16코어 96GB|1.5TB|40|4000만|378GB|128|30|
|16코어 128GB|2TB|40|4000만|378GB|128|30|
|24코어 244GB|3TB|60|4000만|567GB|128|30|
|48코어 488GB|6TB|60|4000만|567GB|128|30|
|48코어 488GB(최적화)|6TB|60|1000만|140GB|128|30|

<span id="document_test_result"></span>
## 테스트 결과

|인스턴스 사양|스토리지 용량|데이터 세트|클라이언트 수|단일 클라이언트 동시 접속 수|QPS|TPS|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1코어 1GB|200GB|19GB|1|128|1757|97|
|1코어 2GB|200GB|38GB|1|128|3016|167|
|2코어 4GB|200GB|76GB|1|128|4082|816|
|4코어 8GB|200GB|142GB|1|128|6551|1310|
|4코어 16GB|400GB|238GB|1|128|11098|2219|
|8코어 32GB|700GB|238GB|2|128|20484|3768|
|16코어 64GB|1TB|378GB|2|128|36395|7279|
|16코어 96GB|1.5TB|378GB|3|128|56464|11292|
|16코어 128GB|2TB|378GB|3|128|81752|16350|
|24코어 244GB|3TB|567GB|4|128|98528|19705|
|48코어 488GB|6TB|567GB|6|128|142246|28449|
|48코어 488GB(최적화)|6TB|140GB|6|128|245509|46304|
