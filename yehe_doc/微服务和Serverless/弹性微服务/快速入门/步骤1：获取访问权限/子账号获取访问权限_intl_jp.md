## CAMの基本概念

ルートアカウントはサブアカウントにポリシーをバインドすることで権限承認を行います。ポリシーの設定は、**[API、リソース、ユーザー/ユーザーグループ、許可/拒否、条件]**の次元まで精密に行うことができます。

#### ユーザーのタイプ

- **ルートアカウント**：Tencent Cloudのすべてのリソースを所有し、どのリソースにも任意にアクセスできます。
- **サブアカウント**：サブユーザー、WeComサブユーザー、コラボレーター、メッセージ受信者が含まれます。

ルートアカウントとサブアカウントの詳細な定義および機能の説明については、[CAM-ユーザーのタイプ](https://intl.cloud.tencent.com/document/product/598/32633)をご参照ください。

#### リソースと権限

- **リソース**：リソースとは、クラウドサービスにおいて操作の対象となるものであり、例えばCVMインスタンス、COSバケット、VPCインスタンスなどがあります。
- **権限**：権限とは、ある何人かのユーザーに対し、あるいくつかの操作の実行を許可または拒否することを指します。デフォルトでは、**ルートアカウントはその名前の下にあるすべてのリソースへのアクセス権限を有する**一方、**サブアカウントにはルートアカウント下の何らかのリソースへのアクセス権限がありません**。
- **ポリシー**：ポリシーは、1つまたは複数の権限を定義および説明する構文仕様です。**ルートアカウント**はユーザー/ユーザーグループに**ポリシーをバインドする**ことによって権限承認を行います。


## サブアカウントによるTEMの使用

コラボレーターとサブアカウントがTEMを使用する場合は、次の3つの面で権限承認を行う必要があります。

1. ロール（およびその許可ポリシー）をTEMサービスに渡します。ユーザーはサービスに**ロールを渡す**許可を有する、すなわちPassRoleポリシーを作成する必要があります。詳細な操作については[PassRoleポリシーの承認](#PassRole)をご参照ください。
2. TEMの権限を使用して、サブアカウントにQcloudTEMFullAccessポリシーを付与し、サブアカウントがTEMのすべての権限を使用できるようにするか、あるいはQcloudTEMReadOnlyAccessポリシーによってサブアカウントに読み取り専用権限を承認することができます。詳細な操作については[TEMプラットフォーム使用権限の承認](#TEMプラットフォーム使用権限の承認)をご参照ください。
3. TEMの使用の過程で他の製品に対する呼び出しを伴う場合は、ルートアカウントがサブアカウントに対し権限承認を行う必要があります。詳細な説明は[他のクラウド製品へのアクセス権限の承認](#他のクラウド製品へのアクセス権限の承認)をご参照ください。

[](id:PassRole)
### PassRoleポリシーの承認

#### ステップ1. ポリシーの新規作成

1. [CAMコンソール](https://console.cloud.tencent.com/cam)にログインします。
2. 左側ナビゲーションバーで**ポリシー**をクリックし、ポリシー管理リストページに進みます。
3. **カスタムポリシーの新規作成**をクリックします。
4. ポリシー作成方式を選択するポップアップボックスで、**ポリシー構文で作成**をクリックし、ポリシー構文での作成ページに進みます。
5. [ポリシー構文で作成ページ](https://console.cloud.tencent.com/cam/policy/createV2) で、**空白テンプレート**を選択し、**次のステップ**をクリックします。
6. ポリシー名と内容を入力し、**ポリシーの作成**をクリックします。ルートアカウントまたは管理権限を有するサブアカウントを使用して次の2つのカスタムポリシーを作成します。ポリシー構文は次のとおりです。
	- CLS以外のクラウド製品リソースへのアクセス：
	```json
	{
			"version": "2.0",
			"statement": {
					"effect": "allow",
					"action": "cam:PassRole",
					"resource": "qcs::cam::uin/${OwnerUin}:role/tencentcloudServiceRoleName/TEM_QCSLinkedRoleInAccessCluster"
			}
	}
	```
	- CLSクラウド製品リソースへのアクセス：
	```json
	{
			"version": "2.0",
			"statement": {
					"effect": "allow",
					"action": "cam:PassRole",
					"resource": "qcs::cam::uin/${OwnerUin}:role/tencentcloudServiceRoleName/TEM_QCSLinkedRoleInTEMLog"
			}
	}
```
このうち`${OwnerUin}`はルートアカウントIDです。コンソールの[アカウント情報](https://console.cloud.tencent.com/developer)ページから取得できます。


#### ステップ2：ポリシーをユーザーにバインド

1. 左側ナビゲーションバーで、**ユーザー** > [**ユーザーリスト**](https://console.cloud.tencent.com/cam)をクリックし、ユーザー管理ページに進みます。
2. TEM使用権限を承認したいユーザーを選択し、操作列の**権限承認**をクリックします。
3. ポリシーリストから**ステップ1**で作成したポリシーを選択します。
4. **OK**をクリックし、ポリシーのバインドを行います。このポリシーはユーザーのポリシーリストに表示されます。

### TEMプラットフォーム使用権限の承認[](id:TEMプラットフォーム使用権限の承認)

**全読み取り書き込みポリシー**

サブユーザーにTEMサービスの完全な管理権限（作成、管理などの全操作）を承認します。

```json
{
    "version": "2.0",
    "statement": [
        {
            "action": "tem:*",
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

システムの[全読み取り書き込みポリシー](https://console.cloud.tencent.com/cam/policy/createV2)の設定によってもサポート可能です。

1. [CAMコンソール](https://console.cloud.tencent.com/cam/overview)にログインします。
2. 左側メニューバーで**[ポリシー](https://console.cloud.tencent.com/cam/policy)**をクリックします。
3. ポリシーリストで、**カスタムポリシーの新規作成**をクリックします。
4. ポリシー作成方式を選択するポップアップウィンドウで、**ポリシー構文で作成**を選択します。
5. テンプレートのタイプから「tem」を検索し、TEMの全読み取り書き込みアクセス権限**QcloudTEMFullAccess**を選択し、**次のステップ**をクリックします。
6. **完了**をクリックします。

その後の操作：作成したポリシーを対象のユーザーにバインドします。

**読み取り専用ポリシー**

サブユーザーにTEMサービスの読み取り専用権限を承認します。

```json
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "tem:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

システムの[読み取り専用ポリシー](https://console.cloud.tencent.com/cam/policy/createV2)の設定によってもサポート可能です。

1. [CAMコンソール](https://console.cloud.tencent.com/cam/overview)にログインします
2. 左側メニューバーで**[ポリシー](https://console.cloud.tencent.com/cam/policy)**をクリックします。
3. ポリシーリストで、**カスタムポリシーの新規作成**をクリックします。
4. ポリシー作成方式を選択するポップアップウィンドウで、**ポリシー構文で作成**を選択します。
5. テンプレートのタイプから「tem」を検索し、TEMの読み取り専用アクセスポリシー**QcloudTEMReadOnlyAccess**を選択し、**次のステップ**をクリックします。
6. **ポリシーの作成**をクリックします。

### 他のクラウド製品へのアクセス権限の承認[](id:他のクラウド製品へのアクセス権限の承認)

TEMプラットフォームは使用中に以下のクラウド製品に対する呼び出しを行います。対応するTEM製品機能の使用を保証するためには、ルートアカウントがサブアカウントに対し単独の権限承認を行う必要があります。

権限承認の例は次のとおりです。

```json
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cam:DescribeRoleList",
                "cvm:DescribeSecurityGroups",
                "vpc:DescribeVpcEx",
                "vpc:DescribeSubnetEx",
                "tse:DescribeSREInstances",
                "cls:DescribeLogsets",
                "cls:DescribeTopics",
                "cfs:DescribeCfsFileSystems",
                "ssl:DescribeCertificate",
                "tcr:DescribeRepositoryOwnerPersonal",
                "tcr:DescribeRepositories",
                "tcr:DescribeInstances",
                "tcr:DescribeInternalEndpoints",
                "tcr:CreateInstanceToken"
            ],
            "resource": [
                "*"
            ]
        }
    ]
}
```
