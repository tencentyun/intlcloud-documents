## 1. API 설명

API 요청 도메인 이름: cdb.tencentcloudapi.com.

이 API(DescribeDBInstances)는 데이터베이스 인스턴스 리스트 조회에 사용합니다. 프로젝트 ID, 인스턴스 ID, 접근 주소, 인스턴스 상태 등 필터를 통한 인스턴스 필터링을 지원합니다. 마스터 인스턴스, 재해 복구 인스턴스 및 읽기 전용 인스턴스 정보 리스트 조회를 지원합니다.

기본적 API 요청 빈도 제한: 100회/초.

주의: 이 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 있고 서로 통하지 않아서, 공통 매개변수 Region이 금융 지역 도메인(예: ap-shanghai-fsi)일 경우, 금융 지역의 도메인 이름을 동시에 지정해야 하며, Region의 도메인과 일치시키는 것이 가장 좋습니다. 예: cdb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수 및 일부 공통 매개변수만 나열되며, 완전한 공통 매개변수 리스트는 [공통 요청 매개변수](/document/api/236/15833)를 참조하십시오.

| 매개변수 이름 | 필수 항목 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, 이 API 값: DescribeDBInstances |
| Version | 예 | String | 공통 매개변수, 이 API 선택 값: 2017-03-20 |
| Region | 아니요 | String | 공통 매개변수, 자세한 내용은 제품의 지원되는 [지역 리스트](/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오. |
| ProjectId | 아니요 | Integer | 프로젝트 ID, [프로젝트 리스트 조회](https://cloud.tencent.com/document/product/378/4400) API를 사용하여 프로젝트 ID를 조회할 수 있습니다. |
| InstanceTypes.N | 아니요 | Array of Integer | 인스턴스 유형, 선택 값: 1-마스터 인스턴스, 2-재해 복구 인스턴스, 3-읽기 전용 인스턴스 |
| Vips.N | 아니요 | Array of String | 인스턴스의 사설 IP 주소 |
| Status.N | 아니요 | Array of Integer | 인스턴스 상태, 가능한 값: 0-생성 중, 1-실행 중, 4-격리 중, 5-격리됨 |
| Offset | 아니요 | Integer | 오프셋, 기본값은 0입니다. |
| Limit | 아니요 | Integer | 1회 요청의 반환 수량, 기본값은 20, 최대값은 2000입니다. |
| SecurityGroupId | 아니요 | String | 보안 그룹 ID |
| PayTypes.N | 아니요 | Array of Integer | 지불 유형, 가능한 값: 0-연/월정액 요금제, 1-시간제 |
| InstanceNames.N | 아니요 | Array of String | 인스턴스 이름 |
| TaskStatus.N | 아니요 | Array of Integer | 인스턴스 태스크 상태, 선택 가능 값: <br>0-태스크 없음<br>1-업그레이드 중<br>2-데이터 가져오기 중<br>3-슬레이브 활성화 중<br>4-공중망 접근 활성화 중<br>5-배치 작업 실행 중<br>6-롤백 중<br>7-공중망 접근 종료 중<br>8-비밀번호 수정 중<br>9-인스턴스 이름 수정 중<br>10-다시 시작 중<br>12-자체 생성 데이터베이스 마이그레이션 중<br>13-데이터베이스 테이블 삭제 중<br>14-재해 복구 인스턴스 생성 동기화 중<br>15-업그레이드 전환 대기 중<br>16-업그레이드 전환 중<br>17-업그레이드 전환 완료 |
| EngineVersions.N | 아니요 | Array of String | 인스턴스 데이터베이스 엔진 버전, 선택 가능 값: 5.1, 5.5, 5.6 및 5.7 |
| VpcIds.N | 아니요 | Array of Integer | VPC ID |
| ZoneIds.N | 아니요 | Array of Integer | 가용 영역 ID |
| SubnetIds.N | 아니요 | Array of Integer | 서브넷 ID |
| CdbErrors.N | 아니요 | Array of Integer | 잠금 여부 플래그 |
| OrderBy | 아니요 | String | 반환 결과 집합 정렬 필드, 현재 지원되는 값: "InstanceId", "InstanceName", "CreateTime", "DeadlineTime" |
| OrderDirection | 아니요 | String | 반환 결과 집합 정렬 방식, 현재 지원 값: “ASC” 또는 “DESC” |
| WithSecurityGroup | 아니요 | Integer | 보안 그룹 세부 정보 포함 여부, 선택 가능 값: 0-포함되지 않음, 1-포함 |
| WithExCluster | 아니요 | Integer | 독점적 클러스터 세부 정보 포함 여부, 선택 가능 값: 0-포함되지 않음, 1-포함 |
| ExClusterId | 아니요 | String | 독점적 클러스터 ID |
| InstanceIds.N | 아니요 | Array of String | 인스턴스 ID |
| InitFlag | 아니요 | Integer | 초기화 플래그, 선택 가능 값: 0-초기화하지 않음, 1-초기화 |
| WithDr | 아니요 | Integer | 재해 복구 인스턴스 포함 여부, 선택 가능 값: 0-포함되지 않음, 1-포함 |
| WithRo | 아니요 | Integer | 읽기 전용 인스턴스 포함 여부, 선택 가능 값: 0-포함되지 않음, 1-포함 |
| WithMaster | 아니요 | Integer | 마스터 인스턴스 포함 여부, 선택 가능 값: 0-포함되지 않음, 1-포함 |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| TotalCount | Integer | 조회 조건에 부합하는 인스턴스 총수 |
| Items | Array of [InstanceInfo](/document/api/236/15878#InstanceInfo) | 인스턴스 세부 정보 |
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예시1 인스턴스 리스트 조회

#### 입력 예시

```
https://cdb.tencentcloudapi.com/?Action=DescribeDBInstances
&InstanceIds.0=cdb-70zdmgg1
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response":{
        "TotalCount": 1,
	"RequestId": "756bb037-a44a-4b4f-abe0-6efd34a6c792",
	"Items": [{
			"WanStatus": 0,
			"Zone": "ap-chengdu-1",
			"InitFlag": 1,
			"Memory": 1000,
			"Status": 1,
			"VpcId": 511512,
			"SlaveInfo": {
				"First": {
					"Vip": "",
					"Region": "ap-chengdu",
					"Vport": 0,
					"Zone": "ap-chengdu-1"
				}
			},
			"InstanceId": "cdb-70zdmgg1",
			"Volume": 50,
			"AutoRenew": 0,
			"ProtectMode": 0,
			"RoGroups": [{
					"RoInstances": [{
							"Status": 1,
							"VpcId": 511512,
							"InstanceType": 3,
							"Zone": "ap-chengdu-1",
							"Qps": 1000,
							"InstanceId": "cdbro-3i70uj0k",
							"Region": "ap-chengdu",
							"DeadlineTime": "0000-00-00 00:00:00",
							"PayType": 1,
							"TaskStatus": 0,
							"Volume": 50,
							"EngineVersion": "5.6",
							"DeviceType": "CUSTOM",
							"Memory": 1000,
							"SubnetId": 115839,
							"Vip": "172.16.0.11",
							"Vport": 3306,
							"InstanceName": "cdb_ro_103608",
							"HourFeeStatus": 1
						}
					],
					"MinRoInGroup": 1,
					"Vip": "172.16.0.11",
					"RoGroupName": "ro_group_103608",
					"Vport": 3306,
					"WeightMode": "system",
					"RoGroupId": "cdbrg-3i70uj0k",
					"RoMaxDelayTime": 1
				}, {
					"RoInstances": [{
							"Status": 1,
							"VpcId": 511512,
							"InstanceType": 3,
							"Zone": "ap-chengdu-1",
							"Qps": 1000,
							"InstanceId": "cdbro-6scijza8",
							"Region": "ap-chengdu",
							"DeadlineTime": "0000-00-00 00:00:00",
							"PayType": 1,
							"TaskStatus": 0,
							"Volume": 25,
							"EngineVersion": "5.6",
							"DeviceType": "CUSTOM",
							"Memory": 1000,
							"SubnetId": 115839,
							"Vip": "172.16.0.25",
							"Vport": 3306,
							"InstanceName": "cdb_ro_103610",
							"HourFeeStatus": 1
						}
					],
					"MinRoInGroup": 1,
					"Vip": "172.16.0.25",
					"RoGroupName": "ro_group_103610",
					"Vport": 3306,
					"WeightMode": "system",
					"RoGroupId": "cdbrg-6scijza8",
					"RoMaxDelayTime": 1
				}
			],
			"SubnetId": 115839,
			"InstanceType": 1,
			"ProjectId": 0,
			"Region": "ap-chengdu",
			"DeadlineTime": "0000-00-00 00:00:00",
			"DeployMode": 0,
			"TaskStatus": 0,
			"DeviceType": "CUSTOM",
			"EngineVersion": "5.6",
			"InstanceName": "jersey_test",
			"DrInfo": [],
			"UniqVpcId": "vpc-5v8wn9mg",
			"WanDomain": "",
			"WanPort": 0,
			"PayType": 1,
			"CreateTime": "2018-05-03 14:53:23",
			"Vip": "172.16.0.16",
			"UniqSubnetId": "subnet-1typ0s7d",
			"Vport": 3306,
			"CdbError": 0
		}
	]
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 인덱스 API 등의 기능을 제공하여, 클라우드 API의 어려움을 크게 줄일 수 있으므로 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=DescribeDBInstances)

### SDK

클라우드 API 3.0은 매칭되는 소프트웨어 개발 키트(SDK)를 제공하고 여러 가지 프로그래밍 언어를 지원하여 더욱 편리한 API 호출이 가능합니다.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. 오류 코드

다음은 API 비즈니스 로직과 관련된 오류 코드만 나열하며 다른 오류 코드는 [공통 오류 코드](/document/api/236/15835#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)를 참조하십시오.

| 오류 코드 | 설명 |
|---------|---------|
| CdbError | 백 엔드 오류 또는 프로세스 오류. |
| InternalError.DatabaseAccessError | 데이터베이스 내부 오류. |
| InternalError.DesError | 시스템 내부 오류. |
| InvalidParameter | 매개변수 오류. |
| InvalidParameter.InstanceNotFound | 인스턴스가 존재하지 않음. |
| OperationDenied.WrongStatus | 백 엔드 태스크 상태 오류. |

