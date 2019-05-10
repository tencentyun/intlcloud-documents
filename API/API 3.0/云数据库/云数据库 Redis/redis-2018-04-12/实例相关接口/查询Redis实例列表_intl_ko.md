## 1. API 설명

API 요청 도메인 이름: redis.tencentcloudapi.com.

Redis 인스턴스 리스트 조회

기본적 API 요청 빈도 제한: 20회/초.

주의: 이 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 있고 서로 통하지 않아서, 공통 매개변수 Region이 금융 지역 도메인(예: ap-shanghai-fsi)일 경우, 금융 지역의 도메인 이름을 동시에 지정해야 하며, Region의 도메인과 일치시키는 것이 가장 좋습니다. 예: redis.ap-shanghai-fsi.tencentcloudapi.com.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수 및 일부 공통 매개변수만 나열되며, 완전한 공통 매개변수 리스트는 [공통 요청 매개변수](/document/api/239/20005)를 참조하십시오.

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, 이 API 값: DescribeInstances |
| Version | 예 | String | 공통 매개변수, 이 API 값: 2018-04-12 |
| Region | 예 | String | 공통 매개변수, 자세한 내용은 제품이 지원되는 [지역 리스트](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오. |
| Limit | 아니요 | Integer | 인스턴스 리스트의 크기, 매개변수 기본값: 20 |
| Offset | 아니요 | Integer | 오프셋, Limit의 정수 배수 |
| InstanceId | 아니요 | String | 인스턴스 ID, 예: crs-6ubhgouj |
| OrderBy | 아니요 | String | 나열 범위: projectId, createtime, instancenamfe, type, curDeadline |
| OrderType | 아니요 | Integer | 1 내림차순, 0 오름차순, 기본: 내림차순 |
| VpcIds.N | 아니요 | Array of String | VPC ID 배열, 배열 아래 첨자는 0부터 시작하며 비워 있으면 기본 네트워크를 기본으로 선택합니다. 예: 47525 |
| SubnetIds.N | 아니요 | Array of String | 서브넷 ID 배열, 배열 아래 첨자는 0부터 시작합니다. 예: 56854 |
| ProjectIds.N | 아니요 | Array of Integer | 프로젝트 ID로 구성된 배열, 배열 아래 첨자는 0부터 시작합니다. |
| SearchKey | 아니요 | String | 조회할 인스턴스의 ID. |
| InstanceName | 아니요 | String | 인스턴스 이름 |
| UniqVpcIds.N | 아니요 | Array of String | VPC ID 배열, 배열 아래 첨자는 0부터 시작하며 비워 있으면 기본 네트워크를 기본으로 선택합니다. 예: vpc-sad23jfdfk |
| UniqSubnetIds.N | 아니요 | Array of String | 서브넷 ID 배열, 배열 아래 첨자는 0부터 시작합니다. 예: subnet-fdj24n34j2 |
| RegionIds.N | 아니요 | Array of Integer | 지역 ID, 이미 사용 폐기되었으며 공통 매개변수 Region을 통해 해당 지역을 조회할 수 있습니다. |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| TotalCount | Integer | 인스턴스 수|
| InstanceSet | Array of [InstanceSet](/document/api/239/20022#InstanceSet) | 인스턴스 세부 정보 리스트|
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예시 1 요청 예시

#### 입력 예시

```
https://redis.tencentcloudapi.com/?Action=DescribeInstances
&Limit=5
&Offset=0
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "TotalCount": 1,
        "InstanceSet": [
            {
                "InstanceName": "crs-6ubhgouj",
                "InstanceId": "crs-6ubhgouj",
                "Appid": 251005863,
                "ProjectId": 0,
                "RegionId": 1,
                "ZoneId": 100002,
                "VpcId": 0,
                "SubnetId": 0,
                "UniqVpcId": "",
                "UniqSubnetId": "",
                "Status": 2,
                "WanIp": "10.66.126.126",
                "Port": 6379,
                "Createtime": "2015-06-11 16:54:21",
                "Type": 1,
                "BillingMode": 1,
                "Engine": "Redis 커뮤니티 버전",
                "ProductType": "Redis2.8 클러스터 버전",
                "Size": 2048,
                "SizeUsed": 0,
                "DeadlineTime": "2020-09-08 16:21:05",
                "AutoRenewFlag": 0
            }
        ],
        "RequestId": "03f6c2f8-cd3f-41aa-82b8-3bce0c605da5"
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 인덱스 API 등의 기능을 제공하여, 클라우드 API의 어려움을 크게 줄일 수 있으므로 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=DescribeInstances)

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
| InternalError.DbOperationFailed | 시스템 DB 작업 오류, 가능한 값: update insert select.. |
| InvalidParameter | 매개변수 오류 |
| InvalidParameter.EmptyParam | 매개변수가 비어 있습니다. |
| InvalidParameter.InvalidParameter | 비즈니스 매개변수가 잘못되었습니다. |
| UnauthorizedOperation.NoCAMAuthed | cam 권한이 없습니다. |
