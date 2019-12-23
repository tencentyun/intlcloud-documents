## API説明

このAPI（ListAttachedRolePolicies）は、ロールにバインディングされているポリシーのリストを取得するために使用されます。
リクエストドメイン名：

```
cam.api.qcloud.com
```

## 入力パラメータ

以下のリクエストパラメーターリストにはAPIリクエストパラメータのみがリストされ、[共通リクエストパラメータ](https://cloud.tencent.com/document/api/213/6976)がリストされていません。

| パラメータ名   | タイプ   | 必須項目 | 説明                                                         |
| ---------- | ------ | ---- | ------------------------------------------------------------ |
| roleId     | string | いいえ   | ロールID。ロールを指定するために使用され、入力パラメータroleIdとroleNameのいずれかを選択します        |
| roleName   | string | いいえ   | ロール名。ロールを指定するために使用され、入力パラメータroleIdとroleNameのいずれかを選択します         |
| page       | int    | いいえ   | ページ番号、1から始まります。デフォルト値は1です                                  |
| rp         | int    | いいえ   | ページサイズ。デフォルト値は20です                                        |
| policyType | string | いいえ   | User値はカスタムポリシーのみ、QCSはプリセットポリシーのみ、入力しない場合は関連付けられているすべてのポリシーが照合されることを意味します |

## 出力パラメータ

| フィールド     | タイプ  | 説明                                                         |
| -------- | ----- | ------------------------------------------------------------ |
| totalNum | int   | ポリシーの総数                                                     |
| list     | array | ポリシー配列。配列の各メンバーには以下のフィールドが含まれます。<li>policyId：ポリシーID<li>policyName：ポリシー名<li>addTime：ポリシーの作成時間<li>description：ポリシーの説明<li> createMode：1はビジネス権限によって作成されたポリシーを表し、その他の値はポリシー構文を確認でき、ポリシー構文によってポリシーをアップデートすることを示します|

## 例
### 入力
```
https://cam.api.qcloud.com/v2/index.php
?roleName=testRole
&page=1
&rp=20
&SignatureMethod=HmacSHA256
&Action=ListAttachedRolePolicies
&Region=gz
&SecretId=AKIDWwGVed95Zu693ltdoopjcKrDct20DKky
&Nonce=33994
&Timestamp=1508492653
&RequestClient=SDK_PHP_1.1
&Signature=YQflvL9ZCPDfTJNum84oXRQex6iKKTNi2fwgLUh2qZE%3D
```

### 出力

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "totalNum": 3,
        "list": [
            {
                "policyId": 524497,
                "policyName": "testpppName323",
                "addTime": "2017-10-20 17:26:16",
                "policyType": "User",
                "createMode": 2
            },
            {
                "policyId": 296232,
                "policyName": "QcloudCCSInnerFullAccess",
                "addTime": "2017-10-20 17:11:19",
                "policyType": "QCS",
                "createMode": 2
            },
            {
                "policyId": 219851,
                "policyName": "QcloudCLBReadOnlyAccess",
                "addTime": "2017-09-04 16:40:15",
                "policyType": "QCS",
                "createMode": 2
            }
        ]
    }
}
```

## エラーコード
[エラーコード](https://intl.cloud.tencent.com/document/product/598/13884)を参照してください。
