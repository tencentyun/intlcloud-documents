## API説明
このAPI（CreateRole）はロールを作成するために使用されます。
リクエストドメイン名：cam.api.qcloud.com

## 入力パラメータ
以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/6976)がリストされていません。

|フィールド|必須項目|タイプ|説明|
| ------------ | ------------ | ------------ | ------------ |
|policyDocument|はい|string|ロールの信頼ポリシー|
|description|いいえ|string|ロールの説明|
|roleName|はい|string|ロール名|

## 出力パラメータ
 
| フィールド  | タイプ  | 説明  |
| ------------ | ------------ | ------------ |
|  roleId | string  | ロールID |

## 例
入力
```
https://cam.api.qcloud.com/v2/index.php?Action=CreateRole&roleName=testroleName
&policyDocument=%7B%22version%22%3A%222.0%22%2C%22statement%22%3A%5B%7B%22action%22%3A%22name%2Fsts%3AAssumeRole%22%2C%22effect%22%3A%22allow%22%2C%22principal%22%3A%7B%22qcs%22%3A%5B%22qcs%3A%3Acam%3A%3Auin%12345678%3Aroot%22%5D%7D%7D%5D%7D&<共通リクエストパラメータ>
```
policyDocumentフィールド値は次のとおりです。 
{"version":"2.0","statement":[{"action":"name/sts:AssumeRole","effect":"allow","principal":{"qcs":["qcs::cam::uin/12345678:root"]}}]}

出力
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "roleId": "4611686018427397919"
    }
}

````

