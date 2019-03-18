## API説明
このAPI（AssumeRole）は、ロールの一時的認証情報を申請するために使用されます。
リクエストドメイン名：

```
sts.api.qcloud.com
```

## 入力パラメータ
以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/6976)がリストされていません。

|フィールド|必須項目|タイプ|説明|
| ------------ | ------------ | ------------ | ------------ |
|roleArn|はい|String|ロールのリソースの説明。例えば：qcs::cam::uin/12345678:role/4611686018427397919、qcs::cam::uin/12345678:roleName/testRoleName|
|roleSessionName|はい|String|一時的セッション名、ユーザーのカスタム定義名|
|durationSeconds|いいえ|Int|一時的証明書の有効期間を指定します。単位は秒、デフォルトは1800秒、最大有効期間は7200秒です|

## 出力パラメータ

| フィールド  | タイプ  | 説明  |
| ------------ | ------------ | ------------ |
|  credentials | [credentials](#dataStructure)  | オブジェクトにtoken、tmpSecretId、tmpSecretKeyトライアドが含まれています  |

<span id="dataStructure"></span>
## Credentialsデータ構造

| フィールド  | タイプ  | 説明  |
|---------|---------|---------|
| token | String | token 値 |
| tmpSecretId | String | 一時的セキュリティ証明書ID |
| tmpSecretKey | String | 一時的セキュリティ証明書Key |

## 例
#### 入力

```
https://sts.api.qcloud.com/v2/index.php?Action=AssumeRole&roleArn=qcs%3a%3acam%3a%3auin%2f12345678%3arole%2f4611686018427397919
&roleSessionName=abc&durationSeconds=1800&<共通リクエストパラメータ>
```

#### 出力

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "credentials": {
            "sessionToken": "5e776c4216ff4d31a7c74fe194a978a3ff2a42864",
            "tmpSecretId": "AKIDcAZnqgar9ByWq6m7ucIn8LNEuY2MkPCl",
            "tmpSecretKey": "VpxrX0IMCpHXWL0Wr3KQNCqJix1uhMqD"
        },
        "expiredTime": 1506433269,
        "expiration": "2017-09-26T13:41:09Z"
    }
}
```

