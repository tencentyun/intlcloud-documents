### 承認されたサブアカウントは、作成したメッセージキューに対するすべての権限を持っています

企業アカウントCompanyExampleには、Developerサブアカウントがあります。このサブアカウントは、自分で作成したメッセージキューにアクセスしたいと考えています。

ソリューションA：

企業アカウントCompanyExampleは、プリセットポリシーQCloudCmqQueueCreaterFullAccessおよびQCloudCmqTopicCreaterFullAccessをサブアカウントDeveloperに直接付与します。付与方法については、[認証管理](https://intl.cloud.tencent.com/document/product/598/10602)を参照してください。

ソリューションB：

step1：ポリシー構文を通して次のポリシーを作成します

```
{
    "version": "2.0",
    "statement":
    [
       {
           "effect": "allow",
           "action": "cmqtopic:*",
           "resource": "qcs::cmqtopic:::topicName/uin/${uin}/*"
       },
       {
           "effect": "allow",
           "action": "cmqqueue:*",
           "resource": "qcs::cmqqueue:::queueName/uin/${uin}/*"
       }
    ]
}
```

step2：このポリシーをサブアカウントに付与します。付与方法については、[認証管理](https://intl.cloud.tencent.com/document/product/598/10602)を参照してください。


