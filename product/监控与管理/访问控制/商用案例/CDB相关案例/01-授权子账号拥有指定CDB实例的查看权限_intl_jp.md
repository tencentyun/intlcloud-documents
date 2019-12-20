###　承認されたサブアカウントは、指定CDBインスタンスの確認権限を持っています

企業アカウントCompanyExample（ownerUinは12345678）には、サブアカウントDeveloperがあります。このサブアカウントは、企業アカウントCompanyExampleの2つのcdbインスタンス（インスタンスIDはそれぞれcdb-1とcdb-2）に対する確認権限を持っている必要があります。

step1：ポリシー構文を通して次のポリシーを作成します
```
 {
    "version": "2.0",
    "statement":
     {
         "effect": "allow",
         "action": "cdb:*",
         "resource": ["qcs::cdb::uin/12345678:instanceId/cdb-1", "qcs::cdb::uin/12345678:instanceId/cdb-2"]
     }
}
```
step2：このポリシーをサブアカウントに付与します。付与方法については、[認証管理](https://intl.cloud.tencent.com/document/product/598/10602)を参照してください。

注：サブアカウントDeveloperは、CDB照合リストページでインスタンスIDがcdb-1およびcdb-2のリソースだけを確認できます。


