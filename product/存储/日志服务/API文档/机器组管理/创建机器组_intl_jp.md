## 機能説明

このAPIはサーバーグループを作成し、新規作成されたサーバーグループのIDを返すために使用されます。

## リクエスト

### リクエスト例

```
POST /machinegroup HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
Content-Type: application/json

{"group_name": "testname", "ips": ["10.10.10.10", "10.10.10.11"]}
```

### リクエストライン

```
POST /machinegroup
```

### リクエストヘッダー

共通ヘッダー以外に特別なリクエストヘッダーは使用されません。

### リクエストパラメータ

| フィールド名        |  タイプ  | 場所  | 必須項目 |      意味                       |
|--------------|--------|------|---------|--------------------------------|
| group_name   | string | body | はい      |サーバーグループの名、重複できません             |
| ips          | JsonArray| body| はい     |サーバーグループ下のIPリスト                  |

## 応答

### 応答例

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{"group_id": "xxxx-xx-xx-xx-xxxxxxxx"}
```

### 応答ヘッダー

共通の応答ヘッダー以外に特別な応答ヘッダーはありません。

### 応答パラメータ

|  フィールド名      |  タイプ     | 必須項目 |        意味                    |
|-------------|-----------|---------|-------------------------------|
| group_id    | string    | はい      | サーバーグループのID                  |

## エラーコード

詳細については、[エラーコード](https://cloud.tencent.com/document/product/614/12402)を参照してください。

