## 1. API 설명

API 요청 도메인 이름: redis.tencentcloudapi.com.

Redis 인스턴스 생성

기본적 API 요청 빈도 제한: 20회/초.

주의: 이 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 있고 서로 통하지 않아서, 공통 매개변수 Region이 금융 지역 도메인(예: ap-shanghai-fsi)일 경우, 금융 지역의 도메인 이름을 동시에 지정해야 하며, Region의 도메인과 일치시키는 것이 가장 좋습니다. 예: redis.ap-shanghai-fsi.tencentcloudapi.com.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수 및 일부 공통 매개변수만 나열되며, 완전한 공통 매개변수 리스트는 [공통 요청 매개변수](/document/api/239/20005)를 참조하십시오.

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, 이 API 값: CreateInstances |
| Version | 예 | String | 공통 매개변수, 이 API 값: 2018-04-12 |
| Region | 예 | String | 공통 매개변수, 자세한 내용은 제품이 지원되는 [지역 리스트](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오. |
| ZoneId | 예 | Integer | 인스턴스 소속 가용 영역 ID |
| TypeId | 예 | Integer | 인스턴스 유형: 2 – Redis 2.8 마스터/슬레이브 버전, 3 – Redis 3.2 마스터/슬레이브 버전(CKV 마스터/슬레이브 버전), 4 – Redis 3.2 클러스터 버전(CKV 클러스터 버전), 5-Redis 2.8 스탠드 얼로운, 7 – Redis 4.0 클러스터 버전 |
| MemSize | 예 | Integer | 인스턴스 용량(MB), 값 크기는 판매 사양 조회 API가 반환한 사양을 기준으로 합니다. |
| GoodsNum | 예 | Integer | 인스턴스 수량, 1회 구매 인스턴스 수량은 판매 사양 조회 API가 반환한 사양을 기준으로 합니다. |
| Period | 예 | Integer | 구매 시간(월), 값 범위: [1,2,3,4,5,6,7,8,9,10,11,12,24,36] |
| Password | 예 | String | 인스턴스 비밀번호, 비밀번호 규칙: 1. 길이는 8 - 16자입니다. 2. 적어도 알파벳, 숫자와 특수 문자 !@^*() 중 두 가지를 포함합니다. |
| BillingMode | 예 | Integer | 결제 방식: 0 - 사용량 기반, 1 - 연/월정액 |
| VpcId | 아니요 | String |  VPC ID, 비워 있는 경우 기본적으로 기본 네트워크를 선택합니다. VPC 리스트를 사용하여 조회하십시오. 예: vpc-sad23jfdfk |
| SubnetId | 아니요 | String | 기본 네트워크에서 subnetId는 무효하고, vpc 서브넷에서 값은 서브넷 리스트 조회 API가 반환한 subnetId를 기준으로 합니다. 예: subnet-fdj24n34j2 |
| ProjectId | 아니요 | Integer | 프로젝트 ID, 값은 사용자 계정 > 사용자 계정 관련 API > 프로젝트 리스트가 반환한 projectId를 기준으로 합니다. |
| AutoRenew | 아니요 | Integer | 자동 갱신 상태. 0 - 기본 상태(수동 갱신). 1 - 자동 갱신. 2 - 명확히 자동 갱신하지 않음 |
| SecurityGroupIdList.N | 아니요 | Array of String | 보안 그룹 ID 배열 |
| VPort | 아니요 | Integer | 사용자 지정한 포트, 입력하지 않으면 기본값(6379)으로 표시됩니다. |
| RedisShardNum | 아니요 | Integer | 인스턴스 샤딩 수량, Redis 2.8 마스터/슬레이브 버전, CKV 마스터/슬레이브 버전과 Redis 2.8 스탠드 얼로운은 입력할 필요가 없습니다. |
| RedisReplicasNum | 아니요 | Integer | 인스턴스 복제본 수량, Redis 2.8 마스터/슬레이브 버전, CKV 마스터/슬레이브 버전과 Redis 2.8 스탠드 얼로운은 입력할 필요가 없습니다. |
| ReplicasReadonly | 아니요 | Boolean | 복제본 읽기 전용 지원 여부, Redis 2.8 마스터/슬레이브 버전, CKV 마스터/슬레이브 버전과 Redis 2.8 스탠드 얼로운은 입력할 필요가 없습니다. |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| DealId | String | 거래 ID|
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예시 1 요청 예시

#### 입력 예시

```
https://redis.tencentcloudapi.com/?Action=CreateInstances
&ZoneId=100002
&TypeId=2
&MemSize=1024
&GoodsNum=1
&Period=1
&Password=********
&BillingMode=1
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "DealId": "123456",
        "RequestId": "d4e2fd95-eac5-41ef-a7a9-7d30024d5507"
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 인덱스 API 등의 기능을 제공하여, 클라우드 API의 어려움을 크게 줄일 수 있으므로 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=CreateInstances)

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

다음은 API 비즈니스 로직과 관련된 오류 코드만 나열하며 다른 오류 코드는 [공통 오류 코드](/document/api/239/20007#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)를 참조하십시오.

| 오류 코드 | 설명 |
|---------|---------|
| InvalidParameter.OnlyVPCOnSpecZoneId | 상하이 금융은 VPC만 제공. |
| InvalidParameterValue.InvalidInstanceTypeId | 구매한 인스턴스 유형 오류(TypeId 1: 클러스터 버전, 2: 마스터/슬레이브 버전, 즉, 기존 마스터/슬레이브 버전). |
| InvalidParameterValue.InvalidSubnetId | VPC에서 서브넷 ID가 잘못되었습니다. |
| InvalidParameterValue.PasswordEmpty | 비밀번호가 비어 있습니다. |
| InvalidParameterValue.PasswordRuleError | 비밀번호 리셋 시, MC가 가져온 old password와 이전에 설정한 암호과 같지 않습니다. |
| LimitExceeded.InvalidMemSize | 요청 용량이 판매 사양에 있지 않습니다(memSize는 1024의 정수 배수여야 하며, 단위는 MB입니다). |
| LimitExceeded.InvalidParameterGoodsNumNotInRange | 한 번 구매한 인스턴스 수는 판매 수량 한도 범위 내에 있지 않습니다. |
| LimitExceeded.PeriodExceedMaxLimit | 구매 시간이 3년을 초과하고, 요청 시간이 최대 시간을 초과합니다. |
| LimitExceeded.PeriodLessThanMinLimit | 구매 시간이 잘못되었으며, 시간은 최소 1개월입니다. |
| ResourceNotFound.AccountDoesNotExists | uin 값이 비어 있습니다. |
| ResourceNotFound.InstanceNotExists | serialId에 따라 해당 Redis를 찾지 못했습니다. |
| ResourceUnavailable.InstanceDeleted | 인스턴스가 회수되었습니다. |
| ResourceUnavailable.NoRedisService | 요청한 지역은 현재 요청 유형의 Redis 서비스를 제공하지 않습니다. |
| ResourceUnavailable.NoTypeIdRedisService | 요청한 지역은 현재 요청 유형의 Redis 서비스를 제공하지 않습니다. |
| UnauthorizedOperation.NoCAMAuthed | cam 권한이 없습니다. |
| UnauthorizedOperation.UserNotInWhiteList | 사용자가 화이트리스트에 없습니다. |
