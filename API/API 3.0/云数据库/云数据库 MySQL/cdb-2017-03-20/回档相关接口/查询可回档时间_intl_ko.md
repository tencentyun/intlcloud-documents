## 1. API 설명

API 요청 도메인 이름: cdb.tencentcloudapi.com.

이 API(DescribeRollbackRangeTime)는 데이터베이스 인스턴스 리스트의 롤백 가능한 시간 범위 조회에 사용합니다.

기본적 API 요청 빈도 제한: 20회/초.

주의: 이 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 있고 서로 통하지 않아서, 공통 매개변수 Region이 금융 지역 도메인(예: ap-shanghai-fsi)일 경우, 금융 지역의 도메인 이름을 동시에 지정해야 하며, Region의 도메인과 일치시키는 것이 가장 좋습니다. 예: cdb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수 및 일부 공통 매개변수만 나열되며, 완전한 공통 매개변수 리스트는 [공통 요청 매개변수](/document/api/236/15833)를 참조하십시오.

| 매개변수 이름 | 필수 항목 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, 이 API 값: DescribeRollbackRangeTime |
| Version | 예 | String | 공통 매개변수, 이 API 선택 값: 2017-03-20 |
| Region | 아니요 | String | 공통 매개변수, 자세한 내용은 제품의 지원되는 [지역 리스트](/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오. |
| InstanceIds.N | Yes | Array of String | 인스턴스 ID 리스트, 단일 인스턴스 ID의 형식 예: cdb-c1nl9rpv. TencentDB 콘솔 페이지에 표시된 인스턴스 ID와 동일합니다. |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| TotalCount | Integer | 조회 조건에 부합하는 인스턴스 총수. |
| Items | Array of [InstanceRollbackRangeTime](/document/api/236/15878#InstanceRollbackRangeTime) | 반환된 매개변수 정보. |
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예시1 롤백 가능한 시간 조회

#### 입력 예시

```
https://cdb.tencentcloudapi.com/?Action=DescribeRollbackRangeTime
&InstanceIds.0=cdb-fix44sxh
&InstanceIds.1=cdb-bdf7h3j1
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response":
    {
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "TotalCount":2,
        "Items":[
            {
                "InstanceId":"cdb-fix44sxh",
                "Message":"ok",
                "Code":0,
                "Times":[
                    {
                        "Begin":"2017-08-21 02:06:20",
                        "End":"2017-08-25 17:52:05"
                    }
                ]
            },
            {
                "InstanceId":"cdb-bdf7h3j1",
                "Message":"ok",
                "Code":0,
                "Times":[
                    {
                        "Begin":"2017-08-21 02:06:00",
                        "End":"2017-08-25 17:52:05"
                    }
                ]
            }
        ]
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 인덱스 API 등의 기능을 제공하여, 클라우드 API의 어려움을 크게 줄일 수 있으므로 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=DescribeRollbackRangeTime)

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
| InternalError.DatabaseAccessError | 데이터베이스 내부 오류. |
| InvalidParameter | 매개변수 오류. |
| InvalidParameter.InstanceNotFound | 인스턴스가 존재하지 않음. |
| OperationDenied | 작업이 허용되지 않음. |

