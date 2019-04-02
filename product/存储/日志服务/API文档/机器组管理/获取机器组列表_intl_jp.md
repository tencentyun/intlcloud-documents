## 機能説明

このAPIは、サーバーグループ情報のリストを取得するために使用されます。

## リクエスト

### リクエスト例

```
GET /machinegroups HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>

```

### リクエストライン

```
GET /machinegroups
```

### リクエストヘッダー

共通ヘッダー以外に特別なリクエストヘッダーは使用されません。

### リクエストパラメータ

なし

## 応答

### 応答例

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
  "machine_groups": [
    {
    "group_id": "xxxx-xx-xx-xx-xxxxxxxx",
    "group_name": "testname",
    "create_time": "2017-08-08 12:12:12"
    }
  ]
]
```

### 応答ヘッダー

共通の応答ヘッダー以外に特別な応答ヘッダーはありません。

### 応答パラメータ

|  フィールド名      |  タイプ     | 必須項目 |        意味                    |
|-------------|-----------|---------|-------------------------------|
| machine_groups|JsonArray| はい      | サーバーグループ情報配列                  |

MachineGroupInfoのフォーマットは次のとおりです：

|  フィールド名     |  タイプ  | 必須項目 |        意味                    |
|------------|--------|---------|-------------------------------|
| group_id   | string | はい      | サーバーグループのID                  |
| group_name | string | はい      | サーバーグループの名前                    |
| create_time| string | いいえ      | 作成時間                       |

## エラーコード

詳細については、[エラーコード](https://cloud.tencent.com/document/product/614/12402)を参照してください。

