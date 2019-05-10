## 1. API 설명

API 요청 도메인 이름: redis.tencentcloudapi.com.

인스턴스 갱신

기본적 API 요청 빈도 제한: 20회/초.

주의: 이 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 있고 서로 통하지 않아서, 공통 매개변수 Region이 금융 지역 도메인(예: ap-shanghai-fsi)일 경우, 금융 지역의 도메인 이름을 동시에 지정해야 하며, Region의 도메인과 일치시키는 것이 가장 좋습니다. 예: redis.ap-shanghai-fsi.tencentcloudapi.com.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수 및 일부 공통 매개변수만 나열되며, 완전한 공통 매개변수 리스트는 [공통 요청 매개변수](/document/api/239/20005)를 참조하십시오.

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, 이 API 값: RenewInstance |
| Version | 예 | String | 공통 매개변수, 이 API 값: 2018-04-12 |
| Region | 예 | String | 공통 매개변수, 자세한 내용은 제품이 지원되는 [지역 리스트](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오. |
| Period | 예 | Integer | 구매 시간(월) |
| InstanceId | 예 | String | 인스턴스 ID |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| DealId | String | 주문 ID|
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예시 1 요청 예시

#### 입력 예시

```
https://redis.tencentcloudapi.com/?Action=RenewInstance
&Period=12
&InstanceId=crs-5a4py64p
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "DealId": "6954225",
        "RequestId": "495d8e9f-61bf-465e-aa4e-14be54a9095a"
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 인덱스 API 등의 기능을 제공하여, 클라우드 API의 어려움을 크게 줄일 수 있으므로 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=RenewInstance)

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
| InvalidParameter.EmptyParam | 매개변수가 비어 있습니다. |
| LimitExceeded.PeriodExceedMaxLimit | 구매 시간이 3년을 초과하고, 요청 시간이 최대 시간을 초과합니다. |
| LimitExceeded.PeriodLessThanMinLimit | 구매 시간이 잘못되었으며, 시간은 최소 1개월입니다. |
| ResourceInUse.InstanceBeenLocked | 인스턴스가 기타 프로세스에 잠겼습니다. |
| ResourceNotFound.InstanceNotExists | serialId에 따라 해당 Redis를 찾지 못했습니다. |
| ResourceUnavailable.AccountBalanceNotEnough | 요청 주문 번호가 존재하지 않습니다. |
| ResourceUnavailable.InstanceDeleted | 인스턴스가 회수되었습니다. |
