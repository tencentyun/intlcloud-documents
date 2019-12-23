## API説明

このAPI（UpdateGroup）はユーザーグループをアップデートするために使用できます。

リクエストドメイン名：

```
cam.api.qcloud.com
```

## 入力パラメータ

以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/6976)がリストされていません。

| パラメータ名  | タイプ   | 必須項目 | 説明       |
| --------- | ------ | ---- | ---------- |
| groupId   | int    | はい   | ユーザーグループID  |
| groupName | string | いいえ   | ユーザーグループ名   |
| remark    | string | いいえ   | ユーザーグループの説明 |

## 出力パラメータ
なし。
## 例

### 入力

```
https://cam.api.qcloud.com/v2/index.php
?groupId=28791
&groupName=testgrname
&remark=tee123
&SignatureMethod=HmacSHA256
&Action=UpdateGroup
&Region=gz
&SecretId=AKIDWwGVed95Zu693ltdoopjcKrDct20DKky
&Nonce=52700
&Timestamp=1512703514
&RequestClient=SDK_PHP_1.1
&Signature=K0vw4YiIN%2B%2FZzl7bBVZzOm7CqIvuuOlx0ZkHMQUcnUk%3D
```

### 出力

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": []
}
```

## エラーコード

[エラーコード](https://intl.cloud.tencent.com/document/product/598/13884)を参照してください。

