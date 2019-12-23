## API説明

このAPI（ListGroupsForUser）は、ユーザーに関連付けられているユーザーグループを羅列するために使用されます。

リクエストドメイン名：

```
cam.api.qcloud.com
```

## 入力パラメータ

以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/6976)がリストされていません。

| パラメータ名 | タイプ | 必須項目 | 説明                                  |
| -------- | ---- | -------- | ------------------------------------- |
| page     | int  | いいえ       | ページ番号、デフォルト値は1で、1から200までです         |
| rp       | int  | いいえ       | 1ページの数量、デフォルト値は20で、必ず0より大きくて、200までです|
| uid      | int  | はい       | ユーザーID                               |

## 出力パラメータ

| パラメータ名  | タイプ  | 説明                                                         |
| --------- | ----- | ------------------------------------------------------------ |
| totalNum  | int   | ユーザーが参加しているユーザーグループの総数                                                   |
| groupInfo | array | ユーザーグループ配列、配列の各メンバーは、groupId（ユーザーグループID）、groupName（ユーザーグループ名）、remark（ユーザーグループの説明）フィールドを持ちます |

## 例

### 入力

```
https://cam.api.qcloud.com/v2/index.php
?rp=10
&page=1
&uid=1133398
&SignatureMethod=HmacSHA256
&Action=ListGroupsForUser
&Region=gz
&SecretId=AKIDWwGVed95Zu693ltdoopjcKrDct20DKky
&Nonce=23509
&Timestamp=1512716160
&RequestClient=SDK_PHP_1.1
&Signature=PsukZTcNW5Ev2%2FY%2F6QBBpu1DntyI4VMFu6PywZQQ5Ww%3D
```

### 出力

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "groupInfo": [
            {
                "groupId": 28791,
                "groupName": "testgrname",
                "remark": "tee123"
            }
        ],
        "totalNum": "1"
    }
}
```

## エラーコード

[エラーコード](https://intl.cloud.tencent.com/document/product/598/13884)を参照してください。

