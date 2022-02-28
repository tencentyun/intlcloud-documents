#### 리소스 수준 권한 제어가 지원되는 작업

| 작업 이름               | API 이름                         | 설정 후 콘솔 적용 여부 |
| -------------------- | ------------------------------ | -------------------- |
| 전용 인스턴스 복구         | ActiveDedicatedDBInstance      | YES                  |
| 보안 그룹 바인딩           | AssociateSecurityGroups        | YES                  |
| IP 상태 확인           | CheckIpStatus                  | YES                  |
| 클로닝 계정             | CloneAccount                   | YES                  |
| 인스턴스 공용 네트워크 액세스 비활성화         | CloseDBExtranetAccess          | YES                  |
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
| 인스턴스의 보안 그룹 정보 쿼리   | DescribeDBSecurityGroups       | YES                  |
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
| 플로우 상태 쿼리         | DescribeFlow                   | YES                  |
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
| 일괄 자동 갱신 설정     | ModifyAutoRenewFlag            | YES                  |
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
