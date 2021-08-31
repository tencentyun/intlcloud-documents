<span id = "celueyufa"></span>
## ポリシー文法
CAMポリシー：
```
{	 
        "version":"2.0", 
        "statement": 
        [ 
           { 
              "effect":"effect", 
              "action":["action"], 
              "resource":["resource"], 
               "condition": {"key":{"value"}} 
           } 
       ] 
} 
```
- **バージョンversion**：記入必須項目であり、現時点で「2.0」の値のみを許可しています。
- **ステートメントstatement**：1つ又は複数の権限の詳細情報を記述します。この要素は効力、操作、リソース、条件などの複数のその他の要素の権限又は権限集合を含みます。1つのポリシーには1つのステートメント要素だけしかありません。
 - **影響 effect**：必須項目で、ステートメントにより生じる結果が「許可」か「明示式拒否」かを記述します。allow（許可）及びdeny（明示式拒否）の2種類の状況を含みます。
 - **操作 action**：必須項目で、許可又は拒絶の操作について記述します。操作はAPIであることが可能です（cdb: プレフィックスで記述します）。
 - **リソース resource**：必須項目で、認証された具体的なデータについて記述します。リソースは6段式で記述され、各製品のリソース定義の詳細は異なります。
 - **発効条件condition** は必須項目で、ポリシー発効の制約条件を記述します。条件はオペレーター、操作キーと操作値を含みます。条件値は時間、IPアドレスなどの情報を含んでいます。一部のサービスは、条件の中で他の値を指定することを許可しています。

<span id = "caozuo"></span>
## CDBの操作
CDBポリシーのステートメントでは、CDBをサポートするすべてのサービスの中から任意のAPI操作を指定することができます。CDBについては、cdb: をプレフィックスとするAPIを使用してください。例：cdb:CreateDBInstance又はcdb:CreateAccounts。

1つのステートメントで複数の操作を指定する場合は、以下のとおりコンマで区切ってください。
```
"action":["cdb:action1","cdb:action2"]
```
ワイルドカードで複数の操作を指定することも可能です。例えば、以下のとおり名前が「Describe」の単語で始まるすべての操作を指定することが可能です。
```
"action":["cdb:Describe*"]
```
CDBにおけるすべての操作を指定する場合は、以下のとおり*ワイルドカードを使用してください。
```
"action"：["cdb:*"]
```

<span id = "ziyuanlujing"></span> 
## CDBのリソース
各CAMポリシーステートメントは自身に適用されるリソースがあります。
リソースの一般的な形式は次のとおりです。
```
qcs:project_id:service_type:region:account:resource
```
- ** project_id**：プロジェクト情報を記述します。CAMの早期ロジックと互換させるためだけのもので、記入する必要はありません。
- ** service_type：製品略称です（例：cdb）。
- **region**：地域情報です（例：ap-guangzhou）。
- **account**：リソース所有者のメインアカウント情報です（例：uin/164256472）。
- **resource**：各製品の具体的なリソース詳細です（例：instanceId/instance_id1又はinstanceId/*）。


例えば、以下のとおり特定のインスタンス（cdb-k05xdcta）を使用して、ステートメントでそれを指定することができます。
```
"resource":[ "qcs::cdb:ap-guangzhou:uin/653339763:instanceId/cdb-k05xdcta"]
```
以下のとおり*ワイルドカードで特定アカウントに属するすべてのインスタンスを指定することもできます。
```
"resource":[ "qcs::cdb:ap-guangzhou:uin/653339763:instanceId/*"]
```
すべてのリソースを指定したい場合、又は特定のAPI操作がリソース級の権限をサポートしていない場合、以下のとおりresource要素の中で*ワイルドカードを使ってください。
```
"resource": ["*"]
```
1つのコマンドで同時に複数のリソースを指定したい場合は、コンマで区切ってください。以下で示すのは、2つのリソースを指定した例です。
```
"resource":["resource1","resource2"]
```

以下の表ではCDBが使用できるリソースと対応するリソースの記述方法を説明します。そのうち、$がプレフィックスの単語はいずれも別称であり、regionは地域、accountはアカウントIDを指します。

| リソース | 認証ポリシーにおけるリソースの記述方法 |
|-------|-------|
|インスタンス|  `qcs::cdb:$region:$account:instanceId/$instanceId`|
|VPC|  `qcs::vpc:$region:$account:vpc/$vpcId`|
|セキュリティグループ|  `qcs::cvm:$region:$account:sg/$sgId`|
