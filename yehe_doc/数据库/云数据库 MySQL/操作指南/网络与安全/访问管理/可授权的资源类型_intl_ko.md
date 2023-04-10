
리소스 수준 권한을 사용하여 사용자가 조작할 수 있는 리소스를 지정할 수 있습니다. TencentDB는 일부 리소스 수준 권한을 지원합니다. 즉, 리소스 수준 권한을 지원하는 TencentDB 작업의 경우 사용자의 작업 수행 가능 시간 또는 지정된 리소스 사용 가능 시간을 제어할 수 있습니다. 다음 표에서는 CAM에서 권한을 부여할 수 있는 리소스 유형을 설명합니다.

| 리소스 유형 | 권한 부여 정책의 리소스 설명 방법 |
| :-------- |:-------------- |
| TencentDB 인스턴스 관련 |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`

아래 표는 현재 리소스 수준 권한 제어를 지원하는 TencentDB API 작업과 각 작업에서 지원되는 리소스 및 조건 키가 나열되어 있습니다. 리소스 경로를 지정할 때 * 와일드카드를 사용할 수 있습니다.

## 리소스 수준에서 권한 부여를 지원하는 API 리스트
| API 작업 | 리소스 경로 |
|:---------|:-------------|
| AddTimeWindow| `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| AssociateSecurityGroups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| CloseWanService|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| CreateAccounts|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| CreateBackup|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| CreateDBImportJob|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DeleteAccounts|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DeleteBackup|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DeleteTimeWindow|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeAccountPrivileges|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeAccounts|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeBackupConfig|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeBackupDatabases|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeBackupDownloadDbTableCode|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeBackups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeBackupTables|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeBinlogs|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDatabases|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBImportRecords|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBInstanceCharset|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBInstanceConfig|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBInstanceGTID|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBInstanceRebootTime|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBSwitchRecords|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBSecurityGroups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeInstanceParamRecords|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeInstanceParams|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeRoGroups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeRollbackRangeTime|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeSlowLogs|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeSupportedPrivileges|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeTables|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeTimeWindow|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDatabasesForInstances |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeMonitorData |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeTableColumns |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DropDatabaseTables|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| InitDBInstances|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| IsolateDBInstance|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyAccountDescription|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyAccountPassword|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyAccountPrivileges|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyAutoRenewFlag|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyBackupConfig|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyBackupInfo|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyDBInstanceName|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyDBInstanceProject|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyDBInstanceSecurityGroups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyDBInstanceVipVport|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyInstanceParam|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyDBInstanceModes|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyTimeWindow|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyProtectMode |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| OfflineDBInstances |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| OpenDBInstanceGTID|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| OpenWanService|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ReleaseIsolatedDBInstances|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| RestartDBInstances|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| StartBatchRollback|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| SubmitBatchOperation|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| SwitchDrInstanceToMaster|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| SwitchForUpgrade|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DisassociateSecurityGroups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| UpgradeDBInstance|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| UpgradeDBInstanceEngineVersion|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 

## 리소스 수준에서 권한 부여를 지원하지 않는 API 리스트
리소스 권한을 지원하지 않는 TencentDB API에 대해서도 해당 작업의 사용 권한을 사용자에게 부여할 수는 있지만, 이때 정책 명령의 리소스 엘리먼트(Resource Element)를 반드시 *로 지정해야 합니다.

| API 작업                       | API 설명                      |
| ----------------------------- | ---------------------------- |
|CreateDBInstance              | TencentDB 인스턴스 생성(정액 과금제) |
| CreateDBInstanceHour          | TencentDB 인스턴스 생성(종량제) |
| CreateParamTemplate           | 매개변수 템플릿 생성                 |
| DeleteParamTemplate           | 모니터링 템플릿의 항목 삭제           |
| DescribeProjectSecurityGroups | 항목 보안 그룹 정보 조회           |
| DescribeDefaultParams         | 기본 설정 가능한 매개변수 리스트 조회     |
| DescribeParamTemplateInfo     | 매개변수 템플릿 상세 조회             |
| DescribeParamTemplates        | 매개변수 템플릿 리스트 조회             |
| DescribeAsyncRequestInfo      | 비동기화 작업의 실행 결과 조회       |
| DescribeTasks                 | TencentDB 인스턴스 작업 리스트 조회     |
| DescribeUploadedFiles         | 가져온 SQL 파일 리스트 조회          |
| ModifyParamTemplate           | 매개변수 템플릿 수정                 |
| RenewDBInstance               | TencentDB 인스턴스 구독 연장             |
| StopDBImportJob               | 데이터 가져오기 작업 중단             |
| DescribleRoMinScale           | 읽기 전용 인스턴스에서 지원하는 최저 사양 조회          |
| DescribeRequestResult           | 작업 상세 조회       |
| DescribeRoMinScale           | 읽기 전용 인스턴스 구매 또는 업그레이드 시 최저 사양 조회          |

