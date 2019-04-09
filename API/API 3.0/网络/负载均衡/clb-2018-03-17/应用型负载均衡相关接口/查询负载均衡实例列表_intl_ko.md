## 1. API 설명

API 요청의 도메인 이름: clb.tencentcloudapi.com.

로드밸런서 인스턴스 리스트 조회


기본적 API 요청 빈도 제한: 20회/초.

주의: 이 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 서로 연결되지 않기 때문에 공통 매개변수 Region이 금융 지역인 경우(예: ap-shanghai-fsi) 금융 지역을 포함한 지역 이름을 동시에 지정해야 하며 가장 좋은 것은 Region의 지역과 일치하는 것입니다. 예를 들어, clb.ap-shanghai-fsi.tencentcloudapi.com입니다.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수 및 일부 공통 매개변수만 나열되며, 완전한 공통 매개변수 리스트는 [공통 요청 매개변수](/document/api/214/30670)를 참조하십시오.

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, API 값: DescribeLoadBalancers |
| Version | 예 | String | 공통 매개변수, API 값: 2018-03-17 |
| Region | 예 | String | 공통 매개변수, 세부 정보는 [지역 리스트](/document/api/214/30670#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오. |
| LoadBalancerIds.N | 아니요 | Array of String | 로드밸런서 인스턴스 ID. |
| LoadBalancerType | 아니요 | String | 로드밸런서 인스턴스의 네트워크 유형: <br/>OPEN: 공중망 속성, INTERNAL: 사설망 속성. |
| Forward | 아니요 | Integer | 1: 응용형, 0: 전통형. |
| LoadBalancerName | 아니요 | String | 로드밸런서 인스턴스 이름. |
| Domain | 아니요 | String | Tencent Cloud는 로드밸런서 인스턴스를 위해 할당한 도메인 이름. 응용형 CLB에는 이 필드가 적용되지 않음. |
| LoadBalancerVips.N | 아니요 | Array of String | 로드밸런서 인스턴스의 VIP 주소, 여러 개 지원. |
| BackendPublicIps.N | 아니요 | Array of String | 백 엔드 CVM의 공인 IP. |
| BackendPrivateIps.N | 아니요 | Array of String | 백 엔드 CVM의 사설 IP. |
| Offset | 아니요 | Integer | 데이터 오프셋, 기본값: 0. |
| Limit | 아니요 | Integer | 로드밸런서 인스턴스 반환 수량, 기본값: 20. |
| OrderBy | 아니요 | String | 정렬 필드, 지원하는 필드: LoadBalancerName, CreateTime, Domain, LoadBalancerType. |
| OrderType | 아니요 | Integer | 1: 내림차순, 0: 오름차순, 기본값: 생성 시간에 따라 내림차순. |
| SearchKey | 아니요 | String | 검색 필드, 이름, 도메인 이름, VIP에 대한 유사 매치 |
| ProjectId | 아니요 | Integer | 로드밸런서 인스턴스 속한 프로젝트 ID, DescribeProject API로 획득 가능. |
| WithRs | 아니요 | Integer | 조회한 로드밸런서가 RS와 바인딩 여부, 0: CVM을 바인딩하지 않음, 1: CVM을 바인딩함, -1: 전체 조회 |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| TotalCount | Integer | 필터링 조건을 만족시키는 로드밸런서 인스턴스의 총 수량. |
| LoadBalancerSet | Array of [LoadBalancer](/document/api/214/30694#LoadBalancer) | 반환된 로드밸런서 인스턴스 그룹. |
| RequestId | String | 유일한 요청 ID, 요청할 때마다 반환됨. 문재를 해결할 때, 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예시 1 로드밸런서 인스턴스에 따라 ID 조회

#### 입력 예시

```
https://clb.tencentcloudapi.com/?Action=DescribeLoadBalancers
&LoadBalancerIds.0=lb-6efswuxa
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "TotalCount": 1,
        "LoadBalancerSet": [
            {
                "LoadBalancerId": "lb-6efswuxa",
                "LoadBalancerName": "newlbname",
                "Forward": 1,
                "Domain": "",
                "LoadBalancerVips": [
                    "139.199.232.22"
                ],
                "LoadBalancerType": "OPEN",
                "Status": 1,
                "CreateTime": "2018-09-13 10:25:03",
                "StatusTime": "2018-09-13 10:45:55",
                "ProjectId": 0,
                "VpcId": "",
                "OpenBgp": 0,
                "Snat": false,
                "Isolation": 0,
                "Log": ""
            }
        ],
        "RequestId": "319412e1-8138-49a4-a128-a290641054c1"
    }
}
```

### 예시 2 로드밸런서 유형, 소속 프로젝트, 로드밸런서 이름, 로드밸런서 인스턴스에 따른vip 조회

#### 입력 예시

```
https://clb.tencentcloudapi.com/?Action=DescribeLoadBalancers
&LoadBalancerType=OPEN
&Forward=1
&ProjectId=0
&LoadBalancerName=newlbname
&LoadBalancerVips.0=139.199.232.22
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "TotalCount": 1,
        "LoadBalancerSet": [
            {
                "LoadBalancerId": "lb-6efswuxa",
                "LoadBalancerName": "newlbname",
                "Forward": 1,
                "Domain": "",
                "LoadBalancerVips": [
                    "139.199.232.22"
                ],
                "LoadBalancerType": "OPEN",
                "Status": 1,
                "CreateTime": "2018-09-13 10:25:03",
                "StatusTime": "2018-09-13 10:45:55",
                "ProjectId": 0,
                "VpcId": "",
                "OpenBgp": 0,
                "Snat": false,
                "Isolation": 0,
                "Log": ""
            }
        ],
        "RequestId": "cbe24464-5c73-4493-9943-f72306c6ac14"
    }
}
```

### 예시 3 백 엔드에 바인딩되고 사설 IP를 지정된 CVM의 로드밸런싱 조회

사설 IP가 10.186.225.251인 CVM의 로드밸런서 인스턴스 조회

#### 입력 예시

```
https://clb.tencentcloudapi.com/?Action=DescribeLoadBalancers
&WithRs=1
&BackendPrivateIps.0=10.186.225.25
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "TotalCount": 1,
        "LoadBalancerSet": [
            {
                "LoadBalancerId": "lb-o5z8mjxc",
                "LoadBalancerName": "atomtest",
                "Forward": 1,
                "Domain": "",
                "LoadBalancerVips": [
                    "139.199.232.90"
                ],
                "LoadBalancerType": "OPEN",
                "Status": 1,
                "CreateTime": "2017-11-13 10:37:43",
                "StatusTime": "2018-08-10 11:06:39",
                "ProjectId": 0,
                "VpcId": "",
                "OpenBgp": 0,
                "Snat": false,
                "Isolation": 1,
                "Log": ""
            }
        ],
        "RequestId": "5c51b1cb-88bf-4774-b671-436a59449c12"
    }
}
```

### 예시 4 이름, 도메인 이름, VIP 필드에 따라 로드밸런서 인스턴스 유사 조회

#### 입력 예시

```
https://clb.tencentcloudapi.com/?Action=DescribeLoadBalancers
&SearchKey=newlbname
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "TotalCount": 1,
        "LoadBalancerSet": [
            {
                "LoadBalancerId": "lb-6efswuxa",
                "LoadBalancerName": "newlbname",
                "Forward": 1,
                "Domain": "",
                "LoadBalancerVips": [
                    "139.199.232.22"
                ],
                "LoadBalancerType": "OPEN",
                "Status": 1,
                "CreateTime": "2018-09-13 10:25:03",
                "StatusTime": "2018-09-13 10:45:55",
                "ProjectId": 0,
                "VpcId": "",
                "OpenBgp": 0,
                "Snat": false,
                "Isolation": 0,
                "Log": ""
            }
        ],
        "RequestId": "1c9e2295-f5ef-48c0-847d-47a6d950578d"
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 인덱스 API 등의 기능을 제공하여, 클라우드 API의 어려움을 크게 줄일 수 있으므로 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=clb&Version=2018-03-17&Action=DescribeLoadBalancers)

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
| FailedOperation | 조작 실패 |
| InternalError | 내부 오류 |
| InvalidParameter | 매개변수 오류 | |
| InvalidParameterValue | 매개변수 값 오류 |
| UnauthorizedOperation | 권한이 없는 작업 |

