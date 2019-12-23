ロールキャリアとしてのメインアカウントは、そのサブアカウントがそのロールを果たすことを許可します。ここでは、サブアカウントにロールのポリシーを作成および付与する方法を簡単に理解するためにケースを使用します。

次のシナリオを想定すると、会社Aは保守管理エンジニアのポジションを持ち、そのポジションを会社Bにアウトソーシングしたいと考えています。このポジションでは、会社A広州地域のすべてのCVMリソースを操作する必要があります。

会社Aの企業アカウントCompanyExampleA（ownerUinは12345）、ロールを作成し、ロールキャリアを会社Bの企業アカウントCompanyExampleB（ownerUinは67890）に設定します。会社A（CompanyExampleA）はCreateRole APIを呼び出して、ロール名（roleName）がDevOpsRoleであるロールを作成し、会社Aの企業アカウントCompanyExampleAは、作成されたロールDevOpsRoleに権限を付与します。上記の手順については、[APIで作成](https://intl.cloud.tencent.com/document/product/598/19381#.E9.80.9A.E8.BF.87-api-.E5.88.9B.E5.BB.BA)を参照してください。

会社Bの企業アカウント（CompanyExampleB）にこのロールを付与された後、サブアカウントDevBがその仕事をすることが望まれます。会社B（CompanyExampleB）は、会社A（CompanyExampleA）のロールDevOpsRoleを申請するために、サブアカウントDevBに権限を付与する必要があります。

1. ポリシーAssumeRoleを作成します。例は次のとおりです。
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
2. サブアカウントDevBに該当ポリシーを付与すると、サブアカウントには、ロールDevOpsRoleの権限が与えられています。

ロールを取得した後ロールを使用する方法については、[ロールの使用](https://intl.cloud.tencent.com/document/product/598/19419)を参照してください。


