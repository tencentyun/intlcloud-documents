## 1. API 설명

API 요청 도메인 이름: as.tencentcloudapi.com.

본 API(CreateLaunchConfiguration)는 새로운 시동 구성 생성에 사용됩니다.

* 시동 구성, `ModifyLaunchConfigurationAttributes`를 통해 소량의 필드를 수정합니다. 새로운 시동 구성을 사용해야 하는 경우 시동 구성을 재생성하기를 권장합니다.

* 각 프로젝트는 최대 20개의 시동 구성만 생성할 수 있고 자세한 내용은 [사용 제한](https://cloud.tencent.com/document/product/377/3120)을 참조하십시오.


기본 API 요청 빈도 제한: 20회/초.

주의: 본 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 서로 연결되지 않기 때문에 공통 매개변수 Region이 금융 지역인 경우(예: ap-shanghai-fsi) 금융 지역을 포함한 지역명을 동시에 지정해야 하며 가장 좋은 것은 Region의 지역과 일치하는 것입니다. 예를 들어, as.ap-shanghai-fsi.tencentcloudapi.com입니다.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수와 일부 공통 매개변수만 나열합니다. 완전한 공통 매개변수 리스트는 [공통 매개변수](/document/api/377/20426)를 참조하십시오.

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, 본 API 값: CreateLaunchConfiguration |
| Version | 예 | String | 공통 매개변수, 본 API 값: 2018-04-19 |
| Region | 예 | String | 공통 매개변수, 세부 정보는 제품이 지원하는 [지역 리스트](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오 |
| LaunchConfigurationName | 예 | String | 시동 구성 표시 이름입니다. 이름은 중문, 영문, 숫자, 밑줄, 구분 기호 "-", 소수점만을 지원하고 60바이트를 초과할 수 없습니다. |
| ImageId | 예 | String | 유효한 [이미지](https://cloud.tencent.com/document/product/213/4940) ID 지정, 형식은 예를 들어 `img-8toqc6s3`과 같습니다. 이미지 유형은 4가지로 구분: <br/><li>공통 이미지</li><li> 사용자 지정 이미지</li><li>공유 이미지</li><li>서비스 마켓 이미지</li><br/>다음의 방식을 통해 사용 가능한 이미지 ID 획득: <br/><li>`공통 이미지`, `사용자 지정 이미지`, `공유 이미지`의 이미지 ID는 [콘솔](https://console.cloud.tencent.com/cvm/image?rid=1&imageType=PUBLIC_IMAGE)에 로그인하여 조회할 수 있습니다. `서비스 이미지 마켓`의 이미지 ID는 [클라우드 마켓](https://market.cloud.tencent.com/list)을 통해 조회합니다. </li><li>API [DescribeImages](https://cloud.tencent.com/document/api/213/15715)를 호출해 반환 정보 중 `ImageId` 필드를 불러옵니다.</li> |
| ProjectId | 아니요 | Integer | 인스턴스가 속한 프로젝트 ID입니다. 해당 매개변수는 [DescribeProject](https://cloud.tencent.com/document/api/378/4400)를 호출하여 반환값의 `projectId` 필드를 통해 획득할 수 있습니다. 입력하지 않으면 기본 프로젝트가 됩니다. |
| InstanceType | 아니요 | String | 인스턴스 모델. 서로 다른 인스턴스 모델은 서로 다른 리소스 사양을 지정하고 구체적인 값은 API [DescribeInstanceTypeConfigs](https://cloud.tencent.com/document/api/213/15749)를 호출하여 최신의 사양 리스트를 획득하거나 [인스턴스 유형](https://cloud.tencent.com/document/product/213/11518)의 설명을 참조하십시오. <br/>`InstanceType`과 `InstanceTypes` 매개변수는 상호 배타적이기 때문에 2가지 중 반드시 하나를 입력해야 하고 하나만을 입력할 수 있습니다. |
| SystemDisk | 아니요 | [SystemDisk](/document/api/377/20453#SystemDisk) | 인스턴스 시스템 디스크 설정 정보입니다. 해당 매개변수를 지정하지 않으면 시스템 기본값에 따라 할당합니다. |
| DataDisks.N | 아니요 | Array of [DataDisk](/document/api/377/20453#DataDisk) | 인스턴스 데이터 디스크 설정 정보입니다. 해당 매개변수를 설정하지 않으면 기본적으로 데이터 디스크를 구매하지 않습니다. 최대 11개 데이터 디스크 지정을 지원합니다. |
| InternetAccessible | 아니요 | [InternetAccessible](/document/api/377/20453#InternetAccessible) | 공중망 대역폭 관련 정보 설정입니다. 해당 매개변수를 지정하지 않으면 공중망 대역폭은 기본적으로 0Mbps입니다. |
| LoginSettings | 아니요 | [LoginSettings](/document/api/377/20453#LoginSettings) | 인스턴스 로그인 설정입니다. 해당 매개변수를 통해 인스턴스의 로그인 비밀번호나 키를 설정하거나 이미지의 기존 로그인 설정을 유지할 수 있습니다. 기본 상황에서 랜덤으로 비밀번호를 생성하고 내부 메시지를 통해 사용자에게 발송합니다. |
| SecurityGroupIds.아니요 | 아니요 | Array of String | 인스턴스가 속한 보안 그룹입니다. 해당 매개변수는 [DescribeSecurityGroups](https://cloud.tencent.com/document/api/215/15808)를 호출하여 반환된 값 중 `SecurityGroupId` 필드를 통해 획득할 수 있습니다. 해당 매개변수를 지정하지 않으면 기본적으로 보안 그룹을 바인딩하지 않습니다. |
| EnhancedService | 아니요 | [EnhancedService](/document/api/377/20453#EnhancedService) | 강화형 서비스입니다. 해당 매개변수를 통해 클라우드 보안, CM 등 서비스 활성화 여부를 지정할 수 있습니다. 해당 매개변수를 지정하지 않으면 기본적으로 CM, 클라우드 보안 서비스를 활성화합니다. |
| UserData | 아니요 | String | Base64로 인코딩된 사용자 지정 데이터, 길이는 16KB를 초과할 수 없습니다. |
| InstanceChargeType | 아니요 | String | 인스턴스 요금제, CVM은 기본적으로 POSTPAID_BY_HOUR를 채택합니다. <br/><br><li>POSTPAID_BY_HOUR: 시간에 따른 후불제<br/><br><li>SPOTPAID: 비딩 지불 |
| InstanceMarketOptions | 아니요 | [InstanceMarketOptionsRequest](/document/api/377/20453#InstanceMarketOptionsRequest) | 인스턴스의 마켓 관련 선택 사항, 예를 들어 스팟 인스턴스 관련 매개변수는 지정한 인스턴스의 지불 모드가 비딩 지불이면 해당 매개변수는 반드시 전달합니다. |
| InstanceTypes.N | 아니요 | Array of String | 인스턴스 모델 리스트, 서로 다른 인스턴스 모델은 서로 다른 리소스 사양을 지정하고 최대 5가지 인스턴스 모델을 지원합니다. <br/>`InstanceType`와 `InstanceTypes` 매개변수는 상호 배타적이기 때문에 2가지 중 반드시 하나를 입력해야 하고 하나만을 입력할 수 있습니다. |
| InstanceTypesCheckPolicy | 아니요 | String | 인스턴스 유형 검사 전략, 값은 ALL과 ANY를 포함하고 기본값은 ANY입니다. <br/><br><li> ALL, 모든 인스턴스 유형(InstanceType)이 사용 가능하면 검사를 통과하고 그렇지 않은 경우 검사 오류를 보고합니다. <br/><br><li> ANY, 임의 하나의 인스턴스 유형(InstanceType)이 사용 가능하면 검사를 통과하고 그렇지 않은 경우 검사 오류를 보고합니다. <br/><br/>인스턴스 유형을 사용할 수 없는 일반적인 원인은 해당 인스턴스 유형 매진, 대응하는 클라우드 디스크 매진 등이 포함됩니다. <br/> InstanceTypes 중 하나의 모델이 존재하지 않거나 오프라인이 된 경우, InstanceTypesCheckPolicy에서 어떤 값을 선택해도 검사 오류를 보고합니다. |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| LaunchConfigurationId | String | 본 API를 통해 시동 구성을 생성 시 해당 매개변수를 반환하고 시동 구성 ID를 나타냅니다. |
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예제 1 간단한 매개변수 생성

전달해야 하는 시동 구성 이름만 전달합니다. 인스턴스 모델, 이미지 ID, 기타는 모두 시스템 기본값을 적용하고 구체적인 구성은 다음과 같습니다. 시동 구성 이름은 as_test, 인스턴스 모델은 표준 2형 1C1G(S2.SMALL1), 이미지 ID는 img-8toqc6s3입니다.

#### 입력 예시

```
https://as.tencentcloudapi.com/?Action=CreateLaunchConfiguration
&LaunchConfigurationName=as_test
&InstanceType=S2.SMALL1
&ImageId=img-8toqc6s3
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "LaunchConfigurationId": "asc-23h37kyn",
        "RequestId": "d639dd64-9e46-4246-b13c-80954f81c11b"
    }
}
```

### 예제 2 상세한 매개변수 생성

시동 구성 이름: As_test, 이미지ID: Img-8toqc6s3, 선택한 모델: 표준2형 1C1G(S2.SMALL1). 시스템 디스크는 50G의 로컬 디스크, 데이터 디스크는 100G HDD 클라우드 디스크를 사용합니다. 공중망은 트래픽 기반 시간별 후불제를 적용하고 공중망 대역폭 상한은 5Mbps이며 공인 IP 할당, 키 선택하여 로그인, CM 및 클라우드 보안 설치를 수행합니다.

#### 입력 예시

```
https://as.tencentcloudapi.com/?Action=CreateLaunchConfiguration
&LaunchConfigurationName=as_test
&ImageId=img-8toqc6s3
&InstanceType=S2.SMALL1
&SystemDisk.DiskType=LOCAL_BASIC
&SystemDisk.DiskSize=50
&DataDisks.0.DiskType=CLOUD_BASIC
&DataDisks.0.DiskSize=100
&InternetAccessible.InternetChargeType=TRAFFIC_POSTPAID_BY_HOUR
&InternetAccessible.InternetMaxBandwidthOut=5
&InternetAccessible.PublicIpAssigned=TRUE
&LoginSettings.KeyIds.0=skey-k8eypc1l
&EnhancedService.SecurityService.Enabled=TRUE
&EnhancedService.MonitorService.Enabled=TRUE
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "LaunchConfigurationId": "asc-fdz8j7dh",
        "RequestId": "9a7209d3-2260-49d7-952a-dfa2001f8822"
    }
}
```

### 예제 3 스팟 인스턴스 구성 생성

시동 구성 이름: spot-test, 모델: 표준 2형 2C4G(S2.MEDIUM4), 요금제는 비딩 지불(SPOTPAID)로 설정하고 최고 비딩가는 0.99CNY/시간입니다.

#### 입력 예시

```
https://as.tencentcloudapi.com/?Action=CreateLaunchConfiguration
&LaunchConfigurationName=spot-test
&InstanceType=S2.MEDIUM4
&ImageId=img-8toqc6s3
&SystemDisk.DiskType=CLOUD_PREMIUM
&SystemDisk.DiskSize=50
&InternetAccessible.InternetChargeType=TRAFFIC_POSTPAID_BY_HOUR
&InternetAccessible.InternetMaxBandwidthOut=20
&InternetAccessible.PublicIpAssigned=true
&InstanceChargeType=SPOTPAID
&InstanceMarketOptions.MarketType=spot
&InstanceMarketOptions.SpotOptions.MaxPrice=0.99
&InstanceMarketOptions.SpotOptions.SpotInstanceType=one-time
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "LaunchConfigurationId": "asc-hpzwe3o2",
        "RequestId": "ccfe3052-e9c9-47ee-bf3d-5bc2dfd972c0"
    }
}
```

### 예제 4 시동 구성 생성, 여러 인스턴스 모델 지원

2가지 인스턴스 모델을 지원하고 각각 S2.SMALL2와 S2.SMALL4입니다.

#### 입력 예시

```
https://as.tencentcloudapi.com/?Action=CreateLaunchConfiguration
&LaunchConfigurationName=multi_instance_types
&InstanceTypes.0=S2.SMALL2
&InstanceTypes.1=S2.SMALL4
&ImageId=img-8toqc6s3
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "LaunchConfigurationId": "asc-77mh1cho",
        "RequestId": "2864c860-27a0-439e-a1e1-0003b76734e7"
    }
}
```


## 5. 개발자 리소스

### API Explorer

**해당 도구는 온라인 호출, 서명 인증, SDK 코드 생성과 빠른 검색 API 등 기능을 제공하고 클라우드 API 사용 난이도를 대폭 낮춰 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=CreateLaunchConfiguration)

### SDK

클라우드 API 3.0은 일체화된 SDK를 제공하고 여러 종류의 프로그래밍 언어를 지원하여 편리하게 API를 호출할 수 있습니다.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. 오류 코드

다음은 API 비즈니스 로직과 관련된 오류 코드만 나열하며 다른 오류 코드는 [공통 오류 코드](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)를 참조하십시오.

| 오류 코드 | 설명 |
|---------|---------|
| AccountQualificationRestrictions | 해당 요청 계정은 자격 심사를 통과하지 못했습니다. |
| CallCvmError | CVM API 호출 실패. |
| InvalidImageId.NotFound | 해당 이미지를 찾지 못했습니다. |
| InvalidLaunchConfiguration.NameDuplicate | 시동 구성 이름 중복. |
| InvalidParameter.Conflict | 매개변수 충돌. 지정한 여러 매개변수가 충돌해 동시에 존재할 수 없습니다. |
| InvalidParameter.MustOneParameter | 매개변수 결함. 두 개의 매개변수 중 반드시 하나를 지정해야 합니다. |
| InvalidParameterValue.CvmConfigurationError | CVM 매개변수 검사에 이상이 생겼습니다. |
| InvalidPermission | 계정이 해당 작업을 지원하지 않습니다. |
| LaunchConfigurationQuotaLimitExceeded | 시동 구성 할당량이 한도를 초과했습니다. |

