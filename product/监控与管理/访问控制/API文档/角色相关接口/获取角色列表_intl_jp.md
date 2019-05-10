__1. API説明__ 
このAPI（DescribeRoleList）は、指定されたロールの詳細情報を取得するために使用されます。
リクエストドメイン名：cam.api.qcloud.com

__2. 入力パラメータ__ 
以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/6976)がリストされていません。

|フィールド|必須項目|タイプ|説明|
| ------------ | ------------ | ------------ | ------------ |
|page|はい|int|ページ番号、1から始まります|
|rp|はい|int|ページサイズ、200を超えてはいけません|


 __3. 出力パラメータ__ 

| フィールド  | タイプ  | 説明  |
| ------------ | ------------ | ------------ |
|  totalNum | int  | このownerのロールの総数 |
|  list | array  | ロールリスト |

listフィールドの各ロールには、以下の情報が表示されます 
 
| フィールド  | タイプ  | 説明  |
| ------------ | ------------ | ------------ |
|  roleId | string  | ロールID |
|  roleName | string  | ロール名 |
|  policyDocument | string  | ロール信頼ポリシー |
|  description | string  | ロールの説明 |
|  addTime | string  | ロールの作成時間 |
|  updateTime | string  | ロール最近変更された時間  |


 __4. 例__  
入力
```
https://cam.api.qcloud.com/v2/index.php?Action=DescribeRoleList&page=1&rp=10&<共通リクエストパラメータ>
```

出力
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "totalNum": 2,
        "list": [
            {
                "roleId": "4611686018427397919",
                "roleName": "testroleName001",
                "policyDocument": "{\"version\":\"2.0\",\"statement\":[{\"action\":\"name/sts:AssumeRole\",\"effect\":\"allow\",\"principal\":{\"qcs\":[\"qcs::cam::uin/888888888:root\"]}}]}",
                "description": "",
                "addTime": "2017-09-26 11:02:21",
                "updateTime": "2017-09-26 11:02:21"
            },
            {
                "roleId": "4611686018427397919",
                "roleName": "testroleName002",
                "policyDocument": "{\"version\":\"2.0\",\"statement\":[{\"action\":\"name/sts:AssumeRole\",\"effect\":\"allow\",\"principal\":{\"qcs\":[\"qcs::cam::uin/12345678:root\"]}}]}",
                "description": "",
                "addTime": "2017-09-25 15:19:29",
                "updateTime": "2017-09-25 15:19:29"
            }
        ]
    }
}
````

