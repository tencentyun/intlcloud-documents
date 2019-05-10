

### ステッチ規則
Tencent Cloud APIリクエストURLのステッチ規則は以下の通りです。
> **https:// + リクエストドメイン名 +リクエストパス + ? +最終リクエストパラメータ列**

構成の説明：
-  **リクエストドメイン名：**リクエストドメイン名は、APIが属する製品またはそれが属する製品のモジュールによって決まり、異なる製品または異なる製品のモジュールのリクエストドメイン名は異なります。例えば、Tencent Cloud CVMの照合インスタンスリスト（DescribeInstances）のリクエストドメイン名：`cvm.api.qcloud.com`。具体的な製品リクエストドメイン名については、各APIの説明を参照してください。
-  **リクエストパス：** Tencent Cloud APIの対応製品のリクエストパスは、通常、1つの製品に1つの固定パスが対応します。（例えば、Tencent Cloud CVMの固定リクエストパスは`/v2/index.php`です）。
- **最終リクエストパラメータ列：** APIのリクエストパラメータ列は、共通リクエストパラメータとAPIリクエストパラメータを含みます。

### 使用例
Tencent Cloud APIの最終リクエストURL構造形式は次の通りです。
Tencent Cloud CVM[インスタンスリストの照合](https://cloud.tencent.com/document/api/213/15728)のAPI（DescribeInstances）を例とします。最初の6つのパラメータは共通リクエストパラメータ、最後の6つのパラメータはAPIリクエストパラメータです。

```
https://cvm.api.qcloud.com/v2/index.php?
Action=DescribeInstances
&SecretId=xxxxxxx
&Region=gz
&Timestamp=1465055529
&Nonce=59485
&Signature=mysignature       //共通リクエストパラメータ
&instanceIds.0=ins-0hm4gvho
&instanceIds.1=ins-8oby8q00
&offset=0
&limit=20
&status=2
&zoneId=100003      //APIリクエストパラメータ
```

