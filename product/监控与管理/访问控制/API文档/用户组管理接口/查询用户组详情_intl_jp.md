## API説明

このAPI（GetGroup）は、ユーザーグループの詳細情報を羅列するために使用されます。

リクエストドメイン名：

```
cam.api.qcloud.com
```

## 入力パラメータ

以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/6976)がリストされていません。

| パラメータ名 | タイプ | 必須項目 | 説明      |
| -------- | ---- | -------- | --------- |
| groupId  | int  | はい       | ユーザーグループID |

## 出力パラメータ

| パラメータ名   | タイプ   | 説明                                                         |
| ---------- | ------ | ------------------------------------------------------------ |
| groupId    | int    | ユーザーグループID                                                    |
| groupName  | string | ユーザーグループ名                                                   |
| groupNum   | int    | ユーザーグループのメンバー数                                               |
| remark     | string | ユーザーグループの説明                                                   |
| createTime | string | ユーザーグループの作成時間                                               |
| userInfo   | array  | インデックス配列。メンバーは関連配列であり、メンバーはユーザーグループに参加するユーザーを表します。メンバーフィールドuid（ユーザーグループ）、uin（サブアカウントuin）、name（サブアカウントのニックネーム） |

## 例

### 入力

```
https://cam.api.qcloud.com/v2/index.php
?groupId=28791
&SignatureMethod=HmacSHA256
&Action=GetGroup
&Region=gz
&SecretId=AKIDWwGVed95Zu693ltdoopjcKrDct20DKky
&Nonce=64065
&Timestamp=1512715507
&RequestClient=SDK_PHP_1.1
&Signature=cmXkOx7XeFtmhmaCJTUTUmKYPZ5vT4S6LjIGBnRiTL4%3D
```

### 出力

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "groupId": 28791,
        "groupName": "testgrname",
        "groupNum": 1,
        "channel": 3,
        "remark": "tee123",
        "createTime": "2017-12-08 11:15:56",
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
