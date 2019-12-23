Tencent Cloudでは、CAM APIを使用して新しいロールを使用することができます。APIを使用してロールを使用する方法を簡単に理解するために、典型的なケースを使用します。

次のシナリオを想定すると、会社Aは保守管理エンジニアのポジションを持ち、そのポジションを会社Bにアウトソーシングしたいと考えています。このポジションでは、会社A広州地域のすべてのCVMリソースを操作する必要があります。

会社Aの企業アカウントCompanyExampleA（ownerUinは12345）、ロールを作成し、ロールキャリアを会社Bの企業アカウントCompanyExampleB（ownerUinは67890）に設定します。会社A（CompanyExampleA）はCreateRole APIを呼び出して、ロール名（roleName）がDevOpsRoleであるロールを作成し、会社Aの企業アカウントCompanyExampleAは、作成されたロールに権限を付与します。上記の手順については、[APIで作成](https://intl.cloud.tencent.com/document/product/598/19381#.E9.80.9A.E8.BF.87-api-.E5.88.9B.E5.BB.BA)を参照してください。

企業アカウントCompanyExampleBにこのロールを付与された後、サブアカウントDevBがその仕事をすることが望まれます。会社B（CompanyExampleB）は、DevBがCompanyExampleAのロールであるDevOpsRoleを申請できることを承認します。上記の手順については、[サブアカウントにロールポリシーを付与](https://intl.cloud.tencent.com/document/product/598/19422)を参照してください。

上記のロールの作成、承認を完了し、サブアカウントにロールポリシーを付与した後、サブアカウントDevBはそのロールの使用を開始できます。

1. ロールDevOpsRoleの一時的認証情報を申請するために、[AssumeRole](https://intl.cloud.tencent.com/document/product/598/13895) APIを呼び出す必要があります。入力パラメータは以下のとおりです。 
```
roleArn=qcs::cam::uin/12345:roleName/DevOpsRole，
roleSessionName=DevBAssumeTheRole，
durationSeconds=7200
```
2. APIは次のように結果を成功的に返しました。 
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
3. DevBがロールの一時的認証情報を取得したら、認証情報の有効期限内に権限範囲内で操作を実行できます。例えば、APIを介してCVMリストを確認するために、[DescribeInstances](https://cloud.tencent.com/document/product/213/15728) APIを呼び出すときに、API暗号鍵SecretIdおよびSecretKeyの値をtmpSecretIdおよびtmpSecretKeyに置き換えます。同時に、[共通パラメータ](https://cloud.tencent.com/document/api/213/15692)のTokenをsessionTokenの値に設定します。会社B（CompanyExampleB）は、そのロールの一時的認証情報を直接申請して、会社A（CompanyExampleA）のリソースを操作することもできます。
>**注意：**
>会社A（CompanyExampleA）が会社B（CompanyExampleB）の承認を終了しようとする場合は、ロールDevOpsRoleを削除します。


