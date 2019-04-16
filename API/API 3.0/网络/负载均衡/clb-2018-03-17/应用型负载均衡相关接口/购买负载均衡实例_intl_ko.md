## 1. API 설명

API 요청 도메인 이름: clb.tencentcloudapi.com.

CreateLoadBalancer API는 로드밸런서 인스턴스를 생성하는 데 사용됩니다. CLB를 사용하려면 하나 이상의 로드밸런서 인스턴스를 구매해야 합니다. 해당 API를 성공적으로 호출하면 로드밸런서 인스턴스의 유일한 ID를 반환하게 됩니다. 사용자가 구매할 수 있는 로드밸런서 인스턴스 유형은 공중망(응용형), 사설망(응용형)으로 나뉩니다. 제품 설명의 제품 유형을 참조할 수 있습니다.
이 API 반환에 성공하면 로드밸런서 인스턴스 조회 리스트 API(DescribeLoadBalancers)로 로드밸런서 인스턴스의 상태를 조회해 생성 성공 여부를 확인할 수 있습니다.

기본적 API 요청 빈도 제한: 20회/초.

주의: 이 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 있고 서로 통하지 않아서, 공통 매개변수 Region이 금융 지역 도메인(예: ap-shanghai-fsi)일 경우, 금융 지역의 도메인 이름을 동시에 지정해야 하며, Region의 도메인과 일치시키는 것이 가장 좋습니다. 예: clb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수 및 일부 공통 매개변수만 나열되며, 완전한 공통 매개변수 리스트는 [공통 요청 매개변수](/document/api/214/30670)를 참조하십시오.

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, API 값: CreateLoadBalancer |
| Version | 예 | String | 공통 매개변수, API 값: 2018-03-17 |
| Region | 예 | String | 공통 매개변수, 세부 정보는 [지역 리스트](/document/api/214/30670#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오.
| LoadBalancerType | 예 | String | 로드밸런서 인스턴스의 네트워크 유형<br/>OPEN: 공중망 속성, INTERNAL: 사설망 속성. |
| Forward | 아니요 | Integer | 로드밸런서 인스턴스. 1: 응용형, 0: 전통형. 기본값: 응용형 로드밸런서 인스턴스 |
| LoadBalancerName | 아니요 | String | 로드밸런서 인스턴스의 이름으로 1개를 생성할 때 적용됩니다. 규칙: 1-50자 영문, 한글, 숫자, 연결선 "-" 또는 밑줄 "_"을 사용합니다.<br/>주의: 이름이 기존 로드밸런서 인스턴스와 중복될 경우, 시스템은 이번 생성한 로드밸런서 인스턴스 이름을 자동으로 생성합니다. |
| VpcId | 아니요 | String | CLB 백 엔드 인스턴스 소속 네트워크 ID로 DescribeVpcEx API를 통해 획득할 수 있습니다. 입력하지 않으면 기본 네트워크로 간주됩니다. |
| SubnetId | 아니요 | String | VPC에서 사설망 로드밸런서 인스턴스를 구매할 때에는 서브넷 ID를 지정해야 하며, 사설망 로드밸런서 인스턴스의 VIP는 이 서브넷에서 생성됩니다. 기타 상황에서는 해당 필드를 입력할 필요가 없습니다.|
| ProjectId | 아니요 | Integer | 로드밸런서 인스턴스 소속 항목 ID로 DescribeProject API를 통해 획득할 수 있습니다. 입력하지 않으면 기본 프로젝트에 속하게 됩니다. |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| LoadBalancerIds | Array of String | 로드밸런서 인스턴스 통일 ID로 구성한 배열.|
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예시 1 공중망 응용형 LB 인스턴스 1개 생성

#### 입력 예시

```
https://clb.tencentcloudapi.com/?Action=CreateLoadBalancer
&LoadBalancerType=OPEN
&Forward=1
&LoadBalancerName=test
&ProjectId=0
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "LoadBalancerIds": [
            "lb-6efswuxa"
        ],
        "RequestId": "9b3f0b57-fb64-4918-8dd6-ce02604fb52c"
    }
}
```

### 예시 2 사설망 응용형 LB 인스턴스 1개 생성

#### 입력 예시

```
https://clb.tencentcloudapi.com/?Action=CreateLoadBalancer
&LoadBalancerType=INTERNAL
&Forward=1
&LoadBalancerName=test_internal
&VpcId=vpc-30xqxt9p
&SubnetId=subnet-k57djpow
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "LoadBalancerIds": [
            "lb-kmfrnqci"
        ],
        "RequestId": "7ffa6830-cd1b-4bc4-8e24-1688885f594a"
    }
}
```


## 5. 개발자 리소스

### API Explorer

**이 도구는 온라인 호출, 서명 인증, SDK 코드 생성 및 빠른 인덱스 API 등의 기능을 제공하여, 클라우드 API의 어려움을 크게 줄일 수 있으므로 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=clb&Version=2018-03-17&Action=CreateLoadBalancer)

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

