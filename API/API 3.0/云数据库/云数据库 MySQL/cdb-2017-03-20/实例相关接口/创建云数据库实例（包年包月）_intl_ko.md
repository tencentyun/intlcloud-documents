## 1. API 설명

API 요청 도메인 이름: cdb.tencentcloudapi.com.

이 API(CreateDBInstance)는 연/월정액 요금제 데이터베이스 인스턴스(마스터 인스턴스, 재해 복구 인스턴스 및 읽기 전용 인스턴스 포함)를 생성하는 데 사용되며, 인스턴스 사양, MySQL 버전 번호, 구매 시간 및 수량 등의 정보를 입력하여 데이터베이스 인스턴스를 생성할 수 있습니다.

이 API는 비동기화 API이며, [인스턴스 리스트 조회](https://cloud.tencent.com/document/api/236/15872) API를 사용하여 해당 인스턴스의 세부 정보를 조회할 수 있습니다. 인스턴스의 Status가 1이고, TaskStatus가 0이면 인스턴스가 성공적으로 발송되었음을 나타냅니다.

1. 먼저 [데이터베이스 판매 가능 사양 획득](https://cloud.tencent.com/document/api/236/17229) API를 사용하여 생성 가능한 인스턴스 사양 정보를 조회한 후, [데이터베이스 가격 조회](https://cloud.tencent.com/document/api/236/18566) API를 사용하여 생성 가능한 인스턴스의 판매 가격을 조회합니다.
2. 1회 최대 100개의 인스턴스를 생성할 수 있으며, 인스턴스 기간은 최대 36개월까지 지원합니다.
3. MySQL5.5, MySQL5.6, MySQL5.7 버전 생성을 지원합니다.
4. 마스터 인스턴스, 읽기 전용 인스턴스, 재해 복구 인스턴스를 지원합니다.

기본적 API 요청 빈도 제한: 20회/초.

주의: 이 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 있고 서로 통하지 않아서, 공통 매개변수 Region이 금융 지역 도메인(예: ap-shanghai-fsi)일 경우, 금융 지역의 도메인 이름을 동시에 지정해야 하며, Region의 도메인과 일치시키는 것이 가장 좋습니다. 예: cdb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수 및 일부 공통 매개변수만 나열되며, 완전한 공통 매개변수 리스트는 [공통 요청 매개변수](/document/api/236/15833)를 참조하십시오.

| 매개변수 이름 | 필수 항목 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, 이 API 값: CreateDBInstance |
| Version | 예 | String | 공통 매개변수, 이 API 선택 값: 2017-03-20 |
| Region | 아니요 | String | 공통 매개변수, 자세한 내용은 제품의 지원되는 [지역 리스트](/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오. |
| Memory | 예 | Integer | 인스턴스 메모리 크기, 단위: MB, [데이터베이스 판매 가능 사양 획득](https://cloud.tencent.com/document/api/236/17229) API를 사용하여 생성 가능한 메모리 사양을 획득하십시오. |
| Volume | 아니요 | Integer | 인스턴스 디스크 크기, 단위: GB, [데이터베이스 판매 가능 사양 획득](https://cloud.tencent.com/document/api/236/17229) API를 사용하여 생성 가능한 디스크 범위를 획득하십시오. |
| Period | 예 | Integer | 인스턴스 기간, 단위: 월, 사용 가능한 값은 [1,2,3,4,5,6,7,8,9,10,11,12,24,36]입니다. |
| GoodsNum | 예 | Integer | 인스턴스 수량, 기본값은 1, 최소값은 1, 최대값은 100입니다. |
| Zone | 아니요 | String | 가용 영역 정보, 해당 매개변수가 없으면 시스템은 자동으로 한 개의 가용 영역을 선택합니다. [데이터베이스 판매 가능 사양 획득](https://cloud.tencent.com/document/api/236/17229) API를 사용하여 생성 가능한 가용 영역을 획득하십시오. |
| UniqVpcId | 아니요 | String | VPC ID, 전달하지 않을 경우 기본적으로 기본 네트워크를 선택합니다. [VPC 리스트 조회](/document/api/215/15778) API를 사용하십시오. |
| UniqSubnetId | 아니요 | String | VPC 하의 서브넷 ID, UniqVpcId를 설정한 경우, UniqSubnetId를 반드시 입력해야 합니다. [서브넷 리스트 조회](/document/api/215/15784) API를 사용하십시오. |
| ProjectId | 아니요 | Integer | 프로젝트 ID, 입력하지 않으면 기본적으로 기본 프로젝트입니다. [프로젝트 리스트 조회](https://cloud.tencent.com/document/product/378/4400) API를 사용하여 프로젝트 ID를 획득하십시오. |
| Port | 아니요 | Integer | 사용자 지정 포트, 포트 지원 범위: [1024, -65535] |
| InstanceRole | 아니요 | String | 인스턴스 유형, 기본값은 master, 지원 값은 master-마스터 인스턴스, dr-재해 복구 인스턴스, or-읽기 전용 인스턴스입니다. |
| MasterInstanceId | 아니요 | String | 인스턴스 ID, 읽기 전용 인스턴스 구매 시 반드시 입력해야 하며, 이 필드는 읽기 전용 인스턴스의 마스터 인스턴스 ID를 표시합니다. [인스턴스 리스트 조회](https://cloud.tencent.com/document/api/236/15872) API를 사용하여 데이터베이스 인스턴스 ID를 조회하십시오. |
| EngineVersion | 아니요 | String | MySQL 버전, 포함 값: 5.5, 5.6 및 5.7, [데이터베이스 판매 가능 사양 획득](https://cloud.tencent.com/document/api/236/17229) API를 사용하여 생성 가능한 인스턴스 버전을 획득하십시오. |
| Password | 아니요 | String | root 계정 비밀번호 설정, 비밀번호 규칙: 8-64자, 알파벳, 숫자, 특수 문자(_+-&=!@#$%^*() 지원) 중 최소 두 가지를 포함해야 합니다. 마스터 인스턴스 구매 시 해당 매개변수를 지정할 수 있으며, 읽기 전용 인스턴스 또는 재해 복구 인스턴스 구매 시 해당 매개변수를 지정해도 의미가 없습니다. |
| ProtectMode | 아니요 | Integer | 데이터 복제 방식, 기본값은 0, 지원되는 값은 0-비동기화 복제, 1-반동기화 복제, 2-강제 동기화 복제입니다. |
| DeployMode | 아니요 | Integer | 멀티 가용 영역, 기본값은 0, 지원되는 값은 0-단일 가용 영역, 1-멀티 가용 영역입니다. |
| SlaveZone | 아니요 | String | 슬레이브 데이터베이스1의 가용 영역 정보, 기본적으로 zone의 값입니다 |
| ParamList.N | 아니요 | Array of [ParamInfo](/document/api/236/15878#ParamInfo) | 매개변수 리스트, 매개변수 형식 예: ParamList.0.Name=auto_increment&ParamList.0.Value=1. [인스턴스의 설정 가능 매개 변수 리스트 조회](https://cloud.tencent.com/document/api/236/20411) API를 통해 설정 가능한 매개변수를 조회할 수 있습니다. |
| BackupZone | 아니요 | String | 슬레이브 데이터베이스2의 가용 영역 ID, 기본값은 0입니다. 마스터 인스턴스 구매 시 해당 값을 지정할 수 있으며, 읽기 전용 인스턴스 또는 재해 복구 인스턴스 구매 시 해당 매개변수를 지정해도 의미가 없습니다. |
| AutoRenewFlag | 아니요 | Integer | 자동 갱신 플래그, 선택 가능 값: 0-자동 갱신되지 않음, 1-자동 갱신 |
| MasterRegion | 아니요 | String | 마스터 인스턴스 지역 정보, 재해 복구 인스턴스 구매 시, 해당 필드를 반드시 입력해야 합니다. |
| SecurityGroup.N | 아니요 | Array of String | 보안 그룹 매개변수, [프로젝트 보안 그룹 정보 조회](https://cloud.tencent.com/document/api/236/15850) API를 사용하여 프로젝트의 보안 그룹 세부 정보를 조회할 수 있습니다. |
| RoGroup | 아니요 | [RoGroup](/document/api/236/15878#RoGroup) | 읽기 전용 인스턴스 매개변수 |
| InstanceName | 아니요 | String | 인스턴스 이름 |
| ResourceTags.N | 아니요 | Array of [TagInfo](/document/api/236/15878#TagInfo) | 인스턴스에 바인딩할 태그 |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| DealIds | Array of String | 짧은 주문 ID |
| InstanceIds | Array of String | 인스턴스 ID 리스트 |
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예시1 마스터 인스턴스 구매

#### 입력 예시

```
https://cdb.tencentcloudapi.com/?Action=CreateDBInstance
&Memory=1000
&Volume=25
&Period=1
&GoodsNum=1
&Zone=ap-guangzhou-3
&UniqVpcId=vpc-0akbol5v
&UniqSubnetId=subnet-fyrtjbqw
&ProjectId=0
&InstanceRole=master
&EngineVersion=5.6
&ResourceTags.0.TagKey=marchtest
&ResourceTags.0.TagValue.0=test1
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response":{
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "InstanceIds":["cdb-pn6gd5jp"],
        "DealIds":["20171201110011"]
    }
}
```

### 예시2 읽기 전용 인스턴스 구매

#### 입력 예시

```
https://cdb.tencentcloudapi.com/?Action=CreateDBInstance
&MasterInstanceId=cdb-fn3f9xpx
&Period=1
&GoodsNum=1
&Memory=4000
&Volume=100
&InstanceRole=ro
&RoGroup.roGroupMode=allinone
&RoGroup.roGroupName=jersey_test
&RoGroup.roOfflineDelay=1
&RoGroup.roMaxDelayTime=5
&RoGroup.minRoInGroup=1
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "DealIds": ["20171205110051"],
        "InstanceIds": ["cdbro-hlpl4ik9"]
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 인덱스 API 등의 기능을 제공하여, 클라우드 API의 어려움을 크게 줄일 수 있으므로 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=CreateDBInstance)

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
| FailedOperation.StatusConflict | 태스크 상태 충돌. |
| InternalError.DatabaseAccessError | 데이터베이스 내부 오류. |
| InternalError.DfwError | 보안 그룹 조작 오류. |
| InternalError.TradeError | 거래 시스템 오류. |
| InternalError.VpcError | VPC 또는 서브넷 오류. |
| InvalidParameter | 매개변수 오류. |
| OperationDenied.ActionNotSupport | 지원되지 않는 조작. |
| OperationDenied.WrongPassword | 비밀번호 오류 또는 인증을 통과하지 못했습니다. |

