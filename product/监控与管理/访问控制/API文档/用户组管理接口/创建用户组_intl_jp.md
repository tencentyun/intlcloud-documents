## API説明

このAPI（CreateGroup）はユーザーグループを作成するために使用されます。

リクエストドメイン名：

```
cam.api.qcloud.com
```

## 入力パラメータ

以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/6976)がリストされていません。

| パラメータ名  | タイプ   | 必須項目 | 説明       |
| --------- | ------ | ---- | ---------- |
| groupName | string | いいえ   | ユーザーグループ名   |
| remark    | string | いいえ   | ユーザーグループの説明 |

## 出力パラメータ

| パラメータ名 | タイプ | 説明 |
| -------- | ---- | ---- |
| groupId   | int | ユーザーグループID  |

## 例

### 入力

```
https://cam.api.qcloud.com/v2/index.php
?groupName=testgroupname
&remark=testre123
&SignatureMethod=HmacSHA256
&Action=CreateGroup
&Region=gz
&SecretId=AKIDWwGVed95Zu693ltdoopjcKrDct20DKky
&Nonce=38803
&Timestamp=1512702940
&RequestClient=SDK_PHP_1.1
&Signature=p4APCiYw5pHhjVk9Fwjk6U9n2%2FuTTaVGzSehd2G4YZc%3D
```

### 出力

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "groupId": 28791
    }
}
```

## エラーコード

[エラーコード](https://intl.cloud.tencent.com/document/product/598/13884)を参照してください。
