## API説明

このAPI（ListUsersForGroup）は、ユーザーグループに関連付けられているユーザーリストを照合するために使用されます。

リクエストドメイン名：

```
cam.api.qcloud.com
```

## 入力パラメータ

以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/6976)がリストされていません。

| パラメータ名 | タイプ | 必須項目 | 説明                                  |
| -------- | ---- | ---- | ------------------------------------- |
| page     | int  | いいえ   | ページ番号、デフォルト値は1で、1から200までです         |
| rp       | int  | いいえ   | 1ページの数量、デフォルト値は20で、必ず0より大きくて、200 までです|
| groupId  | int  | はい   | ユーザーグループID                             |

## 出力パラメータ

| パラメータ名 | タイプ  | 説明                                                         |
| -------- | ----- | ------------------------------------------------------------ |
| totalNum | int   | ユーザーグループに関連付けられているユーザーの総数                                         |
| userInfo | array | ユーザー配列、配列の各メンバーは、uid（ユーザーID）、uin（ユーザーuin）、name（ユーザー名）、createTime（作成時間）、isReceiverOwner（メインアカウントかどうか）などのフィールドを持ちます |

## 例

### 入力

```
https://cam.api.qcloud.com/v2/index.php
?rp=10
&page=1
&groupId=23742
&SignatureMethod=HmacSHA256
&Action=ListUsersForGroup
&Region=gz
&SecretId=AKIDWwGVed95Zu693ltdoopjcKrDct20DKky
&Nonce=53463
&Timestamp=1510737439
&RequestClient=SDK_PHP_1.1
&Signature=43rnmIrGF64te4WuPdWgBDdHPRAU1CsuF19WUR8dxVc%3D
```

### 出力

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "groupInfo": [],
        "totalNum": "1",
        "userInfo": [
            {
                "uid": 1133398,
                "uin": 3449203261,
                "name": "test1",
                "phoneNum": "13631422209",
                "countryCode": "86",
                "phoneFlag": 0,
                "email": "2385420691@qq.com",
                "emailFlag": 0,
                "userType": 3,
                "createTime": "2017-09-04 16:40:15",
                "isReceiverOwner": 0
            }
        ]
    }
}
```

## エラーコード

[エラーコード](https://intl.cloud.tencent.com/document/product/598/13884)を参照してください。

