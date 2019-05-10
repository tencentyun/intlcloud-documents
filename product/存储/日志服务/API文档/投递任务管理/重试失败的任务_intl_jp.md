## 機能説明

このAPIは、失敗した配信タスクを再試行するために使用されます。

## リクエスト


### リクエスト例

```
PUT /task HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
Content-Type: application/json

{
  "shipper_id": "xxxxxx-xx-xx-xx-xxxxxxxx",
  "task_id": "xxxxxx-xx-xx-xx-xyyyyyyy",
}
```
### リクエストライン

```
PUT /task
```
### リクエストヘッダー

共通ヘッダー以外に特別なリクエストヘッダーは使用されません。

### リクエストパラメータ

| フィールド名        |  タイプ  | 場所  | 必須項目 |      意味                       |
|--------------|--------|------|---------|--------------------------------|
| shipper_id   | string | body | はい      |配信規則のIDです                     |
| task_id      | string | body | はい      |配信タスクのIDです                     |

## 応答

### 応答例

```
HTTP/1.1 200 OK
Content-Length: 0
```

### 応答ヘッダー

共通の応答ヘッダー以外に特別な応答ヘッダーはありません。

### 応答パラメータ

なし

## エラーコード

詳細については、[エラーコード](https://cloud.tencent.com/document/product/614/12402)を参照してください。

