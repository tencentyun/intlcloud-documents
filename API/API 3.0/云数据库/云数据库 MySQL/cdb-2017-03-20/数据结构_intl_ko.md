## Account

데이터베이스 계정 정보

다음 API에 참조됨: CreateAccounts, DeleteAccounts, ModifyAccountDescription, ModifyAccountPassword, ModifyAccountPrivileges.

| 이름 | 유형 | 필수 항목 여부 | 설명 |
|------|------|----------|------|
| User | String | 예 | 새 계정의 이름 |
| Host | String | 예 | 새 계정의 도메인 이름 |

## AccountInfo

계정 세부 정보

다음 API에 참조됨: DescribeAccounts.

| 이름 | 유형 | 설명 |
|------|------|-------|
| Notes | String | 계정 비고 정보 |
| Host | String | 계정의 도메인 이름 |
| User | String | 계정의 이름 |
| ModifyTime | Timestamp | 계정 정보 수정 시간 |
| ModifyPasswordTime | Timestamp | 비밀번호 수정 시간 |
| CreateTime | Timestamp | 계정의 생성 시간 |

## BackupConfig

ECDB 두 번째 슬레이브 데이터베이스 구성 정보, ECDB 인스턴스에만 이 필드가 있습니다.

다음 API에 참조됨: DescribeDBInstanceConfig.

| 이름 | 유형 | 설명 |
|------|------|-------|
| ReplicationMode | String | 두 번째 슬레이브 데이터베이스 복사 방식, 가능한 반환값: async-비동기화, semisync-반동기화 |
| Zone | String | 두 번째 슬레이브 데이터베이스 가용 영역의 정식 이름, 예: ap-shanghai-1. |
| Vip | String | 두 번째 슬레이브 데이터베이스의 IP 주소 |
| Vport | String | 두 번째 슬레이브 데이터베이스 접근 포트 |

## BackupInfo

백업 세부 정보

다음 API에 참조됨: DescribeBackups.

| 이름 | 유형 | 설명 |
|------|------|-------|
| Name | String | 백업 파일 이름 |
| Size | Integer | 백업 파일 크기, 단위: 바이트 |
| Date | String | 백업 스냅샷, 시간 형식: 2016-03-17 02:10:37 |
| IntranetUrl | String | 사설망 다운로드 주소 |
| InternetUrl | String | 공중망 다운로드 주소 |
| Type | String | 로그 구체적 유형, 가능한 값: logic - 로직 콜드 백업, physical - 물리적 콜드 백업 |
| BackupId | Integer | 백업 서브 태스크 ID, 백업 파일 삭제 시 사용 |
| Status | String | 백업 태스크 상태 |
| FinishTime | String | 백업 태스크의 완료 시간 |
| Creator | String | 백업의 생성자, 가능한 값: SYSTEM - 시스템 생성, Uin - 개시자 Uin 값 |

## BinlogInfo

이진 로그 정보

다음 API에 참조됨: DescribeBinlogs.

| 이름 | 유형 | 설명 |
|------|------|-------|
| Name | String | 백업 파일 이름 |
| Size | Integer | 백업 파일 크기, 단위: 바이트 |
| Date | Timestamp | 백업 스냅샷 시간, 시간 형식: 2016-03-17 02:10:37 |
| IntranetUrl | String | 사설망 다운로드 주소 |
| InternetUrl | String | 공중망 다운로드 주소 |
| Type | String | 로그 구체적 유형, 가능한 값: binlog - 이진 로그 |

## ColumnPrivilege

열 권한 정보

다음 API에 참조됨: DescribeAccountPrivileges, ModifyAccountPrivileges.

| 이름 | 유형 | 필수 항목 여부 | 설명 |
|------|------|----------|------|
| Database | String | 예 | 데이터베이스 이름 |
| Database | String | 예 | 데이터베이스 테이블 이름 |
| Column | String | 예 | 데이터베이스 열 이름 |
| Privileges | Array of String | 예 | 권한 정보 |

## DBSwitchInfo

데이터베이스 전환 기록

다음 API에 참조됨: DescribeDBSwitchRecords.

| 이름 | 유형 | 설명 |
|------|------|-------|
| SwitchTime | Timestamp | 전환 시간, 형식: 2017-09-03 01:34:31 |
| SwitchType | String | 전환 유형, 가능한 반환값: TRANSFER - 데이터 마이그레이션, MASTER2SLAVE - 마스터/슬레이브 스위칭, RECOVERY - 마스터/슬레이브 복구 |

## DatabaseName

데이터베이스 테이블 이름

다음 API에 참조됨: DescribeBackupDatabases.

| 이름 | 유형 | 설명 |
|------|------|-------|
| DatabaseName | String | 데이터베이스 테이블 이름 |

## DatabasePrivilege

데이터베이스 권한

다음 API에 참조됨: DescribeAccountPrivileges, ModifyAccountPrivileges.

| 이름 | 유형 | 필수 항목 여부 | 설명 |
|------|------|----------|------|
| Privileges | Array of String | 예 | 권한 정보 |
| Database | String | 예 | 데이터베이스 이름 |

## DeviceCpuInfo

 CPU 부하

다음 API에 참조됨: DescribeDeviceMonitorInfo.

| 이름 | 유형 | 설명 |
|------|------|-------|
| Rate | Array of [DeviceCpuRateInfo](#DeviceCpuRateInfo) | 인스턴스 CPU 평균 사용률 |
| Load | Array of Integer | 인스턴스 CPU 모니터링 데이터 |

## DeviceCpuRateInfo

인스턴스 CPU 평균 사용률

다음 API에 참조됨: DescribeDeviceMonitorInfo.

| 이름 | 유형 | 설명 |
|------|------|-------|
| CpuCore | Integer | CPU 코어 번호 |
| Rate | Array of Integer | CPU 사용률 |

## DeviceDiskInfo

인스턴스 디스크 모니터링 데이터

다음 API에 참조됨: DescribeDeviceMonitorInfo.

| 이름 | 유형 | 설명 |
|------|------|-------|
| IoRatioPerSec | Array of Integer | 초당 평균 I/O 조작에 사용되는 시간의 백분율 |
| IoWaitTime | Array of Integer | 초당 평균 I/O 조작 백업의 대기 시간(단위는 ms)*100, . 예: 해당 값이 201이라면, 평균 매회 I/O 조작 대기 시간은 다음과 같이 나타냄. 201/100=2.1ms |
| Read | Array of Integer | 디스크 초당 평균 읽기 조작 완료 회수 총합*100. 예: 해당 값이 2002라면, 디스크 초당 평균 읽기 조작 완료 횟수는 다음과 같이 나타냄. 2002/100=20.2회 |
| Write | Array of Integer | 디스크 초당 평균 쓰기 조작 완료 회수 총합*100. 예: 해당 값이 30001이라면, 디스크 초당 평균 읽기 조작 완료 회수는 다음과 같이 나타냄. 30001/100=300.01회 |

## DeviceMemInfo

인스턴스의 물리적 기기 메모리 모니터링 정보

다음 API에 참조됨: DescribeDeviceMonitorInfo.

| 이름 | 유형 | 설명 |
|------|------|-------|
| Total | Array of Integer | 총 메모리 크기. free 명령 중 Mem: 행 total의 값, 단위: KB |
| Used | Array of Integer | 사용된 메모리. free 명령 중 Mem: 행 used의 값, 단위: KB |

## DeviceNetInfo

인스턴스 소재 물리적 기기 네트워크 모니터링 정보

다음 API에 참조됨: DescribeDeviceMonitorInfo.

| 이름 | 유형 | 설명 |
|------|------|-------|
| Conn | Array of Integer | tcp 연결 수 |
| PackageIn | Array of Integer | ENI 인바운드 패킷 |
| PackageOut | Array of Integer | ENI 아웃바운드 패킷 |
| FlowIn | Array of Integer | 인바운드 트래픽, 단위: KB |
| FlowOut | Array of Integer | 아웃바운드 트래픽, 단위: KB |

## DrInfo

재해 복구 인스턴스 정보

다음 API에 참조됨: DescribeDBInstances.

| 이름 | 유형 | 설명 |
|------|------|-------|
| Status | Integer | 재해 복구 인스턴스 상태 |
| Zone | String | 가용 영역 정보 |
| InstanceId | String | 인스턴스 ID |
| Region | String | 지역 정보 |
| SyncStatus | Integer | 인스턴스 동기화 상태 |
| InstanceName | String | 인스턴스 이름 |
| InstanceType | Integer | 인스턴스 유형 |

## ImportRecord

가져오기 태스크 기록

다음 API에 참조됨: DescribeDBImportRecords.

| 이름 | 유형 | 설명 |
|------|------|-------|
| Status | Integer | 상태 값 |
| Code | Integer | 상태 값 |
| CostTime | Integer | 실행 시간 |
| InstanceId | String | 인스턴스 ID |
| WorkId | String | 백 엔드 태스크 ID |
| FileName | String | 파일 이름 가져오기 |
| Process | Integer | 실행 진행도 |
| CreateTime | Timestamp | 태스크 생성 시간 |
| FileSize | String | 파일 크기 |
| Message | String | 태스크 실행 정보 |
| JobId | Integer | 태스크 ID |
| DbName | String | 데이터베이스 테이블 이름 가져오기 |
| AsyncRequestId | String | 비동기화 태스크의 요청 ID |

## Inbound

보안 그룹 인바운드 규칙

다음 API에 참조됨: DescribeDBSecurityGroups, DescribeProjectSecurityGroups.

| 이름 | 유형 | 설명 |
|------|------|-------|
| Action | String | 전략, ACCEPT 또는 DROP |
| CidrIp | String | 소스 IP 또는 IP 주소 범위, 예: 192.168.0.0/16 |
| PortRange | String | 포트 |
| IpProtocol | String | 네트워크 프로토콜, udp, tcp 등 지원 |
| Dir | String | 규칙에 규정된 방향, 인바운드 규칙은 INPUT |

## InstanceInfo

인스턴스 세부 정보

다음 API에 참조됨: DescribeDBInstances.

| 이름 | 유형 | 설명 |
|------|------|-------|
| WanStatus | Integer | 공중망 상태, 가능한 반환값: 0 - 공중망 비활성화, 1-공중망 활성화, 2-공중망 종료됨 |
| Zone | String | 가용 영역 정보 |
| InitFlag | Integer | 초기화 표시, 가능한 반환값: 0-초기화하지 않음, 1-초기화됨 |
| RoVipInfo | [RoVipInfo](#RoVipInfo) | 읽기 전용 vip 정보. 이 필드는 읽기 전용 인스턴스 액세스가 단독 활성화된 읽기 전용 인스턴스에서만 사용할 수 있습니다.
| Memory | Integer | 메모리 용량, 단위는 MB |
| Status | Integer | 인스턴스 상태, 가능한 반환값: 0-생성 중, 1-실행 중, 4-격리 중, 5-격리됨 |
| VpcId | Integer | VPC ID, 예:51102 |
| SlaveInfo | [SlaveInfo](#SlaveInfo) | 슬레이브 정보 |
| InstanceId | String | 인스턴스 ID |
| Volume | Integer | 디스크 용량, 단위는 GB |
| AutoRenew | Integer | 자동 갱신 표시, 가능한 반환값: 0-자동 갱신 비활성화, 1-자동 갱신 활성화, 2-자동 갱신 종료됨 |
| ProtectMode | Integer | 데이터 복제 방식 |
| RoGroups | Array of [RoGroup](#RoGroup) | 읽기 전용 그룹 세부 정보 |
| SubnetId | Integer | 서브넷 ID, 예:2333 |
| InstanceType | Integer | 인스턴스 유형, 가능한 반환값: 1-마스터 인스턴스, 2-재해 복구 인스턴스, 3-읽기 전용 인스턴스 |
| ProjectId | Integer | 프로젝트 ID |
| Region | String | 지역 정보 |
| DeadlineTime | Timestamp | 인스턴스 만료 기간 |
| DeployMode | Integer | 가용 영역 배포 방식 |
| TaskStatus | Integer | 인스턴스 태스크 상태 |
| MasterInfo | [MasterInfo](#MasterInfo) | 마스터 인스턴스 세부 정보 |
| DeviceType | String | 인스턴스 유형, 가능한 반환값: "HA"- 고가용 버전, “BASIC”-기본 버전 |
| EngineVersion | String | 커널 버전 |
| InstanceName | String | 인스턴스 이름 |
| DrInfo | Array of [DrInfo](#DrInfo) | 재해 복구 인스턴스 세부 정보 |
| WanDomain | String | 공중망 도메인 이름 |
| WanPort | Integer | 공중망 포트 번호 |
| PayType | Integer | 지불 유형, 가능한 반환값: 0-연/월정액 요금제, 1-사용량 기반 요금제 |
| CreateTime | String | 인스턴스 생성 시간 |
| Vip | String | 인스턴스 IP |
| Vport | Integer | 포트 번호 |
| CdbError | Integer | 플래그 잠금 여부 |
| UniqVpcId | String | VPC 설명자, 예:“vpc-5v8wn9mg” |
| UniqSubnetId | String | 서브넷 설명자, 예: “subnet-1typ0s7d” |
| PhysicalId | String | 물리적 ID |
| Cpu | Integer | 코어 수 |
| Qps | Integer | 초당 조회 수 |
| ZoneName | String | 가용 영역 한글 이름 |

## InstanceRebootTime

인스턴스의 다시 시작 예상 시간

다음 API에 참조됨: DescribeDBInstanceRebootTime.

| 이름 | 유형 | 설명 |
|------|------|-------|
| InstanceId | String | 인스턴스 ID, 형식 예: cdb-c1nl9rpv, TencentDB 콘솔 페이지에 표시된 인스턴스 ID와 동일합니다 |
| TimeInSeconds | Integer | 다시 시작 예상 시간 |

## InstanceRollbackRangeTime

인스턴스 롤백 가능 시간 범위

다음 API에 참조됨: DescribeRollbackRangeTime.

| 이름 | 유형 | 설명 |
|------|------|-------|
| Code | Integer | 데이터베이스 오류 코드 조회 |
| Message | String | 데이터베이스 오류 정보 조회 |
| InstanceId | String | 인스턴스 ID 리스트, 단일 인스턴스 ID의 형식 예: cdb-c1nl9rpv, TencentDB 콘솔 페이지에 표시된 인스턴스 ID와 동일합니다 |
| Times | Array of [RollbackTimeRange](#RollbackTimeRange) | 롤백 가능한 시간 범위 |

## MasterInfo

마스터 인스턴스 정보

다음 API에 참조됨: DescribeDBInstances.

| 이름 | 유형 | 설명 |
|------|------|-------|
| Region | String | 지역 정보 |
| RegionId | Integer | 지역 ID |
| ZoneId | Integer | 가용 영역 ID |
| Zone | String | 가용 영역 정보 |
| InstanceId | String | 인스턴스 ID |
| ResourceId | String | 인스턴스 긴 ID |
| Status | Integer | 인스턴스 상태 |
| InstanceName | String | 인스턴스 이름 |
| InstanceType | Integer | 인스턴스 유형 |
| TaskStatus | Integer | 태스크 상태 |
| Memory | Integer | 메모리 용량 |
| Volume | Integer | 디스크 용량 |
| DeviceType | String | 인스턴스 모델 |
| Qps | Integer | 매초 조회 수 |
| VpcId | Integer | VPC ID |
| SubnetId | Integer | 서브넷 ID |
| ExClusterId | String | 독점적 클러스터 ID |
| ExClusterName | String | 독점적 클러스터 이름 |

## Outbound

보안 그룹 아웃바운드 규칙

다음 API에 참조됨: DescribeDBSecurityGroups, DescribeProjectSecurityGroups.

| 이름 | 유형 | 설명 |
|------|------|-------|
| Action | String | 전략, ACCEPT 또는 DROP |
| CidrIp | String | 대상 IP 또는 IP 주소 범위, 예: 172.16.0.0/12 |
| PortRange | String | 포트 또는 포트 범위 |
| IpProtocol | String | 네트워크 프로토콜, udp, tcp 등 지원 |
| Dir | String | 규칙에 규정된 방향, 인바운드 규칙은 OUTPUT |

## ParamInfo

인스턴스 매개변수 정보

다음 API에 참조됨: CreateDBInstance, CreateDBInstanceHour, InitDBInstances.

| 이름 | 유형 | 필수 항목 여부 | 설명 |
|------|------|----------|------|
| Name | String | 예 | 매개변수 이름 |
| Value | String | 예 | 매개변수 값 |

## ParamRecord

매개변수 수정 기록

다음 API에 참조됨: DescribeInstanceParamRecords.

| 이름 | 유형 | 설명 |
|------|------|-------|
| InstanceId | String | 인스턴스 ID |
| ParamName | String | 매개변수 이름 |
| OldValue | String | 매개변수 수정하기 전의 값 |
| NewValue | String | 매개변수 수정한 후의 값 |
| IsSucess | Boolean | 매개변수 수정 성공 여부 |
| ModifyTime | String | 수정 시간 |

## ParamTemplateInfo

매개변수 템플릿 정보

다음 API에 참조됨: DescribeParamTemplates.

| 이름 | 유형 | 설명 |
|------|------|-------|
| TemplateId | Integer | 매개변수 템플릿 ID |
| Name | String | 매개변수 템플릿 이름 |
| Description | String | 매개변수 템플릿 설명 |
| EngineVersion | String | 인스턴스 엔진 버전 |

## Parameter

데이터베이스 인스턴스 매개변수

다음 API에 참조됨: CreateParamTemplate, ModifyInstanceParam, ModifyParamTemplate.

| 이름 | 유형 | 필수 항목 여부 | 설명 |
|------|------|----------|------|
| Name | String | 예 | 매개변수 이름 |
| CurrentValue | String | 예 | 매개변수 값 |

## ParameterDetail

인스턴스 매개변수의 상세 설명

다음 API에 참조됨: DescribeDefaultParams, DescribeInstanceParams, DescribeParamTemplateInfo.

| 이름 | 유형 | 설명 |
|------|------|-------|
| Name | String | 매개변수 이름 |
| ParamType | String | 매개변수 유형 |
| Default | String | 매개변수 기본값 |
| Description | String | 매개변수 설명 |
| CurrentValue | String | 매개변수 현재 값 |
| NeedReboot | Integer | 매개변수 수정 후, 매개변수가 적용되려면 데이터베이스를 다시 시작해야 하는지 여부. 가능한 값: 0-다시 시작 불필요, 1-다시 시작 필요 |
| Max | Integer | 매개변수 허용 최대값 |
| Min | Integer | 매개변수 허용 최소값 |
| EnumValue | Array of String | 매개변수의 선택 가능 열거 값. 비열거형의 경우 비워둡니다. |

## RegionSellConf

지역 판매 구성

다음 API에 참조됨: DescribeDBZoneConfig.

| 이름 | 유형 | 설명 |
|------|------|-------|
| RegionName | String | 지역 한글 이름 |
| Area | String | 소속 구역 |
| IsDefaultRegion | Integer | 기본 지역인지의 여부 |
| Region | String | 지역 이름 |
| ZonesConf | Array of [ZoneSellConf](#ZoneSellConf) | 가용 영역 판매 구성 |

## RoGroup

읽기 전용 그룹 매개변수

다음 API에 참조됨: CreateDBInstance, CreateDBInstanceHour, DescribeDBInstances.

| 이름 | 유형 | 필수 항목 여부 | 설명 |
|------|------|----------|------|
| RoGroupMode | String | 예 | 읽기 전용 그룹 모드, 선택 가능 값: alone-시스템이 읽기 전용 그룹 자동 할당, allinone-읽기 전용 그룹 새로 만들기, join-기존 읽기 전용 그룹 사용 |
| RoGroupId | String | 아니요 | 읽기 전용 그룹 ID |
| RoGroupName | String | 아니요 | 읽기 전용 그룹 이름 |
| RoOfflineDelay | Integer | 아니요 | 지연 제한 초과 제거 기능 사용 여부, 해당 기능 사용 후, 읽기 전용 인스턴스와 마스터 인스턴스의 지연이 지연 임계값을 초과하면 읽기 전용 인스턴스가 격리됩니다. 선택 가능 값: 1-사용, 0-미사용 |
| RoMaxDelayTime | Integer | 아니요 | 지연 임계값 |
| MinRoInGroup | Integer | 아니요 | 최소 인스턴스 보관 개수, 읽기 전용 인스턴스의 구매 수량이 설정 수량보다 작으면 삭제하지 않습니다. |
| WeightMode | String | 아니요 | 읽기/쓰기 가중치 할당 모드, 가능한 값: system-시스템 자동 할당, custom-사용자 지정 |
| Weight | Integer | 아니요 | 가중치 |
| RoInstances | Array of [RoInstanceInfo](#RoInstanceInfo) | 아니요 | 읽기 전용 그룹의 읽기 전용 인스턴스 세부 정보 |
| Vip | String | 아니요 | 읽기 전용 그룹의 사설 IP |
| Vport | Integer | 아니요 | 읽기 전용 그룹의 사설망 포트 번호 |

## RoInstanceInfo

RO 인스턴스의 세부 정보

다음 API에 참조됨: CreateDBInstance, CreateDBInstanceHour, DescribeDBInstances.

| 이름 | 유형 | 설명 |
|------|------|-------|
| MasterInstanceId | String | RO 그룹에 해당하는 마스터 인스턴스의 ID |
| RoStatus | String | RO 인스턴스의 RO 그룹 내에서의 상태, 가능한 값: online-온라인, offline-오프라인 |
| OfflineTime | String | RO 인스턴스의 RO 그룹 내에서 마지막 오프라인 시간 |
| Weight | Integer | RO 인스턴스의 RO 그룹 내에서 가중치 |
| Region | String | RO 인스턴스 소재 지역, 예: ap-shanghai |
| Zone | String | RO 가용 영역의 정식 이름, 예: ap-shanghai-1 |
| InstanceId | String | RO 인스턴스 ID, 형식 예: cdbro-c1nl9rpv |
| Status | Integer | RO 인스턴스 상태, 가능한 반환값: 0-생성 중, 1-실행 중, 4-삭제 중 |
| InstanceType | Integer | 인스턴스 유형, 가능한 반환값: 1-마스터 인스턴스, 2-재해 복구 인스턴스, 3-읽기 전용 인스턴스 |
| InstanceName | String | RO 인스턴스 이름 |
| HourFeeStatus | Integer | 사용량 기반 요금제 상태, 가능한 값: 1-정상, 2-체납 |
| TaskStatus | Integer | RO 인스턴스 태스크 상태, 가능한 반환값: <br>0-태스크 없음<br>1-업그레이드 중<br>2-데이터 가져오기 중<br>3-슬레이브 활성화 중<br>4-공중망 접근 활성화 중<br>5-배치 작업 실행 중<br>6-롤백 중<br>7-공중망 접근 종료 중<br>8-비밀번호 수정 중<br>9-인스턴스 이름 수정 중<br>10-다시 시작 중<br>12-자체 생성 데이터베이스 마이그레이션 중<br>13-데이터베이스 테이블 삭제 중<br>14-재해 복구 인스턴스 동기화 생성 중 |
| Memory | Integer | RO 인스턴스 메모리 크기, 단위: MB |
| Volume | Integer | RO 인스턴스 디스크 크기, 단위: GB |
| Qps | Integer | 매회 조회 수 |
| Vip | String | RO 인스턴스의 사설 IP |
| Vport | Integer | RO 인스턴스 접근 포트 |
| VpcId | Integer | RO 인스턴스 소재 VPC ID |
| SubnetId | Integer | RO 인스턴스 소재 VPC 서브넷 ID |
| DeviceType | String | RO 인스턴스 사양 설명, 현재 선택 가능한 값 CUSTOM |
| EngineVersion | String | RO 인스턴스 데이터베이스 엔진 버전, 가능한 반환값: 5.1, 5.5, 5.6 및 5.7 |
| DeadlineTime | String | RO 인스턴스 만료 기간, 시간 형식: yyyy-mm-dd hh:mm:ss, 인스턴스가 사용량 기반 요금제인 경우 이 필드의 값은 0000-00-00 00:00:00입니다 |
| PayType | Integer | RO 인스턴스 요금제, 가능한 반환값: 0-연/월정액 요금제, 1-사용량 기반 요금제, 2-월별 결산 후불제 |

## RoVipInfo

읽기 전용 vip 정보

다음 API에 참조됨: DescribeDBInstances.

| 이름 | 유형 | 설명 |
|------|------|-------|
| RoVipStatus | Integer | 읽기 전용 vip 상태 |
| RoSubnetId | Integer | 읽기 전용 vip의 서브넷 |
| RoVpcId | Integer | 읽기 전용 vip의 VPC |
| RoVport | Integer | 읽기 전용 vip의 포트 번호 |
| RoVip | String | 읽기 전용 vip |

## RollbackDBName

롤백에 사용하는 데이터베이스 이름

다음 API에 참조됨: StartBatchRollback.

| 이름 | 유형 | 필수 항목 여부 | 설명 |
|------|------|----------|------|
| DatabaseName | String | 예 | 롤백 전의 원래 데이터베이스 이름 |
| NewDatabaseName | String | 예 | 롤백 후의 새로운 데이터베이스 이름 |

## RollbackInstancesInfo

롤백에 사용되는 인스턴스 세부 정보

다음 API에 참조됨: StartBatchRollback.

| 이름 | 유형 | 필수 항목 여부 | 설명 |
|------|------|----------|------|
| InstanceId | String | 예 | 데이터베이스 인스턴스 ID |
| Strategy | String | 예 | 롤백 전략. 선택 가능 값: table, db, full. 기본값은 full입니다. table-긴급 롤백 모드, 선택한 테이블 수준의 백업 및 binlog만 가져오며, 크로스 테이블 작업이 있고, 관련 테이블이 동시에 선택되어 있지 않으면 롤백이 실패합니다. 해당 모드에서 Database는 반드시 비어 있어야 합니다. db-빠른 모드, 선택한 데이터베이스 수준의 백업 및 binlog만 가져오며, 크로스 테이블 작업이 있고 관련 데이터베이스가 동시에 선택되어 있지 않으면 롤백이 실패합니다. full-일반 롤백 모드, 전체 인스턴스의 백업 및 binlog를 가져오며, 속도가 비교적 느립니다. |[AD1]
| RollbackTime | String | 예 | 데이터베이스 롤백 시간, 시간 형식: yyyy-mm-dd hh:mm:ss |
| Databases | Array of [RollbackDBName](#RollbackDBName) | 아니요 | 롤백 대기 중인 데이터베이스 테이블 정보, 전체 데이터베이스 롤백을 나타냅니다 |
| Tables | Array of [RollbackTables](#RollbackTables) | 아니요 | 롤백 대기 중인 데이터베이스 테이블 정보, 테이블별 롤백을 나타냅니다 |

## RollbackTableName

롤백에 사용하는 데이터베이스 테이블 이름

다음 API에 참조됨: StartBatchRollback.

| 이름 | 유형 | 필수 항목 여부 | 설명 |
|------|------|----------|------|
| TableName | String | 예 | 롤백 전의 원래 데이터베이스 테이블 이름 |
| NewTableName | String | 예 | 롤백 후의 새로운 데이터베이스 테이블 이름 |

## RollbackTables

롤백에 사용하는 데이터베이스 테이블 세부 정보

다음 API에 참조됨: StartBatchRollback.

| 이름 | 유형 | 필수 항목 여부 | 설명 |
|------|------|----------|------|
| Database | String | 예 | 데이터베이스 이름 |
| Table | Array of [RollbackTableName](#RollbackTableName) | 예 | 데이터베이스 테이블 세부 정보 |

## RollbackTimeRange

롤백 가능 시간 범위

다음 API에 참조됨: DescribeRollbackRangeTime.

| 이름 | 유형 | 설명 |
|------|------|-------|
| Begin | String | 인스턴스 롤백 가능 시작 시간, 시간 형식: 2016-10-29 01:06:04 |
| End | String | 인스턴스 롤백 가능 종료 시간, 시간 형식: 2016-11-02 11:44:47 |

## SecurityGroup

보안 그룹 세부 정보

다음 API에 참조됨: DescribeDBSecurityGroups, DescribeProjectSecurityGroups.

| 이름 | 유형 | 설명 |
|------|------|-------|
| ProjectId | Integer | 프로젝트 ID |
| CreateTime | String | 생성 시간, 시간 형식: yyyy-mm-dd hh:mm:ss |
| Inbound | Array of [Inbound](#Inbound) | 인바운드 규칙 |
| Outbound | Array of [Outbound](#Outbound) | 아웃바운드 규칙 |
| SecurityGroupId | String | 보안 그룹 ID |
| SecurityGroupName | String | 보안 그룹 이름 |
| SecurityGroupRemark | String | 보안 그룹 비고 |

## SellConfig

판매 구성 세부 정보

다음 API에 참조됨: DescribeDBZoneConfig.

| 이름 | 유형 | 설명 |
|------|------|-------|
| Device | String | 장치 유형 |
| Type | String | 판매 사양 설명 |
| CdbType | String | 인스턴스 유형 |
| Memory | Integer | 메모리 크기, 단위는 MB |
| Cpu | Integer | CPU 코어 수 |
| VolumeMin | Integer | 디스크 최소 사양, 단위는 GB |
| VolumeMax | Integer | 디스크 최대 사양, 단위는 GB |
| VolumeStep | Integer | 디스크 진행 속도, 단위는 GB |
| Connection | Integer | 링크 수 |
| Qps | Integer | 초당 조회 수 |
| Iops | Integer | 매초 IO 수량 |
| Info | String | 적용 시나리오 설명 |
| Status | Integer | 상태 값 |

## SellType

판매 인스턴스 유형

다음 API에 참조됨: DescribeDBZoneConfig.

| 이름 | 유형 | 설명 |
|------|------|-------|
| TypeName | String | 판매 인스턴스 이름 |
| EngineVersion | Array of String | 커널 버전 번호 |
| Configs | Array of [SellConfig](#SellConfig) | 판매 사양 상세 구성 |

## SlaveConfig

슬레이브 데이터베이스의 구성 정보

다음 API에 참조됨: DescribeDBInstanceConfig.

| 이름 | 유형 | 설명 |
|------|------|-------|
| ReplicationMode | String | 슬레이브 데이터베이스 복사 방식, 가능한 반환값: async-비동기화, semisync-반동기화 |
| Zone | String | 슬레이브 데이터베이스 가용 영역의 정식 이름, 예: ap-shanghai-1 |

## SlaveInfo

슬레이브 정보

다음 API에 참조됨: DescribeDBInstances.

| 이름 | 유형 | 설명 |
|------|------|-------|
| First | [SlaveInstanceInfo](#SlaveInstanceInfo) | 첫 번째 슬레이브 정보 |
| Second | [SlaveInstanceInfo](#SlaveInstanceInfo) | 두 번째 슬레이브 정보 |

## SlaveInstanceInfo

슬레이브 정보

다음 API에 참조됨: DescribeDBInstances.

| 이름 | 유형 | 설명 |
|------|------|-------|
| Vport | Integer | 포트 번호 |
| Region | String | 지역 정보 |
| Vip | String | 가상 IP 정보 |
| Zone | String | 가용 영역 정보 |

## SlowLogInfo

슬로우 로그 세부 정보

다음 API에 참조됨: DescribeSlowLogs.

| 이름 | 유형 | 설명 |
|------|------|-------|
| Name | String | 백업 파일 이름 |
| Size | Integer | 백업 파일 크기, 단위: 바이트 |
| Date | Timestamp | 백업 스냅샷 시간, 시간 형식: 2016-03-17 02:10:37 |
| IntranetUrl | String | 사설망 다운로드 주소 |
| InternetUrl | String | 공중망 다운로드 주소 |
| Type | String | 로그 구체적 유형, 가능한 값: slowlog - 슬로우 로그 |

## SqlFileInfo

sql 파일 정보

다음 API에 참조됨: DescribeUploadedFiles.

| 이름 | 유형 | 설명 |
|------|------|-------|
| UploadTime | Timestamp | 업로드 시간 |
| UploadInfo | [UploadInfo](#UploadInfo) | 업로드 진행도 |
| FileName | String | 파일 이름 |
| FileSize | Integer | 파일 크기, 단위는 바이트 |
| IsUploadFinished | Integer | 업로드 완료 여부 표시, 선택 가능 값: 0 - 미완료, 1 - 완료됨 |
| FileId | String | 파일 ID |

## TableName

테이블 이름

다음 API에 참조됨: DescribeBackupTables.

| 이름 | 유형 | 설명 |
|------|------|-------|
| TableName | String | 테이블 이름 |

## TablePrivilege

데이터베이스 테이블 권한

다음 API에 참조됨: DescribeAccountPrivileges, ModifyAccountPrivileges.

| 이름 | 유형 | 필수 항목 여부 | 설명 |
|------|------|----------|------|
| Database | String | 예 | 데이터베이스 이름 |
| Database | String | 예 | 데이터베이스 테이블 이름 |
| Privileges | Array of String | 예 | 권한 정보 |

## TagInfo

태그 정보

다음 API에 참조됨: CreateDBInstance, CreateDBInstanceHour, ModifyInstanceTag.

| 이름 | 유형 | 설명 |
|------|------|-------|
| TagKey | String | 태그 키 |
| TagValue | Array of String | 태그 값 |

## TagInfoUnit

태그 정보 유닛

다음 API에 참조됨: DescribeTagsOfInstanceIds.

| 이름 | 유형 | 설명 |
|------|------|-------|
| TagKey | String | 태그 키 |
| TagValue | String | 태그 값 |

## TagsInfoOfInstance

인스턴스의 태그 정보

다음 API에 참조됨: DescribeTagsOfInstanceIds.

| 이름 | 유형 | 설명 |
|------|------|-------|
| InstanceId | String | 인스턴스 ID |
| Tags | Array of [TagInfoUnit](#TagInfoUnit) | 태그 정보 |

## UploadInfo

파일 업로드 설명

다음 API에 참조됨: DescribeUploadedFiles.

| 이름 | 유형 | 설명 |
|------|------|-------|
| AllSliceNum | Integer | 파일의 모든 조각 수량 |
| CompleteNum | Integer | 완료된 조각 수량 |

## ZoneConf

멀티 가용 영역 정보

다음 API에 참조됨: DescribeDBZoneConfig.

| 이름 | 유형 | 필수 항목 여부 | 설명 |
|------|------|----------|------|
| DeployMode | Array of Integer | 예 | 가용 영역 배포 방식, 가능한 값: 0-단일 가용 영역, 1-멀티 가용 영역 |
| MasterZone | Array of String | 예 | 마스터 인스턴스가 있는 가용 영역 |
| SlaveZone | Array of String | 예 | 인스턴스는 멀티 가용 영역 배치 시, 슬레이브 1이 있는 가용 영역 |
| BackupZone | Array of String | 예 | 인스턴스 멀티 가용 영역 배치 시, 슬레이브 2가 있는 가용 영역 |

## ZoneSellConf

가용 영역 판매 구성

다음 API에 참조됨: DescribeDBZoneConfig.

| 이름 | 유형 | 설명 |
|------|------|-------|
| Status | Integer | 가용 영역 상태. 가능한 반환값: 0-미런칭, 1-런칭, 2-개방, 3-판매 중지, 4-표시 안 함 |
| ZoneName | String | 가용 영역 한글 이름 |
| IsCustom | Boolean | 인스턴스 유형이 사용자 지정 유형인지 여부 |
| IsSupportDr | Boolean | 재해 복구 지원 여부 |
| IsSupportVpc | Boolean | VPC 지원 여부 |
| HourInstanceSaleMaxNum | Integer | 시간제 요금 계산 인스턴스 최대 판매 수량 |
| IsDefaultZone | Boolean | 기본 가용 영역인지 여부 |
| IsBm | Boolean | BM 영역인지 여부 |
| PayType | Array of String | 지원하는 지불 유형. 가능한 반환값: 0-연/월정액 요금제, 1-시간제, 2-후불제 |
| ProtectMode | Array of String | 데이터 복제 유형. 0-비동기화 복제, 1-반동기화 복제, 2-강제 동기화 복제 |
| Zone | String | 가용 영역 이름 |
| SellType | Array of [SellType](#SellType) | 판매 유형 인스턴스 배열 |
| ZoneConf | [ZoneConf](#ZoneConf) | 멀티 가용 영역 정보 |


[AD1]Database?
