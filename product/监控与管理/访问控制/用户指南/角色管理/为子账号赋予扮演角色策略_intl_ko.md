역할 캐리어인 기본 계정은 서브 계정이 역할을 하는 것을 허용할 수 있습니다. 이제 사례를 통해 서브 계정에 역할 전략을 생성하고 역할을 부여하는 방법을 소개하도록 하겠습니다.

A사는 하나의 운영 엔지니어 일자리가 있는데 해당 일자리를 B사에 아웃소싱하려고 합니다. 해당 엔지니어직은 A사 광저우 지역의 모든 CVM 리소스를 관리해야 합니다.

A사 기업 계정은 CompanyExampleA(ownerUin은 12345)이고 역할을 생성하고 B사의 기업 계정 CompanyExampleB(ownerUin은 67890)를 역할 캐리어로 설정합니다. A사(CompanyExampleA)는 CreateRole API를 호출하여 DevOpsRole(역할 이름)이라는 역할을 생성하고 A사 기업 계정 CompanyExampleA는 생성된 역할 DevOpsRole에 권한을 부여합니다. 위의 절차는 [API를 통해 생성](https://intl.cloud.tencent.com/document/product/598/19381#.E9.80.9A.E8.BF.87-api-.E5.88.9B.E5.BB.BA)을 참조하십시오.

B사 기업 계정(CompanyExampleB)이 이 역할 권한을 부여받은 후 서브 계정 DevB에 해당 작업을 맡기려고 합니다. B사(CompanyExampleB)가 서브 계정 DevB에 A사(CompanyExampleA)의 역할 DevOpsRole을 신청할 수 있는 권한을 부여해야 합니다.

1. 전략 AssumeRole을 생성합니다. 예제는 다음과 같습니다.
```
{
	"version": "2.0",
	"statement": [{
		"effect": "allow",
		"action": ["name/sts:AssumeRole"],
		"resource": ["qcs::cam::uin/12345:roleName/DevOpsRole"]
	}]
}
```
2. 서브 계정 DevB에 해당 전략에 대한 권한을 부여합니다. 즉 서브 계정은 역할 DevOpsRole을 하는 권한을 부여받습니다.

약할 권한을 부여받은 후 역할을 사용하는 방법은 [역할 사용](https://intl.cloud.tencent.com/document/product/598/19419)을 참조하십시오.
