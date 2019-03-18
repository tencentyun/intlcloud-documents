## API説明
このAPI（GetRole）は、指定されたロールの詳細情報を取得するために使用されます。
リクエストドメイン名：cam.api.qcloud.com

## 入力パラメータ
以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/6976)がリストされていません。

|フィールド|必須項目|タイプ|説明|
| ------------ | ------------ | ------------ | ------------ |
|roleId|いいえ|string|ロールID。ロールを指定するために使用され、入力パラメータroleIdとroleNameのいずれかを選択します|
|roleName|いいえ|string|ロール名。ロールを指定するために使用され、入力パラメータroleIdとroleNameのいずれかを選択します|

## 出力パラメータ
 
| フィールド  | タイプ  | 説明  |
| ------------ | ------------ | ------------ |
|  roleId | string  | ロールID |
|  roleName | string  | ロール名 |
|  policyDocument | string  | ロール信頼ポリシー |
|  description | string  | ロールの説明 |
|  addTime | string  | ロールの作成時間 |
|  updateTime | string  | ロール最近変更された時間  |

## 例
入力
```
https://cam.api.qcloud.com/v2/index.php?Action=GetRole&roleName=testroleName323&<共通リクエストパラメータ>
```

出力
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "roleId": "4611686018427397919",
        "roleName": "testroleName323",
        "policyDocument": "{\"version\":\"2.0\",\"statement\":[{\"action\":\"name/sts:AssumeRole\",\"effect\":\"allow\",\"principal\":{\"qcs\":[\"qcs::cam::uin/2385420691:root\"]}}]}",
        "description": "",
        "addTime": "2017-09-26 11:02:21",
        "updateTime": "2017-09-26 11:02:21"
    }
}

````

