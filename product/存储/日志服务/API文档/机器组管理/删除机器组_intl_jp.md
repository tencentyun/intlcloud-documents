## 機能説明

このAPIは、サーバーグループを削除するために使用されます。

## リクエスト

### リクエスト例

```
DELETE /machinegroup?group_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>

```

### リクエストライン

```
DELETE /machinegroup
```

### リクエストヘッダー

共通の応答ヘッダー以外に特別な応答ヘッダーはありません。

### リクエストパラメータ

| フィールド名        |  タイプ  | 場所  | 必須項目 |      意味                       |
|--------------|--------|------|---------|--------------------------------|
| group_id     | string | query| はい      |削除するサーバーグループのID                |

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

