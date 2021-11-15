
デフォルトの状態では、サブアカウントにMySQLデータベース監査を利用する権利はありません。ユーザーはポリシーを作成して、サブアカウントにデータベース監査の利用を許可する必要があります。
サブアカウントに対してMySQLデータベース監査関連リソースのアクセス管理を行う必要がない場合は、このドキュメントを無視することができます。

[CAM](https://intl.cloud.tencent.com/document/product/598/10583)（Cloud Access Management、CAM）は、Tencent Cloudが提供するWebサービスであり、主にユーザーがTencent Cloudアカウントのリソースへのアクセス権限を安全に管理するのに役立ちます。CAMを使用すると、ユーザー（グループ）を作成、管理、および廃棄でき、ID管理とポリシー管理を介して、Tencent Cloudリソースの使用が許可されるユーザーを指定し、制御できます。

CAMを使用する場合は、ポリシーを1人のユーザーまたは1組のユーザーグループと関連付けて、指定されたリソースを使用して指定されたタスクを完了することを許可または拒否できます。CAMポリシーのより詳細な基本情報については、[ポリシー構文](https://intl.cloud.tencent.com/document/product/598/10603)をご参照ください。


## サブアカウントの権限承認
1. ルートアカウントで[CAMコンソール](https://console.cloud.tencent.com/cam)にログインし、ユーザーリストで対応するサブユーザーを選択して、【承認】をクリックします。
![](https://main.qcloudimg.com/raw/a406ba643c22f2733699cf881ab336fb.png)
2. ポップアップしたダイアログボックスで、【QcloudCDBFullAccessクラウドデータベース（CDB）全読み取り/書き込みアクセス権限】または【QcloudCDBInnerReadOnlyAccessクラウドデータベース（CDB）読み取り専用アクセス権限】プリセットポリシーを選択し、【OK】をクリックして、サブユーザーの権限承認を完了します。
>?MySQLデータベース監査はMySQLデータベースのサブモジュールです。このため、上記で述べたMySQLの2種類の権限プリセットポリシーは、MySQLデータベース監査に必要な権限ポリシーをカバーします。サブユーザーがMySQLデータベース監査に必要な権限のみを必要とする場合は、 [MySQLデータベース監査ポリシーのカスタマイズ](#zdymsjksjcl)をご参照ください。
>
![](https://main.qcloudimg.com/raw/8500ea99c00fd496139e8535f45dadd2.png)


## [ポリシー構文](id:clyf)
MySQLデータベース監査のCAMポリシーの説明は以下のとおりです。
```
{     
        "version":"2.0", 
        "statement": 
        [ 
           { 
              "effect":"effect", 
              "action":["action"], 
              "resource":["resource"]
           } 
       ] 
} 
```

- **バージョンversion**：入力必須項目であり、現時点では"2.0"のみを認めています。
- **ステートメント statement**：1つか複数の権限の詳細情報を説明することに使われます。この要素にはeffect、action、resource等いくつかの他の要素の権限または権限セットが含まれます。1つのポリシーには1つのstatement要素しかありません。
- **影響effect**：入力必須項目であり、ステートメントによる結果が「許可」であるか「明示的な拒否」であるかを説明します。allow（許可）とdeny（明示的な拒否）という2種類の状況が含まれています。
- **アクションaction**：入力必須項目であり、許可する、または拒否するアクションを説明することに使われます。アクションはAPI（nameプレフィックス）または機能セット（permidプレフィックスが付いた特定のAPIセット）を指定できます。
- **リソース resource**：入力必須項目であり、権限承認の具体的データを説明します。


## APIの操作
CAMポリシーステートメントの中で、CAMをサポートしているすべてのサービスから、任意のAPI操作を指定できます。データベース監査については、name/cdb:というプレフィックスが付いたAPIをご使用ください。1つのステートメントの中で複数の操作を指定したい場合は、下記のようにコンマで区切ってください：
```
"action":["name/cdb:action1","name/cdb:action2"]
```

ワイルドカードで複数のアクションを指定することも可能です。例えば、下記のとおり先頭が 「Describe」で始まるすべてのアクションを指定することが可能です。
```
"action":["name/cdb:Describe*"]
```


## リソースパス
リソースパスの一般的な形式は以下のとおりです。
```
qcs::service_type::account:resource
```

- service_type：製品の略称です。ここではcdb。
- account：リソース所有者のルートアカウント情報です。例えばuin/326xxx46。
- resource：製品の具体的なリソース詳細です。各MySQLインスタンス（instanceId）が1つのリソースです。

例：
```
 "resource": ["qcs::cdb::uin/326xxx46:instanceId/cdb-kf291vh3"]
```
このうち、cdb-kf291vh3はMySQLインスタンスリソースのIDで、ここではCAMポリシーステートメント中のリソースresourceです。

## 事例
以下の例はCAMの使用方法のみを示したものです。MySQLデータベース監査の完全なAPIについては、[APIドキュメント](https://cloud.tencent.com/document/product/236/45460)をご参照ください。

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/cdb: DescribeAuditRules"
            ],
            "resource": [
                "*"
            ]
        },
        {
            "effect": "allow",
            "action": [
                "name/cdb: CreateAuditPolicy"
            ],
            "resource": [
                "*"
            ]
        },
       
        {
            "effect": "allow",
            "action": [
                "name/cdb: DescribeAuditLogFiles"
            ],
            "resource": [
                "qcs::cdb::uin/326xxx46:instanceId/cdb-kf291vh3"
            ]
        }
    ]
}
```

## [MySQLデータベース監査ポリシーのカスタマイズ](id:zdymsjksjcl)
1. ルートアカウントで[CAMコンソール](https://console.cloud.tencent.com/cam/policy)にログインし、ポリシーリストで、【カスタムポリシーの新規作成】をクリックします。
![](https://main.qcloudimg.com/raw/772bd2ef82786ef54086307849606b9d.png)
2. ポップアップしたダイアログボックスで、【ポリシージェネレーターで作成】を選択します。
3. サービスおよび操作の選択画面で、各項目の設定を選択し、【ステートメントの追加】をクリックした後、【次のステップ】をクリックします。
 - サービス(Service)：【TencentDB for MySQL】を選択します。
 - アクション(Action)：MySQLデータベース監査のすべてのAPIを選択します。[APIドキュメント](https://cloud.tencent.com/document/product/236/45449)をご参照ください。
  - リソース(Resource)：[リソース記述法](https://intl.cloud.tencent.com/document/product/598/10606)をご参照ください。`*`を入力し、すべてのMySQLインスタンスの監査ログが操作可能であることを示します。
![](https://main.qcloudimg.com/raw/ebd4dd9cc00e6caaac6c59ba397fb842.png)
4. ポリシー編集画面で、命名仕様に従い、「ポリシー名」（例えばSQLAuditFullAccess）と「説明」を入力後、【完了】をクリックします。
![](https://main.qcloudimg.com/raw/cb5d0db2683cd54114c5d29685cd1da4.png)
5. ポリシーリストに戻ると、作成したカスタムポリシーを確認することができます。
![](https://main.qcloudimg.com/raw/050e310f11386c1b795410150af73b52.png)

