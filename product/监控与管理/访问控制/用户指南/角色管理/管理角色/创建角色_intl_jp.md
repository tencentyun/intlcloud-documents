ロールを作成する方法は2つあります。CAMコンソールまたはCAM APIを使用することができます。ロールを作成する具体的な手順は、Tencent Cloudアカウント、Tencent Cloud製品サービス、またはIDプロバイダーのいずれかにロールを作成するかによって若干異なります。

##　コンソールで作成

###　Tencent Cloudメインアカウント用のロールを作成
1. アクセス管理（CAM）コンソールにログインして、[ロール管理](https://console.cloud.tencent.com/cam/role)ページに移動します。
2. 【ロールの作成】をクリックし、【ロールキャリアの選択】を実行して、ロールキャリアとして【Tencent Cloudアカウント】を選択します。
3. ロールとしてTencent Cloudリソースへのアクセスが許可されるメインアカウントIDを【アカウントID】ボックスに入力します。デフォルトはメインアカウントIDを入力します。
他のTencent Cloudサブアカウントにロールを付与したい場合は、[サブユーザーにロールポリシーを付与](https://intl.cloud.tencent.com/document/product/598/19422)を参照してください。
4. ロール権限構成を完了するために、ポリシーリストで、現在作成されているロールに付与するポリシーを選択します。
5. ロール名を入力し、作成しようとしているロールに関する情報を確認し、【完了】をクリックしてカスタムロールの作成を完了します。

###　Tencent Cloud製品サービス用のロールを作成
1. アクセス管理（CAM）コンソールにログインして、[ロール管理](https://console.cloud.tencent.com/cam/role)ページに移動します。
2. 【ロールの作成】をクリックし、【ロールキャリアの選択】を実行して、ロールキャリアとして【Tencent Cloud製品サービス】を選択します。
Tencent Cloud製品サービスがサービスロールの使用をサポートしているかどうかを確認するために、[CAMをサポートするクラウドサービス](https://intl.cloud.tencent.com/document/product/598/10588)を参照してください。
3. ロール機能をすでにサポートしているサービス製品のリストで、ロールキャリアとして必要なサービスを選択します。
4. ロールのポリシーを構成するために、ポリシーリストで、現在ロールに追加するポリシーを選択します。
5. ロール名を入力し、作成しようとしているロールに関する情報を確認し、【完了】をクリックしてカスタムロールの作成を完了します。

###　IDプロバイダー用のロールを作成
1. アクセス管理（CAM）コンソールにログインして、[ロール管理](https://console.cloud.tencent.com/cam/role)ページに移動します。
2. 【ロールの作成】をクリックし、【ロールキャリアの選択】を実行して、ロールキャリアとして【IDプロバイダー】を選択します。
【IDプロバイダー】は、正常に作成されたIDプロバイダーを意味し、今度はロールを作成するIDプロバイダーを選択します。
3. （オプション）【コンソールアクセス】で、ロールがTencent Cloud管理コンソールへのログインを許可するかどうかを管理できます。ロールはデフォルトでプログラミングによってTencent Cloudにアクセス可能です。
4.	（オプション）【使用条件】で、IDプロバイダーがロールを使用する条件を管理できます。
>　現在サポートされている条件は次のとおりです。
>  - saml:aud：受信者。SAMLアサーションが送信されるエンドポイントのURL、このキーの値は、Audienceフィールドではなく、アサーション内のSAML Recipientフィールドから取得されます。
>  - saml:iss：送信者。URNで表されて、このキーの値はアサーションのSAML Issuerフィールドから取得されます。
>  - saml:sub：外部アカウントID。これは、組織内のユーザーを識別する唯一の値を含むステートメントの対象です。このキーはアサーションのSAML NameIDフィールドから取得されます。
>  - saml:sub_type：外部ユーザータイプ。このキーは、アサーション内のSMAL NameIDのFormat属性から取得されます。
5.	ロール権限構成を完了するために、ポリシーリストで、現在のロールに追加するポリシーを選択します。
6.	カスタムロール名を入力すると、【備考】にこのロールのメモを入力できます。
7.	作成しようとしているロールに関する情報を確認し、【完了】をクリックしてカスタムロールの作成を完了します。

##　APIで作成

###　Tencent Cloudアカウント用のロールを作成

Tencent Cloudでは、CAM APIを使用して新しいロールを作成することができます。APIを使用してロールを作成する方法を簡単に理解するために、典型的なケースを使用します。

次のシナリオを想定すると、会社Aは保守管理エンジニアのポジションを持ち、そのポジションを会社Bにアウトソーシングしたいと考えています。このポジションでは、会社A広州地域のすべてのCVMリソースを操作する必要があります。

会社Aの企業アカウントCompanyExampleA（ownerUinは12345）、ロールを作成して、ロールキャリアを会社Bの企業アカウントCompanyExampleB（ownerUinは67890）に設定します。

1. 会社Aの企業アカウントCompanyExampleA（ownerUinは12345）はCreateRole APIを呼び出して、roleNameがDevOpsRoleのロールを作成して、policyDocument（ロール信頼ポリシー）パラメータを次のように設定します。
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

2. 会社Aの企業アカウントCompanyExampleA（ownerUinは12345）はさっき作成したロールに権限を付与する必要があります。
 1. 会社Aの企業アカウントCompanyExampleA（ownerUinは12345）はポリシーDevOpsPolicyを作成します。ポリシーの構文は次のとおりです。
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
 2. 会社Aの企業アカウントCompanyExampleA（ownerUinは12345）は、[AttachRolePolicy](https://intl.cloud.tencent.com/document/product/598/13889)を呼び出します。step1で作成したポリシーをロールDevOpsRoleにバインディングして、入力パラメータはpolicyName=DevOpsPolicy、roleName=DevOpsRoleです。

上記の手順を通じて、会社Aの企業アカウントCompanyExampleA（ownerUinは12345）はロールの作成と認証を完了しました。

###　IDプロバイダー用のロールを作成

IDプロバイダー用のロールを作成する前に、CAMでSAML IDプロバイダーを作成する必要があります。SAML IDプロバイダーの作成方法については、[SAML IDプロバイダーの作成]()を参照してください。

1. 作成しようとしているロールの信頼ポリシーを準備します。
>　信頼ポリシーの各フィールドは次のように定義されています。
>  - actionフィールド：SAML統合身元が現在のロールを使用可能なAPIを定義します。`sts:AssumeRoleWithSAML`を使用します。
>  - principalフィールド：現在のロールを使用可能なIDプロバイダーを定義します。qcs::cam::uin/10001:saml-provider/idp_nameのように、`{"federated": [ IdPArn ]}`という文字列を使用します。
>  - conditionフィールド：現在のロールの利用条件を定義します。デフォルトでは` {"StringEquals": {"SAML:aud": "https://cloud.tencent.com/login/saml"}}`を使用します。この条件によって、SAML統合エンドポイントがTencent CloudのIDプロバイダーのみがこのロールを使用できます。

 ロールの信頼ポリシーの例は次のとおりです。
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

2.	作成しようとしているロールの権限ポリシーを準備します。権限ポリシーについては、[ポリシー](https://intl.cloud.tencent.com/document/product/598/10601)を参照してください。
3.	 [cam:CreateRole](https://cloud.tencent.com/document/api/598/13886) APIを呼び出して、IDプロバイダーロールを作成します。





