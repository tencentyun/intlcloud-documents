## 1. API 설명

API 요청 도메인 이름: as.tencentcloudapi.com.

본 API(ModifyLaunchConfigurationAttributes)는 시동 구성 일부 속성 수정에 사용됩니다.

* 시동 구성 수정 후 해당 시동 구성을 사용하여 이미 확장한 기존 인스턴스는 변경하지 않고 그 후 해당 시동 구성을 적용한 새로 추가된 인스턴스는 새로운 구성에 따라 확장됩니다. 
* 본 API는 일부 간단한 유형의 수정을 지원합니다.

기본 API 요청 빈도 제한: 20회/초.

주의: 본 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 서로 연결되지 않기 때문에 공통 매개변수 Region이 금융 지역인 경우(예: ap-shanghai-fsi) 금융 지역을 포함한 지역명을 동시에 지정해야 하며 가장 좋은 것은 Region의 지역과 일치하는 것입니다. 예를 들어, as.ap-shanghai-fsi.tencentcloudapi.com입니다.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수와 일부 공통 매개변수만 나열합니다. 완전한 공통 매개변수 리스트는 [공통 매개변수](/document/api/377/20426)를 참조하십시오.

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, 본 API 값: ModifyLaunchConfigurationAttributes |
| Version | 예 | String | 공통 매개변수, 본 API 값: 2018-04-19 |
| Region | 예 | String | 공통 매개변수, 세부 정보는 제품이 지원하는 [지역 리스트](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오 |
| LaunchConfigurationId | 예 | String | 시동 구성 ID |
| ImageId | 아니요 | String | 유효한 [이미지](https://cloud.tencent.com/document/product/213/4940) ID 지정, 형식은 예를 들어 `img-8toqc6s3`과 같습니다. 이미지 유형은 4가지로 구분: <br/><li>공통 이미지</li><li>사용자 지정 이미지</li><li>공유 이미지</li><li>서비스 마켓 이미지</li><br/>다음의 방식을 통해 사용 가능한 이미지 ID를 획득할 수 있습니다. <br/><li>`공통 이미지 `, `사용자 지정 이미지`, `공유 이미지`의 이미지 ID는 [콘솔](https://console.cloud.tencent.com/cvm/image?rid=1&imageType=PUBLIC_IMAGE)에 로그인하여 조회할 수 있습니다. `서비스 이미지 마켓`의 이미지 ID는 [클라우드 마켓](https://market.cloud.tencent.com/list)을 통해 조회합니다. </li><li>API [DescribeImages](https://cloud.tencent.com/document/api/213/15715)를 호출해 반환 정보 중 `ImageId` 필드를 불러옵니다.</li> |
| InstanceTypes.N | 아니요 | Array of String | 인스턴스 유형 리스트, 서로 다른 인스턴스 모델은 서로 다른 리소스 사양을 지정하고 최대 5가지의 인스턴스 모델을 지원합니다. <br/>시동 구성, InstanceType을 통해 단일한 인스턴스 유형을 나타내고 InstanceTypes를 통해 다중 인스턴스 유형을 표시합니다. 지정된 InstanceTypes를 성공적으로 시동 구성한 후 기존의 InstanceType은 자동으로 무효화됩니다. |
| InstanceTypesCheckPolicy | 아니요 | String | 인스턴스 유형 검사 전략, InstanceTypes를 수정 시 사용되며 가능한 값은 ALL과 ANY를 포함하고 기본값은 ANY입니다.<br/><br><li> ALL, 모든 인스턴스 유형(InstanceType)이 사용 가능하면 검사를 통과하고 그렇지 않은 경우 검사 오류를 보고합니다.<br/><br><li> ANY, 임의 하나의 인스턴스 유형(InstanceType)이 사용 가능하면 검사를 통과하고 그렇지 않은 경우 검사 오류를 보고합니다.<br/><br/>인스턴스 유형을 사용할 수 없는 일반적인 원인은 해당 인스턴스 유형 매진, 대응하는 클라우드 디스크 매진 등이 포함됩니다.<br/>InstanceTypes 중 하나의 모델이 존재하지 않거나 오프라인이 된 경우, InstanceTypesCheckPolicy에서 어떤 값을 선택해도 검사 오류를 보고합니다. |
| LaunchConfigurationName | 아니요 | String | 시동 구성 표시 이름입니다. 이름은 중문, 영문, 숫자, 밑줄, 구분 기호 "-", 소수점만을 지원하고 60바이트를 초과할 수 없습니다. |
| UserData | 아니요 | String | Base64로 인코딩된 사용자 지정 데이터, 길이는 16KB를 초과할 수 없습니다. UserData를 지우고 싶다면, 이를 빈 문자열로 지정합니다. |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예제 1 시동 구성 지정, 이미지, 인스턴스 유형, 이름 수정

#### 입력 예시

```
https://as.tencentcloudapi.com/?Action=ModifyLaunchConfigurationAttributes
&LaunchConfigurationId=asc-291kq6ku
&ImageId=img-8toqc6s3
&InstanceTypes.0=S2.SMALL1
&LaunchConfigurationName=updated_config
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "RequestId": "07022dcb-5bba-48f0-a2b0-800ad006d031"
    }
}
```

### 예제 2 UserData 지우기

#### 입력 예시

```
https://as.tencentcloudapi.com/?Action=ModifyLaunchConfigurationAttributes
&LaunchConfigurationId=asc-291kq6ku
&UserData=
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "RequestId": "2c027f22-3a3b-489a-a77a-89c53fc15212"
    }
}
```


## 5. 개발자 리소스

### API Explorer

**해당 도구는 온라인 호출, 서명 인증, SDK 코드 생성과 빠른 검색 API 등 기능을 제공하고 클라우드 API 사용 난이도를 대폭 낮춰 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=ModifyLaunchConfigurationAttributes)

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
| InvalidParameterValue.CvmConfigurationError | CVM 매개변수 검사에 이상이 생겼습니다. |

