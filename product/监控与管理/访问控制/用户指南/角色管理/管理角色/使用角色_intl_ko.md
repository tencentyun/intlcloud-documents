Tencent Cloud에서 CAM API를 사용하여 역할을 사용할 수 있습니다. 이제 사례를 통해 API로 역할을 사용하는 방법을 소개합니다.

A사는 하나의 운영 엔지니어 일자리가 있는데 해당 일자리를 B사에 아웃소싱하려고 하합니다. 해당 엔지니어직은 A사 광저우 지역의 모든 CVM 리소스를 관리해야 합니다.

A사 기업 계정은 CompanyExampleA(ownerUin은 12345)입니다. 역할을 생성하고 B사의 기업 계정 CompanyExampleB(ownerUin은 67890)를 역할 캐리어로 설정합니다. A사(CompanyExampleA)는 CreateRole API를 호출하여 DevOpsRole(역할 이름)이라는 역할을 생성하고 A사 기업 계정 CompanyExampleA가 생성된 역할에게 권한을 부여합니다. 위의 절차는 [API 를 통해 생성](https://intl.cloud.tencent.com/document/product/598/19381#.E9.80.9A.E8.BF.87-api-.E5.88.9B.E5.BB.BA)을 참조하십시오.

기업 계정 CompanyExampleB가 이 역할의 권한을 부여받은 후 해당 작업을 서브 계정 DevB에 맡기려고 합니다. B사(CompanyExampleB)는 DevB에 CompanyExampleA의 역할인 DevOpsRole을 신청하는 권한을 부여합니다. 위의 절차는 [서브 계정에 역할 전략 부여](https://intl.cloud.tencent.com/document/product/598/19422)를 참조하십시오.

위의 역할 생성, 권한 부여 작업을 마치고 서브 계정에 역할 전략을 부여한 후 서브 계정 DevB는 역할 사용을 시작할 수 있습니다.

1. 역할 DevOpsRole에 대한 임시 자격 증명을 신청하려면 [AssumeRole](https://intl.cloud.tencent.com/document/product/598/13895) API를 호출해야 합니다. 입력 매개변수는 다음과 같습니다.
```
roleArn=qcs::cam::uin/12345:roleName/DevOpsRole，
roleSessionName=DevBAssumeTheRole，
durationSeconds=7200
```
2. 이 API는 다음과 같은 결과를 성공적으로 리턴합니다.
```
{
	"credentials": {
		"sessionToken": "5e776c4216ff4d31a7c74fe194a978a3ff2a42864",
		"tmpSecretId": "AKIDcAZnqgar9ByWq6m7ucIn8LNEuY2MkPCl",
		"tmpSecretKey": "VpxrX0IMCpHXWL0Wr3KQNCqJix1uhMqD"
	},
	"expiredTime": 1506433269,
	"expiration": "2018-09-26T13:41:09Z"
}
```
3. DevB가 역할의 임시 자격 증명을 획득한 후, 자격 증명의 유효 기간 내에 권한 받은 작업을 수행할 수 있습니다. 예를 들면 API를 통해 CVM 리스트를 확인하려면 [DescribeInstances](https://cloud.tencent.com/document/product/213/15728) API를 호출할 때 API 키 SecretId 및 SecretKey의 값을 tmpSecretId 및 tmpSecretKey의 값으로 바꾸며 동시에 [공통 매개변수](https://cloud.tencent.com/document/api/213/15692)의 토큰을 sessionToken의 값으로 설정합니다. B사(CompanyExampleB)는 역할의 임시 자격 증명을 직접 신청하여 A사(CompanyExampleA)의 리소스를 조작할 수도 있습니다.
>**주의: **
>A사(CompanyExampleA)가 B사(CompanyExampleB)에 부여한 권한을 종료하려면 역할 DevOpsRole을 삭제하면 됩니다.
