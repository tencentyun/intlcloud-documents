## 1. API 설명

API 요청 도메인 이름: clb.tencentcloudapi.com.

로드밸런서 인스턴스에 수신기를 생성합니다.
본 API는 비동기 API이며, 본 API 반환 성공 후에는 반환한 RequestID를 입력 매개변수로 하여 DescribeTaskStatus API를 호출해 이번 태스크 성공 여부를 조회합니다.

기본적 API 요청 빈도 제한: 20회/초.

주의: 이 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 있고 서로 통하지 않아서, 공통 매개변수 Region이 금융 지역 도메인(예: ap-shanghai-fsi)일 경우, 금융 지역의 도메인 이름을 동시에 지정해야 하며, Region의 도메인과 일치시키는 것이 가장 좋습니다. 예: clb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수 및 일부 공통 매개변수만 나열되며, 완전한 공통 매개변수 리스트는 [공통 요청 매개변수](/document/api/214/30670)를 참조하십시오.

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, API 값: CreateListener |
| Version | 예 | String | 공통 매개변수, API 값: 2018-03-17 |
| Region | 예 | String | 공통 매개변수, 세부 정보는 [지역 리스트](/document/api/214/30670#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오.
| LoadBalancerId | 예 | String | 로드밸런서 인스턴스 ID |
| Ports.N | 예 | Array of Integer | 수신기를 생성할 목표 포트 번호로 각 포트는 1개의 새로운 수신기와 대응합니다. |
| Protocol | 예 | String | 수신기 프로토콜: HTTP &#124, HTTPS &#124, TCP &#124, TCP_SSL |
| ListenerNames.N | 아니요 | Array of String | 생성할 수신기의 이름 리스트로 이름은 Ports 배열과 순서대로 일일이 대응합니다. 이름을 바로 지정할 필요가 없는 경우, 이 매개변수를 제공할 필요가 없습니다. |
| HealthCheck | 아니요 | [HealthCheck](/document/api/214/30694#HealthCheck) | 상태 검사 관련 매개변수로 TCP/UDP/TCP_SSL 수신기에만 적용됩니다. |
| Certificate | 아니요 | [CertificateInput](/document/api/214/30694#CertificateInput) | 인증서 관련 정보로 HTTPS/TCP_SSL 수신기에만 적용됩니다. |
| SessionExpireTime | 아니요 | Integer | 세션 유지 시간, 단위: 초. 선택 가능 값: 30~3600이며 기본은 0으로 활성화되지 않음을 의미합니다. 이 매개변수는 TCP/UDP 수신기에만 적용됩니다. |
| Scheduler | 아니요 | String | 수신기의 포워딩한 방식으로 선택 가능 값: WRR, LEAST_CONN<br/>WRR: 가중치에 따른 라운드 로빈, LEAST_CONN: 최소 연결 수 기본값: WRR. 이 매개변수는 TCP/UDP/TCP_SSL 수신기에만 적용됩니다. |
| SniSwitch | 아니요 | Integer | SNI 특성 활성화 여부로 HTTPS 수신기에만 적용됩니다. |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| ListenerIds | Array of String | 생성한 수신기의 유일한 식별 배열|
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예시 1 7569와 7570 포트를 따로 수신할 TCP 수신기 2개 생성 각각 lis0과 lis1로 명명

7569와 7570 포트를 따로 수신할 TCP 수신기 2개를 생성하여 각각 lis0과 lis1로 명명합니다.

#### 입력 예시

```
https://clb.tencentcloudapi.com/?Action=CreateListener
&LoadBalancerId=lb-cuxw2rm0
&Protocol=TCP
&Ports.0=7569
&Ports.1=7570
&ListenerNames.0=lis0
&ListenerNames.1=lis1
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "ListenerIds": [
            "lbl-d1ubsydq",
            "lbl-4udz130k"
        ],
        "RequestId": "8f272cef-14ff-458c-b67e-1bd21bd2942b"
    }
}
```

### 예시 2 TCP 수신기 생성과 동시에 상태 검사 정보 설정

#### 입력 예시

```
https://clb.tencentcloudapi.com/?Action=CreateListener
&LoadBalancerId=lb-cuxw2rm0
&Protocol=TCP
&Ports.0=7571
&HealthCheck.HealthSwitch=1
&HealthCheck.TimeOut=5
&HealthCheck.IntervalTime=7
&HealthCheck.HealthNum=4
&HealthCheck.UnHealthNum=4
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "ListenerIds": [
            "lbl-lbbxvq26"
        ],
        "RequestId": "fff13c83-dcb5-481a-ba7c-30e92c276c19"
    }
}
```

### 예시 3 HTTPS 수신기 생성 및 기존 인증서 바인딩

#### 입력 예시

```
https://clb.tencentcloudapi.com/?Action=CreateListener
&LoadBalancerId=lb-cuxw2rm0
&Protocol=HTTPS
&Ports.0=7572
&Certificate.SSLMode=UNIDIRECTIONAL
&Certificate.CertId=MsJyaXVm
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "ListenerIds": [
            "lbl-4fbxq45k"
        ],
        "RequestId": "db8ae69f-ebda-402b-8d02-ead459aa6ff9"
    }
}
```

### 예시 4 HTTPS 수신기 생성 및 새로 추가된 인증서 바인딩

#### 입력 예시

```
https://clb.tencentcloudapi.com/?Action=CreateListener
&LoadBalancerId=lb-cuxw2rm0
&Protocol=HTTPS
&Ports.0=7573
&Certificate.SSLMode=UNIDIRECTIONAL
&Certificate.CertName=my-cert
&Certificate.CertContent=-----BEGIN CERTIFICATE-----
MIIEjTCCA3WgAwIBAgIQA4ZHUAVOv4yrszl3lLfo3TANBgkqhkiG9w0BAQsFADBy
MQswCQYDVQQGEwJDTjElMCMGA1UEChMcVHJ1c3RBc2lhIFRlY2hub2xvZ2llcywg
SW5jLjEdMBsGA1UECxMURG9tYWluIFZhbGlkYXRlZCBTU0wxHTAbBgNVBAMTFFRy
dXN0QXNpYSBUTFMgUlNBIENBMB4XDTE4MDEwOTAwMDAwMFoXDTE5MDEwOTEyMDAw
MFowFjEUMBIGA1UEAxMLZmx5Zmx5Lm5hbWUwggEiMA0GCSqGSIb3DQEBAQUAA4IB
DwAwggEKAoIBAQClpnigB7r3ahv7BMuQw9KzB9Yfq3p+cRUbX9EMRyri2GrJbmrP
pESP8XQuIn4MZESvePR0r4gGHAHVri8nXzyQw6/m77BT/fIf4cQtEyz61gopDlYq
bLTAKVfGFhGVikvQPoItOYbA9/l2YwtDENl8wBhcFrghWTRifnFSC0bNPj1ot5eu
L8x5UOZLSa9kaQCm2/RQUBii5w3YBh+HmJgb7HPs8OoHKVScBo6eAyOcr+HNrA8W
KsM6r4LpS+Rpfng7+fAKGE+vFsssXfRMBTo0TPp+h8ohuM8xqujbK+T7LMEXNWN9
3FGYuuH+qmPvx/gAXFjLARKVyf0IsNnu6TLLAgMBAAGjggF5MIIBdTAfBgNVHSME
GDAWgBR/05nzoEcOMQBWViKOt8ye3coBijAdBgNVHQ4EFgQUUCq9/Hmfgli5URvx
AbSDNsDCCqcwJwYDVR0RBCAwHoILZmx5Zmx5Lm5hbWWCD3d3dy5mbHlmbHkubmFt
ZTAOBgNVHQ8BAf8EBAMCBaAwHQYDVR0lBBYwFAYIKwYBBQUHAwEGCCsGAQUFBwMC
MEwGA1UdIARFMEMwNwYJYIZIAYb9bAECMCowKAYIKwYBBQUHAgEWHGh0dHBzOi8v
d3d3LmRpZ2ljZXJ0LmNvbS9DUFMwCAYGZ4EMAQIBMIGBBggrBgEFBQcBAQR1MHMw
JQYIKwYBBQUHMAGGGWh0dHA6Ly9vY3NwMi5kaWdpY2VydC5jb20wSgYIKwYBBQUH
MAKGPmh0dHA6Ly9jYWNlcnRzLmRpZ2l0YWxjZXJ0dmFsaWRhdGlvbi5jb20vVHJ1
c3RBc2lhVExTUlNBQ0EuY3J0MAkGA1UdEwQCMAAwDQYJKoZIhvcNAQELBQADggEB
ADstNGgqYXG6eBDcBGVZk6DnJdS4GYdSzFZgCwt298cPMmZj107VM0QsB5K8V5Zd
zJl5c7o4tEXiGP+lk0TVqgP/CkcMXcpxeKB94ldyX9ILii/L4hI9j7hVrLVM1eAn
fS66Yg65xIYU8PdFtP3uhI9WdhE3nYRngyoHAAMjIvu0bqGPYbqpnHYp8fmjyetF
C9CZcjkqHmwTSpjXuFjbDLx/BXd1Q81TNXwv8alkuXKfIJ5tW2lH372GmQb8I3oI
PREP38tlBbmfEu4p7+UzwwuQuD8cEUVuG/x7cUN2uAGiZGoohydrORWm8kqdNY9c
YOuRvokzVT4lsaln5LKkKxw=
-----END CERTIFICATE-----
&Certificate.CertKey=-----BEGIN RSA PRIVATE KEY-----
MIIEoAIBAAKCAQEApaZ4oAe692ob+wTLkMPSswfWH6t6fnEVG1/RDEcq4thqyW5q
z6REj/F0LiJ+DGREr3j0dK+IBhwB1a4vJ188kMOv5u+wU/3yH+HELRMs+tYKKQ5W
Kmy0wClXxhYRlYpL0D6CLTmGwPf5dmMLQxDZfMAYXBa4IVk0Yn5xUgtGzT49aLeX
ri/MeVDmS0mvZGkAptv0UFAYoucN2AYfh5iYG+xz7PDqBylUnAaOngMjnK/hzawP
FirDOq+C6UvkaX54O/nwChhPrxbLLF30TAU6NEz6fofKIbjPMaro2yvk+yzBFzVj
fdxRmLrh/qpj78f4AFxYywESlcn9CLDZ7ukyywIDAQABAoH/KoiULD7g9kAEZrQp
1SQusYVRl+E8xeVUdQhHcfCyAUkIAEpZzV2TtLd+DFqKrbTvITBT+vd9sYtdU6K7
Z8cMcMoSpNMq+/+wK/b/m4I/6EqEt8HDb0NpSBBEeWUxQM4fumnsFBcXtew6iCtu
2vzN7G2IwqUSxI5nbY2SektZ4q5ZRvwEND6gE51uqcqo4i6hA/TYsJLZ63L+Ux0A
nm0AsmtMct+DT13NAlpyi6feDQCr1cxcSpqfhfgkWpawJVSxtxKvIn044iRBXb7Y
RcW/8YYU1PrTIhhE9AnES7g8mnAgBHRryxuUotXkk7VotTHDbTO0q5KvO2bZ2T6z
vQ4BAoGBANqoZE/wAB41wbJ7KwyblxyegI3Y9XYtkPLZlLK+GbCaC9UHNhPqSdaH
WPoc3rtm8tOFQc7QMTFtxTLwQ3wEeSO4BFckVHgywuJoGRw1ZYxN8vAzHF1Gc/J1
YcX0CDBuKgc0CxlhM7tDAzOgcfJR0EFRVhvLcUAA9hUoeN3EetSBAoGBAMHwnjWc
+Y/vBW5yCefQciqppaylwB89H6kds+p0fDlVZQ080VB3b61t6VXOoYAzY4abOjxK
AfNyVQcOEuO3gtZp3THK3fkV6bKaNHG41Ang32VW3XGb+MeEkJZwJk4JFbLrz8ln
te4M9PjVpYuEQCJZvUjrhd+LJRubTTUXIHFLAoGAU0KJp/KwaNB5aDgERXG9kbU9
KEYz+YMSTZbSS1mduKR/2uc7DUxKP3kcRWjW2y8xSZ/VViXqhXLSAzp/x+qAIjzA
0lnQHFDf6oxO+3HNsCZCWnpr04yvO+S8jT8GG0LnmASWMVzU8Ppsbq0qlmXW0fhh
vIW0IvX6vkXB+FgHmYECgYBrsJe5P4QYV2oVrP8xGL78T51uY89tyTwWZSbtTmdY
UsG8+wNjgh6iF8EUY5usG1ztdq58ob+5lcf/FeKJTfI56yjnKDXfxToycYwjhbVA
Ev0ZQYXPOwOGjmbXEklC1aqV4nlL5enQ2KMCtWeqM/KE4H3JyvZYbeRaEv9pNoFO
RwKBgBs+g0d81ufZSuTBlxfivDwrNV6LNzrgnwsTn+H/T7MfyoIEkT3nSGjanQHF
wzPYyUpQx5OzNZp1ZEzKeW3GXVWjK+bfKlA7fmrZwDa8/JR6kTfCmc3WRrrQ92yq
lFRW1kinLCP5y56SJEBz+DRSYV7ql9wOHyaM23sHkbCF0HAa
-----END RSA PRIVATE KEY-----
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "ListenerIds": [
            "lbl-bzfmg9m6"
        ],
        "RequestId": "6082314c-030c-429d-9eae-2dc6b159b5b9"
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 인덱스 API 등의 기능을 제공하여, 클라우드 API의 어려움을 크게 줄일 수 있으므로 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=clb&Version=2018-03-17&Action=CreateListener)

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
| LimitExceeded | 할당량 한도 초과 |
| ResourceInsufficient | 리소스 부족 |
| UnauthorizedOperation | 권한이 없는 작업 |

