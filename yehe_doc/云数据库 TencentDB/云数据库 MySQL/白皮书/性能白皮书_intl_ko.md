## 테스트 툴
데이터베이스의 표준 성능 테스트는 sysbench 0.5로 진행합니다.

툴 수정 설명:
sysbench의 otlp 스크립트에서 읽기/쓰기의 비율을 1:1로 수정하고, 테스트 명령어 매개변수인 oltp_point_selects와 oltp_index_updates를 실행하여 읽기/쓰기 비율을 제어합니다. 본 문서의 테스트 사례는 모두 select 포인트 4개와 update 포인트 1개를 사용하여 읽기/쓰기 비율을 4:1로 유지합니다.

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
>?위는 부하 테스트 CVM(CentOS 시스템)에 설치하는 방법입니다. 다른 운영 체제에 설치하려면 [Sysbench 공식 홈페이지 문서](https://github.com/akopytov/sysbench?spm=a2c4g.11186623.2.12.36061072oZL2qS)를 참조하십시오.

## 테스트 환경

|유형|설명|
|--|--|
|베어메탈 인스턴스|이중 노드-단일 기기에 최대 488GB 메모리, 6TB 디스크의 데이터베이스 지원|
|인스턴스 사양|판매 중인 주요 설정 사양(아래 [테스트 사례](#cscs) 문서 참조)|
|클라이언트 사양| 4코어 8GB 메모리|
|클라이언트 수량|1~6개(사양 업그레이드 시 클라이언트 수량도 늘려야 함)|
|네트워크 환경|10GB 네트워크 데이터 센터, 네트워크 딜레이 < 0.05ms|
|환경 부하|mysql 설치 시 기기의 부하 > 70%(비전용 인스턴스 대상)|

- 클라이언트 사양 설명: 비교적 높은 사양의 클라이언트 기기를 사용하여 단일 클라이언트도 데이터베이스 인스턴스의 성능 부하 테스트를 수행할 수 있습니다. 클라이언트의 사양이 낮은 경우, 인스턴스에 대해 여러 클라이언트로 동시에 부하 테스트를 수행하여 데이터의 합계를 구하는 것을 권장합니다.
- 네트워크 딜레이 설명: 테스트 환경은 클라이언트 기기와 데이터베이스 인스턴스가 동일한 가용존에 있도록 설정해야 합니다. 테스트 결과는 네트워크 환경의 영향을 받지 않습니다.

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

### 2. 데이터 행 포맷 테스트
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
- `--test=tests/db/oltp.lua`는 tests/db/oltp.lua 스크립트를 호출해 oltp 모드 테스트를 진행함을 의미합니다.
- `--oltp_tables_count=20`은 테스트에 사용되는 테이블 수량이 20개임을 의미합니다.
- `--oltp-table-size=10000000`은 각 테스트 테이블에 입력된 데이터 행 수가 1,000만 개임을 의미합니다.
- `--rand-init=on`은 각 테스트 테이블이 임의의 데이터로 입력되었음을 의미합니다.
  

### 4. 성능 부하 테스트 명령어
```
sysbench --mysql-host=xxxx --mysql-port=xxx --mysql-user=xxx --mysql-password=xxx --mysql-db=test --test=/root/sysbench_for_z3/sysbench/tests/db/oltp.lua --oltp_tables_count=xx --oltp-table-size=xxxx --num-threads=xxx --oltp-read-only=off --rand-type=special --max-time=600 --max-requests=0 --percentile=99 --oltp-point-selects=4 run
```

성능 부하 테스트 매개변수 설명:
- `--test=/root/sysbench_for_z3/sysbench/tests/db/oltp.lua`는 /root/sysbench_for_z3/sysbench/tests/db/oltp.lua 스크립트를 호출해 oltp 모드의 테스트를 진행함을 의미합니다.
- `--oltp_tables_count=20`은 이번 테스트에 사용되는 테이블 수량이 20개임을 의미합니다.
- `--oltp-table-size=10000000`은 이번 테스트에 사용되는 테이블 행 수가 1,000만 개임을 의미합니다.
- `--num-threads=128`은 이번 테스트의 클라이언트 동시 접속 수가 128개임을 의미합니다.
- `--oltp-read-only=off`에서 off 는 테스트 시 읽기 전용 테스트 모델을 비활성화하고 읽기/쓰기 혼합 모델을 사용한다는 의미입니다.
- `--rand-type=special`은 랜덤 모델이 특정 유형임을 의미합니다.
- `--max-time=1800`은 이번 테스트의 실행 시간을 의미합니다.
- `--max-requests=0`에서 0은 요청 수가 제한되어 있지 않으며, max-time에 따라 테스트함을 의미합니다.
- `--percentile=99`는 샘플링 레이트 설정을 의미하며 기본값은 95%입니다. 즉, 1%의 긴 요청 외에 나머지 99%에서 최댓값을 취한다는 뜻입니다.
- `--oltp-point-selects=4`는 oltp 스크립트의 sql 테스트 명령어로, select 작업 횟수가 4라는 의미입니다. 기본값은 1입니다.

### 5. 시나리오 모델
본 문서의 사례는 모두 sysbench의 lua 스크립트를 사용해 select 포인트 쿼리 4개와 update 1개(인덱스 열)로 수정하였고, 읽기/쓰기 비율은 4:1입니다.
최대 사양 유형에 대해서는 데이터 시나리오에 매개변수 최적화 모델을 추가했습니다. 테스트 결과는 아래 [테스트 결과](#document_test_result) 문서를 참조하십시오.


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
