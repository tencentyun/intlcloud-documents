###　承認されたサブアカウントはCloud VODに対するすべての権限を持っています

企業アカウントCompanyExample（ownerUinは12345678）には、サブアカウントDeveloperがあります。このサブアカウントは、企業アカウントCompanyExampleのCloud VODサービスに対する完全な管理権限が必要です。

ソリューションA：

企業アカウントCompanyExampleは、プリセットポリシーQcloudVODFullAccessをサブアカウントDeveloperに直接付与します。付与方法については、[認証管理](https://intl.cloud.tencent.com/document/product/598/10602)を参照してください。

ソリューションB：

step1：ポリシー構文を通して次のポリシーを作成します
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "vod:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": "cos:*",
            "resource": "qcs::cos::uid/10022853:*",
            "effect": "allow"
        }
    ]
}
```
step2：このポリシーをサブアカウントに付与します。付与方法については、[認証管理](https://intl.cloud.tencent.com/document/product/598/10602)を参照してください。


