역할을 생성하려면 CAM 콘솔을 통해 생성 또는 CAM API를 통해 생성과 같은 두 가지 방법이 있습니다. 역할을 생성하는 구체적인 절차는 역할 생성 대상, 즉 Tencent Cloud 계정, Tencent Cloud 제품 서비스 또는 ID 공급업체에 따라 다릅니다.

## 콘솔을 통해 생성

### Tencent Cloud 기본 계정에 대한 역할 생성
1. CAM 콘솔에 로그인하고 [역할 관리](https://console.cloud.tencent.com/cam/role) 페이지로 이동합니다.
2. [역할 생성]을 클릭하여 [역할 캐리어 선택]을 한 다음 [Tencent Cloud 계정]을 역할 캐리어로 선택합니다.
3. [계정 ID] 확인란에 역할을 하여 Tencent Cloud 리소스에 대한 접근이 허용된 기본 계정 ID를 입력합니다. 기본값은 귀하의 기본 계정 ID입니다.
다른 Tencent Cloud 서브 계정에 역할을 부여하려면 [서브 사용자에게 역할 전략 부여](https://intl.cloud.tencent.com/document/product/598/19422)를 참조하십시오.
4. 전략 리스트에서 현재 생성된 역할에 부여할 전략을 선택하여 역할 권한 구성을 완료합니다.
5. 역할 이름을 입력하고 생성할 역할에 대한 정보를 확인한 다음 [완성]을 클릭하여 사용자 지정 역할 생성을 완료합니다.

### Tencent Cloud 제품 서비스에 대한 역할 생성
1. CAM 콘솔에 로그인하고 [역할 관리](https://console.cloud.tencent.com/cam/role) 페이지로 이동합니다.
2. [역할 생성]을 클릭하고 [역할 캐리어 선택]을 한 다음 [Tencent Cloud 제품 서비스]를 역할 캐리어로 선택합니다.
Tencent Cloud 제품 서비스가 서비스 역할 사용을 지원하는지 확인하려면 [CAM을 지원하는 클라우드 서비스](https://intl.cloud.tencent.com/document/product/598/10588)를 참조하십시오.
3. 역할 맡기를 지원하는 서비스 제품 리스트에서 역할 캐리어로 필요한 서비스를 선택합니다.
4. 전략 리스트에서 기존 역할에 추가할 전략을 선택하여 역할에 대한 전략을 구성합니다.
5. 역할 이름을 입력하고 생성할 역할에 대한 정보를 확인한 다음 [완성]을 클릭하여 사용자 지정 역할 생성을 완료합니다.

### ID 공급업체에 대한 역할 생성
1. CAM 콘솔에 로그인하고 [역할 관리](https://console.cloud.tencent.com/cam/role) 페이지로 이동합니다.
2. [역할 생성]을 클릭하고 [역할 캐리어 선택]을 한 다음 [ID 공급업체]를 역할 캐리어로 선택합니다.
[ID 공급업체]란 성공적으로 생성된 ID 공급업체를 의미하며 그 중에서 이번에 역할 생성 대상을 선택합니다.
3. (옵션)[콘솔 접근]에서 역할이 Tencent Cloud 관리 콘솔에 로그인할 수 있는지를 관리할 수 있습니다. 역할은 기본적으로 프로그래밍을 통해 Tencent Cloud에 접근할 수 있습니다.
4.	(옵션)[사용 조건]에서 ID 공급업체가 해당 역할을 사용하는 조건을 관리할 수 있습니다.
> 현재 지원되는 조건은 다음과 같습니다.
>  - saml: aud: 수신자. SAML 어설션이 제출된 터미널 노드 URL. 이 키의 값은 Audience 필드가 아니라 어설션의 SAML Recipient 필드에서 가져온 것입니다.
>  - saml: iss: 발신자(URN으로 표시). 이 키의 값은 어설션의 SAML Issuer 필드에서 가져온 것입니다.
>  - saml: sub: 외부 계정 ID. 이는 스테이트먼트 주제이며 조직의 사용자를 유일하게 식별하는 값을 포함합니다. 이 키는 어설션의 SAML NameID 필드에서 가져온 것입니다.
>  - saml: sub_type: 외부 사용자 유형. 이 키는 어설션의 SMAL NameID의 Format 속성에서 가져온 것입니다.
5.	전략 리스트에서 현재 역할에 추가할 전략을 선택하고 역할에 대한 권한 구성을 완료합니다.
6.	사용자 지정 역할 이름을 입력하고 [참고]에 이 역할에 대한 메모 정보를 입력할 수 있습니다.
7.	생성할 역할에 대한 정보를 확인하고 [완료]를 클릭하여 사용자 지정 역할 생성을 완료합니다.

## API를 통해 생성

### Tencent Cloud 계정에 대한 역할 생성

Tencent Cloud에서 CAM API를 사용하여 새 역할을 생성할 수 있습니다. 이제 사례를 통해 API로 역할을 생성하는 방법을 소개합니다.

A사는 하나의 운영 엔지니어 일자리가 있는데 해당 일자리를 B사에 아웃소싱하려고 합니다. 해당 엔지니어직은 A사 광저우 지역의 모든 CVM 리소스를 관리해야 합니다.

A사 기업 계정은 CompanyExampleA(ownerUin은 12345임) 역할을 생성하고 B사의 기업 계정 CompanyExampleB(ownerUin은 67890임)를 역할 캐리어로 설정합니다.

1. A사 기업 계정 CompanyExampleA(ownerUin은 12345)는 CreateRole API를 호출하여 DevOpsRole이라는 이름으로 역할을 생성하고 policyDocument(역할 신뢰 전략) 매개변수가 다음과 같습니다.
```
{
	"version": "2.0",
	"statement": [{
		"action": "name/sts:AssumeRole",
		"effect": "allow",
		"principal": {
			"qcs": ["qcs::cam::uin/67890:root"]
		}
	}]
}
```

2. A사 기업 계정 CompanyExampleA(ownerUin은 12345)는 생성한 역할에 대해 권한을 추가해야 합니다.
 1. A사 기업 계정 CompanyExampleA(ownerUin은 12345)는 전략 DevOpsPolicy를 생성합니다. 전략 구문은 다음과 같습니다.
```
{
	"version": "2.0",
	"statement": [{
		"effect": "allow",
		"action": "cvm:*",
		"resource": "qcs::cvm:ap-guangzhou::*"
	}]
}
```
 2. A사 기업 계정 CompanyExampleA(ownerUin은 12345)는 [AttachRolePolicy](https://intl.cloud.tencent.com/document/product/598/13889)를 호출하여 단계 1에서 생성한 전략을 역할 DevOpsRole에 바인딩하고 입력 매개변수는 policyName=DevOpsPolicy, roleName=DevOpsRole입니다.

위의 절차를 걸쳐 A사 기업 계정 CompanyExampleA(ownerUin 은 12345)는 역할 생성 및 권한 부여를 마칩니다.

### ID 공급업체에 대한 역할 생성

ID 공급업체에게 역할을 생성하기 전에 CAM에서 SAML ID 공급업체를 생성해야 합니다. SAML ID 공급업체 생성은 [SAML ID 공급업체 생성]()을 참조하십시오.

1. 생성할 역할에게 신뢰 전략을 준비합니다.
> 신뢰 전략의 각 필드는 다음과 같이 지정됩니다.
>  - action 필드: SAML 페더레이션 ID가 현재 역할을 사용할 수 있는 API를 정의합니다. `sts: AssumeRoleWithSAML`이 사용됩니다.
>  - principal 필드: 현재 역할을 사용할 수 있는 ID 공급업체를 정의합니다. `{"federated": [ IdPArn ]}` 문자열이 사용됩니다. 예: qcs::cam::uin/10001:saml-provider/idp_name
>  - condition 필드: 현재 역할을 사용할 수 있는 조건을 정의합니다. 기본적으로 `{"StringEquals": {"SAML:aud": "https://cloud.tencent.com/login/saml"}}`이 사용됩니다. 이 조건에 따라 SAML 페더레이션 터미널 노드가 Tencent Cloud인 ID 공급업체만 이 역할을 사용할 수 있습니다.

 역할 신뢰 전략의 예제는 다음과 같습니다.
```
{
  "version": "2.0",
  "statement": [
    {
      "action": "name/sts:AssumeRoleWithSAML",
      "effect": "allow",
      "principal": {
        "federated": [
          "qcs::cam::uin/10001:saml-provider/idp_name"
        ]
      },
      "condition": {
        "string_equal": {
          "saml:aud": "https://cloud.tencent.com/login/saml"
        }
      }
    }
  ]
}
```

2.	생성할 역할에게 권한 전략을 준비합니다. 권한 전략에 대해서는 [전략](https://intl.cloud.tencent.com/document/product/598/10601)을 참조하십시오.
3.	[cam: CreateRole](https://cloud.tencent.com/document/api/598/13886) API를 호출하여 ID 공급업체 역할을 생성합니다.
