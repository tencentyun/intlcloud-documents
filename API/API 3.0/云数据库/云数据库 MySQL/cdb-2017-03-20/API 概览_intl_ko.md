## 태스크 관련 API

| API 이름 | API 기능 |
|---------|---------|
| [DescribeAsyncRequestInfo](/document/api/236/20410) | 비동기화 태스크 실행 결과 조회 |
| [DescribeTasks](/document/api/236/15848) | 데이터베이스 인스턴스 태스크 리스트 조회 |

## 매개변수 관련 API

| API 이름 | API 기능 |
|---------|---------|
| [CreateParamTemplate](/document/api/236/32663) | 매개변수 템플릿 생성 |
| [DeleteParamTemplate](/document/api/236/32824) | 매개변수 템플릿 삭제 |
| [DescribeDefaultParams](/document/api/236/32662) | 기본적인 설정 가능 매개변수 리스트 조회 |
| [DescribeInstanceParamRecords](/document/api/236/32661) | 인스턴스 매개변수 수정 이력 조회 |
| [DescribeInstanceParams](/document/api/236/20411) | 인스턴스의 설정 가능 매개변수 리스트 조회 |
| [DescribeParamTemplateInfo](/document/api/236/32660) | 매개변수 템플릿 세부 정보 조회 |
| [DescribeParamTemplates](/document/api/236/32659) | 매개변수 템플릿 리스트 조회 |
| [ModifyInstanceParam](/document/api/236/15860) | 인스턴스 매개변수 수정 |
| [ModifyParamTemplate](/document/api/236/32658) | 매개변수 템플릿 수정 |

## 롤백 관련 API

| API 이름 | API 기능 |
|---------|---------|
| [DescribeRollbackRangeTime](/document/api/236/18726) | 롤백 가능 시간 조회 |
| [StartBatchRollback](/document/api/236/18725) | 롤백 데이터베이스 테이블 |

## 백업 관련 API

| API 이름 | API 기능 |
|---------|---------|
| [CreateBackup](/document/api/236/15844) | 데이터베이스 백업 생성 |
| [DeleteBackup](/document/api/236/15841) | 데이터베이스 백업 삭제 |
| [DescribeBackupConfig](/document/api/236/15837) | 데이터베이스 구성 정보 조회 |
| [DescribeBackupDatabases](/document/api/236/15840) | 백업 데이터베이스 리스트 조회 |
| [DescribeBackupTables](/document/api/236/15846) | 지정 데이터베이스의 백업 데이터 테이블 조회 |
| [DescribeBackups](/document/api/236/15842) | 백업 로그 조회 |
| [DescribeBinlogs](/document/api/236/15843) | 이진 로그 조회 |
| [DescribeSlowLogs](/document/api/236/15845) | 슬로우 로그 조회 |
| [ModifyBackupConfig](/document/api/236/15839) | 데이터베이스 백업 구성 수정 |

## 보안 그룹 관련 API

| API 이름 | API 기능 |
|---------|---------|
| [AssociateSecurityGroups](/document/api/236/15852) | 보안 그룹에 클라우드 리소스 배치 바인딩 |
| [DescribeDBSecurityGroups](/document/api/236/15854) | 인스턴스 보안 그룹 정보 조회 |
| [DescribeProjectSecurityGroups](/document/api/236/15850) | 프로젝트 보안 그룹 정보 조회 |
| [DisassociateSecurityGroups](/document/api/236/15851) | 보안 그룹에서 클라우드 리소스 배치 언바인딩 |
| [ModifyDBInstanceSecurityGroups](/document/api/236/15853) | 데이터베이스 보안 그룹 수정 |

## 인스턴스 관련 API

| API 이름 | API 기능 |
|---------|---------|
| [CloseWanService](/document/api/236/15863) | 인스턴스 공중망 액세스 종료 |
| [CreateDBInstance](/document/api/236/15871) | 데이터베이스 인스턴스(연/월정액 요금제) 생성 |
| [CreateDBInstanceHour](/document/api/236/15865) | 데이터베이스 인스턴스(사용량 기반 요금제) 생성 |
| [DescribeDBInstanceCharset](/document/api/236/15866) | 데이터베이스 인스턴스의 문자 집합 조회 |
| [DescribeDBInstanceConfig](/document/api/236/17491) | 데이터베이스 인스턴스의 구성 정보 조회 |
| [DescribeDBInstanceGTID](/document/api/236/15862) | 데이터베이스 인스턴스의 GTID 활성화 여부 조회 |
| [DescribeDBInstanceRebootTime](/document/api/236/15874) | 데이터베이스 인스턴스의 다시 시작 예상 시간 조회 |
| [DescribeDBInstances](/document/api/236/15872) | 인스턴스 리스트 조회 |
| [DescribeDBPrice](/document/api/236/18566) | 데이터베이스 가격 조회 |
| [DescribeDBSwitchRecords](/document/api/236/17490) | ㅍ 전환 기록 조회 |
| [DescribeDBZoneConfig](/document/api/236/17229) | 데이터베이스 판매 가능 사양 획득 |
| [DescribeTagsOfInstanceIds](/document/api/236/32666) | 인스턴스에 바인딩된 tag 획득 |
| [InitDBInstances](/document/api/236/15873) | 새로운 인스턴스 초기화 |
| [InquiryPriceUpgradeInstances](/document/api/236/32665) | 데이터베이스 업그레이드 가격 조회 |
| [IsolateDBInstance](/document/api/236/15869) | 데이터베이스 인스턴스 격리 |
| [ModifyAutoRenewFlag](/document/api/236/19652) | 데이터베이스 인스턴스의 자동 갱신 플래그 수정 |
| [ModifyDBInstanceName](/document/api/236/15877) | 데이터베이스 인스턴스 이름 수정 |
| [ModifyDBInstanceProject](/document/api/236/15868) | 데이터베이스 인스턴스의 소속 프로젝트 수정 |
| [ModifyDBInstanceVipVport](/document/api/236/15867) | 데이터베이스 인스턴스의 IP 및 포트 번호 수정 |
| [ModifyInstanceTag](/document/api/236/32664) | 인스턴스 태그 수정 |
| [OpenDBInstanceGTID](/document/api/236/17489) | 인스턴스의 GTID 사용 |
| [OpenWanService](/document/api/236/15875) | 인스턴스 공중망 접근 활성화 |
| [RenewDBInstance](/document/api/236/30160) | 데이터베이스 인스턴스 갱신 |
| [RestartDBInstances](/document/api/236/17488) | 인스턴스 다시 시작 |
| [SwitchForUpgrade](/document/api/236/15864) | 전환하여 새로운 인스턴스 액세스 |
| [UpgradeDBInstance](/document/api/236/15876) | 데이터베이스 인스턴스 업그레이드 |
| [UpgradeDBInstanceEngineVersion](/document/api/236/15870) | 인스턴스 버전 업그레이드 |

## 데이터 가져오기 관련 API

| API 이름 | API 기능 |
|---------|---------|
| [CreateDBImportJob](/document/api/236/15858) | 데이터 가져오기 태스크 생성 |
| [DescribeDBImportRecords](/document/api/236/15856) | 데이터베이스 가져오기 태스크 기록 조회 |
| [DescribeUploadedFiles](/document/api/236/30161) | SQL 파일 가져오기 리스트 조회 |
| [StopDBImportJob](/document/api/236/15857) | 데이터 가져오기 태스크 종료 |

## 데이터베이스 관련 API

| API 이름 | API 기능 |
|---------|---------|
| [DescribeDatabases](/document/api/236/17493) | 데이터베이스 조회 |
| [DescribeTables](/document/api/236/18727) | 데이터베이스 테이블 조회 |

## 모니터링 관련 API

| API 이름 | API 기능 |
|---------|---------|
| [DescribeDeviceMonitorInfo](/document/api/236/32668) | 물리적 기기 모니터링 정보 |

## 계정 관련 API

| API 이름 | API 기능 |
|---------|---------|
| [CreateAccounts](/document/api/236/17502) | 데이터베이스 계정 생성 |
| [DeleteAccounts](/document/api/236/17501) | 데이터베이스 계정 삭제 |
| [DescribeAccountPrivileges](/document/api/236/17500) | 데이터베이스 계정 권한 정보 조회 |
| [DescribeAccounts](/document/api/236/17499) | 데이터베이스의 모든 계정 정보 조회 |
| [DescribeSupportedPrivileges](/document/api/236/32825) | 데이터베이스 인스턴스 지원 권한 정보 조회 |
| [ModifyAccountDescription](/document/api/236/17498) | 데이터베이스 인스턴스 계정의 비고 정보 수정 |
| [ModifyAccountPassword](/document/api/236/17497) | 데이터베이스 인스턴스 계정 비밀번호 수정 |
| [ModifyAccountPrivileges](/document/api/236/17496) | 데이터베이스 인스턴스 계정의 권한 수정 |
| [VerifyRootAccount](/document/api/236/17495) | root 계정 권한 인증 |


