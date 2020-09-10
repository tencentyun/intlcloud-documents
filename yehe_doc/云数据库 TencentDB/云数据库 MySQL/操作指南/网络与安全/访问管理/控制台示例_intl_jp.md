## 操作シナリオ
Cloud Access Management（CAM）を使用して、ユーザーにCDBコンソールで特定のリソースを確認し使用する権限を持たせることができます。この部分の例では、ユーザーにコンソールの特定部分のポリシーを使用させることができます。

## 操作手順
### CDBの全読み書きポリシー
ユーザーにCDBインスタンスを作成し管理する権限を持たせたい場合、このユーザーに対して名称がQcloudCDBFullAccessのポリシーを使用することができます。

[ポリシー管理](https://console.cloud.tencent.com/cam/policy)画面に入り、右上隅の検索ボックスに[QcloudCDBFullAccess] を入力して、ポリシーを見つけます。 ![](https://main.qcloudimg.com/raw/5ec89e71595a5edd3e7f723a19c01a6a.png)

ポリシー文法は以下の通りです。
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cdb:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "vpc:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "cvm:*"
            ],
            "resource": "qcs::cvm:::sg/*",
            "effect": "allow"
        },
        {
            "action": [
                "cos:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": "monitor:*",
            "resource": "*"
        },
        {
            "action": [
                "kms:CreateKey",
                "kms:GenerateDataKey",
                "kms:Decrypt",
                "kms:ListKey"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
以上のポリシーはユーザーにそれぞれCDB及びVirtual Private Cloud、セキュリティグループ、Cloud Object Storage、Key Management Service、Monitor中のすべてのリソースに対してCAMポリシー認証を行わせることにより目的に達します。

### CDBの読取専用ポリシー
ユーザーにCDBインスタンスを照会する権限のみを持たせ、作成及び削除、修正の権限を持たせたくない場合、このユーザーに対して名称がQcloudCDBInnerReadOnlyAccessのポリシーを使用することができます。

> CDBの読取専用ポリシーを構成することをお勧めします。

[ポリシーの管理](https://console.cloud.tencent.com/cam/policy)インターフェースに進み、列項目【サービスのタイプ】をクリックし、プルダウンオプションから【MySQL】を選択すると、結果からこのポリシーを見つけることができます。

ポリシー文法は以下の通りです。
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cdb:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

### CDB関連リソースの読取専用ポリシー
ユーザーにCDBインスタンス及び関連リソース（Virtual Private Cloud、セキュリティグループ、Cloud Object Storage、Monitor）を照会する権限のみを持たせ、このユーザーが作成及び削除、修正などの操作権限を持つことを許可しない場合、このユーザーに対して名称がQcloudCDBReadOnlyAccessのポリシーを使用することができます。

[ポリシーの管理](https://console.cloud.tencent.com/cam/policy)インターフェースに進み、列項目【サービスのタイプ】をクリックし、プルダウンオプションから【MySQL】を選択すると、結果からこのポリシーを見つけることができます。

ポリシー文法は以下の通りです。
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cdb:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "vpc:Describe*",
                "vpc:Inquiry*",
                "vpc:Get*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "cvm:DescribeSecurityGroup*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "cos:List*",
                "cos:Get*",
                "cos:Head*",
                "cos:OptionsObject"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": "monitor:*",
            "resource": "*"
        }
    ]
}
```
以上のポリシーは、ユーザーにそれぞれ以下の操作についてCAMポリシー認証を行わせることにより、目的に達します。
- CDB中のすべての「Describe」という単語で始まる操作。
- Virtual Private Cloud中のすべての「Describe」という単語で始まる操作及びすべての「Inquiry」という単語で始まる操作、すべての「Get」という単語で始まる操作。
- セキュリティグループ中のすべての「DescribeSecurityGroup」という単語で始まる操作。
- Cloud Object Storage中のすべての「List」という単語で始まる操作及びすべての「Get」という単語で始まる操作、すべての「Head」という単語で始まる操作、「OptionsObject」という名前の操作。
- Monitor中のすべての操作。

### ユーザーに非リソース級のAPIインターフェースの操作権限を認証する際のポリシー
ユーザーに非リソース級のAPIインターフェースの操作権限を認証したい場合、このユーザーに対して名称がQcloudCDBProjectToUserのポリシーを使用することができます。
[ポリシーの管理](https://console.cloud.tencent.com/cam/policy)インターフェースに進み、列項目【サービスのタイプ】をクリックし、プルダウンオプションから【MySQL】を選択すると、結果からこのポリシーを見つけることができます。
ポリシー文法は以下の通りです。
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cdb:BalanceRoGroupLoad",
                "cdb:CancelBatchOperation",
                "cdb:CreateBatchJobFiles",
                "cdb:CreateDBInstance",
                "cdb:CreateDBInstanceHour",
                "cdb:CreateMonitorTemplate",
                "cdb:CreateParamTemplate",
                "cdb:DeleteBatchJobFiles",
                "cdb:DeleteMonitorTemplate",
                "cdb:DeleteParamTemplate",
                "cdb:DescribeBatchJobFileContent",
                "cdb:DescribeBatchJobFiles",
                "cdb:DescribeBatchJobInfo",
                "cdb:DescribeProjectSecurityGroups",
                "cdb:DescribeDefaultParams",
                "cdb:DescribeMonitorTemplate",
                "cdb:DescribeParamTemplateInfo",
                "cdb:DescribeParamTemplates",
                "cdb:DescribeRequestResult",
                "cdb:DescribeRoGroupInfo",
                "cdb:DescribeRoMinScale",
                "cdb:DescribeTasks",
                "cdb:DescribeUploadedFiles",
                "cdb:ModifyMonitorTemplate",
                "cdb:ModifyParamTemplate",
                "cdb:ModifyRoGroupInfo",
                "cdb:ModifyRoGroupVipVport",
                "cdb:StopDBImportJob",
                "cdb:UploadSqlFiles"
            ],
            "effect": "allow",
            "resource": "*"
        }
    ]
}
```

### ユーザーに特定のCDBの操作権限を認証する際のポリシー
ユーザーに特定のCDBの操作権限を認証したい場合、以下のポリシーをこのユーザーに関連付けます。以下のポリシーは、ユーザーにIDがcdb-xxxの、広州地域のCDBインスタンスに対する操作権限を許可します。
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cdb:*",
            "resource": "qcs::cdb:ap-guangzhou::instanceId/cdb-xxx",
            "effect": "allow"
        }
    ]
}
```

### ユーザーにCDB一括操作権限を認証する際のポリシー
ユーザーにCDBの一括操作権限を認証したい場合、以下のポリシーをこのユーザーに関連付けます。以下のポリシーは、ユーザーにIDがcdb--xxxの、広州地域のCDBインスタンスに対する操作権限とIDがcdb-zzzの、北京地域のCDBインスタンスに対する操作権限を許可します。
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cdb:*",
            "resource": ["qcs::cdb:ap-guangzhou::instanceId/cdb-xxx", "qcs::cdb:ap-guangzhou::instanceId/cdb-yyy", "qcs::cdb:ap-beijing::instanceId/cdb-zzz"],
            "effect": "allow"
        }
    ]
}
```

### ユーザーに特定地域のCDBの操作権限を認証する際のポリシー
ユーザーに特定地域のCDBの操作権限を認証したい場合、以下のポリシーをこのユーザーに関連付けます。以下のポリシーは、ユーザーの広州地域のCDBサーバーに対する操作権限を許可します。
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cdb:*",
            "resource": "qcs::cdb:ap-guangzhou::*",
            "effect": "allow"
        }
    ]
}
```

### カスタマイズポリシー
プリセットされたポリシーが要求を満たすことができていないと感じた場合、カスタマイズポリシーを作成することができます。リソースに従い認証を行う場合、リソース権限をサポートしないCDBのAPI操作について、ユーザーにこの操作を使用する権限を付与することができますが、ポリシーのステートメントのリソース要素は*に指定しなければなりません。
     
カスタマイズポリシー文法は以下の通りです。
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "Action"
            ],
            "resource": "Resource",
            "effect": "Effect"
        }
    ]
}
```
- Actionで許可又は拒否したい操作に置き換えます。
- Resourceで認証する特定のリソースに置き換えます。
- Effectで許可又は拒否に置き換えます。
