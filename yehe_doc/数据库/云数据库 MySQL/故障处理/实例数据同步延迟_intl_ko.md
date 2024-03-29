
## 현상 설명
TencentDB for MySQL의 상응하는 기본 백업 데이터베이스, 재해 복구 인스턴스, 읽기 전용 인스턴스는 모두 MySQL 네이티브 binlog 복제 기술을 사용하며, 데이터 복제 방식이 비동기화 복제 또는 반동기화 복제인 경우 딜레이가 발생할 수 있습니다.

## 장애 영향
- [백업 데이터베이스](https://intl.cloud.tencent.com/document/product/236/38328)에 딜레이가 있는 경우, 프라이머리/세컨더리 인스턴스가 짧은 시간 내에 전환되지 않아 비즈니스가 신속하게 정상화되지 않을 수 있습니다.
- [재해 복구 인스턴스]에 딜레이가 있는 경우, 쌓인 binlog가 모두 적용되지 않을 때까지 재해 복구 인스턴스를 프라이머리 인스턴스로 성공적으로 업그레이드할 수 없으며, 이 기간 동안 비즈니스 연속성이 영향을 받을 수 있습니다.
- 읽기 서비스가 데이터 일관성에 대한 요구 사항이 높을 경우 [읽기 전용 그룹](https://intl.cloud.tencent.com/document/product/236/11361#.E9.85.8D.E7.BD.AE.E5.8F.AA.E8.AF.BB.E5.AE.9E.E4.BE.8B-ro-.E7.BB.84)은 딜레이 제거 정책을 설정할 수 있으며 읽기 전용 인스턴스와 프라이머리 인스턴스 간의 딜레이 시간이 임계값을 초과하면 해당 읽기 전용 인스턴스가 자동으로 제거되어 읽기 서비스가 읽기 전용 인스턴스에 정상적으로 액세스할 수 없습니다.

## 예상 원인
- **기본 키 또는 2단계 인덱스 없음**
binlog가 row 포맷이고 테이블에 기본 키 또는 2단계 인덱스가 없는 상태에서 대용량 테이블에 DML 작업(예: delete, update, insert)을 진행하고 세컨더리 데이터베이스에서 binlog 로그를 응용하는 경우, 기본 키 또는 2단계 인덱스에 따라 변경할 행을 검색합니다. 해당 테이블에 기본 키 또는 2단계 인덱스를 생성하지 않은 경우 대량의 전체 테이블 스캔 작업으로 로그 응용 속도가 감소되고 데이터 딜레이가 발생합니다.
처리 순서는 [기본 키 또는 2단계 인덱스 없음](#wzjhejsy)을 참고하십시오.

- **대규모 트랜잭션** 
대규모 트랜잭션: 데이터를 추가, 삭제, 수정하는 insert, update, delete, replace와 같은 명령을 의미합니다. 한 트랜잭션에 수백만 행의 데이터 작업이 포함되어 있거나 한 SQL 명령이 백만 행의 데이터를 수정하는 경우 실행 시간이 30초를 초과하게 됩니다.
프라이머리 인스턴스에서 대량의 데이터 DML 작업을 진행하여 대량의 binlog 로그가 세컨더리 데이터베이스로 전송되는 경우, 세컨더리 데이터베이스는 해당 트랜잭션을 완료하는 데 프라이머리 인스턴스와 동일한 시간을 소모하므로 세컨더리 데이터베이스에 데이터 딜레이가 발생합니다. 처리 순서는 [트랜잭션](#dsw)을 참고하십시오.


- **DDL 작업**
읽기 전용 노드에서는 사용자의 쿼리가 상위에서 실행됩니다. 읽기 전용 노드에 실행 시간이 긴 쿼리가 실행 중인 경우, 작업이 종료될 때까지 해당 쿼리가 프라이머리 데이터베이스의 DDL을 차단하여 읽기 전용 노드에 데이터 딜레이가 발생할 수 있습니다. 처리 순서는 [DDL 작업](#dcz)을 참고하십시오.

- **너무 낮은 인스턴스 사양**
읽기 전용 인스턴스, 재해 복구 인스턴스의 사양이 너무 낮고 프라이머리 인스턴스의 부하가 비교적 높은 경우, 읽기 전용 인스턴스, 재해 복구 인스턴스에 데이터 딜레이가 발생합니다.
처리 순서는 [너무 낮은 인스턴스 사양](#slgggx)을 참고하십시오.

- **Waiting for table metadata lock 오류 보고**
대규모 트랜잭션이 실행되어 DDL을 차단하고 동일 테이블의 모든 후속 작업을 차단합니다. 미제출 트랜잭션이 DDL을 차단하고 동일 테이블의 모든 후속 작업을 차단합니다.
처리 순서는 [Waiting for table metadata lock 오류 보고](#wftmlbc)를 참고하십시오.

## 처리 단계
### [기본 키 또는 2단계 인덱스 없음](id:wzjhejsy)
[DBbrain 콘솔](https://console.cloud.tencent.com/dbbrain/performance/disk)에 로그인한 후, 왼쪽 사이드바에서 **진단 최적화**를 선택한 다음 상단에서 해당하는 데이터베이스를 선택하고 **용량 분석** 페이지를 선택합니다.
2. 용량 분석 페이지 하단에서 **기본 키가 없는 테이블** 페이지를 선택해 리스트에서 기본 키가 없는 테이블을 클릭하면 테이블의 필드 및 인덱스 정보를 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/070bf60984827fb43a33048a38a5969b.png)
>?기본 키가 없는 테이블 리스트는 정기 스캔(하루 1회 스캔) 및 수동 업데이트 두 가지 방식을 지원하며, 실제 상황에 따라 선택할 수 있습니다.
3. 2단계의 기본 키가 없는 테이블에 기본 키를 생성합니다. 테이블에 기본 키를 생성하지 못하는 경우 기수가 높은 열을 선택해 2단계 인덱스를 생성하는 것을 권장합니다.

### [대규모 트랜잭션](id:dsw)
1. [DBbrain 콘솔](https://console.cloud.tencent.com/dbbrain/event)에 로그인한 후, 이상 알람 페이지에서 해당 데이터베이스와 리전을 선택하고 **진단 항목**에서 **트랜잭션으로 인한 복사 딜레이**를 선택하면 인스턴스의 대규모 트랜잭션을 필터링하여 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/508e3bfd033a2f5a5422aae9902cc598.png)
2. 대규모 트랜잭션을 소규모 트랜잭션으로 분할하여 where 조건으로 매번 처리해야 하는 데이터 양을 제한합니다.
>?DBbrain을 통해 시간이 소모되는 대규모 트랜잭션을 파악하고 대규모 트랜잭션을 소규모 트랜잭션으로 분할하면 읽기 전용 노드에서 트랜잭션을 빠르게 완료할 수 있으며 데이터 딜레이가 발생하지 않습니다.

### [DDL 작업](id:dcz)
1. [DBbrain 콘솔](https://console.cloud.tencent.com/dbbrain/event)에 로그인한 후, 이상 알람 페이지에서 해당 데이터베이스와 리전을 선택하고 **진단 항목**에서 **DDL로 인한 복사 딜레이**를 선택하면 인스턴스의 해당 DDL 작업을 필터링하여 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/7d7c9ec01da894fa1554f6d9bf135366.png)
2. 알람 테이블에서 **작업** 열의 **상세 내용**을 클릭하면 이벤트 세부 사항 페이지로 이동해 처리할 수 있습니다.
 - 이벤트 상세 내용: 진단 항목, 시작 및 종료 시간, 리스크 등급, 지속 시간, 개요 등의 정보 포함
 - 현장 설명: 이상 이벤트(또는 상태 점검 이벤트)의 표면적 현상 스냅샷 및 성능 추세
 - 스마트 분석: 성능 이상을 초래한 근본 원인 분석 및 구체적 작업 파악
 - 최적화 권장 사항: SQL 최적화(인덱스 권장 사항, 다시 쓰기 권장 사항), 리소스 설정 최적화, 매개변수 최적화 조정 등의 최적화 가이드 권장 사항 제공


### [너무 낮은 인스턴스 사양](id:slgggx)
1. 읽기 전용 인스턴스, 재해 복구 인스턴스 사양의 크기는 프라이머리 인스턴스보다 동일하거나 높은 사양으로 사용하기를 권장합니다. 인스턴스 사양은 [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인하여 인스턴스 리스트에서 확인할 수 있습니다.
2. 읽기 전용 인스턴스, 재해 복구 인스턴스가 대량의 분석 작업을 실행하여 인스턴스 부하가 너무 높아지는 경우, 해당 인스턴스 사양을 적합한 설정으로 업그레이드하거나 성능 효율이 낮은 SQL을 최적화해야 합니다.
 - 저효율 SQL 최적화에 대한 자세한 내용은 [SQL 최적화](https://intl.cloud.tencent.com/document/product/1035/36040)를 참고하십시오.
 - 인스턴스 사양 업그레이드에 대한 자세한 내용은 [데이터베이스 인스턴스 사양 변경](https://intl.cloud.tencent.com/document/product/236/19707)을 참고하십시오.

### [Waiting for table metadata lock 오류 보고](id:wftmlbc)
[DBbrain](https://intl.cloud.tencent.com/document/product/1035/36036)을 사용하여 실제 비즈니스 및 인스턴스를 진단하고 슬로우 쿼리 등의 지표를 점검하여 시간을 소모하는 대규모 트랜잭션을 파악하는 것을 권장합니다.
1. [DBbrain 콘솔](https://console.cloud.tencent.com/dbbrain/event)에 로그인한 후, 이상 알람 페이지에서 해당 데이터베이스와 리전을 선택하고 **진단 항목**에서 아래와 같은 진단 항목을 선택해 시간을 소모하는 대규모 트랜잭션을 파악합니다.
![](https://main.qcloudimg.com/raw/11e0dc3ba8fa61eaf07ec3ecf7e38474.png)
2. 각 장애 시나리오별 처리 조치
 - 대규모 트랜잭션이 실행되어 DDL을 차단하고 동일 테이블의 모든 후속 작업을 차단한 경우, DBbrain의 이상 진단 안내에 따라 대규모 트랜잭션의 ID를 찾은 후 kill합니다.
 - 미제출 트랜잭션이 DDL을 차단하고 동일 테이블의 모든 후속 작업을 차단한 경우, DBbrain의 이상 진단에 따라 미제출 트랜젝션의 ID를 찾은 후 kill하고 프로그램을 진단해 즉시 트랜잭션을 제출합니다.
 - 명시적 트랜잭션에서 TableA에 대한 작업에 실패했고(예: 존재하지 않는 필드 조회), 이때 트랜잭션이 시작되진 않았지만 실패 명령이 획득한 잠금 상태가 여전히 유효하여 릴리스되지 않는 경우, DBbrain의 이상 진단에 따라 session ID를 찾은 후 kill합니다.
