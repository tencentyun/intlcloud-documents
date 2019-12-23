## API説明

このAPI（ListGroups）は、ユーザーグループリストを照合するために使用されます。

リクエストドメイン名：

```
cam.api.qcloud.com
```

## 入力パラメータ

以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/6976)がリストされていません。

| パラメータ名 | タイプ   | 必須項目 | 説明                                  |
| -------- | ------ | ---- | ------------------------------------- |
| page     | int    | いいえ   | ページ番号、デフォルト値は1で、1から200までです         |
| rp       | int    | いいえ   | 1ページの数量、デフォルト値は20で、必ず0より大きくて、200までです|
| keyword  | string | いいえ   | ユーザーグループ名によってマッチング                      |

## 出力パラメータ

| パラメータ名  | タイプ  | 説明                                                         |
| --------- | ----- | ------------------------------------------------------------ |
| totalNum  | int   | ユーザーグループの総数                                                   |
| groupInfo | array | ユーザーグループ配列、配列の各メンバーは、groupId（ユーザーグループID）、groupName（ユーザーグループ名）、createTime（ユーザーグループの作成時間）、remark（ユーザーグループの説明）フィールドを持ちます |

## 例

### 入力

```
https://cam.api.qcloud.com/v2/index.php
?rp=10
&page=1
&SignatureMethod=HmacSHA256
&Action=ListGroups
&Region=gz
&SecretId=AKIDWwGVed95Zu693ltdoopjcKrDct20DKky
&Nonce=21810
&Timestamp=1510736488
&RequestClient=SDK_PHP_1.1
&Signature=d8ZMD4byKJB0vBVqLqj0NJoyMa3c5DtFsZcbw1oLCEk%3D
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
                "groupId": 26705,
                "groupName": "ckwmwsllx",
                "channel": 3,
                "remark": "这很西游5",
                "createTime": "2017-10-23 20:49:49"
            },
            {
                "groupId": 23742,
                "groupName": "gtdx",
                "channel": 3,
                "remark": null,
                "createTime": "2017-07-24 19:42:39"
            }
        ],
        "totalNum": "2"
    }
}
```

## エラーコード

[エラーコード](https://intl.cloud.tencent.com/document/product/598/13884)を参照してください。

