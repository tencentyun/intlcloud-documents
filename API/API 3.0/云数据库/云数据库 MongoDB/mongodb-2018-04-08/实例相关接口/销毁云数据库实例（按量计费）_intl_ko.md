﻿## 1. API 설명

API 요청 도메인 이름: mongodb.tencentcloudapi.com.

본 API(TerminateDBInstance)는 사용량 기반 요금제의 TencentDB for MongoDB 인스턴스를 폐기하는 데 사용됩니다.

기본 API 요청 빈도 제한: 20회/초.

주의: 본 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 서로 격리되어 있습니다. 따라서 공통 매개변수 Region이 금융 지역(예: ap-shanghai-fsi)일 때, 금융 지역 이름(Region의 지역과 일치하는 것이 가장 좋음)이 포함된 도메인 이름을 동시에 지정해야 합니다. 예: mongodb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. 입력 매개변수

다음 요청 매개변수 리스트는 API 요청 매개변수와 일부 공통 매개변수만 나열하였습니다. 전체 공통 매개변수 리스트는 [공통 요청 매개변수](https://cloud.tencent.com/document/api/240/31800)를 참조하십시오.

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수. 해당 API의 값: TerminateDBInstance |
| Version | 예 | String | 공통 매개변수. 해당 API의 값: 2018-04-08 |
| Region | 예 | String | 공통 매개변수. 제품이 지원하는 [지역 리스트](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/240/31800#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) 참조 |
| InstanceId | 예 | String | 인스턴스 ID. 형식 예: cmgo-p8vnipr5 |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| AsyncRequestId | String | 주문 ID. 인스턴스를 성공적으로 폐기한 것을 나타냅니다. |
| RequestId | String | 유일한 요청 ID. 요청할 때마다 반환됩니다. 문제를 지정할 때 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예제

### 예제1 사용량 기반 요금제의 TencentDB 인스턴스 폐기 

#### 입력 예제

```
https://mongodb.tencentcloudapi.com/?Action=TerminateDBInstance
&InstanceId=cmgo-f555zzzz
&<공통 요청 매개변수>
```

#### 출력 예제

```
{
    "Response":{
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "AsyncRequestId":"28920"
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 검증, SDK 코드 생성과 API 빠른 검색 등의 기능을 제공하며 클라우드 API 사용 난이도를 크게 낮추어 사용을 추천합니다.

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mongodb&Version=2018-04-08&Action=TerminateDBInstance)

### SDK

클라우드 API 3.0은 맞춤형 개발도구 모음(SDK)을 제공하며 다양한 프로그래밍 언어를 지원하여 더욱 편리하게 API를 호출할 수 있습니다.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. 오류 코드

다음은 API 비즈니스 로직과 관련된 오류 코드만 나열하였습니다. 다른 오류 코드는 [공통 오류 코드](https://cloud.tencent.com/document/api/240/31803#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)를 참조하십시오.

| 오류 코드 | 설명 |
|---------|---------|
| InternalError.AsyncRequestError | 비동기 태스크 조회 오류. |
| InvalidParameter | 매개변수 오류 |


