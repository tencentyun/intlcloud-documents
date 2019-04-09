## 1. API 설명

API 요청 도메인 이름: clb.tencentcloudapi.com.

DescribeListeners API는 로드밸런서 ID, 수신기의 프로토콜 또는 포트에 따라 수신기 리스트를 획득할 수 있습니다. 필터링 조건을 지정하지 않을 경우, 기본적으로 해당 로드밸런서의 기본 데이터 길이(20개)의 수신기를 반환하게 됩니다.

기본적 API 요청 빈도 제한: 20회/초.

주의: 이 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 있고 서로 통하지 않아서, 공통 매개변수 Region이 금융 지역 도메인(예: ap-shanghai-fsi)일 경우, 금융 지역의 도메인 이름을 동시에 지정해야 하며, Region의 도메인과 일치시키는 것이 가장 좋습니다. 예: clb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수 및 일부 공통 매개변수만 나열되며, 완전한 공통 매개변수 리스트는 [공통 요청 매개변수](/document/api/214/30670)를 참조하십시오.

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, API 값: DescribeListeners |
| Version | 예 | String | 공통 매개변수, API 값: 2018-03-17 |
| Region | 예 | String | 공통 매개변수, 세부 정보는 [지역 리스트](/document/api/214/30670#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오.
| LoadBalancerId | 예 | String | 로드밸런서 인스턴스 ID |
| ListenerIds.N | 아니요 | Array of String | 조회할 응용형 CLB 수신기 ID 배열 |
| Protocol | 아니요 | String | 조회할 수신기 프로토콜 유형, 값: TCP &#124, UDP &#124, HTTP &#124, HTTPS &#124, TCP_SSL |
| Port | 아니요 | Integer | 조회할 수신기의 포트 |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| Listeners | Array of [Listener](/document/api/214/30694#Listener) | 수신기 리스트|
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예시 1 로드밸런서 인스턴스의 전체 수신기 정보 조회

#### 입력 예시

```
https://clb.tencentcloudapi.com/?Action=DescribeListeners
&LoadBalancerId=lb-1wvl0ejw
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "Listeners": [
            {
                "ListenerId": "lbl-7gogrzv2",
                "Protocol": "HTTPS",
                "Port": 1111,
                "HealthCheck": null,
                "Certificate": null,
                "Scheduler": null,
                "SessionExpireTime": null,
                "SniSwitch": 1,
                "Rules": [
                    {
                        "LocationId": "loc-8s90r6oc",
                        "Domain": "clue.foo2",
                        "Url": "/aa1",
                        "SessionExpireTime": 0,
                        "HealthCheck": {
                            "HealthSwitch": 0,
                            "TimeOut": 2,
                            "IntervalTime": 5,
                            "HealthNum": 3,
                            "UnHealthNum": 3,
                            "HttpCode": 31,
                            "HttpCheckPath": "/",
                            "HttpCheckDomain": "clue.foo",
                            "HttpCheckMethod": "head"
                        },
                        "Certificate": {
                            "SSLMode": "UNIDIRECTIONAL",
                            "CertId": "McKgYApY",
                            "CertCaId": ""
                        },
                        "Scheduler": "WRR"
                    }
                ]
            }
        ],
        "RequestId": "e571614d-c674-4dd8-9f00-4ba0f322d1c1"
    }
}
```

### 예시 2 포트, 프로토콜 및 수신기 ID에 따라 수신기 조회

#### 입력 예시

```
https://clb.tencentcloudapi.com/?Action=DescribeListeners
&LoadBalancerId=lb-1wvl0ejw
&Protocol=TCP
&Port=2007
&ListenerIds.0=lbl-ohamxrok
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "Listeners": [
            {
                "ListenerId": "lbl-ohamxrok",
                "Protocol": "TCP",
                "Port": 2007,
                "HealthCheck": {
                    "HealthSwitch": 1,
                    "TimeOut": 2,
                    "IntervalTime": 5,
                    "HealthNum": 3,
                    "UnHealthNum": 3,
                    "HttpCode": null,
                    "HttpCheckPath": null,
                    "HttpCheckDomain": null,
                    "HttpCheckMethod": null
                },
                "Certificate": null,
                "Scheduler": "WRR",
                "SessionExpireTime": 0,
                "SniSwitch": 0,
                "Rules": null
            }
        ],
        "RequestId": "7371485a-fa7a-48c0-b733-fa8b0fdb1a72"
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 인덱스 API 등의 기능을 제공하여, 클라우드 API의 어려움을 크게 줄일 수 있으므로 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=clb&Version=2018-03-17&Action=DescribeListeners)

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

