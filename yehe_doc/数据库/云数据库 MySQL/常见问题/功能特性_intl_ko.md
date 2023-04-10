### TencentDB for MySQL을 사용하려면 어떤 준비가 필요합니까?
TencentDB for MySQL 사용 전에는 다음 두 가지 문제를 고려해야 합니다.
- 데이터베이스가 귀하의 애플리케이션에 적합합니까? 예를 들어 데이터 볼륨이 작고, 액세스 트래픽이 많으며, key-value 스토리지가 있는 시나리오의 경우 메모리 수준 영구 스토리지 서비스 [TencentDB for Memcached](https://cloud.tencent.com/product/cmem)가 권장됩니다.
- 데이터베이스가 적절하게 설계되었습니까? 예를 들어 쿼리 핫스팟이 분명하거나 데이터 양이 많은 테이블은 여러 테이블로 분할하는 것을 고려해야 합니다.

### TencentDB for MySQL은 MySQL을 어떻게 관리하나요?
MySQL의 일상적인 유지 관리 및 조정은 TencentDB의 OPS 시스템에서 진행하므로 걱정할 필요가 없습니다.
MySQL에 예외가 발생한 경우 OPS 시스템은 즉시 문제를 식별하고 OPS 팀에 알릴 수 있습니다. 개발자는 어떤 변경 작업도 진행할 필요가 없습니다.

### TencentDB for MySQL은 물리적 머신을 기반으로 하나요?
예. TencentDB for MySQL은 물리적 머신 기반입니다.

### TencentDB for MySQL은 데이터베이스와 테이블을 분할하는 데 도움이 됩니까?
아니요. 데이터베이스와 테이블을 분할하는 표준은 특정 비즈니스 로직에 따라 달라지기 때문입니다.

### TencentDB for MySQL의 점유 용량과 사용 용량에는 어떤 차이점이 있나요?
사용 용량: MySQL 데이터 디렉터리만 포함하며, binlog, relaylog, undolog, errorlog, slowlog 로그는 포함하지 않습니다.
점유 용량: MySQL 데이터 디렉터리와 binlog, relaylog, undolog, errorlog, slowlog 로그를 포함합니다.

### TencentDB for MySQL 작업 실행 중에 버퍼가 있습니까?
**질문:**
매우 짧은 시간 내에 실행을 위해 N 개의 SQL 문을 TencentDB로 보내면 TencentDB for MySQL이 하나씩 실행하거나 충돌합니까? 허용되는 최대 동시 연결 수는 얼마입니까?
**답변:**
TencentDB for MySQL 인스턴스는 자체 구축한 MySQL 인스턴스와 동일한 방식으로 작동합니다. 동시에 실행되는 문이 충돌을 일으키는지 여부는 시스템 리소스와 SQL 문 자체에 따라 다릅니다.
연결 수 max_connections에 도달하면 인스턴스가 정상적으로 서비스를 제공하지 않습니다. 이는 일반적으로 다음과 같은 이유로 발생합니다.
- 비즈니스 애플리케이션의 bug로 인해 Null 세션이 과도하게 발생하는 경우;
- 프런트엔드 액세스가 인스턴스의 처리 능력을 크게 초과하는 경우;
- 너무 오래 실행되는 연결은 MySQL 리소스를 독점적으로 차지하므로 많은 수의 차단된 액세스 요청이 발생하는 경우입니다.

### TencentDB for MySQL 사용 시 주의사항은 무엇인가요?
자세한 내용은 [사용 제한](https://intl.cloud.tencent.com/document/product/236/7259)을 참고하십시오.

### TencentDB for MySQL 인스턴스의 기본 복제본에 대한 읽기 전용 권한을 어떻게 활성화 또는 비활성화합니까?
기본 복제본은 읽거나 쓸 수 없습니다. 주로 고가용성 전환에 사용됩니다.

### 주의해야 할 인스턴스의 모니터링 지표는 무엇입니까?
CPU 사용률, 메모리 사용률 및 디스크 공간 사용률입니다. 필요에 따라 [알람 구성](https://intl.cloud.tencent.com/document/product/236/8457)이 가능하며, 알람을 수신하면 해당 조치를 취하여 알람을 해결할 수 있습니다.

[](id:congkufangwen) 
### TencentDB for MySQL은 복제본 액세스를 지원합니까?
데이터베이스 보안을 위해 TencentDB for MySQL은 복제본에서 읽거나 쓰는 것을 허용하지 않습니다. 예를 들어 원본에 장애가 발생한 경우 신속하게 복제본으로 전환할 수 있습니다.
읽기/쓰기 능력을 확장하려면 인스턴스 구성을 업그레이드하거나 [읽기 전용 인스턴스](https://intl.cloud.tencent.com/document/product/236/7270) 구매를 고려하십시오.

[](id:myisam)
### MyISAM 데이터베이스 엔진을 사용하려면 어떻게 합니까?
MySQL v5.5를 사용하여 MyISAM을 지원할 수 있습니다. 그러나 MySQL v5.7과 같은 상위 버전을 선택하는 것이 좋습니다. 이는 상위 버전의 InnoDB 엔진이 더 세밀한 행 레벨 잠금을 제공하고, 더 높은 쓰기 성능을 제공하고, 데이터 무결성을 보장하고, 데이터베이스 장애 시 데이터 손실을 방지할 수 있기 때문입니다.

[](id:kuadiyufangwen) 
### TencentDB for MySQL은 리전 간 액세스를 지원합니까?
다른 리전의 VPC는 서로 격리되어 있으므로 기본적으로 VPC의 인스턴스에 대한 리전 간 액세스는 사용할 수 없습니다. 높은 서비스 속도와 안정성을 보장하는 로컬 데이터 액세스를 활성화하려면 CVM 인스턴스와 동일한 리전에서 TencentDB for MySQL 인스턴스를 구입하는 것이 좋습니다.

### 사용자에게 file 권한을 부여할 수 없는 이유는 무엇입니까?
현재 root 사용자는 shutdown 및 file 권한을 사용할 수 없으므로 root 사용자는 모든 권한을 가진 사용자를 생성할 수 없습니다. 권한 부여 시 다음 명령을 참고하십시오.
```
grant SELECT,INSERT, UPDATE, DELETE, CREATE, DROP, ALTER on *.* to 'myuser'@'%' identified by 'mypasswd';
```

[](id:genghuandiyu)

### TencentDB for MySQL 리전을 어떻게 변경합니까?
현재 리전 변경은 지원되지 않습니다. [DTS](https://www.tencentcloud.com/document/product/571)를 사용하여 서로 다른 리전의 인스턴스 간에 데이터를 마이그레이션할 수 있습니다. DTS는 실시간 데이터 동기화를 지원합니다. 데이터 마이그레이션이 완료되면 셀프 서비스를 통해 소스 인스턴스를 반환할 수 있습니다.

### 어떤 것이 인스턴스 용량을 차지합니까?
사용자 데이터(백업 데이터 제외), 인스턴스 실행에 필요한 데이터(시스템 데이터베이스, 데이터베이스 로그, 인덱스 등 포함). MySQL 데이터베이스에서 생성된 binlog도 포함됩니다.

### 1개의 인스턴스에서 몇 개의 데이터베이스를 실행할 수 있나요?
TencentDB for MySQL 인스턴스에서 생성할 수 있는 최대 데이터베이스 및 테이블 수는 MySQL에 따라 다릅니다. 자세한 내용은 [MySQL 공식 문서](https://dev.mysql.com/doc/)를 참고하십시오.

### 단일 노드 인스턴스를 2노드 또는 3노드 인스턴스로 업그레이드할 수 있습니까?
아니요. 현재는 2노드 인스턴스만 3노드 인스턴스로 업그레이드할 수 있습니다.

### 종량제 과금에서 정액 과금제로 전환하면 데이터베이스 비즈니스가 영향을 받습니까?
종량제 과금 인스턴스를 정액 과금제로 전환하는 것은 인스턴스 자체의 운영에는 어떤 영향도 미치지 않으며, 지불 유형만 전환됩니다. 전환 단계는 [종량제를 정액 과금제로 전환](https://www.tencentcloud.com/document/product/236/52515)을 참고하십시오.

### innodb를 myisam으로 변환할 수 없는 이유는 무엇입니까?
인스턴스가 innodb만 지원하는 MySQL v5.6 또는 v5.7을 실행 중이기 때문일 수 있습니다. myisam을 지원하려면 MySQL v5.5를 사용하십시오.

### RO 그룹 생성 수량에 제한이 있나요?
기본적으로 원본 인스턴스에 대해 최대 5개의 RO 그룹을 생성할 수 있습니다.

### canal을 사용하여 TencentDB for MySQL에서 binlog를 가져올 수 있습니까?
예. 하지만 다음 사항을 주의해야 합니다.
- canal이 배포된 CVM 인스턴스와 TencentDB for MySQL 인스턴스는 동일한 VPC에 있어야 합니다.
- 데이터 동기화에 사용되는 TencentDB for MySQL 데이터베이스 계정을 생성하고 권한을 올바르게 부여해야 합니다.
- TencentDB for MySQL 데이터베이스 매개변수: binlog_row_image=FULL 및 binlog_format=ROW를 설정해야 합니다. 

### TencentDB for MySQL 인스턴스는 물리적 머신과 CVM 중 어디에 배포됩니까?
TencentDB for MySQL 인스턴스는 가상화 기술을 사용하여 물리적 클러스터에 배포됩니다. 물리적 클러스터와 달리 CVM은 주로 확장 가능한 클라우드 컴퓨팅 서비스를 제공하는 데 사용됩니다.

### 클론이 원본 인스턴스에 영향을 줍니까?
아니요. TencentDB는 백업 데이터를 풀링해서 인스턴스를 클론하기 때문입니다. 클론이 완료되면 원본 인스턴스를 정상적으로 사용하거나 더 이상 필요하지 않으면 폐기할 수 있습니다.
