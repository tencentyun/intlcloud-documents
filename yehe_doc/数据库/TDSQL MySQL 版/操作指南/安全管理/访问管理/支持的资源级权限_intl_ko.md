
>!기존 이유로 액세스 관리에서 TDSQL for MySQL의 인터페이스 키워드는 dcdb입니다.

리소스 수준 권한을 사용하여 사용자가 조작할 수 있는 리소스를 지정할 수 있습니다. TencentDB는 특정 리소스 수준 권한을 지원합니다. 즉, 일부 TencentDB 작업의 경우 사용자가 작업(필수 조건에 따라)을 수행하거나 지정된 리소스를 사용하도록 허용되는 시간을 제어할 수 있습니다. 다음 표는 TencentDB에서 권한을 부여할 수 있는 리소스 유형을 설명합니다.

CAM에서 승인할 수 있는 리소스 유형:

| 리소스 유형 | 권한 부여 정책 중 리소스 메소드 설명 |
| :-------- |:-------------- |
| CDB 인스턴스 관련 |  `qcs::dcdb:$region:$account:instance/*`<br>`qcs::dcdb:$region:$account:instance/$instanceId`

아래 표에서는 현재 리소스 권한 부여를 지원하는 CDB API 작업과 더불어, 각 작업에서 지원되는 리소스 및 조건 키에 대해 소개하고 있습니다. 리소스 경로를 지정할 때에는 * 와일드카드 문자를 사용할 수 있습니다.

>?상기에 나열되지 않은 TencentDB API 작업은 리소스 수준 권한을 지원하지 않습니다. TencentDB API 작업이 리소스 수준 권한을 지원하지 않는 경우에도 사용자에게 이 작업을 수행하도록 권한을 부여할 수 있지만 정책 설명의 리소스 요소에 *를 지정해야 합니다.

#### 다음 작업은 리소스 수준 권한 제어 지원

| 작업 이름               | API 이름                         | 설정 후 콘솔 적용 여부 |
| -------------------- | ------------------------------ | -------------------- |
| 전용 인스턴스 복구         | ActiveDedicatedDBInstance      | YES                  |
| 보안 그룹 바인딩           | AssociateSecurityGroups        | YES                  |
| IP 상태 확인           | CheckIpStatus                  | YES                  |
| 계정 복제             | CloneAccount                   | YES                  |
| 인스턴스에 대한 공용 네트워크 액세스 비활성화         | CloseDBExtranetAccess          | YES                  |
| 계정 권한 복사         | CopyAccountPrivileges          | YES                  |
| 계정 생성             | CreateAccount                  | YES                  |
| 인스턴스 생성             | CreateDCDBInstance             | YES                  |
| 계정 삭제             | DeleteAccount                  | YES                  |
| 계정 권한 쿼리         | DescribeAccountPrivileges      | YES                  |
| 계정 목록 쿼리         | DescribeAccounts               | YES                  |
| 감사 로그 쿼리         | DescribeAuditLogs              | YES                  |
| 감사 규칙 세부 정보 쿼리     | DescribeAuditRuleDetail        | YES                  |
| 감사 규칙 목록 쿼리     | DescribeAuditRules             | YES                  |
| 감사 정책 쿼리         | DescribeAuditStrategies        | YES                  |
| 일괄 인스턴스 갱신 가격 쿼리 | DescribeBatchDCDBRenewalPrice  | YES                  |
| 인스턴스 객체 쿼리         | DescribeDatabaseObjects        | YES                  |
| 인스턴스 BD 이름 쿼리         | DescribeDatabases              | YES                  |
| 인스턴스 테이블의 컬럼 정보 쿼리   | DescribeDatabaseTable          | YES                  |
| 로그 목록 가져오기         | DescribeDBLogFiles             | YES                  |
| 모니터링 정보 쿼리         | DescribeDBMetrics              | YES                  |
| 데이터베이스 매개변수 조회       | DescribeDBParameters           | YES                  |
| 인스턴스 보안 그룹 정보 쿼리   | DescribeDBSecurityGroups       | YES                  |
| 슬로우 로그 기록 세부 정보 가져오기   | DescribeDBSlowLogAnalysis      | YES                  |
| 슬로우 로그 목록 가져오기   | DescribeDBSlowLogs             | YES                  |
| 인스턴스 동기화 모드 쿼리     | DescribeDBSyncMode             | YES                  |
| 인스턴스 세부정보 가져오기     | DescribeDCDBInstanceDetail     | YES                  |
| 인스턴스 목록 보기         | DescribeDCDBInstances          | YES                  |
| 가격 쿼리             | DescribeDCDBPrice              | YES                  |
| 인스턴스 갱신 가격 쿼리     | DescribeDCDBRenewalPrice       | YES                  |
| 구매 가능한 AZ 쿼리       | DescribeDCDBSaleInfo           | YES                  |
| 인스턴스 샤드 쿼리     | DescribeDCDBShards             | YES                  |
| 인스턴스의 업그레이드 가격 쿼리     | DescribeDCDBUpgradePrice       | YES                  |
| 전용 클러스터 사양 쿼리     | DescribeFenceShardSpec         | YES                  |
| 흐름 상태 쿼리         | DescribeFlow                   | YES                  |
| 최신 DBA 점검 결과 쿼리  | DescribeLatestCloudDBAReport   | YES                  |
| 백업 로그 설정 보기     | DescribeLogFileRetentionPeriod | YES                  |
| 주문 정보 쿼리         | DescribeOrders                 | YES                  |
| 프로젝트 쿼리             | DescribeProjects               | YES                  |
| 프로젝트의 보안 그룹 정보 쿼리   | DescribeProjectSecurityGroups  | YES                  |
| 인스턴스 사양 쿼리         | DescribeShardSpec              | YES                  |
| SQL 로그 가져오기          | DescribeSqlLogs                | YES                  |
| Tencent Cloud 리소스에서 보안 그룹을 일괄적으로 바인딩 해제 | DisassociateSecurityGroups     | YES                  |
| 계정 권한 설정         | GrantAccountPrivileges         | YES                  |
| 인스턴스 초기화           | InitDCDBInstances              | YES                  |
| 전용 인스턴스 격리         | IsolateDedicatedDBInstance     | YES                  |
| 데이터베이스 계정 비고 수정   | ModifyAccountDescription       | YES                  |
| 일괄 자동 연장 설정     | ModifyAutoRenewFlag            | YES                  |
| 인스턴스 이름 수정         | ModifyDBInstanceName           | YES                  |
| TencentDB 인스턴스에 바인딩된 보안 그룹 수정   | ModifyDBInstanceSecurityGroups | YES                  |
| 인스턴스 프로젝트 수정         | ModifyDBInstancesProject       | YES                  |
| 데이터베이스 매개변수 수정       | ModifyDBParameters             | YES                  |
| 인스턴스 동기화 모드 수정     | ModifyDBSyncMode               | YES                  |
| 인스턴스 네트워크 수정     | ModifyInstanceNetwork          | YES                  |
| 인스턴스 VIP 수정          | ModifyInstanceVip              | YES                  |
| 백업 로그 설정 수정     | ModifyLogFileRetentionPeriod   | YES                  |
| 공용 네트워크 액세스 활성화             | OpenDBExtranetAccess           | YES                  |
| 인스턴스 갱신             | RenewDCDBInstance              | YES                  |
| 계정 비밀번호 재설정         | ResetAccountPassword           | YES                  |
| 스마트 DBA 활성화          | StartSmartDBA                  | YES                  |
| 인스턴스 확장             | UpgradeDCDBInstance            | YES                  |
| 전용 인스턴스 업그레이드     | UpgradeDedicatedDCDBInstance   | YES                  |


