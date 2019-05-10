## 機能説明

このAPIはログセットを作成し、新規作成されたログセットのIDを返すために使用されます。

## リクエスト

### リクエスト例

```
POST /logset HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
Content-Type: application/json

{"logset_name": "testname","period": 15}
```

### リクエストライン

```
POST /logset
```

### リクエストヘッダー

共通の応答ヘッダー以外に特別な応答ヘッダーはありません。

### リクエストパラメータ

| フィールド名        |  タイプ  | 場所  | 必須項目 |      意味                       |
|--------------|--------|------|---------|--------------------------------|
| logset_name  | string | body | はい      |ログセットの名、重複できません             |
| period       | int    | body | はい      |ログセットの保存期間、単位は日、最大は90日    |

## 応答

### 応答例

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{"logset_id": "xxxx-xx-xx-xx-xxxxxxxx"}
```

### 応答ヘッダー

共通の応答ヘッダー以外に特別な応答ヘッダーはありません。

### 応答パラメータ

|  フィールド名      |  タイプ     | 必須項目 |        意味                    |
|-------------|-----------|---------|-------------------------------|
| logset_id   | string    | はい      | ログセットのID                  |

## エラーコード

詳細については、[エラーコード](https://cloud.tencent.com/document/product/614/12402)を参照してください。

