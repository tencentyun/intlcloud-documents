
Cloud Access Management（CAM）ポリシーを使用して、クラウドデータベースコンソールにおいて特定のリソースを表示して使用する権限をユーザーに付与できます。この例ではユーザーにコンソールの特定部分の使用を許可するポリシーとなっています。

## クラウドデータベースの全読み取り書き込みポリシー
ユーザーにクラウドデータベースインスタンスを作成し管理する権限を持たせたい場合、そのユーザーに対してQcloudCDBFullAccesというポリシーを使用することができます。

[ポリシー管理](https://console.cloud.tencent.com/cam/policy)インターフェースに移動し、右上隅の検索ボックスでQcloudCDBFullAccessを検索すると、このポリシーを見つけることができます。
![](https://main.qcloudimg.com/raw/5ec89e71595a5edd3e7f723a19c01a6a.png)
ポリシー構文は以下のとおりです。
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
上記のポリシーは、ユーザーがクラウドデータベース、VPC、セキュリティグループ、Cloud Object Storage、キー管理サービス、Monitorのすべてのリソースに対し、個別にCAMポリシーの権限を承認することで実現します。

## クラウドデータベースの読み取り専用ポリシー
ユーザーにすべてのクラウドデータベースインスタンスをクエリーする権限のみを付与し、作成、削除および変更しないようにする場合は、そのユーザーに対してQcloudCDBInnerReadOnlyAccessというポリシーを使用することができます。

>?クラウドデータベースの読み取り専用ポリシーの設定をお勧めします。

[ポリシー管理](https://console.cloud.tencent.com/cam/policy)インターフェースに移動し、【サービスのタイプ】をクリックし、プルダウンした選択項目から【TencentDB for MySQL】を選択すると、その結果からポリシーを見つけることができます

ポリシー構文は以下のとおりです。
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

## クラウドデータベース関連リソースの読み取り専用ポリシー
ユーザーにクラウドデータベースインスタンスおよび関連リソース（VPC、セキュリティグループ、Cloud Object Storage、Monitor）をクエリーする権限のみを付与し、ユーザーに作成、削除および変更などの操作をさせないようにする場合は、そのユーザーに対してQcloudCDBReadOnlyAccessというポリシーを使用することができます。

[ポリシー管理](https://console.cloud.tencent.com/cam/policy)インターフェースに移動し、【サービスのタイプ】をクリックし、プルダウンした選択項目から【TencentDB for MySQL】を選択すると、その結果からポリシーを見つけることができます

ポリシー構文は以下のとおりです。
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
上記のポリシーは、以下の操作に対し、ユーザーがCAMポリシーの権限を承認することで実現します。
- クラウドデータベース中の「Describe」という単語で始まるすべての操作。
- VPC中の「Describe」という単語で始まるすべての操作、「Inquiry」という単語で始まるすべての操作、および「Get」という単語で始まるすべての操作。
- セキュリティグループ中の「DescribeSecurityGroup」という単語で始まるすべての操作。
- Cloud Object Storage中の「List」という単語で始まるすべての操作、「Get」という単語で始まるすべての操作、「Head」という単語で始まるすべての操作、および「OptionsObject」という名の操作。
- Monitor中のすべての操作。

## ユーザーに非リソースレベルのAPIの操作権限を付与するポリシー
ユーザーに非リソースレベルのAPIの操作権限を持たせたい場合、そのユーザーに対してQcloudCDBProjectToUserというポリシーを使用することができます。
[ポリシー管理](https://console.cloud.tencent.com/cam/policy)インターフェースに移動し、【サービスのタイプ】をクリックし、プルダウンした選択項目から【TencentDB for MySQL】を選択すると、その結果からポリシーを見つけることができます
ポリシー構文は以下のとおりです。
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

## ユーザーに特定のクラウドデータベースの操作権限を付与するポリシー
ユーザーに特定のクラウドデータベースを操作する権限を持たせたい場合、以下のポリシーをそのユーザーに関連付けることができます。以下のポリシーは、IDがcdb-xxxで、広州リージョンのクラウドデータベースインスタンスに対する操作権限をユーザーに付与します。
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

## ユーザーに大量のクラウドデータベースの操作権限を付与するポリシー
ユーザーに大量のクラウドデータベースを操作する権限を持たせたい場合、以下のポリシーをそのユーザーに関連付けることができます。以下のポリシーは、IDがcdb-xxx、cdb-yyyで、広州リージョンのクラウドデータベースインスタンスに対する操作権限、およびIDがcdb-zzzで、北京リージョンのクラウドデータベースインスタンスに対する操作権限をユーザーに付与します。
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

## ユーザーに特定リージョンのクラウドデータベースの操作権限を付与するポリシー
ユーザーに特定リージョンのクラウドデータベースを操作する権限を持たせたい場合、以下のポリシーをそのユーザーに関連付けることができます。以下のポリシーは、広州リージョンのクラウドデータベース機器に対する操作権限をユーザーに付与します。
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

## カスタムポリシー
プリセットポリシーでは希望する要件を満たせないと感じた場合、カスタムポリシーを作成することもできます。リソースによって承認する場合、リソースレベルの権限をサポートしていないクラウドデータベースのAPI操作について、ユーザーにその操作を行う権限を付与することはできますが、ポリシーステートメントのリソース要素には*を指定する必要があります。
     
カスタマイズされたポリシー構文は以下のとおりです。
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
- Actionの中は許可または拒否したい操作に置き換えます。
- Resourceの中は権限承認する具体的なリソースに置き換えます。
- Effectの中は許可または拒否に置き換えます。
