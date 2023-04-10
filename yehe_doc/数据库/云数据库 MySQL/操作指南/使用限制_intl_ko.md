## 데이터양 제한
TencentDB for MySQL은 제한된 리소스로 인한 성능 문제를 격리하기 위해 모든 유형의 MySQL 인스턴스에 데이터양 제한을 적용합니다. 본문은 대용량 데이터양이 있는 단일 인스턴스 또는 테이블이 MySQL에 미치는 기술적 영향에 대해 설명합니다.

**데이터양이 큰 인스턴스**: TencentDB의 기본 스토리지 엔진은 InnoDB입니다. cache, buffer가 MySQL 인스턴스의 모든 데이터 및 인덱스 페이지를 캐시할 수 있는 경우 인스턴스는 많은 수의 동시 액세스 요청을 지원할 수 있습니다. 인스턴스에 너무 많은 데이터가 포함되어 있으면 cache와 buffer가 데이터를 자주 교환하여 IO 병목 현상이 빠르게 발생하고 처리량이 감소합니다. 예를 들어 TencentDB 인스턴스가 초당 최대 8000개의 액세스 요청을 유지하도록 설계된 경우 데이터양이 cache 및 buffer 크기의 두 배일 때 초당 700개 정도만 지원할 수 있습니다.

**데이터양이 큰 테이블**: 테이블에 너무 많은 데이터가 포함되어 있으면 MySQL은 테이블 리소스(데이터, 인덱스 등)를 관리하기가 더 어려워 테이블 처리 효율성이 떨어집니다. 예를 들어 트랜잭션 테이블(InnoDB)의 크기가 10GB를 초과하면 업데이트 작업의 대기 시간이 급증하여 트랜잭션에 대한 응답 시간이 늘어납니다. 이 경우 샤딩과 마이그레이션을 통해서만 문제를 해결할 수 있습니다.

>?단일 인스턴스의 테이블 수가 100만 개를 초과하면 백업, 모니터링, 업그레이드가 실패하고 데이터베이스 모니터링이 영향을 받을 수 있습니다. 단일 인스턴스의 테이블 수가 100만 미만인지 확인하십시오.

## 연결 수 제한
MySQL 인스턴스에 대한 최대 연결 수는 MySQL 시스템 변수 max_connections로 지정됩니다. 실제 연결 수가 max_connections를 초과하면 더 이상 연결을 설정할 수 없습니다.
TencentDB에 대한 기본 연결 수는 [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에서 인스턴스 ID를 클릭하고, **데이터베이스 관리** > **매개변수 설정** 페이지로 들어가 볼 수 있으며, 필요한 경우 max_connections 값을 조정할 수 있습니다. 그러나 더 많은 연결은 더 많은 시스템 리소스가 소비됨을 의미합니다. 연결 수가 실제 시스템 부하 용량을 초과하면 시스템 서비스 품질이 필연적으로 저하됩니다.
max_connections에 대한 자세한 내용은 [MySQL 공식 문서](https://dev.mysql.com/doc/)를 참고하십시오.

## MySQL 클라이언트 버전 제한
CVM과 함께 제공되는 MySQL 클라이언트 및 라이브러리를 사용하여 TencentDB 인스턴스에 연결하는 것이 좋습니다.

### 슬로우 로그에 대한 참고 사항
- Linux CVM 인스턴스의 경우 TencentDB의 내보내기 툴을 사용하여 슬로우 쿼리 로그를 가져올 수 있습니다. 자세한 내용은 [물리 백업을 사용하여 데이터베이스 복구](https://intl.cloud.tencent.com/document/product/236/31910)를 참고하십시오.
- Windows CVM 인스턴스의 경우 현재 슬로우 쿼리 로그를 직접 가져올 수 없습니다. 필요한 경우 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)하여 도움을 받으십시오.

### TencentDB binlog 보관 기간에 대한 참고 사항
TencentDB for MySQL binlog는 7일(기본값) - 1830일 동안 보관할 수 있습니다(인스턴스 ID를 클릭하여 **백업 및 복원** > **자동 백업 설정** 페이지로 이동하여 설정 가능). 
binlog를 너무 오래 보관하거나 증가 속도가 지나치게 빠른 경우, 백업을 위한 추가 공간이 필요하며, 공간이 백업 용량의 프리 티어를 초과하는 경우 요금이 부과됩니다.

### 문자 세트에 대한 참고 사항
TencentDB for MySQL은 기본적으로 UTF8 문자 세트를 사용합니다.
TencentDB는 기본 문자 세트 변경을 지원하지만 테이블을 생성할 때 테이블의 인코딩 형식을 명시적으로 지정하고 연결 설정 중에 연결 인코딩을 지정하는 것이 좋습니다. 이렇게 하면 애플리케이션의 이식성이 향상됩니다.
MySQL 문자 세트 리소스에 대한 자세한 내용은 [MySQL 공식 문서](https://dev.mysql.com/doc/)를 참고하십시오.

SQL 또는 TencentDB for MySQL 콘솔을 통해 문자 세트를 수정할 수 있습니다.

#### SQL을 통한 문자 세트 수정
1. 다음 SQL 문을 실행하여 TencentDB 인스턴스의 기본 문자 세트를 변경합니다.
```
SET @@global.character_set_client = utf8;
SET @@global.character_set_results = utf8;
SET @@global.character_set_connection = utf8;
SET @@global.character_set_server = utf8;
```
명령문이 실행된 후 @@global.character_set_server는 약 10분 안에 지속성을 위해 로컬 파일에 자동으로 동기화되지만, 다른 3개의 변수는 동기화되지 않습니다. 구성된 값은 마이그레이션 또는 재시작 후에도 변경되지 않은 상태로 유지됩니다.
2. 다음 문을 실행하여 현재 연결에 대한 문자 세트 인코딩을 변경합니다.
```
SET @@session.character_set_client = utf8;
SET @@session.character_set_results = utf8;
SET @@session.character_set_connection = utf8;
```
 또는 
```
SET names utf8;
```
3. PHP 프로그램의 경우 다음 기능을 사용하여 현재 연결에 대한 문자 세트 인코딩을 구성할 수 있습니다.
```
bool mysqli::set_charset(string charset);
```
 또는 
```
bool mysqli_set_charset(mysqli link, string charset);
```
4. Java 프로그램의 경우 아래와 같이 현재 연결에 대한 문자 세트 인코딩을 구성할 수 있습니다.
```
jdbc:mysql://localhost:3306/dbname?useUnicode=true&characterEncoding=UTF-8
```

#### TencentDB for MySQL 콘솔에서 문자 세트 수정
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인하고 인스턴스 목록에서 인스턴스 ID를 클릭하여 인스턴스 세부 정보 페이지로 이동합니다.
2. 기본 정보에서 문자 세트를 찾고, 수정 아이콘을 클릭하여 문자 세트를 수정합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c970624cd5c1424b880719a2708c1e55.png)
3. 팝업 창에서 문자 세트를 선택하고 **확인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/53466da07103fff22b41c6fa6f5ca4e7.png)

### 작업 제한
1. MySQL 인스턴스 기존 계정의 정보와 권한을 수정하지 마십시오. 그렇지 않으면 일부 클러스터 서비스를 사용할 수 없게 될 수 있습니다.
2. 인스턴스가 많은 수의 동시 액세스 요청을 더 잘 지원할 수 있도록 데이터베이스 및 테이블 생성에 InnoDB 엔진 사용할 것을 권장합니다.
3. master-slave 관계를 수정하거나 종료하지 마십시오. 그렇지 않으면 핫 백업이 실패할 수 있습니다.

### 테이블 이름 제한
중국어 테이블 이름은 롤백 및 업그레이드와 같은 프로세스의 실패를 초래할 수 있으므로 지원되지 않습니다.

## 데이터베이스 계정 권한
TencentDB for MySQL은 더 이상 super user 권한을 제공하지 않습니다. 이 권한이 필요한 매개변수를 수정하려면 [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 후 인스턴스 ID를 클릭하여 **데이터베이스 관리** > **매개변수 설정** 페이지로 이동한 후 수정합니다.

## 네트워크 선택
VPC를 사용하는 것이 좋습니다. VPC에서 IP 범위 분할, IP 주소 및 라우팅 정책을 자유롭게 정의할 수 있습니다. 기존 네트워크와 비교할 때 VPC는 사용자 지정 네트워크 구성이 필요한 시나리오에 더 적합합니다. VPC와 기존 네트워크의 비교는 [개요](https://intl.cloud.tencent.com/document/product/215/31807)를 참고하십시오.

