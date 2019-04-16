## API説明
このAPI（DetachRolePolicy）はロールのポリシーをバインディング解除するために使用されます。
リクエストドメイン名：cam.api.qcloud.com

## 入力パラメータ
以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/6976)がリストされていません。

|フィールド|必須項目|タイプ|説明|
| ------------ | ------------ | ------------ | ------------ |
|policyId|いいえ|int|ポリシーID、入力パラメータpolicyIdとpolicyNameのいずれかを選択します|
|policyName|いいえ|string|ポリシー名、入力パラメータpolicyIdとpolicyNameのいずれかを選択します|
|roleId|いいえ|string|ロールID。ロールを指定するために使用され、入力パラメータroleIdとroleNameのいずれかを選択します|
|roleName|いいえ|string|ロール名。ロールを指定するために使用され、入力パラメータroleIdとroleNameのいずれかを選択します|

## 出力パラメータ

| フィールド  | タイプ  | 説明  |
| ------------ | ------------ | ------------ |
| code | Int | 共通エラーコード、0は成功、他の値は失敗を意味します。詳細については、エラーコードページの<a href='https://cloud.tencent.com/doc/api/372/%E9%94%99%E8%AF%AF%E7%A0%81#1.E3.80.81.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81' title='公共错误码'>共通エラーコード</a>を参照してください。|
| message | String | APIに関連するモジュールエラーメッセージの説明。|
| codeDesc | String | 英語のエラー説明 |

## 例 
入力
```
https://cam.api.qcloud.com/v2/index.php?Action=DetachRolePolicy&policyId=296232
&roleId=4611686018427397919&<共通リクエストパラメータ>
```

出力
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": []
}

````
