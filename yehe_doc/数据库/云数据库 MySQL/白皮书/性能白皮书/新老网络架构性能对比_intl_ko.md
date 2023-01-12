TencentDB for MySQL은 더 높은 성능과 더 짧은 대기 시간을 위해 데이터베이스 인스턴스의 네트워크 아키텍처를 업그레이드했습니다. 본문은 이전 버전과 새 버전의 성능 테스트에 대해 설명합니다.
>?
>- **2022년 11월 9일부터 새로 구입한 인스턴스에 새로운 네트워크 아키텍처가 적용**되어 더 짧은 지연 시간과 더 높은 성능을 제공합니다.
>- **2022년 12월 31일에 모든 기존 데이터베이스 인스턴스가 새로운 네트워크 아키텍처로 전환**되어 액세스에 영향을 미치지 않습니다.
>- 클라우드 디스크 버전의 단일 노드 인스턴스는 이미 최적의 네트워크 아키텍처에 있으므로 세부 정보 페이지에 네트워크 아키텍처가 새로운지 여부가 표시되지 않습니다.
>- 기존 네트워크에서는 새로운 네트워크 아키텍처를 사용할 수 없습니다. 이를 사용하려면 [네트워크 변경](https://intl.cloud.tencent.com/document/product/236/31915)의 안내에 따라 VPC로 전환하고 네트워크 아키텍처가 업그레이드될 때까지 기다립니다.
>- 자세한 내용은 [네트워크 아키텍처 업그레이드](https://www.tencentcloud.com/document/product/236/51945)를 참고하십시오.

## 테스트 환경
- 리전/AZ: 베이징 - 베이징 6존.
- 클라이언트 사양: S5.2XLARGE16(8개의 CPU 코어 및 16GB 메모리).
- 클라이언트 운영 체제: TencentOS Server 3.2.
- 네트워크: CVM과 TencentDB for MySQL 인스턴스는 모두 동일한 VPC 서브넷에 있습니다.
- 스토리지 유형: 로컬 SSD 디스크.
- 인스턴스 사양: 일반(4개의 CPU 코어 및 16GB 메모리).
- 매개변수 템플릿: 고성능 템플릿.
- 복제 방식: 비동기 복제.

## 테스트 툴
SysBench는 집약적인 부하에서 데이터베이스를 실행하는 시스템에 중요한 OS 매개변수를 평가하기 위한 모듈식, 크로스 플랫폼 및 멀티 스레드 벤치마크 툴입니다. 이 벤치마크 제품군의 아이디어는 복잡한 데이터베이스 벤치마크를 설정하지 않거나 데이터베이스를 전혀 설치하지 않고도 시스템 성능에 대한 인상을 신속하게 얻는 것입니다. 이 스트레스 테스트는 SysBench 1.0.20을 사용합니다.

## 테스트 시나리오
이 스트레스 테스트에는 쓰기 전용, 읽기 전용 및 읽기-쓰기 시나리오가 포함되며 각각 2 – 3000개의 스레드가 테스트됩니다. QPS는 성능 메트릭으로 사용됩니다.

## 테스트 방법
**1단계: 데이터 준비**
다음 명령을 실행합니다.
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX
--mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=10000000
--tables=10 --events=0 --time=300 --threads={2~3000} oltp_read_write prepare
```

**2단계: workload 실행**
쓰기 전용, 읽기 전용 및 읽기-쓰기 시나리오에서 workload를 실행합니다. 구성이 올바른지 확인하십시오.
- OLTP 쓰기 전용 시나리오
다음 명령을 실행합니다.
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX
--mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=10000000
--tables=10 --events=0 --time=300  --threads={2~3000} --percentile=95 --report-interval=1 oltp_write_only
run
```
- OLTP 읽기 전용 시나리오
다음 명령을 실행합니다.
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX
--mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=10000000
--tables=10 --events=0 --time=300 --threads={2~3000} --percentile=95 --skip-trx=1 --report-interval=1
oltp_read_only
run
```
- OLTP 읽기-쓰기 시나리오
다음 명령을 실행합니다.
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX
--mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=10000000
--tables=10 --events=0 --time=300  --threads={2~3000} --percentile=95 --report-interval=1 oltp_read_write
run
```

**3단계: 데이터 지우기**
테스트가 실행된 후 다음 명령을 실행하여 데이터를 지웁니다.
```
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX
--mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600   --threads=XXX --percentile=95  oltp_read_write cleanup
```

## 테스트 메트릭
테스트 메트릭은 초당 쿼리 수(QPS)입니다.

## 테스트 결과
**쓰기 전용 시나리오의 테스트 결과**
쓰기 전용 시나리오에서 TencentDB for MySQL의 새로운 아키텍처는 스레드 수가 증가함에 따라 항상 기존 아키텍처보다 성능이 우수합니다. QPS는 256개 스레드에서 정점에 도달하고 이전 아키텍처의 512개 스레드보다 20% 더 높습니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/EXhD388_PRELIM__%E4%BA%91%E6%95%B0%E6%8D%AE%E5%BA%93%20MySQL_%E6%B5%81%E7%A8%8B%E5%9B%BE_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-1.png)

**읽기 전용 시나리오의 테스트 결과**
읽기 전용 시나리오에서 TencentDB for MySQL의 새로운 아키텍처는 스레드 양이 작은 수에서 증가함에 따라 선형 QPS가 크게 증가하는 것을 확인했으며, QPS는 기존 아키텍처의 16 스레드보다 22% 더 높고 64 스레드 이상에서 꾸준히 증가하고 있습니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/EXhD388_PRELIM__%E4%BA%91%E6%95%B0%E6%8D%AE%E5%BA%93%20MySQL_%E6%B5%81%E7%A8%8B%E5%9B%BE_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-1.png)

**읽기-쓰기 시나리오의 테스트 결과**
읽기-쓰기 시나리오에서 TencentDB for MySQL의 새로운 아키텍처는 스레드 수가 적은 수에서 증가함에 따라 QPS가 크게 증가하는 것을 확인합니다. QPS는 512 스레드에서 정점(이전 아키텍처보다 18% 더 높음)에 도달한 후 꾸준히 감소합니다.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/EXhD388_PRELIM__%E4%BA%91%E6%95%B0%E6%8D%AE%E5%BA%93%20MySQL_%E6%B5%81%E7%A8%8B%E5%9B%BE_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-1.png)

## 결론
>? 상기 성능 테스트 결과는 참고용입니다.
>
상기 시나리오 테스트는 TencentDB for MySQL의 새로운 네트워크 아키텍처가 이전 아키텍처보다 훨씬 뛰어난 성능을 보인다는 것을 보여줍니다. 2~3000 스레드 범위에서 QPS가 평균 20% 이상 향상됩니다.
