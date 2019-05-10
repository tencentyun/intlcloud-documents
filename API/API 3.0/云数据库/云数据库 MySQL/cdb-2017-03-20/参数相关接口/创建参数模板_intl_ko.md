## 1. API 설명

API 요청 도메인 이름: cdb.tencentcloudapi.com.

이 API(CreateParamTemplate)는 매개변수 템플릿 생성에 사용합니다.

기본적 API 요청 빈도 제한: 100회/초.

주의: 이 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 있고 서로 통하지 않아서, 공통 매개변수 Region이 금융 지역 도메인(예: ap-shanghai-fsi)일 경우, 금융 지역의 도메인 이름을 동시에 지정해야 하며, Region의 도메인과 일치시키는 것이 가장 좋습니다. 예: cdb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수 및 일부 공통 매개변수만 나열되며, 완전한 공통 매개변수 리스트는 [공통 요청 매개변수](/document/api/236/15833)를 참조하십시오.

| 매개변수 이름 | 필수 항목 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, 이 API 값: CreateParamTemplate |
| Version | 예 | String | 공통 매개변수, 이 API 선택 값: 2017-03-20 |
| Region | 아니요 | String | 공통 매개변수, 자세한 내용은 제품의 지원되는 [지역 리스트](/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오. |
| Name | 예 | String | 매개변수 템플릿 이름. |
| Description | 아니요 | String | 매개변수 템플릿 설명. |
| EngineVersion | 아니요 | String | mysql 버전. |
| TemplateId | 아니요 | Integer | 소스 매개변수 템플릿 ID. |
| ParamList.N | 아니요 | Array of [Parameter](/document/api/236/15878#Parameter) | 매개변수 리스트. |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| TemplateId | Integer | 매개변수 템플릿 ID. |
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예시1 매개변수 템플릿 생성

#### 입력 예시

```
https://cdb.tencentcloudapi.com/?Action=CreateParamTemplate
&EngineVersion=5.7
&Name=test
&ParamList.0.Name=auto_increment_increment
&ParamList.0.Value=1
&ParamList.1.Name=binlog_format
&ParamList.2.Value=MIXED
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response":{
	"RequestId": "756bb037-a44a-4b4f-abe0-6efd34a6c792",
        "TemplateId": 2333
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 인덱스 API 등의 기능을 제공하여, 클라우드 API의 어려움을 크게 줄일 수 있으므로 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=CreateParamTemplate)

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
| InvalidParameter | 매개변수 오류. |
| InvalidParameter.InvalidName | 잘못된 이름. |

