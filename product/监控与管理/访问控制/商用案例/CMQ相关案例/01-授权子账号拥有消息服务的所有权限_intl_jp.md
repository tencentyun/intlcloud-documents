### 承認されたサブアカウントはメッセージサービスに対するすべての権限を持っています

企業アカウントCompanyExampleには、Developerサブアカウントがあります。このサブアカウントは、企業アカウントCompanyExampleのメッセージキューに対するすべての権限を持っている必要があります。メッセージキューがトピックモデルでもキューモデルでも、読み書きできます。

ソリューションA：

企業アカウントCompanyExampleは、プリセットポリシーQCloudCmqQueueFullAccessおよびQCloudCmqTopicFullAccessをサブアカウントDeveloperに直接付与します。付与方法については、[認証管理](https://intl.cloud.tencent.com/document/product/598/10602)を参照してください。

ソリューションB：

step1：ポリシー構文を通して次のポリシーを作成します
```
 {
    "version": "2.0",
    "statement":
     {
         "effect": "allow",
         "action": ["cmqtopic:*","camqueue:*"]
         "resource": "*"
     }
}
```
step2：このポリシーをサブアカウントに付与します。付与方法については、[認証管理](https://intl.cloud.tencent.com/document/product/598/10602)を参照してください。


