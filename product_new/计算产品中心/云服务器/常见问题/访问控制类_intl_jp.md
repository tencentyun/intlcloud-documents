### カスタマイズポリシーを作成には、どうすればいいですか。

プリセットのポリシーがご要望を満たさない場合は、ポリシーをカスタマイズで作成できます。
カスタマイズポリシーの構文は次のとおりです。

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

- Action 許可または拒否するアクションに置き換えてください。
- Resource 許可する特定のリソースに置き換えてください。
- Effect 許可または拒否に置き換えてください。

### CVMの読取専用ポリシーを構成するには、どうすればいいですか。

ユーザーにCVMインスタンスをクエリーする権限のみを許可したいですが、作成、削除、および起動・シャットダウンの権限を許可しない場合、そのユーザーに対してQcloudCVMInnerReadOnlyAccessという名前のポリシーを使用することができます。

Cloud Access Managementコンソールにログインし、[ポリシー管理](https://console.cloud.tencent.comCloud Access Management/cam/policy)画面で**CVM**を検索して、対象ポリシーをすばやく見つけます。

ポリシー構文は次のとおりです。

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cvm:Describe*",
                "name/cvm:Inquiry*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

上記のポリシーは、**ユーザーに次の操作の操作権限を持たせる**ことで目的を達成します。

- CVM内で「Describe」という単語で始まるすべての操作。
- CVM内で「Inquiry」という単語で始まるすべての操作。

### CVM関連リソースの読取専用ポリシーを構成するには、どうすればいいですか。

ユーザーにCVMインスタンスと関連リソース(VPC、CLB)をクエリーする権限のみを許可したいですが、ユーザーに作成、削除、起動・シャットダウンなどの操作権限を許可しない場合、ユーザーにQcloudCVMReadOnlyAccessという名前のポリシーを使用することができます。 

Cloud Access Managementコンソールにログインし、[ポリシー管理](https://console.cloud.tencent.com/cam/policy)画面で**CVM**を検索して、対象ポリシーをすばやく見つけます。

ポリシー構文は次のとおりです。

```
 {
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cvm:Describe*",
                "name/cvm:Inquiry*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "name/vpc:Describe*",
                "name/vpc:Inquiry*",
                "name/vpc:Get*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "name/clb:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": "name/monitor:*",
            "resource": "*"
        }
    ]
}
```

上記のポリシーは、**ユーザーに次の操作の操作権限を持たせること**で目的を達成します。

- CVM内で「Describe」という単語で始まるすべての操作と「Inquiry」という単語で始まるすべての操作。
- VPC 内で「Describe」という単語で始まるすべての操作、「Inquiry」という単語で始まるすべての操作、および「Get」という単語で始まるすべての操作。
- CLB内で「Describe」という単語で始まるすべての操作。
- Monitor 内のすべての操作。

