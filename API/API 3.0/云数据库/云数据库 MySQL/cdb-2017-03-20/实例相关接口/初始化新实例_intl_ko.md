## 1. API 설명

API 요청 도메인 이름: cdb.tencentcloudapi.com.

이 API(InitDBInstances)는 비밀번호, 기본 문자 집합, 인스턴스 포트 번호 초기화 등 데이터베이스 인스턴스 초기화에 사용합니다.

기본적 API 요청 빈도 제한: 100회/초.

주의: 이 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 있고 서로 통하지 않아서, 공통 매개변수 Region이 금융 지역 도메인(예: ap-shanghai-fsi)일 경우, 금융 지역의 도메인 이름을 동시에 지정해야 하며, Region의 도메인과 일치시키는 것이 가장 좋습니다. 예: cdb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수 및 일부 공통 매개변수만 나열되며, 완전한 공통 매개변수 리스트는 [공통 요청 매개변수](/document/api/236/15833)를 참조하십시오.

| 매개변수 이름 | 필수 항목 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, 이 API 값: InitDBInstances |
| Version | 예 | String | 공통 매개변수, 이 API 선택 값: 2017-03-20 |
| Region | 아니요 | String | 공통 매개변수, 자세한 내용은 제품의 지원되는 [지역 리스트](/document/api/236/15833#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오. |
| InstanceIds.N | 예 | Array of String | 인스턴스 ID, 형식 예: cdb-c1nl9rpv, TencentDB 콘솔 페이지에 표시된 인스턴스 ID와 동일합니다. [인스턴스 리스트 조회](https://cloud.tencent.com/document/api/236/15872) API를 사용하여 획득할 수 있으며, 그 값은 출력 매개변수 중 필드 InstanceId의 값입니다. |
| NewPassword | 예 | String | 인스턴스의 새 비밀번호, 비밀번호 규칙: 8-64자, 알파벳, 숫자, 특수 문자(!@#$%^*() 지원) 중 최소 두 가지를 포함해야 합니다. |
| Parameters.N | 예 | Array of [ParamInfo](/document/api/236/15878#ParamInfo) | 인스턴스의 매개변수 리스트, 현재 “character_set_server”, “lower_case_table_names” 매개변수 설정을 지원합니다. 그 중, “character_set_server” 선택 가능 값은 ["utf8","latin1","gbk","utf8mb4"], “lower_case_table_names” 선택 가능 값은 [“0”,“1”]입니다. |
| Vport | 아니요 | Integer | 인스턴스의 포트, 값 범위는 [1024, 65535]입니다. |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| AsyncRequestIds | Array of String | 비동기화 태스크의 요청 ID 배열, 이 ID를 사용하여 비동기화 태스크의 실행 결과를 조회할 수 있습니다. |
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예시1 새로운 인스턴스 초기화

#### 입력 예시

```
https://cdb.tencentcloudapi.com/?Action=InitDBInstances
&InstanceIds.0=cdb-f35wr6wj
&NewPassword=Gx18ux23F^X
&Parameters.0.name=lower_case_table_names
&Parameters.0.value=1
&Parameters.1.name=character_set_server
&Parameters.1.value=utf8
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response":{
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "AsyncRequestIds":[
            "8cd119d4-61ba-11e7-aeff-018cfa1f5560"
        ]
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 인덱스 API 등의 기능을 제공하여, 클라우드 API의 어려움을 크게 줄일 수 있으므로 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdb&Version=2017-03-20&Action=InitDBInstances)

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
| InvalidParameter | 매개변수 오류. |

