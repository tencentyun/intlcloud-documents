
## 데이터 양 제한
리소스에 제한이 있음에 따라 성능 면에서 사용자 간의 영향을 차단하기 위해 TencentDB for MySQL은 각 유형의 MySQL 인스턴스의 데이터양을 제한하였습니다. 아래는 기술적 각도에서, 대용량 데이터일 때 MySQL에서 단일 인스턴스 및 단일 테이블 사용 시의 영향에 대해 안내합니다.

**대용량 데이터 인스턴스**: 클라우드 데이터베이스의 기본 스토리지 엔진은 InnoDB입니다. 인스턴스의 데이터 및 인덱스 페이지 모두 InnoDB의 cache, buffer에 의해 캐싱 될 수 있는 경우, MySQL 인스턴스는 대규모의 동시 액세스를 지원합니다. 인스턴스의 데이터가 지나치게 크면 cache, buffer가 빈번한 데이터 인/아웃을 야기하며 MySQL 병목 현상이 곧 IO로 전환되어 액세스 처리량이 대폭 줄어듭니다(예시, 어떤 클라우드 데이터베이스 인스턴스가 8,000회까지 액세스를 지원하고, 데이터 양이 cache, buffer 크기의 두 배인 경우, 초당 약 700회 정도만 액세스할 수 있습니다).

**대용량 데이터 테이블**: 개별 테이블의 데이터 양이 지나치게 큰 경우, MySQL에서 개별 테이블의 리소스를 관리하는 요금(데이터, 인덱스 등)이 변경됩니다. 이는 직접 테이블의 프로세싱 효율에 영향을 미칩니다. 예를 들면 서비스 테이블(InnoDB)의 데이터 양이 10GB에 달하면 업데이트 시 딜레이가 뚜렷이 증가하므로 서비스 응답 시간에 영향을 미칩니다. 심할 경우 마이그레이션, 테이블 샤딩으로 해결해야 합니다.

>?단일 인스턴스의 테이블 수량이 100만 개를 초과하면 백업, 모니터링, 업그레이드에 실패할 수 있으며 데이터베이스 모니터링에도 영향을 미칠 수 있으므로 테이블 수량을 합리적인 수준으로 적용하시고, 단일 인스턴스 테이블 수량이 100만 개를 넘지 않도록 제어하시기 바랍니다.

## 연결 수 제한
MySQL의 연결수 상한은 MySQL의 시스템 변량 max_connections입니다. MySQL 인스턴스 연결수가 max_connections를 초과 시에 신규 연결을 생성할 수 없습니다.
클라우드 데이터베이스 기본 연결 수는 [MySQL 콘솔](https://console.cloud.tencent.com/cdb)의 인스턴스 ID를 클릭하여 **데이터베이스 관리** > **매개변수 설정**에서 확인할 수 있습니다. 사용자의 필요에 따라 max_connections 값을 변경할 수 있으나, 연결 수가 많을수록 시스템 리소스의 소모량도 증가합니다. 연결 수가 실제 시스템 부하 범위를 초과하면 시스템 서비스 품질에 영향을 미칩니다.
max_connections 관련 사항은 [MySQL 공식 문서](https://dev.mysql.com/doc/)를 참고하십시오.

## 클라우드 데이터베이스에 연결된 MySQL 클라이언트 제한
CVM 시스템에 적용된 MySQL 클라이언트와 lib 라이브러리를 사용하여 클라우드 데이터베이스 인스턴스를 연결하시기 바랍니다.

### 슬로우 쿼리 설명
- Linux CVM을 사용하는 개발자의 경우, 클라우드 데이터베이스 출력 툴을 이용하여 슬로우 쿼리 로그를 획득할 수 있습니다. 상세 내역은 [백업 파일과 로그 다운로드](https://intl.cloud.tencent.com/document/product/236/31910)를 참고하십시오.
- Windows CVM을 사용하는 개발자의 경우, 현재로선 슬로우 쿼리 로그를 직접 획득할 수 없습니다. 필요하다면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 슬로우 쿼리 로그 파일을 획득할 수 있습니다.

### 클라우드 데이터베이스의 binlog 보관 시간 설명
TencentDB for MySQL binlog 로그 파일은 7일 - 1830일 동안 보관할 수 있으며 기본값은 7일입니다(인스턴스 ID를 클릭하여 **백업 복구** > **자동 백업 설정**을 입력하여 보관 기간 설정). 
binlog를 너무 오래 보관하거나 증가 속도가 지나치게 빠를 경우 백업 용량이 커질 수 있습니다. 백업 용량이 시스템에서 할당한 용량을 초과하면 추가 요금이 부과될 수 있습니다.

### 문자 세트 설명
TencentDB for MySQL의 기본 문자 세트 인코딩 포맷은 UTF8입니다.
클라우드 데이터베이스는 기본적으로 문자 세트 코딩을 설정합니다. 하지만 테이블 생성 시 지정 테이블의 코딩을 명시하고, 연결 시 연결 코딩을 지정해야 애플리케이션을 보다 원활히 포팅할 수 있습니다.
MySQL 문자 세트 리소스에 대한 내용은 [MySQL 공식 문서](https://dev.mysql.com/doc/)를 참고 바랍니다.

SQL 언어 또는 MySQL 콘솔을 통해 문자 세트를 수정할 수 있습니다.

#### SQL 언어로 문자 세트 수정
1. SQL 언어를 통해 다음 명령문을 실행하여 클라우드 데이터베이스 인스턴스의 기본 문자 세트 인코딩을 수정할 수 있습니다.
```
SET @@global.character_set_client = utf8;
SET @@global.character_set_results = utf8;
SET @@global.character_set_connection = utf8;
SET @@global.character_set_server = utf8;
```
명령을 실행한 후, 그 중의 @@global.character_set_server가 10분 정도 대기한 다음 로컬 파일에 자동으로 동기화되고 지속(다른 3개의 변수는 로컬 파일에 동기화되지 않음)됩니다. 마이그레이션 혹은 재시작하면 설정한 후의 값이 유지됩니다.
2. 다음 문구를 실행하면 기존에 연결한 문자 세트 코딩을 수정할 수 있습니다.
```
SET @@session.character_set_client = utf8;
SET @@session.character_set_results = utf8;
SET @@session.character_set_connection = utf8;
```
 또는 
```
SET names utf8;
```
3. PHP 프로그램의 경우, 다음 함수를 통해 기존에 연결한 문자 세트 코딩을 설정할 수 있습니다.
```
bool mysqli::set_charset(string charset);
```
 또는 
```
bool mysqli_set_charset(mysqli link, string charset);
```
4. Java 프로그램의 경우, 다음 방법으로 기존에 연결한 문자 세트 코딩을 설정할 수 있습니다.
```
jdbc:mysql://localhost:3306/dbname?useUnicode=true&characterEncoding=UTF-8
```

#### MySQL 콘솔을 통해 문자 세트 수정
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 후, 인스턴스 리스트에서 인스턴스 ID를 클릭하여 인스턴스 상세 페이지로 이동합니다.
2. 기본 정보에서 문자 세트를 찾고, 수정 아이콘을 클릭하여 문자 세트를 수정합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c970624cd5c1424b880719a2708c1e55.png)
3. 팝업 창에서 문자 세트를 선택하고 **확인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/53466da07103fff22b41c6fa6f5ca4e7.png)

### 작업 제한
1. MySQL 인스턴스 기존 계정의 정보와 권한을 수정하지 마십시오. 수정 시 일부 클러스터 서비스가 적용되지 않을 수 있습니다.
2. 라이브러리와 테이블을 생성 시에 일괄 InnoDB 엔진을 사용하시기를 권장드립니다. 해당 엔진을 사용하면 인스턴스는 더 뛰어난 성능으로 액세스할 수 있습니다. 
3. master-slave 관계를 수정하거나 종료하지 마십시오. 이 작업으로 핫 백업이 적용되지 않을 수 있습니다. 

### 데이터베이스 테이블명 제한
테이블명은 중국어로 적용할 수 없으며, 테이블을 생성 시에 잘 확인해주시기 바랍니다. 중국어 테이블명은 롤백하거나 업그레이드 프로세스 실패를 야기할 수 있습니다.

## 데이터베이스 계정 권한
TencentDB for MySQL은 더 이상 super user 권한을 제공하지 않습니다. 수정 시 이 권한이 필요한 매개변수는 [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에서 인스턴스 ID를 클릭하고 **데이터베이스 관리** > **매개변수 설정**에서 수정합니다.

## 네트워크 선택
VPC를 사용하는 것이 좋습니다. 필요에 따라 IP 범위 세분화, IP 주소 및 라우팅 정책을 정의할 수 있습니다. 기존 네트워크와 비교하여 VPC는 사용자 지정 네트워크 구성이 필요한 시나리오에 더 적합합니다. VPC와 Classiclink의 비교는 [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807)를 참고하십시오.

