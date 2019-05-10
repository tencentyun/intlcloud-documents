## 1. API 설명

API 요청 도메인 이름: clb.tencentcloudapi.com.

ModifyListener는 응용형 CLB 수신기의 속성을 수정하는 데 사용되며 수신기 이름, 상태 검사 매개변수, 인증서 정보, 포워딩 전략 등이 포함됩니다.
본 API는 비동기 API이며, 본 API 반환 성공 후에는 반환한 RequestID를 입력 매개변수로 하여 DescribeTaskStatus API를 호출해 이번 태스크 성공 여부를 조회합니다.

기본적 API 요청 빈도 제한: 20회/초.

주의: 이 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 있고 서로 통하지 않아서, 공통 매개변수 Region이 금융 지역 도메인(예: ap-shanghai-fsi)일 경우, 금융 지역의 도메인 이름을 동시에 지정해야 하며, Region의 도메인과 일치시키는 것이 가장 좋습니다. 예: clb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수 및 일부 공통 매개변수만 나열되며, 완전한 공통 매개변수 리스트는 [공통 요청 매개변수](/document/api/214/30670)를 참조하십시오.

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, API 값: ModifyListener |
| Version | 예 | String | 공통 매개변수, API 값: 2018-03-17 |
| Region | 예 | String | 공통 매개변수, 세부 정보는 [지역 리스트](/document/api/214/30670#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오.
| LoadBalancerId | 예 | String | 로드밸런서 인스턴스 ID |
| ListenerId | 예 | String | 로드밸런서 수신기 ID |
| ListenerName | 아니요 | String | 새로운 수신기 이름 |
| SessionExpireTime | 아니요 | Integer | 세션 유지 시간, 단위: 초. 선택 가능 값: 30~3600이며 기본은 0으로 활성화되지 않음을 의미합니다. 이 매개변수는 TCP/UDP 수신기에만 적용됩니다. |
| HealthCheck | 아니요 | [HealthCheck](/document/api/214/30694#HealthCheck) | 상태 검사 관련 매개변수로 TCP/UDP/TCP_SSL 수신기에만 적용됩니다. |
| Certificate | 아니요 | [CertificateInput](/document/api/214/30694#CertificateInput) | 인증서 관련 정보로 HTTPS/TCP_SSL 수신기에만 적용됩니다. |
| Scheduler | 아니요 | String | 수신기의 포워딩한 방식으로 선택 가능 값: WRR, LEAST_CONN<br/>WRR: 가중치에 따른 라운드 로빈, LEAST_CONN: 최소 연결 수 기본값: WRR. |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예시 1 TCP 수신기의 이름, 상태 검사 매개변수 및 포워딩 전략 수정

#### 입력 예시

```
https://clb.tencentcloudapi.com/?Action=ModifyListener
&LoadBalancerId=lb-cuxw2rm0
&ListenerId=lbl-d1ubsydq
&ListenerName=newlis
&SessionExpireTime=120
&Scheduler=LEAST_CONN
&HealthCheck.HealthSwitch=1
&HealthCheck.TimeOut=35
&HealthCheck.IntervalTime=60
&HealthCheck.HealthNum=5
&HealthCheck.UnHealthNum=5
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "RequestId": "8cd88c83-fd30-47c0-8e7a-89bf13a7a83c"
    }
}
```

### 예시 2 HTTPS 수신기가 바인딩한 인증서 수정

#### 입력 예시

```
https://clb.tencentcloudapi.com/?Action=ModifyListener
&LoadBalancerId=lb-cuxw2rm0
&ListenerId=lbl-4fbxq45k
&Certificate.SSLMode=UNIDIRECTIONAL
&Certificate.CertId=Nb1DY3hQ
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "RequestId": "b64574f9-5bc7-4a63-a9d7-3671b6a6d62b"
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 인덱스 API 등의 기능을 제공하여, 클라우드 API의 어려움을 크게 줄일 수 있으므로 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=clb&Version=2018-03-17&Action=ModifyListener)

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

다음은 API 비즈니스 로직과 관련된 오류 코드만 나열하며 다른 오류 코드는 [공통 오류 코드](/document/api/214/30673#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)를 참조하십시오.

| 오류 코드 | 설명 |
|---------|---------|
| FailedOperation | 조작 실패. |
| InternalError | 내부 오류 |
| InvalidParameter | 매개변수 오류. |
| InvalidParameterValue | 매개변수 값 오류 |
| UnauthorizedOperation | 권한이 없는 작업 |

