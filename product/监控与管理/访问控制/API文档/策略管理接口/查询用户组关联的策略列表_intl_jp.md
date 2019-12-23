## API説明

このAPI（ListAttachedGroupPolicies）は、ユーザーグループに関連付けられているポリシーリストを照合するために使用されます。

リクエストドメイン名：

```
cam.api.qcloud.com 
```

## 入力パラメータ

以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/6976)がリストされていません。

| パラメータ名 | タイプ | 必須項目 | 説明                        |
| -------- | ---- | ---- | --------------------------- |
| groupId  | int  | はい   | ユーザーグループID                   |
| page     | int  | いいえ   | ページ番号、デフォルト値は1で、1から始まります |
| rp       | int  | いいえ   | ページサイズ、デフォルト値は20です       |

## 出力パラメータ

[ListPolicies](https://intl.cloud.tencent.com/document/product/598/15426) APIの説明を参照してください。

## 例

### 入力

```
https://cam.api.qcloud.com/v2/index.php
?groupId=34444
&page=1
&rp=20
&SignatureMethod=HmacSHA256
&Action=ListAttachedGroupPolicies
&Region=gz
&SecretId=AKIDWwGVed95Zu693ltdoopjcKrDct20DKky
&Nonce=44835
&Timestamp=1523262775
&RequestClient=SDK_PHP_1.1&
Signature=vBfc7JZiDSZZysKesDoywMN3ca80pgZmWVdiQ4QXJJg%3D
```

### 出力

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "totalNum": 1,
        "list": [
            {
                "policyId": 1,
                "policyName": "AdministratorAccess",
                "addTime": "2018-04-09 16:31:19",
                "createMode": 2
            }
        ]
    }
}
```

## エラーコード

[エラーコード](https://intl.cloud.tencent.com/document/product/598/13884)を参照してください。

