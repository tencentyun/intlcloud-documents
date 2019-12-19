###　承認されたサブアカウントは特定のトピックモデルのメッセージキューの読み取り権限を持っています

企業アカウントCompanyExample（ownerUinは12345678）には、トピックモデルに基づくメッセージキューがあって、また、そのメッセージキューにアクセスしたがるサブアカウントDeveloperもあります。

step1：ポリシー構文を通して次のポリシーを作成します
```
{
    "version": "2.0",
    "statement":   
     {
        "action": "cmqqueue:SendMessage",
        "resource":"qcs::cmqqueue:::queueName/uin/12345678/test-caten",
        "effect": "allow"
     } 
}
```

step2：このポリシーをサブアカウントに付与します。付与方法については、[認証管理](https://intl.cloud.tencent.com/document/product/598/10602)を参照してください。

