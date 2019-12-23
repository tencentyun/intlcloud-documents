## API説明

このAPI（DeleteGroup）はユーザーグループを削除するために使用できます。

リクエストドメイン名：

```
cam.api.qcloud.com
```

## 入力パラメータ

以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/6976)がリストされていません。

| パラメータ名 | タイプ | 必須項目 | 説明      |
| -------- | ---- | ---- | --------- |
| groupId  | int  | はい   | ユーザーグループID |

## 出力パラメータ
なし。

## 例

### 入力

```
https://cam.api.qcloud.com/v2/index.php
?groupId=28791
&SignatureMethod=HmacSHA256
&Action=DeleteGroup
&Region=gz
&SecretId=AKIDWwGVed95Zu693ltdoopjcKrDct20DKky
&Nonce=59745
&Timestamp=1512716474
&RequestClient=SDK_PHP_1.1
&Signature=A2IYDCP1SGf%2BDoxLDerfWxKC4XEGxAigvo0HgSZr67o%3D
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

